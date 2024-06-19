### 자바 버전 변경 (1.6 -> 11)
```xml
<!-- pom.xml JDK 1.6 -->

<java-version>1.6</java-version>
<source>1.6</source>
<target>1.6</target>
<org.springframwork-version>3.1.1.RELEASE</org.springframework-version>
```
```xml
<!-- pom.xml JDK 11 -->

<java-version>11</java-version>
<source>11</source>
<target>11</target>
<org.springframwork-version>5.2.9.RELEASE</org.springframework-version>
```

### 한글 인코딩 (web.xml)
```xml
<filter>
  <filter-name>encodingFilter</filter-name>
  <filter-class>org.springframework.web.filter.characterEncodingFilter</filter-class>
  <init-param>
    <param-name>encoding</param-name>
    <param-value>UTF-8</param-value>
  </init-param>
  <init-param>
    <param-name>forceEncoding</param-name>
    <param-value>true</param-value>
  </init-param>
</filter>
<filter-mapping>
  <filter-name>encodingFilter</filter-name>
  <url-pattern>/*</url-pattern>
</filter-mapping>
```

### 프로젝트 구조
- src/main/
  - java
    > java 파일 위치, 웹 애플리케이션에 사용되는 Controller, Service, Dao 객체가 있는 폴더
  - webapp
    > web과 관련된 파일들이 있는 폴더
  - resource
    > CSS, JS파일이 있는 폴더
- web.xml
  > 웹 서비스의 전반적인 설정
- pom.xml
  > 메인 리포지터리에서 프로젝트에 필요한 라이브러리를 내려 받기 위한 메이븐 설정 파일

### 스프링 MVC 설정
- pom.xml
```xml
<dependency>
  <groupId>org.springframework</groupId>
  <artifactId>spring-webmvc</artifactId>
  <version>${org.springframework-version}</version>
</dependency>
```

### spring-jdbc와 maria-java-client 모듈 가져오는 코드
- pom.xml
```xml
<!-- JDBC -->
<dependency>
  <groupId>org.springframework</groupId>
  <artifactId>spring-jdbc</artifactId>
  <version>${org.springframework-version}</version>
</dependency>

<!-- MariaDB -->
<dependency>
  <groupId>org.mariadb.jdbc</groupId>
  <artifactId>mariadb-java-client</artifactId>
  <version>3.1.2</version>
</dependency>
```

### 프로젝트가 서버에서 실행될 때 jdbc-context.xml파일 인식할 수 있도록 web.xml에 코드 작성
- web.xml
```xml
<context-param>
  <param-name>contextConfigLocation</param-name>
  <param-value>
    /WEB-INF/spring/root-context.xml
    /WEB-INF/spring/jdbc-context.xml
  </param-value>
</context-param>
```
- Dao.java
```java
@Autowired
JdbcTempalte jdbcTemplate;
```

## 애너테이션
### @Controller
> 해당 클래스가 웹 애플리케이션에서 Controller로 사용됨을 명시
- servlet-context.xml
```xml
<annotation-driven />
```
- AdminMemberController.java
```java
@Controller
public class AdminMemberController { ... }
```

### @RequestMapping
> 메서드가 사용자의 요청을 받음

> 속성이 value 하나라면 값만 입력할 수 있음

> method속성의 Defalut값은 GET으로 해당 속성을 생략하면 자동 GET방식으로 처리
```java
@RequestMapping(value="/", method=Request.GET)

// method 속성의 Default 값은 GET방식

@RequestMapping(value = "/")

//  속성이 value 하나 뿐이면 값만 써도 됨

@RequestMapping("/")
```

### @GetMapping, PostMapping
> @RequestMapping의 method속성이 Request.GET 방식인지, Request.POST 방식인지에 따라 애너테이션으로 변환 가능
```java
// @RequestMapping(value="/createAccountForm", method=Request.GET)
@GetMapping("/createAccountForm")

// @RequestMapping(value="/createAccountConfirm", method=Request.POST)
@PostMapping("/createAccountConfirm")
```

### @RequestParam
> 클라이언트에서 입력한 데이터를 받아옴
```jsp
<input type ="text" name="m_id">
```
```java
public returnType methodName(@RequestParam("m_id") String m_id)

// 파라미터 변수 명이 jsp의 input태그 name의 값과 일치하는 경우 ("name값") 생략 가능

public returnType methodName(@RequestParam String m_id) { .. }
```

### @Service, @Component, @Repository
> 빈 객체 생성에 이용되는 애너테이션으로, 클래스 위에 작성

### @Configuration
- JdbcTemplageConfig.java
```java
@Configuration
public class JdbcTemplateConfig {
  @Value("#{infoProperty['db.driver']}")
  private String dbDriver;

  @Value("#{infoProperty['db.url']}")
  private String dbUrl;

  @Value("#{infoProperty['db.username']}")
  private String dbUsername;

  @Value("#{infoProperty['db.password']}")
  private String dbPassword;

  @Bean
  public DataSource dataSource() {
    DriverManagerDataSource dataSource = new DriverManagerDataSource();
    dataSource.setDriverClassName(dbDriver);
    dataSource.setUrl(dbUrl);
    dataSource.setUsername(dbUsername);
    dataSource.setPassword(dbPassword);

    return dataSource;
  }

  @Bean
  public JdbcTemplate jdbcTemplate() {
    return new JdbcTemplate(dataSource());
  }

  @Bean
  public DataSourceTransactionManager transactionManager() {
    DataSourceTransactionManager transactionManager = new DataSourceTransactionManager();

    return transactionManager;
  }
}
```

## 개념
### DTO와 VO
- DTO
  > 데이터를 변환하고 전달
  
  > Getter/Setter메서드만 구현(데이터 변경이 가능)
- VO
  > 데이터 자체에 의미가 존재
  
  > Getter 메서드만 구현(데이터 변경X)

  > 필드 값이 모두 같다면 같은 객체로 인식해야 하기 때문에 equals(), hashCode()메서드 @Override해야함

### 빈 충돌
- 이유
  > 빈(Bean)은 IoC컨테이너에 등록될 때 클래스 첫 이름이 소문자로 변환되어 클래스 이름이 ID로 사용됨. 이때, 중복된 ID가 있다면 충돌이 발생
- 해결 방법
  1. 아이디를 다르게 설정
  2. BeanNameGenerator 사용
      > BeanNameGenerator를 상속하는 클래스 LibraryBeanNameGenerator.java 생성

      > servlet.xml파일에 <context:component-scan base-package="com.office.library" name-generator="com.office.library.config.LibraryBeanNameGenerator">추가

### HandlerInterceptAdaptor
1. HandlerInterceptAdaptor상속하는 클래스 UserMemberLoginInterceptor.java생성
2. sevlet-context.xml파일에 아래 코드 추가
```xml
<interceptors>
  <interceptor>
    <mapping path="/book/user/rentalBookConfirm"/>
    <beans:bean class="com.office.library.user.member.UserMemberLoginInterceptor" />
  </interceptor>
</interceptors>
```
- preHandle()
  > 클라이언트 요청이 컨트롤러에 도달전에 호출됨. boolean반환. 매개변수로 handler받으며 true일때만 실행됨
- postHandle()
  > 클라이언트 요청이 컨트롤러에 실행된 후 호출됨. 컨트롤러에서 예외가 발생하지 않아야 실행됨
- afterCompletion()
  > 클라이언트의 요청이 컨트롤러에서 실행되고, 뷰를 통해서 응답이 완료된 후 호출됨. 뷰 생성시 예외 발생해도 실행됨

```xml
<mapping path="/user/member"/>
<exclude-mapping path="/user/member/loginConfirm"/>
```

### DB 이원화
  > 서비스 DB의 데이터는 사용자의 중요한 데이터를 개발자가 개발 및 테스트 목적으로 사용하지 못함

### 프로퍼티(Property)
  > DB 이원화로 인해 개발과 배포 단계에 DB URL을 수시로 변경해줘야 하는 번거로움을 공용으로 사용 가능한 프로퍼티 파일을 만들어 다양한 설정 값들을 정의해 놓을 수 있음
- properties-context.xml
```xml
<util:properties id="infoProperty" location="WEB-INF/spring/properties/dev.info.properties"/>
```
- web.xml
```xml
WEB-INF/spring/properties-context.xml
```
- jdbc-context.xml
```xml
<bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
  <property name="driverClassName" value="{infoProperty['db.driver']}"/>
  <property name="url" value="{infoProperty['db.url']}"/>
  <property name="username" value="{infoProperty['db.username']}"/>
  <property name="password" value="{infoProperty['db.password']}"/>
</bean>
```

## 서비스 객체 생성과 이용 방법
1. 객체 생성 연산자(new)를 이용하여 서비스 객체를 생성 및 이용
```java
MemberService memberService = new MemberService();
memberService.method();
```

2. 스프링 설정 파일(servlet-context.xml)을 이용하여 컨테이너에 빈(Bean) 객체를 생성하고, 의존 객체를 자동 주입하는 방법을 이용하여 서비스 객체를 이용
```xml
<!-- servlet.xml -->
<beans:bean id="MemberService" class="com.company.hello.member.MemberService"/>
```
```java
@Autowired
MemberService memberService;
```

3. 서비스 클래스(Sevice.java)에 애너테이션을 명시하여 스프링 컨테이너에 빈(Bean) 객체를 생성하고, 의존 객체를 자동 주입하는 방법을 이용하여 서비스 객체를 이용
```java
@Service
public class MemberService { ... }

// 다른 클래스에서 MemberSerive 의존
@Autowired
MemberService memberService;
```

## DB 연동 이전 Map이용
### DB가 없다면 Dao.java에 Map 자료구조 이용
> (Key, value) = m_id, MemberVo
```java
Map<String, MemberVo> memberDB = new HashMap<String, MemberVo>();
```

### Map의 memberDB내용 전체 출력 메서드
```java
public void printAll() {
  Set<String> keys = keys.keySet();
  Iterator<String> iterator = keys.iterator();
  while(iterator.hasNext()) {
    String key = iterator.next();
    MemberVo memberVo = memberDB.get(key);
    System.out.println(memberVo.toString());
  }
}
```

## @Configuration과 @Bean이용
### CommonsMultipartResolver - 파일 업로드
- comm.info.properties
```properties
uploadfile.size=10240000
uploadfile.encoding=utf-8
```
- properties-context.xml
```xml
<util:properties id="commInfoProperty" location="/WEB-INF/spring/properties/comm.info.properties"/>
```
- MultipartResolverConfig.java
```java
@Configuration
public class MultipartResolverConfig {
  @Value("#{commInfoProperty['uploadfile.size']}")
  private long fileSize;

  @Value("#{commInfoProperty['uploadfile.encoding']}")
  private String fileEncoding;

  @Bean
  public CommonsMultipartResolver multipartResolver() {
    CommonsMultipartResolver multipartResolver = new CommonsMultipartResolver();

    multipartResolver.setMaxUploadSize(fileSize);
    multipartResolver.setDefaultEncoding(fileEncoding);

    return multipartResolver;
  }
}
```

### JavaMailSenderImpl - 메일 발송
- comm.info.properties
```properties
mail.host=smtp.gmail.com
mail.port=587
mail.username=이메일
mail.password=앱비밀번호
mail.smtp.auth=true
mail.smtp.starttls.enable=true
```
- MailSenderConfig.java
```java
@Configuration
public class MailSenderConfig {
  @Value("#{commInfoProperty['mail.host']}")
  private String mailHost;

  @Value("#{commInfoProperty['mail.port']}")
  private String mailPort;

  @Value("#{commInfoProperty['mail.username']}")
  private String mailUsername;

  @Value("#{commInfoProperty['mail.password']}")
  private String mailPassword;

  @Value("#{commInfoProperty['mail.smtp.auth']}")
  private String mailSmtpAuth;

  @Value("#{commInfoProperty['mail.smtp.starttls.enable']}")
  private String mailSmtpStarttlsEnable;

  @Bean
  public JavaMailSenderImpl mailSender() {
    JavaMailSenderImpl mailSender = new JavaMailSenderImpl();

    mailSender.setHost(mailHost);
    mailSender.setPort(mailPort);
    mailSender.setUsername(mailUsername);
    mailSender.setPassword(mailPassword);

    Properties properties = new Properties();

    properties.setProperty("mailSmtpAuth", mailSmtpAuth);
    properties.setProperty("mailSmtpStarttlsEnable", mailSmtpStarttlsEnable);

    mailSender.setJavaMailProperties(properties);
  }
}
```

### BeanPropertyRowMapper
```java
RowMapper<AdminMemberVo> rowMapper = BeanPropertyRowMapper.newInstance(AdminMemberVo.class);
adminMemberVos = jdbcTemplate.query(sql, rowMapper, adminMemberVo.getA_m_id());
```

### 비밀번호 암호화
```java
@Configuration
public class SecurityConfig {
  @Bean
  public BCryptPasswordEncoder bCryptPasswordEncoder() {
    return new BCryptPasswordEncoder();
  }
}
```