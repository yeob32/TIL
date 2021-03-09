a
스프링 애플리케이션 컨텍스트 초기화 시 자기 자신도 빈으로 등록한다.
ex) @Autowired ApplicationContext;

## 애노테이션
- DirtiesContext
  - 테스트 메소드에서 애플리케이션 컨텍스트의 구성이나 상태를 변경한다는 것을 테스트 컨텍스트 프레임워크에 알려준다.
