# Spring

`Spring`은 Java를 사용하여 쉽게 웹 응용프로그램을 만들 수 있게 해주는 <ins>POJO 기반 경량화 프레임워크</ins> 입니다.

## Spring의 핵심 3대 요소

**1. IoC/DI**

`IoC(Inversion of Control)`을 직역하면 제어의 역전입니다. 우리가 스프링 코드를 호출하는 것이 아니라 스프링의 코드가 우리의 코드를 필요할 때 호출하여 사용합니다.

`DI(Dependency Injection)`을 직역하면 의존성 주입입니다. 스프링은 DI 컨테이너에 미리 객체(Bean)를 만들고 설정된 의존성을 따라서 의존성을 구성해줍니다.

Spring은 IoC와 DI를 통해 객체를 생성하고 생성자 인자에 넣어 의존성을 만드는 책임을 개발자가 아니라 Spring이 책임집니다. 그래서 개발자는 좀 더 객체지향적인 코딩을 할 수 있고 로직에 집중할 수 있습니다. 

**2. AOP(Aspect Oriented Programming)**

`AOP`는 관점 지향 프로그래밍을 의미합니다. 코딩을 하다보면 비즈니스로직과 관점이 다르지만 공통적으로 중복되어 꼭 들어가는 코드들이 있습니다. 로그, 트랜잭션, 유효성 검사가 그 예입니다. 이러한 코드들은 관심사가 다르기 때문에 응집도를 떨어뜨리고 코드 중복이 많아진다는 단점이 있습니다. 

`AOP`는 이러한 문제를 해결하기 위해 등장했습니다. 비즈니스라는 종단 관심사들을 가로지르는 공통 코드, 즉 횡단 관심사를 분리해서 모듈을 만들어 응집도를 높이고 코드 중복을 낮추는 프로그래밍 방법입니다.

예를 들어 우리가 자주 사용하는 `@Transactional`는 내부적으로 AOP를 통해 트랜잭션 처리 코드가 전 후로 수행됩니다. 포인트컷 정보로 활용되어 실제 객체 빈이 생성된 이후 후처리기에 의해 프록시 객체로 대체되어 DI 됩니다. 

**3. PSA(Portable Service Abstraction)**

`PSA`는 편하게 사용할 수 있는 서비스 추상화를 의미합니다. 스프링의 코드는 철저히 SOLID 원칙을 지키고 있기 때문에 인터페이스가 잘 만들어져 있습니다. **구현체가 아니라 인터페이스를 의존**하고 있기 때문에 개발자는 코드를 수정할 필요 없이 설정만 바꾸어 쉽게 구현체를 바꿀 수 있습니다. 지원되는 외부 라이브러리들도 많기 때문에 유연한 구조의 개발이 가능해집니다. 

추가적으로 Spring의 DI와 PSA를 이용하면 테스트를 용이하게 만들 수도 있습니다. 예를 들어 Mocking하고 싶은 서비스를 추상화 시키고 테스트 시 가짜 Service를 DI하는 식으로 테스트하기 쉬운 코드로 만들 수 있습니다.