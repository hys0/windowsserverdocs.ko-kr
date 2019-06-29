---
title: Azure에서 active Directory Federation Services | Microsoft Docs
description: 이 문서에서는 고가용성을 위해 Azure에서 AD FS를 배포 하는 방법을 배웁니다.
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
ms.openlocfilehash: f075f91e97f806555507bfc0e0c5f3d1589a71e6
ms.sourcegitcommit: 63926404009f9e1330a4a0aa8cb9821a2dd7187e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/29/2019
ms.locfileid: "67469646"
---
# <a name="deploying-active-directory-federation-services-in-azure"></a>Azure에서 Active Directory Federation Services 배포
AD FS는 간편 하 고 안전한 id 페더레이션 및 웹에서 single sign-on (SSO) 기능을 제공 합니다. Azure AD와 페더레이션 하거나 O365 온-프레미스 자격 증명을 사용 하 여 인증 하 고 클라우드에서 모든 리소스에에서 액세스 하는 사용자를 사용 하도록 설정 합니다. 결과적으로, 온-프레미스 리소스에 액세스 하려면 항상 사용 가능한 AD FS 인프라를 마련해 야 됩니다 및 클라우드에서 합니다. Azure에서 AD FS 배포 필요한 최소한의 노력으로 고가용성을 달성 하는 데 도움이 됩니다.
Azure에서 AD FS를 배포 하는 몇 가지 이점은, 그 중 일부는 다음과 같습니다.

* **고가용성** -Azure 가용성 집합의 기능을 사용 하 여 항상 사용 가능한 인프라를 해야 합니다.
* **규모 조정 용이** – 더 높은 성능이 필요한? Azure에서 몇 번 클릭 하 여 더 강력한 컴퓨터로 쉽게 마이그레이션하십시오
* **지역간 중복성** – Azure 지역 중복성을 보장할 수 인프라는 전 세계에 걸쳐 항상 사용 가능
* **관리 용이** – Azure portal의 단순화 된 관리 옵션을 사용 하 여 관리 인프라는 매우 간편 하 고 간편한 

## <a name="design-principles"></a>디자인 원칙
![배포 디자인](./media/how-to-connect-fed-azure-adfs/deployment.png)

위의 다이어그램은 Azure에서 AD FS 인프라를 배포 하려면 권장 되는 기본 토폴로지를 보여줍니다. 토폴로지의 다양 한 구성의 원리는 다음과 같습니다.

* **DC / ADFS 서버**: 1,000 개 미만의 사용자가 있는 경우 도메인 컨트롤러에 AD FS 역할을 간단히 설치할 수 있습니다. 도메인 컨트롤러에 성능 영향을 주지 않으려면 또는 1,000 명 이상의 사용자가 있는 경우 별도 서버에서 AD FS를 배포 합니다.
* **WAP 서버** – 사용자가 AD FS 있지 않은 경우 회사 네트워크에도 연결할 수 있도록 웹 응용 프로그램 프록시 서버를 배포 하는 데 필요한 것입니다.
* **DMZ**: 웹 응용 프로그램 프록시 서버는 DMZ에 배치 하 고 DMZ와 내부 서브넷 간에 tcp/443 액세스가 허용 됩니다.
* **부하 분산 장치**: AD FS 및 웹 응용 프로그램 프록시 서버의 고가용성을 위해 웹 응용 프로그램 프록시 서버에 대 한 AD FS 서버 및 Azure Load Balancer에 대 한 내부 부하 분산을 사용 하는 것이 좋습니다.
* **가용성 집합**: AD FS 배포에 중복성을 제공 하려면 비슷한 워크 로드에 대 한 가용성 집합에서 두 개 이상의 가상 머신을 그룹화 하는 것이 좋습니다. 이 구성을 통해 수행 하는 동안 계획 되거나 계획 되지 않은 유지 관리 이벤트를 하나 이상의 가상 머신을 사용할 수 있도록
* **저장소 계정**: 두 개의 저장소 계정을 사용 하는 것이 좋습니다. 단일 저장소 계정을 단일 실패 지점이 생성 될 수 있습니다 하 고 배포를 저장소 계정이 중단 되는 가능성이 적은 시나리오에서 사용할 수 없게 될 수 있습니다. 두 개의 저장소 계정이 각 오류 줄에 하나의 저장소 계정에 연결 하는 데 도움이 됩니다.
* **네트워크 분리**:  웹 응용 프로그램 프록시 서버를 별도 DMZ 네트워크에 배포 해야 합니다. 두 개의 서브넷에 하나의 가상 네트워크를 나눌 수 있으며 다음 격리 된 서브넷에 웹 응용 프로그램 프록시 서버를 배포할 수 있습니다. 각 서브넷에 네트워크 보안 그룹 설정을 구성 하 고 두 서브넷 간에 필요한 통신만 허용 하기만 하면 됩니다. 자세한 내용은 아래 배포 시나리오 별로 지정 됩니다.

## <a name="steps-to-deploy-ad-fs-in-azure"></a>Azure에서 AD FS를 배포 하는 단계
이 섹션에 나와 있는 단계 개요 배포 가이드는 Azure에서 AD FS 인프라와 같이 아래.

### <a name="1-deploying-the-network"></a>1. 네트워크를 배포합니다.
위에서 설명한 대로 있습니다 수 단일 가상 네트워크에서 두 개의 서브넷을 만드는 없거나 두 개의 완전히 다른 가상 네트워크 (VNet)를 만듭니다. 이 문서는 단일 가상 네트워크를 배포 하는 방법에 집중 하 고 두 개의 서브넷으로 분할 됩니다. 현재 두 개의 별도 Vnet 통신용 VNet 대 VNet 게이트웨이 해야 하는 대로 하는 쉬운 방법입니다.

**1.1 가상 네트워크 만들기**

![가상 네트워크 만들기](./media/how-to-connect-fed-azure-adfs/deploynetwork1.png)

Azure portal에서 가상 네트워크를 선택 하 고이 가상 네트워크와 하나의 서브넷만 번의 클릭으로 즉시 배포할 수 있습니다. INT 서브넷을 정의 하 추가할 vm의 경우 이제 준비 되었습니다.
네트워크, 즉 DMZ 서브넷에 다른 서브넷을 추가 하려면 다음 단계가입니다. 단순히 DMZ 서브넷을 만들려면

* 새로 만든된 네트워크 선택
* 속성에서 서브넷 선택
* 서브넷에 패널 추가 단추 클릭
* 서브넷을 만들려는 서브넷 이름 및 주소 공간 정보를 제공 합니다.

![Subnet](./media/how-to-connect-fed-azure-adfs/deploynetwork2.png)

![DMZ 서브넷](./media/how-to-connect-fed-azure-adfs/deploynetwork3.png)

**1.2. 네트워크 보안 그룹 만들기**

네트워크 보안 그룹 (NSG)에 가상 네트워크에 VM 인스턴스에 대 한 네트워크 트래픽을 허용 하거나 거부 하는 액세스 제어 목록 (ACL) 규칙의 목록을 포함 합니다. Nsg는 서브넷 또는 서브넷 내의 개별 VM 인스턴스 중 하나를 사용 하 여 연결할 수 있습니다. NSG를 서브넷과 연결한 경우 ACL 규칙은 서브넷의 모든 VM 인스턴스에 적용 됩니다.
이 지침을 위해 2 개의 Nsg를 만듭니다: DMZ와 내부 네트워크에 대해 각각 1입니다. 레이블이 지정 됩니다 NSG_INT 및 NSG_DMZ 각각.

![NSG 만들기](./media/how-to-connect-fed-azure-adfs/creatensg1.png)

NSG를 만든 후 0 인바운드 및 0 아웃 바운드 규칙이 됩니다. 각 서버의 역할이 설치 되 면 원하는 수준 보안에 따라 인바운드 및 아웃 바운드 규칙을 만들 수 있습니다.

![NSG 초기화](./media/how-to-connect-fed-azure-adfs/nsgint1.png)

Nsg를 만든 후에 nsg_int를 서브넷 INT 및 DMZ 서브넷을 사용 하 여 NSG_DMZ입니다. 스크린 샷 예가 아래에 제공 됩니다.

![NSG 구성](./media/how-to-connect-fed-azure-adfs/nsgconfigure1.png)

* 서브넷에 대 한 패널을 엽니다. 서브넷을 클릭
* NSG와 연결할 서브넷을 선택 합니다. 

구성 후 서브넷에 대 한 패널은 다음과 같이 표시 됩니다.

![NSG 이후 서브넷](./media/how-to-connect-fed-azure-adfs/nsgconfigure2.png)

**1.3. 온-프레미스 간 연결 만들기**

Azure에서 도메인 컨트롤러 (DC)를 배포 하기 위해 온-프레미스에 연결을 해야 합니다. Azure는 Azure 인프라에 온-프레미스 인프라를 연결 하는 다양 한 연결 옵션을 제공 합니다.

* 지점 및 사이트
* 가상 네트워크 사이트 및 사이트 간
* ExpressRoute

ExpressRoute를 사용 하는 것이 좋습니다. ExpressRoute를 사용 하면 온-프레미스 또는 공동 배치 환경의 인프라와 Azure 데이터 센터 간에 개인 연결을 만들 수 있습니다. ExpressRoute 연결은 공용 인터넷을 통해 이동 하지 마십시오. 인터넷을 통해 더 많은 안정성, 빠른 속도, 짧은 대기 시간 및 일반 연결 보다 보안성이 높습니다을 제공합니다.
ExpressRoute를 사용 하는 것이 좋습니다, 조직에 가장 적합 한 연결 방법을 선택할 수 있습니다. ExpressRoute에 대 한 자세한 내용은 및 ExpressRoute를 사용 하 여 다양 한 연결 옵션에 알아보려면 [ExpressRoute 기술 개요](https://aka.ms/Azure/ExpressRoute)합니다.

### <a name="2-create-storage-accounts"></a>2. 저장소 계정 만들기
고가용성을 유지 하 고 단일 저장소 계정에 대 한 종속성을 방지 하기 위해 두 개의 저장소 계정을 만들 수 있습니다. 각 가용성 집합의 컴퓨터를 두 그룹으로 나누는 하 고 각 그룹을 별도 저장소 계정을 할당 합니다.

![저장소 계정 만들기](./media/how-to-connect-fed-azure-adfs/storageaccount1.png)

### <a name="3-create-availability-sets"></a>3. 가용성 집합 만들기
각 역할 (DC/AD FS 및 WAP)에 대 한 최소 2 개의 컴퓨터를 포함 하는 가용성 집합을 만듭니다. 각 역할에 대 한 고가용성을 달성 하는 데 도움이 됩니다. 만들 가용성 집합을 하는 동안 다음 결정 하려면 반드시:

* **장애 도메인**: 동일한 장애 도메인의 가상 머신은 동일한 전원 및 실제 네트워크 스위치를 공유합니다. 최소 2 개의 장애 도메인을 사용 하는 것이 좋습니다. 기본값은 3 및이 배포 목적으로 그대로 둘 수 있습니다.
* **업데이트 도메인**: 동일한 업데이트 도메인에 속한 컴퓨터 업데이트 하는 동안 함께 다시 시작 됩니다. 최소 2 개의 업데이트 도메인이 하려고 합니다. 기본값은 5이 고이 배포 목적으로 그대로 둘 수 있습니다.

![가용성 집합](./media/how-to-connect-fed-azure-adfs/availabilityset1.png)

다음과 같은 가용성 집합 만들기

| 가용성 집합 | 역할 | 오류 도메인 | 업데이트 도메인 |
|:---:|:---:|:---:|:--- |
| contosodcset |DC/ADFS |3 |5 |
| contosowapset |WAP |3 |5 |

### <a name="4-deploy-virtual-machines"></a>4. 가상 컴퓨터 배포
다음 단계 인프라의 다양 한 역할을 호스트 하는 가상 컴퓨터를 배포 하는 것입니다. 각 가용성 집합에 최소 두 개의 컴퓨터를 사용 하는 것이 좋습니다. 기본 배포를 위해 4 개의 가상 머신을 만듭니다.

| Machine | 역할 | Subnet | 가용성 집합 | Storage 계정 | IP 주소 |
|:---:|:---:|:---:|:---:|:---:|:---:|
| contosodc1 |DC/ADFS |INT |contosodcset |contososac1 |정적 |
| contosodc2 |DC/ADFS |INT |contosodcset |contososac2 |정적 |
| contosowap1 |WAP |DMZ |contosowapset |contososac1 |정적 |
| contosowap2 |WAP |DMZ |contosowapset |contososac2 |정적 |

보셨을, 대로 NSG 없음이 지정 되었습니다. 즉, azure는 서브넷 수준 NSG를 사용할 수 있습니다. 그런 다음 서브넷 없거나 NIC 개체와 연결 된 개별 NSG를 사용 하 여 컴퓨터 네트워크 트래픽을 제어할 수 있습니다. 자세한 내용은 [(NSG (네트워크 보안 그룹) 란](https://aka.ms/Azure/NSG)합니다.
고정 IP 주소는 DNS를 관리 하는 경우에 권장 됩니다. Azure DNS를 사용 하 고 대신 도메인의 DNS 레코드에 해당 Azure Fqdn으로 새 컴퓨터 참조 수 있습니다.
가상 컴퓨터 창은 배포가 완료 되 면 다음과 같이 표시 됩니다.

![배포 된 Virtual Machines](./media/how-to-connect-fed-azure-adfs/virtualmachinesdeployed_noadfs.png)

### <a name="5-configuring-the-domain-controller--ad-fs-servers"></a>5. 도메인 컨트롤러 구성 / AD FS 서버
 들어오는 모든 요청을 인증 하기 위해 AD FS는 도메인 컨트롤러에 연결 해야 합니다. Azure에서 인증을 위해 온-프레미스 DC에 비용이 많이 드는 여정을 저장 하려면 Azure에서 도메인 컨트롤러의 복제본을 배포 하는 것이 좋습니다. 고가용성을 달성 하기 위해 최소 2 개의 도메인 컨트롤러의 가용성 집합을 만들려면는 것이 좋습니다.

| 도메인 컨트롤러 | 역할 | Storage 계정 |
|:---:|:---:|:---:|
| contosodc1 |복제본 |contososac1 |
| contosodc2 |복제본 |contososac2 |

* 두 서버 DNS 사용 하 여 복제본 도메인 컨트롤러로 승격
* 서버 관리자를 사용 하 여 AD FS 역할을 설치 하 여 AD FS 서버를 구성 합니다.

### <a name="6-deploying-internal-load-balancer-ilb"></a>6. 내부 부하 분산 장치 (ILB) 배포
**6.1. ILB 만들기**

ILB를 배포 하려면 Azure portal 및 클릭 선택 부하 분산 장치 (+)를 추가 합니다.

> [!NOTE]
> 표시 되지 않으면 **부하 분산 장치** 메뉴를 클릭 **찾아보기** 표시 될 때까지 스크롤 고 포털의 왼쪽 아래에서 **부하 분산 장치**합니다.  메뉴에 추가할 노란색 별표를 클릭 합니다. 이제 load balancer의 구성을 시작 하 여 패널을 열고 새 부하 분산 장치 아이콘을 선택 합니다.
> 
> 

![부하 분산 장치 찾아보기](./media/how-to-connect-fed-azure-adfs/browseloadbalancer.png)

* **이름**: 부하 분산 장치에 적합 한 이름을 제공합니다
* **구성표**: 이 부하 분산 장치는 AD FS 서버 앞에 배치 됩니다 하 고 내부 네트워크 연결에 것를 "내부" 선택
* **가상 네트워크**: AD FS를 배포 하는 가상 네트워크를 선택 합니다.
* **서브넷**: 여기서 내부 서브넷을 선택 합니다.
* **IP 주소 할당**: 정적

![내부 부하 분산 장치](./media/how-to-connect-fed-azure-adfs/ilbdeployment1.png)

클릭 한 후 만들기 및 ILB가 배포, 부하 분산 장치 목록에 표시 됩니다.

![ILB 이후 부하 분산 장치](./media/how-to-connect-fed-azure-adfs/ilbdeployment2.png)

다음 단계는 백 엔드 풀 및 백 엔드 프로브를 구성 하는 것입니다.

**6.2. ILB 백 엔드 풀 구성**

부하 분산 장치 패널에서 새로 만든된 ILB를 선택 합니다. 설정 패널이 열립니다. 

1. 설정 패널에서 백 엔드 풀을 선택 합니다.
2. 백 엔드 풀 추가 패널에서 가상 머신 추가 클릭
3. 가용성 집합을 선택할 수 있는 패널로 나타납니다.
4. AD FS 가용성 집합 선택

![ILB 백 엔드 풀 구성](./media/how-to-connect-fed-azure-adfs/ilbdeployment3.png)

**6.3. 프로브 구성**

ILB 설정 패널에서 상태 프로브를 선택 합니다.

1. 추가 클릭 합니다.
2. 프로브에 대 한 세부 정보 제공을 합니다. **이름**: 이름 b를 검색 합니다. **프로토콜**: HTTP c. **포트**: 80 (HTTP) d입니다. **경로**: / adf/프로브 e입니다. **간격**: (기본값)-5는 ILB 백 엔드 풀 f의에서 컴퓨터를 검색 합니다 간격입니다. **비정상 임계값 제한**: (기본값)-2는 임계값 연속 프로브 오류는 응답 하지 않는 및 트래픽 전송을 중지 ILB 백 엔드 풀에서 컴퓨터를 선언 합니다.

![ILB 프로브 구성](./media/how-to-connect-fed-azure-adfs/ilbdeployment4.png)

사용 하 여 AD FS 환경에서 상태 검사에 대 한 명시적으로 만든 /adfs/probe 끝점 전체 HTTPS 경로 확인 상황이 발생할 수 없습니다.  이것이 최신 AD FS 배포의 상태를 정확 하 게 반영 하지 않습니다는 기본 포트 443 검사를 보다 훨씬 더 잘입니다.  이 대 한 자세한 내용은에서 찾을 수 있습니다 https://blogs.technet.microsoft.com/applicationproxyblog/2014/10/17/hardware-load-balancer-health-checks-and-web-application-proxy-ad-fs-2012-r2/ 합니다.

**6.4. 부하 분산 규칙 만들기**

트래픽을 효과적으로 분산을 위해 ILB는 부하 분산 규칙을 사용 하 여 구성 되어야 합니다. 부하 분산 규칙을 만들려면 

1. ILB의 설정 패널에서 부하 분산 규칙을 선택 합니다.
2. 부하 분산 규칙 패널에서에서 추가 클릭
3. 추가 부하 분산 규칙 패널에에서는 합니다. **이름**: 규칙 b에 대 한 이름을 제공 합니다. **프로토콜**: TCP c를 선택 합니다. **포트**: 443 d입니다. **백 엔드 포트**: 443 e. **백 엔드 풀**: AD FS 클러스터 이전 f에 대해 만든 풀을 선택 합니다. **프로브**: 이전에 AD FS 서버에 만든 프로브를 선택 합니다.

![ILB 분산 규칙 구성](./media/how-to-connect-fed-azure-adfs/ilbdeployment5.png)

**6.5. ILB 사용 하 여 DNS 업데이트**

DNS 서버에 이동한 ILB에 대 한 CNAME을 만들어야 합니다. CNAME은 ILB의 IP 주소를 가리키는 IP 주소를 사용 하 여 페더레이션 서비스에 대 한 이어야 합니다. 예를 들어 ILB DIP 주소가 10.3.0.8을 및 설치 하는 페더레이션 서비스 fs.contoso.com 이면 10.3.0.8을 가리키는 fs.contoso.com에 대 한 CNAME을 만듭니다.
이렇게 하면 fs.contoso.com과 관련 통신은 모두 ILB로 끝나게을 적절 하 게 라우팅됩니다.

### <a name="7-configuring-the-web-application-proxy-server"></a>7. 웹 응용 프로그램 프록시 서버 구성
**7.1. AD FS 서버에 연결할 웹 응용 프로그램 프록시 서버 구성**

웹 응용 프로그램 프록시 서버는 ILB 뒤 AD FS 서버에 연결할 수 있도록 ILB에 대 한는 %systemroot%\system32\drivers\etc\hosts에 레코드를 만듭니다. 고유 이름 (DN) 페더레이션 서비스 이름, 예: fs.contoso.com 되도록 해야 note 합니다. 하며 IP 항목은 ILB의 IP 주소 (예제와 같이 10.3.0.8) 여야 합니다.

**7.2. 웹 응용 프로그램 프록시 역할 설치**

웹 응용 프로그램 프록시 서버가 ilb AD FS 서버에 연결할 수 있는지를 확인 한 후에 다음 웹 응용 프로그램 프록시 서버를 설치할 수 있습니다. 웹 응용 프로그램 프록시 서버를 도메인에 가입 되지 해야 합니다. 원격 액세스 역할을 선택 하 여 두 명의 웹 응용 프로그램 프록시 서버에 웹 응용 프로그램 프록시 역할을 설치 합니다. 서버 관리자에서는 WAP 설치를 완료 하려면 안내 합니다.
WAP를 배포 하는 방법에 대 한 자세한 내용은 읽을 [웹 응용 프로그램 프록시 서버 설치 및 구성](https://technet.microsoft.com/library/dn383662.aspx)합니다.

### <a name="8--deploying-the-internet-facing-public-load-balancer"></a>8.  인터넷 (공용) 부하 분산 장치 배포
**8.1.  인터넷 연결 (공용) 부하 분산 장치 만들기**

Azure portal에서 부하 분산 장치를 선택 하 고 추가 클릭 합니다. 부하 분산 장치 만들기 패널에서 다음 정보를 입력 합니다.

1. **이름**: 부하 분산 장치에 대 한 이름
2. **구성표**: 공용 –이 옵션이 부하 분산 장치에 공용 주소가 필요 함을 Azure에 알려줍니다.
3. **IP 주소**: 새 IP 주소 (동적) 만들기

![인터넷 연결 부하 분산 장치](./media/how-to-connect-fed-azure-adfs/elbdeployment1.png)

배포 후 부하 분산 장치는 부하 분산 장치 목록에 표시 됩니다.

![부하 분산 장치 목록](./media/how-to-connect-fed-azure-adfs/elbdeployment2.png)

**8.2. 공용 IP에 DNS 레이블 할당**

구성에 대 한 패널을 표시 하려면 부하 분산 장치 패널에서 새로 만든된 부하 분산 장치 항목을 클릭 합니다. 공용 IP에 대 한 DNS 레이블을 구성 하려면 다음 단계를 수행 합니다.

1. 공용 IP 주소를 클릭 합니다. 이 공용 IP 및 해당 설정에 대 한 패널이 열립니다.
2. 구성을 클릭합니다
3. DNS 레이블을 제공 합니다. 이 예를 들어 contosofs.westus.cloudapp.azure.com과 같이 어디에서 나 액세스할 수 있는 공용 DNS 레이블이 됩니다. 외부 부하 분산 장치 (contosofs.westus.cloudapp.azure.com)의 DNS 레이블로 확인 되는 페더레이션 서비스 (예: fs.contoso.com)에 대 한 외부 dns 항목을 추가할 수 있습니다.

![인터넷 연결 load balancer 구성](./media/how-to-connect-fed-azure-adfs/elbdeployment3.png) 

![인터넷 연결 부하 분산 장치 (DNS)를 구성 합니다.](./media/how-to-connect-fed-azure-adfs/elbdeployment4.png)

**8.3. 인터넷 연결 (공용) 부하 분산 장치의 백 엔드 풀 구성** 

가용성 WAP 서버에 대 한 집합으로 인터넷 연결 (공용) 부하 분산 장치에 대 한 백 엔드 풀을 구성 하는 내부 부하 분산 장치 만들기와 동일한 단계를 수행 합니다. 예를 들어 contosowapset.

![인터넷 연결 부하 분산 장치의 백 엔드 풀 구성](./media/how-to-connect-fed-azure-adfs/elbdeployment5.png)

**8.4. 프로브 구성**

WAP 서버의 백 엔드 풀에 대 한 프로브를 구성 하려면 내부 부하 분산 장치는 동일한 단계를 따릅니다.

![인터넷 연결 부하 분산 장치의 프로브 구성](./media/how-to-connect-fed-azure-adfs/elbdeployment6.png)

**8.5. 부하 분산 규칙 만들기**

ILB는 부하 분산 규칙 TCP 443에 대 한 구성에 동일한 단계를 따릅니다.

![인터넷 연결 부하 분산 장치의 분산 규칙 구성](./media/how-to-connect-fed-azure-adfs/elbdeployment7.png)

### <a name="9-securing-the-network"></a>9. 네트워크 보안
**9.1. 내부 서브넷 보안**

(아래에 나열 된 순서)에서 내부 서브넷을 효율적으로 보호 하는 다음 규칙 해야 전반적으로

| 규칙 | 설명 | 흐름 |
|:--- |:--- |:---:|
| AllowHTTPSFromDMZ |DMZ에서 HTTPS 통신을 허용 합니다. |인바운드 |
| DenyInternetOutbound |인터넷에 액세스할 수 없습니다 |아웃바운드 |

![INT 액세스 규칙 (인바운드)](./media/how-to-connect-fed-azure-adfs/nsg_int.png)

**9.2. DMZ 서브넷 보안**

| 규칙 | 설명 | 흐름 |
|:--- |:--- |:---:|
| AllowHTTPSFromInternet |DMZ를 인터넷에서 HTTPS를 허용 |인바운드 |
| DenyInternetOutbound |차단 된 인터넷에 HTTPS 외 |아웃바운드 |

![EXT 액세스 규칙 (인바운드)](./media/how-to-connect-fed-azure-adfs/nsg_dmz.png)

> [!NOTE]
> 클라이언트 사용자 인증서 인증 하는 경우 (clientTLS 인증 X509를 사용 하 여 사용자 인증서)이 필요한 경우 AD FS 필요한 TCP 포트 49443 인바운드 액세스를 위해 사용 하도록 설정 합니다.
> 
> 

### <a name="10-test-the-ad-fs-sign-in"></a>10. AD FS 로그인 테스트
가장 쉬운 방법은 IdpInitiatedSignon.aspx 페이지를 사용 하 여는 AD FS를 테스트 합니다. 점을 할 수 있도록 AD FS 속성에 IdpInitiatedSignOn을 사용 하도록 설정 해야 합니다. AD FS 설치를 확인 하려면 다음 단계를 수행 합니다.

1. 실행을 사용 하도록 설정 하려면 PowerShell을 사용 하 여 AD FS 서버의 cmdlet 아래.
   Set-AdfsProperties -EnableIdPInitiatedSignonPage $true 
2. 모든 외부 컴퓨터에서 https 액세스:\//adfs-server.contoso.com/adfs/ls/IdpInitiatedSignon.aspx 합니다.  
3. AD FS 페이지를 참조 해야 아래와 같은:

![테스트 로그인 페이지](./media/how-to-connect-fed-azure-adfs/test1.png)

성공적으로 로그인 하면 성공 메시지를 사용 하 여 아래와 같이:

![테스트 성공](./media/how-to-connect-fed-azure-adfs/test2.png)

## <a name="template-for-deploying-ad-fs-in-azure"></a>Azure에서 AD FS를 배포 하기 위한 템플릿
템플릿은 각 2 도메인 컨트롤러, AD FS 및 WAP에 대 한 6 개의 컴퓨터 설치를 배포 합니다.

[Azure 배포 템플릿에서 AD FS](https://github.com/paulomarquesc/adfs-6vms-regular-template-based)

기존 가상 네트워크를 사용할 수도 있고이 템플릿을 배포 하는 동안 새 VNET을 만듭니다. 배포 프로세스의 매개 변수 사용에 대 한 설명을 사용 하 여 배포를 사용자 지정에 사용할 수 있는 다양 한 매개 변수는 다음과 같습니다. 

| 매개 변수 | 설명 |
|:--- |:--- |
| 위치 |영역 리소스를 배포, 예: 동부 미국입니다. |
| StorageAccountType |만든 저장소 계정 유형 |
| VirtualNetworkUsage |새 가상 네트워크를 만들지 아니면 기존 계정을 사용할 경우를 나타냅니다. |
| VirtualNetworkName |기존 또는 새 가상 네트워크 사용에서 필수인 만들 Virtual Network의 이름 |
| VirtualNetworkResourceGroupName |기존 가상 네트워크가 있는 리소스 그룹의 이름을 지정 합니다. 기존 virtual network를 사용 하는 경우 이것이 필수 매개 변수는 배포는 기존 가상 네트워크의 ID를 찾을 수 있도록 |
| VirtualNetworkAddressRange |새 가상 네트워크를 만드는 경우 필수인 새 VNET의 주소 범위 |
| InternalSubnetName |(신규 또는 기존) 가상 네트워크 사용 옵션에서 필수인 내부 서브넷의 이름 |
| InternalSubnetAddressRange |새 가상 네트워크를 만드는 경우 필수인 도메인 컨트롤러 및 ADFS 서버를 포함 하는 내부 서브넷의 주소 범위입니다. |
| DMZSubnetAddressRange |새 가상 네트워크를 만드는 경우 Windows 응용 프로그램 프록시 서버를 필수를 포함 하는 dmz 서브넷의 주소 범위입니다. |
| DMZSubnetName |(신규 또는 기존) 가상 네트워크 사용 옵션에서 필수인 내부 서브넷의 이름입니다. |
| ADDC01NICIPAddress |첫 번째 도메인 컨트롤러의 내부 IP 주소를이 IP 주소는 DC에 정적으로 할당할 및 내부 서브넷 내에서 유효한 ip 주소 여야 합니다. |
| ADDC02NICIPAddress |두 번째 도메인 컨트롤러의 내부 IP 주소를이 IP 주소는 DC에 정적으로 할당할 및 내부 서브넷 내에서 유효한 ip 주소 여야 합니다. |
| ADFS01NICIPAddress |첫 번째 ADFS 서버의 내부 IP 주소를이 IP 주소는 ADFS 서버에 정적으로 할당할 및 내부 서브넷 내에서 유효한 ip 주소 여야 합니다. |
| ADFS02NICIPAddress |두 번째 ADFS 서버의 내부 IP 주소를이 IP 주소는 ADFS 서버에 정적으로 할당할 및 내부 서브넷 내에서 유효한 ip 주소 여야 합니다. |
| WAP01NICIPAddress |첫 번째 WAP 서버의 내부 IP 주소를이 IP 주소는 WAP 서버에 정적으로 할당할 및 DMZ 서브넷 내에서 유효한 ip 주소 여야 합니다. |
| WAP02NICIPAddress |두 번째 WAP 서버의 내부 IP 주소를이 IP 주소는 WAP 서버에 정적으로 할당할 및 DMZ 서브넷 내에서 유효한 ip 주소 여야 합니다. |
| ADFSLoadBalancerPrivateIPAddress |ADFS 부하 분산 장치의 내부 IP 주소를이 IP 주소는 부하 분산 장치에 정적으로 할당할 및 내부 서브넷 내에서 유효한 ip 주소 여야 합니다. |
| ADDCVMNamePrefix |도메인 컨트롤러에 대 한 Virtual Machine 이름 접두사 |
| ADFSVMNamePrefix |ADFS 서버에 대 한 Virtual Machine 이름 접두사 |
| WAPVMNamePrefix |WAP 서버에 대 한 Virtual Machine 이름 접두사 |
| ADDCVMSize |도메인 컨트롤러의 vm 크기 |
| ADFSVMSize |ADFS 서버의 vm 크기 |
| WAPVMSize |WAP 서버의 vm 크기 |
| AdminUserName |가상 머신의 로컬 관리자의 이름 |
| AdminPassword |가상 머신의 로컬 관리자 계정의 암호 |

## <a name="additional-resources"></a>추가 자료
* [가용성 집합](https://aka.ms/Azure/Availability) 
* [Azure Load Balancer](https://aka.ms/Azure/ILB)
* [내부 부하 분산 장치](https://aka.ms/Azure/ILB/Internal)
* [인터넷 연결 부하 분산 장치](https://aka.ms/Azure/ILB/Internet)
* [저장소 계정](https://aka.ms/Azure/Storage)
* [Azure Virtual Network](https://aka.ms/Azure/VNet)
* [AD FS 및 웹 응용 프로그램 프록시 링크](https://aka.ms/ADFSLinks) 

## <a name="next-steps"></a>다음 단계
* [Azure Active Directory와 온-프레미스 id 통합](https://docs.microsoft.com/azure/active-directory/hybrid/whatis-hybrid-identity)
* [구성 및 Azure AD Connect를 사용 하 여 AD FS 관리](/azure/active-directory/hybrid/how-to-connect-fed-whatis)
* [Azure Traffic Manager를 사용 하 여 Azure에서 고가용성 교차 지리적 AD FS 배포](active-directory-adfs-in-azure-with-azure-traffic-manager.md)
