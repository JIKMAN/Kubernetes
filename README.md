# Kubernetes

쿠버네티스 개인 학습 레포지토리

참고문서

https://kubernetes.io/ko/docs/home/

https://subicura.com/k8s/

## 쿠버네티스가 왜 필요한가

컨테이너는 애플리케이션을 포장하고 실행하는 좋은 방법이다. 프로덕션 환경에서는 애플리케이션을 실행하는 컨테이너를 관리하고 가동 중지 시간이 없는지 확인해야 한다. 예를 들어 컨테이너가 다운되면 다른 컨테이너를 다시 시작해야 한다. 이 문제를 시스템에 의해 처리한다면 더 쉽지 않을까?

그것이 쿠버네티스가 필요한 이유이다! 쿠버네티스는 분산 시스템을 탄력적으로 실행하기 위한 프레임 워크를 제공한다. 애플리케이션의 확장과 장애 조치를 처리하고, 배포 패턴 등을 제공한다.

- **서비스 디스커버리와 로드 밸런싱** : 쿠버네티스는 DNS 이름을 사용하거나 자체 IP 주소를 사용하여 컨테이너를 노출할 수 있다. 컨테이너에 대한 트래픽이 많으면, 쿠버네티스는 네트워크 트래픽을 로드밸런싱하고 배포하여 배포가 안정적으로 이루어질 수 있다.
- **스토리지 오케스트레이션** : 쿠버네티스를 사용하면 로컬 저장소, 공용 클라우드 공급자 등과 같이 원하는 저장소 시스템을 자동으로 탑재 할 수 있다.
- **자동화된 롤아웃과 롤백** : 쿠버네티스를 사용하여 배포된 컨테이너의 상태를 보여주며 현재 상태를 설정한 속도에 따라 변경할 수 있다. 예를 들어 쿠버네티스를 자동화해서 배포용 새 컨테이너를 만들고, 기존 컨테이너를 제거하고, 모든 리소스를 새 컨테이너에 적용할 수 있다.
- **자동화된 빈 패킹(bin packing)** : 컨테이너화된 작업을 실행하는데 사용할 수 있는 쿠버네티스 클러스터 노드를 제공한다. 각 컨테이너가 필요로 하는 CPU와 메모리(RAM)를 할당한다. 쿠버네티스는 리소스를 절절히 관리한다.
- **자동화된 복구(self-healing)** : 실패한 컨테이너를 다시 시작하고, 컨테이너를 교체하며, 응답하지 않는 컨테이너를 kill한다. 이 모든 과정이 백그라운드 상에서 이루어진다.
- **보안 및 구성 관리** : 쿠버네티스를 사용하면 암호, OAuth 토큰 및 SSH 키와 같은 중요한 정보를 저장하고 관리 할 수 있다. 컨테이너 이미지를 재구성하지 않고 스택 구성에 노출하지 않고도 애플리케이션 구성을 배포 및 업데이트 할 수 있다.

## 쿠버네티스 구성요소

쿠버네티스를 배포하면 클러스터를 얻는다.

쿠버네티스 클러스터는 컨테이너화된 애플리케이션을 실행하는 노드

워커 노드는 애플리케이션의 구성요소인 **Pod**를 호스트한다. **Control Plane**은 워커 노드와 클러스터 내 파드를 관리한다. 프로덕션 환경에서는 일반적으로 컨트롤 플레인이 여러 컴퓨터에 걸쳐 실행되고, 클러스터는 일반적으로 여러 노드를 실행하므로 내결함성과 고가용성이 제공된다.

![쿠버네티스 클러스터](https://d33wubrfki0l68.cloudfront.net/2475489eaf20163ec0f54ddc1d92aa8d4c87c96b/e7c81/images/docs/components-of-kubernetes.svg)

>  ### 컨트롤 플레인 구성요소
>
> 컨트롤 플레인은 클러스터에 관한 전반적인 결정(ex, 스케줄링)을 수행하고 클러스터 이벤트(ex, `replicas` 필드에 대한 요구 조건이 충족되지 않을 경우 새로운 Pods를 구동시키는 것)를 감지하고 반응한다.

* ### kube-apiserver

  API 서버는 쿠버네티스 API를 노출하는 컨트롤 플레인의 프론트 엔드 역할

* ### etcd

  모든 클러스터 데이터를 담는 쿠버네티스 뒷단의 저장소로 사용되는 일관성·고가용성 키-값 저장소.

* ### kube-scheduler

  노드가 배정되지 않은 새로 생성된 파드를 감지하고, 실행할 노드를 선택

* ### kube-controller-manager

  컨트롤러 프로세스를 실행

  * node controller : 노드가 다운되었을 때 통지와 대응에 관한 책임을 가진다.
  * replication controller : 시스템의 모든 레플리케이션 컨트롤러 오브젝트에 대해 알맞은 수의 파드들을 유지시켜 주는 책임을 가진다.
  * end-point controller : 엔드포인트 오브젝트를 채운다(즉, 서비스와 파드를 연결시킨다.)
  * service account & token controller : 새로운 네임스페이스에 대한 기본 계정과 API 접근 토큰을 생성한다.

* ### cloud-controller-manager

  클라우드별 컨트롤 로직을 포함한다. 클러스터를 클라우드 공급자의 API에 연결하고, 해당 클라우드 플랫폼과 상호 작용하는 컴포넌트와 클러스터와만 상호 작용하는 컴포넌트를 구분할 수 있게 해 준다.

---

>  ### 노드 구성요소
>
> 노드 컴포넌트는 동작 중인 파드를 유지시키고 쿠버네티스 런타임 환경을 제공하며, 모든 노드 상에서 동작한다.

* ### kubelet

  클러스터의 각 노드에서 실행되는 에이전트. 파드에서 컨테이너가 확실하게 동작하도록 관리(health check)

* ### kube-proxy

  클러스터의 각 노드에서 실행되는 네트워크 프록시

* ### Container Runtime

  컨테이너 실행을 담당하는 소프트웨어

---

> ### Add-on

* ### DNS

  모든 쿠버네티스 클러스터는 클러스터 DNS를 갖추어야만 한다.

* ### 웹 UI (대시보드)

* ### 컨테이너 리소스 모니터링

  중앙 데이터베이스 내의 컨테이너들에 대한 포괄적인 시계열 매트릭스를 기록하고 그 데이터를 열람하기 위한 UI를 제공

* ### 클러스터-레벨 로깅

  검색/열람 인터페이스와 함께 중앙 로그 저장소에 컨테이너 로그를 저장