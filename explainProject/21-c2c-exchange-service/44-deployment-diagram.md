# Deployment Diagram

UML 사용 배포 흐름도 작성

## 배포 다이어그램

<img src="https://github.com/Peoplestone2021/TIL/blob/main/explainProject/21-c2c-exchange-service/images/deploy_diagram.PNG?raw=true" width="100%" title="deployment diagram" alt="deployment_diagram"></img><br />

- 각 서버, 클라이언트, DB, API를 Device단위로 분류하여 도식화함
- 콤포넌트 간 의존성은 점선, 디바이스 간 연결은 실선으로 표현
- ORM은 의존성과 같은 형태로 표현했는데 만족스럽지 않음

### Explain

Client는 프론트엔드 서버 80포트로 접근함.
프론트엔드 서버는 현재 라우팅테이블 설정을 변경하여 80포트 접속 시도 시 3000번 포트로 이어줌. 이유는 다음과 같음.

- 서버 상에서 Pages 빌드하는 시점, 80번 포트가 사용 중인 문제가 발생
- 리버스 프록시를 적용하는 등 다른 방법도 있으나 관리자 권한 실행이 어려운 문제가 있어 라우팅테이블만 변경함

이후 Browser는 프론트엔드 서버에서 JS클라이언트를 받아와 백엔드와 직접 통신하는 방식임. 백엔드 디바이스들은 Entity를 생성하거나 업데이트 또는 삭제하고, 객체들을 DB와 JPA를 통해 관계형 맵핑하는 구조로 구성
