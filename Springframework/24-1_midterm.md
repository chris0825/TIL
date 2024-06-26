# 목차
[- 개념](#MVC-개념)<br>
[- 의존 객체 자동 주입](#의존-객체-자동-주입)<br>
[- XML 파일 대신 Java 파일 이용하기](#XML-파일-대신-Java-파일-이용하기)<br>

### MVC 개념
> 모델(M), 뷰(V), 컨트롤러(C)를 이용해서 프로그래밍하는 소프트웨어 설계 방법
- M(model): 모델
  > 데이터베이스와 밀접한 관계를 갖고 비즈니스 로직 담당
- V(view): 뷰
  > 클라이언트와 밀접한 관계를 갖고 비즈니스 로직의 결과를 출력하기 위한 화면 구성 담당
- C(controller): 컨트롤러
  > 클라이언트의 요청에 대해 모델과 뷰를 컨트롤하는 업무를 담당
### 메이븐 디렉터리 구성
- root 디렉터리
- java 디렉터리
  > 프로젝트에 필요한 java파일이 관리되는 곳
- resources 디렉터디
  > 프로젝트에 필요한 자원이 관리되는 폴더 (XML 파일, property 파일 등)
### DI ( Dependency Injection ): 의존성 주입
> 필요한(의존하는) 객체를 직접 생성하지 않고 외부에서 주입하는 방식
### IoC (Inversion of Control): 제어의 역전
> 프로그램의 제어권을 개발자가 아닌 외부에서 컨트롤 하는 방식
```java
// Main.java
MyCalculator calculator = new Mycalculator();
calculator.calAdd(10, 5);

// MyCalculator.java
public void calAdd(int fNum, int sNum) {
  ICalculator calculator = new CalAdd();            // 객체 직접 생성
  int value = Calculator.doOperation(fNum, sNum);   // 덧셈 실행
  System.out.println("result: " + value);
}
```
🔽 의존성 주입(DI)
```java
// Main.java
MyCalculator calculator = new Mycalculator();
calculator.calAdd(10, 5, new CalAdd());                  // 객체 주입

// MyCalculator.java
public void calAdd(int fNum, int sNum, CalAdd calAdd) {  // CalAdd 객체 주입
  int value = calAdd.doOperation(fNum, sNum);            // 덧셈 실행
  System.out.println("result: " + value);
}
```
🔽 인터페이스 활용
```java
// Main.java
MyCalculator calculator = new Mycalculator();
calculator.calAdd(10, 5, new CalAdd());                             // 객체 주입

// MyCalculator.java
public void calAdd(int fNum, int sNum, ICalculator calculator) {    // ICalculator 객체 주입
  int value = calAdd.doOperation(fNum, sNum);                       // 덧셈 실행
  System.out.println("result: " + value);
}
```
🔽 제어의 역전(IoC)
```java
// Main.java
new CalAssembler();

//CalAssembler.java
MyCalculator calculator;
CalAdd calAdd;
CalSub calSub;

public CalAssembler() {
  calculator = new Calculator();
  calAdd = new CalAdd();
  calSub = new CalSub();

  assembler();
}

public void assembler() {
  calculator.calculate(10, 5, calAdd);
  calculator.calculate(10, 5, calSub);\
}
```
### 컴파일 ⊂ 빌드
- 컴파일
  > 우리가 코딩한 코드 파일을 컴파일러가 바이트코드 파일로 변환하는 과정
- 빌드
  > 라이브러리 다운로드 및 연결, 컴파일, 링크, 패키징 등 애플리케이션 제작에 필요한 전반적인 과정
  - 빌드 툴
    - Ant
      > 내부 스크립트가 다소 복잡<br>
      > 과거에 많이 사용했으나 사용빈도 줄어듦
    - Maven
      > 스프링 애플리케이션 개발에 사용<br>
      > 오래전부터 현재까지 많은 산업 현장에서 사용중
    - Gradle
      > Maven보다 약 두 배가량 속도가 빠름
      > 최근 인기
### GenericXmlApplicationContext 라이브러리 호출
```xml
<!-- spring-context 모듈 -->
<dependencies>
  <dependency>
    <groupId>org.springframework</groupId>              // org.springframework 그룹의
    <artifactId>spring-context</artifactId>             // spring-context 모듈의 (artifact는 모듈의 단위)
    <version>5.2.9.RELEASE</version>                    // 5.2.9.RELEASE 버전 사용(의존)
  </dependency>
</dependencies>

<!-- 빌드 설정 -->
<build> // java파일을 컴파일 할 때 JDK 11 버전으로 컴파일, java 소스를 UTF-8로 인코딩
  <plugins>
    <plugin>
      <artifactId>maven-complier-plugin</artifactId>
      <version>3.1</version>
      <configuration>
        <source>11</source>
        <target>11</target>
        <encoding>UTF-8</encoding>
      </configuration>
    </plugin>
  </plugins>
</build>
```
### 객체 생성
- 기존 객체 생성 방법
```java
TransportationWalk tWalk = new TransportationWalk();
```
- IoC 컨테이너 객체 생성 방법
```xml
<bean id="tWalk" class="패키지.TransportationWalk" />
```
### 필드 초기화
- 기존 필드 초기화 방법
```java
pricate String[] sNums = {"v1", "v2"};
```
- IoC 컨테이너 필드 초기화 방법
```xml
<bean id="변수 명", class="패키지.클래스명" />
  <property name="sNums">
    <array>
      <value>v1</value>
      <value>v2</value>
    </array>
  </property>
</bean>
```
  - \<bean\>은 생성자를 호출해서 빈을 생성함
    > 컴파일 단계에서 디폴트 생성자를 만듦 (어떠한 생성자도 명시되어있지 않을 시)<br>
    > 생성자가 명시되어 있다면 에러발생 ➡️ \<bean\> 하위 태그로 \<constructor-arg\> 태그의 ref 속성을 지정해 주어야 함
    ```xml
    <bean id="A" class="패키지명.파일명" />
    <bean id="B" class="패키지명.파일명">
      <constructor-arg ref="A" />
    </bean>
    ```
  - \<property\>가 필드를 초기화 하기 위해서는 setter메서드를 이용
    > setter메서드 <ins>**무조건 명시**</ins>되어 있어야 함(12장에서 자동 생성 배움)
### 필드 초기화 (데이터가 1개 뿐일때)
```xml
<property name="변수명">
  <value>원소1</value>
</property>
```
🔽
```xml
<property name="변수명" value="원소1" />
```
### 필드 초기화 (자료형)
- List
```xml
// private List<String> 변수명 = new ArrayList<>(Arrays.asList("원소1", "원소2"));
<property name="변수명">
  <list>
    <value>원소1</value>
    <value>원소2</value>
  </list>
</property>
```
- Map
```xml
// private Map<String, String> 변수명 = new HashMap<String, String>(){{put("키1", "원소1");}};
<property name="변수명">
  <map>
    <entry>
      <key>
        <value>키1</value>
      </key>
      <value>원소1</value>
    </entry>
  </map>
</property>
```
- 사용자 데이터 타입(기초 데이터 타입 X)
```xml
// private Map<String, 사용자 데이터 타입> 변수명;
<property name="변수명">
  <map>
    <entry>
      <key>
        <value>키1</value>
      </key>
      <ref bean="사용자 데이터 타입 빈id" />
    </entry>
  </map
</property>
```
### 분리된 XML파일 (GenericXmlApplicationContext)
- 기본
```java
GenericXmlApplicationContext ctx = new GenericXmlApplicationContext("classpath:파일명1.xml", "classpath:파일명2.xml");
```
- 리스트 사용
```java
String[] 리스트명 = {"classpath:파일명1.xml", "classpath:파일명2.xml"};
GenericXmlApplicationContext ctx = new GenericXmlApplicationContext(리스트명);
```
- 하나의 xml파일에 \<import\>태그 사용하여 묶기
```
// 파일import.xml
<?xml version="1.0" encoding="UTF-8"?>

<beans xmlns="~생략">
  <import resource="classpath:파일명.xml"/>
</bean>

// java
GenericXmlApplicationContext ctx = new GenericXmlApplicationContext("classpath:파일import.xml");
```
### 스프링 빈 범위<sub>Spring Bean Scope</sub>: 싱글턴<sub>singleton</sub> 과 프로토타입<sub>prototype</sub>
> 스프링 컨테이너에서 생성된 빈을 <ins>getBean()</ins>메서드로 가져올 때<br>
```java
GenericXmlApplicationContext ctx = new GenericXmlApplicationContext("classpath:파일명.xml");
자료형클래스 변수명 = ctx.getBean("빈id", "클래스명.class");
```
> 동일 빈을 재사용 ➡️ 싱글턴 (default)<br>
```xml
<bean id="변수명" class="패키지.파일명" />
<!-- OR -->
<bean id="변수명" class="패키지.파일명" scope="singleton" />
```
> 매번 다른 빈 사용 ➡️ 프로토타입
```xml
<bean id="변수명" class="패키지.파일명" scope="prototype" />
```
### 의존 객체 자동 주입
- 기존 방식
```xml
<bean id="빈id" class="패키지.파일명">

  <constructor-arg ref="의존 빈id" />

</bean>
```
- 자동 주입 방식
  > 매개변수의 데이터 타입을 기준으로 자동 주입
```xml
<beans xmlns="생략
  http://www.springframework.org/schema/context
  http://www.springframework.org/schema/context/spring-context.xsd">

  <context:annotation-config/>

</bean>
```
### 의존객체 자동 주입: 클래스 생성자 오버라이드<sub>override</sub>
- @Autowired
  > <ins>데이터 타입</ins> 이용하여 객체 자동 주입, 필드/<ins>생성자</ins>/메서드 이용 가능, <ins>스프링</ins>에서 제공하는 애너테이션<br>
- @Resource
  > <ins>빈 객체의 이름</ins>을 이용하여 객체 자동 주입, 필드/메서드 이용 가능, <ins>자바</ins>에서 제공하는 애너테이션(관련 모듈 설정 필요)
- @Inject
  > @Autowired과 대부분 동일<br>
  > 동일 기능 다른 명칭: @Autowired + @Qualifier ➡️ @Inject + @Named<br>
  > 차이점: 자바에서 제공하는 애너테이션, required 속성 지원X
```java
import org.springframework.beans.factory.annotation.Autowired;

public 클래스명() {
  System.out.println("default 생성자");
}

@Autowired // @Resource 사용 X: 생성자 사용 불가
public 클래스명(매개변수) {
  System.out.println("매개변수");
  this.매개변수 = 매개변수;
}
```
> 이 경우 default생성자는 없어도 컴파일시 자동 생성해주기때문에 작성하지 않아도 됨<br>
> 그러나 <ins>필드/메서드</ins> 사용시에는 **생성자 무조건 필요**
### 의존객체 자동 주입: 다수 빈 객체 중 의존 대상 객체 선정
> \<qualifier value="태그"\>
- 변수가 1개 인 경우
```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Qualifier;

@Autowired
@Qualifier("태그")      // 객체를 자동 주입하려는 빈의 id와 변수명이 같으면 @Qualifier 애너테이션 없어도 자동 주입됨
private 자료형 변수명;
```
- 변수가 2개 이상인 경우
```java
@Autowired
public AutoWiredEx(@Qualifier("태그") 자료형1 변수명1, 자료형2 변수명2) {}
```
### 의존객체 자동 주입: 필수 OR 선택
> 빈을 생성하지 않고 @Autowired를 사용하면 의존 객체를 찾을 수 없어 에러 발생<br>
> ➡️ @Autowired의 required속성 이용하여 필수가 아닌 선택으로 변경 가능
```java
@Autowired(required = false)
private 자료형 변수명;
```
## XML 파일 대신 Java 파일 이용하기
### @Configuration
> java 파일을 스프링 설정파일로 만들어줌
### @Bean
> 빈 객체 생성
```java
import org.springframework.context.annotation.Configuration;

@Configuration
public class 클래스명 {

  // <bean id="함수명" class="패키지.자료형클래스" />
  @Bean
  public 자료형클래스 함수명() {
    return new 객체명();
  }

  // 의존 객체 Ver.
  /**
  <bean id="함수명" class="패키지.자료형클래스">
    <constructor-arg ref="의존객체 빈id"/>
  </bean>
  */
  @Bean
  public 자료형클래스 함수명() {
    return new 자료형클래스(의존객체 빈id());
  }

}
```
### XML 파일 대신 Java 파일 이용하기: 의존 객체 주입
```xml
<bean id="빈id" class="패키지.자료형클래스">
  <property name="이름1" value="원소1" />
  <property name="이름2" value="원소2" />
</bean>
```
🔽
```java
@Bean
public 자료형클래스 빈id() {
  자료형클래스 객체명 = new 자료형클래스();
  객체명.set이름1("원소1");
  객체명.set이름2("원소2");

  return 객체명;
}
```
### XML 파일 대신 Java 파일 이용하기: IoC 컨테이너 초기화
- before
```java
GenericXmlApplicationContext ctx = new GenericXmlApplicationContext("classpath:파일명.xml");
```
- after
```java
AnnotationConfigApplicationContext ctx = new AnnotationConfigApplicationContext(클래스명.class);
```
### XML 파일 대신 Java 파일 이용하기: 파일 분리
- 파일 분리 후 @Autowired 애너테이션 이용하여 빈 객체 선언해주어야 함
```java
@Configuration
public class 클래스명1 {

  @Autowired              // 의존 객체 주입
  자료형클래스 클래스명2;

}
```
- 초기화
```java
AnnotationConfigApplicationContext ctx = new AnnotationConfigApplicationContext(클래스명1.class, 클래스명2.class);
```
### XML 파일 대신 Java 파일 이용하기: 분리한 파일 import
- before
```xml
<import resource="classpath:파일명.xml" />
```
- after
```java
@Configuration
@Import({파일명1.class, 파일명2.class})
public class 클래스명 {
}
```
