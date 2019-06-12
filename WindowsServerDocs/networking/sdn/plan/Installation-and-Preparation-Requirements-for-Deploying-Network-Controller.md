---
title: 네트워크 컨트롤러를 배포 하기 위한 요구 사항
description: 하나 이상의 컴퓨터 또는 Vm 및 컴퓨터 또는 VM을 해야 하는 네트워크 컨트롤러 배포에 대 한 데이터 센터를 준비 합니다. 네트워크 컨트롤러를 배포 하기 전에 보안 그룹, 로그 파일 위치 (필요한 경우) 및 동적 DNS 등록을 구성 해야 합니다.
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.topic: get-started-article
ms.assetid: 7f899e62-6e5b-4fca-9a59-130d4766ee2f
ms.author: pashort
author: shortpatti
ms.date: 08/10/2018
ms.openlocfilehash: 51ba991397a7c35ee0198f8e75c67b2f99b7c7bc
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446311"
---
# <a name="requirements-for-deploying-network-controller"></a>네트워크 컨트롤러를 배포 하기 위한 요구 사항

>적용 대상: Windows Server (반기 채널), Windows Server 2016

하나 이상의 컴퓨터 또는 Vm 및 컴퓨터 또는 VM을 해야 하는 네트워크 컨트롤러 배포에 대 한 데이터 센터를 준비 합니다. 네트워크 컨트롤러를 배포 하기 전에 보안 그룹, 로그 파일 위치 (필요한 경우) 및 동적 DNS 등록을 구성 해야 합니다.


## <a name="network-controller-requirements"></a>네트워크 컨트롤러 요구 사항

네트워크 컨트롤러 배포에는 하나 이상의 컴퓨터 또는 컴퓨터와 네트워크 컨트롤러를 처리 하는 Vm 또는 VM에 네트워크 컨트롤러에 대 한 관리 클라이언트 역할도 필요 합니다. 

- 모든 Vm 및 네트워크 컨트롤러 노드를 계획 하는 컴퓨터를 Windows Server 2016 Datacenter edition에 실행 되어야 합니다. 
- 모든 컴퓨터 또는 VM (가상 머신) 네트워크 컨트롤러를 설치 하는 Windows Server 2016 Datacenter edition을 실행 해야 합니다. 
- 관리 클라이언트 컴퓨터 또는 VM 네트워크 컨트롤러에 대 한 Windows 10을 실행 해야 합니다. 


## <a name="configuration-requirements"></a>구성 요구 사항

네트워크 컨트롤러를 배포 하기 전에 보안 그룹, 로그 파일 위치 (필요한 경우) 및 동적 DNS 등록을 구성 해야 합니다.

### <a name="step-1-configure-your-security-groups"></a>1단계. 보안 그룹 구성

가장 먼저 수행 하려는 경우 Kerberos 인증에 대 한 두 개의 보안 그룹 만들기 

권한이 있는 사용자에 대 한 그룹을 만들어야 하 합니다. 

1. 네트워크 컨트롤러를 구성 합니다.<p>예를 들어이 그룹의 네트워크 컨트롤러 관리자 이름을 지정할 수 있습니다. 
2.  구성 하 고 네트워크 컨트롤러를 사용 하 여 네트워크를 관리 합니다.<p>예를 들어이 그룹 네트워크 컨트롤러 사용자 이름을 지정할 수 있습니다. REST Representational State Transfer ()를 사용 하 여 구성 하 고 네트워크 컨트롤러를 관리 합니다.

>[!NOTE]
>모든 사용자를 추가 하면 Active Directory 사용자 및 컴퓨터에서 Domain Users 그룹의 구성원 이어야 합니다.

### <a name="step-2-configure-log-file-locations-if-needed"></a>2단계. 필요한 경우 로그 파일 위치를 구성 합니다.

다음 수행 하려는 것 원격 파일 공유 또는 네트워크 컨트롤러 컴퓨터 또는 VM에서 네트워크 컨트롤러 디버그 로그를 저장 하는 파일 위치를 구성 합니다. 

>[!NOTE]
>원격 파일 공유에서 로그를 저장 하는 경우 공유 네트워크 컨트롤러에서 액세스할 수 있는지 확인 합니다.


### <a name="step-3-configure-dynamic-dns-registration-for-network-controller"></a>3단계. 네트워크 컨트롤러에 대 한 동적 DNS 등록을 구성 합니다.

마지막으로, 다음 수행 하려는 것 같은 서브넷 또는 다른 서브넷에 네트워크 컨트롤러 클러스터 노드를 배포 합니다. 


|         해당하는 경우         |                                                                                                                                                         발생하는 결과                                                                                                                                                         |
|-----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  동일한 서브넷에서  |                                                                                                                                네트워크 컨트롤러 REST IP 주소를 제공 해야 합니다.                                                                                                                                 |
| 서로 다른 서브넷에 | 배포 프로세스 중에 만든 네트워크 컨트롤러 REST DNS 이름을 제공 해야 합니다. 또한 다음을 수행 해야 합니다.<ul><li>DNS 서버에서 네트워크 컨트롤러의 DNS 이름에 대 한 DNS 동적 업데이트를 구성 합니다.</li><li>DNS 동적 업데이트를 네트워크 컨트롤러 노드만 제한 합니다.</li></ul> |

---

> [!NOTE]
> 멤버 자격이 **Domain Admins**, 또는 이와 동등한이 절차를 수행 하는 데 필요한 최소값입니다.

1. 영역에 대 한 DNS 동적 업데이트를 허용 합니다.

   a. DNS 관리자를 열고 콘솔 트리에서 해당 영역을 마우스 오른쪽 단추로 클릭 하 고 클릭 **속성**합니다. 

   b. 에 **일반적인** 탭, 영역 유형 중 하나 인지 확인 **주** 또는 **Active Directory 통합**합니다.

   c. **동적 업데이트**, 되어 있는지 확인 **보안 된 항목만** 를 선택한 다음 클릭 **확인**합니다.

2. 네트워크 컨트롤러 노드에 대 한 DNS 영역 보안 권한을 구성합니다

   a.  클릭 하 고 **보안** 탭을 클릭 한 후 **고급**합니다. 

   b. **Advanced Security Settings**, 클릭 **추가**합니다. 

   c. **보안 주체 선택**을 클릭합니다. 

   d. 에 **사용자, 컴퓨터, 서비스 계정 또는 그룹 선택** 대화 상자, 클릭 **개체 유형**합니다. 

   e. **개체 유형**를 선택 **컴퓨터**를 클릭 하 고 **확인**합니다.

   f. 에 **사용자, 컴퓨터, 서비스 계정 또는 그룹 선택** 대화 상자에서 배포에서 네트워크 컨트롤러 노드 중 하나의 NetBIOS 이름을 입력 하 고 클릭 **확인**합니다.

   g. **사용 권한 항목**, 다음 값을 확인 합니다.

      - **형식** = 허용
      - **적용할** =이 개체 및 모든 하위 개체

   h. **사용 권한**를 선택 **모든 속성 쓰기** 및 **삭제**를 클릭 하 고 **확인**합니다.

3. 네트워크 컨트롤러 클러스터의 모든 컴퓨터 및 Vm에 대해 반복 합니다.

### <a name="step-4-configure-service-principal-name-if-using-kerberos-based-authentication"></a>4단계. Kerberos를 사용 하 여 인증을 기반으로 하는 경우 서비스 주체 이름 구성

네트워크 컨트롤러 관리 클라이언트와의 통신에 Kerberos 기반 인증을 사용 하는, 경우에 Active Directory에서 네트워크 컨트롤러에 대 한를 이름 SPN (서비스 사용자)를 구성 해야 합니다. 네트워크 컨트롤러는 자동으로 SPN을 구성합니다. 하기만 하면 등록 하 고 SPN을 수정 하는 네트워크 컨트롤러 컴퓨터에 대 한 권한을 제공 하는 것입니다. 자세한 내용은 참조 하세요. [구성 이름 SPN (서비스 사용자)](https://docs.microsoft.com/windows-server/networking/sdn/security/kerberos-with-spn#configure-service-principal-names-spn)합니다.

## <a name="deployment-options"></a>배포 옵션

### <a name="network-controller-deployment"></a>네트워크 컨트롤러 배포

가상 컴퓨터에 구성 된 세 가지 네트워크 컨트롤러 노드를 사용 하 여 설치를 항상 사용 가능한 경우 두 가상 서브넷으로 분리 된 테 넌 트 2의 가상 네트워크를 사용 하 여 두 명의 테 넌 트가 웹 계층과 데이터베이스 계층을 시뮬레이션은 표시 됩니다.  

![SDN NC 계획](../../media/Plan-a-Software-Defined-Network-Infrastructure/SDN-NC-Planning.png)

### <a name="network-controller-and-software-load-balancer-deployment"></a>네트워크 컨트롤러 및 소프트웨어 부하 분산 장치 배포

고가용성, SLB/MUX 노드 두 개 이상 있습니다.

![SDN NC 계획](../../media/Plan-a-Software-Defined-Network-Infrastructure/SDN-SLB-Deployment.png)

### <a name="network-controller-software-load-balancer-and-ras-gateway-deployment"></a>네트워크 컨트롤러, 소프트웨어 부하 분산 장치 및 RAS 게이트웨이 배포

세 개의 게이트웨이 가상 컴퓨터가; 둘은 활성화 하 고 하나는 중복 키를 누릅니다.

![SDN NC 계획](../../media/Plan-a-Software-Defined-Network-Infrastructure/SDN-GW-Deployment.png)  



TP5 기반 배포 자동화, Active Directory 사용 가능 하 고 이러한 서브넷에서 연결할 수 있어야 합니다. Active Directory에 대 한 자세한 내용은 참조 하세요. [Active Directory Domain Services 개요](https://docs.microsoft.com/windows-server/identity/ad-ds/get-started/virtual-dc/active-directory-domain-services-overview)합니다.  

>[!IMPORTANT] 
>VMM을 사용 하 여 배포 하는 경우 확인 인프라 가상 컴퓨터 (VMM 서버에 AD/DNS, SQL Server, 등)이 다이어그램에서는 4 명의 호스트 중 하나에서 호스트 되지 않으므로 합니다.  


## <a name="next-steps"></a>다음 단계
[소프트웨어 정의 네트워크 인프라 계획](https://technet.microsoft.com/windows-server-docs/networking/sdn/plan/plan-a-software-defined-network-infrastructure)합니다.

## <a name="related-topics"></a>관련 항목
- [네트워크 컨트롤러](../technologies/network-controller/Network-Controller.md) 
- [네트워크 컨트롤러에 대 한 고가용성 정보](../technologies/network-controller/network-controller-high-availability.md) 
- [Windows PowerShell을 사용하여 네트워크 컨트롤러 배포](../deploy/Deploy-Network-Controller-using-Windows-PowerShell.md)   
- [서버 관리자를 사용하여 네트워크 컨트롤러 서버 역할 설치](../technologies/network-controller/Install-the-Network-Controller-server-role-using-Server-Manager.md)   
