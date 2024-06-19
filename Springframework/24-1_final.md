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

