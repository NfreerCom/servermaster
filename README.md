

DOCKER 설치 스크립트
curl -fsSL https://get.docker.com/ | sudo sh

su -
systemctl start docker
systemctl enable docker
docker version

루트로 실행할것
docker version

자세히 조회

kubectl describe node linux-server

<도커그룹추가 - 퍼미션 에러시>
sudo usermod -a -G docker dockermake

https://docs.docker.com/engine/install/centos/

swapoff -a && sed -i '/swap/s/^/#/' /etc/fstab

systemctl daemon-reload && systemctl restart kubelet

< 도커 설치 후 도커 그룹에 관리자 추가>
usermod -a -G docker master

확인
docker ps
<도커실행상태 확인>
systemctl status docker
<재부팅시 계속 실행되게>
systemctl enable docker

<쿠버네티스 우분투(데비안) 계열
swapoff -a && sed -i '/swap/s/^/#/' /etc/fstab
cat <<EOF > /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
EOF
sysctl --system
systemctl stop firewalld 
systemctl disable firewalld && sudo apt-get update && sudo apt-get install -y apt-transport-https ca-certificates curl && sudo curl -fsSLo /usr/share/keyrings/kubernetes-archive-keyring.gpg https://packages.cloud.google.com/apt/doc/apt-key.gpg && echo "deb [signed-by=/usr/share/keyrings/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list && sudo apt-get update && sudo apt-get install -y kubelet kubeadm kubectl && sudo apt-mark hold kubelet kubeadm kubectl && systemctl start kubelet && systemctl enable kubelet

< centos>
cat <<EOF | sudo tee /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-\$basearch
enabled=1
gpgcheck=1
gpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg
exclude=kubelet kubeadm kubectl
EOF
sudo setenforce 0
sudo sed -i 's/^SELINUX=enforcing$/SELINUX=permissive/' /etc/selinux/config
sudo yum install -y kubelet kubeadm kubectl --disableexcludes=kubernetes
sudo systemctl enable --now kubelet

도커 실행 컨테이너 확인
docker ps

< helm 설치>
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 && chmod 700 get_helm.sh && ./get_helm.sh && helm version && helm repo add stable https://charts.helm.sh/stable && helm repo list && helm repo update

< 쿠베 네임스페이스 생성>
kubectl create namespace db 
<사용 >
--namespace

wsl2 설치
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart

Docker build
이미지를 빌드하는 명령어는 다음과 같습니다.
docker build [OPTIONS] PATH | URL | -
생성할 이미지 이름을 지정하기 위한 -t(--tag) 옵션만 알면 빌드가 가능합니다.
Dockerfile을 만든 디렉토리로 이동하여 다음 명령어를 입력합니다.

1	docker build -tapp .

kubectl annotate node/{nodename} kubeadm.alpha.kubernetes.io/cri-socket- node/{nodename} annotated
kubectl annotate node/{nodename} kubeadm.alpha.kubernetes.io/cri-socket=unix:///run/containerd/containerd.sock node/{nodename} annotated

[ERROR CRI]: container runtime is not running
 
 
/etc/containerd/config.toml 파일에서 
disabled_plugins 항목에서 CRI 제거한 뒤
 
$ systemctl restart containerd

kubeadm init

<root>

mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config

kubectl get nodes

<master 에게도 한번더 >

mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config

sudo kubectl get nodes

kubectl apply -f "https://cloud.weave.works/k8s/net?k8s-version=$(kubectl version | base64 | tr -d '\n')"

< 노드들에 붙여넣기 실행해준다>

kubeadm join 200.0.0.10:6443 --token u4o1x8.o0uy4m4p72n5h27t \
	--discovery-token-ca-cert-hash sha256:1ffa3e046cf5048be5b43f9483b6d29846ec598fb2b82697ad4b8a94256bfe36

kubeadm join 200.0.0.10:6443 --token u4o1x8.o0uy4m4p72n5h27t \
	--discovery-token-ca-cert-hash sha256:1ffa3e046cf5048be5b43f9483b6d29846ec598fb2b82697ad4b8a94256bfe36

kubeadm 설치
https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/

cat token.txt

ctrl+d

아래 에러 경우
Unable to connect to the server: x509

export KUBECONFIG=/etc/kubernetes/admin.conf
<root 가 아닌 관리자(master) 로그인시>
sudo cp /etc/kubernetes/admin.conf /etc/kubernetes/master.conf
sudo chown master /etc/kubernetes/master.conf
sudo chown :master /etc/kubernetes/master.conf
export KUBECONFIG=/etc/kubernetes/master.conf

노드 에러나면 서버는
kubeadm reset
kubeadm init
export KUBECONFIG=/etc/kubernetes/admin.conf
kubectl apply -f "https://cloud.weave.works/k8s/net?k8s-version=$(kubectl version | base64 | tr -d '\n')"
systemctl stop firewalld 

클라이언트는 리셋하고 서버 방화벽 해제 후
root 로 토큰을 실행해준다

systemctl stop firewalld 
systemctl disable firewall

wsl --export CentOS7 F:\111\EDU\Coding\centos\centos7.tar

source <(kubectl completion bash)
echo "source <(kubectl completion bash)" >> ~/.bashrc

echo > token.txt 텍스트

<조회 4종>
kubectl get nodes -o wide && kubectl get pods -n kube-system -o wide && kubectl get pods -o wide && kubectl get namespaces
< 조회2종 추천>
kubectl get nodes -o wide && kubectl get pods --all-namespaces -o wide && kubectl get svc,pod -n cert-manager

kubectl config view

kubectl get nodes -o wide

< 쿠버 설정파일>
sudo cat /var/lib/kubelet/config.yaml

< static pod 관리 폴더>
staticPodPath: /etc/kubernetes/manifests

쿠버네티스 서버 재부팅시
export KUBECONFIG=/etc/kubernetes/master.conf

만 실행해주면 된다

kubectl run webserver --image=nginx:1.20 --port 80
kubectl apply -f prometheus.yaml
kubectl get pods -o wide

<도커 이미지 바로 실행 > 
docker run -dit --name 컨테이너명 이미지명

<도커 태그 >
docker tag 이미지명 192.168.111.12:80/태그명

실행 중인 포드에서 yaml 파일을 만듭니다.
	1. kubectl get po -n nginx nginx-deployment-755cfc7dcf-5s7j8 -o yaml > podDetail.yaml
실행 중인 포드에서 replicaset yaml 파일을 작성하십시오.
	2. kubectl get rs -n nginx -o yaml > latestReplicaSet.yaml
실행 중인 포드에서 배포 yaml 파일을 생성합니다.
	3. kubectl get deploy -n nginx -o yaml > latestDeployement.yaml

출처: <https://stackoverflow.com/questions/43941772/get-yaml-for-deployed-kubernetes-services> 

<1개 만들때>
kubectl run harbor-server --image=bitnami/harbor-core:latest --port 5000

< 다중 생성>
kubectl create deployment dep-web --image=httpd --replicas=2

<centos 관리자그룹>
wheel
usermod -aG wheel $USER

< 원격 폴더 파일 복사해올때>
scp -p 5000 worker2@192.168.111.12:~/docker_repository/certs/* ~/certs/

파트 자세히 볼때
kubectl describe pod nginx

파드 안으로 들어갈때
kubectl exec web -it -- /bin/bash

쿠버네티스 서버ip 변경먹통시 /etc/kubernetes 내의 ip 모두 변경해줄것

< 파일 내용 찾기>
find / -type f | xargs grep 200.0.0.10

파트 지울때
kubectl delete deployments.apps pod명

git clone git주소

dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart

kubectl get pod --show-labels

FROM node:12
COPY /source/hello.js /
CMD  ["node","/hello.js"]


docker build -t hellojs:lastest .

<docker compose 설치 >
sudo curl -L "https://github.com/docker/compose/releases/download/v2.8.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

sudo chmod +x /usr/local/bin/docker-compose

docker-compose --version

< 도커 그룹에 추가 >

sudo usermod -aG docker $USER
sudo service docker restart or 재부팅
<그룹없을때만>
sudo groupadd docker

<IPv4 forwarding is disabled. Networking will not work >

I added the following to /etc/sysctl.conf:
net.ipv4.ip_forward=1
I then restarted the network service and validated the setting:
[root@pprdespap322 deploy]#  systemctl restart network
[root@pprdespap322 deploy]# sysctl net.ipv4.ip_forward

< 실행문제 확인시>
kubectl describe pods &&  kubectl logs -f harbor-server  --since=5m

< 쿠버네티스 pods 삭제 > 
kubectl delete pods 파드명


<docker iptables 관련 에러 >
sudo iptables -t filter -F && sudo iptables -t filter -X && systemctl restart docker

<도커 private local registry 구축>
sudo iptables -t filter -F && sudo iptables -t filter -X && systemctl restart docker

sudo vim /etc/docker/daemon.json

{
"insecure-registries" : ["localhost:5000"]
}

sudo systemctl daemon-reload
sudo systemctl restart docker

docker pull registry
sudo mkdir -p /mnt/docker/registry-mount
docker run -dit --restart always -v /mnt/docker/registry-mount:/var/lib/registry --name docker-registry -p 5000:5000 registry
docker ps
docker tag registry localhost:5000/docker-push
docker push localhost:5000/docker-push
curl -X GET http://localhost:5000/v2/_catalog

<도커 nginx >
docker pull nginx
docker run -d --name webserver -p 80:80 nginx:1.21.1


-------------------------------------------------------------

server {
     listen [::]:80;
     listen 80;
server_name domain.com reg-server.com;
location ~ /.well-known/acme-challenge {
         allow all; 
         root /var/www/certbot;
     }
} 



< 2초마다 pod 조회>
watch kubectl get pods -o wide

< 도커 실행 컨테이너 내부 접속>
docker exec -itu 0 59fedb45ac25 /bin/bash

<쿠버네티스 컨테이너 내부 접속>
kubectl exec pod명 -it -- /bin/bash

<nginx 경로> /usr/share/nginx/html/
<아파치 경로> /usr/local/apache2/htdocs/

< 쿠버 외부노출>
kubectl expose deployment NAME --port 8080 --type NodePort
kubectl port-forward apache-74469546f4-8cd84 8080:8080

ps -ef | grep dockerd
sudo systemctl status docker
< start-limit 오류시>
sudo vim /lib/systemd/system/docker.service


< 쿠버 디플로이먼트 편집 >
kubectl edit deployment apache

< 쿠버 pod 실행대신 yaml파일로

kubectl run apache --image=httpd --port 80 --dry-run -o yaml > apache-pod.yaml

< 파일로 실행 >
kubectl create -f apache-pod.yaml

< 볼륨 예제>
docker run -d --name 컨테이너명 -v /경로:/로컬경로 -e MYSQL_ROOT_PASSWORD=비밀번호 mysql

docker run -dit --name dbrun2 -v /dbdata:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=pass mysql:latest

< 반복 저장 쉘스크립트>

< ip테이블 보기>
sudo iptables -t nat -L -v

쿠버 네임스페이스 현재 설정
kubectl config set-context --current --namespace=nginx

< cert-manager 설치>

kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.9.1/
![image](https://user-images.githubusercontent.com/66663205/216630929-307445c6-50d7-4b36-9106-d464d92aa211.png)
