# AWS DDoS Defense Guide 

[https://d0.awsstatic.com/International/ko_KR/whitepapers/DDoS_Whitepaper.pdf](https://d0.awsstatic.com/International/ko_KR/whitepapers/DDoS_Whitepaper.pdf)


# Python Security

OWASP python security : [http://www.pythonsecurity.org/](http://www.pythonsecurity.org/)


# Ubuntu Security

Initial Server Setup with Ubuntu 14.04 : [https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-14-04](https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-14-04)

Additional Recommended Steps for New Ubuntu 14.04 Server : [https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-14-04](https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-14-04)


# Security Testing

## MetaSploit

**메타스플로잇**은 오픈소스 도구로, 공격 코드, 페이로드 인코더, 정찰 도구, 보안 테스팅 등을 제공하는 일종의 체계

### 특징
* 공개된 공격 코드 정리/검증으로 시간 단축
* 여러 플랫폼에서 사용 가능
* 취약점 빠르게 최신화
* 취약점에 대한 쉡코드 제공

### 프레임워크
![image](http://cfile4.uf.tistory.com/image/2445C44C52230A9935947A)

### 용어

1. Exploit
	* 익스플로잇은 공격자 또는 모의해킹 테스터가 시스템 응용프로그램, 서비스 내의 결함을 찾는데에 유익한 수단이 된다.
	* 공격자는 결코 개발자가 의도하지 않은 산출물 안의 결과들에서 시스템을 공격하는 한 방법으로 익스플로잇을 사용한다.
	* 일반적인 익스플로잇은 버퍼 오버플로우, 웹 어플리케이션 취약점, 그리고 설정 에러 등을 모두 포함한다.

2. Payoad
	* 페이로드는 프레임워크에 의해 선택되고 전송되어 실행되길 원하는 시스템의 코드이다
	* Reverse shell 은 windows command prompt를 통해 타겟 마신이 공격자로 연결을 생성하도록 하는 payload이다.
	* 페이로드는 공격대상인 운영시스템에서 수행될 몇몇 명령어들을 심플하게 해놓은 것일 수 있다.

3. Shell code
	* 쉡 코드는 Exploitation을 할 때 페이로드에 사용되어지는 명령의 한 묶음
	* 쉘 코드는 전통적으로 어셈블리어로 가성

4. Module
	* 모듈은 MetaSploit Framework에 의해 사용될 수 있는 소프트웨어의 한 부분 (예 : 스캐닝 모듈)

5. Listener
	* 리스너는 어떤 종류의 연결을 대기하는 메타스플로잇 안의 구성요소이다
	* 리스너 핸들은 익스플로잇 시스템에 의해 접근이 될 공격 머신을 기다린다.

6. MetaSploit Interface
	* 메타스플로잇 인터페이스는 콘솔, cmd 그리고 그래픽 유저 인터페이스를 포함한ㄷ.

7. MSFConsole
	* msfconsole은 프레임워크안에서 이용가능한 거의 모든 설정과 옵션을 제공하는 툴이다.

8. LHost(Local Host), LPort(Local Port)
	* Lhost : 공격자의 IP 주소
	* LPort : 공격자의 포트

9. RHost(Remote Host), RPort(Remote Port)
	* RHost : 피해자의 IP 주소
	* RPort : 피해자의 포트


