# Spring Bean

Beans는 애플리케이션의 핵심을 이루는 객체이며, Spring IoC(Inversion of Control) 컨테이너에 의해 인스턴스화, 관리, 생성된다.


### Scope
* 스프링은 기본적으로 모든 bean을 singleton으로 생성하여 관리한다.
* 구체적으로는 애플리케이션 구동 시 JVM 안에서 스프링이 bean마다 하나의 객체를 생성하는 것을 의미한다.
* request, session, global session의 Scope는 일반 Spring 어플리케이션이 아닌, Spring MVC Web Application에서만 사용된다.

**singleton**
하나의 Bean 정의에 대해서 Spring IoC Container 내에 단 하나의 객체만 존재.


**prototype** @Scope("prototype")  
하나의 Bean 정의에 대해서 다수의 객체가 존재 할 수 있다.


**request**  @Scope(value = WebApplicationContext.SCOPE_REQUEST)
하나의 Bean 정의에 대해서 하나의 HTTP request 의 생명주기 안에 단 하나의 객체만 존재.
즉, 각각의 HTTP request 는 자신만의 객체를 가진다.
Web-aware Spring ApplicationContext 안에서만 유효


**session**  @Scope(value = WebApplicationContext.SCOPE_SESSION) 
하나의 Bean 정의에 대해서 하나의 HTTP Session 의 생명주기에 안에 단 하나의 객체만 존재.
Web-aware Spring ApplicationContext 안에서만 유효


**global session**  
하나의 Bean 정의에 대해서 하나의 global HTTP Session 의 생명주기 안에 단 하나의 객체만 존재.
일반적으로 portlet context 안에서 유효.
Web-aware Spring ApplicationContext 안에서만 유효


### 참고
* https://gmlwjd9405.github.io/2018/11/10/spring-beans.html
