# AngularJS

> * `sudo npm install -g grunt-cli`
> * `npm install`
> * `grunt webserver`

Add npm modules to the *PATH*
> * `export PATH="/usr/local/Cellar/node/5.2.0/lib/node_modules/grunt/bin:$PATH"`

## bower install

> * `sudo npm install -g bower`

Add npm modules to the *PATH*
> * `export PATH="/usr/local/Cellar/node/5.2.0/lib/node_modules/bower/bin:$PATH"`
> 
> * `bower install angular`
> * `bower install jquery`

Bower Package 등록도 가능
> * `bower init`

## Angular-seed 클론을 이용한 프로젝트 구성

> * `git clone git://github.com/angular-seed.git`

**ADM (Asynchronouse Module Difinition)**

테스트 환경과 node.js 서버 환경을 위해서 node.js와 karma를 설치한다.

> * `npm install -g karma`
> * `npm run start`
 
 
## AngularJS 주요기능

* 양방향 데이터 바인딩
* MVC 구조
* 지시자(directive)를 이용한 HTML 확장
* 의존관계 주입(Dependency Injection)
* 단일 페이지 웹 애플리케이션을 위한 라우터(Router)
* $q를 이용한 자바스크립트 비동기 지원
* 자바스크립트 테스팅 지원


## The Zen of Angular

AngularJS는 UI를 만들고 소프트웨어 컴포넌트들을 서로 엮는 것에는 선언적 코드가 명령적 코드보다 더 좋다는 믿음에서 만들어졌다. 물론 비즈니스 로직을 표현하는데는 명령적 코드가 더 좋다.

> * 애플리케이션 로직으로부터 DOM 조작을 분리하는 것은 매우 좋은 생각이다. 이는 코드의 테스트 가능성을 매우 향상시킨다.
> * 애플리케이션 테스팅이 애플리케이션 작성만크 중요하다고 여기는 것은 매우 중요한다. 테스팅 어려움의 정도는 코드가 어떻게 구조적으로 만들어졌는가에 직접적으로 영향을 받는다.
> * 클라이언트 쪽의 애플리케이션과 서버 쪽을 분리하는 것은 훌륭한 생각이다. 이는 동시에 양쪽에서 개발할 수 있게 하며 양쪽 모두 재사용할 수 있게 한다.
> * 프레임워크가 개발자로 하여금 애플리케이션 개발에 있어서 처음부터 끝까지 전체적으로 가이드하는 것은 매우 유용하다. 처음부터 끝이라 함은 UI를 디자인하는 것부터 비즈니스 로직 개발을 거쳐 테스튺지를 말한다.
> * 애플리케이션의 공통적은 일을 신경 쓰지 않게 하고 어려운 일을 가능케 하는 것은 항상 좋은 일이다. 