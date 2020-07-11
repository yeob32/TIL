# Spring Bean

> Beans는 애플리케이션의 핵심을 이루는 객체이며, Spring IoC(Inversion of Control) 컨테이너에 의해 인스턴스화, 관리, 생성된다.


### Scope
* 스프링은 기본적으로 모든 bean을 singleton으로 생성하여 관리한다.
* 구체적으로는 애플리케이션 구동 시 JVM 안에서 스프링이 bean마다 하나의 객체를 생성하는 것을 의미한다.
* request, session, global session의 Scope는 일반 Spring 어플리케이션이 아닌, Spring MVC Web Application에서만 사용된다.

| Scope | Description |


**singleton**  
하나의 Bean 정의에 대해서 Spring IoC Container 내에 단 하나의 객체만 존재.


**prototype** @Scope(value = "prototype", proxyMode = ScopedProxyMode.TARGET_CLASS)    
하나의 Bean 정의에 대해서 다수의 객체가 존재 할 수 있다.


**request**  @RequestScope
하나의 Bean 정의에 대해서 하나의 HTTP request 의 생명주기 안에 단 하나의 객체만 존재.
즉, 각각의 HTTP request 는 자신만의 객체를 가진다.
Web-aware Spring ApplicationContext 안에서만 유효


**session**  @SessionScope
하나의 Bean 정의에 대해서 하나의 HTTP Session 의 생명주기에 안에 단 하나의 객체만 존재.
Web-aware Spring ApplicationContext 안에서만 유효


**global session**    
하나의 Bean 정의에 대해서 하나의 global HTTP Session 의 생명주기 안에 단 하나의 객체만 존재.
일반적으로 portlet context 안에서 유효.
Web-aware Spring ApplicationContext 안에서만 유효

**application** @ApplicationScope
Spring 컨테이너는 전체 웹 응용 프로그램에 대해 한 번 appPreferences bean 정의를 사용하여 appPreferences bean의 새 인스턴스를 만든다.
즉, appPreferences 콩은 일반의 ServletContext 속성으로 저장하는 ServletContext 수준에서 범위가있다. 
이것은 싱글톤 bean과 다소 비슷하지만 중요한 두 가지가 다르다
이것은 ServletContext 마다 싱글톤이지만, 스프링 ApplicationContext 마다는 아니고(또는 특정 웹 응용 프로그램에서 여러 가지가있을 수 있다) 실제로 노출되는 것은 ServletContext 의 속성에 따라 볼 수 있다.

### proxyMode
> 해당 객체를 참조하는 싱글톤 객체들은 프록시 객체를 주입 받음.

### 참고
* https://docs.spring.io/spring/docs/5.2.7.RELEASE/spring-framework-reference/core.html#beans-factory-scopes-application
* https://gmlwjd9405.github.io/2018/11/10/spring-beans.html
