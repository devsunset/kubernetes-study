-------------------------------------------------

			# KUBERNETES-STUDY #

-------------------------------------------------

########################################################
### Kubernetes 

https://kubernetes.io/
https://kubernetes.io/ko/

https://www.docker.com/
https://docs.docker.com/
https://hub.docker.com/

https://docmoa.github.io/02-Private%20Platform/Kubernetes/02-Config/vagrant_k8s.html
https://github.com/Great-Stone/vagrant-k8s

########################################################
### Reference

(시작하세요. 도커/쿠버네티스 book)
https://github.com/alicek106/start-docker-kubernetes

########################################################
### Kubernetes  Guide
(시작하세요. 도커/쿠버네티스 book 요약 정리) 

########################################################
## 소개 
* 쿠버네티스 - 그리스어로 조타수라는 뜻

사실상 표준으로 사용되고 있는 컨테이너 오케스트레이션 도구 
- 도커 스윔 모드 처럼 여러 대의 도커 호스트를 하나의 클러스터로 만들어 준다는 점은 같지만 세부적인 기능을 더욱 폭넓게 제공

# 장점
- 서버 자원 클러스터링 , 마이크로 서비스 구조의 컨테이너 배포, 서비스 장애 복구등 컨테이너 기반의 서비스 운영에 필요한 대부분의
  오케스트레이션 기능을 폭넓게 지원
- 구글,레드햇 등 많은 오픈소스 진영에서 기역 하고 있기 때문에 성능과 안정성 면에서 신뢰 
- 영속적 볼륨, 스케줄링, 장애 복구, 오토 스케일링, 서비스 디스커버리 및 인그레스 등 컨테이너 기반의 클라우드를 운영할 때 필요한 
  기능 과 컴포넌트를 사용자가 커스터 마이징 가능
- CNCF(Cloud Native Computing Foundation) 및 다른 클라우드 운영 도구들과 쉽게 연동 됨으로 확장성 우수 

# 단점
- 휠씬 다양한 지식이 필요 
- 쿠버네티스 자체 관리가 어려울 수도 있음 (소규모 조직에서는 오히려 오버 엔지니어링)

# 종류
- 개발 용도의 쿠버네티스 Minikube (Dockr Desktop for Mac/Windows에 내장된 서비스)
   로컬 노드를 standalone 모드로 사용하기 때문에 쿠버네티스의 기능을 완벽하게 사용해 보기에는 적합하지 않음   
   * 1개의 노드에서 쿠버네티스 설치 및 사용 
   * 간편하게 로컬에서 기본 기능 테스트 가능
   * 쿠버네티스 일부 기능 제한 
- 서비스 테스트 또는 운영 용도의 쿠버 네티스 kops , kubespray, kubeadm , EKS, GKE 등의 Managed 서비스 
  
  * 자체 서버 설치 
     모든 인프라 직접 설치 및 관리 , 원하는 대로 구성 할 수 있다는 장점 , 운영 및 유지 보수가 복잡 해 진다는 단점 
     kubespray, kubeadm 등의 도구를 이용해 쿠버네티스 설치 
  
  * 클라우드 플랫폼 설치
    서버 인스턴스만을 사용해 쿠버네티스 설치 할지 , 쿠버네티스 자체를 서비스로서 제공하는 매니지드 서비스를 사용할지 선택 해야 함
    서버 인스턴스만을 사용 : 서버, 네트워크 등 인프라에 대한 관리는 AWS, GCP 와 같은 클라우드 제공자에게 맡기되 쿠버네티스의 
    설치 및 관리를 직접 수행 ex) AWS EC2 인스턴스를 생성 후 직접 쿠버네티스 설치 kubespray, kubeadm, kops  등의 도구를 이용

        - kubespray, kubeadm 
          - 온프레미스 환경에서 쿠버네티스 설치 가능
          - 클라우드 인프라에서도 쿠버네티스 설치 가능
          * 서버 인프라 및 쿠버네티스 관리가 다소 어려울 수 있음

        - kops
          - 특정 클라우드 플랫폼에 쉽게 쿠버네티스 설치 가능
          - 서버, 네트원크 등 각종 인프라도 자동 프로비저닝

  * 쿠버네티스 자체를 클라우드 서비스로서 사용 
     AWS EKS(Elastic Kubernetes Service), GCP GKE(Google Kubernetes Engine) 등의 매니지드 서비를 이용
     설치 및 관리 까지 클라우드 제공자가 담당 , 관리 및 유지보수 비용이 절감 
     * 설치 필요 없음 가장 쉽게 사용
     * 클라우드 플랫폼에 종송적인 기능도 사용 가능 (로드 밸런서, 퍼시스턴 볼륨 등의 기능)
     * 클라우드 사용 비용 및 의존성 증가
     * 쿠버네티스 자체 학습 하기에는 적합 하지 않음

########################################################
## 설치 

# 쿠버네티스 버젼 선택 

# Docker Desktop for Mac / Windows 
  쿠버네티스 별도로 설치 하지 않아도 됨 
  설정 메뉴에서 쿠버네티스를 활성화 해주기만 하면 됨

  kubectl version --short 

# Minikube
  로컬에서 가상 머신이나 도커 엔진을 통해 쿠버네티스를 사용할 수 있는 환경 제공 

  1) virtualbox 설치
  apt-get install virtualbox
  
  2) minikube, kubectl 내려 받기 
    https://minikube.sigs.k8s.io/docs/start/

    curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
    sudo install minikube-linux-amd64 /usr/local/bin/minikube

    curl -LO "https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl"
    chmod +x ./kubectl
    sudo mv ./kubectl /usr/local/bin/kubectl

  3) minikube 가상 머신 설치 
    minikube start
    특정 버젼의 쿠버네티스를 설치하려면 --kubernetes-version옵션을 추가
    minikube start --kubernetes-version v1.23.5

        리눅스 서버에서 가상 머신 없이 도커 엔진만으로 minikube설치
        - 도커엔진이 설치된 리눅스에서는 가상 머신 생성하지 않고 Minikube를 이용해 쿠버네티스 설치 할수 있음
          minikube , kubectl 내려 받은 다음 아래 명령어 실행
          minikube start --vm-driver=none

    minikube 삭제 하려면  minikube delete 명령어 사용 

# 여러 서버로 구성된 쿠버네티스 클러스터 설치 
   kubeadm, kops, GKE
   최소한 3대이상 환경 구성 
   - 모든 서버 시간 ntp를 통해 동기화
   - MAC 주소가 각기 다른지 체크
   - 2G Memory , 2 CPU 이상의 충분한 자원
   - swapoff -a 명령어를 통해 메모리 swap을 비 활성화 쿠버네티스 설치 도구는 메모리 스왑을 허용 하지 않음

   * ntp 설정 
   sudo apt-get install -y ntp 
   sudo vi /etc/ntp.conf
      pool 3.ubuntu.pool.ntp.org iburst 하단에 아래 내용 추가 
      server 203.248.240.140 iburst 추가 
      - 동기화 서버 리스트
      time.bora.net (203.248.240.140)
      time.nuri.net (211.115.194.21)
      time2.kriss.re.kr (210.98.16.101)

   ntp 서비스 실행
    sudo systemctl start ntp (서비스 실행)
    sudo systemctl status ntp (서비스 상태 확인)
    ntpq -p (동기화 상태 확인)
    date (시스템 날짜 확인)

    sudo timedatectl set-timezone Asia/Seoul


   마스터 1대  , 워커 노드 3대 구성 

   # kubeadm으로 쿠버네티스 설치 
    쿠버네티스를 쉽게 설치 할 수 있는 관리 도구 
    온프레미스 환경 , 클라우드 인프라 환경 상관 없이 일반적인 리눅스 서버라면 모두 사용 가능 
    
    서버 예시 
    kube-master1 172.31.0.100
    kube-worker1 172.31.0.101
    kube-worker2 172.31.0.102
    kube-worker3 172.31.0.103

    1) 쿠버네티스 저장소 추가 
    모든 노드에서 아래 명령어로 저장소 추가 
    curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
    cat <<EOF > /etc/apt/source.list.d/kuberenets.list
    deb http://apt.kubernetes.io/ kubernetes-xenial main
    EOF 

    2) containerd 및 kubeadm 설치
      도커를 설치하면 도커에 포함된 containerd가 함께 설치 됨으로 도커에 포함된 containerd를 쿠버네티스와 연동해 사용 

      모든 노드에서 도커를 설치
      wget -q0- get.docker.co | sh 

      도커를 통해 설치된 containerd의 설정 파일은 기본적으로 컨테이너 런타임 인터페이스가 비활성 상태 
      containerd기본 설정값으로 덮어 씌운 뒤 재시작 
      containerd config default > /etc/containerd/config.toml
      service containerd restart

      container (runC)   container (runC)   container (runC)
                                  containerd  <------- kubernetes 
                                  Dockr Engine (docker demon)

    도커 없이 containerd만 설치해도 문제 없이 쿠버네티스를 사용할 수 있음 
    (docker 대신 crictl이라는 명령어를 통해 컨테이너를 제어)
    crictl --runtime-endpoint unix:///run/containerd/containerd.sock ps 
    쿠버네티스는 kubectl을 사용 할수 있음으로 crictl을 사용 하는 경우는 많지 않음 

    모든 노드에서 쿠버네티스에 필요한 패키지 설치
    apt-get install -y kubelet kubeadm kubectl kuberenetes-cni 
   
   3) 쿠버네티스 클러스터 초기화 
   마스터 노드로 사용할 호스트에서 다음 명령어로 클러스터 초기화 
   kubeadm init --apiserver-advertise-address 172.31.0.100 \
   --pod-network-cidr=192.168.0/16 --cri-socket /run/containerd/containerd.sock 

   --apiserver-advertise-address  : 다른 노드가 마스터에 접근할 IP 
   --pod-network-cidr : 쿠버네티스가 사용할 네트워크 대역 
   --cri-socket /run/containerd/containerd.sock  : containerd 런타임 인터페이스를 통해 컨테이너를 사용하도록 설정

  쿠버네티스 1.23까지는 도커 엔진 자체를 컨테이너 런타임 인터페이스로 사용 할 수 있었음
  도커엔진은 컨테이너 런타임 인터페이스를 구현하지 않았으므로 dockershim이라고 불리는 중간 단계를 거쳐야 했음 
  1.24 버전 부터는 도커 엔진을 사용 할수 없게 변경 될 예정 반드시 containerd, cri-o등을 사용 해야 함 

  초기화 처리 되면 출력되는 내용중 중간의 3줄을 복사해 마스터 노드에서 실행
  ...
  mkdir -p $HOME/.kube
  sudo cp -i /etc/kuberenetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config 
  ....

  kubeadm join 172.31.0.100:6443 --token ......

  맨 마지막에 출력된 kubeadm join ... 은 마스터를 제외한 노드인 워커 노드들에서 실행 
  실행시 --cri-socket /run/containerd/containerd.sock 옵션을 명령어 마지막에 추가 
 ex) 
  kubeadm join 172.31.0.100:6443 --token ...... --cri-socket /run/containerd/containerd.sock 

  4) 컨테이너 네트워크 애드온 설치 
  쿠버네티스의 컨테이너 간 통신을 위해 flannel, weaveNet등 여러 오버레이 네트워크를 사용 할 수 있지만 
  예제 에서는 calico를 기준으로 설명
  마스터 노드에서 calico 네트워크 플러그인을 설치 
  kubectl apply -f https://docs.projectcalico.org/v3.22/maifests/calico.yaml

  설치 확인 - STATUS 항목 값이 전부  Running으로 나와야 함
  kubectl get pods --namespace kube-system 
  kubectl get nodes 

kubeadm으로 설치된 쿠버네티스는 각 노드에서 아래 명령어로 삭제 처리 가능 (설치중 오류 발생하거나 테스트용 클러스터 삭제 시 유용)
kubeadm reset 

이전에 설치했던 쿠버네티스 파일들이 /etc/kubernetes 디렉토리에 남아 있는 경우 kubeadm reset명령어로 
초기화 해도 설치시 실패 할수 있음 kubeadm reset 명령어 사용한 뒤 설치시 에러가 발생하면 /etc/kubernetes 삭제 후 재 시도 

# kops로 AWS에서 쿠버네티스 설치 
kops는 클라우드 플랫폼에서 쉽게 쿠버네티스를 설치할 수 있도록 도와 주는 도구 
kubeadm은 서버 인프라를 직접 마련해야 하지만 kops는 서버 인스턴스와 네트워크 리소스 등을 클라우드에서 자동으로 생성해 설치 
kops는 AWS, GCP 등의 클라우드 플랫폼에서 설치를 지원 

1) kops 및 kubectl 실행 바이너리 내려 받기 
wget -O kops https://github.com/kubernetes/kops/releases/download/v1.23.1/kops-linux-amd64
chmod +x ./kops
sudo mv ./kops /usr/local/bin/ 

curl -LO "https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl

2) AWS 사용자 생성 , 정책 연결 및 AWS CLI 설정 
  네트워크 리소스등 자동으로 생성하기 위해 aws CLI와 AWS 접근 정보 사용 
 ( AWS 문서 참조 )

3) S3 버킷에 쿠버네티스 클러스터의 설정 정보 저장 
kops는 쿠버네티스의 설정 정보를 S3 버킷에 저장 
사용할 S3 버킷을 미리 생성해 두어야 함 

aws s3api create-bucket \
--bucket devsunset-k8s-bucket \
--create-bucket-configuration LocationConstraint=ap-northeast-2

aws s3api put-bucket-versioning \
--bucket devsunset-k8s-bucket \
--versioning-configuration Status=Enabled 

쿠버네티스의 클러스터 이름과 S3 버킷 이름을 환경 변수로서 설정
 export NAME=mycluster.k8s.local
 export KOPS_STATE_STORE=s3://devsunset-k8s-bucket

 쿠버네티스를 설치할 EC2 인스턴스에 배포될 SSH 키를 생성
 ssh-keygen -t rsa -N "" -f ./id_rsa

 클러스터 설정 파일 생성 
 kops create cluster \
 --zones ap-northeast-2a \
 --networking calico \
 --ssh-public-key ./id_rsa.pub \
 $NAME 

 4) 쿠버네티스 클러스터 옵션 변경
 마스터 워커 노드의 인스턴수 타입이나 개수 등 조정 
 kops edit -ig ==name $NAME nodes-ap-northeast-2a 

 5) 쿠버네티스 클러스터 생성
 아래 명령어 입력 하면 자동으로 쿠버네티스가 설치 됨 
 kops update cluster --yes $NAME 

 쿠버 네티스에 접근 할 수 있는 설정 파일 가져오기 
 kops export kubeconfig --admin 

 쿠버네티스 설치 진행 상황 확인 
 kops validate cluster 

 kubectl get node 

 쿠버네시트 삭제 
 kops delete cluster $NAME --yes 


# 구글 클라우드 플랫폼의 GKE로 쿠버네티스 사용하기 
클라우드에서 서비스로 제공하는 GKE , EKS 등  ()

########################################################
##  Vagrant 기반으로 Kubernetes 클러스터  로컬 환경 구성 

https://docmoa.github.io/02-Private%20Platform/Kubernetes/02-Config/vagrant_k8s.html
https://github.com/Great-Stone/vagrant-k8s

git clone https://github.com/Great-Stone/vagrant-k8s.git
cd vagrant-k8s/1.23

RUN example
~/vagrant-k8s/1.23> vagrant up

Check kubeconfig
~/vagrant-k8s/1.23> kubectl --kubeconfig=./.kube/config get nodes

마스터 노드에서 아래 내용 실행
$ mkdir -p $HOME/.kube
$ sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
$ sudo chown $(id -u):$(id -g) $HOME/.kube/config

########################################################
##  Kubernetes 시작하기

* 모든 리소스는 오브젝트 형태로 관리 됨 
  컨테이너 집합 (Pods)
  컨테이너 집합을 관리 하는 컴트롤러(Replica Set)
  Service
  Deployment
  ...

오브젝트 조회 명령어 
kubectl api-resources

The connection to the server localhost:8080 was refused - did you specify the right host or port
원인: 마스터노드에서의 kubectl 관련 config가 설정이 되지 않았기 때문 (kubectl config view  출력 내용 확인)
마스터 노드에서 아래 내용 실행
$ mkdir -p $HOME/.kube
$ sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
$ sudo chown $(id -u):$(id -g) $HOME/.kube/config

오브젝트 설명
kubectl explain 오브젝트 

* 쿠버네티스는 명령어로도 사용 할 수 있지만 YAML 파일을 더 많이 사용 

* 쿠버네티스는 여러 개의 컴포넌트로 구성 
  마스터노드 
    API  서버 (kube-apiserver)
    컨트롤러 매니저 (kube-controller-manager)
    스케줄러(kube-scheduler)
    DNS서버(coreDNS)
    프락시(kube-proxy)
    네트워크 플러그인(calico, flannel)
crictl --runtime-endpoint unix:///run/containered/containerd.sock ps 
쿠버네티스 클러스터 구성을 위해 kubelet 에이전트 모든 노드에서 실행 

* 쿠버네티스에서 반드시 containerd를 사용해야 할 필요는 없으며 OCI(Open Container Initiative) 라는 컨테이너 런타임 표준을
  구현한 컨테이너 런타임을 갖추고 있다면 사용 가능 

#  pod(Pod) : 컨테이너를 다루는 기본 단위 
   1개 이상의 컨테이너로 구성된 컨테이너 집합 
   여러 개의 컨테이너를 추상화해 하나의 애플리케이션으로 동작 하게 만드는 컨테이너 묶음 

* nginx-pod.yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-nginx-pod
spec:
  containers:
  - name: my-nginx-container
    image: nginx:latest
    ports:
    - containerPort: 80
      protocol: TCP

    생성
    kubectl apply -f nginx-pod.yaml 
    pods 확인
    kubectl get pods  
    상세 내용 확인 
    kubectl describe my-nginx-pod
    curl ip값으로 nginx 설치 확인

        클러스터 노드로 접속할 수 없는 상황이라면 
        클러스터 내부에 테스트용 pod를 생성해 임시로 사용 가능
        kubectl run -i --tty --rm debug --image=alicek106/ubuntu:curl --restart=Never bash 
        exit로 테스트용 pod에서 빠져나오면 pod는 삭제됨 

    pod 내부로 직접 접속
    kubectl exec -it my-nginx-pod bash
    로그 확인
    kubectl logs my-nginx-pod
    pod 삭제
    kubectl delete -f nginx-pod.yaml or kubectl delete pod <pod명>

  * pod vs. 도커 컨테이너 
  쿠버네티스의 pod는 docker run으로 생성된 단일 nginx 컨테이너와 비슷
  pod를 사용 하는 이유는 컨테이너 런타임의 인터페이스 제공 등 여러 가지 이유가 있지만 그 중에 하나는 여러 리눅스 namespace를 공유하는
  여러 컨테이너들을 추상화 된 집합으로 사용 하기 위함 

* nginx-pod-with-ubuntu.yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-nginx-pod
spec:
  containers:
  - name: my-nginx-container
    image: nginx:latest
    ports:
    - containerPort: 80
      protocol: TCP

  - name: ubuntu-sidecar-container
    image: alicek106/rr-test:curl
    command: ["tail"]
    args: ["-f", "/dev/null"] # 포드가 종료되지 않도록 유지합니다

  nginx pod에 2개의 컨테이너가 설치 됨
  -c 옵션을 사용 하여 pod의 특정 컨테이너에 접근 가능 
  kubectl exec -it my-nginx-pod -c ubuntu-sidecar-container bash 
  curl localhost
  우분투 서버에 nginx를 설치 하지 않았는데도 localhost로 접근이 가능 함
  - pod 내의 컨테이너들이 네트워크 namespace 등과 같은 리눅스 namespace를 공유해 사용하기 때문

* 완전환 애플리케이션으로서의 pod 
  '하나의 pod는 하나의 완전한 애플리케이션'
  사이드카 컨테이너 - pod에 정의된 부가적인 컨테이너 ex) nginx 컨테이너에 부가적으로 설정변경,로그 수집등의 프로세스가 nginx 컨테이너와 함께 수행 
  pod 냉의 다른 컨테이너와 네트워크 환경을 공유 

* pod의 네트워크 namespace는 pause라는 이름의 컨테이너로부터 네트워크를 공유 받아 사용
   pause  pod별로 생성되는 컨테이너며 각 pod에 의해 자동으로 생성
   ps aux | grep pause

#  replicaset(Replica Set) : 일정 개수의 pod를 유지 하는 컨트롤러 
   pod가 생성된 노드에 장애가 발생하더라도 pod는 다른 노드를 다시 생성하지 않으면 단지 종료된 상태로 유지 됨 
   이런 문제점을 해결하기 위해 replicaset과 같이 사용됨 
   
   replicaset
   * 정해진 수의 동일한 pod가 항상 실행되도록 관리 
   * 노드 장애 등의 이유로 pod를 사용할 수 없다면 다른 노드에서 pod를 다시 생성 

* replicaset-nginx.yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: replicaset-nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-nginx-pods-label
  template:
    metadata:
      name: my-nginx-pod
      labels:
        app: my-nginx-pods-label
    spec:
      containers:
      - name: nginx
        image: nginx:latest
        ports:
        - containerPort: 80
 
* kubectl api-resources 출력 내용 중 SHORTNAMES 항목으로 명령어를 줄여 사용 할 수 있음
ex) kubectl get pods -> kubectl get po

* replicas: 3 -> replicas: 4 로 변경 후  apply 재 실행 하면 pod가 1개 추가 생성 됨 
kubectl apply -f replicaset-nginx.yaml
replicaset.apps/replicaset-nginx configured

* kubectl delete rs replicaset-nginx 수행하면 replicaset에 의해 생성된 pod 또한 함께 삭제 됨 

* 라벨 셀렉터 (Label Selector)
  selector:
    matchLabels:
      app: my-nginx-pods-label

* 이전 버젼의 쿠버네티스에서는 replicaset이 아닌 레플리케이션 컨트롤러 라는 오브젝트를 통해 pod의 개수를 유지 

# 디플로이먼트(Deployment) : replicaset, pod의 배포를 관리 
replicaset과 pod의 정보를 정의하는 디플로이먼트 라는 이름의 오브젝트를 YAML 파일에 정의해 사용 
replicaset의 상위 오브젝트 디플로이먼트 생성하면 대응 하는 replicaset도 함께 생성

* deployment-nginx.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-nginx-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-nginx
  template:
    metadata:
      name: my-nginx-pod
      labels:
        app: my-nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.10
        ports:
        - containerPort: 80

* kubectl apply -f deployment-nginx.yaml
* kubectl get deployment
* kubectl get replicasets
* kubectl get pods
* kubectl delete deploy my-nginx-deployment

* 디플로이먼트를 사용하는 이유 
애플리케이션을 업데이트 할 때 replicaset의 변경 사항을 저장하는 리비전을 남겨 롤백을 가능 하게 지원
무중단 서비스를 위해 롤링 업데이트의 전략을 지정 가능 

* kubectl apply -f deployment-nginx.yaml --record 
디플로이먼트에서 생성된 pod의 이미지를 변경 한다고 가정
kubectl set image 사용 하여 변경
kubectl set image deployment my-nginx-deployment nginx=nginx:1.11 --record
위의 명령어는 image 항목을 nginx:1.11로 변경 후 kubectl apply -f 명령어로 적용해도 동일하게 변경 
kubectl get replicasets 명령어로 출력하면 2개의 리플리카셋이 출력 됨 
변경하여 새롭게 생성하였으나 이전 replicaset은  pod수가 0인 상태로 유지 (리비전으로서 보존)
아래 명령어로 자세히 확인 가능 
kubectl roolout history deployment my-nginx-deployment
이전 버젼으로 롤백 하려고 한다면 아래 명령어로 롤백 처리 
kubectl rollout undo deployment my-nginx-deployment --to-revision=1 
kubectl get replicates --show-labels
kubectl describe deploy my-nginx-deployment

* 리소스 정리 (모두 삭제 처리)
kubectl delete deployment,pods,rs --all

# 서비스(Service) : pod를 연결하고 외부에 노출 
YAML 파일에서 containerPort 항목을 정의했다고 해서 이 pod가 바로 외부로 노출되는 것은 아님
외부로 노출해 사용자들이 접근하거나, 다른 디플로이먼트의 pod들이 내부적으로로 접근 하려면 서비스라고 부르는 별도의 쿠버네티스 오브젝트를 생성 해야 함 

서비스 기능
* 여러 갱의 pod에 쉽게 접근할 수 있도록 고유한 도메인 이름을 부여
* 여러 개의 pod에 접근할 때, 요청을 분산하는 로드 밸런서 기능을 수행
* 클라우드 플랫폼의 로드 밸런서, 클러스터 노드의 포트 등을 통해 pod를 외부로 노출 

서비스의 종류
* ClusterIP 타입 
쿠버네티스 내부에서만 pod들에 접근할 때 사용 - 외부에서 pod에 접근할 수 없는 서비스 타입 
* Node Port 타입 
pod에 접근할 수 있는 포트를 클러스터의 모든 노드에 동일하게 개방 - 외부에서 pod에 접근할 수 있는 서비스 타입 
접근할 수 있는 포트는 랜덤으로 정해지지만 특정 포트로 접근 하도록 설정할 수도 있음 
* LoadBalancer 타입 
클라우드 플랫폼에서 제공하는 로드 밴런서를 동적으로 프로지저닝해 pod에 연결 - 외부에서 pod에 접근 할 수 있는 서비스 타입 
AWS, GCP 등과 같은 클라우드 플랫폼 환경에서만 사용 가능 


웹에 접속하면 호스트명을 출력해주는 서비스 
* deployment-hostname.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hostname-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: webserver
  template:
    metadata:
      name: my-webserver
      labels:
        app: webserver
    spec:
      containers:
      - name: my-webserver
        image: alicek106/rr-test:echo-hostname
        ports:
        - containerPort: 80

kubectl  apply -f deployment-hostname.yaml
kubectl get pods
kubectl get pods -o wide  (IP 값 출력 옵션)
클러스터 노드 중 하나에 접속해 노드에서 curl을 통해 pod로 접근 

* ClusterIP 타입의 서비스 - 쿠버네티스 내부에서만 pod에 접근하기 
* hostname-svc-clusterip.yaml
apiVersion: v1
kind: Service
metadata:
  name: hostname-svc-clusterip
spec:
  ports:
    - name: web-port
      port: 8080
      targetPort: 80
  selector:
    app: webserver
  type: ClusterIP

* spec.selector : selector 항목은 이 서비스에서 어떠한 라벨을 가지는 pod에 접근할 수 있게 만들 것인지 결정
위 예시에서는 app:webserver 라는 라벨을 가지는 pod들의 집합에 접근 할 수 있는 서비스를 생성 
deployment-hostname.yaml 로 생성된 pod는 해당 라벨이 설정되어 있으므로 서비스에 접근 가능한 대상에 추가 됨

* spec.ports.port : 생성된 서비스는 쿠버네티스 내부에서만 사용할 수 있는 공유한 IP(ClusterIP)를 할당 받음
서비스의 IP에 접근할 때 사용할 포트를 설정 

* spec.ports.targetPort : select 항목에서 정의한 라벨에 의해 접근 대상이 된 pod들이 내부적으로 사용하고 있는 포트를 입력 
pod 템플릿에 정의된 containerPort와 같은 값으로 설정 

* spec.type : 서비스가 어떤 타입인지 나타냄 (ClusterIP, NodePort, LoadBalancer)

서비스 목록 
kubectl get services # services 대신 svc 라고 사용 가능 

vagrant@master:~$ kubectl get services
NAME                     TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)    AGE
hostname-svc-clusterip   ClusterIP   10.99.231.150   <none>        8080/TCP   5m17s
kubernetes               ClusterIP   10.96.0.1       <none>        443/TCP    23h

클러스터 노드 중 아무곳에서나 접속하여 CLUSTER-IP 값으로 접속  요청 

kubectl run 명령어로 임시 pod를 생성하여 접속 요청 
kubectl run -i --tty --rm debug --image=alicek106/ubuntu:curl --restart=Never -- bash
curl 10.99.231.150 --silent | grep Hello
curl hostname-svc-clusterip:8080 --silent | grep Hello (IP 뿐만 아니라 NAME으로도 접근 - 내부 DNS을 구동하고 자동으로 이 DNS를 사용하도록 설정 됨)
(여러번 호출해 보면 서비스와 연결된 여러개의 pod에 자동으로 요청이 분산됨 - 별도의 설정을 하지 않아도 서비스는 연결된 pod에 대해 로드밸런싱을 수행)

서비스의 라벨 셀렉터와 pod의 라벨이 매칭돼 연결되면 자동으로 엔드포인트라고 부르는 오브젝트를 생성 
kubectl get endpoints # endpoints 대신 ep 사용해도 됨 

서비스 삭제 
kubectl delete svc hostname-svc-clusterip
kubectl delete -f hostname-svc-clusterip.yaml 

# NodePort 타입의 서비스 - 서비스를 이용해 pod를 외부에 노출
스윔모드에서 컨테이너를 외부로 노출하는 방식과 비슷
모든 노드의 특정 포트를 개방해 서비스에 접근 하는 방식 

* hostname-svc-nodeport.yaml
apiVersion: v1
kind: Service
metadata:
  name: hostname-svc-nodeport
spec:
  ports:
    - name: web-port
      port: 8080
      targetPort: 80
  selector:
    app: webserver
  type: NodePort

kubectl  apply -f hostname-svc-nodeport.yaml
kubectl get services

vagrant@master:~$ kubectl get services
NAME                    TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)          AGE
hostname-svc-nodeport   NodePort    10.98.198.11   <none>        8080:31143/TCP   53s
kubernetes              ClusterIP   10.96.0.1      <none>        443/TCP          25h

31143 모든 노드에서 동일하게 접근할 수 있는 포트를 의미 
kubectl get nodes -o wide
GKE에서 쿠버네티스 사용하는 경우 각 노드의 랜덤한 포트에 접근하기 위해 별도로 방화벽 설정을 추가 해야 함 
AWS에서도 Security Group에 별도의 Inbound 규칙을 추가하지 않으면 접속 안됨 
gcloud compute firewall-rules create temp-nodeport-svc --allow=tcp:31143 # 규칙추가
gcloud compute firewall-rules delete temp-nodeport-svc #규칙삭제 

각 노드에서 개방되는 포트는 기본적으로 30000 ~32768 포트 중에 랜덤으로 설정됨 
(API 서버 컴포넌트의 실행 옵션을 변경하면 포트 범위 설정 가능 --service-node-port-range=30000-35000)
YAML 파일에서 nodePort 항목을 정의 하면 원하는 포트로 선택 가능
spec:
  ports:
    - name: web-port
      port: 8080
      targetPort: 80
      nodePort: 31000

kubectl get nodes -o wide
NodePort 타입의 서비스가 ClusterIP의 기능을 포함 하고 있기 때문에 내부 IP와 DNS 이름으로 접속도 가능 

NodePort로 서비스를 외부에 제공하는 경우는 많지 않음
- NodePort에서 포트 번호를 80 또는 443으로 설정하기에 적절하지 않음
- SSL 인증서 적용 , 라우팅 등과 같은 복잡한 설정을 서비스에 적용하기 어려움 
- NodePort서비스 그 자체를 통해 서비스를 외부에 제공하기 보다는 Ingress 부르는 쿠버네티스의 오브젝트를 간접적으로 사용하는 경우가 많음 

특정 클라이언트가 같은 pod로부터만 처리되게 하려면 sessionAffinity: ClientIP로 설정 
spec:
 essionAffinity: ClientIP

# LoadBalancer 타입의 서비스 - 클라우드 플랫폼의 로드 밴런서와 연동하기 
서비스 생성과 동시에 로드 밸런서를 새롭게 생성해 pod와 연결 
클라우드 플랫폼으로부터 도메인 이름과 IP를 할당 받기 때문에 NodePort보다 더욱 쉽게 pod에 접근 
로드 밸런서를 동적으로 생성하는 기능을 제공하는 환경에서만 사용 가능 
(MetalLB, 오픈스택의 LBassB등과 같은 온프레스미 환경에서도 LoadBalancer 타입의 서비스를 사용할 수 있는 방법이 있음)

* hostname-svc-lb.yaml
apiVersion: v1
kind: Service
metadata:
  name: hostname-svc-lb
spec:
  ports:
    - name: web-port
      port: 80
      targetPort: 80
  selector:
    app: webserver
  type: LoadBalancer

쿠버네티스 1.18.0 버전을 기준으로 서비스의 YAML 파일에서 아무런 설정 하지 않으면 AWS의 클래식 로드 밸런서를 생성

NLB(네트워크 로드 밸런서)를 생성하려면 아래와 같이 정의 하면 됨
* hostname-svc-nlb.yaml
apiVersion: v1
kind: Service
metadata:
  name: hostname-svc-nlb
  annotations:
    service.beta.kubernetes.io/aws-load-balancer-type: "nlb"
spec:
  ports:
    - name: web-port
      port: 80
      targetPort: 80
  selector:
    app: webserver
  type: LoadBalancer

* 온프레스미 환경에서 LoadBalancer 타입의 서비스 사용하기 
MetalLB, 오픈스택과 같은 특수한 환경을 직접 구축 

* 트래픽의 분배를 결정하는 서비스 속성 : externalTrafficPolicy
kubectl get  svc hostname-svc-nodeport -o yaml 
externalTrafficPolicy: Cluster <- 기본 값 해당 값을 Local로 설정하면 
pod가 생성된 노드에서만 pod로 접근할 수 있음 , 로컬 노드에 위치한 pod 중 하나로 요청이 전달 

* hostname-svc-lb-local.yaml
apiVersion: v1
kind: Service
metadata:
  name: hostname-svc-lb-local
spec:
  externalTrafficPolicy: Local
  ports:
    - name: web-port
      port: 80
      targetPort: 80
  selector:
    app: webserver
  type: LoadBalancer

Cluster와 Local 둘다 장단점이 있음
불필요한 네트워크 홉으로 인한 레이턴시나 클라이언트의 IP 보존이 중요하지 않다면 Cluster 사용 
그 반대라면 Local을 사용 

* 요청을 외부로 리다이렉트하는 서비스 : ExternalName 
쿠버네티스를 외부 시스템과 연동해야 할 때는 ExternalName 타입의 서비스를 사용 
서비스가 외부 도메인을 기리키도록 설정 할 수 있음 

* external-svc.yaml (쿠버네티스를 레거시 시스템과 연동시 유용)
apiVersion: v1
kind: Service
metadata:
  name: externalname-svc
spec:
  type: ExternalName
  externalName: my.database.com

  서비스 접근시 외부 서비스로 리다이렉트 처리 해줌 

########################################################
##  Kubernetes 리소스의 관리와 설정

# Namespace : 리소스를 논리적으로 구분하는 장벽
pod, replicaset, 디플로이먼트, 서비스 등과 같은 쿠버네티스 리소스들이 묶여 있는 하나의 가상 공간 또는 그룹 
논리적으로 구분된 것일 뿐 물리적으로 구분된 거는 아님 

kubectl get namespace  or ns 
기본으로 default , kube-node-lease, kube-public, kube-system 존재

특정 namespace 에 대한 정보 확인  (--namespace 옵션 명시 하지 않으면 기본적으로 default 사용됨)
kubectl get pods --namespace default

라벨 또한 리소스 분류 하고 구분하기 위한 하나의 방법 
kubectl get pods -l app=webserver

# namespace 사용하기 
* namespace 생성 
* production-namespace.yaml
apiVersion: v1
kind: Namespace
metadata:
  name: production

kubectl apply -f production-namespace.yaml
or
kubectl create namespace production

생성확인 
kubectl get ns | grep production 

* 특정 namespace에 리소스를 생성 
yaml 파일의 metadata.namespace 항목을 설정 
*  hostname-deploy-svc-ns.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hostname-deployment-ns
  namespace: production
spec:
  replicas: 1
  selector:
    matchLabels:
      app: webserver
  template:
    metadata:
      name: my-webserver
      labels:
        app: webserver
    spec:
      containers:
      - name: my-webserver
        image: alicek106/rr-test:echo-hostname
        ports:
        - containerPort: 80
---
apiVersion: v1
kind: Service
metadata:
  name: hostname-svc-clusterip-ns
  namespace: production
spec:
  ports:
    - name: web-port
      port: 8080
      targetPort: 80
  selector:
    app: webserver
  type: ClusterIP

kubectl apply -f hostname-deploy-svc-ns.yaml
kubectl get pods,services -n production
kubectl get pods --all-namespaces # 모든 namespace의 내용 확인 

# namespace의 서비스 접근하기 
<서비스이름>.<namespace이름>.svc  처럼 서비스 이름 뒤에 namespace 이름을 붙이면 다른 namespace의 서비스에 접근 가능
curl hostname-svc-clusterip-ns.production.svc:8080 --silent | grep Hello

namespace 삭제 시 namespace에 존재하는 모든 리소스도 함께 삭제 됨
kubectl delete namespace production

# namespace에 종속되는 쿠버네티스 오브젝트와 독립적인 오브젝트 
모든 리소스가 namespace에 의해 구분되는 것은 아님
pod,서비스,replicaset,디플로이먼트는 namespace 단위로 구분

namespace에 속하는 오브젝트의 종류 확인 명령어 
kubectl api-resources --namespaced=true

namespace에 종속하지 않는 오브젝트 종류 확인 명령어
kubectl api-resources --namespaced=false

기본적으로 사용하도록 설정되는 namespace는 default 지만 쿠버네티스 설정을 담고 있는 kubeconfig라는 파일 수정으로 변경 가능
kubens 오픈 소스 스크립트를 사용해 변경 가능 
아래는 기본 namespace를 kube-system으로 변경 처리 
kubens kube-system

# Configmap , Secret : 설정 값을 pod에 전달
YAML 파일에 환경 변수를 직접 설정 (ex : LOG_LEVEL 설정) - 실행 환경 별로 YAML 파일을 다중으로 관리하게 되는 문제점 발생 
spec:
      containers:
      - name: nginx
        env:
        - name: LOG_LEVEL
          value: INFO
        image: nginx:1.10

쿠버네티스는 YAML 파일과 설정값을 분리할 수 있는 Configmap, Secret 라는 오브젝트 제공 

# Configmap
일반적인 설정값을 담아 저장할 수 있는 쿠버네티스 오브젝트 , namespace에 속하기 때문에 namespace별로 Configmap이 존재 

생성방법
yaml 파일로 생성 해도 되지만 kubectl create configmap 명령어로도 생성 가능 
kubectl create configmap <configmap 이름><설정 값>
kubectl create configmap log-level-configmap --from-literal LOG_LEVEL=debug
kubectl create configmap start-k8s --from-literal k8s=kubernetes --from-literal container=docker 

설정값 확인
kubectl get configmap or cm 
kubectl describe configmap log-level-configmap 

사용방법 
* configmap 값을 pod의 컨테이너 환경 변수로 사용 
  configmap에 저장된 키-값 데이터가 컨테이너의 환경 변수의 키-값으로 그대로 사용 
  shell 에서  echo $LOG_LEVEL  과 같은 방법으로 확인 
  시스템 환경 변수로서 설정 값을 사용 한다면 이 방법이 유용 

* configmap 값을 pod 내부의 파일로 마운트해 사용 
  LOG_LEVEL=INFO 라는 값을 가지는 configmap을  /etc/config/log_level 이라는 파일로 마운트 하면 log_level 파일에 INFO라는 값이 저장 됨
  파일이 위치할 경로는 별도로 설정 가능 nginx.conf등의 파일을 통해 설정값을 읽어 들인다면 이 방법이 유용 

* configmap의 데이터를 컨테이너의 환경 변수로 가져오기 
* all-env-from-configmap.yaml
apiVersion: v1
kind: Pod
metadata:
  name: container-env-example
spec:
  containers:
    - name: my-container
      image: busybox
      args: ['tail', '-f', '/dev/null']
      envFrom:
      - configMapRef:
          name: log-level-configmap
      - configMapRef:
          name: start-k8s

kubectl apply -f all-env-from-configmap.yaml
kubectl exec container-env-example env

* selective-env-from-configmap.yaml
apiVersion: v1
kind: Pod
metadata:
  name: container-selective-env-example
spec:
  containers:
    - name: my-container
      image: busybox
      args: ['tail', '-f', '/dev/null']
      env:
      - name: ENV_KEYNAME_1     # (1.1) 컨테이너에 새롭게 등록될 환경 변수 이름
        valueFrom:
          configMapKeyRef:
            name: log-level-configmap
            key: LOG_LEVEL
      - name: ENV_KEYNAME_2  # (1.2) 컨테이너에 새롭게 등록될 환경 변수 이름
        valueFrom:
          configMapKeyRef:
            name: start-k8s      # (2) 참조할 컨피그맵의 이름
            key: k8s             # (3) 가져올 데이터 값의 키
                                 # 최종 결과 -> ENV_KEYNAME_2=$(k8s 키에 해당하는 값)
                                 #              ENV_KEYNAME_2=kubernetes

kubectl apply -f selective-env-from-configmap.yaml
kubectl exec container-selective-env-example env | grep ENV

envFrom : configmap에 존재하는 모든 키-값 쌍을 가져옴
valueFrom,configMapKeyRf : configmap에 존재하는 키-값 쌍 중에서 원한는 데이타만 선택적으로 가져옴 

* configmap 의 내용을 파일로 pod 내부에서 마운트하기 

* volume-mount-configmap.yaml
apiVersion: v1
kind: Pod
metadata:
  name: configmap-volume-pod
spec:
  containers:
    - name: my-container
      image: busybox
      args: [ "tail", "-f", "/dev/null" ]
      volumeMounts:
      - name: configmap-volume          # volumes에서 정의한 컨피그맵 볼륨 이름
        mountPath: /etc/config             # 컨피그맵의 데이터가 위치할 경로

  volumes:
    - name: configmap-volume            # 컨피그맵 볼륨 이름
      configMap:
        name: start-k8s

* spec.volumes: YAML 파일에서 사용할 볼륨을 정의 
* spec.containers.volumeMounts: volumes 항목에서 정의된 볼륨을 컨테이너 내부의 어떤 디렉토리에 마운트 할 것인지 정의 

kubectl apply -f volume-mount-configmap.yaml
kubectl exec configmap-volume-pod ls /etc/config 
kubectl exec configmap-volume-pod cat /etc/config/k8s

* selective-volume-configmap.yaml
apiVersion: v1
kind: Pod
metadata:
  name: selective-cm-volume-pod
spec:
  containers:
    - name: my-container
      image: busybox
      args: [ "tail", "-f", "/dev/null" ]
      volumeMounts:
      - name: configmap-volume
        mountPath: /etc/config       
  volumes:
    - name: configmap-volume
      configMap:
        name: start-k8s
        items:                       # 컨피그맵에서 가여올 키-값의 목록을 나열
        - key: k8s                    # k8s라는 키에 대응하는 값을 가져옴
          path: k8s_fullname         # 최종 파일 이름은 k8s_fullname

* items: 컨피그맵에서 가져올 키-값의 목록을 의미 
* path : 최종적으로 디렉토리에 위치할 파이을 이름을 입력 하는 항목 

kubectl apply -f selective-volume-configmap.yaml
kubectl exec selective-cm-volume-pod ls /etc/config
kubectl exec selective-cm-volume-pod cat /etc/config/k8s_fullname

# 파일로부터 configmap 생성하기 
단순 문자열 값을 이용해 configmap 생성할때는 kubectl create configmap --from-literal 명령어 사용 
파일로부터 생성하려면 --from-file 옵션을 사용 , 옵션을 여러번 사용해 여러 개의 파일을 configmap에 저장 할 수 도 있음 
kubectl create configmap <컨피그맵 이름> --from-file <파일 이름>
echo Hello, world >> index.html
kubectl create configmap index-file --from-file index.html 
--from-file 옵션에서 별도의 키를 지정하지 않으면 파일 이름이 키로 파일의 내용이 값으로 저장 됨
kubectl describe configmap index-file 
키의 이름을 직접 지정 하는 방식 
kubectl create configmap index-file-customkey --from-file myindex=index.html 
--from-env-file 옵션으로 여러 개의 키-값 형태의 내용으로 구성된 설정 파일을 한꺼번에 컨피그맵으로 가져올 수도 있음 
cat multiple-keyvalue.env
mykey1=myvalue1 
mykey2=myvalue2
mykey3=myvalue3 

kubectl create configmap from-envfile --from-env-file multiple-keyvalue.env
kubectl get cm from-envfile -o yaml 

# YAML 파일로 컨피그맵 정의하기 
kubectl create 명령어에서 --dry-run   -o yaml  옵션을 사용하면 컨피그앱을 생성하지 않은 채로 YAML 파일의 내용을 출력 가능 
kubectl create configmap my-configmap --from-literal mykey=myvalue --dry-run -o yaml 
출력된 내용을 yaml 파일로 배포에 사용 
kubectl create configmap my-configmap --from-literal mykey=myvalue --dry-run -o yaml  > my-configmap.yaml
kubectl apply -f my-configmap.yaml 
--dry-run 옵션을 추가하면 실행 가능 여부를 확인 실제로 쿠버네티스에 리소스를 생성 하지 않음 

# Secret
SSH키, 비밀번호 등과 같이 민감한 정보를 저장하기 위한 용도로 사용  네임스페이스에 종속되는 오브젝트 
configmap과 사용법 비슷 
kubectl create secret generic my-password --from-literal password=1q2w3e4r
configmap 처럼 --from-literal, --from-file, --from-env-file  옵션 사용 가능 
kubectl get secrets
kubectl get secret my-password -o yaml  
값이 base64로 인코딩되어 있음 아래 명령어로 원래 값 확인 가능 
echo MXEydzNlNHI=  |  base64 -d
위 처럼 생성한 secret는 configmap과 비슷 하게 사용 가능 
YAML 파일에 base64로 인코딩한 값을 입력했더라도 secret pod의 환경 변수나 볼륨 파일로서 가져오면 base64 디코딩된 원래의 값을 사용하게 됨 

# 이미지 레지스트리 접근을 위한 docker-registry 타입의 시크릿 사용하기 
kubectl get secrets
출력되는 항목 중 TYPE 항목이 시크릿의 종류에 해당
Opaque : 별도로 시크릿의 종류를 명시하지 않으면 자동으로 설정되는 타입 생성시 generic 로 명시했던 것이 Opaque 타입에 해당 하는 종류

쿠버네티스에서 이미지 받아올때 인증 정보 처리 
1. docker login 명령어로 로그인에 성공했을 때 도커 엔진이 자동으로 생성하는 ~/.docker/config.json파일 사용 
kubectl create secret generic registry-auth --from-file=.dockerconfigjson=/root/.docker/config.json --type=kubernetes.io/dockerconfigjson 
2. 시크릿을 생성하는 명령어에서 직접 로그인 인증 정보를 명시 
kubectl create secret docker-registry registry-auth-by-cmd --docker-username=username --docker-password=password
--docker-server 옵션을 사용하지 않으면 기본적으로 도커허브를 사용 
사설 레지스트리를 사용하려면  --docker-server 옵션에 서버의 주소 또는 도메인 이름을 설정
kubectl create secret docker-registry registry-auth-by-cmd --docker-username=username --docker-password=password --docker-server=private_registry_address_or_domain 

도커 허브의 Private Repository 에 저장된 이미지를 통해 파드를 생성하려면 YAML 파일에서 imagePullSecret항목을 정의 
apiVersion: apps/v1
kind: Deployment
metadata:
  name: deployment-from-prvate-repo
spec:
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      name: mypod
      labels:
        app: myapp
    spec:
      containers:
      - name: test-container
        image: alicek106.ipdisk.co.kr/busybox:latest
        args: ['tail', '-f', '/dev/null']
      imagePullSecrets:
      - name: registry-auth-registry

# TLS 키를  저장할 수 있는 tls 타입의 시크릿 
시크릿은 TLS 연결에 사용되는 공개키, 비밀키 등을 쿠버네티스에 자체적으로 저장할 수 있도록 tls 타입을 지원 
테스트용 키 페어 생성
openssl req -new -newkey rsa:4096 -days 365 -nodes -x509 -subj "/CN=example.com" -keyout cert.key -out cert.crt 
kubectl create secret tls  my-tls-secret --cert cert.crt --key cert.key 
kubectl get secrets my-tls-secret 
kubectl get secrets my-tls-secret -o yaml 

# 쉡게 컨피그맵과 시크릿 리소스 배포하기 
시크릿이나 컨피그맵을 배포하기 위해 YAML 파일을 작성할 때 , 데이터를 YAML 파일로부터 분리 할 수 있는 kustomize 기능 제공 
kustomize는 kubectl 1.14 버전 부터 지원 
자주 사용되는 YAML 파일의 속성을 별도로 정의해 재사용 하거나 여러 YAML 파일을 하나로 묶는 등 다양한 용도록 사용할 수 있는 기능 

* kustomization.yaml 
secretGenerator:                # 시크릿을 생성하기 위한 지시문
- name: kustomize-secret
  type: kubernetes.io/tls       # tls 타입의 시크릿을 생성
  files:
  - tls.crt=cert.crt            # tls.crt 라는 키에 cert.crt 파일의 내용을 저장
  - tls.key=cert.key            # tls.key 라는 키에 cert.key 파일의 내용을 저장

시크릿을 생성하기 전에 kustomize로 부터 생성될 시크릿 정보를 미리 확인 하려면 kubectl kustomize 명령어 사용 
,/ 경로에 kustomization.yaml 파일 위치 
kubectl kustomize ./ 
생성 
kubectl apply -k ./ 
삭제
kubectl delete -k ./ 

컨피그맵을 kustomize로부터 생성하고 싶다면 kustomization.yaml  파일에서 secretGenerator 대신 configmapGenerator를 사용 하면 됨 
시크릿과 달리 type 항목은 정의 하지 않음 
* kustomization.yaml 
configmapGenerator:                # 컨피그맵을 생성하기 위한 지시문
- name: kustomize-configmap
  files:
  - tls.crt=cert.crt            # tls.crt 라는 키에 cert.crt 파일의 내용을 저장
  - tls.key=cert.key            # tls.key 라는 키에 cert.key 파일의 내용을 저장

  kustomization으로 생성된 컴피그맵이나 시크릿의 이름 뒤에는 저장된 데이타로부터 추출된 해시값이 자동으로 추가 
  kubectl 명령어 사용할 때도 --append-hash 옵션을 이용해 리소스의 이름뒤에 해시값을 추가할 수 있음
  kubectl create secret tls kustomize-secret --cert cert.crt --key cert.key --append-hash 
  --append-hash를 사용하면 데이터를 시크릿이나 컨피그앱의 이름에 명확히 나타낼수 있다는 장점 

#  컨피그맵이나 시크릿을 업데이트해 애플리케이션의 설정값 변경하기 
3가지 방법 
kubectl edit  명령어로 수정  
YAML 파잉을 변경한 뒤 다시 kubectl apply 명령어 실행 
kubectl patch 명령어 사용 

리소스 정리 
kubectl delete deployment --all
kubectl delete pod --all
kubectl delete configmap --all
kubectl delete secret --all

########################################################
##  Ingress (설정 내용 추가 Study 필요) 

외부 요청을 어떻게 처리할 것인지 네트워크 7계층 레벨에서 정의하는 쿠버네티스 오브젝트 
* 외부 요청의 라우팅 : /apple , /apple/red 등과 같이 특정 경로로 들어온 요청을 어떠한 서비스에 전달할지 정의 하는 라우팅 규칙 
* 가상 호스트 기반의 요청 처리 : 같은 IP에 대해 다른 도메인 이름으로 요청이 도착했을 때 어떻게 처리할 것인지 정의 
* SSL/TLS 보안 연결 처리 : 여러개의 서비스로 요청을 라우팅할 때 보안 연결을 위한 인증서를 쉽게 적용 

* 인그레스를 사용하는 이유
인그레스 오브젝트를 사용하면 URL 엔드포인트를 단 하나만 생성함
라우팅 정의나 보안 연결 등과 같은 세부 설정은 서비스와 디플로이먼트가 아닌 인그레스에 의해 수행 됨으로 설정이 간소화 

* 인그레스의 구조 
kubectel get ingress or ing
* ingress-example-k8s-latest.yaml 
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: ingress-example
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
    kubernetes.io/ingress.class: "nginx"
spec:
  rules:
  - host: alicek106.example.com                   # [1]
    http:
      paths:
      - path: /echo-hostname                     # [2]
        pathType: Prefix
        backend:
          service:
            name: hostname-service               # [3]
            port:
              number: 80

host : 해당 도메인 이름으로 접근하는 요청에 대해서 처리 규칙을 적용 
path : 해당 경로에 들어온 요청을 어느 서비스로 전달할 것인지 정의  , 여러 개으이 path를 정의해 경로를 처리할 수 있음 
name, port : path로 들어온 요청이 전달될 서비스와 포트 

kubectl apply -f ingress-example-k8s-latest.yaml
kubectl get ingress
인그레스는 단지 요청을 처리하는 규칙을 정의하는 선언적인 오브젝트일 뿐, 외부 요청ㅇㄹ 받아들일 수 있는 실제 서버가 아님 
인그레스 컨트롤러라고 하는 특수한 서버에 적용해야만 그 규칙을 사용 할 수 있음 
실제로 외부 요청을 받아 들이는 것은 인그레스 컨트롤러 서버 이며 이 서버가 인그레스 규칙을 로드해 사용 
인그레스는 반드시 인그레스 컨트롤러라는 서버와 함께 사용 

* 인그레스 컨트롤러 
Nginx 웹 서버 인그레스 컨트롤러 
Kong API 게이트웨이 
GKE 등의 클라우드 플랫폼에서 제공되는 인그레스 컨트롤러 

* Nginx 웹 서버 인그레스 컨트롤러 와 관련된 리소스를 한번에 설치 (쿠버네티스에서 공식적으로 개발)
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.2.0/deploy/static/provider/cloud/deploy.yaml
kubectl get pods,deployment -n ingress-nginx
kubectl get svc -n ingress-nginx

온프레미스에서의 운영 단계를 계획 하고 있다면 MetalLB나 오픈스택의 로드 밸런서를 사용 
클라우드 아닌 환경에서 인그레스를 테스트하고 싶다면 LoadBalancer 대신 NodePort 타입의 서비스를 생성해 사용 
각 노드의 랜덤한 포트로 Nginx 인그레스 컨트롤러에 접근 
* ingress-nginx-svc-nodeport.yaml 
apiVersion: v1
kind: Service
metadata:
  labels:
    app.kubernetes.io/component: controller
    app.kubernetes.io/instance: ingress-nginx
    app.kubernetes.io/managed-by: Helm
    app.kubernetes.io/name: ingress-nginx
  name: ingress-nginx-controller-nodeport
  namespace: ingress-nginx
spec:
  ports:
  - name: http
    nodePort: 31000
    port: 80
    protocol: TCP
    targetPort: http
  - name: https
    nodePort: 32000
    port: 443
    protocol: TCP
    targetPort: https
  selector:
    app.kubernetes.io/component: controller
    app.kubernetes.io/instance: ingress-nginx
    app.kubernetes.io/name: ingress-nginx
  type: NodePort

* hostname-deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hostname-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: webserver
  template:
    metadata:
      name: my-webserver
      labels:
        app: webserver
    spec:
      containers:
      - name: my-webserver
        image: alicek106/ingress-annotation-test:0.0
        ports:
        - containerPort: 5000
          name: flask-port

  kubectl apply -f hostname-deployment.yaml 

* hostname-service.yaml 
apiVersion: v1
kind: Service
metadata:
  name: hostname-service
spec:
  ports:
    - name: web-port
      port: 80
      targetPort: flask-port
  selector:
    app: webserver
  type: ClusterIP

인그레스 컨트롤러에 의해 요청이 최종적으로 도착할 디플로이먼트의 서비스는 어떤 타입이든지 상관 없음
외부에 서비스를 노출할 필요가 없다면 ClusterIP 타입을 사용 하는 것이 좋음 
  kubectl apply -f hostname-service.yaml 

  kubectl get pods,services

AWS 
curl a20...2.elb.amazonaws.com/echo-hostname 

Nginx에 접근하기 위한 LoadBalancer타입의 서비스를 생성했을 때 GKE에서 부하 분산기의 IP만 할당 받았다면 
curl 명령어의 --resolve옵션을 통해 임시로 도메인명을 설정 할 수 있음
curl --resolve alicek106.example.com:80:<부하 분산 IP> alicek106.example.com/echo-hostname
 
온프레스미 환경이나 GKE와 같이 IP만 할당받아 상요하고 있다면 /etc/hosts 파일에 IP와 도메인을 설정해 임시로 동작여부 테스트 

NodePort  타입으로 서비스를 생성했다면 다음과 같은 명령어로 테스트 
curl --resolve alicek106.example.com:31000:<노드 중 하나의 IP를 입력> alicek106.example.com:31000/echo-hostname

AWS에서 임의의 DNS를 LoadBalancer타입의 서비스에 할당받았다면 이미 생성된 인그레스 리소스의 정보에서 host 항목을 직접 로드 밸런서의 DNS로 수정
kubectl edit ingress ingress-example
spec:
  rules:
   - host: a206556....ap.-northeast-2.elb.amazonwas.com

# 인그레스 컨트롤러의 동작 원리 
1.공식 깃허브에서 제공되는 YAML 파일로 Nginx 인그레스 컨트롤러 생성
2.Nginx 인그레스 컨트롤러를 외부로 노출하기 위한 서비스를 생성
3.요청 처리 규칙을 정의하는 인그레스 오브젝트를 생성
4.Nginx 인그레스 컨트롤러로 들어온 요청은 인그레스 규칙에 따라 적절한 서비스로 전달 

쿠버네티스  API에는 특정 오브젝트의 상태가 변화하는 것을 확인할 수 잇는 Watch API 존재 
Watch는 리소스에 생성,삭제,수정 등의 이벤트가 발생했을때 이를 알려주는 기능 
kubectl get 명령어에서도 -w 옵션을 붙여 사용 가능 
kubectl get pods -w 

요청이 실제로 hostname-service 라는 서비스로 전달 되는 것은 아님
Nginx 인그레스 컨트롤러는 서비스에 의해 생성된 엔드포인트로 요청을 직접 전달 ( 이러한 동작을 쿠버네티스에서는 bypass라 함)

# 인그레스의 세부 기능 : annotation을 이용한 설정 
인그레스는 YAML 파일의 주석 항목을 정의함으로써 다양한 옵션을 사용할 수 있음 
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: ingress-example
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
    kubernetes.io/ingress.class: "nginx"

nginx.ingress.kubernetes.io/rewrite-target  Nginx 인그레스 컨트롤러에서만 사용 할 수 있는 기능 - 인그레스에 정의된 경로로 들어오는 요청을 rewrite-target에 설정된 경로로 전달 
kubernetes.io/ingress.class는 해당 인그레스 규칙을 어떤 인그레스 컨트롤러에 적용할 것인지를 의미 

# Nginx 인그레스 컨트롤러에 SSL/TLS 보안 연결 적용 
인그레스 컨틀로러 지점에서 인증서를 적용해 두면 요청이 전달되는 애플리케이션에 대해 모두 인증서 처리를  할 수 있음 

보안키 생성
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout tls.key -out tls.crt -subj "/CN=alicek106.example.com/0=alicek106"
/CN에는 Nginx 인그레스 컨트롤러에 접근하기 위한 Public DNS 이름을 입력 

시크릿 생성
kubectl create secret tls tls-secret --key tls.key --cert tls.crt 

* ingress-tls-k8s-latest.yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: ingress-example
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
    kubernetes.io/ingress.class: "nginx"
spec:
  tls:
  - hosts:
    - alicek106.example.com            # 여러분의 도메인 이름을 입력해야 합니다.
    secretName: tls-secret
  rules:
  - host: alicek106.example.com          # 여러분의 도메인 이름을 입력해야 합니다.
    http:
      paths:
      - path: /echo-hostname
        pathType: Prefix
        backend:
          service:
            name: hostname-service
            port:
              number: 80

#  여러 개의 인그레스 컨트롤러 사용하기 
kubernetes.io/ingress.class annotation에 Nginx, Kong, GKE등 여러 개의 인그레스 컨트롤러 중 어는 것을 사용할 것인지 명시 

아래 처럼 변경해서 설정도 가능
1. wget https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.2.0/deploy/static/provider/cloud/deploy.yaml
2. vi deploy.xml 
--ingress-class=alicek106-nginx  로 수정
3.kubernetes.io/ingress.class: "alicek106-nginx"

########################################################
##  퍼시스턴트 볼륨(PV) 과 퍼시트턴트 볼륨 클레임 (PVC)

파드의 데이타를 영속적으로 저장하기 위한 방법 
호스트에 위치한 디렉토리를 각 파드와 공유함으로써 데이타를 보존 - pod 장애시 대응 힘듬
퍼시스턴트 볼륨 - 워커 노드들이 네트워크상에서 스토리지를 마운트해 영속적으로 데이타를 저장할 수 있는 볼륨
NFS, AWS EBS(Elastic Block Store), Ceph , ClusterFS 
쿠버네티스는 퍼시스턴트 볼륨을 사용하기 위한 기능을 자체적으로 제공 

# 로컬 볼륨 : hostPath, emptyDir 
hostPath : 호스트와 볼륨을 공유 하기 위해 사용
emptyDir : 파드의 컨테이너 간에 볼륨을 공유 하기 위해 사용 

# 워커 노드의 로컬 디렉토리를 볼륨으로 사용 : hostPath 
* hostpath-pod.yaml 
apiVersion: v1
kind: Pod
metadata:
  name: hostpath-pod
spec:
  containers:
    - name: my-container
      image: busybox
      args: [ "tail", "-f", "/dev/null" ]
      volumeMounts:
      - name: my-hostpath-volume
        mountPath: /etc/data
  volumes:
    - name: my-hostpath-volume
      hostPath:
        path: /tmp

kubectl apply -f hostpath-pod.yaml
kubectl exec -it hostpath-pod touch /etc/data/mydata
파드가  생성된 워커 노드에 접속
ls /tmp/mydata

디플로이먼트 파드에 장애가 생겨 다른 노드로 파드가 옮겨갔을 경우 , 이전 노드에 저장된 데이타를 사용할 수 없음 
스케줄링을 이용해 특정 노드에만 파드를 배치하는 방법도 있지만 호스트 서버에 장애가 생기면 데이터를 읽게 되는 단점 
hostPath 볼륨은 모든 노드에 배치해야 하는 특수한 파드의 경우에 유용 

# 파드 내의 컨테이너 간 임시 데이터 공유 : emptyDir 
파드의 데이터를 영속적으로 보존하기 위해 외부 볼륨을 사용하는 것이 아닌 파드가 실행되는 도중에만 필요한 휘발성 데이터를 
각 컨테이너가 함께 사용할 수 있도록 임시 저장 공간을 생성 
비어있는 상태로 생성되며 파드가 삭제되면 emptyDir에 저장돼 있던 데이터도 함께 삭제됨 

* emptydir-pod.yaml 
apiVersion: v1
kind: Pod
metadata:
  name: emptydir-pod
spec:
  containers:
  - name: content-creator
    image: alicek106/alpine-wget:latest
    args: ["tail", "-f", "/dev/null"]
    volumeMounts:
    - name: my-emptydir-volume
      mountPath: /data                      # 1. 이 컨테이너가 /data 에 파일을 생성하면
  - name: apache-webserver
    image: httpd:2
    volumeMounts:
    - name: my-emptydir-volume
      mountPath: /usr/local/apache2/htdocs/  # 2. 아파치 웹 서버에서 접근 가능합니다.
  volumes:
    - name: my-emptydir-volume
      emptyDir: {}                             # 포드 내에서 파일을 공유하는 emptyDir

emptyDir은 한 컨테이너가 파일을 관리하고 한 컨테이너가 그 파일을 사용하는 경우에 유용 
kubectl apply -f emptydir-pod.yaml
kubectl exec -it emptydir-pod -c content-creator sh 
echo Hello, Kubernetes! >> /data/test.html 
kubectl describe pod emptydir-pod | grep IP
kubectl run -i --tty --rm debug --image=alicek106/ubuntu:curl --restart=Never -- curl IP/test.html 

# 네트워크 볼륨
플러그인 설치하지 않아도 다양한 종류의 네트워크 볼륨을 파드에 마운트 가능 
온프레스미 환경에서 구축할 수 있는 NFS, iSCSI, ClusterFS, Ceph
AWS EBS(Elastic Block Store)
GCP gcePersistentDisk

# NFS를 네트워크 볼륨으로 사용하기 
NFS(Network File System) 네트워크 스토리지 
여러 개의 스토리지를 클러스터링 하는 다른 솔루션에 비해 안정성이 떨어지나 하나의 서버만으로 간편하게 사용 , 로컬 스토리지 처럼 사용할 수 있다는 장점
NFS Server : 영속적인 데이터가 실제로 저장되는 네트워크 스토리지 서버 
NFS Client  : NFS 서버에 마운트해 스토리지에 파일을 읽고 쓰는 역활 

아래 NFS 서버는 네트워크 볼륨 기능을 테스트하기 위한 용도 실 운영 시는 NFS  서버 도입 필요 

* nfs-deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nfs-server
spec:
  selector:
    matchLabels:
      role: nfs-server
  template:
    metadata:
      labels:
        role: nfs-server
    spec:
      containers:
      - name: nfs-server
        image: gcr.io/google_containers/volume-nfs:0.8
        ports:
          - name: nfs
            containerPort: 2049
          - name: mountd
            containerPort: 20048
          - name: rpcbind
            containerPort: 111
        securityContext:
          privileged: true

* nfs-service.yaml 
apiVersion: v1
kind: Service
metadata:
  name: nfs-service
spec:
  ports:
  - name: nfs
    port: 2049
  - name: mountd
    port: 20048
  - name: rpcbind
    port: 111
  selector:
    role: nfs-server

kubectl apply -f nfs-deployment.yaml
kubectl apply -f nfs-service.yaml 

* nfs-pod.yaml
apiVersion: v1
kind: Pod
metadata:
  name: nfs-pod
spec:
  containers:
    - name: nfs-mount-container
      image: busybox
      args: [ "tail", "-f", "/dev/null" ]
      volumeMounts:
      - name: nfs-volume
        mountPath: /mnt           # 포드 컨테이너 내부의 /mnt 디렉터리에 마운트합니다.
  volumes:
  - name : nfs-volume
    nfs:                            # NFS 서버의 볼륨을 포드의 컨테이너에 마운트합니다.
      path: /
      server: {NFS_SERVICE_IP}

server 항목이 nfs-service 의 DNS 이름이 아닌 {NFS_SERVICE_IP}로 설정
NFS 볼륨의 마운트는 컨테이너 내부가 아닌 워커 노드에서 발생하므로 서비스의 DNS 이름으로 NFS 서버에 접근 할수 없음
노드에서는 파드의 IP로 통신은 할 수 있지만 쿠버네티스의 DNS를 사용하도록 설정돼 있지는 않기 때문 
예외적으로 NFS 서비스의 ClusterIP를 직접 얻은 뒤 YAML 파일에 사용 하여 파드 생성

*  NFS 서버에 접근하기 위한 서비스의 ClusterIP 
export NFS_CLUSTER_IP=$(kubectl get svc/nfs-service -o jsonpath='{.spec.clusterIP}')
* nfs-pod의 server 항목을 NFS_CLUSTER_IP로 교체해 생성
cat nfs-pod.yaml | sed "s/{NFS_SERVICE_IP}/$NFS_CLUSTER_IP/g" | kubectl apply -f - 

kubectl get pod nfs-pod
kubectl exec -it nfs-pod sh 
# df -h 
NFS 서버에 마운트 하려면 워커 노드에서 별도의 NFS 패키지를 설치 해야 할 수도 있음
apt-get install nfs-common 

# PV,PVC를 이용한 볼륨 관리 
퍼시스턴트 볼륨과 퍼시스턴트 볼륨 클레임을 사용 하는 이유
YAML 파일에 NFS 처럼 볼륨을 명시하는 경우 볼륨과 애플리케이션의 정의가 서로 밀접하게 연관돼 있어 서로 분리할 수 없는 상황 초래
PV,PVC는 볼륨이 세부적인 사항을 몰라도 볼륨을 사용할 수 있도록 추상화 해주는 역활을 담당 
파드를 생성하는 YAML 입장에서는 네트워크의 볼륨이 NFS인지 EBS인지 상관없이 볼륨을 사용할 수 있도록 해주는게 핵심 
- PV로 네트워크 스토리지 관련 내용 설정 
- PVC로 YAML 파일에 명시 
PV의 속성과 PVC의 요구 사항이 일치하면 두개의 리소스를 bind 
사용자는 디플로이먼트의 YAML 파일에 볼륨의 상세한 스펙을 정의하지 않아도 됨 

# 퍼시스턴트 볼륨과 퍼시스턴트 볼륨 클레임 사용하기 
퍼시스턴트 볼륨 : persistentvolume  or  pv
퍼시스턴트 볼륨 클레임 : persistentvolumeclaim or pvc 
kubectl get persistentvolume,persistentvolumeclaim
kubectl get pv,pvc

# AWS에서 EBS를 퍼시스턴트 볼륨으로 사용하기 (kops로 쿠버네티스 설치했다면 퍼시스턴트 볼륨을 EBS와 연동해 사용 할 수 있음)
1. AWS에서 EBS 생성 
2. 퍼시스턴트 볼륨 생성
* ebs-pv.yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: ebs-pv
spec:
  capacity:
    storage: 5Gi         # 이 볼륨의 크기는 5G입니다.
  accessModes:
    - ReadWriteOnce    # 하나의 포드 (또는 인스턴스) 에 의해서만 마운트 될 수 있습니다.
  awsElasticBlockStore:
    fsType: ext4
    volumeID: <VOLUME_ID>
3. 퍼시스턴트 볼륨 클레임과 파드 생성
* ebs-pod-pvc.yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: my-ebs-pvc                  # 1. my-ebs-pvc라는 이름의 pvc 를 생성합니다.
spec:
  storageClassName: ""
  accessModes:
    - ReadWriteOnce       # 2.1 속성이 ReadWriteOnce인 퍼시스턴트 볼륨과 연결합니다.
  resources:
    requests:
      storage: 5Gi          # 2.2 볼륨 크기가 최소 5Gi인 퍼시스턴트 볼륨과 연결합니다.
---
apiVersion: v1
kind: Pod
metadata:
  name: ebs-mount-container
spec:
  containers:
    - name: ebs-mount-container
      image: busybox
      args: [ "tail", "-f", "/dev/null" ]
      volumeMounts:
      - name: ebs-volume
        mountPath: /mnt
  volumes:
  - name : ebs-volume
    persistentVolumeClaim:
      claimName: my-ebs-pvc    # 3. my-ebs-pvc라는 이름의 pvc를 사용합니다.

accessModes와 resources 항목은 볼륨의 요구사항 - 해당 조건을 만족하는 퍼시스턴트 볼륨과 연결돼야 한다는 의미 
요구사항과 일치하는 퍼시스턴트 볼륨이 존재하지 않는다면 파드는 계속해서 Pending 상태로 남음 
조건에 맞는 볼륨이 생성되면 자동으로 퍼시스턴트 볼륨 클레임과 연결 됨
kubectl get pv,pvc 
퍼시스턴트 볼륨과 퍼시스턴트 볼륨 클레임의 상태가 bound 로 설정 됬다면 성공적으로 연결된 것
EBS 볼륨은 기본적으로 읽기, 쓰기가 모두 가능하면 1:1  관계의 마운트만 가능하기 때문에 ReadWriteOnce를 사용 

# 퍼시스턴트 볼륨을 선택하기 위한 조건 명시 
* accessModes와 볼륨 크기, 스토리지클래스, 라벨 셀렉터를 이용한 퍼시스턴트 볼륨 선택 
accessModes나 볼륨의 크기는 메타데이터일 뿐 볼륨이 정말로 그러한 속성을 가지도록 강제하지는 않음 

# accessModes
ReadWriteOnce RWO 1:1마운트만 가능, 읽기 쓰기 가능
ReadOnlyMany ROX 1:N 마운트 가능, 읽기 전용
ReadWriteMany RWX 1:N 마운트 가능, 읽기 쓰기 가능 

* esb-pv.yaml
spec:
  accessModes:
    - ReadWriteOnce   

* esb-pod-pvc.yaml 
spec:
  accessModes:
    - ReadWriteOnce     

#  resources.requests.storge  볼륨 크기 

* esb-pv.yaml
spec:
  capacity:
    storage: 5Gi

* esb-pod-pvc.yaml 
spec:
  resources:
    requests:
      storage: 5Gi      

#  storageClassName

* ebs-pv-storgeclass.yaml
spec:
  capacity:
    storage: 5Gi
  accessModes:
    - ReadWriteOnce
  storageClassName: my-ebs-volume

* ebs-pod-pvc-custom-sc.yaml 
spec:
  storageClassName: my-ebs-volume

# label 

* ebs-pv-label.yaml 
apiVersion: v1
kind: PersistentVolume
metadata:
  name: ebs-pv-label
  labels:
    region: ap-northeast-2a

* ebs-pod-pvc-label-selector.yaml 
spec:
  selector:
    matchLabels:
      region: ap-northeast-2a

# 퍼시스턴트 볼륨의 라이프사이클과 Reclaim Policy 
kubectl get pv,pvc 

출력 항목중 STATUS 
Available (사용 가능)
Bound (연결됨)
Released( PVC 삭제시  상태 - 퍼시스턴트 볼륨의 사용이 끝났다는 것을 의미 다시 사용 불가 - 실제 데이타는 볼륨 안에 존재 하기 때문에 삭제 하고 다시 생성)

출력 항목중 RECLAIM POLICY 
Reclaim Policy  - 퍼시스턴트 볼륨의 사용이 끝났을때 해당 볼륨을 어떻게 초기화할 것인지 별도로 설정 가능 
Retain , Delete , Recycle 방식이 있음 

# Retain : 기본적으로 보존하는 방식 (LifeCycle : Available -> Bound -> Released)

# Delete :   퍼시스턴트 볼륨 클레임이 삭제됨과 동시에 퍼시턴트 볼륨도 함께 삭제 가능한 경우에 한해서는 연결된 외부 스토리지도 함께 삭제 (데이타 유실)
*  ebs-pv-delete.yaml 
apiVersion: v1
kind: PersistentVolume
metadata:
  name: ebs-pv-delete
spec:
  capacity:
    storage: 5Gi
  accessModes:
    - ReadWriteOnce
  awsElasticBlockStore:
    fsType: ext4
    volumeID: <VOLUME_ID>
  persistentVolumeReclaimPolicy: Delete

# Recycle : 퍼시스턴트 볼륨 클레임이 삭제됬을 때 퍼시스턴트 볼륨의 데이터를 모두 삭제한 뒤 Available 상태로 만들어 줌 Deprecated 될 예정 (데이타 유실 )

# StorageClass와 Dynamic Provisioning 
다이나믹 프로비저닝은 퍼시스턴트 볼륨 클레임이 요구하는 조건과 일치하는 퍼시스턴트 볼륨이 존재하지 않는 다면 자동으로 퍼시스턴트 볼륨과 
외부 스토리지를 함께 프로지저닝 하는 기능 
EBS 와 같은 외부 스토리지를 미리 생성해둘 필요가 없음 퍼시스턴트 볼륨 클레임을 생성화면 외부 스토리지가 자동으로 생성
범용적으로 사용할 수 있는 기능은 아님 다이나믹 프로비저닝 기능이 지원되는 스토리지 프로비저너가 미리 활성화 되어 있어야 함 
AWS aws-ebs-csi-driver , GKE GcePersistentDiskCsiDriver 를 설치 했다면 자동으로 다이나믹 프로비저닝을 사용할 수 있음 
주의 할 점 : 퍼시스턴트 볼륨의 Reclaim Ploicy 가 자동으로 Delete로 설정됨 
                  Delete가 아닌 정책을 사용하고 싶다면 스토리지 클래스를 정의하는 YAML 파일에 reclaimPolicy: Retain 명시 하거나 kubectl edit or patch 등의 명령어로 직접 변경 필요 

- 다아니막 프로지저닝에서 특정 스톨리지 클래스를 기본값으로 사용 
* storageclass-default.yaml 
kind: StorageClass
apiVersion: storage.k8s.io/v1
metadata:
  name: generic
  annotations:
    storageclass.kubernetes.io/is-default-class: "true"
provisioner: kubernetes.io/aws-ebs
parameters:
  type: gp2
  fsType: ext4
  zones: ap-northeast-2a # 여러분의 쿠버네티스 클러스터가 위치한 가용 영역을 입력합니다.
 스토리지 클래스를 별도로 명시하지 않으면 자동으로 기본 스토리지 클래스를 통해 다이나믹 프로비저닝이 수행 
 storageClassName의 값을 "" 공백으로 설정하면 다이나믹 프로비저닝이 발생하지 않음 

# AWS에서 다이나믹 프로비저닝 사용하기 
1. kubectl get storageclass or sc 

2. storageclass 생성 
* storageclass-slow.yaml 
kind: StorageClass
apiVersion: storage.k8s.io/v1
metadata:
  name: slow
provisioner: kubernetes.io/aws-ebs
parameters:
  type: st1
  fsType: ext4
  zones: ap-northeast-2a  # 여러분의 쿠버네티스 클러스터가 위치한 가용 영역을 입력합니다.

* storageclass-fast.yaml 
kind: StorageClass
apiVersion: storage.k8s.io/v1
metadata:
  name: fast
provisioner: kubernetes.io/aws-ebs
parameters:
  type: gp2
  fsType: ext4
  zones: ap-northeast-2a # 여러분의 쿠버네티스 클러스터가 위치한 가용 영역을 입력합니다.

3. 퍼시스턴트 볼륨 클레임을 생성함으로써 다이나믹 프로비저닝을 발생 
* pvc-past-sc.yaml 
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pvc-fast-sc
spec:
  storageClassName: fast
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi

4. 생성 확인
kubectl get pv,pvc

########################################################
##  보안을 위한 인증과 인가 : ServiceAccount와 RBAC

RABC(Role Based Access Control)을 기반으로 하는 Service Account 
RABC라는 기능을 통해 특정 명령을 실행할 수 있는 권한을 서비스 어카운트에 부여 
권한을 부여받은 서비스 어카운트는 해당 권한에 해당하는 기능만 사용 가능 

* kubectl  명령어를 사용할때 내부적으로 처리 되는 절차
user -> kubectl -> http핸들러 -> Authentication -> Authorization -> Mulating Admisssion Controller -> Validating Admisssion Controller -> eted

쿠버네니티스 설치할때 설치 도구가 자동으로 kubectl이 관리자 권한을 갖도록 설정  - 설정 내용은 ~/.kube/config 라는 파일에서 확인 가능 

# 서비스 어카운트와 Role, Cluster Role
서비스 어카운트는 체계적으로 권한을 관리하기 위한 쿠버네티스 오브젝트 
네임스페이스에 속하는 오브젝트로 serviceaccount or sa 라는 이름으로 사용 

kubectl get serviceaccount 
kubectl create , delete 명령어로 생성 삭제 
kubectl create sa alicek106
--as 옵션을 사용하면 임시로 특정 서비스 어카운트 사용 가능 

kubectl get services --as system:serviceaccount:default:alicek106
Error from server (Forbidden): services is forbidden: User "system:serviceaccount:default:alicek106" cannot list resource "services" in API group "" in the namespace "default"
에러 반환 - 서비스 목록을 조회할 수 있는 권한 부여 받지 않았기 때문 

# 권한 부여 2가지 방법 
Role  : 네임스페이스에 속함 , 부여할 권한이 무엇인지를 나타냄 ex) 디플로이먼트를 생성, 서비스 목록 조회 
Cluster Role  : 네임스페이스에 속하지 않음 , 클러스터 단위의 권한을 정의 ex) 퍼시스턴트 볼륨의 목록을 조회 (네임스페이스에 속하지 않는 오브젝트)

kubectl get role
kubectl get clusterrole

* service-reader-role.yaml 
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: default
  name: service-reader
rules:
- apiGroups: [""]                 # 1. 대상이 될 오브젝트의 API 그룹
  resources: ["services"]          # 2. 대상이 될 오브젝트의 이름
  verbs: ["get", "list"]             # 3. 어떠한 동작을 허용할 것인지 명시

 apiGroups : 어떠한 API 그룹에 속하는 오브젝트에 대해 권한을 지정할지 설정 , "" 로 설정한 건 파드, 서비스 등이 포함된 코어 API 그룹을 의미  kubectl api-reousrces 로 오브젝트가 어떤 그룹에 속하는지 확인 가능
 resources : 어떠한 쿠버네티스 오브젝트에 대해 권한을 정의할지 설정 
 verbs : resource에  지정된 오브젝트에 대해 어떤 동작을 수행할 수 있는지 정의 (get, list, watch, create, update, patch , delete 등에서 선택 할수 있고 와일드 카드를 의미 하는 * 를 사용할 수 있음)
            특정 리소스에 한정된 기능을 사용할 때는 서브 리소스를 명시 해야 할 수도 있음 ex) resources: ["pods/exec"]

 Role을 생성하는 것만으로 서비스 어카운트나 사용자에게 권한이 부여되지 않음 
 Role을 특정 대상에게 부여하려면 롤바인딩(RoleBinding) 이라는 오브젝트를 통해 특정 대상과 롤을 연결해야 함 

 * rolebinding-service-reader.yaml 
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: service-reader-rolebinding
  namespace: default
subjects:
- kind: ServiceAccount
  name: alicek106
  namespace: default
roleRef:
  kind: Role
  name: service-reader
  apiGroup: rbac.authorization.k8s.io

kubectl apply -f service-reader-role.yaml  
kubectl apply -f rolebinding-service-reader.yaml 
kubectl get services --as system:serviceaccount:default:alicek106

롤 바인딩과 롤, 서비스 어카운트는 모두 1:1 관계가 아님 
하나의 롤은 여러 개의 롤 바인딩에 의해 참조 될수 있고 하나의 서비스 어카운트는 여러 개의 롤 바인딩에 의해 권한을 부여 받을 수 있음 
 
 # Role vs Cluster Role

kubectl get node --as system:serviceaccount:default:alicek106 
kubectl get services --as system:serviceaccount:default:alicek106 --all-namespaces
Error from server (Forbidden): services is forbidden: User "system:serviceaccount:default:alicek106" cannot list resource "services" in API group "" at the cluster scops

Role 은 네임스페이스에 종속 Cluster Role은 네임스페이스에 종속 안됨 - Cluster Role ( 클러스터 단위의 리소스에 권한을 정의하기 위해 사용)

* nodes-reader-clusterrole.yaml 
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  namespace: default
  name: nodes-reader
rules:
- apiGroups: [""]
  resources: ["nodes"]
  verbs: ["get", "list"]

* clusterrolebinding-nodes-reader.yaml 
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: nodes-reader-clusterrolebinding
  namespace: default
subjects:
- kind: ServiceAccount
  name: alicek106
  namespace: default
roleRef:
  kind: ClusterRole
  name: nodes-reader
  apiGroup: rbac.authorization.k8s.io

  kubectl apply -f nodes-reader-clusterrole.yaml 
  kubectl apply -f clusterrolebinding-nodes-reader.yaml 

# 여러 개의 클러스터 롤을 조합해서 사용하기 
자주 사용되는 클러스터 롤이 있다면 다른 클러스터 롤에 포함시켜 재사용 - Role aggregration 
* clusterrole-aggregation.yaml 
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: grand-parent-clusterrole
  labels:
    rbac.authorization.k8s.io/aggregate-to-parent-clusterrole: "true"
rules: []
  #- apiGroups: [""]
  #  resources: ["nodes"]
  #  verbs: ["get", "list"]
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
aggregationRule:
  clusterRoleSelectors:
  - matchLabels:
      rbac.authorization.k8s.io/aggregate-to-parent-clusterrole: "true"
metadata:
  name: parent-clusterrole
  labels:
    rbac.authorization.k8s.io/aggregate-to-child-clusterrole: "true"
rules: []
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: child-clusterrole
aggregationRule:
  clusterRoleSelectors:
  - matchLabels:
      rbac.authorization.k8s.io/aggregate-to-child-clusterrole: "true"
rules: [] # 어떠한 권한도 정의하지 않았습니다.
---
apiVersion: v1
kind: ServiceAccount
metadata:
  name: node-reader-test
  namespace: default
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: parent-clusterrolebinding
subjects:
- kind: ServiceAccount
  name: node-reader-test
  namespace: default
roleRef:
  kind: ClusterRole
  name: child-clusterrole
  apiGroup: rbac.authorization.k8s.io

kubectl apply -f clusterrole-appregation.yaml 
kubectl get no --as system:serviceaccount:default:node-reader-test 

# 쿠버네티스 API 서버에 접근 
서비스 어카운트의 시크릿을 이용해 쿠버네티스 API 서버에 접근 
API 서버도 HTTP 요청을 통해 쿠버네티스의 기능을 사용할 수 있도록 REST API 제공 
API 접근 위한 엔드포인트는 자동으로 개방되기 때문에 별도의 설정을 하지 않아도 접근 가능 
기본적으로 HTTPS 요청만 처리 하도록 설정 self-signed 인증서를 사용함 

curl https://localhost:6443 -k
{
  "kind": "Status",
  "apiVersion": "v1",
  "metadata": {},
  "status": "Failure",
  "message": "forbidden: User \"system:anonymous\" cannot get path \"/\"",
  "reason": "Forbidden",
  "details": {},
  "code": 403
}
인증 정보 사용하지 않았기 때문에  403에러 발생 
API 서버에 접근하려면 별도의 인증 정보를 HTTP 페이로드에 포함시켜 REST API 요청을 전송해야 함 
쿠버네티스는 서비스 어카운트를 위한 인증 정보를 시크릿에 저장 - 서비스 어카운트 생성하면 이에 대응하는 시크릿이 자동으로 생성 
서비스 어카운트에 연결된 시크릿에는 ca.crt (쿠버네티스 클러스터의 공개인증서), namespace(해당 서비스 어카운트가 존재하는 네임스페이스 저장), token(JWT) 총 3개의 데이터가 저장 되어 있음 
kubectl get secrets

# API 서버의 REST API 엔드포인트로 요청을 보낼 때 token의 데이터를 함께 담아서 보내야 인증 가능 
* 시크릿의 token 데이터를 base64로 디코딩한 다음 임시로 쉘 변수에 저장 
export secret_name=alicek106-token-cr2jv
export decoded_token=$(kubectl get secret $secret_name -o jsonpath='{.data.token}' | base64 -d)
echo $decoded_token
* header 에 token 정보 담아 재 요청 - 정상 호출 됨 
curl https://localhost:6443/apis --header "Authorization: Bearer $decoded_token" -k 

# kubectl proxy 명령어를 이용해 임시 프락시를 생성해서 API 서버에 별도의 인증 없이도 접근 가능 
   기본적으로 로컬 호스트 요청만 처리할 수 있으므로 가능하면 테스트 용도로만 사용 
kubectl proxy 
curl localhost:8001/   <- 호출 하면 사용할 수 있는 모든 경로를 출력 

kubectl 에서 사용할 수 있는 기능은 모두 REST API 에서 사용 가능 

/metrics 와 /logs에 접근하면 권한이 없다고 오류 반환 
권한 부여 
*  nonresource-rul-clusterrole.yaml
apiVersion: rbac.authorization.k8s.io/v1beta1
kind: ClusterRole
metadata:
  name: api-url-access
rules:
- nonResourceURLs: ["/metrics", "/logs"]
  verbs: ["get"]
---
apiVersion: rbac.authorization.k8s.io/v1beta1
kind: ClusterRoleBinding
metadata:
  name: api-url-access-rolebinding
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: api-url-access
subjects:
- kind: ServiceAccount
  name: alicek106
  namespace: default

# 클러스터 내부에서 kubernetes 서비스를 통해 API 서버에 접근 
사용자가 쿠버네티스 기능을 사용하려면 kubectl 이나 REST API 등의 방법을 통해 API 서버에 접근
쿠버네티스 클러스터 내부에서 실행되는 애플리케이션은   API 접근 할수 있는 서비스 리소슬 미리 생성하고 있음 -  kubernetes 라는 이름의 서비스 
파드는 kubernetes.default.svc라는 DNS 이름을 통해 쿠버네티스 API를 사용할 수 있음  - 접근은 되지만 특별한 권한이 따로 주어지는 것은 아님 
시크릿 토큰을 HTTP 요청에 담아 kubernetes 서비스에 전달해야만 인증가 인가를 진행 
쿠버네티스는 파드를 생성할 때 자동으로 서비스 어카운트의 시크릿을 파드 내부에 마운트 따라서 시크릿의 데이터를 파드로 가져올 필요는 없음 
시크릿 데이터는 기본적으로 파드의 /var/run/secrets/kubernetes.io/serviceaccount 경로에 마운트됨 (데이터가 각각 파일로 존재)
파드 내부에서 API 서버에 접근해야 한다면 token 파일에 저장된 내용을 읽어와 사용하면 됨 

# 쿠버네티스 SDK를 이용해 파드 내부에서 API 서버에 접근 
파드 내부에서 실행되는 애플리케이션이라면  HTTP 요청으로 REST API 를 사용해도 되지만 특정 언어로 바인딩된 쿠버네티스 SDK를 활용하는 방식을 더 많이 사용 

1. 서비스 어카운트 ,  롤, 롤 바인딩 처리 
kubectl create sa alicek106
kubectl apply -f service-reader-role.yaml
kubectl apply -f rolebinding-service-reader.yaml 

2. YAML 파일에 serviceAccountName 항목을 명시적으로 지정해 파드를 생성 
* sa-pod-python-sdk.yaml 
apiVersion: v1
kind: Pod
metadata:
  name: k8s-python-sdk
spec:
  serviceAccountName: alicek106
  containers:
  - name: k8s-python-sdk
    image: alicek106/k8s-sdk-python:latest

kubectl apply -f sa-pod-python-sdk.yaml 

3. 파드 내부에 마운트된 alicek106의 시크릿을 확인
kubectl exec -it k8s-python-sdk bash 
root@k8s-python-sdk:/# ls /var/run/secrets/kubernetes.io/serviceaccount/
ca.crt namespace token 

4. python 코드로 쿠버네티스 API  사용할수 있는 코드  작성 
* list-service-and-pod.py 
from kubernetes import client, config
config.load_incluster_config() # 1 -  파드 내부에 마운트된 어카운트 인증서 정보 읽어 인증 및 인가 수행 

try:
  print('Trying to list service..')
  result = client.CoreV1Api().list_namespaced_service(namespace='default') # 2 -  CoreV1 그룹의 API를 이용해 특정 네임스페이스 서비스 목록 출력 
  for item in result.items:
    print('-> {}'.format(item.metadata.name))
except client.rest.ApiException as e:
  print(e)

print('----')

try:
  print('Trying to list pod..')
  result = client.CoreV1Api().list_namespaced_pod(namespace='default') # 3 - CoreV1 그룹의 API를 이용해 특정 네임스페이스 파드  목록 출력 
  for item in result.items:
    print(item.metadata.name)
except client.rest.ApiException as e:
  print(e)

5. python3 list-service-and-pod.py 
위의 명령어로 파이썬 코드 실행 하면 서비스 목록은 정상 출력되나 파드 목록 출력은 에러 발생 ( 조회 관련 권한을 부여받지 않았기 때문)

# 서비스 어카운트에 이미지 레지스트리 접근을 위한 시크릿 설정   
 docker-registry 타입의 시크릿 도커 이미지 레지스트리에 접근하기 위해 사용 
 디플로이먼트 , 파드 정의 하는 YAML 파일에서 imagePullSecrets항목에 명시해 사용 
 서비스 어카운트를 이용하면 비공개 레지스트리 접근을 위한 시크릿을 서비스 어카운트 자체에 설정 할 수 있음 
 디플로이먼트 , 파드 YAML 파일에 정의 하지 않아도 됨 
ex) registry-auth 라는 이름의 시크릿이 존재 한다면 아래 처럼 작성 
 * sa-reg-auth.yaml 
apiVersion: v1
kind: ServiceAccount
metadata:
  name: reg-auth-alicek106
  namespace: default
imagePullSecrets:
- name: registry-auth

kubectl apply -f sa-reg-auth.yaml 
kubectl describe sa reg-auth-alicek106 | grep image
Image pull secrets: registry-auth 

YAML 파일에서 serviceAccountName 항목을 정의하지 않으면 기본으로 default  서비스 어카운트의 시크릿이 파드에 마운트 됨 
default 서비스 어카운트에 imagePullSecrets 항목을 추가하면 아무런 설정을 하지 않았을 때에도 사설 레지스트리 인증을 기본적으로 수행 되게 설정할 수 있음 

# kubeconfig 파일에 서비스 어카운트 인증 정보 설정 
kubectl 명령어를 사용해 쿠버네티스 클러스터 제어 할때는 kubeconfig 설정 파일을 통해 인증을 진행 
쿠버네티스 설치하면 kubeconfig  파일에는 기본적으로 클러스터 관리자 권한을 가지는 인증서 정보가 저장됨 
권한이 제한된 서비스 어카운트를 통해 kubectl 명령어를 사용하도록 kubeconfig 파일을 설정 할 수 있음 
- 서비스 어카운트에 연결된 시크릿의 token 데이터를 kubeconfig에 명시함으로써 kubelctl 명령어의 권한을 제한 할 수 있음 

kubeconfig 파일은 ~/.kube/config 경로에 존재 - KUBECONFIG 쉘 환경 변수로 경로를 직접 지정 가능 
3개의 파트로 구성 
* clusters 
- kubectl이 사용할 쿠버네티스 API  서버의 접속 정보 목록 
* users
- 쿠버네티스 API 서버에 접속하기 위한 사용자 인증 정보 목록  - 서비스 어카운트의 토큰을 입력 할 수 있음 , 루트 인증서에서 발급한 하위 인증서의 데이타를 입력 
* contexts 
- clusters 항목과 users 항목에 정의된 값을 조합해 최종적으로 사용할 쿠버네티스 클러스터의 정보를 설정 

ex) users 항목에 서비스 어카운트의 token 데이터를 등록 및 컨테스트 추가 및 사용 컨텍스트 변경 
kubectl get secrets
export secret_name=alicek106-token-gfg41
export decoded_token=$(kubectl get secret $secret_name -o jsonpath='{.data.token}' | base64 -d)
kubeconfig 파일은 vim편집기로 직접 수정 해도 되지만 kubectl config 명령어로 수정 가능
kubectl config set-credentials 명령어로 새로운 사용자 등록 가능
kubectl config set-credentials alicek106-user --token=$decoded_token <- 사용자 추가 
kubectl config set-context my-new-context --cluster=kubernetes --user=alicek106-user <- 컨텍스트 생성
kubectl config get-contextskubectl config use-context my-new-context  <- 컨텍스트 변경 

# User & Group 
롤 방인딩이나 클러스터 롤 바인딩을 정의 하는 YAML 파일의 Kind 값에는 ServiceAccount 대신 User , Group 설정 할수 있음 
오브젝트가 아님 kubectl user or group 사용할 수 없음 

kubectl get service --as system:serviceaccount:default:alicek106
--as 에 사용한 system:serviceaccount:default:alicek106은 사실 서비스 어카운트를 지칭하는 고유한  User 이름 임
서비스 어카운트를 생성하면 system:serviceaccount:<네임스페이스 이름>:<서비스어카운트 이름> 이라는 유저 이름으로 서비스 어카운트를 지칭할 수 있음 
Group은 User를 모아 놓은 집합 
쿠버네티스에서 사용할 수 있는 대표적인 그룹은 서비스 어카운트의 집합인 system:serviceaccounts로 시작하는 그룹 
Kind:Group 으로 명시하되 그룹 이름을 system:serviceaccounts로 설정하면 됨 
그룹 예시 - 미리 정의된 유저나 그룹은 접두어   system: 을 사용 
system:serviceaccounts:<네임스페이스 이름> : 특정 네임스페이스의 모든 서비스 어카운트를 의미
system:authenticated : API 서버의 인증에 성공한 그룹
system:unauthenticated : API 서버의 인증에 실패한 그룹
system:anonymous : API 서버의 인증에 실패한 유저 

# 다양한 인증 방법에서의 User와 Group 
kubeconfig 파일에 기본적으로 설정돼 있는 인증 방법은 쿠버네티스 자체적으로 지원하는 인증 방법인 'x509 인증서'
별도의 인증 서버를 사용하면 깃허브 계정, 구글 계정, LDAP 데이터 등을 쿠버네티스 인증에 사용 할 수 있음 
- 별도의 인증 서버는 쿠버네티스가 아닌 별도의 솔루션을 사용해 구축 하는 것이 일반적
  OAuth OIDC를 사용해 인증 시스템을 구축하려면 덱스(Dex)  사용
  단순 토큰을 이용해 웹훅(Webhook) 인증 시스템을 구축하려면 가드(Guard) 사용 

# x509 인증서를 이용한 사용자 인증
보안 연결을 위해 자체적으로 사인한 루트 인증서를 사용 쿠버네티스 설치시 자동으로 생성됨
kubeadm의 경우 기본적으로 쿠버네티스 마스터의 /etc/kubernetes/pki 디렉토리에 저장 
kops를 사용하고 있다면 S3 버킷의 ${클러스터이름}/pki 디렉토리에 저장 

ls /etc/kubernetes/pki 
ca.crt 가 루투 인증서 ca.key 인증서에 대응하는 비밀키 
쿠버네티스 루트 인증서로부터 발급된 하위 인증서를 사용하면 쿠버네티스 사용자를 인증할 수 있음 

ex) 루트 인증서로부터 하위 인증서를 생성해 API 서버에 인증
1. 하위 인증서를 위한 비밀키와 인증서 사인요청 파일을 생성 
openssl genrsa -out alicek106.key 2048
openssl req -new -key alicek106.key -out alicek106.csr -subj "/O=alicek106-org/CN=alicek106-cert"
위 처럼 생성하면 롤 바인딩 등에서 alicek106-cert라는 이름의 유저에게 권한을 부여 해야 함 

2. 쿠버네티스의 비밀키로 alicek106.csr 파일에 서명 - openssl 명령어 직접 사용해도 되지만 서명하는 기능을  API로 제공 
* alicek106-csr-k8s-latest.yaml
# 쿠버네티스 1.19 버전부터 새로운 CSR 리소스 형식이 도입되었습니다.
# 최신 버전 (1.22 버전 이상) 의 쿠버네티스를 사용하고 있다면 아래의 리소스를 사용해주세요.
apiVersion: certificates.k8s.io/v1
kind: CertificateSigningRequest
metadata:
  name: alicek106-csr
spec:
  signerName: kubernetes.io/kube-apiserver-client
  groups:
  - system:authenticated
  request: <CSR>
  usages:
  - digital signature
  - key encipherment
  - client auth

  CertificateSigningRequest  리소스를 생성하면 쿠버네티스에ㅔ서 내부적으로 루트 인증서의 비밀키로 서명해 반환 

alicek106.csr 파일의 내용을 base64로 인코딩한 다음 alicek106-csr.yaml 파일의 <CSR> 부분으로 가져옴
export CSR=$(cat alicek106.csr | base64 | tr -d '\n')
sed -i -e "s/<CSR>/$CSR/g" alicek106.csr.yaml 
kubectl apply -f alicek106-csr-k8s-latest.yaml 
kubectl get csr ( CONDITION 항목이  Pending 상태)
kubectl certificate approve alicek106-csr
kubectl get csr ( CONDITION 항목이  Approved.Issued 상태)
kubectl get csr alicek106-csr -o jsonpath='{status.certificate}' | base64 -d > alicek106.crt 

3. 새롭게 생성된 하위 인증서 파일인 alicek106와 비밀키 파일인 alice_k106.key로 kubeconfog에 새로운 사용자 등록 
kubectl config set-credentials alicek106-x509-user  -- client-certificate=alicek106.crt --client-key=alicek106.key 

* kubectl의 부가 명령어인 --client-certificate , --client-key 옵션을 사용하면 kubeconfig에 하위 인증서와 비밀키 등록하지 않아도 임시로 인증서 테스트 할 수 있음 
kubectl get svc -- client-certificate=alicek106.crt --client-key=alicek106.key 

4. 새롭게 등록한 사용자를 통해 새 컨텍스트 함께 생성  후 사용 컨텍스트 변경 
kubectl config set-context alicek106-x509-context --cluster kubernetes ==user alicek106-x509-user 
kubectl config use-context alicek106-x509-context 

5. 권한 부여 
* x-509-cert-rolebinding-user.yaml 
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: service-reader-rolebinding-user
  namespace: default
subjects:
- kind: User
  name: alicek106-cert
roleRef:
  kind: Role
  name: service-reader
  apiGroup: rbac.authorization.k8s.io

* x-509-cert-rolebinding-group.yaml 
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: service-reader-rolebinding-group
  namespace: default
subjects:
- kind: Group
  name: alicek106-org
roleRef:
  kind: Role
  name: service-reader
  apiGroup: rbac.authorization.k8s.io

x509 인증서를 이용한 인증 방법은 한계점이 있어 실제 환경에서는 사용하기 어려울 수 있음 
인증서가 유출됬을때 하위 인증서를 파기 하는 기능이 제공 안됨 파일로 인증 정보를 관리 하는 것은 보안상 미흡
개념적으로 만 학습 하고 실제 클러스터를 운영할 때는 덱스나 가드 등의 솔루션을 이용해 깃허브 , LDAP 같은 서드 파티에서 인증정보 관리 하는게 효율적임 

########################################################
##  어플리케이션 배포를 위한 고급 설정

# 컨테이너와 파드의 자원 사용량 제한 : Limits
쿠버네티스는 내부적으로 도커 컨테이너와 동일하게 cgroup 이라는 리눅스 기술을 사용하므로 파드를 생성할 때 docker  
명령어와 동일한 원리로  CPU, 메모리 최대 사용량을 제한할 수 있음 
* resource-limit-pod.yaml 
apiVersion: v1
kind: Pod
metadata:
  name: resource-limit-pod
  labels:
    name: resource-limit-pod
spec:
  containers:
  - name: nginx
    image: nginx:latest
    resources:
      limits:
        memory: "256Mi"
        cpu: "1000m"

cpu: "1000m" 는 cpu 1개를 의미 
kubectl apply -f resource-limit-pod.yaml
kubectl get pods -o wide <node 값 확인>
kubectl describe node <node 값>

# 컨테이너와 파드의 자원 사용량 제한하기 : Requests 
Limit는 해당 파드의 컨테이너가 최대로 사용할 수 있는 자원의 상환선
Requests는 적어도 이만큼의 자원은 컨테이너에게 보장돼야 한다는 의미 
쿠버네티스의 Overcommit을 가능하게 만드는 기능 

 Overcommit - 한정된 자원을 효율적으로 사용하기 위한 방법으로, 사용할 수 있는 자원 보다 더 많은 양을 가상 머신이나 컨테이너에게 할당함으로써 
 전체 자원의 사용률(Utilization)을 높이는 방법 
 ex)  총 1G 메모리 탑재한 서버에 컨테이너 A, B 설치 둘다 500M 메모리 할당 해 주었는데 A라는 서버가 더 많은 처리를 해서 메모리를 많이 사용하는 반면
 B 컨테이너는 메모리 사용량이 적은 경우 컨테이너 메모리 설정 자체를 750M 처럼 물리적 메모리를 초과해서 할당 해 주는 방식 
 그러나 A, B 컨테이너 모두가 많은 메모리 사용하게 되면 물리적 메모리를 초과 하게 됨으로 문제 발생 이런 문제를 해결 하기 위해 
 적어도 어느정도만큼은 사용할 수 있다는 경계선을 지정해 주는 부분을 Requests 라고 함 (컨테이너가 최소한으로 보장받아야 하는 자원의 양을 뜻함)

* resource-limit-with-request-pod.yaml
apiVersion: v1
kind: Pod
metadata:
  name: resource-limit-with-request-pod
  labels:
    name: resource-limit-with-request-pod
spec:
  containers:
  - name: nginx
    image: nginx:latest
    resources:
      limits:
        memory: "256Mi"
        cpu: "1000m"
      requests:
        memory: "128Mi"
        cpu: "500m"

최소한 128Mi 의 메모리 사용은 보장되지만, 유휴 메모리 자원이 있다면 최대 256Mi 까지 사용 
CPU 도 같은 원리로 최소한 0.5 CPU 만큼은 사용할 수 있지만 유휴 CPU 자원이 있따면 최대 1 CPU 사용

requests는 컨테이너가 보장받아야 하는 최소한의 자원을 뜻하기 때문에 노드의 총 자원의 크기보다 더 많은 양의 requests를 할 당 할 수는 없음 
파드를 할당할 때 사용되는 자원 할당 기준은 Limits가 아닌 requests
노드에 할당된 파드의 Limits값의 합은 노드의 물리 자원의 크기를 초과할 수도 있음 

# CPU 자원 사용량의 제한 원리 
CPU를 m(밀리코어) 단위로 제한 1개의 CPU는 1000m에 해당 

# QoS 클래스와 메모리 자원 사용량 제한 원리 
파드의 컨테이너는 최대 Limits만큼의 자원을 사용 할수 있지만, 최소한 Requests만큼의 자원을 사용할 수 있도록 보장 
Requests보다 더 많은 자원을 사용하는거를 오버커밋이라 함 
Request를 넘어 자원을 사용하다 다른 컨테이너와 자원 사용 충돌이 발생 하면 CPU 스로틀과 괕은 원리에 의해 자원 사용이 실패 할 수 있음
CPU 는  일시적으로 컨테이너 내부의 프로세스들이 스로틀이 걸릴 뿐 컨테이너 자체에 큰 문제는 발생하지 않음
CPU는 압축 가능 자원 (compressible)
메모리는 압축 불가능한 자원 (Incompressible)
메모리 사용량에 있어서 경합이 발생하면 문제가 심각함 
- 쿠버네티스는 이러한 경우 가용 메모리 확보하기 위해 우선 순위(Limits와 Requests 값에 따라 내부적으로 우선 순위 계산) 가 낮은 파드 또는 프로세스를 강제 종료 하게 설계됨  (Eviction)
  쿠버네티스는 파드의 우선순위를 구분하기 위해 3가지 종류의 QoS(Quality Of Service) 클래스를 명시적으로 파드에 설정 

# 쿠버네티스에서의 메모리 부족과 OOM (Out Of Memory)
쿠버네티스 노드에는 노드의 이상 상태 정보를 제공하는 Condition 라는 값이 존재 (MemoryPressure, DiskPressure등)
kubectl describe nodes 명령어로 확인 가능 
kubectl describe nodes | grep -A9 Conditions
메모리가 부족하지 않은 경우 MemoryPressure Status 값 False  부족한 경우 True (기본적으로 가용 메모리가 100Mi 이하일때 발생하도록 kubectl에 설정되 있음)
메모리 부족이 발생하면 해당 노드에서 실행 중이던 모든 파드의 우선 순위를 매긴 다음 가장 우선 순위가 낮은 파드를 다른 노드로 퇴거(Evict) 처리 
MemoryPressure True이면 더 이상 파드 할당 하지 않음 
MemoryPressure 와 같은 이상 상태를 감지하기 위한 임계치를  Hard Eviction Threshold라고 함 kubectl 실행 옵션에서 설정 값 변경 가능 

 # 리눅스의 OOM(Out of Memory) Killer - 리눅스 시스템에서 운순순위가 낮는 프로세스 종료 하는 처리 
 OOM 우선 순위 점수에는 oom_score_adj, oom_score 존재 OOM  Killer는 oom_score의 값에 따라 종료할 프로세스 선정
 프로세스가 메모리를 얼마나 더 많이 사용하고 있는 지에 따라 프로세스의 최종 oom_score가 갱신 
 ps aux | grep kubelet 출력된 내용중  PID  값 확인 후 아래 명령어로 확인 kubelet는 -999로 메모리 부족하다고 해서 강제 종료 되지 않음 
 cat /proc/PID값/oom_score_adj 

# Qos 클래스의 종류 
 BestEffort, Burstable, Guraranteed 

1. Guaranteed : 컨테이너에 설정된 Limits와 Requests 값이 완전히 동일 할때 부여되는 클래스 
kubectl describe pod resource-limit-pod | grep QoS
QoS Class:  Guaranteed
이전 생성한 파드는 Guaranteed로 설정 되어 있음 
limits 만 명시했는데도 Guaranteed로 분류 됨 - Requests 없이 Limits만 정의 하면 Requests 값 또한 Limits와 동일하게 설정 되기 때문 
Guaranteed를 명시적으로 생성하고 싶다면 YAML 파일에서 Limits , Requests 값을 동일하게 설정 
자원의 오버커밋을 허용하지 않기 때문에 할당 받은 자원을 안정적으로 보장(Guaranteed)
Guaranteed  클래스 파드 내부에서 실행 되는 프로세스들은 모두 기본 OOM점수가 -997로 설정됨 
파드 내에 컨테이너가 여러 개 존재 한다면 모든 컨테이너의 Requests와 Limits의 값이 완전히 같아야만 파드가 Guaranteed로 분류됨 

2. BestEffort : Requests, Limits를 아예 설정하지 않은 파드에 설정되는 클래스 
 YAML 파일에서 resources 항목을 아예 사용하지 않으면 자동으로 BestEffort 클래스로 분류 
 Limits 값을 설정하지 않기 때문에 노드에 유휴 자원이 있다면 제한 없이 모든 자원을 사용 
 Requests 또한 설정하지 않았기 때문에 사용을 보장받을 수 있는 자원이 존재 하지 않음 
상황에 따라 노드에 존재하는 모든 자원을 사용할 수도 있지만 반대로 자원을 전혀 사용 하지 못할 수도 있음 

3. Burstable :  Requests와 Limits가 설정돼 있지만 Limits값이 Requests보다 큰 파드를 의미 
Guraranteed, BestEffort에 속하지 않는 모든 파드는 Burstable로 분류된다고 생각하면 됨 

# QoS 클래스와 메모리 부족 
 Kubelet 이 메모리가 부족한 상황을 감지하면 우선 순위가 가장 낮은 파드를 종료한 뒷 다른 노드로 퇴거(Evict)를 수행
 메모리 사용량이 갑작스럽게 높아지면 리눅스의 OOM Killer는 OOM 점수가 가장 낮은 컨테이너의 프로세스를 강제로 종료 할 수도 있음 
 파드가 퇴거 되면 단순히 다른 노드에서 파드가 다시 생성 OOM Killer에 의해 파드 컨테이너의 프로세스가 종료되면 해당 컨테이너는 
 파드의 재시작 정책(restartPolicy)에 의해 다시 시작 
 OOM Killer는 메모리를 많이 사용하고 있는 프로세스를 강제로 종료하는 것이지 컨테이너나 파드를 종료 시키는 것은 아님 

 파드의 우선순위는 Guaranteed가 가장 높으며 그 뒤로 Burstable, BestEffort 순 
우선 순위는 항상 절대적인 것은 아님 - Burstable, BestEffort 클래스의 파드가 현재 메모리를 얼마나 사용하고 있는지에 따라 우선순위가 역전 될수 있음
파드가 메모리를 많이 사용하면 사용할수록 우선순위가 낮아짐 

# 자원 오버커밋의 필요성 
오버커밋이 쿠버네티스의 기능이라고 해서 반드시 사용해야 하는 것은 아님 

# ResouceQuota & LimitRange
여러 개발팀 쿠버네티스 사용시 가장 이상적인 방법은 개발팀마다 쿠버네티스 클러스터를 하나씩 제공 - 관리 힘듬, 클러스터 프로지저닝을 위한 비용 증가 
대안으로 네임스페이스를 개발팀마다 생성 개발팀이 해당 네임스페이스에서만 쿠버네티스 API 사용할 수 있도록 롤, 롤 바인딩, 적절한  RBAC를 설정 운영
네임스페이스에서 할당할 수 있는 자원의 최대 한도 또는 범위를 설정할 필요 발생 
ResourceQuota를 이용해 네임스페이스의 자원 사용량을 제한 LimitRange로 자원 할당의 기본 값이나 범위를 설정 

# ResouceQuota로 자원 사용량 제한 
네임스페이스의 자원 사용량을 제한할 수 있는 쿠버네티스 오브젝트 
네임스페이스에서 할당할 수 있는 자원(CPU, 메모리, 퍼시스턴트 볼륨 클레임의 크기, 컨테이너 내부의 임시 스토리지)의 총합을 제한
네임스페이스에서 생성할 수 잇는 리소스(서비스, 디플로이먼트 등)의 개수를 제한 
네임스페이스에 종속되는 오브젝트이기 때문에 네임스페이스별로  ResouceQuota 리소스를 생성 해야 함 
kubectl get resourcequota or quota

* resouce-quota.yaml 
apiVersion: v1
kind: ResourceQuota
metadata:
  name: resource-quota-example
  namespace: default
spec:
  hard:
    requests.cpu: "1000m"
    requests.memory: "500Mi"
    limits.cpu: "1500m"
    limits.memory: "1000Mi"

Requests와 Limits를 함께 제한할 필요는 없음 , CPU 메모리를 하나의 ResouceQuota 에서 제한할 필요도 없음 필요에 따라 설정 하면 됨 
default 네임스페이스에서 사용할 수 있는 총 자원의 할당량 제한 , 단일 파드의 자원 할당량을 제한 한 것이 아님 

kubectl apply -f resouce-quota.yaml
kubectl describe quota

새롭게 생성하는 파드가 한계치보다 많은 자원을 사용하려고 하면 파드 생성하는 API 요청은 실패
ResouceQuota를 생성하기 이전에 존재하고 있던 파드들이 이미 자원을 한계치보다 많이 사용하고 있다고 해서 기존의 파드가 종료 되지는 않음 

Test 
메모리를 과도하게 사용하는 파드 생성
kubectl run memory-over-pod --image=nginx --generator=run-pod/v1 --requests='cpu=200m, memory=300Mi' --limits='cpu=200m,memory=3000Mi'
실행시 에러 발생 

deployment yaml 을 이용해 생성 
* deployment-over-memory.yaml 
apiVersion: apps/v1
kind: Deployment
metadata:
  name: deployment-over-memory
spec:
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      name: nginx
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx
        resources:
          limits:
            memory: "3000Mi"
            cpu: "1000m"
          requests:
            memory: "128Mi"
            cpu: "500m"

kubectl apply -f deployment-over-memory.yaml
실행하면 에러 없이 정상적으로 생성  하지만 파드의 목록을 확인해 보면 해당 디플로이먼트로 부터 생성된 파드가 존재 하지 않음 
kubectl get pods | grep deployment-over-memory 

파드를 생성하는 주체는 디플로이먼트가 아니라 레프리카셋 - 디플로이먼트 리소스가 직접 파드를 생성하지는 않기 때문 
에러 로그는 레프리카 셋에 남아 있음 
kubectl get replicasets

레프리카 셋은 지속해서 라벨 셀렉터에 해당하는 파들르 생성하려고 시도 하기 때문에 ResouceQuota 정보가 업데이트 되거나 가용 자원이 발생하면 파드 정상 생성 
- 계속 해서 빠른 속도로 파드를 생성하려고 시도하지는 않음  일반적으로 지수 함수의 간격을 두고 동일한 동작을 다시 시도 
10초 , 20초, 40초, 80초, 160초 ... 와 같은 주기로 파드 생성을 다시 시도 

# ResouceQuota 로 리소스 개수 제한하기 
아래의 쿠버네티스 오브젝트의 개수를 제한할 수 있음
* 디플로이먼트 , 파드, 서비스, 시크릿, 컨피그맵, 퍼시스턴트 볼륨 클레임 등의 개수 
* NodePort 타입의 서비스 개수, LoadBalancer 타입의 서비스 개수 
* QoS 클래스 중에서 BestEffort 클래스에 속하는 파드의 개수 

파드 서비스이 최대 개수를 제한 하려면 YAML 파일에 count/pod  와 같은 형식으로 정의 
제한 예시 
spec:
  hard:
    count/resourcequota:3
    count/secrets: 5
    count/configmaps: 5
    count/persistentvolumeclaims: 2
    count/services.nodeports: 3
    count/services.loadbalancers: 1
    count/deployment.apps: 0 

* quota-limit-pod-svc.yaml 
apiVersion: v1
kind: ResourceQuota
metadata:
  name: resource-quota-example
  namespace: default
spec:
  hard:
    requests.cpu: "1000m"
    requests.memory: "500Mi"
    limits.cpu: "1500m"
    limits.memory: "1000Mi"
    count/pods: 3
    count/services: 5

# ResourceQuota로 BestEffort 클래스의 파드 개수 제한하기 
* quota-limit-besteffort.yaml 
apiVersion: v1
kind: ResourceQuota
metadata:
  name: besteffort-quota
  namespace: default
spec:
  hard:
    count/pods: 1
  scopes:
    - BestEffort

ResouceQuota에 limits,cpu나 limits.memory 등을 이용해 네임스페이스에서 사용 가능한 자원의 합을 설정했다면 
파드를 생성할 때 반드시 해당 함목을 함께 정의해 주어야 함 

# LimitRange 로 자원 사용량 제한 
특정 네임스페이스에서 할당되는 자원의 범위 또는 기본값을 지정할 수 있는 쿠버네티스 오브젝트 
* 파드의 컨테이너에 CPU나 메모리 할당량이 설정돼  읺지 않은 경우 컨테이너에 자동으로 기본 Requests , Limits 값을 설정할 수 있음 
* 파드 또는 컨테이너의 CPU, 메모리, 퍼시스턴트 볼륨 클레임 스토리지 크기의 최소값/최대값을 설정 
네임스페이스에 종속되어 네임스페이스별로 적용할 수 있는 기능 
kubectl get limitranges or limits # 기본적으로 어떠한 LimitRange도 생성돼 있지 않음 

* limitrange-example.yaml 
apiVersion: v1
kind: LimitRange
metadata:
  name: mem-limit-range
spec:
  limits:
  - default:                # 1. 자동으로 설정될 기본 Limit 값
      memory: 256Mi
      cpu: 200m
    defaultRequest:        # 2. 자동으로 설정될 기본 Request 값
      memory: 128Mi
      cpu: 100m
    max:                   # 3. 자원 할당량의 최대값
      memory: 1Gi
      cpu: 1000m
    min:                   # 4. 자원 할당량의 최소값
      memory: 16Mi
      cpu: 50m
    type: Container        # 5. 각 컨테이너에 대해서 적용


LimitRange에서 maxLimitRequestRation 항목을 사용하면 파드의 컨테이너에서 오버커밋되는 자원에 대한 비율을 제한 할 수 있음 
오버커밋을 얼마나 사용할 수 있는지 제어할 수 있을 뿐 아니라 이 값을 1로 설정함으로써 반드시 Guaranteed 클래스의 파드만을 생성하도록 강제하는 용도로 사용 가능 
* limitrange-ratio.yaml 
apiVersion: v1
kind: LimitRange
metadata:
  name: limitrange-ratio
spec:
  limits:
  - maxLimitRequestRatio:
      memory: 1.5
      cpu: 1
    type: Container


파드 단위로 자원 사용량의 범위를 제한 하고 싶은 경우 
* limitrange-example-pod.yaml 
apiVersion: v1
kind: LimitRange
metadata:
  name: pod-limit-range
spec:
  limits:
  - max:
      memory: 1Gi
    min:
      memory: 200Mi
    type: Pod

ResouceQuota에서 네임스페이스의 Limits, Requests를 설정하면 기본적으로 BestEffor  클래스의 파드 생성이 거부 되지만
LimitRange를 사용하면 파드의 컨테이너에 일괄적으로 기본 자원 할당량을 설정할 수 있음 

# ResouceQuota, LimitRange위 원리 : Adminssion Controller 
Adminssion Controller - 사용자의 API 요청이 적절한지 검증하고 , 필요에 따라 API 요청을 변형하는 단계 
ServiceAccount, ResouceQuota, LimitRange 어드미션 컨트롤러의 한 종류 
쿠버네티스에는 총 두 단계의 어드미션 컨트롤러 존재 
API 요청을 검사하는 것을 검증 (Validating) 단계 , API 요청을 적절히 수정하는 것을 변형(Mutating) 단계 라고 함 
- 필요하다면  어드미션 컨트롤러를 직접 구현해 쿠버네티스에 등록 가능 

# 쿠버네티스 스케줄링 
컨테이너가 가상 머신과 같은 인스턴스를 새롭게 생성할 때 그 인스턴스를 어느 서버에 생성할 것일지 결정하는 일 

* 파드가 노드에 생성되는 절차 
1. ServiceAccount, RoleBinding 등의 기능을 이용해 파드 생성을 요청한 사용자의 인증 및 인가 작업을 수행 
2. ResouceQuota, LimitRange와 같은 어드미션 컨트롤러가 해당 파드 요청을 적절히 변형(Mutable) 하거나 검증(Vaildate)
3. 어드미션 컨트롤러의 검증을 통과해 최종적으로 파드 생성이 승인 됬다면 쿠버네티스는 해당 파드를 워커 노드 중 한곳에 생성 

스케줄링은 3번 단계에서 수행됨 
kubectl get pods -n kube-system 
eted는 분산 코디네이터(Distributed Coordinator) 라고 불리는 도구의 일종으로 클라우드 플랫폼 등의 환경에서 여러 컴포넌트가 정상적으로 상호 작용할 수 있도록 데이터를 조정하는 역활을 담당 
디플로이먼트나 파드의 목록과 정보, 클러스터 자체의 정보 등과 같은 대부분의 데이터가 etcd에 저장 
etcd에 저장된 데이타는 무조건 API 서버(kube-apiserver)를 통해서만 접근 
etcd에 저장된 파드의 데이터에는 해당 파드가 어느 워커 노드에서 실행되는 지를 나타내는 nodeName 항목이 존재 
kubectl get pods mypod -o yaml | grep -F3 nodeName
인증 ,인가, 어드미션 컨트롤러 등의 단계를 모두 거쳐 파드 생성 요청이 최종적으로 승인됐다면 API 서븐ㄴ etcd 에 파드 데이터를 저장 하지만 nodeName은 설정되지 않은 상태로 저장됨 
kube-scheduler는 API 서버의 Watch를 통해 nodeName이 비어 있는 파드 데이터가 저장됬다는 사실을 전달 받고 스케줄링 대상으로 판단  파드를 할당할 적절한 노드를 선택한 다음 
API 서버에게 해당 노드의 파드를 바인딩할 것을 요청  그러고 나면 파드의 nodeName항목의 값에는 선택된 노드의 이름이 설정 됨 

# 파드가 생성될 노드를 선택하는 스케줄링 과정 
노드 필터링 , 노드 스코어링 단계를 거쳐 최종적으로 노드를 선택
* 노드 필터링 : 파드를 할당할 수 잇는 노드와 그렇지 않은 노드를 걸러내는 단계 
* 노드 스코어링 : 쿠버네티스의 소스코드에 미리 정의된 알고리즘의 가중치에 따라서 노드의 점수를 계산 , 가장 점수가 높은 노드를 최종적으로 선택 
노드 스코어링은 내장된 로직에  의해 계산되기 때문에 직접 점수를 매기는 알고리즘을 수정하는 경우는 많지 않음 
대부분 스케줄링 조건을 파드의 YAML 파일에 설정함으로써 노드 필터링 단계에 적용할 수 있도록 구성하는 것이 일반적 

# nodeName과 nodeSelector를 사용한 스케줄링 방법 
 특정 워커 노드에 파드를 할당하는 가장 확실한 방법은 파드의 YAML 파일에 노드의 이름을 직접 명시 
 노드의 이름을 고정으로 설정했기 때문에 다른 환경에서 YAML 파일을 보편적으로 사용하기 어려움 노드에 장애 발생시 대처 힘듬 
 kubectl get nodes 
 출력된 노드중에 pod 설치할 node명을  yaml파일에 명시 
 * nodename-nigin.yaml 
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  nodeName: <워커 노드 nodeName> 
  containers:
  - name: nginx
    image: nginx:latest

# 노드의 라벨을 사용 하는 방법 - 라벨을 이용하면 특정 라벨이 존재하는 노드에만 파드를 할당 
노드의 라벨은 쿠버네티스가 자동으로 설정해 놓은 것도 있지만 필요에 따라 직접 라벨을 추가 할 수 있음 
kubectl get nodes --show-labels
미리 설정된 라벨들은 대부분 kubernetes.io/ 라는 접두어로 시작 
기본적으로 설정되는 라벨에는 해당노드의 OS , CPU , 호스트 이름 등이 있음 

노드에 라벨 추가 
kubectl label nodes <노드이름> <추가할라벨>
kubectl label nodes node-1 myalbel/disk=hdd
노드에 설정된 라벨 삭제 
라벨 키의 이름에 대시를 추가 하면 됨 
kubectl label nodes node-1 myalbel/disk=hdd-

mylabel/disk 값이 hdd인 노드에 파드를 할당하려면 YAML nodeSelector를 정의 
* nodeselector-nginx.yaml 
apiVersion: v1
kind: Pod
metadata:
  name: nginx-nodeselector
spec:
  nodeSelector:
    mylabel/disk: hdd
  containers:
  - name: nginx
    image: nginx:latest

myalbel/disk=hdd 라벨을 갖는 노드가 2개 라면 둘중 하나에 생성 됨 
적어도 노드의 이름에 종속적이 않게 YAML 파일 작성 가능 

위와 같으 파드 스케줄링 방법은 단일 파드에 대해 수행된다는 점 
아래 처럼 생성시 디플로이먼트의 모든 파드가 동일한 하나의 노드에 할당되는 것은 아니라는 뜻 
* deployment-nginx-node-selector.yaml 
apiVersion: apps/v1
kind: Deployment
metadata:
  name: deployment-nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: deployment-nginx
  template:
    metadata:
      name: deployment-nginx
      labels:
        app: deployment-nginx
    spec:
      nodeSelector:
        mylabel/disk: hdd
      containers:
      - name: deployment-nginx
        image: nginx:latest

# Node Affinity를 이용한 스케줄링 방법 
nodeSelector 에서 좀더 확장된 라벨 선택 기능을 제공 하며 , 반드시 충족해야하는 조건 (Hard), 선호하는 조건(Soft)을 별도로 정의 

Node Affinity 2가지 종류의 옵션
* requiredDuringSchedulingIgnoredDuringExecution ( 반드시 만족해야만 하는 제약 조건 )
* preferredDuringSchedulingIgnoredDuringExecution ( 반드시 만족해야 할 필요는 없으며 해당 조건을 만족하는 노드가 있다면 그 노느를 좀더 선호 하겠다는 조건 )

* nodeaffinity-required.yaml 
apiVersion: v1
kind: Pod
metadata:
  name: nginx-nodeaffinity-required
spec:
  affinity:
    nodeAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
        - matchExpressions:
          - key: mylabel/disk
            operator: In          # values의 값 중 하나만 만족하면 됩니다.
            values:
            - ssd
            - hdd
  containers:
  - name: nginx
    image: nginx:latest

  "operator: In" 항목은  key의 라벨이 values의  값 중 하나를 만족하는 노드에 파드를 스케줄링 한다는 뜻 
  operator 에는 In , NotIn, Exists, DoesNotExist, Gt(값이 큼), Lt(값이 작음) 조건을 사용할 수 있어 nodeSelector보다 다양하게 활용 가능 

* nodeaffinity-preferred.yaml 
apiVersion: v1
kind: Pod
metadata:
  name: nginx-nodeaffinity-preferred
spec:
  affinity:
    nodeAffinity:
      preferredDuringSchedulingIgnoredDuringExecution:
      - weight: 80               # 조건을 만족하는 노드에 1~100까지의 가중치를 부여 (조건에 해당하는 노드를 얼마나 더 선호할 지를 나타내는 가중치)
        preference:
          matchExpressions:
          - key: mylabel/disk
            operator: In
            values:
            - ssd
  containers:
  - name: nginx
    image: nginx:latest

이러한 스케줄링 조건은 파드를 할당할 당시에만 유효 
파드가 할당된 뒤에 노드의 라벨이 변경되더라도 다른 노드로 파드가 옮겨지는 퇴거(Eviction)가 발생 하지는 않음 

# Pod Affinity를 이용한 스케줄링 방법 
 Node Affinity가 특정 조건을 만족하는 노드를 선택하는 방법이라면 Pod Affinity는 특정 조건을 만족하는 파드와 함께 실행 되도록 스케줄링 
 사용법은 Node Affinity와 같음 

 * podaffinity-requird.yaml 
apiVersion: v1
kind: Pod
metadata:
  name: nginx-podaffinity
spec:
  affinity:
    podAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
      - labelSelector:
          matchExpressions:
          - key: mylabel/database
            operator: In
            values:
            - mysql
        topologyKey: failure-domain.beta.kubernetes.io/zone
  containers:
  - name: nginx
    image: nginx:latest

  대부분의 항목은 Node Affinity를 사용했을 때와 같지만 nodeAffinity 대신 podAffinity 항목을 사용했다는 점이 다름 
  위 YAML 파일은 mylabel/database=mysql 이라는 라벨을 가지는 파드와 함께 위치하도록 스케줄링 하라는 뜻 
  이 라베을 가지는 파드와 무조건 같은 노드에 할당 하라는 뜻은 아님 topologyKey 항목은 해당 라벨을 가지는 토플로지 범위의 노드를 선택 한다는 것을 의미 
  대표적인 활용 용도로는 응답 시간을 최대한 줄여야 하는 두 개의 파드를 동일한 가용 영역(AZ : Available Zone) 또는 리전(Region)의 노드에 할당하는 경우 

topologyKey를 호스트 이름으로 설정 - 호스트 이름은 고유하기 때문에 두개 이상의 노드가 존재 할 수 없음 이는 곧 하나의 노드가 하나의 토플로지에 대응 된다는 것을 의미 
따라서 스케줄러는 반드시 matchExpression을 만족하는 파드가 위치한 노드를 선택  
 * podaffinity-hostname-topology.yaml 
apiVersion: v1
kind: Pod
metadata:
  name: nginx-podaffinity-hostname
spec:
  affinity:
    podAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
      - labelSelector:
          matchExpressions:
          - key: mylabel/database
            operator: In
            values:
            - mysql
        topologyKey: kubernetes.io/hostname
  containers:
  - name: nginx
    image: nginx:latest

# Pod Anti-affinity를 이용한 스케줄링 방법 
Pod Affinity와 반대로 동작  - 특정 파드와 같은 토플로지의 노드를 선택하지 않는 방법 
이 원리를 잘 이용하면 고가용성을 보장하기 위해 파드를 여러 가용 영역 또는 리전에 멀리 퍼뜨리는 전략을 세울 수 있음 
Pod Anti-affinity 사용 하는 방법은 이전에 활용한 YAML 에서 podAffinity 를 podAntiAffnity로 변경만 해주면 됨 

 * pod-antiaffinity-requird.yaml 
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod-antiaffinity
spec:
  affinity:
    podAntiAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
      - labelSelector:
          matchExpressions:
          - key: mylabel/database
            operator: In
            values:
            - mysql
        topologyKey: failure-domain.beta.kubernetes.io/zone
  containers:
  - name: nginx
    image: nginx:latest

Pod Affinity와 Anti-affinity는 Node Affinity와 동일하게 소프트 제한을 사용할 수 있음 
requiredDuringSchedulingIgnoredDuringExecution 을 사용하면 토플로지마다 반드시 하나의 파드만 할당하게 되지만
preferredDuringSchedulingIgnoredDuringExecution을 사용하면 각 토플로지의 노드에 파드를 여러 개 할당 가능 

* pod-antiaffinity-preferred.yaml 
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod-antiaffinity-preferred
spec:
  affinity:
    podAntiAffinity:
      preferredDuringSchedulingIgnoredDuringExecution:
      - podAffinityTerm:
          labelSelector:
            matchExpressions:
            - key: mylabel/database
              operator: In
              values:
              - mysql
          topologyKey: failure-domain.beta.kubernetes.io/zone
        weight: 80
  containers:
  - name: nginx
    image: nginx:latest

  이러한 원리를 조금만 더 활용하면 모든 노드에 파드를 하났기 할당하는 마치 데몬셋(DaemonSet)과 비슷한 디플로이먼트 생성할 수 있음 
* deployment-exclusive.yaml 
apiVersion: apps/v1
kind: Deployment
metadata:
  name: deployment-nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: deployment-nginx
  template:
    metadata:
      name: deployment-nginx
      labels:
        app: deployment-nginx
    spec:
      affinity:
        podAntiAffinity:
          requiredDuringSchedulingIgnoredDuringExecution:
            - labelSelector:
               matchExpressions:
                  - key: app
                    operator: In
                    values:
                      - deployment-nginx
              topologyKey: "kubernetes.io/hostname"
      containers:
      - name: deployment-nginx
        image: nginx:latest

디플로이먼트의 각 파드에 설정된 라벨을 podAntiAffinity의 matchExpressions 조건에 다시 사용함으로써 디플로이먼트의 각 파드가 서로 다른 호스트 이름을 가지는 노드에 할당 

# Taints와 Tolerations를 이용한 파드 스케줄링 
Taints라는 이름이 의미하는 것처럼 특정 노드에 얼룩(Taint)을 지정함으로써 해당 노드에 파드가 할당 되는 것을 막는 기능 
하지만 Taints 에 대응 하는 Tolerations를 파드에 설정하면 Taints가 설정된 노드에도 파드를 할당할 수 있음 
노드에 얼룩(Taint)이 졌지만 이를 용인(Tolerations)할 수 있는 파드만 해당 노드에 할당

Taints의 종류는 매우 다양 
Taints를 노드에 별도로 설정할 수도 있고, 특정 이벤트로 인해 쿠버네티스가 자동으로 노드에 Taints를 설정하기도 함 
kubectl 명령어로 직접 노드에 설정하거나 해제할 수 있음  라벨과 비슷하게 키=값 형태로 사용 라벨과 다른 점은 key=value 뒤에 effect 를 추가로 명시 
Taint효과는 Taint가 노드에 설정됐을 때 어떠한 효과를 낼 것인지 결정 
effect는 아래 3가지 종류 
NoSchedule(파드를 스케줄링하지 않음)
NoExecute(파드의 실행 자체를 허용하지 않음)
PreferNoSchedule(가능하면 스케줄링하지 않음)

ex) kubectl taint nodes nodename key=value:effect 
삭제시 라벨과 마찬가지로 - 대시 를 뒤에 붙이면 됨
ex) kubectl tain nodes nodename key:effect- 

* toleration-test.yaml 
apiVersion: v1
kind: Pod
metadata:
  name: nginx-toleration-test
spec:
  tolerations:
  - key: alicek106/my-taint
    value: dirty
    operator: Equal          # alicek106/my-taint 키의 값이 dirty이며 (Equal)
    effect: NoSchedule       # Taint 효과가 NoSchedule인 경우 해당 Taint를 용인합니다.
  containers:
  - name: nginx
    image: nginx:latest

   위의 YAML 파일은 Taint를 용인할 수 있을 뿐 , 해당 Taint가 설정된 노드에 반드시 파드를 할당한다는 의미는 아님 

   쿠버네티스는 기본적으로 다양한 Taint를 노드에 설정함 
   대표적인 예로 마스터 노드에 기본적으로 설정된 Taint  쿠버네티스는 마스터 노드에 Taint를 설정함으로써 파드가 할당되는 것을 방지 
   kubectl describe node <master 노드> 
   Taints:             node-role.kubernetes.io/master:NoSchedule
   Unschedulable:      false

  Unschedulable 의 값이 false로 설정되어 있는데 이는  스케줄링의 대상이 되는 노드라는 것을 의미 
  마스터 노드에 설정된 Taint는 키-값 형태가 아님 Taint는 기본적으로 키-값 형태를 가지지만 값을 생략해 사용 가능 값이 생략된 경우에는 "" 의 값을 가지는 거로 간주 
  마스터 노드에 설정된 Taint 또한 Toleration을 이용해 용인 할 수 있음
  ( 마스터 노드는 핵심 컴포넌트만 실행하는 것이 바람직 - kubectl get pods -n kube-system | grep api )
  
  * toleration-master.yaml 
apiVersion: v1
kind: Pod
metadata:
  name: nginx-master-toleration
spec:
  tolerations:
  - key: node-role.kubernetes.io/master
    effect: NoSchedule
    operator: Equal
    value: ""
  nodeSelector:
    node-role.kubernetes.io/master: ""   # 마스터 노드에서도 파드가 생성되도록 지정합니다.
  containers:
  - name: nginx
    image: nginx:latest

API 서버 파드에는 :NoExecute라는 Toleration이 설정돼 있음  : Taint의 키 와 값이 무엇이든지 상관없이 모든 :NoExecute 종류의 Taint를 용인 할 수 있음을 의미) 
Toleration에서 operator의 값은 Equal 외에도 Exists 사용 할 수 있음  Exists로 설정된 경우에는 Taint에 대한 와일드카드로서 동작 

* 모든 종류의 Taint 용인
  tolerations:
   - operator: Exists

* 키의 이름이 my-key인 모든 Taint에 대해 값에 상관없이 용인 
  tolerations:
   - key : my-key 
    operator: Exists

* 키의 이름이 my-key 이고 , Taint 효과가 NoExecute인 Taint에 대해 값에 상관없이 용인 
  tolerations:
   - key : my-key 
    effect : NoExecute 
    operator: Exists

# NoExecute 와 tolerationSeconds
NoExecute는 파드를 해당 노드에 스케줄링하지 않을 뿐만 아니라 해당 노드에서 아예 파드를 실행 할 수 없도록 설정 
NoSchedule은 노드에 설정하더라도 기존에 실행 중이던 파드는 정상 동작 하는 반면 NoExecute는 해당 노드에서 실행 중인 파드를 종료 시킴  NoExecute에 대한 Toleration이 설정되 있으면 종료 안함 
단 파드가 디플로이먼트나 레플리카셋 등과 같은 리소스로부터 생성됐다면 NoExecute에 의해 파드가 종료됐더라도 파드는 다른 노드로 옮겨가는 퇴거(Eviction) 발생 
파드를 생성하면 쿠버네티스는 자동으로 NoExecute에 대한 Toleration을 추가 함 

  쿠버네티스는 특정 문제가 발생한 노드에 대해서는 자동으로 Taint를 추가 - (NotReady, Unreachable, memory-pressure, disk-pressure 등)                
  특히나 NotReady, Unreachable는 노드 자체에 장애가 생긴 경우일 수 있기 때문에 쿠버네티스는 노드에 아래의 Taint를 추가 
  node.kubenetes.io/not-ready, node.kubenetes.io/unreachable  노드가 준비되지 않았거나 네트워크 통신이 불가능한 상태일 때를 위한 Toleration
  for 300s 값은 not-ready나 unreachable 상태의 Taint가 발생하더라도 300초 동안은 해당 Taint를 용인 하겠다는 뜻 
  300초 이내에 노드가 정상 상태로 돌와와 Taint가 삭제되지 않으면 파드는 다른 노드로 옮겨 가게 됨 
  즉 장애가 생겨도 해당 노드에서 실행 중이던 파드가 즉시 다른 노드로 옮겨가는 것은 아니며 기본적으로 300초 후에 옮겨가게 됨 
  이러한 옵션을 tolerationSeconds 라고 함 - 파드가 실행 중인 노드에 Taint가 추가됐을 때 해당 Taint 를 용인할 수 있는 최대 시간을 의미 

kubectl describe pod <파드이름> 명령어로 확인할 수 있음
Tolerations :  node.kubenetes.io/not-ready:NoExecute for 300s
                      node.kubernetes.io/unreachable:NoExecute for 300s

# cordon을 이용한 스케줄링 비활성화 
cordon : 쿠버네티스에서 제공하는 명시적인 노드에 스케줄링 막는 처리 - 새로운 파드가 할당 되지 않음 
kubectl get nodes 명령어로 노드의 상태를 확인해 보면 STATUS 항목에 SchedulingDisabled 가 추가됨 
노드에 cordon 명령어를 사용하더라도 해당 노드에서 이미 실행 중인 파드가 종료 되지는 않음 

kubectl cordon <노드 이름>
cordon을 해제하려면 uncordon 명령어를 사용
kubectl uncordon <노드 이름> 

# drain 명령어로 노드 비활성화하기 
cordon 처럼 해당 노드에 스케줄링 금지 하는 것은 동일 하지만 노드에서 기존에 실행 중이던 파드를 다른 노드로 Eviction을 수행 
- 커널 버전 업그레이드 , 유지 보수 등의 이유로 인해 잠시 노드를 중지해야 할 때 유용 

kubectl drain <노드 이름>
kubectl drain <노드 이름> --ignore-daemonsets 

디플로이먼트나 레플리카셋 , 잡 , 스테이트플셋 등에 의해 생성되지 않은 파드가 노드에 존재할때 drain 명령어 실패 - 다른 노드로 옮겨가 다시 생성되지 않기 때문
단일 파드를 무시하고 노드를 drain 하려면 --force  옵션을 함께 사용 

# PodDisruptionBudget으로 파드 개수 유지하기 
drain 명령어 실행하면 Eviction 처리 되면서 다른 노드로 옮겨가 파드가 생성 되게 되는데 그 사이 서비스가 중단 되거나 일시적으로 전체 처리 량이 감소 하는 상황이 발생 
이러한 상황에 대처하기 위해 PodDisruptionBudget 이라는 기능을 제공 
Eviction 발생할 때 특정 개수 또는 비율만큼의 파드는 반드시 정상적인 상태를 유지 하기 위해 사용 
kubectl get poddistruptionbudgets or pub 

* simple-pub-example.yaml 
apiVersion: policy/v1beta1
kind: PodDisruptionBudget
metadata:
  name: simple-pdb-example
spec:
maxUnavailable: 1        # 비활성화될 수 있는 포드의 최대 갯수 또는 비율 (%) - drain 수행시 한번에 몇개 까지 동시에 종료 될 것인지 설정 숫자로 표시하거나 %로 설정 가능 
  # minAvailable: 2       # 최소 몇개의 파드가 정상을 유지 할지 설정   maxUnavailable , minAvailable  맥락이 비슷하기 때문에 둘중 하나만 설정해야 함 
  selector:                     # PDB의 대상이 될 파드를 선택하는 라벨 셀렉터
    matchLabels:
      app: webserver

# 커스텀 스케줄러 구현 
1. 기본 스케줄러가 아닌 커스텀 스케줄러로 파드를 스케줄링 하고 싶다면 파드를 생성할때 schedulerName의 값을 별도로 명시 
* custom-scheduled-pod.yaml 
apiVersion: v1
kind: Pod
metadata:
  name: custom-scheduled-pod
spec:
  schedulerName: my-custom-scheduler
  containers:
  - name: nginx-container
    image: nginx

=======================================
2. 스케줄러 직접 구현 - python 작성 예시 
특별한 경우 아니면 기본 스케줄러 사용하는게 바람직 
=======================================
import random
import json
from kubernetes import client, config, watch

# 이 스케줄러가 담당할 스케줄러 이름을 지정합니다.
scheduler_name = "my-custom-scheduler"

# 이 스케줄러가 스케줄링할 포드의 네임스페이스를 지정합니다. 필요에 따라 전역적으로 사용할 수도 있습니다.
namespace_name = "default"

# 포드 내부에 마운트되어 있는 secret을 읽어옵니다.
config.load_incluster_config()
v1 = client.CoreV1Api()


# 테스트를 위해 랜덤하게 노드를 선택합니다. 별도의 스케줄링 알고리즘을 이 함수에서 구현할 수 있습니다.
def select_node():
    available_nodes = []
    for node in v1.list_node().items:
        for status in node.status.conditions:
            if status.status == "True" and status.type == "Ready":
                available_nodes.append(node.metadata.name)

    selected_node = random.choice(available_nodes)
    return selected_node


# 포드를 특정 노드에 바인딩합니다.
def schedule_pod(pod_name, node_name):
    body = client.V1Binding(
        target=client.V1ObjectReference(
            kind="Node",
            api_version="v1",
            name=node_name
        ),
        metadata=client.V1ObjectMeta(
            name=pod_name
        )
    )

    # From issue https://github.com/kubernetes-client/python/issues/547
    try:
        v1.create_namespaced_binding(namespace=namespace_name, body=body)
    except ValueError:
        pass

    print("Scheduled {} into {}".format(pod_name, node_name))

if __name__ == '__main__':
    # API 서버로부터 Watch를 생성합니다.
    w = watch.Watch()

    # Watch로부터 데이터가 들어오면 스케줄링을 실행합니다.
    for event in w.stream(v1.list_namespaced_pod, namespace_name):
        if event['object'].status.phase == "Pending" and event['object'].spec.scheduler_name == scheduler_name:
            try:
                # 적절한 노드를 선택합니다.
                selected_node = select_node()

                # 포드를 해당 노드에 스케줄링합니다.
                result = schedule_pod(event['object'].metadata.name, selected_node)
            except Exception as e:
                print(json.loads(e.body)['message'])    
=======================================

# 쿠버네티스 애플리케이션 상태와 배포 
kubectl apply -f  

고도화된 배포 방식 
Spinnaker , Helm, Kustomize , ArgoCD, Jenkins 지속적인 패포 도구 (Continuous Delivery)

쿠버네티스는 애플리케이션을 안정적으로 배포할 수 있도록 몇가지 기능을 제공 
- 새로운 버전의 애플리케이션이 점진적으로 배포될 수 있도록 디플로이먼트 롤링 업데이트 
- Revision 
- 새롭게 배포되는 파드의 애플리케이션이 사용자의 요청을 처리할 준비가 됐는지 확인 , 삭제될 파드가 애플리케이션을 우아하게 종료 

# 디플로이먼트를 이용한 레플리카셋의 버전 관리 
- 레플리카셋의 변경 사항을 저장하는 리비전을 디플로이먼트에서 관리 함으로써 애플리케이션의 배포를 용이 
--record 옵션을 추가해 디플로이먼트의 변경 사항을 적용 히스토리에 기록됨 이런 리비전을 이용해 언제든지 롤백 가능 
기본적으로 레플리카셋의 리비전은 10개까지만 히스토리에 저장 필요시 디플로이먼트 생성할때 revisionHistoryLimit 이라는 항목을 직접 설정 가능 

* deployment-history-limit.yaml 
apiVersion: apps/v1
kind: Deployment
metadata:
  name: deployment-history-limit
spec:
  revisionHistoryLimit: 3
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      name: nginx
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.17
        ports:
        - containerPort: 80

  # 디플로이먼트를 통한 롤링 업데이트 설정 
  일시적으로 사용자의 요청을 처리하지 못해도 괜찮은 애플리케이션이라면 쿠버네티스에서 제공하는 ReCreate 방법 사용 
  - 기존의 파드를 모두 삭제 한뒤, 새로운 버전의 파드를 생성하는 방식 
  
   이러한 배포 전략은 디플로이먼트 YAML 파일에 있는 strategy 의 type항목에서 설정 

* deployment-recreate-v1.yaml 
apiVersion: apps/v1
kind: Deployment
metadata:
  name: deployment-recreate
spec:
  replicas: 3
  strategy:
    type: Recreate
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      name: nginx
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.15
        ports:
        - containerPort: 80

파드를 조금씩 삭제하고 생성하는 롤링 업데이트 기능 제공 
- YAML 파일에서 별도의 설정을 하지 않아도 디플로이먼트의 버전을 업데이트할 때는 기본적으로 롤링 업데이트를 사용 하도록 설정 되어 있음 
롤링 업데이트 도중에 기존 버전의 파드를 몇 개씩 삭제할 것인지 , 새로운 버전의 파드는 몇개씩 생성할 것인지 직접 설정 가능 
strategy 의 type 항목을 RollingUpdate 로 설정 

* deployment-rolling-update.yaml 
apiVersion: apps/v1
kind: Deployment
metadata:
  name: deployment-rolling-update
spec:
  replicas: 3
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 2
      maxUnavailable: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      name: nginx
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.15
        ports:
        - containerPort: 80

maxSurge, maxUnavailable 설정 값은 숫자나 비율%로 설정 가능 - 비율로 설정할 시 maxSurge의 소수점 값은 반올림 maxUnavailable 소수점 값은 버림 처리 됨  두 옵션 모두 기본값은 25%
maxUnavailable : 사용 불가능한 상태가 되는 파드의 최대 개수를 설정 
maxSurge : 전체 파드의 개수가 디플로이먼트의 replicas 값보다 얼마나 더 많이 존재할 수 있는지 설정 

* rolling-update-example-v1.yaml 
apiVersion: apps/v1
kind: Deployment
metadata:
  name: deployment-rolling-update
spec:
  replicas: 4
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 2
      maxUnavailable: 1
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      name: nginx
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.15
        ports:
        - containerPort: 80

* rolling-update-example-v2.yaml 
apiVersion: apps/v1
kind: Deployment
metadata:
  name: deployment-rolling-update
spec:
  replicas: 4
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 2
      maxUnavailable: 1
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      name: nginx
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.16
        ports:
        - containerPort: 80

maxUnavailable의 값을 0으로 설정하면 롤링 업데이트 도중 전체 파드 개수는 적어도 replicas의 개수 만큼은 유지  
이때 maxSurge 값도 0으로 함께 설정해 버리면 전체 파드 개수의 상한선과 하한선이 같아져 버리기 때문에 새로운 버전의 파드 생성이 안됨 롤링 업데이트 진행 안됨 
롤링 업데이트 시에는 구버젼 , 신규 버젼 애플리케이션이 공존 할수 있음 

# 블루 그린 배포 사용하기 
기존 버전의 파드를 그대로 둔 상태에서 새로운 버젼의 파드를 미리 생성해 둔 뒤 서비스의 라우팅만 변경하는 배포 방식 
특정 순간에 두 버전의 애플리케이션이 공존 하지 않으며 , Recreate 전략 처럼 중단도 발생하지 않는 다는 장점 
쿠버네티스가 자체적으로 지원하는 방식은 아님 

1.  기존 버전(v1)의 디플로이먼특 생성돼 있으면 서비스는 사용자 요청을 v1 파드로 전달
2. 새로운 버전(v2)의 디플로이먼트를 생성 
3. 서비스의 라벨을 변경함으로써 서비스를 통한 요청이 새로운 버전의 디플로이먼트로 전달되도록 수정
4. 새로운 버전의 디플로이먼트가 잘 동작하는 것을 확인했다면 기존 버전의 디플로이먼트 삭제 

블루그린 배포를 사용하면 특정 순간에는 디플로이먼트에 설정된 replicas 개수의 두배에 해당하는 파드가 실행 되기 때문에 일시적으로 전체 자원을 많이 소모 

# 파드의 생애 주기
kubectl get pods 
출력되는  STATUS 항목
* Pending : 파드를 생성하는 요청이 API 서버에 의해 승인됐지만 , 문제로 인해 아직 실제로 생성되지 않은 상태 
* Running : 파드에 포함된 컨테이너들이 모두 생성돼 파드가 정상적으로 실행된 상태 
* Completed : 파드가 정상적으로 실행돼 종료됐음을 의미 - 컨테이너의 init 프로세스가 종료 코드로서 0 코드를 반환  
* Error : 파드가 정상적으로 실행되지 않은 상태로 종료됐음을 의미  -컨테이너의 init 프로세스가 종료 코드로서 0이 아닌 종료 코드를 반환  
* Terminating : 파드가 삭제 또는 Eviction 되기 위해 삭제 상태에 머물러 있는 경우에 해당 

Completed 상태가 되는 파드 생성 - 생성 후 10초후 종료되나 restartPolicy 정책에 의해 다시 재시작 됨 
restartPolicy 정책 종류 
Always - 파드가 종료되면 재시작 
Naver - 파드가 종료되면 다시 시작 하지 않음
OnFailure  - 파드의 컨테이너가 실패했을 때 0이 아닌 종료 코드를 반환했을 때만 다시 재시작 

* completed-pod.yaml 
apiVersion: v1
kind: Pod
metadata:
  name: completed-pod-example
spec:
  containers:
  - name: completed-pod-example
    image: busybox
    command: ["sh"]
    args: ["-c", "sleep 10 && exit 0"]  

* completed-pod-restart-never.yaml 
apiVersion: v1
kind: Pod
metadata:
  name: completed-pod-restart-never
spec:
  restartPolicy: Never
  containers:
  - name: completed-pod-restart-never
    image: busybox
    command: ["sh"]
    args: ["-c", "sleep 10 && exit 0"]

* error-pod-restart-never.yaml 
apiVersion: v1
kind: Pod
metadata:
  name: error-pod-restart-never
spec:
  restartPolicy: Never
  containers:
  - name: error-pod-restart-never
    image: busybox
    command: ["sh"]
    args: ["-c", "sleep 10 && exit 1"]

kubectl apply -f  
kubectl get pod --watch 
kubectl get pod 파드명 -o yaml | grep restartPolicy 
  restartPolicy : Always  

파드가 종료될 때마다 즉시 재시작 하는 것은 아님 
파드가 재시작 하는 과정을 보면 CrashLoopBackOff라는 상태가 보밈 
쿠버네티스는 어떠한 작업이 잘못돼 실패 했을때 일정 간격을 두고 해당 작업을 재 시도 
실패하는 횟수가 늘어날수록 재시도 하는 간격이 지수 형태로 증가  , 그 중간 상태가 바로 CrashLoopBackOff 상태 

# Running 상태가 되기 위한 조건 
파드를 생성했다고 해서 무조건 Running 상태가 되는 것은 아닐 뿐더라 파드가 Running 상태에 머물러 있다고 해서 컨테이너 내부이 애플리케이션이 정상 동작하고 있을 것이라는 보장은 없음 
이를 위해 쿠버네티스는 다음과 같은 기능을 제공 
* Init Container 
* postStart
* livenessProbe, readinessProbe 

1) Init Container 
Inint Container는 파드의 컨테이너 내부에서 애플리케이션이 실행되기 전에 초기화를 수행하는 컨테이너 
파드의 애플리케이션 컨테이너보다 먼저 실행 됨 - 파드의 애플리케이션 컨테이너가 실행되기 전에 특정 작업을 수행하는 용도로 사용 가능 
1개 이상의  Init 컨테이너를 정의한 경우 순서대로 실행 
*  init-container-example.yaml 
apiVersion: v1
kind: Pod
metadata:
  name: init-container-example
spec:
  initContainers: # 초기화 컨테이너를 이 항목에 정의합니다.
  - name: my-init-container
    image: busybox
    command: ["sh", "-c", "echo Hello World!"]
  containers: # 애플리케이션 컨테이너를 이 항목에 정의합니다.
  - name: nginx
    image: nginx

Init 컨테이너가 하나라도 실패하게 된다면 파드의 애플리케이션 컨테이너는 실행되지 않음 파드의 restartPolicy 에 따라서 Init 컨테이너가 다시 재시작 
이러한 성질을 이용해 Init 컨테이너 내부에서 dig나 nslookup 명령어 등을 이용해 다른 디플로이먼트가 생성되기를 기다리거나 , 애플리케이션 컨테이너가 사용할 설정 파일등을 미리 준비 가능 

다른 서비스 또는 디플로이먼트가 생성될 때가지 Init 컨테이너에서 대기하는 예시 
* init-container-usecase.yaml 
apiVersion: v1
kind: Pod
metadata:
  name: init-container-usecase
spec:
  containers:
  - name: nginx
    image: nginx
  initContainers:
  - name: wait-other-service
    image: busybox
    command: ['sh', '-c', 'until nslookup myservice; do echo waiting..; sleep 1; done;'] 

Init 컨테이너 로그는 kubectl logs <파드 이름> -c <컨테이너 이름> 으로 확인 

2) postStart 
파드의 컨테이너가 실행되거나 삭제될 때 , 특정 작업을 수행하도록 라이프사이클 훅(Hook)을 YAML 파일에 정의 할 수 있음 
Hook에는 두가지 종류 시작시 실행 되는 postStart 종료시 실행되는 preStop 

postStart는 두가지 방식으로 사용할 수 있음 
* HTTP : 컨테이너가 시작한 직후, 특정 주소로 HTTP 요청을 전송 
* Exed : 컨테이너가 시작한 직후, 컨테이너 내부에서 특정 명령어를 실행 

* poststart-hook.yaml 
apiVersion: v1
kind: Pod
metadata:
  name: poststart-hook
spec:
  containers:
  - name: poststart-hook
    image: nginx
    lifecycle:
      postStart:
        exec:
          command: ["sh", "-c", "touch /myfile"]

postStart 의 명령어나 HTTP  요청이 제대로 실행되지 않으면 컨테이너는 Running  상태로 전환 되지 않으며  restartPolicy에 의해 재시작 
postStart 에 의한 실행 로그는 에러가 발생하지 않는 한 별도로 확인 불가 

3)  livenessProbe, readinessProbe , startupProbe - 애플리케이션 상태 검사 
Init Container , postStart 훅이 정상적으로 실행됐다고 해서 애플리케이션이 제대로 동작하고 있다는 보장은 없음 
쿠버네티스에서는 애플리케이션이 사용자의 요청을 처리할 수 있는 상태인지를 판별 하기 위해 
livenessProbe, readinessProbe , startupProbe  세가지 방법을 제공  - Running 상태가 되기 위한 필수 조건은 아니지만 파드 내부의 애플리케이션의 상태를 확인하기 위해 사용 

livenessProbe : 컨테이너 내부의 애플리케이션이 살아 있는지 검사 , 실패할 경우 해당 컨테이너는 restartPolicy에 따라 재시작 됨 
readinessProbe : 컨테이너 내부의 애플리케이션이 사용자 요청을 처리할 준비가 됐는지 검사 , 실패할 경우 컨테이너는 서비스의 라우팅 대상에서 제외 
startupProbe: 애플리케이션이 시작될때 수행되는 초기화 작업 등이 완료되었는지 확인 startupProbe  검사에 성공해야 livenessProbe, readinessProbe 가 시작 , 실패할 경우 해당 컨테이너는 restartPolicy에 따라 재시작 됨 

3가지 방법중 하나로 검사 
* httpGet : HTTP 요청을 전송해 상태 검사, 요청 코드가 200, 300 계열이 아닌 경우 검사 실패 한것으로 간주 요청을 보낼 포트와 경로 헤더 HTTPS 사용 여부 등 추가 설정 가능 
* exec : 컨테이너 내부에서 명령어를 실행해 상태 검사 명령어의 종료 코드가 0이 아닌 경우 검사 살패 로 간주 
* tcpSocket : TCP 연결이 수립될수 있는지 체크 , 연결이 생성될 수 없는 경우에 실패로 간주  

* livenessProbe로 애플리케이션 상태 검사 
* livenessprobe-pod.yaml 
apiVersion: v1
kind: Pod
metadata:
  name: livenessprobe-pod
spec:
  containers:
  - name: livenessprobe-pod
    image: nginx
    livenessProbe:  # 이 컨테이너에 대해 livenessProbe를 정의합니다.
      httpGet:      # HTTP 요청을 통해 애플리케이션의 상태를 검사합니다.
        port: 80    # <포드의 IP>:80/ 경로를 통해 헬스 체크 요청을 보냅니다.
        path: /

* readinessProbe로 애플리케이션 상태 검사 
* readlinessprobe-pod-svc.yaml 
apiVersion: v1
kind: Pod
metadata:
  name: readinessprobe-pod
  labels:
    my-readinessprobe: test
spec:
  containers:
  - name: readinessprobe-pod
    image: nginx       # Nginx 서버 컨테이너를 생성합니다.
    readinessProbe:    # <포드의 IP>:80/ 로 상태 검사 요청을 전송합니다.
      httpGet:
        port: 80
        path: /
---
apiVersion: v1
kind: Service
metadata:
  name: readinessprobe-svc
spec:
  ports:
    - name: nginx
      port: 80
      targetPort: 80
  selector:
    my-readinessprobe: test
  type: ClusterIP

  애플리케이션에 readinessProbe를 적용하기 어렵거나 초기화 시간이 어느정도 필요한 경우에는 디플로이먼트에서 minRedySeconds를 사용 최소 대기 시간을 의미 

  * livenessProbe, readinessProbe 세부 옵션
  - periodSeconds : 상태 검사를 진행할 주기를 설정 기본값은 10초 
  - initialDelaySeconds : 파드가 생성된 뒤 상태 검사를 시작할 때까지의 대기 시간을 설정 기본적으로 설정되 있지 않음 
  - timeoutSeconds : 요청에 대한 타임 아웃 시간을 설정 기본값 1초 
  - successThreshold: 상태 검사를 성공했다고 간주할 검사 성공 횟수를 설정 기본값 1
  - failureThreshold : 상태 검사를 실패했다고 간주할 검사 실패 횟수를 설정 기본값 3 

  * probe-options.yaml 
apiVersion: v1
kind: Pod
metadata:
  name: probe-options-example
  labels:
    my-readinessprobe: test
spec:
  containers:
  - name: probe-options-example
    image: nginx
    readinessProbe:
      httpGet:
        port: 80
        path: /
      periodSeconds: 5
      initialDelaySeconds: 10
      timeoutSeconds: 1
      successThreshold: 1
      failureThreshold: 3

# Terminating 상태와 애플리케이션 종료 
kubectl delete 명령어로 파드 삭제 시 진행 프로세스 
1.  리소스가 삭제될 예정이라는 의미의 deletionTimestamp 값이 파드의 데이터에 추가 되고 파드는 Terminating 상태로 바뀜 
2. 아래 3가지 작업이 동시이 진행
   2.1 파드에 preStop  라이프 사이클 훅이 설정돼 있다면 preStop이 실행
   2.2 파드가 레프리카셋으로부터 생성된 경우 해당 파드는 레플리카셋의 관리 영역에서 해제 레플리카셋은 새로운 파드를 생성하려고 시도 
   2.3 파드가 서비스 리소스의 라우팅 대상에서 제외 
3. preStop 훅이 완료되면 리눅스 시그널 중 SIGTERM 이 파드의 컨테이너에 전달 컨테이너의 Init 프로세스는 SIGTERM 수신한 뒤 종료돼야 함 
4. 특정 유예 기간이 지나도 컨테이너 내부의 프로세스가 여전히 종료되지 않으면 프로세스로 SIGKILL 시그널이 전달 
    유예 기간은 기본적으로 30초 , 파드의 terminationGracePeriodSenconds 항목을 통해 설정 가능 

* prestop-hook.yaml 
apiVersion: v1
kind: Pod
metadata:
  name: prestop-hook
spec:
  containers:
  - name: prestop-hook
    image: nginx
    lifecycle:
      preStop:
        exec:
          command: ["/usr/sbin/nginx","-s","quit"]

* termination-grace-period-seconds.yaml 
apiVersion: v1
kind: Pod
metadata:
  name: termination-grace-period-seconds
spec:
  terminationGracePeriodSeconds: 10
  containers:
  - name: termination-grace-period-seconds
    image: nginx
    lifecycle:
      preStop:
        exec:
          command: ["/usr/sbin/nginx","-s","quit"]

# HPA를 활용한 오토스케일링 
쿠버네티스에서는 리소스 사용량에 따라 디플로이먼트의 파드 개수를 자동으로 조절하는 HPA(Horizontal Pod Autoscaler) 라는 기능 제공 
내장되어 있는 기능이긴 하지만 metrics-server라고 하는 별도의 리소스 메트릭 수집 도구를 설치해야만 오토스케일링 기능을 정상적으로 사용 가능

* simple-hpa.yaml 
apiVersion: autoscaling/v1
kind: HorizontalPodAutoscaler
metadata:
  name: simple-hpa
spec: 
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: hostname-deployment       #  simple-deployment의 자원 사용량에서 
 targetCPUUtilizationPercentage: 50 # CPU 활용률이 50% 이상인 경우 
 maxReplicas: 5                                  # 파드를 최대 5개까지 늘림
 minReplicas: 1                                   # 또는 최소 1개까지 줄일수 있음 

########################################################
##  커스텀 리소스와 컨트롤러 
직접 리소스의 종류를 정의해 사용 가능 이를 커스텀 리소스(Custom Resource) 라고 함 

# 쿠버네티스 컨트롤러의 개념과 동작 방식 
명령형 (Imperative) vs. 선언형(Declarative)
docker run 처럼 특정 명령을 처리하는 주체와 통신해 그 작업을 수행하고 그 결과 값을 돌려 받는 방식을 쿠버네티스에서는 명령형 (Imperative)  이라고 함 
쿠버네티스는 이와 반대로  선언형(Declarative) 방식을 지향  kubectl apply  명령어가 선언형 방식의 대표적인 예 

# 커스텀 리소스에 대한 개념 

# 커스텀 리소스를 정의하기 위한 CRD(Custom Resource Definition)
 customresourcedefinition  이라는 오브젝트를 통해 정의 
 kubectl get crd 

 * my-crd-example.yaml
 apiVersion: apiextensions.k8s.io/v1beta1
kind: CustomResourceDefinition
metadata:
  name: alices.k106.com  # 1. CRD의 이름
spec:
  group: k106.com      # 2. 커스텀 리소스의 API 그룹
  version: v1alpha1     #    커스텀 리소스의 API 버전
  scope: Namespaced   #    커스텀 리소스가 네임스페이스에 속하는지 여부
  names:
    plural: alices        # 3. 커스텀 리소스의 이름 (복수형)
    singular: alice      #    커스텀 리소스의 이름 (단수형)
    kind: Alice         #    YAML 파일 등에서 사용될 커스텀 리소스의 Kind
    shortNames: ["ac"] #    커스텀 리소스 이름의 줄임말
  validation:
    openAPIV3Schema:    # 4. 커스텀 리소스의 데이터를 정의
      required: ["spec"]   #   커스텀 리소스에는 반드시 "spec" 이 존재해야 함.
      properties:         #    커스텀 리소스에 저장될 데이터 형식을 정의
        spec:
          required: ["myvalue"]
          properties:
            myvalue:
              type: "string"
              minimum: 1

 * my-crd-example-k8s-latest.yaml 
apiVersion: apiextensions.k8s.io/v1
kind: CustomResourceDefinition
metadata:
  name: alices.k106.com      # 1. CRD의 이름 - 반드시 spec.names.plural +"."+spec.group 형태 
spec:
  group: k106.com               # 2. 커스텀 리소스의 API 그룹
  scope: Namespaced          #    커스텀 리소스가 네임스페이스에 속하는지 여부
  names:
    plural: alices            # 3. 커스텀 리소스의 이름 (복수형)
    singular: alice          #    커스텀 리소스의 이름 (단수형)
    kind: Alice               #    YAML 파일 등에서 사용될 커스텀 리소스의 Kind
    shortNames: ["ac"]       #    커스텀 리소스 이름의 줄임말
  versions:
  - name: v1alpha1           #    커스텀 리소스의 API 버전
    served: true
    storage: true
    schema:
      openAPIV3Schema:       # 4. 커스텀 리소스의 데이터를 정의
        type: object
        required: ["spec"]   # 커스텀 리소스에는 반드시 "spec"이 존재해야 함
        properties:          # 커스텀 리소스에 저장될 데이터 형식을 정의
          spec:
            required: ["myvalue"]
            type: object
            properties:
              myvalue:
                type: "string"
                minimum: 1

kubectl apply -f my-crd-example.yaml 
kubectl get crds 

* my-cr-example.yaml 
apiVersion: k106.com/v1alpha1
kind: Alice
metadata:
  name: my-custom-resource
spec:
  myvalue: "This is my value"

kubectl apply -f my-cr-example.yaml 
kubectl get alices
kubectl get ac
kubectl describe ac my-custom-resource 

# 커스텀 리소스와 컨트롤러 
CRD로부터 커스텀 리소스를 생성했다고 하더라도 이것만으로는 큰 의미를 갖지 않음 
커스텀 리소스 그 자체는 etcd에 저장된 단순한 데이타일 뿐  실제로 동작하고 있는 파드나 서비스는 아님 
커스텀 리소스를 생성했ㅇㄹ 때 특정 동작을 수행하도록 정의하는 컨트롤러를 별도로 구현해야만 커스텀 리소스가 비로서 의미를 가짐 
컨트롤러를 개발할 수 있도록 도와주는 Operator SDK 나 KubeBuilder 와 같은 다양한 프레임워크 제공됨 

########################################################
##  파드를 사용하는 다른 오브젝트들

# Job
특정 동작을 수행하고 종료해야 하는 작업을 위한 오브젝트 
- 디플로이먼트와 같지만 잡에서 원하는 최종 상태는 특정개수의 파드가 실행 중인 것이 아닌 파드가 실행되어 정상적으로 종료되는 것 점에서 차이 
   잡에서는 파드의 컨테이너가 종료 코드로서 0을 반환해 Completed 상태가 되는 것을 목표 
잡에서 생성된 파드는 항상 실행 중인 것을 목료포 하지 않기 때문에 잡오브젝트를 어디에 사용할 지 의문 
사용자의 요청을 처리하는 서버와 같은 애플리케이션 관점이 아닌 한번 수행하고 종료되는 배치 작업을 위한 관점에서 보면 사용성 있음 
잡의 파드가 실패함녀 파드가 restartPolicy에 따라 재시작될 수도 있어서 잡이 처리하는 작업은 멱등성을 가지는 것이 좋음 

* job-hello-world.yaml 
apiVersion: batch/v1
kind: Job
metadata:
  name: job-hello-world
spec:
  template:
    spec:
      restartPolicy: Never
      containers:
      - image: busybox
        args: ["sh", "-c", "echo Hello, World && exit 0"]
        name: job-hello-world

# 잡의 세부 옵션 
* spec.completions : 잡이 성공했다고 여겨지려면 몇 개의 파드가 성공해야 하는지(정상적으로 종료) 설정 기본값은 1
* spec.parallelism : 동시에 생성될 파드의 개수를 설정 기본값은 1

* job-completions.yaml 
apiVersion: batch/v1
kind: Job
metadata:
  name: job-completions
spec:
  completions: 3
  template:
    spec:
      restartPolicy: Never
      containers:
      - image: busybox
        args: ["sh", "-c", "echo Hello, World && exit 0"]
        name: job-completions

잡의 파드가 실패한다면 restartPolicy에 따라 파드가 다시 재시작 되거나(OnFailure) , 새로운 파드를 다시 생성해 똑같은 작업을 다시 시도(Never)
파드가 실패하면 기본적으로는 최대 6번을 다시 시도 - 최대 재시도 횟수는 spec.backoffLimit 값에 별도로 설정 가능 

* job-parallelism.yaml 
apiVersion: batch/v1
kind: Job
metadata:
  name: job-parallelism
spec:
  parallelism: 3
  template:
    spec:
      restartPolicy: Never
      containers:
      - image: busybox
        args: ["sh", "-c", "echo Hello, World && exit 0"]
        name: job-parallelism
        
spec.completion  과 spec.parallelism을 함께 사용하면 잡의 수행 속도를 조절 할 수 있음 

# CronJobs로 잡을 주기적으로 실행하기 
CronJob은 잡을 주기저그로 실행하는 쿠버네티스 오브젝트 
특정 시간 간격으로 잡을 반복으로 실행할 수 있기 때문에 데이터 백업이나 이메일 전송 등의 용도에 적합 
리눅스에서 쓰이는 Cron 스케줄 방법을 그대로 사용 

* cronjob-example-k8s-latest.yaml 
apiVersion: batch/v1
kind: CronJob
metadata:
  name: cronjob-example
spec:
  schedule: "*/1 * * * *"        # Job의 실행 주기
  jobTemplate:                 # 실행될 Job의 설정 내용 (spec)
    spec:
      template:
        spec:
          restartPolicy: Never
          containers:
          - name: cronjob-example
            image: busybox
            args: ["sh", "-c", "date"]

기본적으로 성공한 잡의 기록은 최대 3개 , 실패한 잡의 기록은 최대 1개 까지만 기록 하도록 설정 되어 있음
이 값은 YAML 파일에서 각각 spec.successfulJobsHistoryLimit 및 spec,failedJobsHistoryLimit 값으로 설정 변경 가능 

# DaemonSets 
모든 노드에 동일한 파드를 하나씩 생성하는 오브젝트 
로깅, 모니터링, 네트워킹 등을 위한 에이전트를 각 노드에 생성해야 할 때 유용 

* daemonset-example.yaml 
apiVersion: apps/v1
kind: DaemonSet                           # [1]
metadata:
  name: daemonset-example
spec:
  selector:
    matchLabels:
      name: my-daemonset-example         # [2.1] 포드를 생성하기 위한 셀렉터 설정
  template:
    metadata:                              # [2.2] 포드 라벨 설정
      labels:
        name: my-daemonset-example
    spec:
      tolerations:                           # [3] 마스터 노드에도 포드를 생성
      - key: node-role.kubernetes.io/master
        effect: NoSchedule
      containers:
      - name: daemonset-example
        image: busybox                      # 테스트를 위해 busybox 이미지 사용
        args: ["tail", "-f", "/dev/null"]
        resources:                           # [4] 자원 할당량을 제한
          limits:
            cpu: 100m
            memory: 200Mi

 데몬셋의 목적은 노드마다 파드를 하나씩 생성하는 것이기 때문에 노드에 장애가 발생했을 때에도 파드가 다른 노드로 Eviction 되지 않아야 함
 - 이를 위해서 데몬셋의 파드에는 다양한 Toleration이 기본적으로 설정돼 있음 

 # StatefulSets 
상태를 갖는 파드를 관리 하기 위한 오브젝트 

* statefulset-example.yaml 
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: statefulset-example
spec:
  serviceName: statefulset-service
  selector:
    matchLabels:
      name: statefulset-example
  replicas: 3
  template:
    metadata:
      labels:
        name: statefulset-example
    spec:
      containers:
      - name: statefulset-example
        image: alicek106/rr-test:echo-hostname
        ports:
        - containerPort: 80
          name: web
---
apiVersion: v1
kind: Service
metadata:
  name: statefulset-service
spec:
  ports:
    - port: 80
      name: web
  clusterIP: None
  selector:
    name: statefulset-example

kubectl apply -f statefulset-example.yaml
kubectl get statefulset or sts 
kubectl get pods 
디플로이먼트에서 생성된 파드는 랜덤한 이름이 붙여지지만 스테이트풀셋으로 부터 생성된 파드들 이름에는 0, 1, 2...  처럼 숫자가 붙어 있음 
스테이트플셋에서는 이처럼 파드 이름에 붙여지는 숫자를 통해 각 파드를 고유하게 식별 

스테이트풀셋의 각 파드는 고유하게 식별돼야 하며 파드에 접근할 때에도 랜덤한 파드가 아닌 개별 파드에 접근해야 함 
이러한 경우 일반적인 서비스가 아닌 헤드리스 서비스(Headless Service) 를 사용할 수 있음
헤드리스 서비스는 서비스의 이름으로 파드의 접근 위치를 알아내기 위해서 사용 되면 서비스의 이름과 파드의 이름을 통해서 파드에 접근 할 수 있음 
clusterIP 항목이 None으로 돼있는데 이것이 헤드리스 서비스라는 것을 의미 

스테이드풀셋에서 replicas 값을 여러 개로 설정해 생성할 경우 기본적으로 0번 파드부터 차례대로 생성 되며 이전 번호의 파드가 완전히 
준비돼야만 다음 번호의 파드가 생성됨 - 이 설정은 YAML  파일의 spec.podManagementPolicy  항목에서 변경 가능 

# 스테이트풀셋과 퍼시스턴트 볼륨 
쿠버네티스는 스테이트풀렛을 생성할 때 파드마다 퍼시스턴트 볼륨 클레임을 자동으로 생성함 - 다이나믹 프로비저닝 기능을 사용할 수 있게 지원 

* statefulset-volume.yaml 
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: statefulset-volume
spec:
  serviceName: statefulset-volume-service
  selector:
    matchLabels:
      name: statefulset-volume-example
  replicas: 3
  template:
    metadata:
      labels:
        name: statefulset-volume-example
    spec:
      containers:
      - name: statefulset-volume-example
        image: alicek106/rr-test:echo-hostname
        ports:
        - containerPort: 80
          name: web
        volumeMounts:
        - name: webserver-files
          mountPath: /var/www/html/
  volumeClaimTemplates:
  - metadata:
      name: webserver-files
    spec:
      accessModes: ["ReadWriteOnce"]
      storageClassName: generic
      resources:
        requests:
          storage: 1Gi
---
apiVersion: v1
kind: Service
metadata:
  name: statefulset-volume-service
spec:
  ports:
    - port: 80
      name: web
  clusterIP: None
  selector:
    name: statefulset-volume-example

########################################################
##  쿠버네티스 모니터링 

Prometheus  : 성능, 사용성 및 다른 도구와의 호환성 등 여러 측면에서 우수하다고 평가되는 시계열 데이타베이스 
Grafana : 데이타베이스에 수집된 데이터를 시각화 
AlertManager  : 슬랙 알림 전송 

유료 모니터링 시스템 :  Datadog, New Relic , AWS CloudWatch 

# 모니터링 기본 구조 
CAdvisor 컨테이너에 관련된 모니터링 데이터를 확인할 수 있는 모니터링 도구 
- 웹 UI에서는 단기간의 매트릭만 제공

프로메테우스와 연동 
1. CAdvisor /meterics 경로로 컨테이너 매트릭을 요청 
2. 프로메테우스 형식의 시계열 매트릭을 반환 
3. CAdvisor로부 터 수집된 매트릭을 저장 

/metrics 경로를 외부에 노출시켜 데이터를 수집할 수 있도록 인터페이스를 제공하는 서버를 일반적으로 exporter 라고 함 
대부분의 오픈소스에서는 매트릭을 반환하기 위한 엔드포인트 경로로 /metrics를 기준으로 함 

# 모니터링 매트릭의 분류 
* 인프라 수준의 매트릭 : 호스트 레벨에서의 매트릭을 의미 - 호스트에서 사용중인 파일 디스크립터의 개수, 디스크 사용량, 호스트  NIC  패킷 전송량 등 (node-pxporter 라는 도구가 제공하는 매트릭 수준)
* 컨테이너 수준의 매트릭 : 컨테이너 레벨에서의 매트릭을 의미 - 컨테이너별 CPU와 메모리 사용량, 프로세스상태, 리소스 할당량, 파드의 상태 등 (CAdvisor가 제공하는 매트릭 수준)
* 애플리케이션 수준의 매트릭 : 애플리케이션 레벨에서 정의하는 모든 매트릭을 의미 - 서버 플레임워크에서 제공하는 모니터링 데이타등 

모니터링 시스템을 구축한 뒤 다루게 될 데이터는 대부분 인프라 또는 컨테이너 수준의 모니터링 데이터 
CAdvisor가 제공하는 컨테이너 수준의 모니터링에 속하지만 인프라 수준의 모니터링 데이터도 일부 제공 
인프라 수준에서의 매트릭을 제공하는 node-exporter 라는 도구 
애플리케이션 수준에서의 매트릭을 제공하는 프레임워크 또는 exporter 라이브러리도 있음 

# 쿠버네티스 모니터링 기초 

* metrics-server
쿠버네티스에서 자체적으로 모니터링 기능을 제공하지는 않지만 매트릭을 수집해 사용할 수 있도록 몇 가지 애드온을 제공 
그 중 가장 기초적인 것은 컨테이너와 인프라 레벨에서의 매트릭을 수집하는 metrics-server 라는 도구 
metrics-server 를 설치하면 파드의 오토스케일링, 사용중인 리소스 확인 등 여러 기능을 추가적으로 사용할 수 있음으로 가능하다면 설치 할 것을 권장 

kubectl top pod 
쿠버네티스는 여러 개의 노드로 구성돼 있기 때문에 쉡게 매트릭을 확인할 수는 없음 
클러스터 내부의 매트릭을 모아서 제공하는 별도의 무어인가가 필요  metrics-server 가 바로 그역활을 담당 

### book 내용 참고 ###
# metrics-server 설치 
# metrics-server 동작 원리 : APIServices 리소스 
# kube-state-metrics 
# node-exporter 
# 프로메테우슬르 활용한 메트릭 수집 
# 그라파나로 프로메테우스 메트릭 시각화 하기 

########################################################
##  유용한 강좌
1. [AWS에서 kubeadm로 클라우드 프로바이더를 설정해 쿠버네티스 설치하기](https://blog.naver.com/alice_k106/221696987140)
2. [kops 설치 시, IAM 역할 및 사용자 생성하기](https://blog.naver.com/alice_k106/221342005691)
3. [쿠버네티스 컴포넌트의 실행 옵션 변경하기](https://blog.naver.com/alice_k106/221737477464)
4. [쿠버네티스 버전이 너무 낮을 때 Nginx Ingress 포드가 Pending으로 뜨는 현상](./lecture4-nginx-ingress.md)
5. [GKE에서 Google Persistent Disk를 사용해 퍼시스턴트 볼륨 사용하기](https://blog.naver.com/alice_k106/221737984779)
6. [Dex와 Guard를 이용한 쿠버네티스 사용자 인증 방법](https://blog.naver.com/alice_k106/221598325656)
7. [CPU Affinity를 위해 CPU Manager 사용하기](https://blog.naver.com/alice_k106/221633530545)
8. [애드미션 컨트롤러를 직접 구현해보기](https://blog.naver.com/alice_k106/221546328906)
9. [커스텀 리소스의 제어를 위한 Operator 직접 구현해보기](https://blog.naver.com/alice_k106/221586279079)
    

    


