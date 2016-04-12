# 서비스 확장 전략


## 개념 설명

### 웹 서비스 아키텍처

Client - Buisness Logic - Storage

**장애를 대비하자면?**

1. 웹 서버 장애
	* API 서버 다운
	* API 서버를 여러대를 놓는다.
	* Load Balancer
2. 디비 서버 장애
	* 서비스가 되지 않는다.
	* 대비 : Master - Slave(장애 대비 - Replication Failover)
	* Read가 많으면? - Slave를 Read로 쓴다. 
		* Replication Lack 발생
		* I/O는 한정되어 있으므로 Write가 증가하면 Read 속도가 감소한다.
		* -> Write도 분산해야함
		* "샤딩", "클러스터링 "
	* 클라스터링 
		* 솔루션에서 데이터의 분배나 이동을 알아서 해주는 경우
		* 각 노드들끼리 정보를 주고 받아서 유지
		* 솔루션에서 알아서 해당 정보를 저장하고 찾을 수 있게
	* 샤딩 (더 일반적)
		* API 서버에서 씨스템에 정의된 룰에 따라서, 데이터를 각기 다른 데이터 서버로 분배하는 방법
			* 유저 1번은 1번 서버
			* 유저 2번은 2번 서버
		* 각 데이터 서버들은 서로 연관이 없음 Shared Northing
		* 정의된 룰에 의해서 데이터를 찾을 수 있다. 
	
> **SPOF** : Single Point of Failure. 죽으면 전체 서비스가 동작하지 않는 부분 -> SPOF 제거! 

확장은 SPOF를 제거할 수 있는 형태로 서비스를 확장해야한다.


### API 서버의 확장이 필요한 경우
* Stateless 한 경우
* CPU 연산이 많이 필요한 경우

### DB 서버의 확장이 필요한 경우
* 해당 서버의 리소스 부족
	* CPU
	* Memory
	* Disk IO
	* 저장공간
* 디비 서버의 확장은 일반적으로는 API 서버의 확장보다 많이 어려움

## 확장의 방법

**샤딩의 방법**

Range

	* Range에 따라서 서버를 분배
	* Range가 너무 크면 서버별 사용 리소스의 차이가 크게 남 -> 노는 서버와 바쁜 서버가 생김
	* Range를 작게 유지하면서 뒤의 Indexed와 연결되면 유리함	
Modular

	* ID % 서버대수로 서버가 정해짐
	* Logical Shard/Physical Shard 방법을 유지함으로써, 단순 Modular의 방식을 개선할 수 있다.
	
Indexed
	
	* 해당 서버가 어디에 존재하는지 Index 서버를 둠
	* Index 변경으로 특정 데이터의 이동이 가능하도록 할 수 있다.
	* Index 서버에 대한 관리가 필요(HA/Failover 등)
	
	

## 데이터 저장

서비스의 확장은 데이터 확장의 이슈

** 키 설계를 어떻게 할 것인가 **
키만 보고 어떤 서버에서 찾아야 할지 알 수 있을까?

Pinterest ID Structure<br/>
64bit<br/>
Shard ID | Type | Local ID

Twitter ID
64bit<br/>
Timestamp(45) | DatacenterId(5) | WorkerID(5) | sequence

> 변화하지 않을 특별한 정보가 있다면 ID에 들어가 있으면 좋다



## 클라우드
* 하루에 서비스 트래픽의 변화가 많은가?
	* 보통 새벽 2시부터 7시 정도까지는 국내 서비스는 트래픽이 적음
	* 보통 서버는 하루 최대 트래픽을 견딜 수 있는 수준으로 있어야 한다.
* 전체 서비스 트래픽의 변화가 많은가?
	* 모바일 게임이라면? 2주 뒤에 살아있다는 보장이 없다.

### 클라우드 장점
* 이제 IaaS 만 있던 시기가 아니다.
* 많은 개발 편의성을 제공한다.
	* AWS S2, AWS lambda, AWS SqS, AWS SNS, Spot, Route53
* Time to market

### 클라우드 단점
* 일단 돈이 많이 든다.
* 좋은 기술을 쓰면 Lock In....
	
	
> Transcoder가 모자라면 쉽게 추가 가능. Spot을 쓰면 더 싸다.

## 설치 & 배포

Capistrano, Ansible, Chef, Puppet

* 실수를 줄이기 위해서 사용한다.
* 생산성을 높여준다.
* 한 대, 두 대 일때도 필요함!!

**롤백도 쉬워야 함**

**만약을 위해 사용하는 라이브러리들의 Local Repo를 가지고 있는게 좋음**

##모니터링은 개발만큼 중요하다

** 무엇을 모니터링 해야하는가? **

* 서버당 기본적인 항목들
	* CPU Usage, Load
	* Memory Usage
	* Disk IO, Usage
	* Network Input/Output
* API Request 수
	* 평균 응답 속도
* 로그 사이즈
* 서비스 특화 리소스

** 꼭 해야한다 **

### 모니터링 툴
* Cacti
* Nagios
* New relic
* Netdata

**서비스가 제대로 동작하는가에 대한 모니터링 지표를 찾아야함**

**에러를 개발자에게 전달해주는 도구도 필요**

> Failover도 모니터링에서 시작
> 


## 로그
** 어떤 내용을 보기 위해 어떤 형식으로 남길지 고민해야 함 **

* TSV or CSV or JSON
	* 확장을 생각하면 JSON

* 툴
	* Logstash
	* Fluentd
	* Kafka 
	
* 사례
	* 쿠키런, Devsisters "AWS를 활용하여 Daily Report 만들기" of Slide Share
	* woonga of slide share


## 테스트

### Unit Test + API Test

* API 레벨의 테스트를 수행
* 하나의 미니 서비스를 테스트용으로 구축
	* Jenkins에서 자동으로 필요한 컴포넌트를 모두 실행
	* 실제 API를 유저 생성부터, 글 생성 까지 호출하여 실제 데이터가 의도한대로 남아있는지 확인
	* 성능 테스트로는 부족함 -> 부하 테스트를 따로 해야함
	* 스토리에는 대략 2000개의 API 테스트가 존재
* COmmit 이 발생하면 자동으로 테스트 수행
* Develop/Master 두 개의 브랜치에 대해서 자동으로 수행
* API 레벨 테스트이므로, 언어의 변경등에 상관없이 그대로 사용 가능함


> 테스트 안 깨졌다고 버그 없는건 아니다. <br/>
> 테스트 깨지면 무조건 버그난다. <br/>
> - regression test



## Q&A

1. 모든 기능을 서버에서 컨트롤 할 수 있도록 해야한다.
	* Flag를 만들어서 클라이언트의 기능을 제한할 수 있도록 한다.
	* 처음에 클라이언트가 서버에서 환경설정을 받아갈 수 있도록 하면 클라이언트가 기능을 조절을 할 수 있도록 한다.
	
2. DB가 나눠지면 Join을 못하기 때문에 APP에서 JOIN을 한다.
	* DB의 부하와 APP의 부하가 높고 낮은 경우를 구분한다.
	* DB에서 JOIN을 쓰지는 않고 Cache로 많이 사용한다.
		* > 캐시(Cache)빨
		
3. 세션을 쓰지 않고 토큰을 쓴다. 토큰에 사용자 정보, 유효성 검사를 한다. 글로벌 서비스 대부분 그렇게 한다.
 

