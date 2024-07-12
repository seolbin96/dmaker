# DMaker

## 소개

---
DMaker는 Spring Boot를 사용하여 간단한 개발자 관리 애플리케이션을 구현한다. 이 애플리케이션은 REST API를 통해 개발자 정보를 관리하며, 개발자의 레벨과 스킬 타입을 정의하는 Enum 타입을 사용한다.

## 프로젝트 구조

---
이 프로젝트는 다음과 같은 주요 구성 요소로 이루어져 있다:

- `Developer`: 개발자 정보를 저장하는 엔티티 클래스
- `DMakerController`: REST API 엔드포인트를 정의하는 컨트롤러 클래스
- `DeveloperRepository`: 개발자 정보를 데이터베이스에 저장하고 조회하는 리포지토리 인터페이스
- `DMakerService`: 비즈니스 로직을 처리하는 서비스 클래스
- `DeveloperLevel`, `DeveloperSkillType`: 개발자의 레벨과 스킬 타입을 정의하는 Enum 클래스

---

### Developer 엔티티 클래스
데이터베이스 테이블의 구조를 정의한다.
- `developerLevel`, `developerSkillType`, `experienceYears`, `memberId`, `name`, `age` 등의 필드를 포함한다.
- `createdAt`, `updatedAt` 필드를 통해 생성 및 수정 시간을 기록한다.

### DMakerController 클래스
REST API 엔드포인트를 정의한다.
- `/developers` 경로로 GET 요청이 오면 개발자 목록을 반환한다.
- `/create-developer` 경로로 GET 요청이 오면 개발자를 생성하고 특정 개발자를 리스트로 반환한다.

### DeveloperRepository 인터페이스
`Developer` 엔티티를 데이터베이스에 CRUD 작업을 할 수 있는 리포지토리로 정의한다.
- `JpaRepository<Developer, Long>`를 상속받아 기본적인 데이터베이스 작업을 수행한다.

### DMakerService 클래스
비즈니스 로직을 처리한다.
- `createDeveloper()` 메소드를 통해 `Developer` 객체를 생성하고 데이터베이스에 저장한다.

### DeveloperLevel 및 DeveloperSkillType 열거형
개발자의 레벨 및 스킬 타입을 정의한다.
- `DeveloperLevel`은 `NEW`, `JUNIOR`, `JUNGNIOR`, `SENIOR`의 네 가지 레벨을 정의한다.
- `DeveloperSkillType`은 `BACK_END`, `FRONT_END`, `FULL_STACK`의 세 가지 스킬 타입을 정의한다.

<br>

> H2DB를 이용해서 간단하게 데이터 저장이나 조작을 테스트해볼 수 있다.
이걸 하기 위해서 Entity라는 특수한 타입의 클래스를 만들어준다.
Entity를 영속하기 위해 Repository 인터페이스를 만들어 서비스에서 호출하고,
컨트롤러에서 이 요청을 받았을 때 createDeveloper를 호출해주도록 해서 Developer라는 Entity의 객체를 Repository에서 세이브 및 영속화
-> H2DB에 저장이 되고 저장된 데이터를 H2 콘솔을 이용해서 확인해볼 수 있다.
