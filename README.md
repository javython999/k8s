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

### 2.1.2 베이그런트로 랩 환경 구축하기
베이그런트는 사용자의 요구에 맞게 시스템 자원을 할당, 배치, 배포해 두었다가 필요할 때 시스템을 사용할 수 있는 상태로 만들어 준다.
이를 프로비저닝(Provisioning)이라 한다.

### 2.1.3 베이그런트 구성하고 테스트 하기
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

### 2.2.1 가상 머신에 필요한 설정 자동으로 구성하기
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

### 2.2.2 가상 머신에 추가 패키지 설치하기
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

### 2.2.3 가상 머신 추가 구성

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
    cfg.vm.provision "file", source: "ping_2_nds.sh", destination: "ping_2_nds.sh"
    cfg.vm.provision "shell", path: "config.sh"
  end

  #=============#
  # Added Nodes #
  #=============#

  (1..3).each do |i| # 1부터 3까지 3개의 인자를 반복해 i로 입력
    config.vm.define "w#{i}-k8s" do |cfg|
      cfg.vm.box = "sysnet4admin/CentOS-k8s"
      cfg.vm.provider "virtualbox" do |vb|
        vb.name = "w#{i}-k8s(github_SysNet4Admin)"
        vb.cpus = 1
        vb.memory = 1024
        vb.customize ["modifyvm", :id, "--groups", "/k8s-SM(github_SysNet4Admin)"]
      end
      cfg.vm.host_name = "w#{i}-k8s"
      cfg.vm.network "private_network", ip: "192.168.1.10#{i}"
      cfg.vm.network "forwarded_port", guest: 22, host: "6010#{i}", auto_corrent: true, id: "ssh"
      cfg.vm.synced_folder "../data", "/vagrant", disabled: true
      cfg.vm.provision "shell", path: "install_pkg.sh"
    end
  end
end
```
* 18 라인: 파일을 게스트 운영체제에 전달하기 위해 "shell"이 아닌 "file" 구문으로 변경.
* 19 라인: `config.sh`를 게스트에서 실행
* 26~37 라인: 추가한 3대의 CentOS에 대한 구성 

```shell
#!/usr/bin/env bash
# install packages
yum install epel-release -y
yum install vim-enhanced -y
```

```shell
# ping 3 times per nodes
pring 192.168.1.101 -c 3
pring 192.168.1.102 -c 3
pring 192.168.1.103 -c 3
```

```shell
#!/usr/bin/env bash
# modfiy permission
chmod 744 ./ping_2_nds.sh
```

1. `vagrant up` 실행
2. `vagrant ssh m-k8s`
3. `./ping_2_nds.sh`
4. `exit`

---
# 3. 컨테이너를 다루는 표준 아키텍처, 쿠버네티스
**컨테이너 인프라 환경**이란 리눅스 운영 체제의 커널 하나에서 여러 개의 컨테이너가 격리된 상태로 실행되는 인프라 환경을 말한다.
가상화 환경에서는 각각의 가상 머신이 모두 독립적인 운영 체제 커널을 가지고 있어야 하기 때문에 그만큼 자원을 더 소모해야 하고 성능이 떨어진다.
하지만 컨테이너 인프라 환경은 운영 체제 커널 하나에 컨테이너 여러 개가 격리된 형태로 실행되기 때문에 자원을 효율적으로 사용할 수 있고 거치는 단계가 적어 속도도 빠르다.

## 3.1 쿠버네티스 이해하기
쿠버네티스는 컨테이너 오케스트레이션을 위한 솔루션이다.
오케스트레이션이란 복잡한 단계를 관리하고 요소들의 유기적인 관계를 미리 정의해 손쉽게 사용하도록 서비스를 제공하는 것을 의미한다.

### 3.1.1 왜 쿠버네티스일까?
다른 오케스트레이션 솔루션보다는 시작하는데 어려움이 있지만, 쉽게 사용할 수 있도록 도와주는 도구들이 있어 설치가 쉬워지는 추세.
모든 벤더와 오픈 소스 진영 모두에서 쿠버네티스를 지원하고 그에 맞게 통합 개발하고 있다.
다양한 종류의 솔루션이 쿠버네티스에 통합되고 있다.

### 3.1.2 쿠버네티스 구성 방법
1. 퍼블릭 클라우드 업체에서 제공하는 관리형 쿠버네티스인 EKS(Amazon Elastic Kubernates Service), AKS(Azure Kubernetes Service), GKE(Google Kubernetes Engine) 등을 사용한다. 구성이 이미 다 갖춰져 있고 마스터 노드를 클라우드 업체에서 관리하기 때문에 학습용으로는 적합하지 않다.
2. 수세의 Rancher, 레드햇의 OpenShift와 같은 플랫폼에서 제공하는 설치형 쿠버네티스를 사용. 유료라 쉽게 접근하기 어렵다.
3. 사용하는 시스템에 쿠버네티스 클러스터를 자동으로 구성해주는 솔루션을 사용. 주요 솔루션으로는 kubeadm, kops(Kubernetes Operations), KRIB(Kubernetes Rebar Integrated Bootstrap), kuberspray가 있다.

### 3.1.3 쿠버네티스 구성하기
### 3.1.4 파드 배포를 중심으로 쿠버네티스 구성 요소 살펴보기
0. `kubectl`: 쿠버네티스 클러스터에 명령을 내리는 역할. 다른 구성요소와 다르게 바로 실행되는 명령 형태인 바이너리로 배포되기 때문에 마스터 노드에 있을 필요는 없지만 통상적으로 API 서버와 주로 통신 하므로 API 서버가 위치한 마스터 노드에 구성했다.
1. `API 서버`: 쿠버네티스 클러스터의 중심 역할을 하는 통로. 주로 상태 값을 저장하는 etcd와 통신하지만, 그 밖의 요소들 또한 API 서버를 중심에 두고 통신한다.
2. `etcd`: 구성 요소들의 상태 값이 모두 저장되는 곳. 실제로 etcd 외의 다른 구성 요소는 상태 값을 관리하지 않는다. 그러므로 etcd의 정보만 백업돼 있다면 긴급한 장애 상황에서도 쿠버네티스 클러스터는 복구할 수 있다.
3. `컨트롤 매니저`: 쿠버네티스 클러스터의 오브젝트 상태를 관리한다. 예를 들어 워커 노드에서 통신이 되지 않는 경우, 상태 체크와 복구는 컨트롤러 매니저에 속한 노드 컨트롤러에서 이루어진다.
4. `스케줄러`: 노드의 상태와 자원, 레이블, 요구 조건 등을 고려해 파드를 어떤 워커 노드에 생성할 것인지를 결정하고 할당 한다.
5. `kubelet`: 파드의 구성 내용(PodSpec)을 받아서 컨테이너 런타임으로 전달하고, 파드 안의 컨테이너들이 정상저그로 작동하는지 모니터링 한다.
6. `컨테이너 런타임(CRI, Container Runtime Interface)`: 파드를 이루는 컨테이너의 실행을 담당한다. 
7. `파드(Pod)`: 한 개 이상의 컨테이너로 단일 목적의 일을 하기 위해서 모인 단위.

8. `네트워크 플러그인`: 쿠버네티스 클러스터의 통신을 위해서 네트워크 플러그인을 선택하고 구성해야 한다. 네트워크 플러그인은 일반적으로 CNI로 구성하는데, 주로 사용하는 CNI에는 캘리코(Calico), 플래널(Flannel), 실리움(Cilium), 큐브 라우터(Kube-router), 로마나(Romana), 위브넷(WeaveNet), Canal이 있다.
9. `CoreDNS`: 클라우드 네이티브 컴퓨팅 재단에서 보증하는 프로젝트로, 빠르고 유연한 DNS 서버이다.

### 3.1.5 파드의 생명주기로 쿠버네티스 구성 요소 살펴보기
생명주기(Life cycle)는 파드가 생성, 수정, 삭제되는 과정을 나타냅니다.

1. kubectl을 통해 API 서버에 파드 생성을 요청한다.
2. API 서버에 전달된 내용이 있으면 API 서버는 etcd에 전달된 내용을 모두 기록해 클러스터의 상태 값을 최신으로 유지한다. 따라서 각 요소가 상태를 업데이트 할 때마다 API 서버를 통해 etcd에 기록된다.
3. API 서버에 파드 생성이 요청된 것을 컨트롤러 매니저가 인지하면 컨트로러 매니저는 파드를 생성하고, 이 상태를 API 서버에 전달한다.
4. API 서버에 파드가 생성됐다는 정보를 스케줄러가 인지한다. 스케줄러는 생성된 파드를 어떤 워커 노드에 적용할지 조건을 고려해 결정하고  해당 워커 노드에 파드를 띄우도록 요청한다.
5. API 서버에 전달된 정보대로 지정한 워커 노드에 파드가 속해 있는지 스케줄러가 kubelet으로 확인한다.
6. kubelet에서 컨테이너 런타임으로 파드 생성을 요청한다.
7. 파드가 생성된다.
8. 파드가 사용 가능한 상태가 된다.

## 3.2 쿠버네티스 기본 사용법

### 3.2.1 파드를 생성하는 방법
1. `kubectl run`명령을 실행하면 쉽게 파드를 생성할 수 있다. run 다음 나오는 `nginx`는 파드의 이름이고 `--image=nginx`는 생서할 이미지의 이름이다.

```shell
kubectl create deployment dpy-nginx --image=nginx
```

2. `kubectl create`. `create`로 파드를 생성하려면 `kubectl create`에 `deployment`를 추가해서 실행해야 한다.
```shell
kubectl run nginx --image=nginx
```
`run`명령을 실행하면 쉽게 파드를 생성할 수 있는데 왜 `kubectl create`명령을 사용할까?

`run`으로 파드를 생성하면 1개만 생성되고 관리된다. `create deployment`로 파드를 생성하면 `디플로이먼트`라는 관리 그룹 내에서 파드가 생성된다.

> 쿠버네티스 1.18 버전부터는 create로 생성을 권고하고 있다.

### 3.2.2 오브젝트란
쿠버네티스를 사용하는 관점에서 파드와 디플로이먼트는 `스펙`과 `상태` 등의 값을 가지고 있다. 이러한 값을 가지고 있는 파드와 디플로이먼트를 개별 속성을 포함해 부르는 단위를 `오브젝트`라고 한다.
쿠버네티스는 여러 유형의 오브젝트를 제공한다.

1. 기본 오브젝트
   * 파드(Pod): 쿠버네티스에서 실행되는 최소 단위, 독립적인 공간과 사용 가능한 IP를 가지고 있다.
   * 네임스페이스(Namespaces): 쿠버네티스 클러스터에서 사용되는 리소스들을 구분해 관리하는 그룹이다. 특별히 지정하지 않으면 `default`가 할당된다. 쿠버네티스 시스템에서 사용되는 `kube-system`, 온프레미스에서 쿠버네티스를 사용할 경우 외부에서 쿠버네티스 클러스터 내부로 접속하게 도와주는 컨테이너들이 속해있는 `metallb-system`이 있다.
   * 볼륨(Volume): 파드가 생성될 때 파드에서 사용할 수 있는 디렉터리를 제공한다. 파드는 영속되는 개념이 아니라 제공되는 디렉터리를 임시로 사용한다. 파드가 사라지더라도 데이터를 저장과 보존을 할 경우 볼륨 오브젝트를 생성하고 사용할 수 있다.
   * 서비스(Service): 파드는 클러스터 내에서 유동적이기 때문에 접속 정보가 고정일 수 없다. 따라서 파드 접속을 안정적으로 유지하도록 서비스를 통해 내/외부로 연결된다. 기존 인프라에서 로드밸런서, 게이트웨이와 비슷한 역할을 한다.
2. 디플로이먼트
   * 기본 오브젝트로만으로도 쿠버네티스를 사용할 수 있다. 하지만 한계가 있어 이를 좀더 효율적으로 작동하도록 기능들을 조합하고 추가해 구현한 것이 디플로이먼트다.
   * 이 외에도 데몬셋, 컨피그맵, 레플리카셋, PV(PersistentVolume), PVC(PersistentVolumeClaim), 스테이풀셋 등이 있다.

### 3.2.3 레플리카셋으로 파드 수 관리하기
많은 사용자를 대상으로 웹 서비스를 하려면 다수의 파드가 필요한데, 이를 하나씩 생성하는 것은 비효율적이다. 쿠버네티스에서는 다수의 파드를 만드는 레플리카셋 오브젝트를 제공한다.
파드를 3개 만들겠다고 레플리카셋에 선언하면 컨트롤러 매니저와 스케줄러가 워커 노드에 파드 3개를 만들도록 선언한다. 레플리카셋은 파드 수를 보장하는 기능만 제공하기에 롤링 업데이트 등의 기능이 추가된 디플로이먼트를 사용해서 파드 수를 관리하기를 권장한다.

```shell
kubectl scale pod nginx-pod --replicas=3
```
`nginx-pod`는 `run`으로 생성했기에 `deployment`에 속하지 않는다. 그래서 리소스를 확인할 수 없다는 에러가 발생한다.

```shell
kubectl scale deployment dpy-nginx --replicas=3
```

### 3.2.4 스펙을 지정해서 오브젝트 생성하기
`kubectl create deployment`명령으로 디플로이먼트를 생성하긴 했지만, 1개의 파드만 만들어졌다. `create`에서는 `replicas`옵션을 사용할 수 없고, `scale`은 이미 만들어진 디플로이먼트에서만 사용할 수 있다.
이런 설정을 적용하려면 필요한 내용을 파일로 작성해야 한다. 이때 작성하는 파일을 `오브젝트 스펙`이라고 한다. 오브젝트 스펙은 yaml(야믈) 문법으로 작성한다.

```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: echo-hname
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
        - name: echo-hname
          image: sysnet4admin/echo-hname
```

```shell
kubectl create -f ~/_Book_k8sInfra/ch3/3.2.4/echo-hname.yaml
```
오브젝트 스펙에 설정한 내용대로 디플로이먼트가 생성된다.
오브젝트 스펙 파일을 변경후 `kubectl create -f ~/_Book_k8sInfra/ch3/3.2.4/echo-hname.yaml` 실행하면 에러가 발생한다.   
`Error from server (AlreadyExists): error when creating "/root/_Book_k8sInfra/ch3/3.2.4/echo-hname.yaml": deployments.apps "echo-hname" already exists`
배포된 오브젝트의 스펙을 변경하고 싶을 때에는 어떻게 해야할까? 지우고 다시 만들어야 할까?

### 3.2.5 apply로 오브젝트 생성하고 관리하기
앞서 확인한 것처럼 파일의 변경사항을 바로 적용할 수 없다는 단점이 있다. 이런 경우를 위해 쿠버네티스는 `apply` 명령어를 제공한다.
```shell
kubectl apply -f ~/_Book_k8sInfra/ch3/3.2.4/echo-hname.yaml
```

### 3.2.6 파드의 컨테이너 자동 복구 방법
쿠버네티스는 거의 모든 부분이 자동 복구되도록 설계됐다. 특히 파드의 자동 복구 기술은 `셀프 힐링(self-healing)`이라고 하는데, 제대로 작동하지 않는 컨테이너를 다시 시작하거나 교체해 파드가 정상적으로 작동하게 한다.

1. 파드 IP 확인
```shell
kubectl get pods -o wide 
```
2. 파드 접속
```shell
kubectl exec -it nginx-pod -- /bin/bash
```
3. nginx 프로세스 ID 확인
```shell
cat /run/nginx.pid
```

4. nginx에 지속적으로 요청 보내기
```shell
i=1; while true; do sleep 1; echo $((i++)) `curl --silent 172.16.132.4 | grep title`; done
```

5. nginx kill
```shell
kill 1
```
6. self-healing 확인
```shell
kubectl get pods
```

### 3.2.7 파드의 동작 보증 기능
쿠버네티스는 파드 자체에 문제가 발생하면 파드를 자동 복구해서 파드가 항상 동작하도록 보장하는 기능도 있다.

1. 파드에 문제가 있는 상황을 만들기 위해 생성한 파드를 삭제한다.
```shell
kubectl get pods
kubectl delete pods nginx-pod
```

2. 파드의 동작을 보증하려면 어떤 조건이 필요하다. 어떤 조건인지 확인해보기 위해 다른 파드도 삭제해 서로 비교해보자.
```shell
kubectl delete pod echo-hname-7894b67f-2xb6n
```
3. 파드 조회
```shell
kubectl get pods
```
아직도 6개의 파드가 존재한다. 그런제 삭제했던 `echo-hname-7894b67f-2xb6n`는 없다. nginx-pod는 디플로이먼트에 속한 파드가 아니며 어떤 컨트롤러도 이 파드를 관리하지 않는다.
따라서 nginx-pod가 삭제되고 다시 생성되지도 않는다. `echo-hname-7894b67f-2xb6n`는 디플로이먼트에 속한 파드이다.
앞에서 replicas를 6으로 선언했다. replicas는 파드를 선언한 수대로 유지하도록 파두의 수를 항상 확인하고 부족하면 새로운 파드를 만들어 낸다.
따라서 임의로 파드를 삭제하면 replicas가 삭제된 파드를 확인하고 총 개수에 맞추기 위해 파드를 생성하게 된다.

4. 디플로이먼트에 속한 파드는 사우이 디플로이먼트를 삭제해야 파드가 삭제된다.
```shell
kubectl delete deployment echo-hname
```

### 3.2.8 노드 자원 보호하기
쿠버네티스는 파드를 안정적으로 작동하도록 관리한다는 것을 알았다. 그렇다면 노드는 어떤 식으로 관리할까?
우선 노드의 목적을 명확히 해야 한다. 노든느 쿠버네티스 스케줄러에서 파드를 할당받고 처리하는 역할을 한다.    

몇 차례 문제가 생긴 노드에 파드를 할당하면 문제가 생길 가능성이 높다. 이런 경우에는 영향도가 적은 파드를 할당해 일정 기간 사용하면서 모니터링 해야 한다.
즉, 노드에 문제가 생기더라도 파드의 문제를 최소화해야 한다. 하지만 쿠버네티스는 모든 노드에 균등하게 파드를 할당하려고 한다.     
이렇게 문제가 생길 가능성이 있는 노드라는 것을 쿠버네티스에게 알려주면 좋을 것이다.

쿠버네티스에는 이런 경우 `cordon` 기능을 사용한다.

1. deployment 배포
```shell
kubectl create -f ~/_Book_k8sInfra/ch3/3.2.8/echo-hname.yaml
```

2. replicas 9개로 설정
```shell
kubectl scale deployment echo-hname --replicas=9
```

3. 배포된 pod 확인
```shell
kubectl get pods -o wide
```
w1-k8s, w2-k8s, w3-k8s 각각 3개씩 파드가 생성되었다.


4. scale로 파드의 수 3개로 줄이기
```shell
kubectl scale deployment echo-hname --replicas=3
```
w1-k8s, w2-k8s, w3-k8s 각각 1개씩 파드가 생성되었다.

5. w3-k8s노드에 문제가 자주 발생해 현재 상태를 보존해야 한다고 가정하자. w3-k8s에 `cordon` 명령을 실행한다.
```shell
kubectl cordon w3-k8s
```

6. `kubectl get nodes`명령을 실행해 `cordon` 명령이 제대로 적용됐는지 확인한다.
```shell
kubectl get nodes
```

```shell
NAME     STATUS                     ROLES    AGE   VERSION
m-k8s    Ready                      master   24h   v1.18.4
w1-k8s   Ready                      <none>   24h   v1.18.4
w2-k8s   Ready                      <none>   24h   v1.18.4
w3-k8s   Ready,SchedulingDisabled   <none>   24h   v1.18.4
```
w3-k8s가 더 이상 파드가 할당되지 않는 상태로 변경됐다.
이처럼 `cordon`명령을 실행하면 해당 노드에 파드가 할당되지 않게 스케줄되지 않는 상태(SchedulingDisabled)라는 표시를 한다.

7. 이 상태에서 파드 수를 9개로 늘린다.
```shell
kubectl scale deployment echo-hname --replicas=9
```
```shell
NAME                        READY   STATUS    RESTARTS   AGE   IP               NODE     NOMINATED NODE   READINESS GATES
echo-hname-7894b67f-7q8dp   1/1     Running   0          11m   172.16.132.9     w3-k8s   <none>           <none>
echo-hname-7894b67f-grc9j   1/1     Running   0          11m   172.16.221.133   w1-k8s   <none>           <none>
echo-hname-7894b67f-hnbkb   1/1     Running   0          11m   172.16.103.132   w2-k8s   <none>           <none>
echo-hname-7894b67f-jfjdz   1/1     Running   0          22s   172.16.221.136   w1-k8s   <none>           <none>
echo-hname-7894b67f-lh9t9   1/1     Running   0          22s   172.16.221.138   w1-k8s   <none>           <none>
echo-hname-7894b67f-ln7p4   1/1     Running   0          22s   172.16.103.135   w2-k8s   <none>           <none>
echo-hname-7894b67f-mzs5t   1/1     Running   0          22s   172.16.103.137   w2-k8s   <none>           <none>
echo-hname-7894b67f-n474h   1/1     Running   0          22s   172.16.221.137   w1-k8s   <none>           <none>
echo-hname-7894b67f-wqk7t   1/1     Running   0          22s   172.16.103.136   w2-k8s   <none>           <none>
```
w3-k8s의 파드 수가 여전히 1개인 것을 확인할 수 있다.

8. 파드의 수를 3개로 줄인다.
```shell
kubectl scale deployment echo-hname --replicas=3
```

9. 각 노드에 할당 된 파드 수가 공평하게 1개씩인지 확인한다.
```shell
kubectl get pods -o wide
```

10. `uncordon` 명령으로 w3-k8s에 파드가 할당되지 않게 설정 했던 것을 해제 한다.
```shell
kubectl uncordon w3-k8s
```

11 `uncordon` 명령이 적용 됐는지 `kubectl get nodes` 명령으로 확인한다.
```shell
kubectl get nodes
```

```shell
NAME     STATUS   ROLES    AGE   VERSION
m-k8s    Ready    master   25h   v1.18.4
w1-k8s   Ready    <none>   24h   v1.18.4
w2-k8s   Ready    <none>   24h   v1.18.4
w3-k8s   Ready    <none>   24h   v1.18.4
```

### 3.2.9 노드 유지보수하기
유지보수를 위해 노드를 꺼야하는 상황이 발생한다. 이런 경우를 대비해 쿠버네티스는 `drain` 기능을 제공한다.
`drain`은 지정된 노드이 파드를 전부 다른 곳으로 이동시켜 해당 노드를 유지보수할 수 있게 한다.

1. `kubectl drain` 명령을 실행해 유지보수할 노드(w3-k8s)를 파드가 없는 상태로 만든다.
```shell
kubectl drain
```

```shell
node/w3-k8s cordoned
error: unable to drain node "w3-k8s", aborting command...

There are pending nodes to be drained:
 w3-k8s
error: cannot delete DaemonSet-managed Pods (use --ignore-daemonsets to ignore): kube-system/calico-node-wmntq, kube-system/kube-proxy-44v2w
```
w3-k8s에서 데몬셋을 지을 수 없어서 명령을 수행할 수 없다고 나온다.
`drain`은 실제로 파드를 옮기는 것이 아니라 노드에서 파드를 삭제하고 다른 곳에서 다시 생성한다.
그런데 DaemonSet은 각 노드에 1개만 존재하는 파드라서 drain으로는 삭제할 수 없다.

2. `drain`명령과 `ignore-daemonstes` 옵션을 함꼐 사용한다. 이옵션을 사용하면 DaemonSet을 무시하고 진행한다.
```shell
kubectl drain w3-k8s --ignore-daemonsets 
```
```shell
node/w3-k8s already cordoned
WARNING: ignoring DaemonSet-managed Pods: kube-system/calico-node-wmntq, kube-system/kube-proxy-44v2w
evicting pod default/echo-hname-7894b67f-7q8dp
pod/echo-hname-7894b67f-7q8dp evicted
node/w3-k8s evicted
```
경고가 발생하지만 모든 파드가 이동된다.

3. `kubectl get pods -o wide` w3-k8s 노드에 파드가 있는지 확인한다.
```shell
NAME                        READY   STATUS    RESTARTS   AGE     IP               NODE     NOMINATED NODE   READINESS GATES
echo-hname-7894b67f-8kfjj   1/1     Running   0          5m36s   172.16.221.140   w1-k8s   <none>           <none>
echo-hname-7894b67f-grc9j   1/1     Running   1          22h     172.16.221.139   w1-k8s   <none>           <none>
echo-hname-7894b67f-hnbkb   1/1     Running   1          22h     172.16.103.138   w2-k8s   <none>           <none>
```

4. `kubectl get nodes`를 실행해 w3-k8s 노드의 상태를 확인한다. cordon을 실행했을 때처럼 `SchedulingDisabled` 상태이다.
```shell
NAME     STATUS                     ROLES    AGE   VERSION
m-k8s    Ready                      master   47h   v1.18.4
w1-k8s   Ready                      <none>   47h   v1.18.4
w2-k8s   Ready                      <none>   47h   v1.18.4
w3-k8s   Ready,SchedulingDisabled   <none>   47h   v1.18.4
``` 
5. 유지보수가 끝났다고 가정하고 w3-k8s에 `uncordon` 명령을 실행해 스케줄을 받을 수 있는 상태로 복귀 시킨다.
```shell
kubectl uncordon w3-k8s
```
6. `kubectl get nodes`로 노드의 상태를 다시 확인한다.
```shell
kubectl get nodes
```

```shell
NAME     STATUS   ROLES    AGE   VERSION
m-k8s    Ready    master   47h   v1.18.4
w1-k8s   Ready    <none>   47h   v1.18.4
w2-k8s   Ready    <none>   47h   v1.18.4
w3-k8s   Ready    <none>   47h   v1.18.4
```

### 3.2.10 파드 업데이트하고 복구하기
파드를 운영하다보면 컨테이너의 버전을 업데이트하거나 기존 버전으로 복구해야하는 일이 발생한다.

* 파드 업데이트 하기
1. 다음 명령어로 업데이트 테스트 파드를 배포한다. `--record`는 매우 중요한 옵션으로, 배포한 정보를 히스토리에 기록한다.
```shell
kubectl apply -f ~/_Book_k8sInfra/ch3/3.2.10/rollout-nginx.yaml --record
```
2. `record` 옵션으로 기록한 히스토리는 rollout history 명령을 실행해 확인할 수 있다.
```shell
kubectl rollout history deployment rollout-nginx
```
```shell
deployment.apps/rollout-nginx 
REVISION  CHANGE-CAUSE
1         kubectl apply --filename=/root/_Book_k8sInfra/ch3/3.2.10/rollout-nginx.yaml --record=true
```
3. 배포한 파드의 정보를 확인한다.
```shell
kubectl get pods -o wide
```
4. 배포된 파더에 속해 있는 nginx 컨테이너 버전을 `curl -I` 명령으로 확인한다.
```shell
curl -I --silent 172.16.132.13 | grep Server
```
```shell
Server: nginx/1.15.12
```

5. `set image` 명령으로 파드의 nginx 컨테이너 버전을 1.16.0으로 업데이트 한다. `--record`를 명령에 포함해 실행한 명령을 기록한다.
```shell
kubectl set image deployment rollout-nginx nginx=nginx:1.16.0 --record
```
```shell
deployment.apps/rollout-nginx image updated
```
6. 업데이트한 후에 파드의 상태를 확인한다.
```shell
kubectl get pods -o wide
```
```shell
NAME                             READY   STATUS    RESTARTS   AGE   IP               NODE     NOMINATED NODE   READINESS GATES
rollout-nginx-8566d57f75-dflvk   1/1     Running   0          33s   172.16.103.140   w2-k8s   <none>           <none>
rollout-nginx-8566d57f75-j9kkc   1/1     Running   0          43s   172.16.221.142   w1-k8s   <none>           <none>
rollout-nginx-8566d57f75-zvjbp   1/1     Running   0          54s   172.16.132.14    w3-k8s   <none>           <none>
```
파드의 이름과 IP가 변경되었다. 파드는 언제라도 지우고 다시 만들 수 있다. 따라서  파드에 속한 nginx 컨테이너를 업데이트하는 가장 쉬운 방법은 파드를 관리하는 replicas의 수를 줄이고
늘려서 파드를 새로 생선하는 것이다. 이때 시스템의 영향을 최소화하기 위해 replicas에 속한 파드를 모두 한 번에 지우는 것이 아니라 파드를 하나씩 순차적으로 지우고 생성한다.
이때 파드 수가 많으면 하나씩이 아니라 다수의 파드가 업데이트 된다. 업데이트 기본값은 전체의 1/4(25%)개이며, 최소값은 1개이다.

7. nginx 컨테이너가 1.16.0으로 모두 업데이트되면 Deployment의 상태를 확인한다.
```shell
kubectl rollout status deployment rollout-nginx
```
```shell
deployment "rollout-nginx" successfully rolled out
```

8. `rollout history` 명령을 실행해 rollout-nginx에 적용된 명령들을 확인한다.
```shell
kubectl rollout history deployment rollout-nginx
```
```shell
deployment.apps/rollout-nginx 
REVISION  CHANGE-CAUSE
1         kubectl apply --filename=/root/_Book_k8sInfra/ch3/3.2.10/rollout-nginx.yaml --record=true
2         kubectl set image deployment rollout-nginx nginx=nginx:1.16.0 --record=true
```

9. `curl -I` 명령으로 업데이트가 제대로 이루어졌는지도 확인한다.
```shell
curl -I --silent 172.16.103.140 | grep Server 
```
```shell
Server: nginx/1.16.0
```

* 업데이트 실패시 복구하기
1. `set image` 명령으로 nginx의 컨테이너 버전을 의도적으로 1.17.2가 아닌 1.17.23 입력한다.
```shell
kubectl set image deployment rollout-nginx nginx=nginx:1.17.23 --record 
```
```shell
deployment.apps/rollout-nginx image updated
```

2. 파드들을 조회한다.
```shell
kubectl get pods -o wide 
```
```shell
NAME                             READY   STATUS             RESTARTS   AGE    IP               NODE     NOMINATED NODE   READINESS GATES
rollout-nginx-8566d57f75-dflvk   1/1     Running            0          11m    172.16.103.140   w2-k8s   <none>           <none>
rollout-nginx-8566d57f75-j9kkc   1/1     Running            0          11m    172.16.221.142   w1-k8s   <none>           <none>
rollout-nginx-8566d57f75-zvjbp   1/1     Running            0          11m    172.16.132.14    w3-k8s   <none>           <none>
rollout-nginx-856f4c79c9-q52h2   0/1     ImagePullBackOff   0          109s   172.16.132.15    w3-k8s   <none>           <none>
```
업데이트 된 파드가 정상적으로 생성되지 않았다.

3. 문제를 확인하기 위해 `rollout status`를 실행한다.
```shell
kubectl rollout status deployment rollout-nginx 
```
```shell
Waiting for deployment "rollout-nginx" rollout to finish: 1 out of 3 new replicas have been updated...
```
새로운 replicas는 생성했으나(new replicas have been updated) 디플로이먼트를 배포하는 단계에서는 대기중(Waiting)으로 더이상 진행되지 않은 것을 확인할 수 있다.

4. `describe` 명령으로 문제를 좀 더 자세히 살펴보자
```shell
kubectl describe deployment rollout-nginx
```
```shell
Name:                   rollout-nginx
Namespace:              default
CreationTimestamp:      Thu, 19 Dec 2024 21:21:59 +0900
Labels:                 <none>
Annotations:            deployment.kubernetes.io/revision: 3
                        kubernetes.io/change-cause: kubectl set image deployment rollout-nginx nginx=nginx:1.17.23 --record=true
Selector:               app=nginx
Replicas:               3 desired | 1 updated | 4 total | 3 available | 1 unavailable
StrategyType:           RollingUpdate
MinReadySeconds:        0
RollingUpdateStrategy:  25% max unavailable, 25% max surge
Pod Template:
  Labels:  app=nginx
  Containers:
   nginx:
    Image:        nginx:1.17.23
    Port:         <none>
    Host Port:    <none>
    Environment:  <none>
    Mounts:       <none>
  Volumes:        <none>
Conditions:
  Type           Status  Reason
  ----           ------  ------
  Available      True    MinimumReplicasAvailable
  Progressing    True    ReplicaSetUpdated
OldReplicaSets:  rollout-nginx-8566d57f75 (3/3 replicas created)
NewReplicaSet:   rollout-nginx-856f4c79c9 (1/1 replicas created)
```
`describe` 명령으로 확인하니 replicas가 새로 생성되는 과정에 멈춰있다. 1.17.23 버전의 nginx 컨테이너가 없기 때문이다.
replicas가 생성을 시도했으나 컨테이너 이미지를 찾을 수 없어 디플로이먼트가 배포되지 않았다.
이를 방지하고자 업데이트할 때 `rollout`을 사용하고 `--record`로 기록하는 것이다.

5. 문제를 확인했으니 정상적인 상태로 복구를 해보겠다. 업데이트할 때 사용했던 명령어들을 `rollout history`로 확인한다.
```shell
kubectl rollout history deployment rollout-nginx 
```
```shell
REVISION  CHANGE-CAUSE
1         kubectl apply --filename=/root/_Book_k8sInfra/ch3/3.2.10/rollout-nginx.yaml --record=true
2         kubectl set image deployment rollout-nginx nginx=nginx:1.16.0 --record=true
3         kubectl set image deployment rollout-nginx nginx=nginx:1.17.23 --record=true
```

6. `rollout undo`로 명령 실행을 취소해 마지막 단계 (revision 3)에서 전 단계(revision 2)로 상태를 되돌린다.
```shell
kubectl rollout undo deployment rollout-nginx
```
```shell
deployment.apps/rollout-nginx rolled back
```

7. 파드의 상태를 다시 확인한다.
```shell
kubectl get pods -o wide
```
```shell
NAME                             READY   STATUS    RESTARTS   AGE   IP               NODE     NOMINATED NODE   READINESS GATES
rollout-nginx-8566d57f75-dflvk   1/1     Running   0          25m   172.16.103.140   w2-k8s   <none>           <none>
rollout-nginx-8566d57f75-j9kkc   1/1     Running   0          25m   172.16.221.142   w1-k8s   <none>           <none>
rollout-nginx-8566d57f75-zvjbp   1/1     Running   0          26m   172.16.132.14    w3-k8s   <none>           <none>
```
8. `rollout history`로 실행된 명령을 확인한다.
```shell
kubectl rollout history deployment rollout-nginx
```
```shell
REVISION  CHANGE-CAUSE
1         kubectl apply --filename=/root/_Book_k8sInfra/ch3/3.2.10/rollout-nginx.yaml --record=true
3         kubectl set image deployment rollout-nginx nginx=nginx:1.17.23 --record=true
4         kubectl set image deployment rollout-nginx nginx=nginx:1.16.0 --record=true
```
revision 4가 추가되고 revision 2가 삭제됐다. 현재 상태를 revision 2로 되돌렸기 때문에 revision 2는 삭제되고 가장 최근 상태는 revision 4가 된다.

9. 컨테이너에 배포된 nginx의 버전을 확인한다.
```shell
curl -I --silent 172.16.103.140 | grep Server
```
```shell
Server: nginx/1.16.0
```
10. `rollout status` 명령으로 변경이 정상적으로 적용됐는지 확인한다.
```shell
kubectl rollout status deployment rollout-nginx
```
```shell
deployment "rollout-nginx" successfully rolled out
```
11. `describe`로 현재 디플로이먼트 상태도 세부적으로 점검하자.
```shell
kubectl describe deployment rollout-nginx
```
```shell
Name:                   rollout-nginx
Namespace:              default
CreationTimestamp:      Thu, 19 Dec 2024 21:21:59 +0900
Labels:                 <none>
Annotations:            deployment.kubernetes.io/revision: 4
                        kubernetes.io/change-cause: kubectl set image deployment rollout-nginx nginx=nginx:1.16.0 --record=true
Selector:               app=nginx
Replicas:               3 desired | 3 updated | 3 total | 3 available | 0 unavailable
StrategyType:           RollingUpdate
MinReadySeconds:        0
RollingUpdateStrategy:  25% max unavailable, 25% max surge
Pod Template:
  Labels:  app=nginx
  Containers:
   nginx:
    Image:        nginx:1.16.0
    Port:         <none>
    Host Port:    <none>
    Environment:  <none>
    Mounts:       <none>
  Volumes:        <none>
Conditions:
  Type           Status  Reason
  ----           ------  ------
  Available      True    MinimumReplicasAvailable
  Progressing    True    NewReplicaSetAvailable
OldReplicaSets:  <none>
NewReplicaSet:   rollout-nginx-8566d57f75 (3/3 replicas created)
```

* 특정 시점으로 파드 복구하기
바로 직전 상태가 아니라 특정 시점으로 돌아가고 싶다면 `--to-revision` 옵션을 사용한다.

1. 처음 상태인 revision 1으로 돌아가보자
```shell
kubectl rollout undo deployment rollout-nginx --to-revision=1
```
```shell
deployment.apps/rollout-nginx rolled back
```
2. 새로 생성된 파드들의 IP를 확인한다.
```shell
kubectl get pods -o wide
```
```shell
NAME                             READY   STATUS    RESTARTS   AGE   IP               NODE     NOMINATED NODE   READINESS GATES
rollout-nginx-64dd56c7b5-ffjpp   1/1     Running   0          34s   172.16.221.143   w1-k8s   <none>           <none>
rollout-nginx-64dd56c7b5-pnxct   1/1     Running   0          37s   172.16.103.141   w2-k8s   <none>           <none>
rollout-nginx-64dd56c7b5-xnthd   1/1     Running   0          36s   172.16.132.16    w3-k8s   <none>           <none>
```
3. `curl -I` 컨테이너 버전을 확인한다.
```shell
curl -I --silent 172.16.221.143 | grep Server
```
```shell
Server: nginx/1.15.12
```
## 3.3 쿠버네티스 연결을 담당하는 서비스

### 3.3.1 가장 간단하게 연결하는 노드포트
1. 노드포트를 설정하면 모든 워커의 노드의 특정 포트(노드포트)를 개방
2. 노드포트로 들어오는 요청은 노드포트 서비스로 전달된다.
3. 노드포트 서비스는 해당 업무를 처리할 수 있는 파드로 요청을 전달.

* 노드 포트 서비스로 외부에서 접속하기
1. 디플로이먼트로 파드를 생성한다. 
```shell
kubectl create deployment np-pods --image=sysnet4admin/echo-hname
```

2. 배포된 파드를 확인한다.
```shell
kubectl get pods
```
```shell
NAME                       READY   STATUS    RESTARTS   AGE
np-pods-5767d54d4b-ncbnw   1/1     Running   0          51s
```

3. `kubectl create`로 노드포트 서비스를 생성한다. 
```shell
kubectl create -f ~/_Book_k8sInfra/ch3/3.3.1/nodeport.yaml
```

```yaml
apiVersion: v1
kind: Service
metadata:
  name: np-svc
spec:
  selector:
    app: np-pods
  ports:
    - name: http
      protocol: TCP
      port: 80
      targetPort: 80
      nodePort: 30000
  type: NodePort
```

4.  `kubectl get services`를 실행해 노드포트 서비스로 생성한 np-svc 서비스를 확인한다.
```shell
kubectl get services
```

```shell
NAME         TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)        AGE
kubernetes   ClusterIP   10.96.0.1      <none>        443/TCP        2d23h
np-svc       NodePort    10.98.92.238   <none>        80:30000/TCP   3m42s
```
노드포트의 포트 번호가 30000번으로 지정됐다. CLUSTER_IP(10.98.92.238)는 쿠버네티스 클러스터의 내부에서 사용하는 IP로 자동으로 지정된다.

5. 쿠버네티스 클러스터의 워커 노드 IP를 확인한다.
```shell
kubectl get nodes -o wide
```

```shell
NAME     STATUS   ROLES    AGE     VERSION   INTERNAL-IP     EXTERNAL-IP   OS-IMAGE                KERNEL-VERSION                CONTAINER-RUNTIME
m-k8s    Ready    master   2d23h   v1.18.4   192.168.1.10    <none>        CentOS Linux 7 (Core)   3.10.0-1160.90.1.el7.x86_64   docker://18.6.0
w1-k8s   Ready    <none>   2d23h   v1.18.4   192.168.1.101   <none>        CentOS Linux 7 (Core)   3.10.0-1160.90.1.el7.x86_64   docker://18.6.0
w2-k8s   Ready    <none>   2d23h   v1.18.4   192.168.1.102   <none>        CentOS Linux 7 (Core)   3.10.0-1160.90.1.el7.x86_64   docker://18.6.0
w3-k8s   Ready    <none>   2d23h   v1.18.4   192.168.1.103   <none>        CentOS Linux 7 (Core)   3.10.0-1160.90.1.el7.x86_64   docker://18.6.0
```
6. 호스트 OS에서 브라우저로 192.168.1.101~103의 30000포트로 요청을 보낸다.

* 부하 분산하기
디플로이먼트로 생성된 파드 1개에 접속하고 있는 중에 파드가 3개로 증가하면 어떻게 될까?
부하가 분산되는지 확인해보자.

1. 호스트 OS에 powershell에서  아래의 명령을 실행해 파드의 이름을 확인한다.
```shell
$i=0; while($true) 
{ 
  % {$i++; write-host -NoNewLine "$i $_"} 
  (Invoke-RestMethod "http://192.168.1.101:30000")-replace '\n', " "
}
```

2. 배포된 파드를 확인한다.
```shell
kubectl get pods
```

3. powershell에 파드의 이름 3개가 돌아가면서 표시된다.
   어떻게 추가된 파드를 외부에서 추적해서 접속하는 것일까? 이는 노드포트 오브젝트 스펙에 적힌 `np-pods`와 디플로이먼트의 이름을 확인해 동일하면 같은 파드라고 간주하기 때문이다.

* expose로 노드포트 서비스 생성하기
노드포트 서비스는 오브젝트 스펙 파일로만 생성할 수 있는게 아니다. `expose` 명령어로도 생성할 수 있다.

1. `expose` 명령어를 사용해 서비스로 내보낼 디플로이먼트를 np-pods로 지정한다. 서비스의 이름은 `np-svc-v2`로, 타입은 `NodePort`로 지정한다.
마지막으로 서비스갚 ㅏ드로 보내줄 연결 포트를 80번으로 지정한다.
```shell
kubectl expose deployment np-pods --type=NodePort --name=np-svc-v2 --port=80
```

2. 생성된 서비스를 확인한다. 오브젝트 스펙으로 생성할 때는 노드포트 번호를 지정할 수 있지만 `expose` 명령어로 생성할 때에는 30000~32767에서 임의로 지정이 된다.

```shell
NAME         TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)        AGE
kubernetes   ClusterIP   10.96.0.1      <none>        443/TCP        3d
np-svc       NodePort    10.98.92.238   <none>        80:30000/TCP   40m
np-svc-v2    NodePort    10.100.164.3   <none>        80:30600/TCP   9s
```

### 3.3.2 사용 목적별로 연결하는 인그레스
노드포트 서비스는 포트를 중복 사용할 수 없어서 1개의 노드포트에 1개의 디플로이먼트만 적용된다.
여러 개의 디플로이먼트가 있을 때 그 수만큼 노드포트 서비스를 구동해야 할까?
쿠버네티스는 이런 경우에 인그레스를 사용한다.
`인그레스(ingress)`는 고유한 주소를 제공해 사용 목적에 따라 다른 응답을 제공할 수 있고, 트래픽에 대한 L4/L7 로드밸런서와 보안 인증처리를 하는 기능을 제공한다.

인그레스를 사용하려면 인그레스 컨트롤러가 필요하다. 다양한 인그레스 컨트롤러가 있지만 쿠버네티스에서 프로젝트로 지원하는 NGINX 인그레스 컨트롤러를 구성해보겠다.
1. 사용자는 노드마다 설정된 노드포트를 통해 노드포트 서비스로 접속한다. 이때 노드포트 서비스를 NGINX 인그레스 컨트롤러로 구성한다.
2. NGINX 인그레스 컨트롤러는 사용자의 접속 겅로에 따라 적합한 클러스터 IP 서비스로 경로를 제공한다.
3. 클러스터 IP 서비스는 사용자를 해당 파드로 연결해 준다.

> 인그레스 컨트롤러는 파드와 직접 통신할 수 없어서 노드포트 또는 로드밸런서 서비스와 연동되어야 한다.

1. 디플로이먼트 2개를 배포한다.
```shell
kubectl create deployment in-hname-pod --image=sysnet4admin/echo-hname
kubectl create deployment in-ip-pod --image=sysnet4admin/echo-ip
```
2. 배포된 pod를 확인한다.
```shell
kubectl get pods
```
3. 인그레스 컨트롤러를 설치한다. 여기에는 많은 종류의 오브젝트 스펙이 포함된다. 
```shell
kubectl apply -f ~/_Book_k8sInfra/ch3/3.3.2/ingress-nginx.yaml
```
4. NGINX 인그레스 컨트롤러의 파드가 배포됐는지 확인한다. NGINX 인그레스 컨트롤러는 default 네임스페이스가 아닌 ingress-nginx 네임스페이스에 속하므로 -n ingress-nginx 옵션을 추가해야 한다.
여기서 `-n`은 namespace으 약어로, default 외의 네임스페이스를 확인할 때 사용하는 옵션이다.

```shell
kubectl get pods -n ingress-nginx
```

5. 인그레스를 사용자 요구 사항에 맞게 설정하려면 경로와 작동을 정의해야 한다. 파일로도 설정할 수 있으므로 다음 경로로 실행해 미리 정의해둔 설정을 적용한다.
```shell
kubectl apply -f ~/_Book_k8sInfra/ch3/3.3.2/ingress-config.yaml
```
```yaml
appVersion: networking.k8s.io/v1beta1
kind: Ingress
metadata:
  name: ingress-nginx
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  rule:
  - http:
      paths:
      - path:
        backend:
          serviceName: hname-svc-default
          servicePort: 80
      - path: /ip
        backend:
          serviceName: ip-svc
          servicePort: 80
      - path: /your-directory
        backend:
          serviceName: your-svc
          servicePort: 80
```

6. 인그레스 설정 파일이 제대로 등록됐는지 `kubectl get ingress`로 확인한다.
```shell
kubectl get ingress
```

```shell
NAME            CLASS    HOSTS   ADDRESS   PORTS   AGE
ingress-nginx   <none>   *                 80      5m31s
```
7. kubectl get ingress -o yaml을 실행해 인그레스에 요청한 내용이 확실하게 적용됐는지 확인한다.
이 명령은 인그레스에 적용된 내용을 야믈 형식으로 출력해 적용딘 내용을 확인할 수 있다.

8. NGINX 인그레스 컨트롤러 생성과 인그레스 설정을 완료했다. 이제 외부에서 NGINX 인그레스 컨트롤러에 접속할 수 있게 노드포트 서비스로 NGINX 인그레스 컨트롤러를 외부에 노출한다.
```shell
kubectl apply -f ~/_Book_k8sInfra/ch3/3.3.2/ingress.yaml
```
```yaml
appVersion: v1
kind: Service
metadata:
  name: nginx-ingress-controller
  namespace: ingress-nginx
spec:
  ports:
  - name: http
    protocol: TCP
    port: 80
    targetPort: 80
    nodePort: 30100
  - name: https
    protocol: TCP
    port: 443
    targetPort: 443
    nodePort: 30101
  selector:
    app.kubernetes.io/name: ingress-nginx
  type: NodePort
```

9. 노드포트 서비스로 생성된 NGINX 인그레스 컨트롤러를 확인한다. 이때도 `-n ingress-nginx`로 네임스페이스를 지정해야만 내용을 확인할 수 있다.
```shell
kubectl get services -n ingress-nginx
```
```shell
NAME                       TYPE       CLUSTER-IP     EXTERNAL-IP   PORT(S)                      AGE
nginx-ingress-controller   NodePort   10.96.97.238   <none>        80:30100/TCP,443:30101/TCP   4m23s
```

10. expose 명령으로 디플로이먼트(in-hname-pod, in-ip-pod)도 서비스로 노출한다. 외부와 통신하기 위해 클러스터 내부에서만 사용하는 파드를 클러스터 외부에 노출할 수 있는 구역으로 옮기는 것이다.
내부와 외부 네트워크를 분리해 관리하는 DMZ(DeMilitarized Zone)와 유사한 기능이다.
```shell
kubectl expose deployment in-hname-pod --name=hname-svc-default --port=80,443
kubectl expose deployment in-ip-pod --name=ip-svc --port=80,443
```
11. 생성된 서비스를 점검해 디플로이먼트들이 서비스에 정상적으로 노출되는지 확인한다. 새로 생성된 서비스는 default 네임스페이스에 있으므로 `-n` 옵션으로 네임스페이스를 지정하지 않아도 된다.
```shell
kubectl get services
```
```shell
NAME                TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
hname-svc-default   ClusterIP   10.99.131.97     <none>        80/TCP,443/TCP   3m55s
ip-svc              ClusterIP   10.110.219.254   <none>        80/TCP,443/TCP   3m
kubernetes          ClusterIP   10.96.0.1        <none>        443/TCP          3d
np-svc              NodePort    10.98.92.238     <none>        80:30000/TCP     80m
np-svc-v2           NodePort    10.100.164.3     <none>        80:30600/TCP     39m
```
12. 호스트OS에 192.168.1.101:30100에 접속해 외부에서 접속되는 경로에 따라 다르게 동작하는지 확인한다.

### 3.3.3 클라우드에서 쉽게 구성 가능한 로드밸런서
앞의 연결 방식은 들어오는 요청을 모두 워커 노드의 노드포트를 통해 노드포트 서비스로 보내고, 다시 쿠버네티스의 파드로 보내는 구조였다.
이 방식은 매우 비효율적이다. 그래서 쿠버네티스는 로드밸런서라는 서비스 타입을 제공한다.

### 3.3.4 온프레미스에서 로드밸런서를 제공하는 MetalLB
온프레미스에서 로드밸런서를 사용하려면 내부에서 로드밸런서 서비스를 받아주는 구성이 필요한데, 이를 지원하는 것이 MetalLB이다.
MetalLB는 베어메탈(bare metal, 운영 체제가 설치되지 않은 하드웨어)로 구성된 쿠버네티스에서도 로드밸런서를 사용할 수 있게 고안된 프로젝트다.
MetalLB는 특별한 네트워크 설정이나 구성이 있는 것이 아니라 기존의 L2 네트워크(ARP/NDP)와 L3 네트워크(BGP)로 로드밸런서를 구현한다.

1. 디플로이먼트를 이용해 2종류(lb-hname-pods, lb-ip-pods)의 파드를 생성한다. 그리고 scale 명령으로 파드를 3개로 늘려 노드당 1개씩 파드가 배포되게 한다.
```shell
kubectl create deployment lb-hname-pods --image=sysnet4admin/echo-hname
kubectl create deployment lb-ip-pods --image=sysnet4admin/echo-ip
kubectl scale deployment lb-hname-pods --replicas=3
kubectl scale deployment lb-ip-pods --replicas=3
```

2. 2종류의 파드가가 3개씩 총 6개가 배포됐는지 확인한다.'
```shell
kubectl get pods
```
```shell
NAME                             READY   STATUS    RESTARTS   AGE
lb-hname-pods-79b95c7c7b-5h6dj   1/1     Running   0          51s
lb-hname-pods-79b95c7c7b-kvntq   1/1     Running   0          58s
lb-hname-pods-79b95c7c7b-sd27f   1/1     Running   0          51s
lb-ip-pods-6c6bb59b4-4mbsq       1/1     Running   0          46s
lb-ip-pods-6c6bb59b4-p7wbj       1/1     Running   0          54s
lb-ip-pods-6c6bb59b4-vhv9t       1/1     Running   0          46s
```
3. 사전에 정의된 오브젝트 스펙으로 MetalLB를 구성한다. 이렇게 하면 MetalLB에 필요한 요소가 모두 설치되고 독립적인 네임스페이스도 함께 만들어진다.
```shell
kubectl apply -f ~/_Book_k8sInfra/ch3/3.3.4/metallb.yaml
```
4. 배포된 MetalLB의 파드가 5개(controller 1개, speaker 4개)인지 확인하고, IP와 상태도 확인한다.
```shell
kubectl get pods -n metallb-system -o wide
```
```shell
NAME                          READY   STATUS    RESTARTS   AGE   IP              NODE     NOMINATED NODE   READINESS GATES
controller-5d48db7f99-5wmvq   1/1     Running   0          16m   172.16.132.21   w3-k8s   <none>           <none>
speaker-6fx82                 1/1     Running   0          16m   192.168.1.103   w3-k8s   <none>           <none>
speaker-bpgv2                 1/1     Running   0          16m   192.168.1.101   w1-k8s   <none>           <none>
speaker-ms9pq                 1/1     Running   0          16m   192.168.1.10    m-k8s    <none>           <none>
speaker-swsgh                 1/1     Running   0          16m   192.168.1.102   w2-k8s   <none>           <none>
```
5. 인그레스와 마찬가지로 MetalLB도 설정을 적용해야 한다. ConfigMap을 사용한다. ConfigMap은 설정이 정의된 포맷이라고 생각하면 된다.

```shell
kubectl apply -f ~/_Book_k8sInfra/ch3/3.3.4/metallb-l2config.yaml
```

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  namespace: metallb-system
  name: config
data:
  config: |
    address-pools:
    - name: nginx-ip-range
      protocol: layer2
      addresses:
      - 192.168.1.11-192.168.1.13
```
6. configMap이 생서됐는지 `kubectl get configmap -n metallb-system`으로 확인한다.
```shell
kubectl get configmap -n metallb-system
```
7. `kubectl get configmap -n metallb-system -o yaml` 명령으로 MetalLB 설정이 올바르게 적용됐는지 확인한다.

8. 모든 설정이 완료됐으니 이제 각 디플로이먼트(lb-hname-pods, lb-ip-pods)를 로드밸런서 서비스로 노출한다.
```shell
kubectl expose deployment lb-hname-pods --type=LoadBalancer --name=lb-hname-svc --port=80
kubectl expose deployment lb-ip-pods --type=LoadBalancer --name=lb-ip-svc --port=80
```
9. 생성된 로드밸런서 서비스별로 CLUSTER-IP와 EXTERNAL-IP가 잘 적용됐는지 확인한다.
```shell
kubectl get services
```
```shell
NAME           TYPE           CLUSTER-IP       EXTERNAL-IP    PORT(S)        AGE
kubernetes     ClusterIP      10.96.0.1        <none>         443/TCP        3d22h
lb-hname-svc   LoadBalancer   10.110.189.159   192.168.1.11   80:30283/TCP   104s
lb-ip-svc      LoadBalancer   10.98.221.15     192.168.1.12   80:31377/TCP   64s
```
10. 호스트OS에서 브라우저로 EXTERNAL-IP로 접속한다. 배포된 파드의 이름이 브라우저에 표시되는지 확인한다.

11. powershell로 로드밸런서 기능이 정상적으로 작동하는지 확인한다.
```shell
$i=0; while($true)
{
  % { $i++; write-host -NoNewline "$i $_" }
  (Invoke-RestMethod "http://192.168.1.11")-replace '\n', " "
}
```
### 3.3.5 부하에 따라 자동으로 파드 수를 조절하는 HPA
사용자가 갑자기 늘어난다면 파드가 더이상 감당할 수 없어 서비스가 불가능한 결과를 초래할 수도 있다.
쿠버네티스는 이런 경우를 대비해 부하량에 따라 디플로이먼트의 파드 수를 유동적으로 관리하는 기능을 제공한다.
이를 HPA(Horizontal Pod Autoscaler)라고 한다.

1. 디플로이먼트 1개를 hpa-hname-pods라는 이름으로 생성한다.
```shell
kubectl create deployment hpa-hname-pods --image=sysnet4admin/echo-hname
```
2. expose를 통해 hpa-hname-pods를 로드밸런서 서비스로 설정한다.
```shell
kubectl expose deployment hpa-hname-pods --type=LoadBalancer --name=hpa-hname-svc --port=80
```
3. 설정된 로드밸런서 서비스와 부여된 IP를 확인한다.
```shell
kubectl get services
```
```shell
NAME            TYPE           CLUSTER-IP       EXTERNAL-IP    PORT(S)        AGE
hpa-hname-svc   LoadBalancer   10.106.135.199   192.168.1.11   80:30510/TCP   31s
kubernetes      ClusterIP      10.96.0.1        <none>         443/TCP        3d22h
```
4. HPA가 작동하려면 파드의 자원이 어느 정도 사용되는지 파악해야 한다. 부하를 확인하는 명령은 리눅스의 top(table of processes)과 비슷한 `kubectl top`을 사용한다.
```shell
kubectl top pods
```
```shell
Error from server (NotFound): the server could not find the requested resource (get services http:heapster:)
```
자원을 요청하는 설정이 없다며 에러가 생기고 진행되지 않는다. 
HPA가 자원을 요청할 때 메트릭 서버를 통해 계측값을 전달 받는다. 현재 메트릭 서버가 없기 때문에 에러가 발생한다.
따라서 계측값을 수집하고 전달하는 메트릭 서버를 설정해야 한다.

5. 서비스에서와 마찬가지로 메트릭 서버도 오브젝트 스펙 파일로 설치할 수 있다.
그러다 그림처럼 오브젝트 스펙 파일이 여러 개라서 git clone 이후에 디렉터리에 있는 파일들을 다시 실행해야하는 번거로움이 있다.
실습에서 사용하려면 몇 가지 추가 설정이 필요한다. 그래서 쿠버네티스 메트릭 서버의 원본 소스를 옮겨 메트릭 서버를 생성하겠다.
```shell
kubectl create -f ~/_Book_k8sInfra/ch3/3.3.5/metrics-server.yaml
```
```yaml
spec:
  containers:
  - image: sysnet4admin/echo-hname
    imagePullPolicy: Always
    name: echo-hname
    resources: 
      requests:
        cpu: "10m"
      limits:
        cpu: "50m"
```
```yaml
resources:
  requests:
    cpu: "10m"
  limits:
    cpu: "50m"
```
을 추가 한다.

6. hpa-hname-pods에 autoscale을 설정해 특정 조건이 만족되는 경우 자동으로 scale 명령이 수행되도록 한다.
min은 최소, max는 최대 파드의 수다. cpu-percent는 cpu사용량이 50%를 넘기게 되면 autoscale 하겠다는 뜻이다.
```shell
kubectl autoscale deployment hpa-hname-pods --min=1 --max=30 --cpu-percent=50
```
7. powershell로 부하를 건다.
```shell
$i=0; while($true)
{
  % { $i++; write-host -NoNewline "$i $_" }
  (Invoke-RestMethod "http://192.168.1.11")-replace '\n', " "
}
```
8. 부하량이 증가하면 자동으로 pod가 추가 생성된다.
```shell
NAME                              CPU(cores)   MEMORY(bytes)
hpa-hname-pods-696b8fcc99-2qgcw   11m          2Mi
```
```shell
NAME                              CPU(cores)   MEMORY(bytes)
hpa-hname-pods-696b8fcc99-2qgcw   11m          2Mi
hpa-hname-pods-696b8fcc99-9skkc   0m           2Mi
hpa-hname-pods-696b8fcc99-b24v9   24m          2Mi
hpa-hname-pods-696b8fcc99-f8wvw   0m           2Mi
hpa-hname-pods-696b8fcc99-frcs9   0m           2Mi
hpa-hname-pods-696b8fcc99-kdvzm   0m           2Mi
hpa-hname-pods-696b8fcc99-km4zf   0m           2Mi
hpa-hname-pods-696b8fcc99-nv6n7   0m           2Mi
hpa-hname-pods-696b8fcc99-q6vl9   0m           2Mi
hpa-hname-pods-696b8fcc99-s4dr7   0m           2Mi
hpa-hname-pods-696b8fcc99-xjv7v   0m           2Mi
```

9. 부하가 없으면 autoscale은 최소 조건인 파드 1개의 상태로 만든다
```shell
NAME                              CPU(cores)   MEMORY(bytes)
hpa-hname-pods-696b8fcc99-q6vl9   0m           2Mi

```

## 3.4 알아두면 쓸모 있는 쿠버네티스 오브젝트

### 3.4.1 데몬셋
데몬셋은 디플로이먼트의 replicas가 노드 수 만큼 정해져 있는 형태라고 할 수 있다. 노드 하나당 파드 한 개만을 생성한다.
노드의 단일 접속 지점으로 노드 외부와 통신하는 경우 파드가 1개 이상 필요하지 않다. 노드를 관리하는 파드라면 데몬셋으로 만드는게 가장 효율적이다.

1. `kubectl get pods -n metallb-system -o wide`를 실행해 현재 MetalLB의 스피커가 각 노드에 분포돼 있는 상태를 확인한다.
```shell
kubectl get pods -n metallb-system -o wide
```
```shell
NAME                          READY   STATUS    RESTARTS   AGE   IP              NODE     NOMINATED NODE   READINESS GATES
controller-5d48db7f99-5wmvq   1/1     Running   0          18h   172.16.132.21   w3-k8s   <none>           <none>
speaker-6fx82                 1/1     Running   0          18h   192.168.1.103   w3-k8s   <none>           <none>
speaker-bpgv2                 1/1     Running   1          18h   192.168.1.101   w1-k8s   <none>           <none>
speaker-ms9pq                 1/1     Running   2          18h   192.168.1.10    m-k8s    <none>           <none>
speaker-swsgh                 1/1     Running   0          18h   192.168.1.102   w2-k8s   <none>           <none>
```
2. 워커 노드를 1개 늘린다.

3. w4-k8s가 추가되면 m-k8s에서 `kubectl get pods -n metallb-system -o wide -w`를 수행한다.
```shell
kubectl get pods -n metallb-system -o wide -w
```
```shell
NAME                          READY   STATUS    RESTARTS   AGE   IP              NODE     NOMINATED NODE   READINESS GATES
controller-5d48db7f99-5wmvq   1/1     Running   1          18h   172.16.132.27   w3-k8s   <none>           <none>
speaker-6fx82                 1/1     Running   1          18h   192.168.1.103   w3-k8s   <none>           <none>
speaker-bpgv2                 1/1     Running   1          18h   192.168.1.101   w1-k8s   <none>           <none>
speaker-gtmks                 1/1     Running   0          36s   192.168.1.104   w4-k8s   <none>           <none>
speaker-ms9pq                 1/1     Running   2          18h   192.168.1.10    m-k8s    <none>           <none>
speaker-swsgh                 1/1     Running   1          18h   192.168.1.102   w2-k8s   <none>           <none>
```
4. 자동으로 추가된 노드에 설치된 스피커가 데몬셋이 맞는지 `kubectl get pods speaker-gtmks -o yaml -n metallb-system` 명령으로 확인한다.
```shell
ownerReferences:
  - apiVersion: apps/v1
    blockOwnerDeletion: true
    controller: true
    kind: DaemonSet
    name: speaker
    uid: 442ef72a-8d1f-431e-9c17-fc0dc36b227f
```
### 3.4.2 컨피그맵
컨피그맵(Config Map)은 이름 그대로 설정을 목적으로 사용하는 오브젝트이다. MetalLB를 구성할 때 컨피그맵을 사용했었다. 인그레스에서는 설정을 위해 오브젝트를 인그레스로 선언했는데, 왜 MetalLB에서는 컨피그맵을 사용 했을까?
명확하게 규정하기는 어려운데 인그레스는 오브젝트가 인그레스로 지정돼 있지만, MetalLB는 프로젝트 타입으로 정해진 오브젝트가 없어서 범용 설정으로 사용되는 컨피그맵을 지정했다.

컨피그맵으로 작성된 MetalLB의 IP 설정을 변경해 보자.

1. 테스트 디플로이먼트를 cfgmap이라는 이름으로 생성한다.
```shell
kubectl create deployment cfgmap --image=sysnet4admin/echo-hname
```
2. cfgmap을 로드밸런서(MetalLB)를 통해 노출하고 이름은 cfgmap-svc로 지정한다.
```shell
kubectl expose deployment cfgmap --type=LoadBalancer --name=cfgmap-svc --port=80
```
3. 생성된 서비스의 IP를 확인한다.
```shell
kubectl get services
```
```shell
NAME         TYPE           CLUSTER-IP     EXTERNAL-IP    PORT(S)        AGE
cfgmap-svc   LoadBalancer   10.107.22.29   192.168.1.11   80:30084/TCP   25m
kubernetes   ClusterIP      10.96.0.1      <none>         443/TCP        4d17h
```
4. 사전에 구성돼 있는 컨피그맵의 기존 IP를 sed 명령을 사용해 192.168.1.21~192.168.1.23으로 변경한다.
```shell
cat ~/_Book_k8sInfra/ch3/3.4.2/metallb-l2config.yaml | grep 192.
sed -i 's/11/21/;s/13/23/' ~/_Book_k8sInfra/ch3/3.4.2/metallb-l2config.yaml
cat ~/_Book_k8sInfra/ch3/3.4.2/metallb-l2config.yaml | grep 192.
```
5. 컨피그맵 설정 파일(metallb-l2config.yaml)에 apply를 실행해 변경된 설정을 적용한다.
```shell
kubectl apply -f ~/_Book_k8sInfra/ch3/3.4.2/metallb-l2config.yaml
```

6. MetalLB와 관련된 모든 파드를 삭제한다. 샂게하고 나면 kubelet에서 해당 파드를 자동으로 모두 다시 생성한다. `--all`은 파드를 모두 삭제하는  옵션이다.
```shell
kubectl delete pods --all -n metallb-system
```

7. 새로 생성된 MetalLB의 파드들을 확인한다.
```shell
kubectl get pods -n metallb-system
```

8. 기존에 노출한 MetalLB 서비스(cfgmap-svc)를 삭제(delete)하고 동일한 이름으로 다시 생성해 새로운 컨피그맵을 적용한 서비스가 올라오게 한다.
```shell
kubectl delete services cfgmap-svc
kubectl expose deployment cfgmap --type=LoadBalancer --name=cfgmap-svc --port=80
```
9. 변경된 설정이 적용돼 새로운 MetalLB 서비스의 IP가 192.168.1.21로 바뀌었는지 확인한다.
```shell
kubectl get services
```
```shell
NAME         TYPE           CLUSTER-IP      EXTERNAL-IP    PORT(S)        AGE
cfgmap-svc   LoadBalancer   10.107.50.111   192.168.1.21   80:31277/TCP   36s
kubernetes   ClusterIP      10.96.0.1       <none>         443/TCP        4d17h
```
10. 호스트OS에서 브라우저에 192.168.1.21로 접속해 파드의 이름이 표시되는지 확인한다.

### 3.4.3 PV와 PVC
파드는 언제라도 생성되고 지워진다. 쿠버네티스에서 의도적으로 이렇게 구현했다.
그런데 파드에서 생성한 내용을 기록하거나 보관하거나, 모든 파드가 동일한 설정 값을 유지하고 관리하기 위해 공유된 볼륨으로부터 공통된 설정을 가지고 올 수 있도록 설계해야 할 때도 있다.

쿠버네티스는 이런 경우를 위해 다음과 같은 목적으로 다양한 형태의 볼륨을 제공한다.
* 임시: emptyDir
* 로컬: host Path, local
* 원격: persistentVolumeClaim, cephfs, cinder, csi, fc(fibre channel), flexVolume, flocker, glusterfs, iscsi, nfs, portworxVolume, quobyte, rbd, scaleIO, storageos, vsphereVolume
* 특수목적: downwardAPI, configMap, secret, azureFile, projected
* 클라우드: awsElasticBlockStore, azureDisk, gcePersistentDisk

쿠버네티스는 필요할 때 PVC(PersistentVolumeClaim, 지속적으로 사용 가능한 볼륨 요청)를 요청해 사용 한다.
PVC를 사용하려면 PV(PersistentVolume, 지속적으로 사용 가능한 볼륨)로 볼륨을 선언해야 한다.
PV는 볼륨을 사용할 수 있게 준비하는 단계.
PVC는 준비된 볼륨에서 일정 공간을 할당 받는 것.

* NFS 볼륨에 PV/PVC를 만들고 파드에 연결하기
1. PV로 선언할 볼륨을 만들기 위해 NFS 서버를 마스터 노드에 구성한다. 공유되는 디렉터리는 `/nfs_shared`로 생성하고, 해당 디렉터리를 NFS로 받아 들일 IP 영역은 192.168.1.0/24로 정한다.
옵션을 적용해 /etc/exports에 기록한다. 옵션에는 rw(읽기/쓰기), sync(쓰기 작업 동기화), no_root_squash(root 계정 사용)

```shell
mkdir /nfs_shared
echo '/nfs_shared 192.168.1.0/24(rw,sync,no_root_squash)' >> /etc/exports
```
2. 해당 내용을 시스템에 적용해 NFS 서버를 활성화하고 다음 시작시에도 자동으로 적용되도록 `systemctl enable --now nfs` 명령을 실행한다.
```shell
systemctl enable --now nfs 
```
3. 오브젝트 스펙을 싱행해 PV를 생성한다.
```shell
kubectl apply -f ~/_Book_k8sInfra/ch3/3.4.3/nfs-pv.yaml
```

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: nfs-pv
spec:
  capacity:
    storage: 100Mi
  accessModes:
    - ReadWriteMany
  persistentVolumeReclaimPolicy: Retain
  nfs:
    server: 192.168.1.10
    path: /nfs_shared
```
* 6~7 라인: storage는 실제 사용하는 용량을 제한하는 것이 아니라 쓸 수 있는 양을 레이블로 붙이는 것과 같다.
* 8~9 라인: PV를 어떤 방식으로 사용할지를 정의한 부분이다. `ReadWriteMany`는 여러 개의 노드가 읽고 쓸 수 있도록 마운트하는 옵션이다. 이 외에도 ReadWriteOnce(하나의 노드에서만 볼륨을 읽고 쓸 수 있게 마운트), ReadOnlyMany(여러 개의 노드가 읽도록 마운트) 옵션이 있다.
* 10 라인: persistentVolumeReclaimPolicy는 PVC가 제거됐을 때 PV가 작동하는 방법을 정의하는 것으로, 여기서는 유지하는 Retain을 사용한다. 그 외에 Delete(삭제), Recycle(재활용, deprecated) 옵션이 있다.
* 11~13 라인: NFS 서버의 연결 위치에 대한 설정

4. `kubectl get pv`를 실행해 생성된 PV의 상태가 Avalilable(사용 가능)임을 확인한다.
```shell
kubectl get pv
```
```shell
NAME     CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS      CLAIM   STORAGECLASS   REASON   AGE
nfs-pv   100Mi      RWX            Retain           Available                                   51m
```

5. 다음 경로에서 오브젝트 스펙을 실행해 PVC를 생성한다.
```shell
kubectl apply -f ~/_Book_k8sInfra/ch3/3.4.3/nfs-pvc.yaml
```

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: nfc-pvc
spec:
  accessModes:
    - ReadWriteMany
  resources:
    requests:
      storage: 10Mi
```
PVC는 PV와 구성이 거의 동일하다. 
하지만 PV는 사용자가 요청한 볼륨 공간을 관리자가 만들고, PVC는 사용자가 볼륨을 요청하는데 사용한다는 점에서 차이가 있다.
여기서 요청하는 `storage: 10Mi`는 동적 볼륨이 아닌 경우에는 레이블 정도의 의미를 가진다.

6. 생성된 PVC를 `kubectl get pvc`로 확인한다.
```shell
kubectl get pvc
```
```shell
NAME      STATUS   VOLUME   CAPACITY   ACCESS MODES   STORAGECLASS   AGE
nfs-pvc   Bound    nfs-pv   100Mi      RWX                           26m
```
여기서 두 가지를 살펴봐야 한다. 첫 번째는 `Bound`로 변경됐다는 것이다. 이는 PV와 PVC가 연결됐음을 의미한다.
두번째는 용량이 설정한 10Mi가 아닌 100Mi라는 것이다. 사실 용량은 동적으로 PVC를 따로 요쳥해 생성하는 경우가 아니면 큰 의미가 없다.

7. PV의 상태도 Bound로 바뀌었음을 `kubectl get pv`로 확인한다.
```shell
kubectl get pv
```
```shell
NAME     CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM             STORAGECLASS   REASON   AGE
nfs-pv   100Mi      RWX            Retain           Bound    default/nfs-pvc                           83m
```
8. 생성한 PVC를 볼륨으로 사용하는 디플로이먼트 오브젝트 스펙을 배포한다.
```shell
kubectl apply -f ~/_Book_k8sInfra/ch3/3.4.3/nfs-pvc-deploy.yaml
```

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nfs-pvc-deploy
spec:
  replicas: 4
  selector:
    matchLabels:
      app: nfs-pvc-deploy
  template:
    metadata:
      labels:
        app: nfs-pvc-deploy
    spec:
      containers:
        - name: audit-trail
          image: sysnet4admin/audit-trail
          volumeMounts:
            - name: nfs-vol
              mountPath: /audit
      volumes:
        - name: nfs-vol
          persistentVolumeClaim:
            claimName: nfs-pvc
```
* 15~17 라인: audit-trail 이미지를 가지고 온다. 해당 컨테이너 이미지는 요청을 처리할 때마다 접속 정보를 로그로 기록한다.
* 18~20 라인: 볼륨이 마운트될 위치 (/audit)를 지정한다.
* 21~24 라인: PVC로 생성된 볼륨을 마운트하기 위해 nfs-pvc라는 이름을 사용한다.

9. 생성된 파드를 확인한다.
```shell
kubectl get pods
```
```shell
NAME                              READY   STATUS    RESTARTS   AGE
nfs-pvc-deploy-5fd9876c46-6jqtd   1/1     Running   0          25m
nfs-pvc-deploy-5fd9876c46-d6d5s   1/1     Running   0          25m
nfs-pvc-deploy-5fd9876c46-vh7m2   1/1     Running   0          25m
nfs-pvc-deploy-5fd9876c46-vp6sd   1/1     Running   0          25m
```

10. 생성한 파드중 하나에 `exec`로 접속한다.
```shell
kubectl exec -it nfs-pvc-deploy-5fd9876c46-6jqtd -- /bin/bash
```

11. df -h를 실행해 PVC의 마운트 상태를 확인한다. 
```shell
Filesystem                Size      Used Available Use% Mounted on
overlay                  37.0G      2.8G     34.2G   8% /
tmpfs                    64.0M         0     64.0M   0% /dev
tmpfs                     1.2G         0      1.2G   0% /sys/fs/cgroup
192.168.1.10:/nfs_shared
                         37.0G      3.6G     33.3G  10% /audit
/dev/mapper/centos_k8s-root
                         37.0G      2.8G     34.2G   8% /dev/termination-log
/dev/mapper/centos_k8s-root
                         37.0G      2.8G     34.2G   8% /etc/resolv.conf
/dev/mapper/centos_k8s-root
                         37.0G      2.8G     34.2G   8% /etc/hostname
/dev/mapper/centos_k8s-root
                         37.0G      2.8G     34.2G   8% /etc/hosts
shm                      64.0M         0     64.0M   0% /dev/shm
tmpfs                     1.2G     12.0K      1.2G   0% /run/secrets/kubernetes.io/serviceaccount
tmpfs                     1.2G         0      1.2G   0% /proc/acpi
tmpfs                    64.0M         0     64.0M   0% /proc/kcore
tmpfs                    64.0M         0     64.0M   0% /proc/keys
tmpfs                    64.0M         0     64.0M   0% /proc/timer_list
tmpfs                    64.0M         0     64.0M   0% /proc/timer_stats
tmpfs                    64.0M         0     64.0M   0% /proc/sched_debug
tmpfs                     1.2G         0      1.2G   0% /proc/scsi
tmpfs                     1.2G         0      1.2G   0% /sys/firmware
```
12. audit-trail 컨테이너의 기능을 테스트 한다. 외부에서 파드(nfs-pv-deploy)에 접속할 수 있도록 expose로 로드밸런서 서비스를 생성한다.
```shell
kubectl expose deploymant nfs-pvc-deploy --type=LoadBalancer --name=nfs-pcs-deploy-svc --port=80
```

13. `kubectl get services`로 생성한 로드밸런서 서비스의 IP를 확인한다.
```shell
kubectl get services
```
14. 호스트OS에서 브라우저로 해당 아이피로 접속해 파드의 이름과 IP가 표시되는지 확인한다.

15. exec를 통해 접속한 파드에서 ls /audit 명령을 실행해 접속 기록 파일이 남았는지 확인한다. cat 명령으로 해당 파일의 내용도 함께 확인한다.

16. 마스터 노드에서 scale 명령으로 파드를 4개에서 8개로 증가시킨다.
```shell
kubectl scale deployment nfs-pvc-deploy --replicas=8
```

17. 생성된 파드를 확인한다.
```shell
kubectl get pods
```
```shell
NAME                              READY   STATUS    RESTARTS   AGE
nfs-pvc-deploy-5fd9876c46-6jqtd   1/1     Running   0          90m
nfs-pvc-deploy-5fd9876c46-c94gw   1/1     Running   0          54m
nfs-pvc-deploy-5fd9876c46-d6d5s   1/1     Running   0          90m
nfs-pvc-deploy-5fd9876c46-v44qt   1/1     Running   0          54m
nfs-pvc-deploy-5fd9876c46-v52zq   1/1     Running   0          54m
nfs-pvc-deploy-5fd9876c46-vh7m2   1/1     Running   0          90m
nfs-pvc-deploy-5fd9876c46-vk5s9   1/1     Running   0          54m
nfs-pvc-deploy-5fd9876c46-vp6sd   1/1     Running   0          90m
```
18. 최근에 증가한 4개의 파드중 1개를 선택해 exec로 접속하고, 기록된 audit 로그가 같은지 확인한다.

19. 다른 브라우저를 열고 192.168.1.21로 접속해 다른 파드 이름과 IP가 표시되는지 확인한다.

20. exec로 접속한 파드에섯 새로 추가된 audit 로그를 확인한다.

21. 기존에 접속한 파드에서도 동일한 로그가 audit에 기록돼 있는지 확인한다.

* NFS 볼륨을 파드에 직접 마운트 하기
1. 사용자가 관리자와 동일한 단일 시스템이라면 PV와 PVC를 사용할 필요가 없다. 어떻게 단순히 볼륨을 마운트하는지 확인해보자.
```shell
kubectl apply -f ~/_Book_k8sInfra/ch3/3.4.3/nfs-ip.yaml
```

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nfs-ip
spec:
  replicas: 4
  selector:
    matchLabels:
      app: nfs-ip
  template:
    metadata:
      labels:
        app: nfs-ip
    spec:
      containers:
        - name: audit-trail
          image: sysnet4admin/audit-trail
          volumeMounts:
            - name: nfs-vol 
              mountPath: /audit
      volumes:
        - name: nfs-vol
          nfs:
            server: 192.168.1.10
            path: /nfs_shared
```
* 21~25 라인을 살펴보면 PV와 PVC를 거치지 않고 바로 NFS 서버로 접속하는 것을 확인할 수 있다.

2. 새로 배포된 파드를 확인하고 그중 하나에 exec로 접속한다.
```shell
kubectl get pods
kubectl exec -it nfs-ip-7789f445b7-l2km7 -- /bin/bash
```
3. `ls /audit`
```shell
ls /audit
```
NFS 볼륨을 바라보고 있음을 확인한다.

### 3.4.4 스테이풀셋
지금까지는 파드가 replicas에 선언된 만큼 무작위로 생성될 뿐이었다.
그런데 파드가 만들어지는 이름과 순서를 예측해야할 때가 있다.
주로 레디스, 주키퍼, 카산드라, 몽고DB 등의 마스터-슬레이브 구조 시스템에서 필요하다.
이런 경우 스테이풀셋을 사용한다. 스테이풀셋은 volumeClaimTemplates 긴능을 사용해 PVC를 자동으로 생성할 수 있고,
각 파드가 순서대로 생성되기 때문에 고정된 이름, 볼륨, 설정 등을 가질 수 있다.
그래서 StatefulSet(이전 상태를 기억하는 세트)라는 이름을 사용한다.

1. PV와 PVC는 앞에서 이미 생성했으므로 바로 스테이풀셋을 다음 명령으로 생성한다.
```shell
kubectl apply -f ~/_Book_k8sInfra/ch3/3.4.4/nfs-pvc-sts.yaml
```

```yaml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: nfs-pvc-sts
spec:
  replicas: 4
  serviceName: sts-svc-domain #statefulset need it
  selector:
    matchLabels:
      app: nfs-pvc-sts
  template:
    metadata:
      labels:
        app: nfs-pvc-sts
    spec:
      containers:
        - name: audit-trail
          image: sysnet4admin/audit-trail
          volumeMounts:
            - name: nfs-vol 
              mountPath: /audit
      volumes:
        - name: nfs-vol
          persistentVolumeClaim:
            claimName: nfs-pvc    
```

2. 파드가 잘 생성됬는지 `kubectl get pods -w`
```shell
kubectl get pods -w
```
```shell
NAME            READY   STATUS    RESTARTS   AGE
nfs-pvc-sts-0   1/1     Running   0          3m55s
nfs-pvc-sts-1   1/1     Running   0          3m49s
nfs-pvc-sts-2   1/1     Running   0          3m44s
nfs-pvc-sts-3   1/1     Running   0          3m40s
```

3. 생성한 스테이트풀셋에 expose를 실행한다.
그런데 에러가 발생한다. expose 명령이 스테이트풀셋을 지원하지 않기 때문이다.
해결하려면 파일로 로드밸런서 서비스를 작성, 실행해야 한다.
```shell
kubectl expose statefulset nfc-pvc-sts --type=LoadBalancer --name=nfs-pvc-sts-svc --port=80
```

4. 다음 경로를 적용해 스테이트풀셋을 노출하기 위한 서비스를 생성하고, kubectl get service 명령으로 생성한 로드밸런서 서비스를 확인한다.
```shell
kubectl apply -f ~/_Book_k8sInfra/ch3/3.4.4/nfs-pvc-sts-svc.yaml
kubectl get services
```
```shell
NAME              TYPE           CLUSTER-IP     EXTERNAL-IP    PORT(S)        AGE
kubernetes        ClusterIP      10.96.0.1      <none>         443/TCP        5d23h
nfs-pvc-sts-svc   LoadBalancer   10.102.83.32   192.168.1.21   80:30980/TCP   16s
```

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nfs-pvc-sts-svc
spec:
  selector:
    app: nfs-pvc-sts
  ports:
    - port: 80
  type: LoadBalancer
```

5. 호스트OS의 브라우저에서 192.168.1.21에 접속해 파드 이름과 IP가 표시되는지 확인한다.

6. exec로 파드에 접속한 후에 ls /audit -l로 새로 접속한 파드의 정보가 추가됐는지 확인한다.

7. `kubectl delete statefulset nfs-pvc-sts`를 실행해 스테이트풀셋의 파드를 삭제한다. 파드는 생성된 순서의 역순으로 삭제되는데, `kubectl get pods -w`를 실행하면 삭제되는 과정을 볼 수 있다.
```shell
kubectl delete statefulset nfs-pvc-sts
kubectl get pods -w
```
---
# 4. 쿠버네티스를 이루는 컨테이너 도우미, 도커

## 4.1 도커를 알아야하는 이유
쿠버네티스를 이루는 기본 오브젝트는 파드이고, 파드는 컨테이너로 이루어져있다.
컨테이너를 만들고 관리하는 도구가 도커이다.
쿠버네티스를 이루고 있는 기술 자체는 컨테이너를 벗어날 수 없다. 따라서 트러블 슈팅을 제대로 하려면 컨테이너를 잘 알아야 한다.

### 4.1.1 파드, 컨테이너, 도커, 쿠버네티스의 관계
파드는 1개 이상의 컨테이너로 이루어져 있다.
파드들은 워커 노드라는 노드 단위로 관리된다.
워커 노드와 마스터 노드가 모여 쿠버네티스 클러스터가 된다.

파드는 쿠버네티스로부터 IP를 받아 컨테이너가 외부와 통신할 수 있는 경로를 제공한다.
컨테이너들이 정상적으로 작동하는지 확인하고 네트워크나 저장 공간을 서로 공유하게 한다.
파드가 이러한 환경을 만들기 때문에 컨테이너들은 마치 하나의 호스트에 존재하는 것처럼 작동할 수 있다.

정리하면 컨테이너를 돌보는 것이 파드고, 파드를 돌보는 것이 쿠버네티스 워커 노드이며,
워커 노드를 돌보는 것이 쿠버네티스 마스터이다. 쿠버네티스 마스터 역시 파드(컨테이너)로 이루어져 있다.

이 구조를 이루는 가장 기본적인 컨테이너는 하나의 운영 체제 안에서 커널을 공유하며 개별적인 실행 환경을 제공하는 격리된 공간이다.
개별적인 실행 환경이란 CPU, 네트워크, 메모리와 같은 시스템 자원을 독자적으로 사용하도록 할당된 환경을 말한다.
개별적인 실행 환경에서는 실행되는 프로세스를 구분하는 ID도 컨테이너 안에 격리돼 관리된다.
그래서 각 컨테이너 내부에서 실행되는 애플리케이션들은 서로 영향을 미치지 않고 독립적으로 작동할 수 있다.

각 컨테이너가 독립적으로 작동하기 때문에 여러 컨테이너를 효과적으로 다룰 방법이 필요해졌다.
오래전부터 유닉스나 리눅스는 하나의 호스트 운영 체제 안에서 자원을 분리해 할당하고, 실행되는 프로세스를 격리해서 관리하는 방법을 제공했다.
하지만 과정이 복잡하고 전문가만 사용할 수 있는 단점이 있었다.
이런 복잡한 과정을 쉽게 만들어주는 것이 도커이다.
도커는 컨테이너를 사용하는 방법을 명령어로 정리한 것이라 보면된다.

### 4.1.2 다양한 컨테이너 관리 도구
컨테이너 관리 도구는 도커 외에도 여러 가지가 있다.
* 컨테이너디(Containerd): Docker사에서 컨테이너 런타임 부분을 분리하여 만든 오픈 소스 컨테이너 관리도구로, 2019년 2월 클라우드 네이티브 컴퓨팅 재단의 졸업 프로젝트가 됐다.
쿠버네티스와 통신에 필요한 CRI(Container Runtime Interface) 규격에 맞춰 구현한 플로그인을 사용해 쿠버네티스와 통합할 수 있다. 컨테이너디는 다른 시스템과 통합해 컨테이너를 관리하는 기능을 제공하기 때문에 컨테이너 관리 도구를 직접 개발하려는 개발자에게 적합하다.
* 크라이오(CRI-O): 레드햇에서 개발해 2019년 클라우드 네이티브 컴퓨팅 재단에 기부한 오픈 소스 프로젝트로, 현재 인큐베이팅(Incubating)단계에 있다.
크라이오는 범용적인 컨테이너 관리 도구인 도커나 컨테이너디와 달리 쿠버네티스와 통합하는 것을 주목적으로 한다. 크라이오는 다른 도구보다 가볍고, 단순하며, CRI 규격을 자체적으로 구현하고 있어서 별도의 구성 요소나 플러그인 없이 쿠버네티스와 통합할 수 있다.
* 카타 컨테이너(Kata Container): 오픈스택 재단(Openstack foundation)에서 후원하는 오픈 소스 컨테이너 관리 도구이다. 컨테이너마다 독립적인 커널을 제공한다는 점에서 기존 컨테이너 방식과 큰 차이가 있다. 카타 컨테이너를 샐행하면 개별 컨테이너를 위한 가벼운 가상 머신을 생성하고 그 위에서 컨테이너가 동작한다.
따라서 독립적인 커널을 사용하므로 다른 컨테이너의 영향을 받지 않는다. 기술적으로 보면 기존 컨테이너 방식과 가상화 방식의 중간 역역에 있다. 기술적으로는 보안에 좀 더 강하지만, 필요한 CPU나 메모리의 크기가 기존 컨테이너 방식보다 크다.
* 도커(Docker): Docker사에서 2013년에 만든 컨테이너 관리 도구로, 컨테이너 관리 기능 외에도 컨테이너를 실행하는 데 필요한 이미지를 만들거나 공유하는 등의 다양한 기능을 제공한다.
도커는 사용자가 명령어를 입력하는 명령어 도구(CLI)와 명령을 받아 들이는 도커 데몬으로 구성돼 있다.

## 4.2 도커로 컨테이너 다루기

### 4.2.1 컨테이너 이미지 알아보기
* 이미지 검색하고 내려 받기

이미지는 레지스트리(Registry)라고 하는 저장소에 모여 있다. 레지스트리는 도커 허브처럼 공개된 유명 레지스트리일 수도 있고, 내부에 구축한 레지스트리일 수도 있다.
이미지는 레지스트리 웹 사이트에서 직접 검색해도 되고, 명령창에서 쿠버네티스 마스터 노드에 접속해 검색할 수 도 있다.
이때 별도의 레지스트리를 지정하지 않으면 기본으로 도커 허브에서 이미지를 찾는다.
`docker search <검색어>`를 입력하면 특정한 이름(검색어)을 포함하는 이미지가 있는지 찾는다.
이미지는 애플리케이션, 미들웨어, 등 고유한 목적에 맞게 패키지돼 있다.

```shell
docker search nginx
```
```shell
NAME                                     DESCRIPTION                                     STARS               OFFICIAL            AUTOMATED
nginx                                    Official build of Nginx.                        20456               [OK]                
bitnami/nginx                            Bitnami container image for NGINX               195                                     [OK]
ubuntu/nginx                             Nginx, a high-performance reverse proxy & we…   123                                     
nginx/nginx-ingress                      NGINX and  NGINX Plus Ingress Controllers fo…   98                                      
nginx/unit                               This repository is retired, use the Docker o…   64                                      
nginx/nginx-prometheus-exporter          NGINX Prometheus Exporter for NGINX and NGIN…   45                                      
rapidfort/nginx                          RapidFort optimized, hardened image for NGINX   15                                      
kasmweb/nginx                            An Nginx image based off nginx:alpine and in…   8                                       
chainguard/nginx                         Build, ship and run secure software with Cha…   4                                       
redash/nginx                             Pre-configured nginx to proxy linked contain…   3                                       
rancher/nginx                                                                            2                                       
circleci/nginx                           This image is for internal use                  2                                       
nginx/nginx-ingress-operator             NGINX Ingress Operator for NGINX and NGINX P…   2                                       
vmware/nginx                                                                             2                                       
corpusops/nginx                          https://github.com/corpusops/docker-images/     1                                       
nginx/nginx-quic-qns                     NGINX QUIC interop                              1                                       
gluufederation/nginx                      A customized NGINX image containing a consu…   1                                       
nginx/nginxaas-loadbalancer-kubernetes                                                   0                                       
paketobuildpacks/nginx                                                                   0                                       
droidwiki/nginx                                                                          0                                       
intel/nginx                                                                              0                                       
bitnamicharts/nginx                      Bitnami Helm chart for NGINX Open Source        0                                       
jitesoft/nginx                           Nginx on alpine linux                           0                                       
nginx/unit-preview                       Unit preview features                           0                                       
antrea/nginx                             Nginx server used for Antrea e2e testing        0   
```
표시되는 각 열의 의미는 다음과 같다.
1. INDEX: 이미지가 저장된 레지스트리의 이름.
2. NAME: 검색된 이미지 이름. 공식 이미지를 제외한 나머지는 '레지스트리 주소/저장소 소유자/이미지 이름' 형태이다.
3. DESCRIPTION: 이미지에 대한 설명.
4. STARS: 해당 이미지를 내려받은 사용자에게 받은 평가
5. OFFICIAL: [OK] 표시는 해당 이미지에 포함된 애플리케이션, 미들웨어 등을 개발한 업체에서 공식적으로 제공한 이미지라는 의미이다.
6. AUTOMATED: [OK] 표시는 도커 허브에서 자체적으로 제공하는 이미지 빌드 자동화 기능을 활용해 생성한 이미지를 의미한다.

docker search로 찾은 이미지는 `docker pull`로 내려 받을 수 있다ㅏ. 앞에서 찾은 nginx 이미지를 내려 받아 사렾보겠다.
```shell
docker pull nginx
```
```shell
Using default tag: latest
latest: Pulling from library/nginx
bc0965b23a04: Pull complete 
650ee30bbe5e: Pull complete 
8cc1569e58f5: Pull complete 
362f35df001b: Pull complete 
13e320bf29cd: Pull complete 
7b50399908e1: Pull complete 
57b64962dd94: Pull complete 
Digest: sha256:fb197595ebe76b9c0c14ab68159fd3c08bd067ec62300583543f0ebda353b5be
Status: Downloaded newer image for nginx:latest
```
이미지를 내려 받을 때 사용하는 태그, 레이어, 이미지의 고유 식별 값 등을 볼 수 있다.
1. 태그(tag): Using default tag와 함께 뒤에 따라오는 태그 이름을 통해 이미지를 내려받을 때 사용한 태그를 알 수 있다. 아무런 조건을 주지 않고 이미지 이름만으로 pull을 수행하면 기본으로 latest 태그가 적용된다. latest태그는 가장 최신 이미지를 의미 한다.
2. 레이어(layer): pull을 수행해 내려받은 레이어이다. 하나의 이미지는 여러 개의 레이어로 이루어져 있어서 레이어마다 Pull complete 메세지가 발생한다.
3. 다이제스트(digest): 이미지의 고유 식별자로, 이미지에 포함된 내용과 이미지의 생성 환경을 식별할 수 있다. 식별자는 해시(hash) 함수로 생성되며 이미지가 동일한지 검증하는 데 사용한다. 다이제스트는 고유한 값이므로 다이제스트가 같은 이미지는 이름이나 태그가 다르더라도 같은 이미지다.
4. 상태: 이미지를 내려받은 레지스트리, 이미지, 태그 등의 상태 정보를 확인할 수 있다. 형식은 '레지스트리 이림/이미지 이름:태그'이다.

* 이미지 태그

태그는 동일한 이미지에 추가하는 식별자다. 이름이 동일해도 도커 이미지의 버전이나 플랫폼이 다를 수 있기 때문에 이를 구분하는데 사용한다.
이미지를 내려 받거나 이미지를 기반으로 컨테이너를 구동할 때는 이미지 이름만 사용하고 태그를 명시하지 않으면 latest 태그를 기본으로 사용한다.


* 이미지 레이어 구조

1. 이미지 파일은 레이어로 구성되어 있다. nginx의 latest 이미지와 stable 이미지를 비교해 확인 해보겠다.
```shell
docker pull nginx:stable
```
```shell
stable: Pulling from library/nginx
bc0965b23a04: Already exists 
af38aa266166: Pull complete 
53a8d9cbfd8a: Pull complete 
61f8f240c02d: Pull complete 
6aec90d25585: Pull complete 
209e8c8a5c7e: Pull complete 
97fc0bab11f2: Pull complete 
Digest: sha256:54b2f7b04062caecedd055427c58c43edf314a45fa6f7cee9d9d69e900bb9799
Status: Downloaded newer image for nginx:stable
```
`bc0965b23a04` 레이어가 `Already exists`라고 나오는데 `bc0965b23a04` 이미지가 이미 존재한다는 뜻이다.
앞서 받은 latest 이미지에 해당 레이어가 있기 때문이다.

2. `docker images <이미지 이름>` 명령을 실행해 내려받은 이미지를 조회한다.
```shell
docker images nginx
```
```shell
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
nginx               latest              66f8bdd3810c        3 weeks ago         192MB
nginx               stable              fa0a8cea5e76        4 months ago        188MB
```
각 이미지의 용량은 192mb, 188mb이다. 두 이미지의 용량을 합치면 380mb지만 공유하는 레이어가 있으므로 실제로는 더 작은 용량을 차지한다.
이처럼 도커로 작성된 컨테이너는 레어이어를 재사용하기 때문에 여러 이미지를 내려받더라도 디스크 용량을 효율적으로 사용할 수 있다.

### 4.2.2 컨테이너 실행하기
* 컨테이너 단순 실행하기

1. `docker run -d --restart always nginx` 명령으로 새로운 컨테이너를 실행한다.
```shell
docker run -d --restart always nginx
```
```shell
614b6f68334629b6f6517dd8c2fd3a7fffcccc3f65f16a03eabba964f0e6066b
```
`docker run`으로 컨테이너를 실행하면 결과값으로 16진수 문자열이 나온다. 이 문자열은 컨테이너를 식별할 수 있는 컨테이너ID이다.
* --d(-detach): 컨테이너를 백그라운드에서 구동한다는 의미다. 옵션을 생략하면 컨테이너 내부에서 실행되는 애플리케이션의 상태가 화면에 계속 표시된다. 이 상태에서 빠져 나오려고 `ctr + c`를 누르면 애플리케이션뿐만 아니라 컨테이너도 함께 중단된다.
따라서 계속 작동해야 하는 서버나, 데이터베이스 같은 프로그램은 -d 옵션을 붙여 백그라운드에서 작동하게 해야 합니다.

* `--restart always`: 컨테이너 재시작과 관련된 정책을 의미하는 옵션이다. 프로그램에서 예상하지 못한 오류가 발생하거나 리눅스 시스템에서 도커 서비스가 중지되는 경우에 컨테이너도 작동이 중지된다. 이때 중지된 컨테이너를 즉시 재시작하거나 리눅스 시스템에서 도커 서비스가 작동할 때 컨테이너를 자동으로 시작하도록 설정할 수 있다.
앞으로는 가상 머신을 중지한 후 다시 실행해도 자동으로 컨테이너가 기존 상태를 이어갈수 있게 --restart always 옵션을 사용하겠다.

> 옵션에 따라 달라지는 컨테이너 시작방법

| 값              | 컨테이너 비정상 종료 시   | 도커 서비스 시작 시     |
|----------------|-----------------|--------------------------|
| no(기본값)        | 컨테이너를 재시작하지 않음  | 컨테이너를 시작하지 않음|
| on-failure     | 컨테이너를 재시작함      | 컨테이너를 시작함         |
| always         | 컨테이너를 재시작함      | 컨테이너를 시작함         |
| unless-stopped | 컨테이너를 재시작함      | 사용자가 직접 정하지 않은 컨테이너만 시작함 |

2. `docker ps` 명령으로 생성한 컨테이너 상태를 확인한다.
```shell
docker ps
```
```shell
CONTAINER ID        IMAGE                  COMMAND                  CREATED             STATUS              PORTS               NAMES
614b6f683346        nginx                  "/docker-entrypoint.…"   9 minutes ago       Up 9 minutes        80/tcp              blissful_archimedes      k8s.gcr.io/pause:3.2   "/pause"                 2 hours ago         Up 2 hours                              k8s_POD_kube-scheduler-m-k8s_kube-system_e541886a4cda0424b9879a78869adc51_8
```
* CONTAINER ID: 컨테이너를 식별하기 위한 고유 ID다.
* IMAGE: 컨테이너를 만드는데 사용한 이미지다.
* COMMAND: 컨테이너가 생성될 때 내부엥서 작동할 프로그램을 실행하는 명령어이다. 여기서는 `docker-entrypoint.sh`며 해당 셸이 nginx 이미지로 컨테이너가 생설될 때 nginx 프로그램을 호출해서 서비스 할 수 있도록 해준다.
* CREATED: 컨테이너가 생성된 시각을 표시한다.
* STATUS: 컨테이너가 작동을 시작한 시각을 표시한다.
* PORTS: 컨테이너가 사용하는 포트와 프로토콜을 표시한다. 80/tcp는 컨테이너 내부에서 80번 포트와 TCP 프로토콜을 사용한다는 뜻이다.
* NAMES: 컨테이너 이름을 표시한다. 이름은 `docker run`에 `--name <이름>` 옵션으로 직접 지정할 수도 있지만, 지정하지 않으면 컨테이너가 시작될 때 도커가 임의로 부여한 값이 나타난다.

3. `docker ps -f id=614` 명령으로 컨테이너를 지정해 검색한다.
```shell
docker ps -f id=614
```
```shell
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS               NAMES
614b6f683346        nginx               "/docker-entrypoint.…"   15 minutes ago      Up 15 minutes       80/tcp              blissful_archimedes
```
docker ps에 -f(--filter) <필터링 대상> 옵션을 주면 검색 결과를 필터링할 수 있다. 필터링 대상을 지정할 때는 key=value 형식으로 입력한다. 이때 value와 정확하게 일치하지 않더라도 문자열을 포함하는 경우를 필터링 한다.

4. 생성된 nginx 컨테이너는 마스터 노드 내부에 존재하므로 curl 127.0.0.1 명령으로 컨테이너가 제공하는 nginx 웹 페이지 정보를 가져와보자
```shell
curl 127.0.0.1
```
```shell
curl: (7) Failed connect to 127.0.0.1:80; Connection refused
```
정상적인 응답이 돌아오지 않고 `Connection refused` 오류가 발생했다. 왜 오류가 발생했는지 알아보자.
앞에서 컨테이너 PORTS 열에 표시되는 80/tcp는 컨테이너 내부에서 TCP 프로토콜의 80번 포트를 사용한다는 의미라고 했다.
하지만 curl 127.0.0.1로 전달한 요청은 로컬호스트의 80번 포트로 전달만 될 뿐 컨테이너까지는 도달하지 못한다.
즉 호스트에 도달한 후 컨테이너로 도달하기 위한 추가 경로 설정이 돼 있지 않은 상태이다.

따라서 응답을 컨테이너에서 처리해주기를 원한다면 80번으로 들어온 것을 컨테이너에서 받아줄 수 있는 포트로 연결해 주는 설정이 필요하다.

5. docker run에 -p 8080:80 옵션을 추가해 새로운 nginx 컨테이너(nginx-exposed)를 실행한다.
```shell
docker run -d -p 8080:80 --name=nginx-exposed --restart always nginx
```
6. 컨테이너가 제대로 작동하는지 docker ps로 확인한다.
```shell
docker ps -f name=nginx-exposed
```
```shell
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                  NAMES
f92c079e6e0e        nginx               "/docker-entrypoint.…"   About a minute ago   Up 10 seconds       0.0.0.0:8080->80/tcp   nginx-exposed
```
0.0.0.0:8080->80/tcp: 0.0.0.0dml 8080번 포트로 들어오는 요청을 컨테이너 내부 80번 포트로 전달한다는 의미이다. 0.0.0.0은 존재하는 모든 네트워크 어댑터를 의미한다. m-k8s 호스트는 자기 자신을 나타내는 127.0.0.1과 외부에 노출된 192.168.1.10 등의 IP를 가지고 있는데, 요청이 호스트에 할당된 어떤 IP의 8080번 포트로 들어오더라도 컨테이너 내부의 80번 포트로 전달된다.

3. 호스트OS의 브라우저에 192.168.1.10:8080을 입력해 컨테이너로 접근할 수 있는지 확인한다.

### 4.2.3 컨테이너 내부 파일 변경하기
도커는 컨테이너 내부에서 컨테이너 외부의 파일을 사용할 수있다. 크게 4가지 방법으로 제공한다.
* `docker cp`: docker cp <호스트 경로> <컨테이너 이름>:<컨테이너 내부 경로> 형식으로 호스트에 위치한 파일을 구동중인 컨테이너 내부에 복사한다. 컨테이너에 임시로 필요한 파일을 단편적으로 전송하기 위해서 사용한다. 또는 컨테이너에 저장돼 있는 설정 및 로그를 추출해 확인하는 목적으로도 사용한다.
* `Dokcerfile ADD`: 이미지는 Dockerfile을 기반으로 만들어지는데, 이때 Dockerfile에는 ADD라는 구문으로 컨테이너 내부로 복사할 파일을 지정하면 이미지를 빌드할 때 지정한 파일이 이미지 내부로 복사된다.
이후 해당 이미지를 기반으로 구동한 컨테이너에서는 복사한 파일을 사용할 수 있다. 그러나 사용자가 원하는 파일을 선택해 사용할 수 없다는 약점이 있다.
* `바인드 마운트`: 호스트 파일 시스템과 컨테이너 내부를 연결해 어느 한쪽에서 작업한 내용이 양쪽에 동시에 반영되는 방법이다. 새로운 컨테이너를 구동할 때도 호스트와 연결할 파일이나 디렉터리의 경로만 지정하면 다른 컨테이너에 있는 파일을 새로 생성한 컨테이너와 연결할 수 있다.
데이터베이스의 데이터 디렉터리나 서버의 첨부 파일 디렉터리처럼 컨테이너가 바뀌어도 없어지면 안 되는 자료는 이 방법으로 보존할 수 있다.
* 볼륨: 호스트 파일 시스템과 컨테이너 내부를 연결하는 것은 바인드 마운트와 동일하지만, 호스트의 특정 디렉터리가 아닌 도커가 관리하는 볼륨을 컨테이너와 연결한다.
여기서 말하는 볼륨은 쿠버네티스에서 살펴본 볼륨 구조와 유사하다. 따라서 도커가 관리하는 볼륨 공간을 NFS와 같은 공유 디렉터리에 생성한다면 다른 호스트에서도 도커가 관리하는 볼륨을 함께 사용할 수 있다.

호스트와 컨테이너를 연결하려면 연결 대상이 되는 컨테이너 내부의 디렉터리 구조를 먼저 알아야 한다.
현재 정상적으로 노출된 nginx 컨테이너의 구조를 살펴보면 처음 접속할 때 노출되는 페이지는 `/usr/share/nginx/html/index.html`이다.
따라서 수정해야 하는 파일이 index.html이며 이런한 경로 설정은 `/etc/nginx/nginx.conf`에 존재한다.

1. 컨테이너 내부에 연결한 `/root/html/` 디렉터리를 호스트에 생성한다.
```shell
mkdir -p /root/html
```

2. `docker run` 명령으로 nginx-bind-mount라는 이름의 컨테이너를 구동하고, 컨테이너의 `/usr/share/nginx/html/ 디렉터리와 호스트의 `/root/html/` 디렉터리를 연결한다.
```shell
docker run -d -p 8081:80 -v /root/html:/usr/share/nginx/html --restart always --name nginx-bind-mounts nginx
```

3. nginx-bind-mounts 컨테이너를 조회해 STATUS가 정상(UP n minutes)인지 확인한다.
```shell
docker ps -f name=nginx-bind-mounts
```
```shell
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                  NAMES
3d5a8c8cf42b        nginx               "/docker-entrypoint.…"   About a minute ago   Up About a minute   0.0.0.0:8081->80/tcp   nginx-bind-mounts
```
4. 컨테이너가 정상적으로 구동했음을 확인하면 컨테이너 내부와 연결된 /root/html/ 디렉터리를 확인한다.
```shell
ls /root/html
```
이 디렉터리는 사용자가 호스트에 생성한 빈 디렉터리인데, 조회하면 여전히 비어있다. 빈 디렉터리가 컨테이너와 연결 되었기 때문에 현재 컨테이너의 nginx는 초기 화면으로 보여줄 파일이 없다.

5. 브라우저를 열고 `192.168.1.10:8081` 연결해 nginx-bind-mounts 컨테이너에서 실행되는 nginx에 접속되는지 확인한다.
nginx에 접속하면 index.html 파일을 읽어서 화면에 표시해 주도록 설계돼 있다. 따라서 바운드 마운트 설정에 따라 호스트 디렉터리의 /root/html에 있는 index.html을 노출하려고 하지만
해당 파일은 존재하지 않기 때문에 403 Forbidden이라는 오류 화면이 출력된다.

6. cp 명령어로 호스트 디렉터리와 컨테이너 디렉터리를 연결할 떄 사용할 index.html을 /root/html/에 복사 한다.
```shell
cp ~/_Book_k8sInfra/ch4/4.2.3/index-BindMount.html /root/html/index.html
```
7. 다시 브라우저를 열고 `192.168.1.10:8081` 연결해보면 index 페이지가 보이게 된다.

볼륨으로 호스트와 컨테이너 연결하기     
볼륨은 도커가 직접 관리하며 컨테이너에 제공하는 호스트의 공간이다.
앞서 배운 바인드 마운트와 어떤차이가 있는지 확인해보자.

1. `docker volume create nginx-volume` 명령으로 볼륨을 생성한다.  nginx-volume은 생성할 볼륨의 이름이다.
```shell
docker volume create nginx-volume
```

2. `docker volume inspect nginx-volume` 명령으로 생성된 볼륨을 조회한다. 볼륨에 적용된 드라이버 종류와 실제호스트에 연결된 디렉터리, 볼륨 이름 등을 조회할 수 있다.
```shell
docker volume inspect nginx-volume
```
```shell
[
    {
        "CreatedAt": "2024-12-25T14:37:13+09:00",
        "Driver": "local",
        "Labels": {},
        "Mountpoint": "/var/lib/docker/volumes/nginx-volume/_data",
        "Name": "nginx-volume",
        "Options": {},
        "Scope": "local"
    }
]
```
`Mountpoint` 행의 `/var/lib/docker/volumes/nginx-volume/_data` 디렉터리가 볼륨 디렉터리임을 확인할 수 있다.
컨테이너 내부와 연결할 떄 전체 디렉터리 경로를 사용하지 않고 nginx-volume이라는 볼륨 이름만으로 간편하게 연결할 수 있다.

3. 볼륨으로 생성된 디렉터리를 확인하자.
```shell
ls /var/lib/docker/volumes/nginx-volume/_data
```
디렉터리는 현재 비어있다. 디렉터리를 컨테이너와 연결해보자. 앞서 바인드 마운트에서 빈 디렉터리를 컨테이너 내부 디렉터리에 덮어쓰는 것과 어떤 차이가 있는지 살펴보자

4. 컨테이너에 연결한 볼륨을 호스트에 생성했으니 호스트와 컨테이너 디렉터리를 연결할 컨테이너를 구동한다. 기존 컨테이너는 설정을 바꿀 수 없으므로 새로운 컨테이너를 구동해야 한다.
nginx-volume이라는 이름의 컨테이너를 구동하고 컨테이너 내부의 /usr/share/nginx/html 디렉터리와 호스트의 nginx-volume 볼륨을 연결한다. 
사용하는 옵션은 `-v [볼륨이름]:[컨테이너 디렉터리]`이다. 앞서 사용한 포트와 중복되지 않게 호스트의 포트번호는 8082로 지정해 컨테이너 내부의 80번 포트와 연결한다.
```shell
docker run -d -v nginx-volume:/usr/share/nginx/html -p 8082:80 --restart always --name nginx-volume nginx
```
```shell
docker run -d -v nginx-volume:/usr/share/nginx/html -p 8082:80 --restart always --name nginx-volume nginx
```
5. 볼륨 디렉터리의 내용을 다시 확인한다.
```shell
ls /var/lib/docker/volumes/nginx-volume/_data
```
```shell
50x.html  index.html
```
컨테이너 내부에 있는 50x.html, index.html 파일을 보존하는 것을 확인할 수 있다.

6. 웹 브라우저로 192.168.1.10:8082로 연결해 nginx-volume 컨테이너의 nginx에 접속한다. 볼륨은 바인드 마운트와 다르게 index.html을 삭제하지 않기 때문에 index.html의 내용이 그대로 표시 된다.

7. ningx-volume에 cp 명령어로 바꿀 파일을 볼륨 디렉터리로 복사해 볼륨에서 변경한 내용이 컨테이너 디렉터리에 동기화 되는지 테스트 한다.
```shell
cp ~/_Book_k8sInfra/ch4/4.2.3/index-Volume.html /var/lib/docker/volumes/nginx-volume/_data/index.html
```

8. 다시 브라우저로 192.168.1.10:8082 접속하면 변경된 index.html의 내용이 표시된다.

### 4.2.4 사용하지 않는 컨테이너 정리하기
사용이 끝나고 더이상 사용하지 않을 컨테이너라면 공간을 확보하기 위해 삭제하는 것이 좋다.
컨테이너나 이미지를 삭제하기 전에 먼저 컨테이너를 정지해야 한다. 삭제할 때 말고도 동일한 호스트의 포트를 사용하는 컨테이너를 배포하거나 작동 중인 컨테이너의 사용 자체를 종료할 때도 먼저 컨테이너를 정지해야 한다.

1. `docker ps -f ancestor=nginx` 명령으로 nginx 이미지를 기반으로 생성된 컨테이너를 조회한다. `ancestor` 키는 컨테이너를 생성하는데 사용한 이미지를 기준으로 필터링 한다.
```shell
docker ps -f ancestor=nginx
```
```shell
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                  NAMES
7fc7746cf341        nginx               "/docker-entrypoint.…"   14 minutes ago      Up 14 minutes       0.0.0.0:8082->80/tcp   nginx-volume
3d5a8c8cf42b        nginx               "/docker-entrypoint.…"   36 minutes ago      Up 36 minutes       0.0.0.0:8081->80/tcp   nginx-bind-mounts
f92c079e6e0e        nginx               "/docker-entrypoint.…"   15 hours ago        Up 42 minutes       0.0.0.0:8080->80/tcp   nginx-exposed
614b6f683346        nginx               "/docker-entrypoint.…"   16 hours ago        Up 42 minutes       80/tcp                 blissful_archimedes
```
2. 컨테이너를 정지하는 명령은 docker stop <컨테이너 이름| ID> 이다. 4번째 컨테이너를 정지해보자.
```shell
docker stop blissful_archimedes
```
3. 3번째 컨테이너를 컨테이너 ID로 종료해보자.
```shell
docker stop f92c079e6e0e
```
4. 컨테이너를 하나씩 정지하면 번거로우니 nginx 이미지를 사용하는 모든 컨테이너를 한꺼번에 정지해보자.
컨테이너 조회 명령에 -q(--quite) 옵션을 추가해 컨테이너 ID만 줄력한다.
```shell
docker ps -q -f ancestor=nginx
```

5. 앞에서 사용한 명령을 docker stop에 인자로 사용하도록 `$()`에 넣는다. 실행하면 nginx 이미지를 사용한 컨테이너가 모두 정지된다.
```shell
docker stop $(docker ps -q -f ancestor=nginx)
```

6. 모든 컨테이너가 정지됐는지 `docker ps -f ancestor=nginx` 명령으로 다시 확인한다.
```shell
docker ps -f ancestor=nginx
```
```shell
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
```

7. 컨테이너가 모두 정지됐으나 삭제된 것은 아니다. 정지된 컨테이너를 포함해 모든 컨테이너 목록을 조회한다. docker ps에 `-a(--all)` 옵션을 주면 정지된 컨테이너를 포함해 조회가 된다. 
```shell
docker ps -a -f ancestor=nginx
```
이때 정지한 컨테이너를 다시 시작하고 싶으면 `docker start <컨테이너 이름 | ID>`를 입력하면 된다.

정지한 컨테이너가 더 이상 필요 없으면 삭제해 사용 중인 컨테이너 목록을 관리하고, 사용하지 않는 컨테이너 이미지를 삭제해 저장 공간을 확보한다.

1. 컨테이너는 `docker rm <컨테이너 이름 | ID>` 명령으로 삭제한다. 이 명령은 한꺼번에 컨테이너를 정지할 때 사용했던 방법을 그대로 사용한다.
기존 옵션과 조합해 `docker rm $(docker ps -aq -f ancestor=nginx)`로 현재 정지된 모든 컨테이너를 삭제한다.
```shell
docker rm $(docker ps -aq -f ancestor=nginx)
```

2. 컨테이너가 정상적으로 삭제됐는지 docker ps -a -f ancestor=nginx 명령으로 확인한다.
```shell
docker ps -a -f ancestor=nginx
```
```shell
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
```

3. 컨테이너는 모두 삭제했지만, 내려받은 이미지는 아직 남아있다. nginx:latest, nginx:stable 이미지를 하나씩 삭제해도 되지만 
`docker rmi $(docker images -q nginx)` 명령으로 한번에 삭제해보자.
여기서 `rmi`는 remove image를 뜻한다.
```shell
docker rmi $(docker images -q nginx)
```


## 4.3 4가지 방법으로 컨테이너 이미지 만들기
## 4.4 쿠버네티스에서 직접 만든 컨테이너 사용하기
---
# 5. 지속적 통합과 배포 자동화, 젠킨스

---
# 6. 안정적인 운영을 완성하는 모니터링, 프로메테우스와 그라파나