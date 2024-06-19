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
