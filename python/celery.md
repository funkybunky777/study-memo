# CELERY

## CELERY + FLASK-SOCKETIO

Flask-socketio를 사용할 때 서버에서 Socket으로 Emit하는 delay로 인해 Response Time이 길어지는 현상을 막기위해 비동기 처리를 해야할 경우가 많다.

Celery는 Flask와 다른 프로세스에서 실해되기 때문에 Client로 Emit을 하기 위해 리소스를 공유해야 한다. Redis를 message_queue로 사용하여 이를 구현할 수 있다. 


* ` socketio = SocketIO(app, message_queue=app.config['SOCKETIO_REDIS_URL'], async_mode=async_mode, ping_timeout=15)`

Celery에서 다음과 같이 새로 SocketIO 객체를 만들어야 하는데, app을 넣지 말고 message_queue를 공유하도록 한다.
 
* `local_socketio = SocketIO(message_queue=app.config['SOCKETIO_REDIS_URL'])`

위와 같이 처리하면 Flask와 Celery에서 rooms을 공유하여 socket emit을 할 수 있다.

다만 나는 바보같은 실수로 하루종일 시간을 낭비하였는데, socketio Initialize를 할 때에 SocketIO() 생성자로 만들어놓고 init_app(app)을 다시 하여 중복 초기화되어 rooms 공유가 안됐다. 아래와 같이 구현하여 정상적으로 작동하지 않았었다.

* `socketio = SocketIO(app, message_queue=app.config['SOCKETIO_REDIS_URL'], async_mode=async_mode, ping_timeout=15)`

* `socketio.init_app(app)`

init_app을 통해 선언 이후에 초기화 해야한다면, 아래와 같이 구현해도 정상적으로 작동한다.

* `socketio = SocketIO(async_mode=async_mode, ping_timeout=15)`

* `socketio.init_app(app, message_queue=app.config['SOCKETIO_REDIS_URL'])`