# Kubernetes



## 실습환경

* 쿠버네티스(minikube) 설치

```bash
# docker 사용시 설치 필요
curl -fsSL https://get.docker.com/ | sudo sh
sudo usermod -aG docker $USER

# install minikube
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 \
  && chmod +x minikube
sudo mkdir -p /usr/local/bin/
sudo install minikube /usr/local/bin/
```



* 기본 명령어

```bash
# 버전확인
minikube version

# 가상머신 시작
minikube start --driver=docker
# driver 에러가 발생한다면 virtual box를 사용
minikube start --driver=virtualbox
# 특정 k8s 버전 실행
minikube start --kubernetes-version=v1.20.0

# minikube 상태확인
minikube status

# minikube 실행
minikube start

# 특정 k8s 버전 실행
minikube start --kubernetes-version=v1.20.0

# 특정 driver 실행
minikube start --driver=virtualbox --kubernetes-version=v1.20.0

# minikube ip 확인 (접속테스트시 필요)
minikube ip

# minikube 종료
minikube stop

# minikube 제거
minikube delete
```

---

## 다양한 운영환경

- [kubeadm(opens new window)](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/)
- [kubespray(opens new window)](https://github.com/kubernetes-sigs/kubespray)
- [Amazon EKS(opens new window)](https://aws.amazon.com/ko/eks)
- [Google Kubernetes Engine(opens new window)](https://cloud.google.com/kubernetes-engine)
- [Azure Kubernetes Service](https://docs.microsoft.com/ko-kr/azure/aks/)

##  다중노드

최신 minikube 버전을 사용한다면, 다중노드를 구성할 수 있습니다.

```sh
# 가상머신 시작 (단일노드, 기본)
minikube start

# 가상머신 시작 (단중노드)
minikube start -n 2
```

## 멀티 프로필

하나의 개발피시에 여러개의 minikube를 사용할 수 있습니다.

```sh
# 가상머신 시작
minikube start # 기본 profile - minikube로 생성

# 두번째 가상머신 시작
minikube start -p hellowlrd # helloworld 라는 이름의 profile로 생성

# profile 목록 확인
minikube profile list

# 현재 사용중인 profile 확인
minikube profile

# 다른 profile로 변경
minikube profile hellowlrd # helloworld로 변경
minikube profile minikube # minikube로 변경

# 가상머신 제거
minikube delete # 현재 사용중인 profile의 가상머신 제거
```

### Kubectl install

```sh
curl -LO "https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl

# test
kubectl version
```


