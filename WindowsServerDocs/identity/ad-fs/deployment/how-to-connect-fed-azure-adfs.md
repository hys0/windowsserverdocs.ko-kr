---
title: Azure의 Active Directory Federation Services | Microsoft Docs
description: 이 문서에서는 Azure에서 high 가용성에 AD FS를 배포 하는 방법에 대해 설명 합니다.
services: active-directory
documentationcenter: ''
author: billmath
manager: mtillman
editor: ''
ms.assetid: 692a188c-badc-44aa-ba86-71c0e8074510
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 10/28/2018
ms.subservice: hybrid
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 15ebf21973f78ad705aca77e178005dfa9529cf2
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70868222"
---
# <a name="deploying-active-directory-federation-services-in-azure"></a>Azure에서 Active Directory Federation Services 배포
AD FS은 간소화 된 보안 id 페더레이션 및 SSO (Web Single Sign-On) 기능을 제공 합니다. Azure AD 또는 O365을 사용한 페더레이션을 통해 사용자는 온-프레미스 자격 증명을 사용 하 여 인증 하 고 클라우드의 모든 리소스에 액세스할 수 있습니다. 따라서 온-프레미스와 클라우드 모두에서 리소스에 대 한 액세스를 보장 하기 위해 항상 사용 가능한 AD FS 인프라를 사용 하는 것이 중요 합니다. Azure에 AD FS를 배포 하면 최소한의 노력으로 고가용성을 유지할 수 있습니다.
Azure에 AD FS을 배포 하는 경우 몇 가지 이점이 있습니다. 그 중 몇 가지는 아래에 나열 되어 있습니다.

* **고가용성-Azure** 가용성 집합의 기능을 사용 하면 항상 사용 가능한 인프라를 보장할 수 있습니다.
* **크기 조정** -더 많은 성능이 필요 한가요? Azure에서 몇 번의 클릭 만으로 더 강력한 컴퓨터로 손쉽게 마이그레이션
* **지역 간 중복성** – Azure 지역 중복성을 통해 인프라를 전 세계에서 항상 사용 가능 하도록 보장할 수 있습니다.
* **관리 용이** – Azure Portal에서 매우 단순화 된 관리 옵션을 사용 하 여 인프라를 관리 하는 것은 매우 쉽고 자유롭게 수행할 수 있습니다. 

## <a name="design-principles"></a>디자인 원칙
![배포 디자인](./media/how-to-connect-fed-azure-adfs/deployment.png)

위의 다이어그램에서는 Azure에서 AD FS 인프라 배포를 시작 하는 데 권장 되는 기본 토폴로지를 보여 줍니다. 토폴로지의 다양 한 구성 요소에 대 한 원리는 다음과 같습니다.

* **DC/ADFS 서버**: 사용자가 1000 명 미만이 면 도메인 컨트롤러에 AD FS 역할을 설치 하기만 하면 됩니다. 도메인 컨트롤러에 대 한 성능 영향을 원하지 않거나 사용자가 1000 이상인 경우 별도의 서버에 AD FS를 배포 합니다.
* **WAP 서버** – 사용자가 회사 네트워크에 있지 않은 경우에도 AD FS에 도달할 수 있도록 웹 응용 프로그램 프록시 서버를 배포 해야 합니다.
* **DMZ**: 웹 응용 프로그램 프록시 서버는 DMZ에 배치 되며 DMZ와 내부 서브넷 사이에는 TCP/443 액세스만 허용 됩니다.
* **부하 분산 장치**: AD FS 및 웹 응용 프로그램 프록시 서버의 고가용성을 보장 하려면 AD FS 서버 및 웹 응용 프로그램 프록시 서버에 대 한 Azure Load Balancer 내부 부하 분산 장치를 사용 하는 것이 좋습니다.
* **가용성 집합**: AD FS 배포에 중복성을 제공 하려면 유사한 워크 로드에 대 한 가용성 집합에서 두 개 이상의 가상 머신을 그룹화 하는 것이 좋습니다. 이 구성은 계획 된 유지 관리 또는 계획 되지 않은 유지 관리 이벤트 중에 하나 이상의 가상 머신을 사용할 수 있게 합니다.
* **저장소 계정**: 저장소 계정 두 개를 포함 하는 것이 좋습니다. 단일 저장소 계정이 있으면 단일 실패 지점이 생성 될 수 있으며, 저장소 계정이 다운 되는 경우가 거의 없는 시나리오에서 배포를 사용할 수 없게 될 수 있습니다. 저장소 계정 두 개는 각 오류 라인에 대해 하나의 저장소 계정을 연결 하는 데 도움이 됩니다.
* **네트워크 분리**:  웹 응용 프로그램 프록시 서버를 별도의 DMZ 네트워크에 배포 해야 합니다. 하나의 가상 네트워크를 두 개의 서브넷으로 나눈 다음 격리 된 서브넷에 웹 응용 프로그램 프록시 서버를 배포할 수 있습니다. 각 서브넷에 대 한 네트워크 보안 그룹 설정을 구성 하 고 두 서브넷 간에 필요한 통신만 허용할 수 있습니다. 자세한 내용은 아래 배포 시나리오 별로 제공 됩니다.

## <a name="steps-to-deploy-ad-fs-in-azure"></a>Azure에서 AD FS를 배포 하는 단계
이 섹션에 설명 된 단계는 Azure에서 아래와 같은 AD FS 인프라를 배포 하기 위한 가이드를 간략히 설명 합니다.

### <a name="1-deploying-the-network"></a>1. 네트워크 배포
위에서 설명한 대로 단일 가상 네트워크에 두 개의 서브넷을 만들거나 두 개의 완전히 다른 가상 네트워크 (VNet)를 만들 수 있습니다. 이 문서에서는 단일 가상 네트워크를 배포 하 고 두 개의 서브넷으로 나누는 방법에 대해 집중적으로 설명 합니다. 이는 서로 다른 두 개의 Vnet 통신을 위한 VNet 간 게이트웨이가 필요 하기 때문에 현재 보다 쉬운 방법입니다.

**1.1 가상 네트워크 만들기**

![가상 네트워크 만들기](./media/how-to-connect-fed-azure-adfs/deploynetwork1.png)

Azure Portal에서 가상 네트워크를 선택 하 고 한 번의 클릭으로 가상 네트워크와 서브넷 하나를 즉시 배포할 수 있습니다. INT 서브넷도 정의 되며 이제 Vm을 추가할 준비가 됩니다.
다음 단계는 네트워크 (예: DMZ 서브넷)에 다른 서브넷을 추가 하는 것입니다. DMZ 서브넷을 만들려면 간단히

* 새로 만든 네트워크를 선택 합니다.
* 속성에서 서브넷 선택
* 서브넷 패널에서 추가 단추를 클릭 합니다.
* 서브넷을 만들 서브넷 이름 및 주소 공간 정보를 제공 합니다.

![Subnet](./media/how-to-connect-fed-azure-adfs/deploynetwork2.png)

![서브넷 DMZ](./media/how-to-connect-fed-azure-adfs/deploynetwork3.png)

**1.2. 네트워크 보안 그룹 만들기**

NSG (네트워크 보안 그룹)에는 Virtual Network의 VM 인스턴스에 대 한 네트워크 트래픽을 허용 하거나 거부 하는 ACL (Access Control 목록) 규칙 목록이 포함 되어 있습니다. NSGs는 서브넷 또는 서브넷 내의 개별 VM 인스턴스 중 하나에 연결할 수 있습니다. NSG가 서브넷에 연결 된 경우 ACL 규칙은 해당 서브넷의 모든 VM 인스턴스에 적용 됩니다.
이 지침의 목적을 위해 내부 네트워크와 DMZ 각각에 해당 하는 두 개의 NSGs를 만듭니다. 각각 NSG_INT 및 NSG_DMZ 레이블이 지정 됩니다.

![NSG 만들기](./media/how-to-connect-fed-azure-adfs/creatensg1.png)

NSG를 만든 후에는 0 인바운드 및 아웃 바운드 규칙이 0이 됩니다. 각 서버의 역할이 설치 되 고 작동 하면 원하는 보안 수준에 따라 인바운드 및 아웃 바운드 규칙을 만들 수 있습니다.

![NSG 초기화](./media/how-to-connect-fed-azure-adfs/nsgint1.png)

NSGs를 만든 후 NSG_INT를 서브넷 INT와 NSG_DMZ와 서브넷 DMZ와 연결 합니다. 예제 스크린샷에서는 다음과 같습니다.

![NSG 구성](./media/how-to-connect-fed-azure-adfs/nsgconfigure1.png)

* 서브넷을 클릭 하 여 서브넷에 대 한 패널을 엽니다.
* NSG와 연결할 서브넷을 선택 합니다. 

구성 후에 서브넷에 대 한 패널은 다음과 같이 표시 됩니다.

![NSG 후의 서브넷](./media/how-to-connect-fed-azure-adfs/nsgconfigure2.png)

**1.3. 온-프레미스에 대 한 연결 만들기**

Azure에서 DC (도메인 컨트롤러)를 배포 하기 위해 온-프레미스에 연결 해야 합니다. Azure는 온-프레미스 인프라를 Azure 인프라에 연결 하는 다양 한 연결 옵션을 제공 합니다.

* 지점 및 사이트 간
* 사이트 간 Virtual Network
* ExpressRoute

Express 경로를 사용 하는 것이 좋습니다. Express 경로를 사용 하면 온-프레미스 또는 공동 배치 환경의 인프라와 Azure 데이터 센터 간에 개인 연결을 만들 수 있습니다. ExpressRoute 연결은 공용 인터넷을 통해 이동하지 않습니다. 인터넷을 통한 일반 연결 보다 안정성, 빠른 속도, 짧은 대기 시간 및 높은 보안을 제공 합니다.
Express 경로를 사용 하는 것이 좋지만 조직에 가장 적합 한 연결 방법을 선택할 수 있습니다. Express 경로 및 express 경로를 사용 하는 다양 한 연결 옵션에 대해 자세히 알아보려면 [express 경로 기술 개요](https://aka.ms/Azure/ExpressRoute)를 참조 하세요.

### <a name="2-create-storage-accounts"></a>2. 저장소 계정 만들기
고가용성을 유지 하 고 단일 저장소 계정에 대 한 종속성을 방지 하기 위해 두 개의 저장소 계정을 만들 수 있습니다. 각 가용성 집합의 컴퓨터를 두 그룹으로 나누고 각 그룹에 별도의 저장소 계정을 할당 합니다.

![저장소 계정 만들기](./media/how-to-connect-fed-azure-adfs/storageaccount1.png)

### <a name="3-create-availability-sets"></a>3. 가용성 집합 만들기
각 역할 (DC/AD FS 및 WAP)에 대해 최소한 두 대의 컴퓨터를 포함 하는 가용성 집합을 만듭니다. 이렇게 하면 각 역할의 가용성을 높일 수 있습니다. 가용성 집합을 만드는 동안 다음을 결정 해야 합니다.

* **장애 도메인**: 동일한 장애 도메인의 가상 머신은 동일한 전원 및 실제 네트워크 스위치를 공유 합니다. 최소 2 개의 장애 도메인을 권장 합니다. 기본값은 3 이며이 배포의 목적으로 그대로 둘 수 있습니다.
* **도메인 업데이트**: 동일한 업데이트 도메인에 속하는 컴퓨터는 업데이트 중에 함께 다시 시작 됩니다. 최소 2 개의 업데이트 도메인이 필요 합니다. 기본값은 5 이며이 배포의 목적으로 그대로 둘 수 있습니다.

![가용성 집합](./media/how-to-connect-fed-azure-adfs/availabilityset1.png)

다음 가용성 집합 만들기

| 가용성 집합 | 역할 | 오류 도메인 | 업데이트 도메인 |
|:---:|:---:|:---:|:--- |
| contosodcset |DC/ADFS |3 |5 |
| contosowapset |WAP |3 |5 |

### <a name="4-deploy-virtual-machines"></a>4. 가상 컴퓨터 배포
다음 단계는 인프라에서 다양 한 역할을 호스트 하는 가상 컴퓨터를 배포 하는 것입니다. 각 가용성 집합에는 최소 두 대의 컴퓨터를 사용 하는 것이 좋습니다. 기본 배포용으로 4 대의 가상 머신을 만듭니다.

| Machine | 역할 | Subnet | 가용성 집합 | Storage 계정 | IP 주소 |
|:---:|:---:|:---:|:---:|:---:|:---:|
| contosodc1 |DC/ADFS |INT |contosodcset |contososac1 |정적 |
| contosodc2 |DC/ADFS |INT |contosodcset |contososac2 |정적 |
| contosowap1 |WAP |DMZ |contosowapset |contososac1 |정적 |
| contosowap2 |WAP |DMZ |contosowapset |contososac2 |정적 |

알 수 있듯이 NSG가 지정 되지 않았습니다. Azure가 서브넷 수준에서 NSG를 사용할 수 있기 때문입니다. 그런 다음 서브넷 또는 NIC 개체와 연결 된 개별 NSG를 사용 하 여 컴퓨터 네트워크 트래픽을 제어할 수 있습니다. [NSG (네트워크 보안 그룹) 란?](https://aka.ms/Azure/NSG)을 참조 하세요.
DNS를 관리 하는 경우 고정 IP 주소를 권장 합니다. 도메인에 대 한 DNS 레코드 대신 Azure DNS 및를 사용할 수 있습니다. Azure Fqdn으로 새 컴퓨터를 참조 하세요.
배포가 완료 되 면 가상 머신 창이 아래와 같이 표시 됩니다.

![배포 Virtual Machines](./media/how-to-connect-fed-azure-adfs/virtualmachinesdeployed_noadfs.png)

### <a name="5-configuring-the-domain-controller--ad-fs-servers"></a>5. 도메인 컨트롤러/AD FS 서버 구성
 들어오는 요청을 인증 하기 위해 AD FS는 도메인 컨트롤러에 연결 해야 합니다. 인증을 위해 Azure에서 온-프레미스 DC로 비용을 절감할 수 있도록 하려면 Azure에서 도메인 컨트롤러의 복제본을 배포 하는 것이 좋습니다. 고가용성을 얻기 위해서는 도메인 컨트롤러 2 개 이상의 가용성 집합을 만드는 것이 좋습니다.

| 도메인 컨트롤러 | 역할 | Storage 계정 |
|:---:|:---:|:---:|
| contosodc1 |복제본 |contososac1 |
| contosodc2 |복제본 |contososac2 |

* DNS를 사용 하 여 두 서버를 복제본 도메인 컨트롤러로 승격
* 서버 관리자를 사용 하 여 AD FS 역할을 설치 하 여 AD FS 서버를 구성 합니다.

### <a name="6-deploying-internal-load-balancer-ilb"></a>6. ILB (내부 Load Balancer 배포)
**6.1. ILB 만들기**

ILB를 배포 하려면 Azure Portal에서 부하 분산 장치를 선택 하 고 추가 (+)를 클릭 합니다.

> [!NOTE]
> 메뉴에 **부하 분산 장치가** 표시 되지 않으면 포털의 왼쪽 아래에서 **찾아보기** 를 클릭 하 고 **부하 분산 장치가**표시 될 때까지 스크롤합니다.  노란색 별표를 클릭 하 여 메뉴에 추가 합니다. 이제 새 부하 분산 장치 아이콘을 선택 하 여 패널을 열고 부하 분산 장치 구성을 시작 합니다.
> 
> 

![부하 분산 장치 찾아보기](./media/how-to-connect-fed-azure-adfs/browseloadbalancer.png)

* **이름**: 부하 분산 장치에 적절 한 이름을 지정 합니다.
* **구성표**: 이 부하 분산 장치는 AD FS 서버 앞에 배치 되 고 내부 네트워크 연결용 으로만 사용할 수 있으므로 "내부"를 선택 합니다.
* **Virtual Network**: AD FS를 배포할 가상 네트워크를 선택 합니다.
* **서브넷**: 여기에서 내부 서브넷을 선택 하세요.
* **IP 주소 할당**: 정적

![내부 부하 분산 장치](./media/how-to-connect-fed-azure-adfs/ilbdeployment1.png)

만들기를 클릭 하 고 ILB가 배포 되 면 부하 분산 장치 목록에 표시 됩니다.

![ILB 후 부하 분산 장치](./media/how-to-connect-fed-azure-adfs/ilbdeployment2.png)

다음 단계는 백 엔드 풀과 백 엔드 프로브를 구성 하는 것입니다.

**6.2. ILB 백 엔드 풀 구성**

부하 분산 장치 패널에서 새로 만든 ILB를 선택 합니다. 그러면 설정 패널이 열립니다. 

1. 설정 패널에서 백 엔드 풀을 선택 합니다.
2. 백 엔드 풀 추가 패널에서 가상 머신 추가를 클릭 합니다.
3. 가용성 집합을 선택할 수 있는 패널이 표시 됩니다.
4. AD FS 가용성 집합을 선택 합니다.

![ILB 백 엔드 풀 구성](./media/how-to-connect-fed-azure-adfs/ilbdeployment3.png)

**6.3. 프로브 구성**

ILB 설정 패널에서 상태 프로브를 선택 합니다.

1. 추가를 클릭 합니다.
2. 프로브 a에 대 한 세부 정보를 제공 합니다. **이름**: 프로브 이름 b. **프로토콜**: HTTP c. **포트**: 80 (HTTP) d. **경로**:/adfs/probe e. **간격**: 5 (기본값)-ILB가 백 엔드 풀의 컴퓨터를 검색 하는 간격입니다. **비정상 임계값 제한**: 2 (기본값)-ILB가 백 엔드 풀의 컴퓨터를 응답 하지 않는 것으로 선언 하 고 해당 컴퓨터에 대 한 트래픽 전송을 중지 하는 연속 프로브 실패의 임계값입니다.

![ILB 프로브 구성](./media/how-to-connect-fed-azure-adfs/ilbdeployment4.png)

전체 HTTPS 경로 검사를 수행할 수 없는 AD FS 환경의 상태 검사에 대해 명시적으로 만든/adfs/probe 끝점을 사용 하 고 있습니다.  이는 최신 AD FS 배포의 상태를 정확 하 게 반영 하지 않는 기본 포트 443 검사 보다 크게 좋습니다.  이에 대 한 자세한 내용은에서 https://blogs.technet.microsoft.com/applicationproxyblog/2014/10/17/hardware-load-balancer-health-checks-and-web-application-proxy-ad-fs-2012-r2/ 찾을 수 있습니다.

**6.4. 부하 분산 규칙 만들기**

트래픽 분산을 위해 ILB는 부하 분산 규칙을 사용 하 여 구성 해야 합니다. 부하 분산 규칙을 만들려면 

1. ILB의 설정 패널에서 부하 분산 규칙을 선택 합니다.
2. 부하 분산 규칙 패널에서 추가를 클릭 합니다.
3. 부하 분산 규칙 패널 a를 추가 합니다. **이름**: 규칙 b의 이름을 제공 합니다. **프로토콜**: TCP c를 선택 합니다. **포트**: 443 d. **백 엔드 포트**: 443 e. **백 엔드 풀**: 이전 f에 AD FS 클러스터에 대해 만든 풀을 선택 합니다. **프로브**: 이전에 AD FS 서버에 대해 만든 프로브를 선택 합니다.

![ILB 분산 규칙 구성](./media/how-to-connect-fed-azure-adfs/ilbdeployment5.png)

**6.5. ILB를 사용 하 여 DNS 업데이트**

DNS 서버로 이동 하 고 ILB에 대 한 CNAME을 만듭니다. CNAME은 ILB의 IP 주소를 가리키는 IP 주소를 사용 하 여 페더레이션 서비스에 대 한 것 이어야 합니다. 예를 들어 ILB DIP 주소가 10.3.0.8이 고 페더레이션 서비스가 설치 된 경우 fs.contoso.com를 가리키는 fs.contoso.com에 대 한 CNAME을 만듭니다.
이렇게 하면 fs.contoso.com 관련 된 모든 통신이 ILB에서 종료 되 고 적절 하 게 라우팅됩니다.

### <a name="7-configuring-the-web-application-proxy-server"></a>7. 웹 응용 프로그램 프록시 서버 구성
**7.1. AD FS 서버에 연결 하도록 웹 응용 프로그램 프록시 서버 구성**

웹 응용 프로그램 프록시 서버가 ILB 뒤의 AD FS 서버에 연결할 수 있도록 하려면 ILB에 대 한%systemroot%\system32\drivers\etc\hosts에 레코드를 만듭니다. DN (고유 이름)은 페더레이션 서비스 이름 (예: fs.contoso.com) 이어야 합니다. 그리고 IP 항목은 ILB의 IP 주소 (예: 10.3.0.8)의 IP 주소 여야 합니다.

**7.2. 웹 응용 프로그램 프록시 역할 설치**

웹 응용 프로그램 프록시 서버가 ILB 뒤의 AD FS 서버에 연결할 수 있는지 확인 한 후 웹 응용 프로그램 프록시 서버를 다음에 설치할 수 있습니다. 웹 응용 프로그램 프록시 서버는 도메인에 가입할 필요가 없습니다. 원격 액세스 역할을 선택 하 여 두 웹 응용 프로그램 프록시 서버에 웹 응용 프로그램 프록시 역할을 설치 합니다. 서버 관리자는 WAP 설치를 완료 하는 방법을 안내 합니다.
WAP를 배포 하는 방법에 대 한 자세한 내용은 [웹 응용 프로그램 프록시 서버 설치 및 구성](https://technet.microsoft.com/library/dn383662.aspx)을 참조 하세요.

### <a name="8--deploying-the-internet-facing-public-load-balancer"></a>8.  인터넷 연결 (공용) Load Balancer
**8.1.  인터넷 연결 (공용) Load Balancer 만들기**

Azure Portal에서 부하 분산 장치를 선택 하 고 추가를 클릭 합니다. 부하 분산 장치 만들기 패널에서 다음 정보를 입력 합니다.

1. **이름**: 부하 분산 장치의 이름
2. **구성표**: 공용 –이 옵션은이 부하 분산 장치에 공용 주소가 필요 함을 Azure에 알려 줍니다.
3. **IP 주소**: 새 IP 주소 만들기 (동적)

![인터넷 연결 부하 분산 장치](./media/how-to-connect-fed-azure-adfs/elbdeployment1.png)

배포 후 부하 분산 장치는 부하 분산 장치 목록에 표시 됩니다.

![부하 분산 장치 목록](./media/how-to-connect-fed-azure-adfs/elbdeployment2.png)

**8.2. 공용 IP에 DNS 레이블 할당**

부하 분산 장치 패널에서 새로 만든 부하 분산 장치 항목을 클릭 하 여 구성에 대 한 패널을 표시 합니다. 아래 단계를 수행 하 여 공용 IP에 대 한 DNS 레이블을 구성 합니다.

1. 공용 IP 주소를 클릭 합니다. 그러면 공용 IP 및 해당 설정에 대 한 패널이 열립니다.
2. 구성 클릭
3. DNS 레이블을 제공 합니다. 모든 위치에서 액세스할 수 있는 공용 DNS 레이블이 됩니다 (예: contosofs.westus.cloudapp.azure.com). 외부 부하 분산 장치 (contosofs.westus.cloudapp.azure.com)의 DNS 레이블로 확인 되는 페더레이션 서비스 (예: fs.contoso.com)의 외부 DNS에 항목을 추가할 수 있습니다.

![인터넷 연결 부하 분산 장치 구성](./media/how-to-connect-fed-azure-adfs/elbdeployment3.png) 

![인터넷 연결 부하 분산 장치 구성 (DNS)](./media/how-to-connect-fed-azure-adfs/elbdeployment4.png)

**8.3. 인터넷 연결 (공용) Load Balancer에 대 한 백 엔드 풀 구성** 

내부 부하 분산 장치를 만들 때와 동일한 단계를 수행 하 여 인터넷 연결 (공용) Load Balancer 백 엔드 풀을 WAP 서버에 대 한 가용성 집합으로 구성 합니다. 예를 들면 contosowapset입니다.

![인터넷 연결 Load Balancer 백 엔드 풀 구성](./media/how-to-connect-fed-azure-adfs/elbdeployment5.png)

**8.4. 프로브 구성**

내부 부하 분산 장치를 구성 하는 것과 동일한 단계를 따라 WAP 서버의 백 엔드 풀에 대 한 프로브를 구성 합니다.

![인터넷 연결 Load Balancer 프로브 구성](./media/how-to-connect-fed-azure-adfs/elbdeployment6.png)

**8.5. 부하 분산 규칙 만들기**

ILB와 동일한 단계를 수행 하 여 TCP 443에 대 한 부하 분산 규칙을 구성 합니다.

![인터넷 연결 Load Balancer의 분산 규칙 구성](./media/how-to-connect-fed-azure-adfs/elbdeployment7.png)

### <a name="9-securing-the-network"></a>9. 네트워크 보안
**9.1. 내부 서브넷 보안**

전반적으로 내부 서브넷을 효율적으로 보호 하기 위해 다음 규칙이 필요 합니다 (아래 나열 된 순서 대로).

| 규칙 | 설명 | 흐름 |
|:--- |:--- |:---:|
| AllowHTTPSFromDMZ |DMZ에서 HTTPS 통신 허용 |인바운드 |
| DenyInternetOutbound |인터넷에 대 한 액세스 권한 없음 |아웃바운드 |

![INT 액세스 규칙 (인바운드)](./media/how-to-connect-fed-azure-adfs/nsg_int.png)

**9.2. DMZ 서브넷 보안**

| 규칙 | 설명 | 흐름 |
|:--- |:--- |:---:|
| AllowHTTPSFromInternet |인터넷에서 DMZ로의 HTTPS 허용 |인바운드 |
| DenyInternetOutbound |인터넷에 대 한 HTTPS를 제외한 모든 항목이 차단 됩니다. |아웃바운드 |

![EXT 액세스 규칙 (인바운드)](./media/how-to-connect-fed-azure-adfs/nsg_dmz.png)

> [!NOTE]
> 클라이언트 사용자 인증서 인증 (X509 사용자 인증서를 사용 하는 clientTLS 인증)이 필요한 경우 AD FS TCP 포트 49443이 인바운드 액세스를 사용 하도록 설정 되어 있어야 합니다.
> 
> 

### <a name="10-test-the-ad-fs-sign-in"></a>10. AD FS 로그인 테스트
가장 쉬운 방법은 Idpinitiatedsignon.aspx 페이지를 사용 하 여 AD FS를 테스트 하는 것입니다. 이 작업을 수행 하려면 AD FS 속성에 대해 Idpinitiatedsignon.aspx를 사용 하도록 설정 해야 합니다. 아래 단계에 따라 AD FS 설치를 확인 합니다.

1. PowerShell을 사용 하 여 AD FS 서버에서 아래 cmdlet을 실행 하 여 사용으로 설정 합니다.
   Set-adfsproperties-EnableIdPInitiatedSignonPage $true 
2. 외부 컴퓨터에서 https:\//adfs-server.contoso.com/adfs/ls/IdpInitiatedSignon.aspx에 액세스 합니다.  
3. 다음과 같이 AD FS 페이지가 표시 됩니다.

![테스트 로그인 페이지](./media/how-to-connect-fed-azure-adfs/test1.png)

성공적으로 로그인 하면 아래와 같은 성공 메시지가 표시 됩니다.

![테스트 성공](./media/how-to-connect-fed-azure-adfs/test2.png)

## <a name="template-for-deploying-ad-fs-in-azure"></a>Azure에서 AD FS를 배포 하기 위한 템플릿
템플릿은 도메인 컨트롤러, AD FS 및 WAP 각각에 대 한 6 개의 컴퓨터 설치를 배포 합니다.

[Azure 배포 템플릿의 AD FS](https://github.com/paulomarquesc/adfs-6vms-regular-template-based)

이 템플릿을 배포 하는 동안 기존 가상 네트워크를 사용 하거나 새 VNET을 만들 수 있습니다. 배포를 사용자 지정 하는 데 사용할 수 있는 다양 한 매개 변수는 배포 프로세스의 매개 변수 사용에 대 한 설명과 함께 아래에 나열 되어 있습니다. 

| 매개 변수 | 설명 |
|:--- |:--- |
| 위치 |리소스를 배포할 지역 (예: 미국 동부)입니다. |
| StorageAccountType |만든 저장소 계정의 유형입니다. |
| VirtualNetworkUsage |새 가상 네트워크를 만들 것인지 기존 가상 네트워크를 사용할 것인지를 나타냅니다. |
| VirtualNetworkName |만들 Virtual Network의 이름입니다. 기존 또는 새 가상 네트워크 사용에 모두 필요 합니다. |
| VirtualNetworkResourceGroupName |기존 가상 네트워크가 있는 리소스 그룹의 이름을 지정 합니다. 기존 가상 네트워크를 사용 하는 경우이 매개 변수가 필수 매개 변수가 되므로 배포가 기존 가상 네트워크의 ID를 찾을 수 있습니다. |
| VirtualNetworkAddressRange |새 가상 네트워크를 만들 경우 새 VNET의 주소 범위는 필수입니다. |
| InternalSubnetName |내부 서브넷의 이름입니다. 두 가상 네트워크 사용 옵션 (신규 또는 기존)에서 필수입니다. |
| InternalSubnetAddressRange |도메인 컨트롤러 및 ADFS 서버를 포함 하는 내부 서브넷의 주소 범위는 새 가상 네트워크를 만들 경우 필수입니다. |
| DMZSubnetAddressRange |Windows 응용 프로그램 프록시 서버를 포함 하는 dmz 서브넷의 주소 범위는 새 가상 네트워크를 만들 경우 필수입니다. |
| DMZSubnetName |내부 서브넷의 이름으로, 두 가상 네트워크 사용 옵션 (신규 또는 기존)에서 모두 필수입니다. |
| ADDC01NICIPAddress |첫 번째 도메인 컨트롤러의 내부 IP 주소인이 IP 주소는 DC에 정적으로 할당 되 고 내부 서브넷 내에서 유효한 ip 주소 여야 합니다. |
| ADDC02NICIPAddress |두 번째 도메인 컨트롤러의 내부 IP 주소인이 IP 주소는 DC에 정적으로 할당 되 고 내부 서브넷 내에서 유효한 ip 주소 여야 합니다. |
| ADFS01NICIPAddress |첫 번째 ADFS 서버의 내부 IP 주소인이 IP 주소는 ADFS 서버에 정적으로 할당 되 고 내부 서브넷 내에서 유효한 ip 주소 여야 합니다. |
| ADFS02NICIPAddress |두 번째 ADFS 서버의 내부 IP 주소인이 IP 주소는 ADFS 서버에 정적으로 할당 되 고 내부 서브넷 내에서 유효한 ip 주소 여야 합니다. |
| WAP01NICIPAddress |첫 번째 WAP 서버의 내부 IP 주소인이 IP 주소는 WAP 서버에 정적으로 할당 되 고 DMZ 서브넷 내에서 유효한 ip 주소 여야 합니다. |
| WAP02NICIPAddress |두 번째 WAP 서버의 내부 IP 주소인이 IP 주소는 WAP 서버에 정적으로 할당 되 고 DMZ 서브넷 내에서 유효한 ip 주소 여야 합니다. |
| ADFSLoadBalancerPrivateIPAddress |ADFS 부하 분산 장치의 내부 IP 주소는이 IP 주소는 부하 분산 장치에 정적으로 할당 되 고 내부 서브넷 내에서 유효한 ip 주소 여야 합니다. |
| ADDCVMNamePrefix |도메인 컨트롤러에 대 한 가상 컴퓨터 이름 접두사 |
| ADFSVMNamePrefix |ADFS 서버에 대 한 가상 컴퓨터 이름 접두사 |
| WAPVMNamePrefix |WAP 서버에 대 한 가상 머신 이름 접두사 |
| ADDCVMSize |도메인 컨트롤러의 vm 크기 |
| ADFSVMSize |ADFS 서버의 vm 크기 |
| WAPVMSize |WAP 서버의 vm 크기 |
| AdminUserName |가상 컴퓨터의 로컬 관리자 이름 |
| adminPassword |가상 컴퓨터의 로컬 관리자 계정에 대 한 암호입니다. |

## <a name="additional-resources"></a>추가 자료
* [가용성 집합](https://aka.ms/Azure/Availability) 
* [Azure Load Balancer](https://aka.ms/Azure/ILB)
* [내부 Load Balancer](https://aka.ms/Azure/ILB/Internal)
* [인터넷 연결 Load Balancer](https://aka.ms/Azure/ILB/Internet)
* [저장소 계정](https://aka.ms/Azure/Storage)
* [Azure 가상 네트워크](https://aka.ms/Azure/VNet)
* [AD FS 및 웹 응용 프로그램 프록시 링크](https://aka.ms/ADFSLinks) 

## <a name="next-steps"></a>다음 단계
* [Azure Active Directory와 온-프레미스 id 통합](https://docs.microsoft.com/azure/active-directory/hybrid/whatis-hybrid-identity)
* [Azure AD Connect를 사용 하 여 AD FS 구성 및 관리](/azure/active-directory/hybrid/how-to-connect-fed-whatis)
* [Azure Traffic Manager를 사용 하 여 Azure에서 고가용성 교차 지리적 AD FS 배포](active-directory-adfs-in-azure-with-azure-traffic-manager.md)
