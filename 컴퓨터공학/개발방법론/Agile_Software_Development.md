# Agile Software Development, Principles, Patterns, and Practices

## 1 애자일 개발

### 1 애자일 실천방법

#### 애자일 연합

##### 애자일 소프트웨어 개발 선언문
* 프로세스와 둘보다 개인과 상호작용이 우선이다.
* 포괄적인 문서보다 동작하는 소프트웨어가 우선이다.
* 계약 협싱보다 고객 협력이 우선이다.
* 계획을 따르는 것보다 변화에 대한 반응이 우선이다.

##### 원칙
* 우리의 최고 가치는 유용한 소프트웨어의 빠르고 지속적인 공개를 통해 고객을 만족시키는 것이다.
* 개발 후반부에 접어들었다 할지라도. 요구사항 변경을 환영하라. 애자일 프로세스는 고객의 경쟁 우위를 위해 변화를 이용한다.
* 개발 중인 소프트웨어를 2주에서 2달 사이, 혹은 더 짧은 시간 간격으로 자주 공개하라.
* 업무를 하는 사람과 개발자는 프로젝트를 통들어 계속 함께 일해야 한다.
* 의욕적인 개인들을 중심으로 프로젝트를 구성하라. 환경과 필요로 하는 지원을 제공하고, 그들이 그 일을 해낼 것이라 믿고 맡겨둬라.
* 개발 팀 내에서 정보틀 전달하고 공유하는 가장 효율적이고 효과적인 방법은 직접 일대일로 대화하는 것이다.
* 개발 중인 소프트웨어가 진척 상황의 일차적 척도다.
* 애자일 프로세스는 지속 가능한 개빌을 촉진한다. 스폰서, 개발자, 그리고 사용자는 무한히 지속적인 속도(pace)들 유지할 수 있어야 한다.
* 우수 기술과 좋은 설계에 대한 지속적인 관심은 속도룰 향상한다.
* 단순성(아직 끝내지 않은 일의 양을 최대화하는 예술)은 필수적이다.
* 최고의 아키텍처, 요구사항. 그리고 설계는 자기 조직적인 팀에서 나온다.
* 규칙적으로 팀은 좀 더 효과적인 방법을 반영해야 하고, 적절히 그 행위를 조율하고 조정해야 한다.

### 2 익스트림 프로그래밍 소개

#### 익스트림 프로그래밍 실천방법
* 익스트림 프로그래밍(XP: Extreme Programming)은 애자일 방법 중에서도 가장 유명한데, 단순하면서도 서로 의존적인 실천방법의 집힙으로 구성

##### 고객 팀 구성원

##### 사용자 스토리
* 현재 진행 중인 요구사항에 관한 대화의 연상 기호다. 이것은 고객이 우선순위와 추정 비용에 근거해 요구사항의 구현 일정을 수립하게 해주는 계획 툴

##### 짧은 반복

##### 인수 테스트

##### 짝 프로그래밍
* 모든 운영 코드(production code)는 같은 워크스테이션으로 일하는 프로그래머 짝들에 의해 작성된다.

##### 테스트 주도 개발
* 모든 운영 코드는 실패하는 단위 테스트를 통과하기 위해 작성된다.

##### 공동 소유권

##### 지속적인 통합

##### 지속 가능한 속도

##### 열린 작업 공간

##### 계획 세우기 게임

##### 단순한 설계
* 어떻게든 동작하는 가장 단순한 것을 생각한다.
* 필요하지 않을 겻이라는 가정에서 시작한다.
* 코드를 중복에서 쓰지 않는다.

##### 리팩토링

##### 메타포

### 3 계획 세우기

### 4 테스트

##### 테스트 주도 개발
* 일차적이고 가장 명백한 효과는 프로그램의 모든 단일 함수가 그 동작을 검증하는 테스트를 갖게 된다는 것
* 명백하진 않지만 더 중요한 효과는, 테스트를 먼저 작성할 경우 프로그래머가 다른 관점에서 문제를 해결할 수 있다는 것
* 테스트를 먼저 작성함으로써, 프로그래머는 자신이 반드시 테스트 가능한 프로그램을 설계하도록 강제할 수 있음
* 테스트가 문서화의 귀중한 한 형태로 기능할 있다는 것

##### 테스트 우선 방식 설계의 예

### 5 리팩토링
* 리팩토링을 "외부행위를 바꾸지 않으면서 내부 구조를 개선하는 방법으로, 소프트웨어 시스템을 변경하는 프로세스"

#### 소수 생성기: 리맥토링의 간단만 예*2

```java

public class PrimeGenerator {

	private static boolean[] isCrossed;
	private static int[] result;

	public static int[] generatePrimes(int maxValue) {
		if (maxValue < 2) {
			return new int[0];
		} else {
			initializeArrayOfIntegers(maxValue);
			crossOutMultiples();
			putUncrossedIntegerIntoResult();
			return result;
		}
	}

	private static void initializeArrayOfIntegers(int maxValue) {
		isCrossed = new boolean[maxValue + 1];
		for (int i = 2; i < isCrossed.length; i++)
			isCrossed[i] = false;
	}

	private static void crossOutMultiples() {
		for (int i = 2; i <= calcMaxPrimeFactor(); i++) {
			if (notCrossed(i)) {
				crossOutMultiplesOf(i);
			}
		}
	}

	private static void crossOutMultiplesOf(int i) {
		for (int j = 2 * i; j < isCrossed.length; j += i) {
			isCrossed[j] = true;
		}
	}

	private static void putUncrossedIntegerIntoResult() {
		result = new int[numberOfUncrossedIntegers()];
		for (int i = 2, j = 0; i < isCrossed.length; i++) {
			if (notCrossed(i))
				result[j++] = i;
		}
	}

	private static int numberOfUncrossedIntegers() {
		int count = 0;
		for (int i = 2; i < isCrossed.length; i++) {
			if (notCrossed(i))
				count++;
		}
		return count;
	}

	private static boolean notCrossed(int i) {
		return isCrossed[i] == false;
	}

	private static int calcMaxPrimeFactor() {
		return (int) Math.sqrt(isCrossed.length) + 1;
	}
}

```

```java

import org.junit.Test;

import static org.junit.Assert.assertEquals;

public class TestGeneratePrimes {

	@Test
	public void testPrimes() {
		int[] nullArray = PrimeGenerator.generatePrimes(0);
		assertEquals(nullArray.length, 0);

		int[] minArray = PrimeGenerator.generatePrimes(2);
		assertEquals(minArray.length, 1);
		assertEquals(minArray[0], 2);

		int[] threeArray = PrimeGenerator.generatePrimes(3);
		assertEquals(threeArray.length, 2);
		assertEquals(threeArray[0], 2);
		assertEquals(threeArray[1], 3);

		int[] centArray = PrimeGenerator.generatePrimes(100);
		assertEquals(centArray.length, 25);
	}

  @Test
	public void testExhaustive() {
		for (int i = 0; i < 500; i++) {
			verifyPrimeList(PrimeGenerator.generatePrimes(i));
		}
	}

	private void verifyPrimeList(int[] list) {
		for (int i : list) {
			verifyPrime(i);
		}
	}

	private void verifyPrime(int n) {
		for (int j = 2; j < n; j++) {
			assertTrue(n % j != 0);
		}
	}
}

```

### 6 프로그래밍 에피소드

## 2 애자일 설계

#### 잘못된 설계의 증상
1. 경직성(Rigidity) : 설계를 변경하기 어려움
2. 취약성(Fragility) : 설계가 망가지지 쉬움
3. 부동성(Immobility) : 설계를 재사용하기 어려움
4. 점착성(Viscosity) : 제대로 동작하기 어려움
5. 불필요한 복잡성 (Needless Complexity) : 과도한 설계
6. 불필요한 반복(Needless Repetition) : 마우스 남용
7. 불투명성(Opacity) : 혼란스러운 표현

#### 원칙
1. SRP: 단일 책임 원칙 (Single Responsibility Principle)
2. OCP: 개방 폐쇄 원칙 (Open-Closed Principle)
3. LSP: 리스코프 치환 원칙 (Liskov Substitution Principle)
4. DIP: 의존 관계 역전 원칙 (Dependency Inversion Principle)
5. ISP: 인터페이스 분리 원칙 (Interface Segregation Principle)

#### 악취의 원칙
* 원칙에 대한 맹종은 불필요한 복잡성이란 설계의 악취로 이어진다.

### 7 애자일 설계란 무엇인가?
* **소스 코드가 바로 설계다.**

#### 소프트웨어에서 어떤 것이 잘못되는가?
* 뭔가 잘못되기 시작한다. (그게 무엇인가?)

#### 설계의 악취: 부패하고 있는 소프트웨어의 냄새

### 8 단일 책임 원칙(SRP)

### 9 개방 폐쇄 원칙(OCP)

### 10 리스코프 치환 원칙(LSP)

### 11 의존 관계 역전 원칙(DIP)

### 12 인터페이스 분리 원칙(ISP)

## 3 급여 관리 사례 연구

### 13 커맨드와 액티브 오브젝트 패턴

### 14 템플릿 메소드와 스트래터지 패턴: 상속과 위임

### 15 퍼사드 패턴

### 16 싱글톤과 모노스테이트 패턴

### 17 널 오브젝트 패턴

### 18 급여 관리 사례 연구: 반복의 시작

### 19 급여 관리 사례 연구: 구현

## 4 급여 관리 시스템 패키징

### 20 패키지 설계의 원칙

### 21 팩토리 패턴

### 22 급여 관리 사례 연구(2부)

## 5 기상 관측기 사례 연구

### 23 컴포지트 패턴

### 24 옵저버 패턴: 패턴으로 돌아가기

### 25 추상 서버, 어댑터, 브리지 패턴

### 26 프록시 패턴 프록시와 천국으로의 계단 패턴: 서드파티 API 관리

### 27 사례 연구: 기상 관측기

## 6 ETS 사례 연구

### 28 비지터 패턴

### 29 스테이트 패턴

### 30 ETS 프레임워크
