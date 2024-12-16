# 1. 새로운 인프라 환경이 온다.

## 1.1. 컨테이너 인프라 환경이란
컨테이너 인프라 환경이란 컨테이너를 중심으로 구성된 인프라 환경이다.
컨테이너는 하나의 운영 체제 커널에서 다른 프로세스에 영향을 받지 않고 독립적으로 실행되는 프로세스 상태를 의미한다.

### 1.1.1 모놀리식 아키텍처
하나의 큰 목적이 있는 서비스 또는 애플리케이션에 여러 기능이 통합돼 있는 구조이다.

* 장점
  * 소프트웨어가 하나의 결합된 코드로 구성되기 때문에 초기 단계에서 설계하기 용이하며 개발이 단순하고 코드관리가 간편하다.
* 단점
  * 소프트웨어가 점점 커질 수록 서비스간 관계가 복잡해지고 특정 서비스가 전체 서비스에 영향을 줄 수 도 있다.

이런 문제의 해결 방안으로 마이크로서비스 아키텍처가 등장했다.

### 1.1.2. 마이크로서비스 아키텍처
시스템 전체가 하나의 목적을 지향하는 바는 모놀리식 아키텍처와 동일하다.
하지만 개별 기능을 하는 작은 서비스를 각각 개발해 연결하는 데서 차이가 보인다.

* 장점
  * 개발된 서비스를 재사용하기 쉽다.
  * 다른 서비스에 영향을 미칠 가능성이 줄어들며 사용량의 변화에 따라 특정 서비스만 확장할 수 있다.
* 단점
  * 모놀리식 아키텍처보다 복잡도가 높다.
  * 각 서비스가 서로 통신하는 구조로 설계되기 때문에 네트워크를 통한 호출 횟수가 증가해 성능에 영향을 줄 수 있다.

### 1.1.3 컨테이너 인프라 환경에 적합한 아키텍처
컨테이너 인프라 환경은 특히 마이크로서비스 아키텍처로 구현하기에 적합하다.
컨테이너를 서비스 단위로 포장해서 손쉽게 배포하고 확장할 수 있다.

## 1.2. 컨테이너 인프라 환경을 지원하는 도구
컨테이너 인프라 환경은 크게 `컨테이너`, `컨테이너 관리`, `개발 환경 구성 및 배포 자동화`, `모니터링`으로 구성된다.

### 1.2.1 도커
도커는 컨ㄴ테이너 환경에서 독립적으로 애플리케이션을 실행할 수 있도록 컨테이너를 만들고 관리하는 것을 도와주는 컨테이너 도구이다.
컨테이너 도구는 도커 외에도 컨테이너디, 크라이오, 파드맨 등이 있지만 가상 많이 사용되는 소프트웨어는 도커이다.

### 1.2.2 쿠버네티스
쿠버네티스는 다수의 컨테이너를 관리하는데 사용한다. 
처음에는 다수의 컨테이너를 관리하는 도구였지만, 지금은 컨테이너 인프라에 필요한 기능을 통합하고 관리하는 솔루션으로 발전했다.
컨테이너 관리 도구는 도커 스웜, 메소스, 노마드 등도 있지만 쿠버네티스만 급격한 상승세를 보이고 있다.

### 1.2.3 젠킨스
젠킨스는 지속적 통합과 지속적 배포를 지원합니다.
지속적 통합과 지속적 배포는 개발한 프로그램의 빌드, 테스트, 패키지화, 배포 단계를 모두 자동화해 개발 단계를 표준화 한다.
지속적 통합과 배포를 관리하는 도구는 뱀부, 깃허브 액션, 팀시티 등 도 있지만 젠킨스가 가장 유명하고 대표적이다.

### 1.2.4 프로메테우스와 그라파나
프로메테우스와 그라파나는 모니터링을 위한 도구이다.
프로메테우스는 상태 데이터를 수집하고, 그라파나는 프로메테우스로 수집한 데이터를 시각화 한다.
프로메테우스 외의 모니터링 데이터 수집도구는 데이터독, 인플럭스DB, 뉴 렐릭 등이 있다.
그라파나 외의 데이터 시각화 도구는 키바나, 크로노래프 등이 있다.

---

# 2. 테스트 환경 구성하기

---
# 3. 컨테이너를 다루는 표준 아키텍처, 쿠버네티스

---
# 4. 쿠버네티스를 이루는 컨테이너 도우미, 도커

---
# 5. 지속적 통합과 배포 자동화, 젠킨스

---
# 6. 안정적인 운영을 완성하는 모니터링, 프로메테우스와 그라파나
