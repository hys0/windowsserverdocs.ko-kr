---
title: 네트워크 컨트롤러 배포를 위한 요구 사항
description: 하나 이상의 컴퓨터 또는 vm과 하나 이상의 컴퓨터 또는 VM이 필요한 네트워크 컨트롤러 배포를 위해 데이터 센터를 준비 합니다. 네트워크 컨트롤러를 배포 하기 전에 보안 그룹, 로그 파일 위치 (필요한 경우) 및 동적 DNS 등록을 구성 해야 합니다.
manager: grcusanz
ms.prod: windows-server
ms.technology: networking-sdn
ms.topic: get-started-article
ms.assetid: 7f899e62-6e5b-4fca-9a59-130d4766ee2f
ms.author: anpaul
author: AnirbanPaul
ms.date: 08/10/2018
ms.openlocfilehash: da9164eea4ab7e2fb38864fb69c47252448b77b6
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80854426"
---
# <a name="requirements-for-deploying-network-controller"></a>네트워크 컨트롤러 배포를 위한 요구 사항

>적용 대상: Windows Server(반기 채널), Windows Server 2016

하나 이상의 컴퓨터 또는 vm과 하나 이상의 컴퓨터 또는 VM이 필요한 네트워크 컨트롤러 배포를 위해 데이터 센터를 준비 합니다. 네트워크 컨트롤러를 배포 하기 전에 보안 그룹, 로그 파일 위치 (필요한 경우) 및 동적 DNS 등록을 구성 해야 합니다.


## <a name="network-controller-requirements"></a>네트워크 컨트롤러 요구 사항

네트워크 컨트롤러 배포에는 네트워크 컨트롤러 역할을 하는 하나 이상의 컴퓨터 또는 vm과 네트워크 컨트롤러에 대 한 관리 클라이언트 역할을 하는 컴퓨터 또는 VM이 하나 이상 필요 합니다. 

- 네트워크 컨트롤러 노드로 계획 된 모든 Vm 및 컴퓨터는 Windows Server 2016 Datacenter edition을 실행 해야 합니다. 
- 네트워크 컨트롤러를 설치 하는 컴퓨터 또는 VM (가상 컴퓨터)은 Windows Server 2016의 Datacenter edition을 실행 해야 합니다. 
- 네트워크 컨트롤러에 대 한 관리 클라이언트 컴퓨터 또는 VM은 Windows 10을 실행 해야 합니다. 


## <a name="configuration-requirements"></a>구성 요구 사항

네트워크 컨트롤러를 배포 하기 전에 보안 그룹, 로그 파일 위치 (필요한 경우) 및 동적 DNS 등록을 구성 해야 합니다.

### <a name="step-1-configure-your-security-groups"></a>1단계. 보안 그룹 구성

가장 먼저 할 일은 Kerberos 인증에 대 한 두 개의 보안 그룹을 만드는 것입니다. 

다음에 대 한 권한이 있는 사용자에 대 한 그룹을 만듭니다. 

1. 네트워크 컨트롤러 구성<p>예를 들어이 그룹의 이름을 네트워크 컨트롤러 관리자로 지정할 수 있습니다. 
2.  네트워크 컨트롤러를 사용 하 여 네트워크 구성 및 관리<p>예를 들어이 그룹의 이름을 네트워크 컨트롤러 사용자로 지정할 수 있습니다. REST (Representational State Transfer)를 사용 하 여 네트워크 컨트롤러를 구성 하 고 관리 합니다.

>[!NOTE]
>사용자가 추가 하는 모든 사용자는 Active Directory 사용자 및 컴퓨터에서 Domain Users 그룹의 구성원 이어야 합니다.

### <a name="step-2-configure-log-file-locations-if-needed"></a>2단계. 필요한 경우 로그 파일 위치 구성

다음에 수행할 작업은 네트워크 컨트롤러 컴퓨터 또는 VM 또는 원격 파일 공유에 네트워크 컨트롤러 디버그 로그를 저장할 파일 위치를 구성 하는 것입니다. 

>[!NOTE]
>원격 파일 공유에 로그를 저장 하는 경우 네트워크 컨트롤러에서 공유에 액세스할 수 있는지 확인 합니다.


### <a name="step-3-configure-dynamic-dns-registration-for-network-controller"></a>3단계. 네트워크 컨트롤러에 대 한 동적 DNS 등록 구성

마지막으로, 다음에 수행할 작업은 동일한 서브넷 또는 다른 서브넷에 네트워크 컨트롤러 클러스터 노드를 배포 하는 것입니다. 


|         조건         |                                                                                                                                                         결과                                                                                                                                                         |
|-----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  동일한 서브넷에서  |                                                                                                                                네트워크 컨트롤러 REST IP 주소를 제공 해야 합니다.                                                                                                                                 |
| 다른 서브넷에서 | 배포 프로세스 중에 만든 네트워크 컨트롤러 REST DNS 이름을 제공 해야 합니다. 또한 다음을 수행 해야 합니다.<ul><li>DNS 서버에서 네트워크 컨트롤러 DNS 이름에 대 한 DNS 동적 업데이트를 구성 합니다.</li><li>DNS 동적 업데이트를 네트워크 컨트롤러 노드로만 제한 합니다.</li></ul> |

---

> [!NOTE]
> 이러한 절차를 수행 하려면 최소한 **Domain Admins**의 구성원 이거나 이와 동등한 자격이 필요 합니다.

1. 영역에 대 한 DNS 동적 업데이트를 허용 합니다.

   a. DNS 관리자를 열고 콘솔 트리에서 적절 한 영역을 마우스 오른쪽 단추로 클릭 한 다음 **속성**을 클릭 합니다. 

   b. **일반** 탭에서 영역 유형이 **기본** 또는 **Active Directory 통합**인지 확인 합니다.

   c. **동적 업데이트**에서 **보안만** 선택 되어 있는지 확인 한 다음 **확인**을 클릭 합니다.

2. 네트워크 컨트롤러 노드에 대 한 DNS 영역 보안 권한 구성

   a.  **보안** 탭을 클릭하고 **고급**을 클릭합니다. 

   b. **고급 보안 설정**에서 **추가**를 클릭 합니다. 

   c. **보안 주체 선택**을 클릭합니다. 

   . **사용자, 컴퓨터, 서비스 계정 또는 그룹 선택** 대화 상자에서 **개체 유형**을 클릭 합니다. 

   e. **개체 유형**에서 **컴퓨터**를 선택 하 고 **확인**을 클릭 합니다.

   f. **사용자, 컴퓨터, 서비스 계정 또는 그룹 선택** 대화 상자에서 배포의 네트워크 컨트롤러 노드 중 하나의 NetBIOS 이름을 입력 한 다음 **확인**을 클릭 합니다.

   g. **사용 권한 항목**에서 다음 값을 확인 합니다.

      - **유형** = 허용
      - **적용 대상** =이 개체 및 모든 하위 개체

   h. **권한**에서 **모든 속성 쓰기** 및 **삭제**를 선택 하 고 **확인**을 클릭 합니다.

3. 네트워크 컨트롤러 클러스터의 모든 컴퓨터 및 Vm에 대해 반복 합니다.

### <a name="step-4-configure-service-principal-name-if-using-kerberos-based-authentication"></a>4단계. Kerberos 기반 인증을 사용 하는 경우 서비스 사용자 이름 구성

네트워크 컨트롤러가 관리 클라이언트와의 통신에 Kerberos 기반 인증을 사용 하는 경우 Active Directory에서 네트워크 컨트롤러에 대 한 SPN (서비스 사용자 이름)을 구성 해야 합니다. 네트워크 컨트롤러에서 SPN을 자동으로 구성 합니다. 네트워크 컨트롤러 컴퓨터에서 SPN을 등록 하 고 수정할 수 있는 권한을 제공 하기만 하면 됩니다. 자세한 내용은 [SPN (서비스 사용자 이름) 구성](https://docs.microsoft.com/windows-server/networking/sdn/security/kerberos-with-spn#configure-service-principal-names-spn)을 참조 하세요.

## <a name="deployment-options"></a>배포 옵션

### <a name="network-controller-deployment"></a>네트워크 컨트롤러 배포

가상 컴퓨터에 구성 된 세 개의 네트워크 컨트롤러 노드를 사용 하 여 설치 프로그램을 항상 사용할 수 있습니다. 또한 웹 계층 및 데이터베이스 계층을 시뮬레이션 하기 위해 테 넌 트 2의 가상 네트워크를 두 개의 가상 서브넷으로 분할 하는 두 개의 테 넌 트가 표시 됩니다.  

![SDN NC 계획](../../media/Plan-a-Software-Defined-Network-Infrastructure/SDN-NC-Planning.png)

### <a name="network-controller-and-software-load-balancer-deployment"></a>네트워크 컨트롤러 및 소프트웨어 부하 분산 장치 배포

높은 가용성의 경우 SLB/MUX 노드가 두 개 이상 있습니다.

![SDN NC 계획](../../media/Plan-a-Software-Defined-Network-Infrastructure/SDN-SLB-Deployment.png)

### <a name="network-controller-software-load-balancer-and-ras-gateway-deployment"></a>네트워크 컨트롤러, 소프트웨어 Load Balancer 및 RAS 게이트웨이 배포

3 개의 게이트웨이 가상 머신이 있습니다. 둘 중 하나가 활성 상태이 고 하나는 중복 됩니다.

![SDN NC 계획](../../media/Plan-a-Software-Defined-Network-Infrastructure/SDN-GW-Deployment.png)  



T P 5 기반 배포 자동화의 경우 Active Directory를 사용 가능 하 고 이러한 서브넷에서 연결할 수 있어야 합니다. Active Directory에 대 한 자세한 내용은 [Active Directory Domain Services 개요](https://docs.microsoft.com/windows-server/identity/ad-ds/get-started/virtual-dc/active-directory-domain-services-overview)를 참조 하세요.  

>[!IMPORTANT] 
>VMM을 사용 하 여 배포 하는 경우 인프라 가상 컴퓨터 (VMM 서버, AD/DNS, SQL Server 등)가 다이어그램에 표시 된 네 개의 호스트에서 호스팅되지 않도록 합니다.  


## <a name="next-steps"></a>다음 단계
[소프트웨어 정의 네트워크 인프라를 계획](https://technet.microsoft.com/windows-server-docs/networking/sdn/plan/plan-a-software-defined-network-infrastructure)합니다.

## <a name="related-topics"></a>관련 항목
- [네트워크 컨트롤러](../technologies/network-controller/Network-Controller.md) 
- [네트워크 컨트롤러 고가용성](../technologies/network-controller/network-controller-high-availability.md) 
- [Windows PowerShell을 사용하여 네트워크 컨트롤러 배포](../deploy/Deploy-Network-Controller-using-Windows-PowerShell.md)   
- [서버 관리자를 사용하여 네트워크 컨트롤러 서버 역할 설치](../technologies/network-controller/Install-the-Network-Controller-server-role-using-Server-Manager.md)   
