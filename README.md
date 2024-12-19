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

```bash
kubectl create deployment dpy-nginx --image=nginx
```

2. `kubectl create`. `create`로 파드를 생성하려면 `kubectl create`에 `deployment`를 추가해서 실행해야 한다.
```bash
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

```bash
kubectl scale pod nginx-pod --replicas=3
```
`nginx-pod`는 `run`으로 생성했기에 `deployment`에 속하지 않는다. 그래서 리소스를 확인할 수 없다는 에러가 발생한다.

```bash
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

```bash
kubectl create -f ~/_Book_k8sInfra/ch3/3.2.4/echo-hname.yaml
```
오브젝트 스펙에 설정한 내용대로 디플로이먼트가 생성된다.
오브젝트 스펙 파일을 변경후 `kubectl create -f ~/_Book_k8sInfra/ch3/3.2.4/echo-hname.yaml` 실행하면 에러가 발생한다.   
`Error from server (AlreadyExists): error when creating "/root/_Book_k8sInfra/ch3/3.2.4/echo-hname.yaml": deployments.apps "echo-hname" already exists`
배포된 오브젝트의 스펙을 변경하고 싶을 때에는 어떻게 해야할까? 지우고 다시 만들어야 할까?

### 3.2.5 apply로 오브젝트 생성하고 관리하기
앞서 확인한 것처럼 파일의 변경사항을 바로 적용할 수 없다는 단점이 있다. 이런 경우를 위해 쿠버네티스는 `apply` 명령어를 제공한다.
```bash
kubectl apply -f ~/_Book_k8sInfra/ch3/3.2.4/echo-hname.yaml
```

### 3.2.6 파드의 컨테이너 자동 복구 방법
쿠버네티스는 거의 모든 부분이 자동 복구되도록 설계됐다. 특히 파드의 자동 복구 기술은 `셀프 힐링(self-healing)`이라고 하는데, 제대로 작동하지 않는 컨테이너를 다시 시작하거나 교체해 파드가 정상적으로 작동하게 한다.

1. 파드 IP 확인
```bash
kubectl get pods -o wide 
```
2. 파드 접속
```bash
kubectl exec -it nginx-pod -- /bin/bash
```
3. nginx 프로세스 ID 확인
```bash
cat /run/nginx.pid
```

4. nginx에 지속적으로 요청 보내기
```bash
i=1; while true; do sleep 1; echo $((i++)) `curl --silent 172.16.132.4 | grep title`; done
```

5. nginx kill
```bash
kill 1
```
6. self-healing 확인
```bash
kubectl get pods
```

### 3.2.7 파드의 동작 보증 기능
쿠버네티스는 파드 자체에 문제가 발생하면 파드를 자동 복구해서 파드가 항상 동작하도록 보장하는 기능도 있다.

1. 파드에 문제가 있는 상황을 만들기 위해 생성한 파드를 삭제한다.
```bash
kubectl get pods
kubectl delete pods nginx-pod
```

2. 파드의 동작을 보증하려면 어떤 조건이 필요하다. 어떤 조건인지 확인해보기 위해 다른 파드도 삭제해 서로 비교해보자.
```bash
kubectl delete pod echo-hname-7894b67f-2xb6n
```
3. 파드 조회
```bash
kubectl get pods
```
아직도 6개의 파드가 존재한다. 그런제 삭제했던 `echo-hname-7894b67f-2xb6n`는 없다. nginx-pod는 디플로이먼트에 속한 파드가 아니며 어떤 컨트롤러도 이 파드를 관리하지 않는다.
따라서 nginx-pod가 삭제되고 다시 생성되지도 않는다. `echo-hname-7894b67f-2xb6n`는 디플로이먼트에 속한 파드이다.
앞에서 replicas를 6으로 선언했다. replicas는 파드를 선언한 수대로 유지하도록 파두의 수를 항상 확인하고 부족하면 새로운 파드를 만들어 낸다.
따라서 임의로 파드를 삭제하면 replicas가 삭제된 파드를 확인하고 총 개수에 맞추기 위해 파드를 생성하게 된다.

4. 디플로이먼트에 속한 파드는 사우이 디플로이먼트를 삭제해야 파드가 삭제된다.
```bash
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
```bash
kubectl create -f ~/_Book_k8sInfra/ch3/3.2.8/echo-hname.yaml
```

2. replicas 9개로 설정
```bash
kubectl scale deployment echo-hname --replicas=9
```

3. 배포된 pod 확인
```bash
kubectl get pods -o wide
```
w1-k8s, w2-k8s, w3-k8s 각각 3개씩 파드가 생성되었다.


4. scale로 파드의 수 3개로 줄이기
```bash
kubectl scale deployment echo-hname --replicas=3
```
w1-k8s, w2-k8s, w3-k8s 각각 1개씩 파드가 생성되었다.

5. w3-k8s노드에 문제가 자주 발생해 현재 상태를 보존해야 한다고 가정하자. w3-k8s에 `cordon` 명령을 실행한다.
```bash
kubectl cordon w3-k8s
```

6. `kubectl get nodes`명령을 실행해 `cordon` 명령이 제대로 적용됐는지 확인한다.
```bash
kubectl get nodes
```

```bash
NAME     STATUS                     ROLES    AGE   VERSION
m-k8s    Ready                      master   24h   v1.18.4
w1-k8s   Ready                      <none>   24h   v1.18.4
w2-k8s   Ready                      <none>   24h   v1.18.4
w3-k8s   Ready,SchedulingDisabled   <none>   24h   v1.18.4
```
w3-k8s가 더 이상 파드가 할당되지 않는 상태로 변경됐다.
이처럼 `cordon`명령을 실행하면 해당 노드에 파드가 할당되지 않게 스케줄되지 않는 상태(SchedulingDisabled)라는 표시를 한다.

7. 이 상태에서 파드 수를 9개로 늘린다.
```bash
kubectl scale deployment echo-hname --replicas=9
```
```bash
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
```bash
kubectl scale deployment echo-hname --replicas=3
```

9. 각 노드에 할당 된 파드 수가 공평하게 1개씩인지 확인한다.
```bash
kubectl get pods -o wide
```

10. `uncordon` 명령으로 w3-k8s에 파드가 할당되지 않게 설정 했던 것을 해제 한다.
```bash
kubectl uncordon w3-k8s
```

11 `uncordon` 명령이 적용 됐는지 `kubectl get nodes` 명령으로 확인한다.
```bash
kubectl get nodes
```

```bash
NAME     STATUS   ROLES    AGE   VERSION
m-k8s    Ready    master   25h   v1.18.4
w1-k8s   Ready    <none>   24h   v1.18.4
w2-k8s   Ready    <none>   24h   v1.18.4
w3-k8s   Ready    <none>   24h   v1.18.4
```

## 3.3 쿠버네티스 연결을 담당하는 서비스
## 3.4 알아두면 쓸모 있는 쿠버네티스 오브젝트
---
# 4. 쿠버네티스를 이루는 컨테이너 도우미, 도커

---
# 5. 지속적 통합과 배포 자동화, 젠킨스

---
# 6. 안정적인 운영을 완성하는 모니터링, 프로메테우스와 그라파나
