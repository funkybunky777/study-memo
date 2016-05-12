# 오픈소스 소프트웨어와 보안

# Netty로 알아보는 오픈 소스 프로젝트 운영 - 이희승 (라이플러스)

## Netty

* 자바 프레임워크
* 클라이언트, 서버 소켓 개발을 쉽고 빠르게
* 빠르지만 유지보수 가능하게 
* 비동기
* 이벤트 기반

## 사용 분야

* 웹 서비스 
* 인스턴트 메시징
* 멀티플레이어 게임
* 스토리지, 데이터베이스
* 고빈도 거래
* 미디어 스트리밍


# 오픈소스 대상 고성능 정적 분석 기술 - 오학주 교수님

## **Sparrow**

* Aims to detect memory errors in C programs
	* e.g., buffer-overrun, memory leak, null-dereference, etc
* Features (vs. testing)

## Static Program Analysis

* Predict SW behavior statically and automaticaly
	* static: before execution, before sell / embed
	* automatic: sw is analyzed by sw ("static analyzers") 
* Applications
	* bug-finding. e.g., find runtie failures of programs
	* security. e.g., is this app malicious or benign?
	* verification e.g., does the program meet its specification?
	* compiler optimization, e.g., automatic parallelization
	
## 정적 분석기의 유용성
* Soundness : Find all bugs / verify absence
	* **Sound**
	* Program States와 error status가 Disjoint 함을 증명
	* Program statues를 Over Approximation을 하면 간접적으로 증명한다.
	* 이것이 증명된다면 Sound 하다고 한다.
	* vs
* Precision : Few false alarms
	* **imprecise**
	* Programs states를 너무 크게 Abstraction하여 False Alarm이 생김
	* 실제 오류가 발생하지 않았는데 발생했다고 판별
	* 이론적으로는 False Alarm이 거의 없도록 할 수 있음
* Scalability : Large programs
	* 수 많은 라인 분석이 가능해야 한다.

* Verifiers : Soundness + Precision
* bug-finders : Scalability + Precision
* Optimizers : Soundness + Scalability


* Research Goal
	* Soundness : Abstract Interpretation Framework
	* Scalability : General Sparse Analysis Framework
	* Precision : Selective X-Sensitivity Approach


## Learning-based Approach

* Parameterized adaptation strategy
	* S(w) : pgm -> 2**(Var)
	* P1, P2, ..., Pm(Code base) => W

1. Represent Program variables as feature vectors.
2. Compute the score of each variable(외적)
3. Choose the top-k variables based on the score.

(1) FEATURES

* Predicates over varables: f = {f1, f2,..., f45}

## Bayesian Optimization

Sampling 할 때 다음 Value를 예측

## 코드 영역별로 Power Consumption 명시 가능



# Software Weakness

1. **보안약점**이란, 소프트웨어 내에 있는 소프투에어 구현, 코딩, 설계, 구조에 내포된 Bug, Flaw, fault, error, mistake

# 취약점 보완
## Secure Coding

MIRSA-C: 2012 Amendment 1

## 정적분석도구 활용
* 시큐어 코딩으로 해결안되고 남아 있는 보안약점을 제거
* 취약점/ 제로데이 취약점/ 미래의 취약점 예방
* PolySpace, Fortify, Sparrow, SecurityPrism, Coverity, AppScan

## 시큐어 디자인
* 마이크로소프트 : 위협모델링
* OWASP : 리스크 분석(위험 분석)
* 현재 58% 사이버 공격이 설계 보안약점을 악용

## 시큐어 소프트웨어 개발 방법론 (Secure Software Development Life Cycle, S-SDLC) 활용
* 소프트웨어 개발 전 단계에서 보안 요소 적용
* 마이크로소프트사의 SLC (Security Development Lifecycle)
* 국토안보부의 S-SDLC, 7 touch


### MS TCI의 SDL 특징
1. 프로젝트 개시 전에 항상 보안 관련 교육을 실시한다.
2. 품질 버그 바 정의 및 보안/개인정보 위험 분석
3. 공격 면 분석 및 위협 모델링
4. 정적분석 도구 결정, 사용 금지된 함수 사용 금지, 정적 분석 실시
5. 동적/퍼즈 테스팅 실시 및 위협모델/공격 면 검증
6. 배포 및 대응


## 오픈소스 SW 보증
* 자체 개발 코드 보다 제 3자 코드, 공개코드, 라이브러리의 활용이 점차 늘어나고 있음
* 공개 소프트웨어에 취약점이 없다는 것을 어떻게 확인/보증 할 것인가?

## 소프트웨어 신뢰성 vs. 보안성

* 100% 신뢰할 수 있는 소프트웨어도 보안성이 없을 수 있음 (명세와 설계에도 오류가 없어도)
	* 소프트웨어의 신뢰성과 보안성은 전혀 다른 속성임

* 신뢰성 테스트와 보안성 테스트는 입력이 다름
	* 신뢰성 테스트 : 명세에서 정의된 범위의 입력 
	* 보안성 테스트 : 명세에서 정의가 안된 범위의 입력

	
## 보안을 위한 테스팅 기법

* 동적 테스트
	* Pen 테스트, 침투 시험
	* Fuzzing (퍼징)

* 정적 테스트 (Static Code Analysis)
	* 변수의 범위에 상관없는 분석
	* 찾은 보안약점이 취약점인지 확인이 필요(취약점이 아니면 False alarm)

	
# 소프트웨어 보증 (Software Assurance, SwA)

* Software Quality/Safety Assurance + Software Security Assurance 
* CNSS IA 


# Software Assurance Level

1. EAL1 : Functionally tested
2. EAL2 : Structurally tested 
--- 정적분석 도구
3. EAL3 : Methodically tested and checked
4. EAL4 : Methodically designed, tested and reviewed
5. EAL5 : Semi-formally designed and tested
6. EAL6 : Semi-formally verifed, designed and tesed
7. EAL7 : Formally verified, designed and tested

# 결론
* OSS 신뢰성 확보/보증을 위한 방안이 필요
	* OSS 개발자/개발 조직의 인식 재고
	* 동적/정적 테스팅으로는 중간 등급 정도의 신뢰성 확보
	* 최상위 등급 신뢰성을 확봏기 위한 방안이 필요
	* 대형 오픈소스 소프트웨어와 소형 오픈소스 소프트웨어의 보증 방안
	