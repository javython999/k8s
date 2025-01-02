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

컨테이너 인프라 환경을 구성할 때 이미 제공된 이미지를 사용하는 경우도 있지만, 직접 만든 애플리케이션으로 컨테이너를 만들 수 도 있다.
컨테이너를 만드는 방법은 다음과 같이 4가지가 있다.
1. 기본적인 방법
2. 용량 줄이기
3. 컨테이너 내부 빌드
4. 멀티 스테이지

### 4.3.1 기본적인 방법
기본적인 컨테이너 빌드 과정은 다음과 같다.
* 자바 소스 빌드
* 도커파일 작성
* 도커파일 빌드
* 빌드 완료

1. 기본적인 컨테이너 빌드 도구와 파일이 있는 빌드 디렉터리로 이동해 어떤 파일이 있는지 확인한다.
```shell
cd ~/_Book_k8sInfra/ch4/4.3.1
```
```shell
Dockerfile  mvnw  pom.xml  src
```
* DockerFile: 컨테이너 이미지를 빌드하기 위한 정보를 담고 있다.
* mvnw: 메이븐 래퍼라는 이름의 리눅스 스크립트로, 메이븐 실행을 위한 환경 설정을 자동화 한다.
* pom.xml: 메이븐 래퍼가 작동할 때 필요한 절차와 빌드 정보를 담고 있다.
* src(디렉터리): 메이븐으로 빌드할 자바 소스 디렉터리이다.

2. 소스 코드가 자바로 작성돼 있으므로 실행 가능한 바이너리(Jar)로 만들려면 현재 시스템에 자바 개발도구(JDK)를 설치해야 한다.
```shell
yum install java-1.8.0-openjdk-devel.x86_64 -y
```

3. 자바를 빌드할 때 메이븐(Maven)을 사용한다. 메이븐은 `clean package` 명령으로 실행한다. 이 명령은 빌드를 진행할 디렉터리를 비우고(clean) Jar(package)를 생성하라는 의미이다.
```shell
chmod 700 mvnw
./mvnw clean package
```

4. 자바 빌드가 끝나면 생성되는 Jar파일을 확인한다.
```shell
ls target
```

5. docker build 명령으로 컨테이너 이미지를빌드한다. 여기서 사용된 -t(tag)는 만들어질 이미지를 의미하고 .(dot)은 이미지에 원하는 내용을 추가하거나 변경하는 데 필요한 작업 공간을 현재 디렉터리로 지정한다는 의미이다.
```shell
docker build -t basic-img .
```
```shell
Sending build context to Docker daemon   17.7MB
Step 1/6 : FROM openjdk:8
8: Pulling from library/openjdk
001c52e26ad5: Pull complete 
d9d4b9b6e964: Pull complete 
2068746827ec: Pull complete 
9daef329d350: Pull complete 
d85151f15b66: Pull complete 
52a8c426d30b: Pull complete 
8754a66e0050: Pull complete 
Digest: sha256:86e863cc57215cfb181bd319736d0baf625fe8f150577f9eb58bd937f5452cb8
Status: Downloaded newer image for openjdk:8
 ---> b273004037cc
Step 2/6 : LABEL description="Echo IP Java Application"
 ---> Running in d043c2a75b9f
Removing intermediate container d043c2a75b9f
 ---> bbf39f2198a2
Step 3/6 : EXPOSE 60431
 ---> Running in c0d29a64ac34
Removing intermediate container c0d29a64ac34
 ---> ef584f50cf19
Step 4/6 : COPY ./target/app-in-host.jar /opt/app-in-image.jar
 ---> bc6cfdfc8790
Step 5/6 : WORKDIR /opt
 ---> Running in eae2775dcd1b
Removing intermediate container eae2775dcd1b
 ---> 6fac50c96e66
Step 6/6 : ENTRYPOINT [ "java", "-jar", "app-in-image.jar" ]
 ---> Running in d20531e0139a
Removing intermediate container d20531e0139a
 ---> 86e30417008b
Successfully built 86e30417008b
Successfully tagged basic-img:latest
```
빌드 내용을 이해하려면 도커 빌드에 사용된 Dockerfile을 살펴봐야 한다.
```yaml
FROM openjdk:8
LABEL description="Echo IP Java Application"
EXPOSE 60431
COPY ./target/app-in-host.jar /opt/app-in-image.jar
WORKDIR /opt
ENTRYPOINT [ "java", "-jar", "app-in-image.jar" ]
```
* 1번 라인: FROM <이미지 이름>:[태그] 형식으로 이미지를 가져온다. 가져온 이미지 내부에서 컨테이너 이미지를 빌드한다.
누군가가 만들어 놓은 이미지에 필요한 부분을 추가한다고 보면된다. 여기서는 openjdk를 기초 이미지로 사용했다. 기초 이미지를 어떤 것을 선택하느냐에 따라 다양한 환경의 컨테이너를 빌드할 수 있다.
* 2번 라인: LABEL <레이블 이름>=<값>의 형식으로 이미지에 부가적인 설명을 위한 레이블을 추가할 때 사용한다. `description="Echo IP Java Application"`라는 값을 담은 description 레이블을 추가 했다.
* 3번 라인: EXPOSE <숫자>의 형식으로 생성된 이미지로 컨테이너를 구동할 때 어떤 포트를 사용하는지 알려준다. EXPOSE를 사용한다고 해서 컨테이너를 구동할 때 자동으로 해당 포트를 호스트 포으와 연결하지 않는다. 외부와 연결하려면 지정한 포트를 호스트 포트와 연결해야 한다는 정보를 제공할 뿐이다. 실제로 외부에서 접속하려면 docker run으로 이미지를 컨테이너로 빌드할 때, 반드시 -p 옵션을 넣어 포트를 연결해야 한다.
* 4번 라인: 호스트에서 새로 생성하는 컨테이너 이미지로 필요한 파일을 복사한다. COPY <호스트 경로> <컨테이너 경로>의 형식이다.
* 5번 라인: 이미지의 현재 작업 위치를 /opt로 변경한다.
* 6번 라인: ENTRYPOINT ["명령어", "옵션"... "옵션"]의 형식이다. 컨테이너 구동시 ENTRYPOINT 뒤에 나오는 대괄호 `[ ]`안에 든 명령을 실행한다.
콤마(`,`)로 구분된 문자열 중 첫 번째 문자열은 실행할 명령어고, 두 번째 문자열부터 명령어를 실행할 때 추가하는 옵션이다.
이 명령어는 실행된 프로세스 컨테이너 내부에서 첫 번쨰로 실행됐다는 의미조 PID는 1이 된다.

6. 5단계에서 실행한 이미지를 확인한다. 이미지가 latest 태그로 생성된 것을 확인할 수 있다. IMAGE ID는 5단계에서 빌드할 때 마지막에 표시된 값과 동일 하다.
```shell
docker image basic-img
```
```shell
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
basic-img           latest              86e30417008b        23 minutes ago      544MB
```

7. docker build에 옵션(-t)을 추가해 1.0과 2.0 태그의 이미지도 생성해 보자. 캐시가 적용돼 매우 빠르게 빌드 된다.
```shell
docker build -t basic-img:1.0 -t basic-img:2.0 .
```
```shell
Sending build context to Docker daemon   17.7MB
Step 1/6 : FROM openjdk:8
 ---> b273004037cc
Step 2/6 : LABEL description="Echo IP Java Application"
 ---> Using cache
 ---> bbf39f2198a2
Step 3/6 : EXPOSE 60431
 ---> Using cache
 ---> ef584f50cf19
Step 4/6 : COPY ./target/app-in-host.jar /opt/app-in-image.jar
 ---> Using cache
 ---> bc6cfdfc8790
Step 5/6 : WORKDIR /opt
 ---> Using cache
 ---> 6fac50c96e66
Step 6/6 : ENTRYPOINT [ "java", "-jar", "app-in-image.jar" ]
 ---> Using cache
 ---> 86e30417008b
Successfully built 86e30417008b
Successfully tagged basic-img:1.0
Successfully tagged basic-img:2.0
```
8. 생성된 이미지를 확인한다. 이미지가 모두 ID와 용량이 같은 것을 볼 수 있다. 즉, 이미지들은 태그 정보만 다를 뿐 모두 같은 이미지이며, 한 공간을 사용한다. 리눅스의 소프트 링크와 비슷하다고 보면 된다.
```shell
docker images basic-img
```
```shell
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
basic-img           1.0                 86e30417008b        28 minutes ago      544MB
basic-img           2.0                 86e30417008b        28 minutes ago      544MB
basic-img           latest              86e30417008b        28 minutes ago      544MB
```

9. Dockerfile 내용 중에서 일부만 변경하면 어떻게 되는지 확인해 보자. sed를 사용해 Dockerfile 2번째 줄에 있는 Application 부분을 Development로 변경하고 다시 빌드 해보자. 이때 버전이 중복되지 않게 3.0 태그를 사용한다.
```shell
sed -i 's/Application/Development/' Dockerfile
docker build -t basic-img:3.0 .
```
```shell
Sending build context to Docker daemon   17.7MB
Step 1/6 : FROM openjdk:8
 ---> b273004037cc
Step 2/6 : LABEL description="Echo IP Java Development"
 ---> Running in e67e0cd0e70f
Removing intermediate container e67e0cd0e70f
 ---> 11a9cf7fe6b4
Step 3/6 : EXPOSE 60431
 ---> Running in 2d24398a215a
Removing intermediate container 2d24398a215a
 ---> 5070bb1860c9
Step 4/6 : COPY ./target/app-in-host.jar /opt/app-in-image.jar
 ---> 180296e57cf1
Step 5/6 : WORKDIR /opt
 ---> Running in 78ac316d988f
Removing intermediate container 78ac316d988f
 ---> f2a2e0437930
Step 6/6 : ENTRYPOINT [ "java", "-jar", "app-in-image.jar" ]
 ---> Running in 9e384bafeceb
Removing intermediate container 9e384bafeceb
 ---> 25698eff5b3c
Successfully built 25698eff5b3c
Successfully tagged basic-img:3.0
```
10. 생성된 이미지를 확인한다. 결과를 보면 완전히 다른 ID가 생성됐다. 이름은 같지만 실제로는 다른 컨테이너 이미지이다.
```shell
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
basic-img           3.0                 25698eff5b3c        57 seconds ago      544MB
basic-img           1.0                 86e30417008b        30 minutes ago      544MB
basic-img           2.0                 86e30417008b        30 minutes ago      544MB
basic-img           latest              86e30417008b        30 minutes ago      544MB
```

11. 생성한 컨테이너 이미지가 컨테이너로 작동하는지 확인한다. docker run으로 컨테이너를 실행하고 docker ps로 컨테이너 상태를 출력한다.
```shell
docker run -d -p 60431:80 --name basic-run --restart always basic-img
docker ps -f name=basic
```
```shell
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                              NAMES
bc05e35f6a85        basic-img           "java -jar app-in-im…"   About a minute ago   Up 30 seconds       60431/tcp, 0.0.0.0:60431->80/tcp   basic-run
```

12. curl을 이용해 컨테이너가 정상적으로 외부 요청에 응답하는지 확인해보자.
```shell
curl 127.0.0.1:60431
```
```shell
src: 172.17.0.1 / dest: 127.0.0.1
```

13. 이미지가 제대로 작동하는 것을 확인했으니 작동중인 컨테이너를 -f(force) 옵션으로 바로 삭제한다.
```shell
docker rm -f basic-run
```

14. 빌드한 컨테이너 이미지를 모두 삭제한다.
```shell
docker rmi -f $(docker images -q basic-img)
```
15. 다음 절에서 빌드할 이미지와 용량 비교를 위해 컨테이너 이미지 하나를 다시 빌드 한다.
```shell
docker build -t basic-img .
```

### 4.3.2 컨테이너 용량 줄이기
컨테이너 이미지의 용량을 줄여 빌드하는 방법을 알아보자.
이미지의 용량을 줄여 빌드하는 과정은 다음과 같다.
* 도커파일 작성
* 도커파일 빌드
* 빌드 완료

기본적인 방법보다 1단계가 줄고, 기초 이미지가 openjdk에서 GCR(Google Container Registry)에서 제공하는 distroles로 변경된다.

1. 컨테이너 용량을 줄여서 빌드하는 과정을 담고 있는 디렉터리로 이동해 어떤 파일이 있는지 살펴보자
```shell
cd ~/_Book_k8sInfra/ch4/4.3.2
ls
```
```shell
build-in-host.sh  Dockerfile  mvnw  pom.xml  src
```

2. 추가된 파일을 cat으로 살펴보자.
```shell
cat build-in-host.sh
```
```shell
#!/usr/bin/env bash
yum -y install java-1.8.0-openjdk-devel
./mvnw clean package
```

3. Dockerfile은 변경이 있다.
```shell
cat Dockerfile
```
```shell
FROM gcr.io/distroless/java:8
LABEL description="Echo IP Java Application"
EXPOSE 60432
COPY ./target/app-in-host.jar /opt/app-in-image.jar
WORKDIR /opt
ENTRYPOINT [ "java", "-jar", "app-in-image.jar" ]
```
사용되는 기초이미지가 openjdk에서 gcr.io/distroless/java로 변경되었다.
distroless는 자바 실행을 위해 경량화된 이미지이다. 기본 방법으로 openjdk 이미지를 설치할 호스트에 자바 개발 도구인 java-1.8.0-openjdk-devel도 함께 설치했다.
그리고 자바 소스를 빌드해서 실행가능한 바이너리인 Jar을 만들어 COPY 명령으로 새롭게 만들어질 컨테이너에 이미지(optimal-img)에 보냈다.
이 과정에서 openjdk 이미지에 포함된 자바 개발 도구는 불필요하게 낭비되는 공간이다.

4. 경량화 이미지를 빌드하기 전에 메이븐에 실행 권한을 부여하자.
```shell
chmod 700 mvnw
```

5. build-in-host.sh를 실행해 경량화 이미지를 빌드한다.
```shell
./build-in-host.sh
```

6. 용량을 줄여 빌드한 컨테이너 이미지와 기본 방법으로 빌드한 이미지를 비교한다.
이때 도커 이미지가 다수 존재하므로 현재 새로 생성된 이미지만 볼 수 있게 head -n 3 옵션을 사용한다.
```shell
docker images | head -n 3
```
```shell
REPOSITORY                           TAG                 IMAGE ID            CREATED              SIZE
optimal-img                          latest              8b21b08e7897        About a minute ago   148MB
basic-img                            latest              d35a68291982        24 hours ago         544MB
```
경량화 빌드를 한 이미지가 용량이 훨씬 작다.

7. 생성한 컨테이너 이미지가 컨테이너로 작동하는지 docker run 명령으로 컨테이너를 실행해 curl로 확인한다.
```shell
docker run -d -p 60432:80 --name optimal-run --restart always optimal-img
curl 127.0.0.1:60432
```
```shell
src: 172.17.0.1 / dest: 127.0.0.1
```

8. 컨테이너가 정상작동하는 것을 확인했으니 빌드한 컨테이너를 삭제한다.
```shell
docker rm -f optimal-run
```
openjdk 이미지에 개발도구가 포힘돼 있는데, 왜 openjdk를 호스트에 설치하고 빌드하고 COPY로 넘기는 번거로운 과정을 진행한 걸까?
매우 좋은 지적이다. 기초 이미지인 openjdk에서 자바 소스를 빌드하면 어떻게 되는지 확인해보자.

### 4.3.3 컨테이너 내부에서 컨테이너 빌드하기
번거로운 과정 없이 바로 자바 소스를 컨테이너 이미지에서 빌드하면 어떻게 되는지 살펴보자.
과정은 다음과 같다.

* 도커파일 작성
* 도커파일 빌드
* 빌드 완료

1. openjdk 이미지에서 자바 소스를 빌드하는 내용이 있는 디렉터리로 이동해 어떤 파일이 있는지 살펴보자.
```shell
cd ~/_Book_k8sInfra/ch4/4.3.3/
ls
```
```shell
Dockerfile
```

2. Dockerfile의 내용을 살펴보면 역시 틀별한 내용이 없다. 이미지 내부에 소스코드를 내려 받으려고 깃을 사용했고, 내려받은 소스 코드를 이미지 내부에서 실행하기 위해 RUN을 추가 했다.
그리고 이미지 내부에서 파일의 위치만 옮기면 되므로 COPY가 아닌 mv를 사용했다.
```shell
cat Dockerfile
```
```shell
FROM openjdk:8
LABEL description="Echo IP Java Application"
EXPOSE 60433
RUN git clone https://github.com/iac-source/inbuilder.git
WORKDIR inbuilder
RUN chmod 700 mvnw
RUN ./mvnw clean package
RUN mv target/app-in-host.jar /opt/app-in-image.jar
WORKDIR /opt
ENTRYPOINT [ "java", "-jar", "app-in-image.jar" ]
```

3. 이미지를 빌드하기 전에 이미지 내부에 내려받은 inbuilder 저장소가 어떤 구조인지 확인한다.
확인해보면 주요 파일은 모두 같다. 
```shell
git clone https://github.com/iac-source/inbuilder.git
```
```shell
Cloning into 'inbuilder'...
remote: Enumerating objects: 53, done.
remote: Counting objects: 100% (53/53), done.
remote: Compressing objects: 100% (36/36), done.
remote: Total 53 (delta 10), reused 38 (delta 2), pack-reused 0 (from 0)
Unpacking objects: 100% (53/53), done.
```
4. docker build로 Dockerfile을 호출해서 컨테이너 이미지를 빌드한다.
```shell
docker build -t nohost-img .
```

5. 새로 빌드한 컨테이너 이미지를 기존 이미지들과 비교 한다. 새로 생성된 nohost-img가 618MB로 이미지 중에 가장 용량이 크다. nohost-img는 컨테이너 내부에서 빌드를 진행하기 때문에 빌드 중간에 생성한 파일들과 내려받은 라이브러리 캐시들이 최종 이미지인 nohost-img에 그대로 남는다.
따라서 빌드 최종 결과물만 전달했던 basic-img 보다 더 커지게 된다.
```shell
docker images | head -n 4
```
```shell
REPOSITORY                           TAG                 IMAGE ID            CREATED              SIZE
nohost-img                           latest              9906e19e479b        About a minute ago   633MB
optimal-img                          latest              8b21b08e7897        15 minutes ago       148MB
basic-img                            latest              d35a68291982        24 hours ago         544MB
```

openJdk 이미지를 기초 이미지로 컨테이너 내부에서 자바 소스로 빌드한 결과, 가장 큰 컨테이너 이미지를 얻었다. 컨테이너 이미지는 커지면 커질 수록 비효율적으로 작동한다.
따라서 openJdk 컨테이너 내부에서 컨테이너를 빌드하는 것은 좋지 않는 방법이다.
하지만 Dockerfile 하나만 빌드하면 컨테이너가 바로 생성되는 편리함을 포기할 수는 없다. 다른 방법은 없을까?

### 4.3.4 최적화해 컨테이너 빌드하기
지금까지 소개한 빌드 방법은 이미지 용량이 커지거나 빌드 과정이 번거로운 등의 단점이 있다. 마지막으로 소개할 멀티 스테이지 빌드 방법은 최종 이미지의 용량을 줄일 수 있고 호스트에 어떠한 빌드 도구도 설치할 필요가 없다.
멀티 스테이지를 이용한 컨테이너 이미지 빌드 과정은 다음과 같다.

* 도커파일 작성
* 도커파일 빌드
* 빌드 완료

멀티 스테이지 빌드는 docker-ce 17.06 버전부터 지원된다. 따라서 현재 우리가 사용하는 도커 버전(docker 1.13.1)을 업그레이드 해야 한다.
따라서 현재 사용 중인 쿠버네티스 클러스터를 삭제하고 docker-ce 18.09.9가 설치된 새로운 쿠버네티스 클러스터를 다시 만들겠다.

1. 쿠버네티스 클러스터를 삭제하기 전에 kubectl get node -o wide 명령으로 현재 사용하는 도커 버전(CONTAINER-RUNTIME 열)을 확인한다.
```shell
kubectl get nodes -o wide
```
```shell
NAME     STATUS   ROLES    AGE    VERSION   INTERNAL-IP     EXTERNAL-IP   OS-IMAGE                KERNEL-VERSION                CONTAINER-RUNTIME
m-k8s    Ready    master   10d    v1.18.4   192.168.1.10    <none>        CentOS Linux 7 (Core)   3.10.0-1160.90.1.el7.x86_64   docker://1.13.1
w1-k8s   Ready    <none>   10d    v1.18.4   192.168.1.101   <none>        CentOS Linux 7 (Core)   3.10.0-1160.90.1.el7.x86_64   docker://1.13.1
w2-k8s   Ready    <none>   10d    v1.18.4   192.168.1.102   <none>        CentOS Linux 7 (Core)   3.10.0-1160.90.1.el7.x86_64   docker://1.13.1
w3-k8s   Ready    <none>   10d    v1.18.4   192.168.1.103   <none>        CentOS Linux 7 (Core)   3.10.0-1160.90.1.el7.x86_64   docker://1.13.1
w4-k8s   Ready    <none>   5d7h   v1.18.4   192.168.1.104   <none>        CentOS Linux 7 (Core)   3.10.0-1160.90.1.el7.x86_64   docker://1.13.1
```

2. 호스트 윈도의 명령 창에서 Vagrantfile에 있는 c:\HashiCorp\_Book_k8sInfra-main\ch3\3.1.3 디렉터리로 이동한다.
기존에 사용하던 가상 머신들을 2장에서 배운 vagrant destroy -f 명령으로 제거 한다.
```shell
cd c:\HashiCorp\_Book_k8sInfra-main\ch3\3.1.3
vagrant destroy -f
```

3. c:\HashiCorp\_Book_k8sInfra-main\ch4\4.3.4\k8s-SingleMaster-18.9_9_w_auto-compl 디렉터리로 이동한다.
vagrant up 명령을 실행해 멀티 스테이지를 지원하는 버전의 도커가 포함된 새로운 쿠버네티스 클러스터 환경을 구성한다.
```shell
cd c:\HashiCorp\_Book_k8sInfra-main\ch4\4.3.4\k8s-SingleMaster-18.9_9_w_auto-compl
vagrant up
```
4. 가상 머신 구성이 완료되면 m-k8s 노드에 접속한다.

5. kubectl get nodes -o wide로 도커 버전을 확인한다.
```shell

```

6. 멀티 스테이지를 위한 파일이 있는 디렉터리(~/_Book_k8sInfra/ch4/4.3.4)로 이동해 Dockerfile이 있는지 확인한다.
```shell
cd ~/_Book_k8sInfra/ch4/4.3.4/
ls
```
```shell
Dockerfile k8s-SingleMaster-18.9_9_w_auto-compl
```

7. Dockerfile을 살펴보면 멀티 스테이지의 핵심은 빌드하는 위치와 최종 이미지를 '분리'하는 것이다. 그래서 최종 이미지는 빌드된 Jar을 가지고 있지만, 용량은 줄일 수 있다.
```shell
FROM openjdk:8 AS int-build # openjdk 이미지에 int-build라는 별칭을 붙임
LABEL description="Java Application builder"
RUN git clone https://github.com/iac-source/inbuilder.git
WORKDIR inbuilder
RUN chmod 700 mvnw
RUN ./mvnw clean package

FROM gcr.io/distoless/java:8
LABEL description="Echo IP Java Application"
EXPOSE 60434
COPY --from=int-build inbuilder/target/app-in-host.jar /opt/app-in-image.jar
WORKDIR /opt
ENTRYPOINT [ "java", "-jar", "app-in-image.jar" ]
```

8. 멀티 스테이지 방식으로 작성된 Dockerfile로 컨테이너 이미지를 빌드한다.
```shell
docker build -t multistage-img .
```

9. 멀티 스테이지로 빌드된 컨테이너 이미지의 용량을 확인하면 optimal-img와 같다. 두 컨테이너 이미지는 빌드 단계가 같고 자바 소스를 호스트에서 빌드했느냐, 컨테이너에서 내에서 빌드했느냐 차이 밖에 없다.
```shell
docker images | head -n 3
```
```shell
REPOSITORY                           TAG                 IMAGE ID            CREATED              SIZE
multistage-img                       latest              f3e2d2fae82b        About a minute ago   148MB
<none>                               <none>              6c0ab6aab3b0        About a minute ago   615MB
```

10. 앞에서 확인한 컨테이너 이미지 중 <none>으로 표시되는 이미지가 있다. 이름이 없는 이런 이미지를 댕글링(dangling) 이미지라고 한다. 멀티 스테이지 과정에서 자바 소스를 빌드 하는 과정에서 생성된 이미지로 보면 된다.
공간을 적게 사용하는 이미지를 만드는 것이 목적이므로 댕글링 이미지(dangling=true)를 삭제한다.
```shell
docker rmi $(docker images -f dangling=true -q)
```
11. docker run을 컨테이너를 실행한다. 생성한 컨테이너 이미지로 빌드한 컨테이너가 잘 동작하는지 curl로 확인한다.
```shell
docker run -d -p 60434:80 --name=multistage-run --restart always multistage-img
curl 127.0.0.1:60434
```
```shell
src: 172.17.0.1 / dest: 127.0.0.1
```
12. 컨테이너가 정상적으로 작동하므로 컨테이너를 삭제하고 다음 실습을 위해 홈 디렉터리로 이동한다.
```shell
docker rm -f multistage-run
```

## 4.4 쿠버네티스에서 직접 만든 컨테이너 사용하기
직접 만든 이미지를 쿠버네티스에서 사용하는 방법을 알아보자.

### 4.4.1 쿠버네티스에서 도커 이미지 구동하기
쿠버네티스는 컨테이너를 효과적으로 다루기 위해 만들어졌고 컨테이너인 파드도 쉽게 부를 수 있다. 따라서 직접 만든 컨테이너 이미지도 kubectl 명령으로 쿠버네티스 클러스터에서 바로 구동할 수 있다.

1. multistage-img 이미지가 노드에 존재하는지 `docker images multistage-img` 명령으로 확인한다.
```shell
docker images multistage-img
```
```shell
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
multistage-img      latest              f3e2d2fae82b        14 hours ago        148MB
```

2. kubectl create 명령으로 디플로이먼트를 생성한다. 이때 --image를 옵션으로 주어 multistage-img를 사용하게 하고 이름은 failure1로 설정한다.
```shell
kubectl create deployment failure1 --image=multistage-img
```

3. `kubectl get pod -w` 파드의 상태 및 변화를 확인한다.
```shell
kubectl get pod -w
```
```shell
NAME                        READY   STATUS         RESTARTS   AGE
failure1-6dc55db9d4-fqkjt   0/1     ErrImagePull   0          43s
failure1-6dc55db9d4-fqkjt   0/1     ImagePullBackOff   0          45s
```
상태가 정상이라면 STATUS에 Running으로 표시돼야 한다. 하지만 이미지를 내려 받는데 문제가 발생해 ErrImagePull, ImagePullBackOff으로 표시된다.
이는 이미지가 호스트에 존재함에도 기본 설정에 따라 이미지를 외부(도커 허브)에서 받으려고 시도하기 때문이다.

4. 이번에는 내부에 존재하는 컨테이너 이미지를 사용하도록 설정해 디플로이먼트를 생성한다. 사용자가 원하는 형태의 디플로이먼트를 만드는 가장 좋은 방법은 현재 수행되는 구문을 yaml 형태로 뽑아내는 것이다.
`--dry-run=client` 옵션은 해당 내용을 실제로 적용하지 않은 채 명령을 수행하고, `-o yaml`은 현재 수행되는 명령을 yaml 형태로 바꾼다.
두 옵션을 조합하면 현재 수행되는 명령을 yaml 형태로 출력해 사용자가 원하는 형태로 변경할 수 있다. `> failure2.yaml`을 붙여 실행 결과를 파일로 저장한다.
```shell
kubectl create deployment failure2 --dry-run=client -o yaml --image=multstage-img > failure2.yaml
```
5. failure2.yaml을 열어 컨테이너 설정에 imagePullPolicy: Never 옵션을 다음과 같이 추가한다. 
이 옵션은 외부에서 이미지를 가져오지 않고 호스트에 존재하는 이미지를 사용하게 한다.
```shell
vi failure2.yaml
```
```shell
spec:
  containers:
    - image: mulistage-img
      imagePullPolicy: Never
      name: multistage-img
      resource: {}
status: {}
```

6. 수정한 failure2.yaml 파일을 디플로이먼트에 적용하고 상태를 확인한다.
```shell
kubectl apply -f failure2.yaml
kubectl get pods
```
```shell
NAME                        READY   STATUS              RESTARTS   AGE
failure1-6dc55db9d4-fqkjt   0/1     ImagePullBackOff    0          10m
failure2-7dddbbfbd4-x6c6q   0/1     ErrImageNeverPull   0          2s
```
여전히 오류가 발생한다. 내부의 이미지를 사용하도록 옵션을 추가했는데 왜 이미지를 가져오지 못할까?

7. 오류가 발생하는 디플로이먼트를 삭제하고 정확히 실습해보자.
```shell
kubectl delete deployment failure1
```

8. w-k8s에 접속한다.

9. 저자가 깃허브에 올려 둔 Dockerfile을 받아 와 테스트를 위한 컨테이너 이미지를 만든다.
```shell
curl -O https://raw.githubusercontent.com/sysnet4admin/_Book_k8sInfra/main/ch4/4.3.4/Dockerfile
```

10. docker build로 컨테이너 이미지 multistage-img를 워커 노드 3번에 빌드하고 결과가 성공적으로 이루어졌는지 확인한다.
```shell
docker build -t multistage-img .
```

11. 마스터 노드로 돌아와 failure2.yaml을 success1.yaml로 복사한다.
```shell
cp failure2.yaml success1.yaml
```

12. sed 명령어로 success1.yaml 파일에 replicas를 1에서 3으로 변경하고 failure2 이름도 success1로 변경한다.
```shell
sed -i 's/replicas: *1/replicas: 3/' success1.yaml
sed -i 's/failure2/success1/' success1.yaml
```
13. 배포에 앞서 w3-k8s의 이미지 빌드가 완료됐는지 확인한다. 이미지 빌드가 완료됐다면 kubectl apply로 succes1.yaml을 실행시키고, kubectl get pods -o wide 명령으로 배포에 성공한 노드가 워커 노드 3번인지 확인한다.
```shell
kubectl apply -f success1.yaml
kubectl get pods -o wide
```
```shell
NAME                        READY   STATUS              RESTARTS   AGE   IP               NODE     NOMINATED NODE   READINESS GATES
success1-6fc588fdf4-c2m2d   0/1     ErrImageNeverPull   0          2s    172.16.103.135   w2-k8s   <none>           <none>
success1-6fc588fdf4-mvvnf   1/1     Running             0          2s    172.16.132.7     w3-k8s   <none>           <none>
success1-6fc588fdf4-wfj96   0/1     ErrImageNeverPull   0          2s    172.16.221.136   w1-k8s   <none>           <none>
```
워커 노드 3번만 배포에 성공했다. 컨테이너 이미지가 워커 노드 3번에만 있기 때문이다.
이 부분을 어떻게 해결해야 할까? 해결 방법은 크게 두 가지가 있다.
기본으로 사용하는 도커 허브에 multistage-img를 올려서 다시 내려 받거나, 쿠버네티스 클러스터가 접근할 수 있는 곳에 이미지 레지스트리를 만들고 그 곳에서 받아오도록 설정하는 것이다.
도커 허브에 올려서 해결하는 것은 너무 쉬우니 좀더 어려운 방법을 알아보자.

14. 다음 실습을 위해 Deployment를 삭제한다.
```shell
kubectl delete -f success1.yaml
```

15. 테스트를 위해 워커 노드 3번에 생성했던 컨테이너 이미지와 댕글링 이미지도 삭제한다.
```shell
docker rmi multistage-img
docker rmi $(docker images -f dangling=true -q)
```

### 4.4.2 레지스트리 구성하기
호스트에서 생성한 이미지를 쿠버네티스에서 사용하려면 모든 노드에서 공통으로 접근하는 레지스트리(저장소)가 필요하다.
도커나 쿠버네티스는 도커 허브라는 레지스트리에서 이미지를 내려 받을 수 있다. 인터넷이 연결돼 있다면 이곳을 이용하면 된다.

때로는 직접 만든 이미지가 외부에 공개되기를 원하지 않는 경우도 있다. 도커 허브에서 제공하는 사설 저장소(private repository)가 있지만,
사설 저장소는 무료 사용자에게는 1개 밖에 허용돼지 않으며 비공개 저장소를 사용하려면 유료 구독을 해야 한다.
또한 무료 사용자는 이미지를 내려받는 횟수에 제약이 있다.

제약 없이 사용할 수 있는 저장소가 필요하다면 레지스트리를 직접 구축하면 된다. 이 경우에는 인터넷을 연결할 필요가 없으므로 보안이 중요한 내부 전산망에서도 구현이 가능하다.
여기서는 도커에서 제공하는 도커 레지스트리 이미지를 사용해 사설 도커 레지스트리를 만들겠다.
도커 레지스트리는 기능은 부족하지만, 컨테이너를 하나만 구동하면 돼서 설치가 간편하고 내부에서 테스트 목적으로 사용하기에 적합하다.

1. 사설 이미지 레지스트리 구성을 위한 파일들을 확인한다.
```shell
ls ~/_Book_k8sInfra/ch4/4.4.2
```
```shell
create-registry.sh  remover.sh  tls.csr
```
디렉터리에는 인증서를 만들어 배포한 뒤 레지스트리를 구동하는 `create-registry.sh` 파일과 인증서를 만들 때 사용하는 `tls.csr` 파일이 있다.
인증서를 생성하려면 서명 요청서(CSR, Certificate signing request)를 작성해야 한다. 
서명 요청서에는 인증서를 생성하는 개인이나 기관의 정보와 인증서를 생성하는데 필요한 몇 가지 추가 정보를 기록한다.
이후 CSR을 기반으로 인증서와 개인키를 생성하는데, 이 예제에서 사용하는 CSR이 `tls.csr` 파일이다.
`remover.sh`는 인증 문제가 생겼을 때 모든 설정을 지우는 스크립트이다.

웹 서버에서 사용하는 인증서를 생성할 때는 서명 요청서 정보 없이 명령줄에서 직접 인증서를 생성한다. 하지만 도커는 이미지를 올리거나 내려받으려고 레지스트리에 접속하는 과정에서
주체 대체 이름(SAN, Subject Alternative Name)이라는 추가 정보를 검증하기 때문에 요청서에 추가 정보를 기입해 인증서를 생성하는 과정이 필요하다.
tls.csr 파일을 살펴 보자.

```shell
[req]
distinguished_name = private_registry_cert_req
x509_extensions = v3_req
prompt = no

[private_registry_cert_req]
C = KR
ST = SEOUL
L = SEOUL
O = gitbut
OU = Book_k8sInfra
CN = 192.168.1.10

[v3_req]
keyUsage = keyEncipherment, dataEncipherment
extendedKeyUsage = serverAuth
subjectAltName = @alt_names

[alt_names]
DNS.0 = m-k8s
IP.0 = 192.168.1.10
```
* 2번 라인: 6번째 줄의 [private_registry_cert_req] 아래의 7~12번째 줄의 정보를 이용해 인증서를 생성한다.
* 3번 라인: 15~17번째 줄의 정보를 추가 정보로 이용한다.
* 6~12번 라인: 인증서 요청자의 국가, 도시, 소속, 이름, 인증서를 설치하는 서버의 주소 등의 정보이다.
* 14~17번 라인: 키의 사용 목적을 기입하고, 19번 라인의 20~21번 라인 정보를 주체 대체 이름으로 사용한다.
* 19~20번 라인: 도메인 이름과 사이트가 일치하는지를 확인할 때 사용하는 추가적인 정보이다.
이 부분이 없으면 도커에서 인증서 검증이 실패해 사설 도커 레지스트리를 정상적으로 사용할 수 없다.

create-registry.sh는 실제로 레지스트리를 생성하고 구동하는 과정이 담긴 스크립트다.
이 스크립트는 인증서 생성과 배포, 레지스트리 생성과 구동의 순서로 이루어져 있다.

```shell
#!/usr/bin/env bash
certs=/etc/docker/certs.d/192.168.1.10:8443
mkdir /registry-image
mkdir /etc/docker/certs
mkdir -p $certs
openssl req -x509 -config $(dirname "$0")/tls.csr -nodes -newkey rsa:4096 -keyout tls.key -out tls.crt -days 365 -extensions v3_req

yum install sshpass -y
for i in {1..3}
  do 
    sshpass -p vagrant ssh -o StrictHostKeyChecking=no root@192.168.1.10$i mkdir -p $certs
    sshpass -p vagrant scp tls.crt 192.168.1.10$i:certs
  done
  
cp tls.crt $certs
mv tls.* /etc/docker/certs

docker run -d \
 --restart always \
 --name registry \ 
  -v /etc/docker/certs:/docker-in-certs:ro \
  -v /registry-image:/var/lib/registry \
  -e REGISTRY_HTTP_ADDR=0.0.0.0:443 \
  -e REGISTRY_HTTP_TLS_CERTIFICATE=/docker-in-certs/tls.crt \
  -e REGISTRY_HTTP_TLS_KEY=/docker-in-certs/tls.key \
  -p 8443:443 \
  registry: 2
```
* 2번 라인: `/etc/docker/certs.d/192.168.1.10:8443`을 `certs`라는 변수에 설정한다.
도커는 `/etc/docker/certs.d` 디렉터리 하위 경로에서 레지스트리 주소와 일치하는 디렉터리에 위치한 인증서를 찾아 레지스트리에 HTTPS 접속을 한다.
따라서 마스터 노드와 워커 노드에 인증서 디렉터리를 생성할 때 변수 certs를 인증서 디렉터리 경로로 사용한다.
* 3번 라인: `/registry-image/` 디렉터리를 생성한다. 22번 라인에 컨테이너 내부의 경로에 연결돼 레지스트리 이미지가 저장된다.
* 4번 라인: `/etc/docker/certs/` 디렉터리를 생성한다. 이 디렉터리는 레지스트리 서버의 인증서들을 보관한다. 24~25번 라인에 레지스트리 컨테이너 내부에 연결돼 인증서를 컨테이너에서도 사용할 수 있게 한다.
* 5번 라인: 변수 certs 에 입력된 경로를 이용해 인증서를 보관할 디렉터리를 생성한다.
* 6번~7번 라인: HTTPS로 접속을 하려면 서버의 정보가 담긴 인증서와 주고 받는 데이터를 암호화와 복호화할 때 사용하는 키가 필요하다.
인증서를 새로 생성하는 요청서가 담긴 tls.csr 파일로 HTTPS 인증서인 tls.crt 파일과 암호화와 복호화에 사용하는 키인 tls.key 파일을 생성한다.
이 중에서 `$(dirname "$0")`는 현재 셸 파일이 실행되는 경로인 ~/_Book_k8sInfra/ch4/4.4.2/를 치환해준다.
* 9번 라인: ssh 접속을 위한 비밀번호를 자동으로 입력하는 sshpass를 설치한다. 별도의 설정이 없다면 ssh 접속 시 비밀번호를 사용자가 키보드로 직접 입력해야 한다. 그러나 사용자가 직접 비밀번호를 입력하면 자동화에 제약이 생긴다.
* 10번 라인: 1~3의 숫자를 반복해 변수 i에 설정하고 10~13번 라인을 반복한다.
변수 i로 워커 노드의 192.168.1.10{i}에 대한 인증서 디렉터리를 생성하고 인증서를 복사하는 작업을 반복한다.
* 12번 라인: 워커 노드에 인증서 디렉터리를 생성한다. sshpass를 이용해 비밀번호를 키보드로 입력하지 않고 vagrant를 ssh 접속 비밀번호로 전달한다. ssh 명령어로 StrictHostKeyChecking=no 옵션을 전달해 ssh로 접속할 때 키를 확인하는 절차를 생략하고 바로 명령을 전달할 수 있게 한다.
9번 라인에서 i에 설정된 숫자를 워커 노드 IP주소의 끝자리로 전달한다.
* 13번 라인: 레지스트리 서버의 인증서 파일을 워커 노드로 복사한다. 9번 라인에서 변수 i에 설정된 워커 노드의 IP주소의 끝자리로 전달한다.
* 16~17번 라인: 6~7번 라인에서 생성한 레지스트리 서버의 인증서 파일인 tls.crt와 암호화와 복호화에 사용하는 키인 tls.key중에 tls.crt를 `/etc/docker/certs.d/192.168.1.10:8443` 디렉터리로 복사하고
tls.crt와 tls.key를 `/etc/docker/certs/` 디렉터리로 옮긴다.
인증서 관련 파일들을 사용해 레지스트리 컨테이너에 들어오는 요청을 인증하고, 인증서가 설치된 호스트에서만 레지스트리에 접근할 수 있게 한다.
* 19~21번 라인: 컨테이너를 백그라운드에서 데몬으로 실행하고 (-d), 정지되면 자동으로 재시작하며 (--restart=always), 생성하는 컨테이너의 이름은 registry(--name registry)로 정한다.
* 22번 라인: 사설 인증서와 관련된 파일들이 위치한 `/etc/docker/certs/` 디렉터리를 컨테이너 내부에서 사용할 수 있도록 -v 옵션으로 컨테이너 내부의 docker-in-certs 디렉터리와 연결한다.
인증서 정보는 외부에서 임의 변경할 수 없더록 안전하게 보관해야 하므로 ro(ReadOnly) 옵션으로 읽기 전용을 설정한다.
* 23번 라인: 레지스트리에 컨테이너 이미지가 계속 저장될 수 있도록 호스트에 저장 공간으로 설정한 registry-image 디렉터리를 컨테이너 내부의 /var/lib/registry/ 디렉터리와 연결한다.
사설 도커 레지스트리는 사용자가 push한 데이터를 내부의 /var/lib/registry/ 디렉터리에 기본으로 저장한다. 별도의 외부 디렉터리에 데이터를 저장하지 않는다면 컨테이너가 새로 구동될 때마다 데이터가 삭제된다.
* 24번 라인: 레지스트리가 요청을 받아들이는 포트로 443번 포트를 설정한다. 443포트는 HTTPS로 접속할 때 사용하는 기본 포트이다.
* 25번 라인: 레지스트리가 사용할 HTTPS 인증서의 경로를 설정한다. 21번 라인에서 연결한 경로 내부에 있는 tls.crt 파일을 HTTPS 인증서로 사용한다.
* 27번 라인: -p 옵션으로 호스트 컴퓨터의 8443번 포트와 컨테이너 내부의 443번 포트로 연결한다. 외부에서 호스트 컴퓨터의 8443번 포트로 요청을 보내면 이 요청은 사설 도커 레지스트리 내부의 443 포트로 전달된다.
* 28번 라인: 도커 허브에 있는 registry 이미지로 레지스트리 컨테이너를 생성한다. 이때 태그 2를 넣어서 레지스트리 2.* 버전 이미지를 사용한다는 것을 명시한다.
나중에 설치를 확인하는 과정에서 버전 2를 의미하는 v2가 경로에 포함된다.

2. create-registry.sh를 실행해 레지스트리를 구성한다. 이 명령으로 인증서 생성 및 배포 작업과 함께 레지스트리를 구동한다.
직접 생성하고 자체적으로 검증하는 인증서를 자체 서명 인증서라고 한다.
```shell
~/_Book_k8sInfra/ch4/4.4.2/create-registry.sh
```

3. registry 컨테이너가 정상적으로 구동되는지 docker ps로 확인한다. PORTS 열을 보면 호스트의 8443번 포트로 들어온 요청을 컨테이너 내부의 443번 포트로 전달한다.
```shell
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                             NAMES
9b35c0e330ae        registry:2          "/entrypoint.sh /etc…"   56 seconds ago      Up 54 seconds       5000/tcp, 0.0.0.0:8443->443/tcp   registry
```
4. 사설 도커 레지스트리에 등록할 수 있게 컨테이너 이미지의 이름을 변경하자. multistage:latest 이미지를 레지스트리에서 읽으려면 레지스트리가 서비스되는 주소(IP와 도메인)와 제공되는 이미지 이름을 레지스트리에 등록될 이름으로 지정해야 한다.
그래야만 해당 정보를 읽어 정상적으로 레지스트리에 등록시킨다. 따라서 docker tag 명령으로 192.168.1.10:8443/multistage-img 라는 multistage-img의 사본을 만든다.
이미지를 따로 만드는 것이 아니라 레이어를 공유하는 사본이 만들어진다. 따라서 원본인 multistage-img가 삭제 돼도 192.168.1.10:8443/multistage-img가 작동하는데 문제가 없다.
두 이미지는 같은 레이어를 바라보는 이름만 다른 존재이기 때문이다.
```shell
docker tag multistage-img 192.168.1.10:8443/multistage-img
```

5. 이미지가 정상적으로 생성됐는지 docker images 192.168.1.10:8443/multistage-img로 확인한다.
```shell
docker images 192.168.1.10:8443/multistage-img
```
```shell
REPOSITORY                         TAG                 IMAGE ID            CREATED             SIZE
192.168.1.10:8443/multistage-img   latest              f3e2d2fae82b        16 hours ago        148MB
```

6. docker push 192.168.1.10:8443/multistage-img로 사설 도커 레지스트리에 이미지를 등록한다.
```shell
docker push 192.168.1.10:8443/multistage-img
```
```shell
The push refers to repository [192.168.1.10:8443/multistage-img]
12385be81a78: Pushed 
1d834f05c29e: Pushed 
b29380a5a354: Pushed 
231bdbae9aea: Pushed 
ba16d454860a: Pushed 
1a5ede0c966b: Pushed 
latest: digest: sha256:c9c95e0462e575f7b0412fb730f1b4e0e60a7f947f1c2abbed8e1c26dec7275b size: 1583
```

7. 이미지가 정상적으로 등록됐는지 확인한다. 사설 도커 레지스트리에 `curl <레지스트리 주소> /v2/_catalog` 요청을 보내면 레지스트리에 등록된 이미지의 목록을 보여준다.
자체 서명 인증서를 쓰는 사이트이기 때문에 `-k`(--insecure) 옵션으로 보안 검증을 생략하고 접속해야 한다.
```shell
curl https://192.168.1.10:8443/v2/_catalog -k
```
```shell
{"repositories":["multistage-img"]}
```
8. 호스트에서 생성한 이미지는 더 이상 사용하지 않으니 삭제한다. 이미지를 삭제하려면 이미지의 ID를 docker images | grep multi 명령으로 알아낸다.
이때 이미지 ID가 동일한 것을 확인할 수 있다. 즉 2개는 완전히 동일한 이미지이다.
```shell
docker images | grep multi
```
```shell
192.168.1.10:8443/multistage-img     latest              f3e2d2fae82b        16 hours ago        148MB
multistage-img                       latest              f3e2d2fae82b        16 hours ago        148MB
```

9. docker rmi -f로 이미지를 삭제한다. -f를 사용한 이유는 같은 ID를 바라보고 있는 2개의 이미지를 한 번에 삭제하기 위함이다.
단순히 이미지 ID로 삭제하려고 하면 이미지가 여러 이름으로 사용되고 있다는 오류가 발생하면서 실행되지 않는다.
```shell
docker rmi f3e2d2fae82b -f 
```
```shell
Untagged: 192.168.1.10:8443/multistage-img:latest
Untagged: 192.168.1.10:8443/multistage-img@sha256:c9c95e0462e575f7b0412fb730f1b4e0e60a7f947f1c2abbed8e1c26dec7275b
Untagged: multistage-img:latest
Deleted: sha256:f3e2d2fae82b77af374d27389e255cacff20620ef537cb37029d9e435602c080
Deleted: sha256:7a46dbe9e150580cabb35e9da7dd58e76240a60b1ffff0e5792b4e5bf3981451
Deleted: sha256:9dafe49d4cb207d237fd80947342c2790af71630d2552a599fde507974ab2962
Deleted: sha256:36c6dbe3c4f2930d89d5ff902a4f93fc47d6960bb2260c550747f16cd33bb8a3
Deleted: sha256:5c84998cb00842984e4d59feb4f2750fd24cab0fa602dba3def5076188c8d8f2
Deleted: sha256:2711e8a2228287466551a39745d49bc6dcf254fcf94972cb565bf4bf0204f7d4
```

10. 이미지가 정상적으로 삭제됐는지 docker images | grep multi로 다시 한 번더 확인한다.
```shell
docker images | grep multi
```
### 4.4.3 직접 만든 이미지로 컨테이너 구동하기
쿠버네티스 클러스터에 속해 있는 노드 어디에서든지 이미지를 내려받을 수 있는 레지스트리를 구성했다. 쿠버네티스에서 파드를 생성할 때 직접 구성한 레지스트리에서 가지고 오는 방법을 확인해 보자.

1. 4.4.1에서 success1.yaml을 복사해 success2.yaml을 생성한다.
```shell
copy success1.yaml success2.yaml
```

2. success2.yaml을 열고 21번 라인을 192.168.1.10:8443/multistage-img로 수정한다.
```shell
vi success2.yaml
```
```shell
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: success1
  name: success1
spec:
  replicas: 3
  selector:
    matchLabels:
      app: success1
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: success1
    spec:
      containers:
      - image: 192.168.1.10:8443/multistage-img
        name: multistage-img
        resources: {}
status: {}
```
3. 워커 노드 3번에 배포한 이미지와 중복되지 않게 success2.yaml에 설정된 이름인 success1을 모두 success2로 변경한다.
```shell
sed -i 's/success1/success2/' success2.yaml
```

4. success2.yaml로 deployment를 생성한다.
```shell
kubectl create -f success2.yaml
```
5. 생성된 디플로이먼트가 정상적으로 작동하는지 확인한다.
```shell
kubectl get pods -o wide
```
```shell
NAME                        READY   STATUS    RESTARTS   AGE   IP               NODE     NOMINATED NODE   READINESS GATES
success2-6575dfbf95-kxccd   1/1     Running   0          10s   172.16.132.12    w3-k8s   <none>           <none>
success2-6575dfbf95-rzv4z   1/1     Running   0          10s   172.16.221.141   w1-k8s   <none>           <none>
success2-6575dfbf95-tt6xn   1/1     Running   0          10s   172.16.103.143   w2-k8s   <none>           <none>
```

6. 배포된 파드가 요청에 정상적으로 응답하는지 curl로 확인한다.
```shell
curl 172.16.132.12
curl 172.16.221.141
curl 172.16.103.143
```
```shell
src: 172.16.171.64 / dest: 172.16.132.12
src: 172.16.171.64 / dest: 172.16.221.141
src: 172.16.171.64 / dest: 172.16.103.143
```
7. 직접 구성한 레지스트리에 올린 이미지로 디플로이먼트가 배포됨을 확인했다. 다음 실습을 위해 디플로이먼트를 삭제한다.
```shell
kubectl delete -f success2.yaml
```
---
# 5. 지속적 통합과 배포 자동화, 젠킨스
컨테이너로 구동하는 애플리케이션을 어떻게 배포하는 것이 가장 좋을까?
4장에서 진행한 과정을 정리하면 다음과 같다.

1. 깃허브 등의 저장소에 저장해둔 애플리케이션 소스 코드를 내려받아 도커 컨테이너 이미지로 빌드한다.
2. 빌드한 컨테이너 임지리를 쿠버네티스에서 사용할 수 있도록 레지스트리에 등록한다.
3. 레지스트리에 등록된 이미지를 기반으로 쿠버네티스 오브젝트를 생성한다.
4. 생성한 오브젝트(파드/디플로이먼트)를 외부에서 접속할 수 있도록 서비스 형태로 노출한다.

이런 과정을 파이프라인(Pipeline)이라고 한다. 기존에는 파이프라인을 사람이 하나하나 수작업으로 진행했지만, 이제는 도구를 사용해 자동화를 할 수 있다.
자동화는 크게 지속적 통합(CI, Continuous Integration), 지속적 배포(CD, Continuous Deployment) 두 가지로 정의되며,
일반적으로 둘을 합쳐 CI/CD라고 한다.

## 5.1 컨테이너 인프라 환경에서 CI/CD
CI는 코드를 커밋하고 빌드했을 때 정상적으로 작동하는지 반복적으로 검증해 애플리케이션의 신뢰성을 높이는 작업이다.
CI 과정을 마친 애플리케이션은 신뢰할 수 있는 상태가 된다.

CD는 CI 과정에서 생성된 신뢰할 수 있는 애플리케이션을 실제 상용 환경에서 자동으로 배포하는 것을 의미한다.
애플리케이션을 상용 환경에 배포할 때 고려해야 할 사항이 이려거 가지 있는데, 이를 CD에 미리 정의하면 실수를 줄이고, 실제 적용 시간도 최소화할 수 있다.

### 5.1.1 CI/CD 도구 비교
CI/CD를 제공하는 도구는 매우 많지만, 대표적인 CI/CD 도구를 비교해 왜 젠킨스를 선택하고 다루는지 알아보자.
오픈소스 CI/CD 도구로, 젠킨스는 사용자가 직접 UI에서 작업을 구성하거나 작업 순서를 코드로 정의할 수 있다.
역사, 인지도, 사용자 수에서 CI/CD 도구의 대명사라고 해도 무리가 없을 정도로 널리 알려져 있다.
사용자가 많기 때문에 필요한 정보를 찾기 쉽고 활용 방법과 플러그인 개발 관련 커뮤니티 활동이 활발하다.
젠킨스는 거의 모든 환경에 사용할 수 있도록 다양한 플러그인을 추가해 원하는 형태를 만드는 블록 방식으로 구성돼 있다.
따라서 CI/CD 시작은 가장 대중적인 젠킨스로 하는 것이 좋다.

### 5.1.2 젠킨스 설치를 위한 간편화 도구 살펴보기
애플리케이션 배포 영역에 쿠버네티스를 사용하면 개발자는 애플리케이션 개발에만 집중할 수 있게 된다.
기존에는 환경이 다른 곳에 빌드한 애플리케이션을 배포하게 되면 개발자가 개발 환경에 맞춰 애플리케이션 코드를 일일이 수정해야 했다.
하지만 모든 배포 환경을 컨테이너 인프라로 일원화하고, CI/CD 도구를 사용하면 애플리케이션에 맞는 환경을 적용해 자동으로 배포할 수 있다.
그리고 통합 과정에서 만들어진 컨테이너 이미지를 기반으로 쿠버네티스가 존재하는 어떤 환경에서도 일관성이 있는 애플리케이션을 배포할 수 있다.

개발자가 작성한 애플리케이션 코드를 소스 코드 저장소에 푸시하면, 
쿠버네티스 내부에 설치된 젠킨스는 애플리케이션 코드를 빌드하고, 
레지스트리에 푸시한 후에 쿠버네티스에서 사용 가능한 형태로 배포한다.

젠킨스는 작업 내용을 아이템(Item) 단위로 정의하고 조건에 따라 자동으로 작업을 수행해 효율을 높이고 실수를 줄인다.
컨테이너 인프라 환경에서 젠킨스를 사용하는 주된 이유는 애플리케이션을 컨테이너로 만들고 배포하는 과정을 자동화하기 위해서이다.
하지만 자동화 환경은 단순히 젠킨스용 파드만을 배포해서 만들어지지 않는다.
젠킨스는 컨트롤러와 에이전트 형태로 구성한 다음 배포해야 하며 여기에 필요한 설정을 모두 넣어야 한다.
애플리케이션을 배포하기 위한 환경을 하나하나 구성하는 것은 매우 복잡하고 번거로운 일이며, 고정된 값이 아니기 때문에 
매니페스트로 작성해 그대로 사용할 수가 없다. 구성 환경에 따라 많은 부분을 동적으로 변경해야 한다.
동적인 변경 사항을 간편하고 빠르게 적용할 수 있도록 도와주는 도구가 있다.
하나는 커스터마이즈(Kustomize)이고, 다른 하나는 헬름(Helm)이다.

## 5.2 젠킨스를 설치하기 위한 간편화 도구 살펴보기

### 5.2.1 배포 간편화 도구 비교하기
그동안 사용한 kubectl은 사실 바이너리 실행 파일로 짜인 배포 도구이다.
kubectl이 없으면 직접 코드를 짜서 API 서버에 명령을 내려야 한다.
커스터마이즈와 헬름은 kubectl을 좀 더 확장해서 복잡한 오브젝트와 구성 환경을 자동으로 맞추는 도구이다.

* kubectl(큐브시티엘): 쿠버네티스에 기본으로 포함된 커맨드라인 도구로, 추가 설치 없이 바로 사용할 수 있다.
오브젝트 생성과 쿠버네티스 클러스터에 존재하는 오브젝트, 이벤트 등의 정보를 확인하는데 사용하는 활용도 높은 도구이다.
또한 오브젝트의 명세가 정의된 야믈 파일을 인자로 입력받아 파일 내용에 따라 오브젝트를 배포할 수도 있다.
kubectl은 정의된 매니페스트 파일을 그대로 배포하기 때문에 개별적인 오브젝트를 관리하거나 배포할 때 사용하는 것이 좋다.

* kustomize(커스터마이즈): 오브젝트를 사용자의 의도에 따라 유동적으로 배포할 수 있다.
별도의 커스터마이즈 실행 파일을 활용해 커스터마이즈 명세를 따르는 야믈 파일을 생성할 수 있다.
야믈 파일이 이미 존재한다면 kubectl로도 배포할 수 있는 옵션이 있을 정도로 kubectl과 매우 밀접하게 동작한다.
커스터마이즈는 명세와 관련된 야믈 파일에 변수나 템플릿을 사용하지는 않지만, 
명령어로 배포 대상 오브젝트의 이미지 태그와 레이블 같은 명세를 변경하거나 일반 파일을 이용해 컨피그맵과 시클릿을 생성하는 기능을 지원한다.
그래서 운영 중인 환경에서 배포 시 가변적인 요소를 적용하는데 적합하다.

* 헬름(Helm): 헬름은 쿠버네티스 사용자의 70% 이상이 사용하고 있을 정도로 널리 알려진 도구로, 
오브젝트 배포에 필요한 사양이 이미 정의된 차트라는 패키지를 활용한다.
앞선 두 가지 도구와 달리 헬름 차트 저장소가 온라인에 있기 때문에 패키지를 검색하고 내려받아 사용하기가 매우 간편하다.
헬름 차트는 자체적인 템플릿 문법을 사용하므로 가변적인 인자를 배포할 때 적용해 다양한 배포 환경에 맞추거나 원하는 조건을 적용할 수 있다.
헬름은 오브젝트를 묶어 패키지 단위로 관리하므로 단순한 1개의 명령어로 애플리케이션에 필요한 오브젝트들을 구성할 수 있다.

### 5.2.2 커스터마이즈로 배포 간편화하기
> 커스터마이즈의 작동 원리

커스터마이즈는 야믈 파일에 정의된 값을 사용자가 원하는 값으로 변경할 수 있다.
쿠버네티스에서 오브젝트에 대한 수정 사항을 반영하려면 사용자가 직접 야믈 파일을 편집기로 수정해야 한다.
일반적으로 이런 방식으로 수정했을 때 큰 문제가 발생하지 않는다.
그런데 만약 수정해야하는 야믈 파일이 매우 많거나 하나의 야믈 파일로 환경이 다른 여러 개의 쿠버네티스 클러스터에 배포해야 해서
LABEL이나 NAME 같은 일부 항목을 수정해야 한다면 매번 일일이 고치는 데 많은 노력이 든다.
커스터마이즈는 이를 위해 `kustomize` 명령을 제공한다.
`kustomize` 명령과 `create` 옵션으로 `kustomization.yaml`이라는 기본 매니페스트를 만들고, 
이 파일에 변경해야하는 값들을 적용한다. 그리고 `build` 옵션으로 변경할 내용이 적용된 최종 야믈 파일을 저장하거나 변경된 내용이 바로 실행되도록 지정한다.

그러면 이제 커스터마이즈로 MetalLB를 구성해보자.
커스터마이즈를 사용해서 MetalLB를 만든다는 것은 사실상 명세서인 kustomization.yaml을 만드는 과정이다.
그리고 만들어진 kustomization.yaml을 통해서 우리가 원하는 내용이 담긴 MetalLB 매니페스트를 생성하고,
이 매니페스트를 통해서 배포하는 것이다. 즉 커스터마이즈는 단순히 최종 매니페스트 생성을 도와주는 도구인 것이다.

1. 커스터마이즈 명령을 사용하기 위해 ~/_Book_k8sInfra/ch5/5.2.2/kustomize-install.sh를 실행해 커스터마이즈 압축 파일을 내려 받고 이를 해제하고
/usr/local/bin을 옮기자.

2. 커스터마이즈에 리소스 및 주소 할당 영역(Pool)을 구성할 때 사용할 파일드을 확인하기 위해서 ~/_Book_k8sInfra/ch5/5.2.2 디렉터리로 이동하고
metallb-l2config.yaml, metallb.yaml, namespace.yaml이 있는 것을 확인한다.

3. 커스터마이즈로 변경될 작업을 정의하기 위해 `kustomize create --namespace=metallb-system --resources namespace.yaml,metallb-l2config.yaml` 명령으로 kutomization.yaml을 생성하겠다.
이때 --namespace는 작업의 네임스페이스를 설정하며, --resources 멸영은 커스터마이즈 명령을 이용해서 kustomization.yaml을 만들기 위핸 소스 파일을 정의한다.
```shell
kustomize create --namespace=metallb-system --resources namespace.yaml,metallb-l2config.yaml
```
4. 생성한 kustomziation.yaml 파일을 확인해 보면, 리소스로 namespace.yaml, metallb.yaml 그리고 metallb-l2config.yaml이 설정됐고, 
네임스페이스는 metallb-system으로 설정된 것을 확인할 수 있다.
```shell
cat kustomization.yaml
```
```shell
apiVersion: kustomize.config.k8s.io/v1beta1
kind: Kustomization
resources:
- namespace.yaml
- metallb-l2config.yaml
namespace: metallb-system
```
5. 설치된 이미지를 안정적인 버전으로 유지하기 위해서 `kustomize edit set image` 옵션을 이용해
MetalLB controller와 speaker의 이미지 태그를 v0.8.2로 지정한다.
```shell
kustomize edit set image metallb/controller:v0.8.2
kustomize edit set image metallb/speaker:v0.8.2
```

6. 커스터마이즈로 생성된 kustomization.yaml에 이미지 태그 정보(v0.8.2)가 설정됐는지 확인한다.
```shell
cat kustomization.yaml
```
```shell
apiVersion: kustomize.config.k8s.io/v1beta1
kind: Kustomization
resources:
- namespace.yaml
- metallb-l2config.yaml
namespace: metallb-system
images:
- name: metallb/controller
  newTag: v0.8.2
- name: metallb/speaker
  newTag: v0.8.2
```
7. 이제 `kustomize build` 명령을 MetalLB 설치를 위한 매니페스트를 생성해보면, 다음과 같이 metallb-l2config.yaml을 통해서 컨피그맵이 만들어졌으며
이미지 태그인 v0.8.2가 적용된 것을 확인할 수 있다.
```shell
kustomize build
```
```shell
apiVersion: kustomize.config.k8s.io/v1beta1
kind: Kustomization
resources:
- namespace.yaml
- metallb-l2config.yaml
namespace: metallb-system
images:
- name: metallb/controller
  newTag: v0.8.2
- name: metallb/speaker
  newTag: v0.8.2
[root@m-k8s 5.2.2]# kustomize build
apiVersion: v1
kind: Namespace
metadata:
  labels:
    app: metallb
  name: metallb-system
---
apiVersion: v1
data:
  config: |
    address-pools:
    - name: metallb-ip-range
      protocol: layer2
      addresses:
      - 192.168.1.11-192.168.1.19
kind: ConfigMap
metadata:
  name: config
  namespace: metallb-system
```
8. 이를 파일로 저장해 MetalLB를 배포할 수도 있지만, 편의를 위해서 `kustomize build | kubectl apply -f -` 명령으로 빌드한 결과가 바로 kubectl apply에 인자로 전달돼 배포되도록 하겠다.
```shell
kustomize build | kubectl apply -f -
```
```shell
namespace/metallb-system created
serviceaccount/controller created
serviceaccount/speaker created
podsecuritypolicy.policy/speaker created
role.rbac.authorization.k8s.io/config-watcher created
clusterrole.rbac.authorization.k8s.io/metallb-system:controller created
clusterrole.rbac.authorization.k8s.io/metallb-system:speaker created
rolebinding.rbac.authorization.k8s.io/config-watcher created
clusterrolebinding.rbac.authorization.k8s.io/metallb-system:controller created
clusterrolebinding.rbac.authorization.k8s.io/metallb-system:speaker created
configmap/config created
deployment.apps/controller created
daemonset.apps/speaker created
```
9. MetalLB가 정상적으로 배포됐는지 `kubectl get pods -n metallb-system` 명령과 `kubectl get configmaps -n metallb-system` 명령으로 확인한다.
```shell
kubectl get pods -n metallb-system
kubectl get configmaps -n metallb-system
```
```shell
NAME                          READY   STATUS    RESTARTS   AGE
controller-5d48db7f99-948pf   1/1     Running   0          101s
speaker-2jp7j                 1/1     Running   0          101s
speaker-69hd4                 1/1     Running   0          101s
speaker-9vswn                 1/1     Running   0          101s
speaker-mwfrg                 1/1     Running   0          101s
```
```shell
NAME     DATA   AGE
config   1      111s
```

10. `kubectl describe pods -n metallb-system | grep Image:` 명령으로 커스터마이즈를 통해서 고정한 MetalLB의 태그가 v0.8.2인지 확인한다.
```shell
kubectl describe pods -n metallb-system | grep Image:
```
```shell
    Image:         quay.io/metallb/controller:v0.8.2
    Image:         quay.io/metallb/speaker:v0.8.2
    Image:         quay.io/metallb/speaker:v0.8.2
    Image:         quay.io/metallb/speaker:v0.8.2
    Image:         quay.io/metallb/speaker:v0.8.2
```
11. 커스터마이즈를 통해서 MetalLB가 생성된 것을 확인했으니 간단하게 테스트해보자. 디플로이먼트 1개를 배포한 다음 LoadBalancer 타입으로 노출하고 IP가 정상적으로 할당됐는지 확인한다.
```shell
kubectl create deployment echo-ip --image=sysnet4admin/echo-ip
kubectl expose deployment echo-ip --type=LoadBalancer --port=80
```
12. 호스트OS에서 브라우저로 192.168.1.11을 입력해 echo-ip가 정상적으로 응답하는지 확인한다.

13. 다음 실습을 위해 MetalLB를 삭제하고 배포했던 echo-ip 관련 오브젝트를 삭제한다.
```shell
kustomize build | kubectl delete -f -
kubectl delete service echo-ip
kubectl delete deployment echo-ip
```

커스터마이즈를 이용하면 MetalLB의 다양한 설정을 사용자의 입맛에 맞게 변경하고 구현할 수 있다.
그러나 커스터마이즈는 여러 가지 변경할 부분을 사용자가 직접 kustomization.yaml에 추가하고 최종적으로 필요한 매니페스트를 만들어 배포해야 한다.
이러한 다소 수동적인 작성방식이 아닌 선언적으로 필요한 내용을 제공하고 이에 맞게 바로 배포하려면 어떻게 해야 할까?
그리고 커스터마이즈를 통해 변경할 수 없었던 주소 할당 영역과 같은 값도 배포 시에 같이 변경하려면 어떻게 해야 할까?
헬름은 이러한 제약 사항들을 업애고 편리성을 높일 수 있다.

### 5.2.3 헬름으로 배포 간편화하기
헬름을 통한 배포는 커스터마이즈에서 제한적이었던 주소 할당 영역과 같은 값을 대체하면서 간단하게 설치할 수 있도록 설계돼 있다.
헬름의 작동 원리와 헬름에서 호출하는 차트를 살펴보자.

> 헬름의 작동 원리

헬림은 쿠버네티스에 패키지를 손쉽게 배포할 수 있도록 패키지를 관리하는 쿠버네티스 전용 패키지 매니저이다.
일반적으로 패키지는 실행 파일뿐만 아니라 실행 환경에 필요한 의존성 파일과 환경 정보들의 묶음이다.
패키지 매니저는 외부에 있는 저장소에서 패키지 정보를 받아와 패키지를 안정적으로 관리하는 도구이다.

컨테이너 인프라 환경에서 애플리케이션을 배포하려면 ConfigMap, ServiceAccount, PV, PVC, Secret 등 애플리캐이션 배포 구성에 필요한 모든 쿠버네티스 오브젝트를 작성하고,
kubectl 명령을 실행해서 쿠버네티스 클러스터에 설치해야 한다.
이때 커스터마이즈를 사용하면 많은 부분을 환경에 맞춰 변경할 수 있지만, 주소 할당 영역과 같은 정보는 값의 형태가 아니라서
변경할 수 없다. 이런 경우에 헬름을 사용하면 주소 할당 영역도 변경이 가능하다.
이 외에도 헬름은 여러 장점이 있다.
다수의 오브젝트 배포 야믈은 파일 구분자인 `---`로 묶어 단일 야믈로 작성해 배포할 수 있다.
이런 경우 변경 사항을 추적할 때 모든 내용이 한 야믈 파일에 담겨 있기 때문에 여러 사람이 동시에 작업하면 충돌이 발생할 수 있다.
문제를 해결하려면 목적에 맞게 디렉터리를 만들고 야믈 파일을 분리해 관리하면서 배포 시에는 디렉터리를 kubectl apply -f의 인자로 넘겨 줘야 한다.
하지만 이런 방식을 사용하면 요구 조건에 변경되는 야믈 파일을 매번 개별 디렉터리에 작성해야 하고 디렉터리가 늘어날수록 관리 영역도 늘어나게 된다.

헬름을 사용하면 요구 조건별로 리소스를 편집하거나 변수를 넘겨서 처리하는 패키지를 만들 수 있다.
이렇게 다양한 요구 조건을 처리할 수 있는 패키지를 차트(chart)라고 하는데, 이를 헬름 저장소에 공개해 여러 사용자와 공유 한다.
각 사용자는 공개된 저장소에 등록된 차트를 이용해 애플리케이션을 원하는 형태로 쿠버네티스에 배포할 수 있다.
또한, 헬름은 배포한 애플리케이션을 업그레이드 하거나 되돌실 수 있는 기능과 삭제할 수 있는 기능을 제공한다.

헬름의 작동 과정은 다음과 같다.
* 생산자 영역: 생산자가 헬름 명령으로 작업 공간을 생성하면 templates 디렉터리로 애플리케이션 배포에 필요한 여러 야믈 파일과 구성을 작성할 수 있다.
이때 templates 디렉터리에 조건별 분기, 값 전달 등을 처리할 수 있도록 values.yaml에 설정된 키를 사용한다.
이때 값이 전달되지 않으면 기본값으로 처리하도록 values.yaml에 설정할 수 있다.
이렇게 필요한 패키지의 여러 분기 처리나 배포에 대한 구성이 완료되면 생산자는 차의 이름, 목적, 배포되는 애플리케이션 버전 과 같은 패키지 정보를 Charts.yaml에 채워 넣는다.
앞의 과정을 모두 거쳐 차트 구성이 완료되면 생산자가 저장소에 업로드 한다. 그리고 업로드한 생산자가 저장소를 아티팩트허브에 등록하면 사용자는 아티팩트 허브에서 생산자가 만든 저장소를 찾을 수 있다.

* 아티팩트허브 영역: 아티팩트허브 검색을 통해 사용자가 찾고자 하는 애플리케이션 패키지를 검색하면 해당 패키지가 저장된 주소를 확인한다. 이렇게 확인한 주소는 각 애플리케이션을 개발하는 주체가 관리한다.
헬름 버전2에서는 이러한 차트 저장소를 개인이 아닌 CNCF가 관리했으나 헬름 버전3가 배포되고 나서는 CNCF가 관리해야 하는 차트가 많아지면서 모든 차트 저장소는 개인 및 단체에서 직접 관리하도록 정책을 변경했다.

* 사용자 영역: 사용자는 설치하려는 애플리케이션의 차트 저장소 주소를 아티팩트허브에서 얻으면 헬름을 통해서 주소를 등록한다. 그리고 이를 최신으로 업데이트한 이후에 차트를 내려받고 설치한다.
이렇게 헬름을 통해 쿠버네티스에 설치된 애플리케이션 패키지를 릴리스라고 한다. 헬름을 통해 배포된 릴리스를 다시 차트를 사용해 업그레이드 할 수 도있고 원래대로 되돌릴 수 있다.
또한 사용하지않는 헬름 릴리스를 제거할 수도 있다.

헬름으로 MetalLB 한 번에 만들기
1. 헬름 명령을 사용하기 위해서 ~/_Book_k8sInfra/ch5/5.2.3/helm-install.sh를 실행해 헬름을 설치하자.
```shell
export DESIRED_VERSION=v3.2.1; ~/_Book_k8sInfra/ch5/5.2.3/helm-install.sh
```
helm-install.sh를 실행하면 항상 최신 버전의 헬름을 내려 받기 때문에 호환성 이슈를 방지하기 위해 DESIRED_VERSION 환경 변수를 설정해 헬름 버전 v3.2.1로 고정해 설치하겠다.
헬름 실행 파일도 /usr/local/bin에 위치한다.

2. MetalLB를 설치하려면 헬름 차트를 등록할 주소를 알아야 한다. 아티팩트허브(https://artifacthub.io)에서 metallb를 검색해 주소를 확인한다.

3. metallb의 상세 페이지에서는 차트 저장소(helm-charts) 등록법 외에도 차트에 대한 다양한 정보도 함께 제공한다.
상세 페이지를 통해서 추가해야 하는 차트 주소 및 등록하는 방법도 함께 확인할 수 있다.

4. 헬름 차트 저장소의 주소도 확인했으니 실제 저장소를 helm repo add 명령으로 등록해서 MetalLB를 설치할 준비를 하자.
여기서 혼동이 올 수 있는 부분이 있다.
헬름 차트 저장소인 `https://iac-source.github.io/helm-charts` 는 저자가 만든 저장소로, 아티팩트허브에 이 경로만을 표시한다는 점을 다시 한 번 기억해주기 바란다.
그리고 edu는 헬름 차트 저장소를 대표하는 이름의 역할을 하는 것으로 자유롭게 변경 등록이 가능하지만, 이 책에서는 edu를 기반으로 작성됐기 때문에 edu를 사용하기 바란다.
```shell
helm repo add edu https://iac-source.github.io/helm-charts
```
```shell
"edu" has been added to your repositories
```

5. 헬름 차트 저장소가 정상적으로 등록됐는지 helm list 명령으로 저장소 목록을 확인하겠다.
```shell
helm repo list
```
```shell
NAME    URL                                     
edu     https://iac-source.github.io/helm-charts
```
확인한 결과 edu라는 이름의 차트 저장소가 등록된 것을 확인할 수 있다.

6. 헬름으로 차트 저장소를 추가한 시점의 차트를 로컬 캐시에 저장해 install과 같은 작업 수행시에 먼저 로컬에 있는 캐시 차트 정보를 참조한다.
만약 저장소 추가 이후에 변경된 차트가 있다면 변경된 정보를 캐시에 업데이트할 수 있도록 helm repo update 명령을 통해 최신 차트정보를 동기화 한다.
이는 관습적으로 이루어지는 것으로 현재의 랩에서는 필요한 요소는 아니지만 이렇게 진행하는 것이 나중에 일어날 수 있는 문제를 방지할 수 있다.
```shell
helm repo update
```
```shell
Hang tight while we grab the latest from your chart repositories...
...Successfully got an update from the "edu" chart repository
Update Complete. ⎈ Happy Helming!⎈ 
```
7. 앞서 등록 및 업데이트한 저장소 edu로부터 MetalLB를 설치하겠다. 헬름 차트를 설치할 때 사용하는 명령어는 `helm install`이며 커스터마이즈와 다르게 인자를 바로 명령줄에서 받아서 처리한다.
현재 사용하는 인자는 다음과 같다. 
* `--namespace`: 헬름 차트를 통해서 생성되는 애플리케이션이 위치할 네임스페이스를 지정한다.
* `--create-namespace`: 네임스페이스 옵션으로 지정된 네임스페이스가 존재하지 않는 경우 네임스페이스를 생성한다.
* `--set`: 헬름에서 사용할 변수를 명령 인자로 전달한다. `key1=value1, key2=value2`와 같이 `,`를 사용해 한 줄에서 여러 인자를 넘겨 줄 수 있으나 가독성을 높이기 위해 `,`로 여러 인자를 넘겨 사용하지 않았다.

일반적으로 배포 이후에 간략한 메세지와 함께 제작자가 작성한 사용 설명서가 함께 출력된다.
이를 통해서 배포가 완료됐음을 확인할 수 있다.
이후 실습에서 설치하는 헬름 차트는 지금 배포한 MetalLB보다 더 많은 인자를 입력 받기 때문에 이후 실습에서는 편의를 위해서 사전에 구성된 스크립트를 통해 차트를 설치하겠다.
```shell
`helm install metallb edu/metallb \
--namespace=metallb-system \
--create-namespace \
--set controller.tag=v0.3.3 \
--set speaker.tag=v0.8.3 \
--set configmap.ipRange=192.168.1.11-192.168.1.29`
```
```shell
NAME: metallb
LAST DEPLOYED: Mon Dec 30 21:25:40 2024
NAMESPACE: metallb-system
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
MetalLB load-balancer is successfully installed.
1. IP Address range 192.168.1.11-192.168.1.29 is available.
2. You can create a LoadBalancer service with following command below.
kubectl expose deployment [deployment-name] --type=LoadBalancer --name=[LoadBalancer-name] --port=[external port]
```
8. 설치된 MetalLB가 정상적인 상태인지 배포 상태를 확인한다.
```shell
kubectl get pods -n metallb-system
kubectl get configmap -n metallb-system
```
```shell
NAME                          READY   STATUS             RESTARTS   AGE
controller-5f84f746cc-f5snt   0/1     ImagePullBackOff   0          104s
speaker-87h2g                 1/1     Running            0          104s
speaker-j8mrk                 1/1     Running            0          104s
speaker-nf4xk                 1/1     Running            0          104s
speaker-ppq2s                 1/1     Running            0          104s
```
```shell
NAME     DATA   AGE
config   1      2m13s
```
9. kubectl describe pods -n metallb-system | grep Image: 명령으로 헬름 set 옵션을 통해 변경된 MetalLB의 태그가 v0.8.3인지 확인한다.
```shell
kubectl describe pods -n metallb-system | grep Image:
```
```shell
    Image:         quay.io/metallb/controller:v0.3.3
    Image:         quay.io/metallb/speaker:v0.8.3
    Image:         quay.io/metallb/speaker:v0.8.3
    Image:         quay.io/metallb/speaker:v0.8.3
    Image:         quay.io/metallb/speaker:v0.8.3
```
10. 헬름을 통해서 MetalLB가 생성된 것을 확인했으니 간단하게 테스트를 해보자.
디플로이먼트 1개를 배포하고 LoadBalancer 타입으로 노출하고 IP가 정상적으로 할당됐는지 확인한다.
```shell
kubectl create deployment echo-ip --image=sysnet4admin/echo-ip
kubectl expose deployment echo-ip --type=LoadBalancer --port=80
kubectl get service echo-ip
```
```shell
deployment.apps/echo-ip created
```
```shell
service/echo-ip exposed
```
```shell
NAME      TYPE           CLUSTER-IP    EXTERNAL-IP    PORT(S)        AGE
echo-ip   LoadBalancer   10.98.56.23   192.168.1.11   80:31260/TCP   10s
```

11. 이후 실습에서 MetalLB는 계쏙 사용할 것이므로 배포했던 echo-ip 관련 오브젝트만 삭제한다.
```shell
kubectl delete service echo-ip
kubectl delete deployment echo-ip
```
 
## 5.3 젠킨스 설치 및 설정하기

### 5.3.1 헬름으로 젠킨스 설치하기
1. 젠킨스로 지속적 통합을 진행하는 과정에서 컨테이너 이미지를 레지스트리에 푸시하는 단계가 있다.
이때 이미지를 저장하는 레지스트리는 앞서 '4.4.2 레지스트리 구성하기'에서 구성한 이미지 레지스트리를 사용한다.
다음과 같은 실행 결과가 나오지 않는다면 4장의 실습을 통해 레지스트리를 우선 구성하기 바란다.
```shell
docker ps -f name=registry
```

2. 헬름으로 설치되는 젠킨스는 파드에서 동작하는 애플리케이션이기 때문에 PV를 마운트 하지 않으면 파드가 다시 시작될 때 내부 볼륨에 저장하는 모든 데이터가 삭제 된다.
이를 방지하기 위해서 애플리케이션의 PV가 NFS를 통해 프로비저닝될 수 있게 NFS 디렉터리를 /nfs_shared/jenkins에 만들겠다.
미리 정의된 nfs-exporter.sh jenkins를 실행한다.
이 스크립트는 NFS용 디렉터리를 만들고 이를 NFS 서비스를 생성하는 과정이 담겨 있다.
```shell
~/_Book_k8sInfra/ch5/5.3.1/nfs-exporter.sh jenkins
```
```shell
Created symlink from /etc/systemd/system/multi-user.target.wants/nfs-server.service to /usr/lib/systemd/system/nfs-server.service.
```
3. 만들어진 디렉터리에 부여된 사용자 ID(uid)와 그룹 ID(gid)의 번호를 -n 옵션으로 확인한다. 0번은 root 사용자에 속해 있다는 의미이다.
```shell
ls -n /nfs_shared
```
```shell
drwxr-xr-x. 2 0 0 6 Dec 31 19:19 jenkins
```

4. 젠킨스를 헬름 차트로 설치해 애플리케이션을 사용하게 되면 젠킨스의 여러 설정 파일과 구성 파일들이 PVC를 통해 PV에 파일로 저장된다.
이때 PV에 적절한 접근 ID를 부여하지 않으면 PVC를 사용해 파일을 읽고 쓰는 기능에 문제가 발생할 수 있다.
이런 문제를 방지하기 위해서 `chown 1000:1000 /nfs_shared/jenkins` 명령어로 젠킨스 PV가 사용할 NFS 디렉터리에 대한 접근 ID(사용자 ID, 그룹 ID)를 1000번으로 설정하겠다.
1000번으로 설정한 이유는 젠킨스 컨트롤러 이미지에 기본적으로 사용하는 유저 ID와 그룹 ID가 1000번이기 때문이다.
```shell
chown 1000:1000 /nfs_shared/jenkins/
ls -n /nfs_shared
```
```shell
drwxr-xr-x. 2 1000 1000 6 Dec 31 19:19 jenkins
```

5. 젠킨스는 사용자가 배포를 위해 생성한 내용과 사용자의 계정 정보, 사용하는 플러그인과 같은 데이터를 저장하기 위해서 PV와 PVC의 구성을 필요로 한다.
시전 구성된 jenkins-volume.yaml을 이용해 PV와 PVC를 구성하고, 구성된 PV와 PVC가 Bound 상태인지 확인한다.

```shell
kubectl apply -f ~/_Book_k8sInfra/ch5/5.3.1/jenkins-volume.yaml
kubectl get pv jenkins
kubectl get pvc jenkins
```
```shell
persistentvolume/jenkins created
persistentvolumeclaim/jenkins created
```
```shell
NAME      CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM             STORAGECLASS   REASON   AGE
jenkins   10Gi       RWX            Retain           Bound    default/jenkins                           3m48s
```
```shell
NAME      STATUS   VOLUME    CAPACITY   ACCESS MODES   STORAGECLASS   AGE
jenkins   Bound    jenkins   10Gi       RWX                           4m36s
```

6. 젠킨스를 설치해보자. 젠킨스 설치에는 필요한 인자가 많기 때문에 모든 인자를 포함해 사전에 구성한 jenkins-install.sh를 실행해 젠킨스를 설치하겠다.
실행하고 나면 젠킨스 릴리스에 대한 정보가 나타나는 것을 확인할 수 있다.
```shell
~/_Book_k8sInfra/ch5/5.3.1/jenkins-install.sh
```
```shell
NAME: jenkins
LAST DEPLOYED: Tue Dec 31 20:03:24 2024
NAMESPACE: default
STATUS: deployed
REVISION: 1
NOTES:
1. Get your 'admin' user password by running:
  printf $(kubectl get secret --namespace default jenkins -o jsonpath="{.data.jenkins-admin-password}" | base64 --decode);echo
2. Get the Jenkins URL to visit by running these commands in the same shell:
  NOTE: It may take a few minutes for the LoadBalancer IP to be available.
        You can watch the status of by running 'kubectl get svc --namespace default -w jenkins'
  export SERVICE_IP=$(kubectl get svc --namespace default jenkins --template "{{ range (index .status.loadBalancer.ingress 0) }}{{ . }}{{ end }}")
  echo http://$SERVICE_IP:80/login

3. Login with the password from step 1 and the username: admin

4. Use Jenkins Configuration as Code by specifying configScripts in your values.yaml file, see documentation: http:///configuration-as-code and examples: https://github.com/jenkinsci/configuration-as-code-plugin/tree/master/demos

For more information on running Jenkins on Kubernetes, visit:
https://cloud.google.com/solutions/jenkins-on-container-engine
For more information about Jenkins Configuration as Code, visit:
https://jenkins.io/projects/jcasc/
```
* `NAME: jenkins` 설치된 젠킨스의 릴리스 이름은 jenkins이다. 이후 헬름 관련 명령으로 젠킨스를 조회, 삭제, 변경 등을 수행할 때 이 이름을 사용한다.
* `NAMESPACE: deafult` 젠킨스가 배포된 네임스페이스는 default 이다.
* `REVISION: 1` 배포된 릴리스가 몇 번째로 배포된 것인지 알려준다. 이 젠킨스는 처음 설치된 것임을 알 수 있다. helm upgrade 명령어를 사용해 젠킨스의 버전을 업그레이드할 때마다 REVISION은 1씩 증가한다.
또한 업그레이드 작업 후 이전 버전으로 돌아가기 위해 helm rollback 명령어를 사용할 수 있다. helm rollback 명령어 사용 시 REVISION 번호를 집접 지정해 특정 리비전으로 돌아가도록 설정할 수 도 있다.
* `NOTES` 설치와 관련된 안내 사항을 몇 가지 표시하고 있습니다. 
NOTES의 1번은 젠킨스의 관리자 비밀번호를 얻어오기 위한 명령어이다.
NOTES의 2번은 젠킨스가 구동되는 파드에 접속할 수 있도록 외부의 트래픽을 쿠버네티스의 파드로 전달하게 만드는 설정이다. 외부에서 쉽게 접속하기 위해서 이 실습에서는 트래픽을 쿠버네티스의 파드로 전달하게 만드는 설정이다.
외부에서 쉽게 접속하기 위해서 이 실습에서는 트래픽을 전달하는 설정을 하지 않고 로드밸런서를 사용하겠다.
NOTES의 3번에 표시된 admin은 젠킨스 접속 시 사용할 유저 이름이다.

7. 순서대로라면 젠킨스의 코드를 살펴봐야 하지만 코드를 이해하기 위해서는 배포된 젠킨스 디플로이먼트의 정보를 함께 비교해서 봐야 한다.
따라서 우선 디플로이먼트가 정상적으로 배포됐는지 확인한다.
```shell
kubectl get deployment
```
```shell
NAME      READY   UP-TO-DATE   AVAILABLE   AGE
jenkins   1/1     1            1           7m57s
```
8. 배포된 젠킨스가 외부에서 접속할 수 있는 상태인지 서비스의 상태를 확인한다.
```shell
kubectl get service jenkins
```
```shell
NAME      TYPE           CLUSTER-IP     EXTERNAL-IP    PORT(S)        AGE
jenkins   LoadBalancer   10.98.187.64   192.168.1.11   80:32287/TCP   9m19s
```
9. 젠킨스를 처음으로 배포해봤으니 파드 상태도 자세히 살펴보자. 그런데 젠킨스가 마스터 노드에 있다. 마스터에도 파드가 배포될 수 있었는지 의문일 것이다. 
```shell
kubectl get pod -o wide
```
```shell
NAME                       READY   STATUS    RESTARTS   AGE   IP              NODE    NOMINATED NODE   READINESS GATES
jenkins-76496d9db7-d24fh   2/2     Running   0          10m   172.16.171.83   m-k8s   <none>           <none>
```

10. 의문점을 해결하기 위해서 `kubectl get node m-k8s -o yaml | nl`과 `kubectl get deployments jenkins -o yaml | nl` 명령을 통해서 상태를 비교해 보자.
```shell
kubectl get node m-k8s -o yaml | nl
```
```shell
   164    taints:
   165    - effect: NoSchedule
   166      key: node-role.kubernetes.io/master
```
```shell
kubectl get deployments jenkins -o yaml | nl
```
```shell
   562        tolerations:
   563        - effect: NoSchedule
   564          key: node-role.kubernetes.io/master
```
출력되는 많은 줄 중에 위에 표시된 테인트(taints)와 톨러레이션(tolerations)이 이런 결과를 만드는 설정이다.
테인트는 손에 잡기 싫은것, 피하고 싶은 것, 가지지 말았으면 하는 것을 의미한다. 그렇지만 상황에 따라 테인트가 설정돼 있는 곳을 만져야 하는 경우가 있다.
그러기 위해서는 톨러레이션, 즉 참아내는 인내가 필요한 것이다.

쿠버네티스의 테인트와 톨러레이션은 사전적인 의미와 반대이다. 
위에서 언급한 것처럼 매우 특별하게 취급돼야 하는 곳에는 테인트를 설정해, 쉽게 접근하지 못하는 소중한 것으로 설정한다.
그리고 톨러레이션이라는 특별한 키를 가져야만 이곳에 출입할 수 있다.
즉 현재 상태에서는 마스터 노드에 테인트가 설정돼 있어 특별한 목적으로 사용되는 노드라는 것을 명시해 두었다.
일반적으로 마스터 노드 이외에도 GPU 노드, DB 전용 노드 등의 특별한 목적으로 사용 될 때 주로 사용한다.

관리의 편의를 위해 젠킨스 컨트롤러가 여러 곳에 스케줄되지 않고 마스터 노드인 m-k8s에서만 스케줄 될 수 있도록 구성했다.
앞으로 컨트롤러를 가지는 애플리케이션 배포시에는 동일하게 마스터 노드에 컨트롤러를 구성하겠다.

테인트와 톨러레이션은 관계를 정의하는 것에 따라 배포를 상당히 유연하게 만들 수 있다.
테인트는 키와 값 그리고 키와 값에 따른 효과의 조합을 통해 테인트를 설정한 노드에 파드 배치의 기준을 설정한다.
그리고 톨러레이션은 테인트와 마찬가지로 키, 값, 효과를 가지고 있으며 이외에 연산자를 추가로 가지고 있다.

우선 테인트에 대한 요소를 살펴보면 키와 값의 조합은 테인트를 설정한 노드가 어떤 노드인지를 구분하기 위해 사용한다.
키는 필수로 설정해야 하지만 값은 생략할 수 있다. 9번 실습의 노드 명세에 나타난 key: node-role.kubernetes.io/master는 이 노드가 마스터 역할을 한다는 것을 나타내기 위해 작성된 것이다.
효과는 테인트와 톨레이션의 요소인 키 또는 값이 일치하지 않는 파드가 노드에 스케줄되려고 하는 경우 어떤 동작을 할 것인지를 나타낸다.
효과는 `NoSchedule`, `PreferNoSchedule`, `NoExecute`를 값으로 가질 수 있는데 효과에 따라 테인트를 설정한 노드는 파드를 새로 배치하는 경우와 파드가 이미 배치된 노드에 대한 동작이 다르다.

|효과              |테인트가 설정된 노드에 파드 신규 배치             |파드가 배치된 노드에 테인트 설정|
|-----------------|------------------------------------------|-------------------------|
|NoSchedule       |노드에 파드 배치를 거부                        |노드에 존재하는 파드 유지      |
|PreferNoSchedule |다른 노드에 파드 배치가 불가능 할때 노드에 파드 배치 |노드에 존재하는 파드 유지      |
|NoExecute        |노드에 파드 배치를 거부                        |파드를 노드에서 제거          |

이번에는 톨레이션의 요소들에 대해 살펴보자. 톨레이션은 테인트와 마찬가지로 키와 값, 효과를 가지고 있으며 연산자라는 특별한 요소를 추가로 가지고 있다.
톨러레이션은 테인트가 설정된 노드로 들어가기 위한 특별한 열쇠의 역할을 하며 키와 효과는 반드시 일치해야 한다.
이때 톨러레인션에만 존재하는 연산자는 기본적으로 Equal로 동작해 테인트와 톨러레이션을 비교하는 역할을 한다.
Exists의 경우에는 비교할 키와 값이 존재한다는 가정으로 테인트에 진입할 수 있는 만킁 키로 바꿔주는 역할을 한다.

톨러레이션은 톨러레이션의 키, 값, 효과를 사용해 연산자를 통해 비교한 후 조건에 맞는 테인트를 식별한다.
키와 효과중 생략된 요소가 있다면 해당 요소는 묵시적으로 모든 키 혹은 모든 효과를 의미한다.
톨러레이션의 키, 값, 효과는 테인트의 키, 값, 효과와 조건에 맞는지를 일치(Equal) 혹은 존재(Exists) 연산자를 통해서 판단한다.
연산자를 생략할 경우에는 묵시적으로 Equal을 의미한다.
조건 판단 결과 테인트와 톨러레이션의 조건이 맞다면 테인트가 설정된 노드에 톨러레이션을 가진 파드를 배치할 수 있다.
조건이 맞다고 파단하는 기준은 Equal 연산자를 사용했을 때 테인트와 톨러레이션의 키와 값 그리고 효과까지 일치하는 경우이다.
Exists 연산자를 사용했을 때는 값은 반드시 생략해야 하며 이 상태에서 키와 효과의 일치 여부를 판단하게 된다.
또한 키와 효과를 모두 생략한 상태에서 Exists 연산자만 사용한다면 테인트의 키와 효과는 모든 키와 모든 효과를 의미하므로 Exists 연산자 하나만으로도 테인트가 설정된 모든 노드에 대해 해당 톨러레이션을 설정한 파드를 배포할 수 있게 된다.

그러면 이제 헬름을 통해 젠킨스를 설치했던 스크립트인 jenkins-install.sh의 내용을 살펴보겠다.
다수의 `--set` 값들을 통해서 이 책 환경에 맞는 젠킨스를 설치할 수 있다.
```shell
     1  #!/usr/bin/env bash
     2  jkopt1="--sessionTimeout=1440"
     3  jkopt2="--sessionEviction=86400"
     4  jvopt1="-Duser.timezone=Asia/Seoul"
     5  jvopt2="-Dcasc.jenkins.config=https://raw.githubusercontent.com/sysnet4admin/_Book_k8sInfra/main/ch5/5.3.1/jenkins-config.yaml"
     6  jvopt3="-Dhudson.model.DownloadService.noSignatureCheck=true"
     7  helm install jenkins edu/jenkins \
     8  --set persistence.existingClaim=jenkins \
     9  --set master.adminPassword=admin \
    10  --set master.nodeSelector."kubernetes\.io/hostname"=m-k8s \
    11  --set master.tolerations[0].key=node-role.kubernetes.io/master \
    12  --set master.tolerations[0].effect=NoSchedule \
    13  --set master.tolerations[0].operator=Exists \
    14  --set master.runAsUser=1000 \
    15  --set master.runAsGroup=1000 \
    16  --set master.tag=2.249.3-lts-centos7 \
    17  --set master.serviceType=LoadBalancer \
    18  --set master.servicePort=80 \
    19  --set master.jenkinsOpts="$jkopt1 $jkopt2" \
    20  --set master.javaOpts="$jvopt1 $jvopt2 $jvopt3"
```
* 2~3번 라인: 기본 설정으로 30분 넘게 사용하지 않으면 세션이 종료돼 실습에 방해가 된다. 추가 설정을 통해서 세션의 유효 기간을 하루(1440분)로 변경하고 세션을 정리하는 시간 또한 하루(85440초)로 변경한다.
* 4번 라인: 기본 설정으로는 시간대가 정확히 맞지 않아 젠킨스를 통한 CI/CD 시에 명확히 작업을 구분하기 힘들다. 이를 서울(Asis/Seoul) 시간대로 변경한다.
* 5번 라인: 쿠버네티스를 위한 젠킨스 에이전트 노드 설정은 Pod Template라는 곳을 통해서 설정값을 입력한다. 그런데 가상 머신인 마스터 노드가 다시 시작하게 되면, 이에 대한 설정이 초기화 된다.
따라서 설정값을 미리 입력해 둔 야믈 파일(jenkins-config.yaml)을 깃허브 저장소에서 받아오도록 설정한다. 미리 입력해 적용되는 내용은 `5.3.4 젠킨스에이전트 설정하기`에서 알아보자.
* 7번 라인: edu 차트 저장소의 jenkins 차트를 사용해 jenkins 릴리스를 설치한다.
* 8번 라인: PVC 동적 프로비저닝을 사용할 수 없는 가상 머신 기반의 환경이기 때문에 이미 만들어 놓은 jenkins라는 이름의 PVC를 사용하도록 설정한다.
* 9번 라인: 젠키스 접속 시 사용할 관리자 비밀번호를 admin으로 설정한다. 이 값을 설정하지 않을 경우에는 설치 과정에서 젠킨스가 임의로 생성한 비밀번호를 사용한다.
* 10번 라인: 젠킨스의 컨트롤러 파드를 쿠버네티스 마스터 노드 m-k8s에 배치하도록 선택한다. nodeSelector는 nodeSelector 뒤에 따라오는 문자열과 일치하는 레이블을 가진 노드에 파드를 스케줄링 하겠다는 설정이다.
위의 설정은 kubernetes.io/hostname=m-k8s 레이블을 가지는 노드에 파드를 배치하겠다는 의미이다.
kubernetes와 .io 사이에 \가 붙어있다. kubernetes.io로 입력하게 되면 kubernetes의 하위 속성으로 io를 분리해서 인식하게 된다. kubernetes.io를 하나의 문자열로 인식시키기 위해 이스케이프 시킨 것이다.
* 11~13번 라인: 10번 줄을 통해 m-k8s 노드에 파드를 배치할 것을 명시했지만 11~13번째 줄의 옵션이 없다면 마스터 노드에 파드를 배치할 수 없다.
현재 마스터 노드에는 파드를 배치하지 않도록 NoSchedule이라는 테인트가 설정된 상태이기 때문이다. 테인트가 설정된 노드에 파드를 배치하려면 tolerations라는 옵션이 필요하다.
tolerations는 테인트에 예외를 설정하는 옵션이다. tolerations에는 예외를 설정할 테인트의 key와 effect, operator가 필요하다.
위의 코드는 key가 node-role.kubernetes.io/master이며 effect가 NoSchedule인 테인트가 존재할 때 테인트를 예외 처리해 마스터 노드에 파드를 배치할 수 있또록 설정한다.
* 14~15번 라인: 젠킨스를 구동하는 파드가 실행될 때 가질 유저 ID와 그룹 ID를 설정한다. 이때 사용되는 runAsUser는 사용자 ID를 의미하고, runAsGroup은 그룹 ID를 의미한다.
* 16번 라인: 이후 젠킨스 버전에 따른 UI 변경을 막기 위해 젠킨스 버전을 2.2249.3으로 설정한다.
* 17번 라인: 차트로 생성되는 서비스의 타입을 로드밸런서로 설정해 외부 IP를 받아온다.
* 18번 라인: 젠킨스가 HTTP상에서도 구동되도록 포트를 80으로 지정한다.
* 19번 라인: 젠킨스에 추가로 필요한 설정들을 2~3번째 줄에 변수로 선언했습니다. 이변수들을 호출해 젠킨스에 적용한다.
* 20번 라인: 젠킨스를 구동하기 위한 환경설정에 필요한 것들을 4~5번 라인에 변수로 선언했다. 이 변수들을 호출해 젠킨스 실행환경(JVM)에 적용한다.

### 5.3.2 젠킨스 살펴보기
젠킨스를 직접 접속해 살펴보기에 앞서 현재 설치된 젠킨스의 구조를 간단히 살펴보자.
젠킨스 컨트롤러는 마스터 노드에 설치했지만 젠킨스 에이전트는 필요 시에 생성되고 작업을 마치면 삭제되는 임시적인 구조를 가진다.
따라서 젠킨스 에이전트 작업 내용들은 삭제 전에 젠킨스 컨트롤러에 저장돼야 하며, 이를 위해 젠킨스 에이전트 서비스가 항상 동작하고 있다.
kubectl get service 명령으로 현재 젠킨스 에이전트 서비스를 확인할 수 있다.
```shell
kubectl get service
```
```shell
NAME            TYPE           CLUSTER-IP     EXTERNAL-IP    PORT(S)        AGE
jenkins         LoadBalancer   10.98.187.64   192.168.1.11   80:32287/TCP   136m
jenkins-agent   ClusterIP      10.101.87.69   <none>         50000/TCP      136m
kubernetes      ClusterIP      10.96.0.1      <none>         443/TCP        3d23h
```
젠킨스 컨트롤러가 단독으로 설치할 경우에는 컨트롤러가 설치된 서버에 젠킨스 자체 시스템 관리, CI/CD 설정, 빌드 등의 작업을 모두 젠킨스 컨트롤러 단일 노드에서 수행한다.
하지만 컨트롤러-에이전트 구조를 설치할 경우 컨트롤러는 젠킨스 자체의 관리 및 CI/CD와 관련된 설정만을 담당하고 실제 빌드 작업은 에이전트로 설정된 노드에서 이루어 진다.

> 젠킨스 접속하기

호스트OS의 브라우저에 로드밸런서 타입의 외부 IP인 192.168.1.11에 접속하면 젠킨스 로그인 화면이 나온다.
로그인을 하면 메인화면이 나오고 좌측에는 다양한 메뉴들이 있다.
* 새로운 Item: 젠킨스를 통해서 빌드할 작업을 아이템이라고 한다. 아이템에 대한 설명은 '5.4 젠킨스로 CI/CD 구현하기'에서 자세히 다루겠다.
* 사람: 사용자를 관리하는 메뉴이다. 현재는 최초 접속한 admin 사용자만 등록돼 있다. 사용자의 정보를 관리하는 데는 젠킨스를 구동하는 서버에서 직접 사용자를 관리하는 방법과 젠킨스가별도의 데이터베이스를 가지고 자체적으로 사용자를 관리하는 방법이 있는데,
별도의 데이터베이스가 없는 환경이기 때문에 현재는 직접 사용자를 관리하도록 구성돼 있다.
* 빌드 기록: 젠킨스 작업에 대한 성고, 실패, 진행 내역을 이곳에서 볼 수 있다.
* Jenkins 관리: 젠킨스의 시스템, 보안, 도구, 플러그인 등 각종 설정을 수행하는 곳이다.
* My Views: 젠킨스에서 각종 작업을 분류해 모아서 볼 수 있는 대시보드이다.
* Lockable Resources: 젠킨스에서는 한 번에 여러 개의 자업이 동시에 일어날 수 있다. 이때 작업이 진행중이라면 옵션에 따라 다른 작업은 대기를 해야할 수 있다. 이를 동시성 문제라고 하며 젠킨스에서는 작업이 끝날 때까지 같은 작업을 하지 못하게 하는 잠금장치를 Lockable Resource로 설정할 수 있다.
* New View: 대시보드인 View를 생성하는 작업이다.

젠킨스를 사용하려면 몇 가지 기본 설정이 필요하다. Jenkins 관리 메뉴를 눌러 젠킨스 설정화면에 대해 알아보겠다.
1. 시스템 설정: 메인 화면에 표시될 문구, 동시에 실행할 수 있는 실행기의 개수, 젠킨스를 접속할 수 있는 경로, 관리자의 정보, 시스템 전체에 사용할 수 있는 환경변수, 시스템에서 공통적으로 활용해야하는 플러그인 파일의 경로와 설정 정보등을 이곳에서 설정할 수 있다.
2. Global Tool Configuration: 빌드 과정에서 사용하는 도구(Maven, JDK, Git, Docker 등)의 경로 및 옵션을 설정할 수 있다. 플러그인 관리를 통해추가로 사용할 도구를 설정하면 이 메뉴에서 해당 도구를 설정하는 메뉴를 찾을 수 있다.
3. 플로그인 관리: 젠킨스에서 사용할 플러그인을 설치, 삭제, 업데이트할 수 있다. 젠킨스 홈 화면에서 보이는 알람은 여기서 플로그인을 업데이트해 해결할 수 있다.
4. 노드 관리: 젠킨스에서 사용하는 노드를 추가, 삭제하거나 노드의 세부 설정 및 상태 모니터링을 할 수 있는 메뉴이다. 젠킨스에서는 작업을 수행할 수 있는 각 단위를 쿠버네티스와 동일하게 노드라고 하며, 
노드에 레이블을 붙여 관리하거나 노드의 동작 방식을 설정할 수 있다.
5. Configuration as Code: 젠킨스의 설정을 내보내거나 불러올 수 있다. 이 메뉴를 통해 다른 곳에서 구성한 젠킨스 설정을 옮겨오거나 내 젠킨스의 설정을 내보내 공유할 수 있다.
6. Manage Credentials: 젠킨스에서 사용하는 플러그인에 필요한 접근 키, 비밀 키, API 토큰과 같은 접속에 필요한 인증 정보를 관리한다. 노출이 되면 곤란한 정보이기 때문에 프로젝트에 직접 입력하지 않고 필요한 경우 호출해서 사용한다.

### 5.3.3 젠킨스 컨트롤러 설정하기
젠킨스를 사용하기 위해서는 기본적으로 컨트롤러와 에이전트 구동과 관련한 여러 설정이 필요하다.
하지만 편의를 위해 컨트롤러와 에이전트에 대한 설정 중에 필요한 입력 부분을 헬름을 설치할 때 이미 포함했다.
미리 입력한 부분과 그 외에 설정은 젠킨스를 관리하기 위해 알아두어야 하므로 어디서 설정이 가능한지 알아보자.

> 젠키스 시스템 설정하기

`젠킨스 관리` > `시스템 설정` 메뉴로 이동한다. 젠킨스 시스템 설정 메뉴에서는 다음과 같은 설정값을 제공한다.

1. 시스템 메세지: 젠킨스 메인 웹 페이지에 접속했을 때 나타나는 메세지를 입력한다.
2. #of executors: 동시에 빌드를 수행할 수 있는 실행기의 개수를 설정하는 옵션이다. 이 옵션은 컨트롤러 노드에 몇 개까지의 빌드를 실행할 수 있을지 설정할 수 있다.
현재 설치된 젠킨스의 경우 에이전트 파드를 통해서 빌드 작업을 생성하므로 이 옵션을 0으로 설정하는 것이 바람직하다.
3. Label: 노드를 구분할 수 있는 레이블을 지정한다. 이렇게 설정한 레이블을 통해 Usage 옵션을 사용하면 특정 작업을 어떤 노드에서 작업할지 결정할 수 있다.
4. Usage: 젠킨스의 빌드 작업에 대해 젠킨스 노드가 어떻게 처리할지 설정한다. Use this node as much as possible(이 노드를 가장 많이 사용) 옵션은 빌드 작업을 수행할 때 별도의 조건 없이 노드에 빌드를 할 수 있는 환경이라면 현재 노드에서 빌드를 진행하도록 설정하는 것이다.
이러한 옵션을 인반적인 환경에서 빌드 작업에 적합하다. Only build jobs with label expressions matching this node(이 노드와 일치하는 레이블 표현식을 가진 작업만 빌드) 옵션은 빌드와 대상의 레이블이 같아야 빌드 할 수 있다.
주로 빌드 환경이 다른 플랫폼에서 빌드를 수행할 때 사용된다.
5. Quiet period: 빌드 작업이 시작될 때까지 잠시 대기하는 시간을 설정하는 값이다. 단위는 초 단위이며, 짧은 시간에 변경된 코드에 대해서 중복으로 작업을 수행하지 않고 가장 마지막으로 변경된 코드를 빌드하기 위해 설정한다.
6. SCM checkout retry count: 소스 코드 저장소(SCM)로부터 파일을 가져오지 못한 경우 몇번 재시도를 설정할지 설정하는 옵션이다.
7. Restrict project naming: 젠킨스를 통해 만들어지는 작업의 이름 규칙을 설정하는 옵션이다. 체크박스에 체크하면 이름 규칙을편집할 수 있는 영역이 생기며 제약 조건은 정규식 패턴으로 작성해 적용할 수 있다.
8. Jenkins URL: 설치된 젠킨스 컨트롤러의 접속 주소이다. 앞에서 헬름을 설치할 때 로드밸런서를 통해 설정된 IP인 192.168.1.11을 설정했다.
9. Resource Root URL: 빌드 결과물과 같은 내용을 외부에 공개하기 위해 사용되는 주소로 Jenkins URL과 다르다. 이 실습에서는 빌드 결과물을 외부에 공개할 수 없는 가상 환경에 구성해 두었기 때문에 설정하지 않겠다.

> 젠킨스 플러그인 관리하기

젠킨스가 실행되는 모든 기능을 플러그인으로 구현하도록 설계돼 있다. 

1. 업데이트 된 플러그인 목록: 젠킨스에 설치된 플러그인 중에 업데이트 된 플러그인이 있는 경우 최신 버전으로 올릴 수 있다.
2. 설치 가능: 설치되지 않은 플러그인을 검색해 설치할 수 있다.
3. 설치된 플러그인 목록: 현재 젠킨스에 설치돼 있는 플러그인 정보를 확인할 수 있으며, 더 이상 필요가 없어진 플러그인의 경우 이 페이지에서 제거할 수 있다.
4. 고급: 외부와 연결되는 프록시 서버 설정을 할 수 있다. 외부와 연결된 프록시 서버를 통해 내부망에서도 젠킨스를 설치하고 업데이트할 수 있다.



## 5.4 젠킨스로 CI/CD 구현하기
## 5.5 젠킨스 플러그인을 통해 구현되는 GitOps

---
# 6. 안정적인 운영을 완성하는 모니터링, 프로메테우스와 그라파나