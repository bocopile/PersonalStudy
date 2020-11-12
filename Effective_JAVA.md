## 들어가기 앞서서
'Effactive Java 3/E' 이라는 책으로 Joshua Bloch 라는 분께서 지으신
책입니다. 백엔드 개발자 4년차로서 이때까지 여러 프로젝트에 사용되었던 언어입니다.
그러나 문득 내가 JAVA에 대해서 얼마나 알고, 자신있게 다른 사람들 한테 내가 아는 지식을 
전파할수 있을까라는 고민을 해본 결과 이쯤에서 java를 한번 깊게 되집어 포는 시간을 가져야 할거 같았습니다.
해당 책의 목차 가 이끌렸고 이번에 이 책으로 되돌아보는 시간을 가지고자 합니다.

### 아이템 21. 인터페이스는 구현하는 쪽을 생각해 설계하라
Java 8 이전에는 기존 구현체를 깨트리지 않고는 인터페이스에 메서드를 추가할 방법이 없었다.
Java 8이 등장하면서 기존 인터페이스에 메서드를 추가할 수 있도록 디폴트 메서드가 등장하였지만 위험이 완전하게 없어지진 않았따.

-> 즉 디폴트 메서드는 컴파일이 성공하더라도 기존 구현체에 런타임 오류를 일으킬수 이싿.

-> 인터페이스를 설계할 떄는 여전히 세심한 주의를 기울여야 한다.


### 아이템 22. 인터페이스는 타입을 정의하는 용도로만 사용해라
인터페이스는 자신을 구현한 클래스의 인스턴스를 참조할 수 있는 타입 역할을 한다.

-> 클래스가 어떤 인터페이스를 구현한다는 것은 자신의 인스턴스로 무엇을 할 수 있는지를 클라이언트에 얘기해주는 것이다.

-> 맞지 않는 예) 상수 인터페이스 안티 패턴

-> 상수를 공개 할 목적이라면 여러가지 선택지가 있다.

- 특정클래스나 인터페이스와 강하게 연관된 상수라면 그 클래스나 인터페이스 자체에 추가해야 한다.

  -> ex) 모든 숫자 기본 타입의 박싱 클래스(Integer,Double의 MIN_VALUE / MAX_VALUE)

- 열거 타입으로 나타내기 적합한 상수라면 열거타입으로 만든 후에 공개한다 (아이템 34)

- 그것도 아니라면, 인스턴스화 할수 없는 유틸리티 클래스(아이템 4)에 담아 공개


#### 정리 : 인터페이스는 타입을 정의하는 용도로만 사용하고 , 상수 공개용 수단으로 사용하지 말자

### 아이템 23. 테그 달린 클래스 보다는 클래스 계층 구조를 활용해라

테그 달린 클래스에는 단점이 많다.

- 열거 타인 선언, 테그 필드, switch문 등 쓸데 없는 코드가 많다.

- 다른 의미를 위한 코드도 언제나 같이 따라다녀 메모리도 많이 사용한다.

- 또 다른 의미를 추가하려면 코드를 수정해야 한다.

- 인스턴스 타입만으로는 현재 나타내는 의미를 알길이 전혀 없다.

 -> 결론 : 테그 달린 클래스는 장황하고 오류가 많으며 비효율적이다.
 
 #### 정리 : 테그 달린 클래스를 써야 하는 상황이 거의 없다. 새로운 클래스를 작서하는데 테그 필드가 등장한다면 테그를 없애고 계층 구조로 대체하는 방법을 살표보자
 
 ### 아이템 24. 멤버 클래스는 되도록 static으로 만들라
 
 중첩 클래스에는 네 가지가 있으며, 가각의 쓰임이 다르다. 메서드 밖에서도 사용해야 하거나
 메서드 안에서 정의하기엔 너무 길다면 맴버 클래스를 만들어라,. 맴버 클래스에 인스턴스 가각이 바깥 인스턴스를 참조한다면 비정적으로, 
 그렇지 않다면 정적으로 만들자.중첩 클래스가 한 메서드 안에서만 쓰이면서 그 인스턴스를 생성하는 지점이 단 한곳이고
 해당 타입으로 쓰기에 적합한 클래스나 인터페이스가 이미 있다면 익명 클래스로 만들고 아니면 지역 클래스로 만들자
 
 
 ### 아이템 25. 톱레벨 클래스는 한 파일에 하나만 담으라
 소스 파일 하나에는 반드시 톱 레벨의 클래스 (또는 인터페이스) 하나만 담자 이 규칙만 따른다면 컴파일러가 한 클래스에
 대한 정의를 여러개 만들어 내는 일은 사라지고, 소스 파일을 어떤 순서로 컴파일 하던 바이너리 파일이나 프로그램의 동작이
 달라지는 일은 결코 일어나지 않을 것이다.
 
 
 ## 5장 Generic
 
 제네릭은 JAVA 5에서 부터 사용할 수 있다. 제네릭이 지원되기 전까지는 컬랙션에서 객체를 꺼낼때마다 형변환을 해줘야 했다.
 그래서 엉뚱한 타입의 객체를 넣어주면 런타임에 형변환 오류가 나곤 했다. 반면 제네릭을 사용하면 컬랙션이 담을 수 있는 타입을 컴파일러에 알려주게 된다. 그래서 컴파일러는 알아서 형변환 코드를 추가할 수ㅡ 있게 되고,
 엉뚱한 타입의 객체를 넣으려는 시도를 컴파일 과정에서 차단한다.
 
 ### 아이템 26. Row type은 사용하지 말라
 
 - 제네릭 클리스(인터페이스) : 클래스/인터페이스 선언에 타입 매개변수가 쓰이는 것
 
 -> ex) List[E]
 
 - 제네릭 타입 : 제네릭 클래스나 인터페이스를 통틀어 지칭하는말
 
 -> 가각의 제네럴 타입은 일련의 매개변수화 타입을 정의한다.
 
 - 로 타입 : 제네릭 타입에서 타입 매개변수를 전혀 사용하지 않을때를 말한다.
 
 -> 로 타입을 사용하게 되면 제네릭이 안겨주는 안정성과 표현력을 모두 잃게 된다.
 
 -> 또한 런타임에 예외가 발생할수 있다.

 -> 즉 제네릭이 도입되기 이전 코드와의 호환성을 위해서 제공될 뿐이다.
 
 
 ### 아이템 27. 비검사 경고를 제공하라
 제네릭을 사용하기 시작하면 수많은 컴파일러 경고를 보게 될것이다.
 
 -> ex) 비검사 형변환 경고, 비검사 메소드 호출 경고, 가변인수 타입 경고, 비검사 변환 경고 등 
 
 -> 할수 있는 한 모든 비검사 경고를 제거하는것이 좋다. (안정성 보장)
 
 -> 경고를 제거할 수는 없지만 타입이 안전하다고 확신을 할수 있다면 '@SuppressWarning("unchecked")'를 사용하자
 
 -> '@SuppressWarning("unchecked")'는 항상 가능한 좁은 범위에 적용해보자 (변수선언, 짧은 메서드, 생성자...)
 
 -> '@SuppressWarning("unchecked")'를 사용할 때에는 그 경고를 무시해도 되는 이유를 항상 주석으로 남겨놓아야 한다.
 
 
 ### 아이템 28. 배열 보다는 List를 사용하자.
 배열과 제네릭 타입에는 중요한 두가지 차이가 있다.
 
 - 배열은 공변(covariant; 共變)이다. 반면 제네릭은 불공변(incovariant; 不共變) 이다.
 
 - 배열은 실체화(reify)가 된다.
  
  -> 배열은 런타임에도 자신이 담기로 한 원소의 타입을 인지하고 확인하다. Long 배열에 String을 넣으면 ArrayStoreException이 발생한다.
  
  -> 형 안정성을 보장 받지 못함
 
 - 제네릭은 타입 정보가 런타임에는 소거가 된다.
 
 ->  원소 타입을 컴파일 타임에만 검사하며 런타임에서는 알수도 없다.
 
 -> 소거는 제네릭이 지원되기 전의 레거시 코드와 제네릭 타입을 함께 사용할 수 있게 해주는 메커니즘
 
 즉 이러한 이유 때문에 컴파일 오류나 경고를 만난다면 배열을 리스트로 대체하는 방법을 적요하자.
 
 
 ### 아이템 29. 이왕이면 제네릭 타입으로 만들라
 
 클라이언트에서 직접 형변환을 하는 타입보다 제네릭 타입이 더 안전하고 쓰기 편하다. 
 그러니 새로운 타입을 설계 할때는 형변환 없이도 사용할 수 있도록 해라, 그
 렇게 하려면 제네릭 타입으로 만들어야 하는 경우가 많다. 기존 클라이언트에서 영향을 주지 않으면서
 새로운 사용자를 훨씬 편하게 해주는 길이다.
 
 ### 아이템 30. 이왕이면 제네릭 메서드로 만들라
 
 제네릭 타입과 마찬가지로, 클라이언트에서 입력 매개변수와 반환값을 명시적으로 형변환을 해야하는 메서드 보다
 제네릭 메서드가 더 안전하며 사용하기도 쉽다.
 타입과 마찬가지로 메서드도 형변환 없이 사용할 수 있는 편이 좋으며, 많은 경우 그렇게 하려면
 제네릭 메서드가 되어야 한다.
 
 ### 아이템 31. 한정적 와일드카드를 사용해 API 유연성을 높이라
 
 - 유연성을 극대화 하려면 원소의 생산자나 소비자용 입력 매개변수에 와일드카드 타입을 사용하는 것이 좋다.
 
 - 단. 반환타입에는 한정적 와일드카드 타입을 사용하면 안된다.
 
 - 즉 조금 복잡하더라도 와일드카드 타입을 적용하면 API가 유연해지나 널리 쓰이는 라이브러리를 작성할 경우 와일드 카드를 적절하게 사용해야 한다
    
    -> PECS( 생산자[producer] 는 extends를 소비자[consumer]는 super를 사용한다.
    
 ### 아이템 32. 제네릭과 가변인수를 함께 쓸 때에는 신중하라
 
 - 가변인수: 필요에 따라 메게변수(인수)를 조절하는 기술
 
 - 가변인수 기능은 배열을 노출하여 추상화가 완벽하지 못하고, 배열과 제네릭 타입 규칙이 서로 다름, 제네릭 varargs 매개변수는 타입 안전하지 않지만 허용된다.
 
 - 메서드에 제네릭(혹은 메게변수화된) varargs 매개변수를 사용하고자 한다면, 먼저 그 메서드가 타입이 안전한지 확인한 다음에 @SafeVarangs 어노테이션을 달아 사용하는데 불편함이 없게 하자
 
 
 ### 아이템 33. 타입 안전 이종 컨테이너를 고려하라
 
 -  컬랙션 API로 대표되는 일반적인 제네릭 형태에서는 한 컨테이너가 다룰수 있는 타입 매개변수의 수가 고정이 되어있다.
 
 - 그러나 컨테이너 자체가 아닌 키를 타입 매개변수로 바꾸면 이런 제약 없는 타입 안전 이종 컨테이너를 만들수 있다. 타입 안전 이종 컨테이너는 class를 키로쓰며 이런식으로 쓰이는 class 객체를 타입 토큰이라고 한다.
 
 - 예) 데이터베이스 행을 표현한 DatabaseROw 타입에는 제네릭 타입인 Column[T]을 키로 쓸수 있다
 
## 6장 열거타입과 어노테이션
 
 JAVA에는 특수한 목적의 참조타입이 두가지 있다.
 
 - 열거 타입 (enum)
 
 - 어노테이션 (annotation)
 
 ### 아이템 34. int 상수 대신 열거 타입을 사용하라
 
 - 열거타입이 정수 상수보다 좋은점은 더 읽기 쉽고 안전하고 강력하다.
 
 - 대다수 열거 타입이 명시적 생성자나 메서드 없이 쓰이지만, 각 상수를 특정 데이터와 연결 짓거나 상수마다 다르게 동작할때는 필요하다.
 
 - 그물게는 하나의 메서드가 상수별로 다르게 동작해야 할때도 있는데 이때는 switch문 대신 상수별 메서드 구현을 사용하는 것이 좋다.
 
 - 열거타입 상수 일부가 같은 동작을 공유한다면 전략 열거 타입 패턴을 사용하자.
 
 ### 아이템 35. ordinal 메서드 대신 인스턴스 필드를 사용하자
 
 
 
 ### 아이템 36. 비트필드 대신 EnumSet을 사용하자
 
 - 열거할 수 있는 타입을 한데 모아 집합 형태로 사용한다고 해도 비트 필드를 사용할 이유는 없다.
 
 - EnumSet 클래스가 비트 필드 수준의 명료함과 서능을 제공하고 열거타입의 장점까지 선사한다.
 
 - EnumSet의 유일한 단점은 (~ JAVA 11) 불변의 EnumSet을 만들수 없다.
 
 - 그때까지 명확성과 성능이 조금 희생되지만 Collections.unmodifiableSet으로 EnumSet을 감싸 사용할수 없다.
 
 ### 아이템 37. ordinal 인덱싱 대신 EnumMap을 사용하라
 
 - 배열의 인덱스를 얻기 위해 ordinal을 쓰는 것은 일반적으로 좋지 않으나, 대신 EnumMap을 사용하자
 
 - 다차원 관계는 EnumMap<... EnumMap<...>>으로 표현하라
 
 - 어플리케이션 프로그래머는 Enum.ordinal을 (웬만해서는) 사용하지 말아야 한다.
 
 ### 아이템 38. 확장할 수 있는 열거 타입이 필요하면 인터페이스를 사용하라
 
 - 열거타입 자체는 확장할수 없으나, 인터페이스와 인터페이스를 구현하는 기본 열거 타입을 함께 사용해 같은 효과를 나타 낼수 있다.
 
 - 이렇게 하게 되면 클라이언트는 이 인터페이스를 구현해 자신만의 열거 타입(또는 다른 타입)을 만들 수 있다. 
 
 - API가 인터페이스 기반으로 작성되었다면 기본 열거 타입과 인스턴스가 쓰이는 모든 곳은 새로 확장한 열거 타입의 인스턴스로 대체해 사용할수 있다.
 
 ### 아이템 39. 명령 패턴 보다 어노테이션을 이용하자
 
 ### 아이템 40. @Override 어노테이션을 일관대게 사용하자
 
 - 상위 클래스의 메소드를 재정의하려는 오든 메소드에 @Override 어노테이션을 달자 (예외 - 구체 클래스에서 상위 클래스의 추상 메소드를 쟈정의 할때)