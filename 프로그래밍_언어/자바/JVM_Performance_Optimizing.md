# Java Virtual Machine Performance Optimizing 및 성능분석 사례

## JVM Internal 파헤치기
### JVM 메모리 구조
#### JVM이란?
* JVM은 정의된 스펙을 구현한 하나의 독자적인 프로세스 형태로 구동되는 Runtime Instance
* Java에서 프로그램을 실행한다는 것은 컴파일 과정을 통하여 생성된 Class 파일을 JVM으로 로딩하고 ByteCode를 해석(interpret)하는 과정을 거쳐 메모리 등의 리소스를 할당하고 관리하며 정보를 처리하는 일련의 작업들을 포함
* JVM은 Thread 관리 및 Garbage Collection과 같은 메모리 정리 작업도 수행
* JVM상에서 Class Loader를 통해 Class 파일들을 로딩시키고, 로딩된 Class 파일들은 Execute Engine을 통해 해석
* 해석된 프로그램은 Runtime Data Areas에 배치되어 실직적인 수행이 이루어짐
![Java 프로그램 수행과정](http://d2.naver.com/content/images/2015/06/helloworld-1230-1.png)
#### Java Heap
##### Hotspot JVM의 Heap 구조
##### IBM JVM의 Heap 구조
### Garbage Collection
#### GC 소개
##### GC 개요
##### GC로 인한 문제점
##### Root Set과 Garbage
##### Garbage Collection 목적
#### Hotspot JVM의 Garbage Collection
##### 개요
##### GC 대상 및 범위
##### GC 관련 옵션들
##### Garbage Collector 종류
#### IBM JVM의 Garbage Collection
##### Garbage Collection 단계
##### Garbage Collector 종류
##### IBM JVM 환경의 Memory Leak 유형
##### 결론
#### GC 튜닝
##### GC 튜닝 필요성
##### GC 튜닝 목적
##### Object 수 최소화의 중요성(Between Eden and Old Area)
##### Full GC Time 줄이기
##### GC의 성능을 결정하는 옵션
##### GC 튜닝 과정
##### 일반적으로 GC 튜닝이 불필요 한 상황
##### GC 방식 선택
##### Memory 크기와 GC 상관 관계
#### GC 성능 테스트
##### 개요
##### Case 1
##### Case 2 / Case 2-1
##### Case 3
##### Case 4
##### 결론
#### GC 관련 장애 발생 유형(OOME) 및 분석 방법
##### OOME의 종류
##### OOME 발생 원인 및 해결 방법
##### OOME 분석 툴
### JVM Sychronization이란?
#### 개요 ㆍㆍㆍㆍㆍㆍㆍ 94
##### Java 그리고 Thread
##### Thread 동기화
##### Mutual Exclusion과 Critical Section
##### Monitor
#### Java의 동기화(Synchronization) 방법
##### Synchronized Statement
##### synchronized Method
##### Wait And Notify
##### synchronized Statement와 synchronized Method 사용
#### Thread 상태
#### Thread의 종류
#### JVM에서의 대기 현상 분석
#### Thread Dump
#### Case별 synchronized에 대한 Thread Dump 분석
##### 동기화 방식별 소스 코드
##### Hot Spot JVM 실행 분석
##### IBM JVM 실행 분석
#### Thread Dump를 통한 Thread 동기화 문제 해결의 실 사례
## 도구(Tool)를 이용한 성능분석
### Java 성능분석 도구 개요
#### JDK 내장 성능분석 도구
#### 3rd Party 성능분석 도구
#### JVM Thread, 메모리 정보
##### Thread Dump와 Stack Trace 정보
##### Heap 메모리 구조
##### Heap Dump 정보
##### 객체 참조, GC와 메모리 누수
### jcmd
#### jcmd를 이용하여 Java 프로세스 정보 확인하기
#### Java Flight Recording 기능 사용하기
#### GC 메모리 분석 기능 사용하기
#### Management Agent(JMX) 기능 사용하기
#### jcmd 도구 vs 다른 도구 비교
### Java Mission Control 도구의 활용
#### 실시간 모니터링
#### Java Flight Recorder 레코딩하기
#### General 정보
#### Memory 정보
#### Code 정보
#### Threads 정보 보기
#### IO 정보 보기
#### System 정보 보기
#### Events 정보 보기
### JConsole
### VisualVM
#### 6.1 Monitor 탭
#### 6.2 Heap Dump 내용 보기
#### 6.3 Threads 탭
#### 6.4 Profiler 수행하기
#### 6.5 Sampler 수행하기
#### 6.6 MBeans Plugin으로 JMX 모니터링하기
#### 6.7 Visual GC Plugin 기능 덧입기
#### 6.8 JConsole Plugin기능을 VisualVM에서 사용하기
### Eclipse Memory Analyzer (MAT)
#### MAT 설치하기
#### HeapDump 분석 방법
#### HeapDump 파일 열기
#### 객체 참조관계 분석
#### ClassLoader 누수 분석 (PermGen이슈)
#### 객체를 사용하는 Thread 분석
#### Collection 분석
#### Dominator Tree 분석
#### Leak Suspects 분석
#### Heap Dump 파일 비교 분석
### IBM HeapAnalyzer
#### IBM HeapAnalyzer 사용되는 용어 정의
#### Summary
#### Leak Suspect
#### Object List
#### Type List
#### Root List / Root Type List
#### Gaps by Size/ Gap Statistics
### Java Thread Dump Analyzer(TDA)
#### TDA 사용하기
#### TDA를 이용한 분석
### 성능분석 도구들 비교
## APM(InterMax) 활용 성능 분석 사례
### InterMax란 무엇인가?
#### 실시간 모니터링
#### 사후 분석
#### 트랜잭션 조회
### 성능 분석 사례
#### 과도한 SQL Fetch에 의한 OOME 발생 사례
#### Full GC 수행에 따른 애플리케이션 수행 지연 발생 사례
#### 특정 오브젝트의 메모리 과다 사용으로 인한 OOME 발생 사례
#### 소켓 타임아웃에 의한 서비스 지연 발생 사례
#### Exception이 발생하며 서비스 수행에 실패하는 사례
#### SQL 수행 지연에 따른 애플리케이션 지연 현상 분석 사례
#### DB Lock에 의한 애플리케이션 지연 현상 분석 사례