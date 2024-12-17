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

## 2.1 테스트 환경을 자동으로 구성하는 도구

### 2.1.1 버추얼박스
버추얼박스는 현존하는 대부분의 운영 체제를 게스트 운영 체제로 사용할 수 있다.

## 2.1.2 베이그런트로 랩 환경 구축하기
베이그런트는 사용자의 요구에 맞게 시스템 자원을 할당, 배치, 배포해 두었다가 필요할 때 시스템을 사용할 수 있는 상태로 만들어 준다.
이를 프로비저닝(Provisioning)이라 한다.

## 2.1.3 베이그런트 구성하고 테스트 하기
* 자주 사용하는 베이그런트 명령어

`vagrant init`: 프로비저닝을 위한 기초 파일을 생성한다.  
`vagrant up`: Vagrantfile을 읽어 들여 프로비저닝을 진행한다.  
`vgrant halt`: 베이그런트에서 다루는 가상 머신을 종료 합니다.   
`vagrant destroy`: 베이그런트에서 관리하는 가상 머신을 삭제한다.  
`vagrant ssh`: 베이그렌트에서 관리하는 가상 머신에 ssh로 접속한다.   
`vagrant provision`: 베이그런트에서 관리하는 가상 머신에 변경된 설정을 적용한다. 

1. `vagrant init`
   * `Vagrantfile`이 생성된다.
2. `vagrant up`
   * 명령 프롬프트에서 vagrant up을 실행
   * 에러 발생 -> 'base'로 명시돼 있으나 베이그런트가 해당 이미지를 찾지 못해 발생하는 에러
3. 에러가 발생하지 않게 운영체제 이미지를 선택(학습에는 `sysnet4admin/CentOS-k8s` 사용)
4. `Vagrantfile`의 `config.vm.box="base"`를 `config.vm.box="sysnet4admin/CentOS-k8s"` 수정
5. `vagrant up`
6. 버추얼박스에 VM이 설치되었는지 확인
7. `vagrant ssh`로 VM에 접속
8. `vagrant destory -f` VM 삭제

## 2.2 베이그런트로 테스트 환경 구축하기
Vagrantfile을 수정해 원하는 구성이 자동으로 CentOS에 입력되도록 해보겠다.

## 2.2.1 가상 머신에 필요한 설정 자동으로 구성하기
Vagrantfile은 `ruby`라는 언어로 작성한다.

```ruby
# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure("2") do |config|
  config.vm.define "m-k8s" do |cfg|
    cfg.vm.box = "sysnet4admin/CentOS-k8s"
    cfg.vm.provider "virtualbox" do |vb|
      vb.name = "m-k8s(github_SysNet4Admin)"
      vb.cpus = 2
      vb.memory = 2048
      vb.customize ["modifyvm", :id, "--groups", "/k8s-SM(github_SysNet4Admin)"]
    end
    cfg.vm.host_name = "m-k8s"
    cfg.vm.network "private_network", ip: "192.168.1.10"
    cfg.vm.network "forwarded_port", guest: 22, host:60010, auto_corrent: true, id: "ssh"
    cfg.vm.synced_folder "../data", "/vagrant", disabled: true
  end
end
```
* 1~2번 라인: 현재 파일이 루비임을 인식하게 하는 호환 코드. `ft`는 파일 종류(file type)의 약자이며 해당 내용은 실행에 아무런 영향을 미치지 않는다.
* 3번 라인: "2"는 베이그런트에서루비로 코드를 읽어 들여 실행할 때 작동하는 API 버전이고, 뒤에 `do |config|`는 베이그런트 설정의 시작을 알린다.
* 4번 라인: 버추얼박스에서 보이는 가상 머신을 `m-k8s`로 정의. `do |cfg|`를 추가해 원하는 설정으로 변경. `do |이름|`으로 시작한 작업은 `end`로 종료한다.
* 5번 라인: 기본값 `config.vm.box`를 `do |cfg|`에 적용한 내용을 받아 `cfg.vm.box`로 변경한다.
* 6번 라인: 베이그런트의 프로바이더가 버추얼박스라는 것을 정의한다. 프로바이더는 베이그런트를 통해 제공되는 코드가 실제로 가상 머신을 배포되게 하는 소프트웨어이다. 다음으로 버추얼박스에 필요한 설정을 정의하는데 그 시작을 `do |vb|`로 선언한다.
* 7~11 라인: 버추얼박스에 생선한 가상 머신의 이름, CPU, MEMORY, 소속된 그룹을 명시, `end`로 설정 종료
* 12번 라인: 가상 머신 자체에 대한 설정으로 `do |cfg|`에 속한 작업 호스트의 이름을 `m-k8s`로 설정
* 13번 라인: 호스트 전용 네트워크를 `private_network`로 설정해 eth1 인터페이스를 호스트 전용으로 구성하고 IP는 `192.168.1.10`으로 지정
* 14번 라인: ssh 통신은 호스트 60010번을 게스트 22번으로 포트포워딩. `auto_corrent: true` 설정을 통해 포트가 중복되면 포트가 자동으로 변경되도록 설정.
* 15번 라인: 호스트와 게스트 사이에 디렉터리 동기화가 이뤄지지 않게 설정
* 16~17 라인: 설정 작업 (do |config|, do |cfg|)이 종료되었음을 `end` 구문으로 명시

## 2.2.2 가상 머신에 추가 패키지 설치하기
Vagrantfile을 통해 CentOS에 호스트 네임, IP 등을 자동으로 설정했다. 이번에는 CentOS에 필요한 패키지를 설치해보겠다.

1. Vagrantfile 수정
```ruby
# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure("2") do |config|
  config.vm.define "m-k8s" do |cfg|
    cfg.vm.box = "sysnet4admin/CentOS-k8s"
    cfg.vm.provider "virtualbox" do |vb|
      vb.name = "m-k8s(github_SysNet4Admin)"
      vb.cpus = 2
      vb.memory = 2048
      vb.customize ["modifyvm", :id, "--groups", "/k8s-SM(github_SysNet4Admin)"]
    end
    cfg.vm.host_name = "m-k8s"
    cfg.vm.network "private_network", ip: "192.168.1.10"
    cfg.vm.network "forwarded_port", guest: 22, host:60010, auto_corrent: true, id: "ssh"
    cfg.vm.synced_folder "../data", "/vagrant", disabled: true
    cfg.vm.provision "shell", path: "install_pkg.sh"
  end
end
```
* 16번 라인: `vm.provision "shell"` 구문으로 경로(path)에 있는 install_pkg.sh를 게스트 내부에서 호출해 실행되도록 한다.

2. 스크립트 작성
```shell
#!/usr/bin/env bash
# install packages
yum install epel-release -y
yum install vim-enhanced -y
```
Vagrantfile이 위치한 디렉터리에 추가 패키지를 설치하기 위한 스크립트를 다음과 같이 작성하고 `install_pkg.sh`라는 이름으로 저장한다.

3. `vagrant provision` 명령어 실행

## 2.3 터미널 프로그램으로 가상 머신 접속하기



---
# 3. 컨테이너를 다루는 표준 아키텍처, 쿠버네티스

---
# 4. 쿠버네티스를 이루는 컨테이너 도우미, 도커

---
# 5. 지속적 통합과 배포 자동화, 젠킨스

---
# 6. 안정적인 운영을 완성하는 모니터링, 프로메테우스와 그라파나
