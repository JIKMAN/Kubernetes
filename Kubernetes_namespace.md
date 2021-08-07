## Kubernetes namespace

클러스터 하나를 여러개의 논리적 단위로 나눠서 사용

쿠버네티스 클레스터 하나를 여러 팀이나 사용자가 함께 공유하거나,

용도에 따라 실행해야 하는 앱을 구분할 때 사용

![img](https://blog.kakaocdn.net/dn/bKJ4e2/btqNg93AvjZ/yhFvwzsKeYquVszWJH4Yy1/img.png)

위는 쿠버네티스 클러스터를 **dev**, **stg**, **prd** 세 개의 네임스페이스로 구분한 겁니다.
dev 목적의 사용자는 dev namespace에 접근하여 오브젝트를 배치 또는 운영하고,
stage 목적의 사용자는 stg namespace에 접근하여 운영하는 거죠.

다만 **namespace는 클러스터를 논리적으로 분리하는 것이지, 물리적으로 분리하는 것은 아니기 때문에**, **isolation은** 되지 않는다.
다른 namespace의 pod이더라도, 서로 통신이 가능할 뿐만 아니라 클러스터의 장애가 발생할 경우, 모든 namespace가 타격을 입게 되니다. namespace를 통한 **fault-tolerance** 확보등은 이루어질 수 없습니다.
isolation을 원할 경우, 쿠버네티스 클러스터를 다중화/이중화 함으로써 해결해야 합니다.

### **namespace의 목적**

#### - 네임스페이스별 리소스 할당량 지정



![img](https://blog.kakaocdn.net/dn/m2y5P/btqNkeiP1UV/R94yeZJRjSBe7TeR27PDs0/img.png)



네임 스페이스를 통해 CPU/GPU 할당량을 조절할 수 있습니다.
서비스의 운영 환경은 지연이 발생하지 않도록 매우 강력한 power와 리소스를 가져야 하지만, 개발과 신규 기능 및 수정 사항을 테스트 하기 위한 환경은 그 정도로 powerful할 필요가 없습니다.
따라서 자원을 각각 필요한 만큼 할당할 수 있습니다.
**빈약한 환경 속에서도 최적의 개발 및 운영 환경을 구축하는 거죠**

 

#### - 사용자별 네임스페이스 접근 권한

**Authorization**이라고 하는 분야의 이야기죠. 권한관리는 Well-made 서비스를 위해 반드시 필요합니다.
쿠버네티스 클러스터의 api나 namespace에 접근하기 위해서, 유효한 사용자 인증(authentication)을 거치게 할 수 있습니다.
사용자 인증 후, 해당 사용자가 api 또는 namespace에 권한이 있는지 체크하고, 검증된 사용자만 api를 사용하게 하게 됩니다.
일반적인 Authorization은 **ABAC**(Attribute-based access control)과 **RBAC**(Role-based access control)로 구분됩니다.
**ABAC**은 속성 기반의 권한 관리로, 사용자/그룹/요청 경로/네임스페이스 등으로 권한을 설정합니다. 여기서 언급된 접근 권한은 ABAC을 의미합니다.
**RBAC**의 경우에는 역할 기반 권한 관리로, 사용자와 역할을 별개로 선언하고 둘을 binding 하여 사용자에게 권한을 부여하는 방식으로 구현됩니다. 일반적으로 RBAC이 더 많이 사용됩니다.