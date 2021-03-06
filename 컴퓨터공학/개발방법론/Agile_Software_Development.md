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
1. 경직성 : 단순한 방법으로도 소프트웨어를 변경하기 어려운 경향
2. 취약성 : 한 군데를 변경했을 때 프로그램의 많은 부분이 잘못되는 경향
3. 부동성 : 다른 시스템에서 유용하게 쓸 수 있는 부분을 포함되고 있지만, 그런 부분을 원래 시스템에서 분리하는 수고와 위험성이 지나치게 클 때 설계는 움직이게 할 수 없음
4. 점착성 : 옳은 동작을 하는 것이 잘못된 동작을 하는 것보다 더 어렵다.
5. 불필요한 복작성 : 직접적인 효용이 전혀 없는 기반구조가 설계에 포함되어 있다.
6. 불필요한 반복 : 단일 추상 개념으로 통합할 수 있는 반복적인 구조가 설계에 포함되어 있다.
7. 불투명성 : 읽고 이해하기 어렵다. 그 의도를 잘 표현하지 못한다.

##### 무엇이 소프트웨어의 부패를 촉진하는가?
* 변경에 대해서도 탄력적인 설계를 만드는 방식을 찾아야 하고, 그것이 부패하지 않도록 보호할 수 있는 방식을 사용해야 함

##### 애자일 팀은 소프트웨어가 부패하도록 내버려두지 않는다

#### 'Copy' 프로그램

![Copy 프로그램 구조 차트](/assets/images/books/컴퓨터공학/개발방법론/Agile_Software_Development/figure_7-1.png)

* Copy 프로그램
```C++
void Copy() {
	int c;
	while ((c = RdKbd()) != EOF)
		WrtPrt(c);
}
```

* Copy 프로그램의 첫 번째 수정본
```C++
bool ptFlag = false;
void Copy() {
	int c;
	while ((c = (ptFlag ? RdPt() : RdKbd())) != EOF)
		WrtPrt(c);
}
```

* Copy 프로그램의 두 번째 수정본
```C++
bool ptFlag = false;
bool punchFlag = false;
void Copy() {
	int c;
	while ((c = (ptFlag ? RdPt() : RdKbd())) != EOF)
		punchFlag ? WrtPunch(c) : WrtPrt(c);
}
```

##### Copy 프로그램의 애자일 설계

```C++
class Reader {
	public : virtual int read() = 0;
}

class KeyboardReader : public Reader {
	public : virtual int read() {
		return RdKdb();
	}
}

KeyboardReader GdefaultReader;

void Copy(Reader & reader = GdefaultReader) {
	int c;
	while ((c = reader.read()) != EOF) {
		WrtPrt(c);
	}
}
```

##### 애자일 개발자는 해야 할 일을 어떻게 알았는가?
* 애플리케이션에서 Copy 모듈은 싱위 수준의 모듈로서. 애플리케이션의 정책을 결정하고 문자를 복사하는 방법을 일고 있댜 따라서 하위 수준의 세부 사항이 바뀔 때, 상위 수준의 정책이 영향을 받게 된다
* 하위 수준의 세부 사항 ?
* 상위 수준의 정책 ?
1. 그들은 다음과 같은 애자일 실천방법을 문제롤 찾아냈다.
2. 그들은 설계 원칙을 적용해 문제를 진단했다.
3. 그리고 적절한 디자인 패턴을 적용해 문제를 해결했다.

#### 가능한 한 좋은 상태로 설계 유지하기
* 애자일 개발자는 설계를 가능한 한 적절하고 명료한 상태로 유지하기 위해 애씀
* 설계의 가장 중요한 표현인 소스 코드 역시 명료한 상태로 유지

#### 결론
* 애자일 설계는 과정이지. 결과가 아니다.

### 8 단일 책임 원칙(SRP)

#### 단일 책임 원칙 (SRP)
* **한 클래스는 단 한가지의 변경 이유만을 가져야 한다.**
* 책임을 별개의 클래스로 분리
* 책임은 변경의 축

![하나 이상의 책임](/assets/images/books/컴퓨터공학/개발방법론/Agile_Software_Development/figure_8-1.png)

* 각기 다른 두 애플리케이션이 Rectangle 클래스를 이용
  * 계산 기하학을 위한 애플리케이션
	* 그래픽을 위한 애플리케이션
	* Rectangle 클래스가 두 가지의 책임을 맡고 있으므로 단일 책임 원칙(SRP)을 위반

![분리된 책임](/assets/images/books/컴퓨터공학/개발방법론/Agile_Software_Development/figure_8-2.png)

* Rectangle에서 계산을 하는 부분을 GeometricRectangle 클래스로 옮김
* 직사각형이 그려지는 방식에 대한 변경은 ComputationGeometryApplication에 영향을 주지 않음

##### 책임이란 무엇인가?
* SRP의 맥락에서, 우리는 책임(responsibility)을 '변경을 위한 이유'로 정의
* 애플리케이션이 서로 다른 시간에 두 가지 책임의 변경을 유발하는 방식으로 바뀌지는다면, 이들을 분리할 필요는 없음
  * 분리하면 불필요한 복작성 증가
* **변경의 축은 변경이 실제로 일어날 때만 변경의 축이다.**

```java
interface Model {
	public void dial(String png);
	public void hangup();
	public void send(char c);
	public void recv();
}
```

![분리된 Modem 인터페이스](/assets/images/books/컴퓨터공학/개발방법론/Agile_Software_Development/figure_8-3.png)

##### 결합된 책임 분리하기

#### 결론

### 9 개방 폐쇄 원칙(OCP)
* Bertrand Meyer "Object-oriented Software Construction"

#### 개방 폐쇄 원칙 (OCP)
* **소프트웨어 개체(클래스, 모듈, 함수 등)는 확장에 대해 열려 있어야 하고, 수정에 대해서는 닫혀 있어야 한다.**

#### 상세설명
* 1. 확장에 대해 열려 있다.
  * 모듈의 행위가 확장 될 수 있음을 의미
	* 애플리케이션의 요구사항이 변경될때, 이 변경에 맞게 새로운 행위를 추가해 모듈을 확장할 수 있음
	* 모듈이 하는 일을 변경할 수 있음
* 2. 수정에 대해 닫혀 있다.
  * 어떤 모듈의 행위를 확장하는 것이 그 모듈의 소스 코드나 바이너리코드의 변경을 초래하지 않음
  * 모듈의 실행 가능한 바이너리 형태는 링킹 가능한 라이브러리, DLL이나 자바의 .jar에서도 고스란히 남아 있음

#### 해결책은 추상화다
* C++, 자바 또는 다른 OOPL에서는, 고정되기는 해도 제한되지 않은 가능한 행위의 묶음을 표현하는 추상화(abstraction)를 만드는 것이 가능
* *추상화는 추상 기반 클래스이자, 모든 가능한 파생 클래스를 대표하는 가능한 행위의 제한되지 않은 묶음*
* **추상 클래스는 자신을 구현하는 클래스보다도 클라이언트에 더 밀접하게 관련**

#### Shape 애플리케이션

##### OCP 위반

##### OCP 따르기
* 기존 코드를 변경하기보다는 새로운 코드를 추가하는 방법으로 변경

##### 그래, 거짓말했다

##### 예상과 '자연스러운' 구조

##### '올가미' 놓기

##### 명시적인 폐쇄를 위해 추상화 사용하기

##### 폐쇄를 위한 '데이터 주도적' 접근 방식 사용하기

#### 결론
* **어설픈 추상화를 피하는 일은 추상화 자체만큼이나 중요하다.**

### 10 리스코프 치환 원칙(LSP)

#### 리스코프 치환 원칙 (LSP)
* **서브타입(subtype)은 그것의 기반 타입(base type)으로 치환 가능해야 한다.**
* 타입 S의 각 객체 o1과 타입 T의 각 객체 o2가 있을 때, T로 프로그램 P를 정의했음에도 불구하고, o1,이 o2로 치환될 때 P의 행위가 변히지 않으면, S는 P의 서브타입이다.

#### LSP 위반의 간단한 예

### 11 의존 관계 역전 원칙(DIP)
* 상위 수준의 모듈은 하위 수준의 모듈에 의존해서는 안된다. 둘 모두 추상화에 의존해야 한다.
* 추상화는 구체적인 사항에 의존해서는 안된다. 구체적인 사항은 추상화에 의존해야 한다.

### 12 인터페이스 분리 원칙(ISP)
* 클라이언트가 자신이 사용하지 않는 메소드에 의존하도록 강제되어서는 안된다.

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
