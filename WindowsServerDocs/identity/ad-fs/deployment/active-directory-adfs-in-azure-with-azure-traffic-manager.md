---
title: Azure Traffic Manager를 사용 하 여 Azure에서 고가용성 교차 지리적 AD FS 배포 | Microsoft Docs
description: 이 문서에서는 Azure에서 high 가용성에 AD FS를 배포 하는 방법에 대해 설명 합니다.
keywords: Azure traffic manager를 사용 하는 Ad fs, Azure Traffic Manager, 지리, 다중 데이터 센터, 지리적 데이터 센터, 다중 지리적 데이터 센터, azure에서 AD FS 배포, azure adfs 배포, azure adfs, azure ad fs 배포, adfs 배포, ad fs 배포, azure에서 adfs 배포, ad fs 배포 azure에서 adfs 배포, azure에 AD FS 배포, adfs azure에서 AD FS, Azure AD FS, azure, iaas, ADFS, adfs를 azure로 이동
services: active-directory
documentationcenter: ''
author: anandyadavmsft
manager: mtillman
editor: ''
ms.assetid: a14bc870-9fad-45ed-acd5-a90ccd432e54
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 09/01/2016
ms.author: anandy;billmath
ms.openlocfilehash: d98eb126513d707bce7abe3e901c8bf584d2319c
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70868021"
---
# <a name="high-availability-cross-geographic-ad-fs-deployment-in-azure-with-azure-traffic-manager"></a>Azure Traffic Manager를 사용 하 여 Azure에서 고가용성 교차 지리적 AD FS 배포
Azure [의 AD FS 배포](how-to-connect-fed-azure-adfs.md) 는 azure에서 조직에 대 한 간단한 AD FS 인프라를 배포할 수 있는 방법에 대 한 단계별 지침을 제공 합니다. 이 문서에서는 azure [Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/)를 사용 하 여 azure에서 AD FS의 지역 간 배포를 만드는 다음 단계를 제공 합니다. Azure Traffic Manager는 인프라의 다양 한 요구에 맞게 사용할 수 있는 라우팅 메서드 범위를 사용 하 여 조직에 대 한 지리적으로 분산 된 고가용성 및 고성능 AD FS 인프라를 만드는 데 도움이 됩니다.

항상 사용 가능한 교차 지리적 AD FS 인프라를 사용 하도록 설정 합니다.

* **단일 실패 지점 제거:** Azure Traffic Manager의 장애 조치 (failover) 기능을 사용 하면 전 세계에 있는 데이터 센터 중 하나가 중단 된 경우에도 항상 사용 가능한 AD FS 인프라를 달성할 수 있습니다.
* **향상 된 성능:** 이 문서에서 제안 된 배포를 사용 하 여 사용자가 더 빨리 인증 하는 데 도움이 될 수 있는 고성능 AD FS 인프라를 제공할 수 있습니다. 

## <a name="design-principles"></a>디자인 원칙
![전체 디자인](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/blockdiagram.png)

기본 디자인 원칙은 Azure의 배포 AD FS 문서에 있는 디자인 원칙에 나열 된 것과 동일 합니다. 위의 다이어그램에서는 다른 지역에 대 한 기본 배포의 간단한 확장을 보여 줍니다. 다음은 배포를 새 지역으로 확장할 때 고려해 야 할 몇 가지 사항입니다.

* **가상 네트워크:** 추가 AD FS 인프라를 배포 하려는 지리적 지역에 새 가상 네트워크를 만들어야 합니다. 위의 다이어그램에서 Geo1 VNET 및 Geo2 VNET을 각 지역에 있는 두 개의 가상 네트워크로 볼 수 있습니다.
* **새 지리적 VNET의 도메인 컨트롤러 및 AD FS 서버:** 새 지역의 도메인 컨트롤러를 배포 하는 것이 좋습니다. AD FS 그러면 새 지역의 도메인 컨트롤러를 다른 네트워크의 도메인 컨트롤러에 연결 하 여 인증을 완료 하 여 성능을 향상 시킬 필요가 없습니다.
* **저장소 계정:** 저장소 계정은 지역에 연결 됩니다. 새 지역에 컴퓨터를 배포할 예정 이므로 지역에서 사용할 새 저장소 계정을 만들어야 합니다.  
* **네트워크 보안 그룹:** 저장소 계정으로 지역에서 만든 네트워크 보안 그룹은 다른 지역에서 사용할 수 없습니다. 따라서 새 지역에서 INT 및 DMZ 서브넷의 첫 번째 지역에 있는 것과 비슷한 새 네트워크 보안 그룹을 만들어야 합니다.
* **공용 IP 주소에 대 한 DNS 레이블:** Azure Traffic Manager는 DNS 레이블을 통해서만 끝점을 참조할 수 있습니다. 따라서 외부 부하 분산 장치의 공용 IP 주소에 대 한 DNS 레이블을 만들어야 합니다.
* **Azure Traffic Manager:** Microsoft Azure Traffic Manager를 사용 하면 전 세계 여러 데이터 센터에서 실행 되는 서비스 끝점에 대 한 사용자 트래픽 배포를 제어할 수 있습니다. Azure Traffic Manager는 DNS 수준에서 작동 합니다. DNS 응답을 사용 하 여 전역으로 분산 되는 끝점으로 최종 사용자 트래픽을 보냅니다. 그러면 클라이언트는 해당 끝점에 직접 연결 됩니다. 성능, 가중치가 적용 되 고 우선 순위에 대 한 다른 라우팅 옵션을 사용 하면 조직의 요구 사항에 가장 적합 한 라우팅 옵션을 쉽게 선택할 수 있습니다. 
* **두 지역 간의 v-net 간 연결:** 가상 네트워크 자체를 연결할 필요는 없습니다. 각 가상 네트워크는 도메인 컨트롤러에 대 한 액세스 권한을 가지 며 자체에 AD FS 및 WAP 서버가 있기 때문에 다른 지역의 가상 네트워크 간 연결 없이 작업할 수 있습니다. 

## <a name="steps-to-integrate-azure-traffic-manager"></a>Azure Traffic Manager를 통합 하는 단계
### <a name="deploy-ad-fs-in-the-new-geographical-region"></a>새 지역에 AD FS 배포
[Azure에서 AD FS 배포](how-to-connect-fed-azure-adfs.md) 의 단계 및 지침에 따라 새 지역에 동일한 토폴로지를 배포 합니다.

### <a name="dns-labels-for-public-ip-addresses-of-the-internet-facing-public-load-balancers"></a>인터넷 연결 (공용) 부하 분산 장치의 공용 IP 주소에 대 한 DNS 레이블
위에서 설명한 것 처럼 Azure Traffic Manager는 DNS 레이블만 끝점으로 참조할 수 있으므로 외부 부하 분산 장치의 공용 IP 주소에 대 한 DNS 레이블을 만드는 것이 중요 합니다. 아래 스크린샷에서는 공용 IP 주소에 대 한 DNS 레이블을 구성 하는 방법을 보여 줍니다. 

![DNS 레이블](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/eastfabstsdnslabel.png)

### <a name="deploying-azure-traffic-manager"></a>Azure Traffic Manager 배포
트래픽 관리자 프로필을 만들려면 아래 단계를 따르세요. 자세한 내용은 [Azure Traffic Manager 프로필 관리](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-manage-profiles)를 참조할 수도 있습니다.

1. **Traffic Manager 프로필을 만듭니다.** Traffic manager 프로필에 고유한 이름을 지정 합니다. 이 프로필 이름은 DNS 이름에 포함 되며 Traffic Manager 도메인 이름 레이블에 대 한 접두사 역할을 합니다. 이름/접두사가 trafficmanager.net에 추가 되어 traffic manager에 대 한 DNS 레이블을 만듭니다. 아래 스크린샷에서는 mysts로 설정 되는 traffic manager DNS 접두사를 보여주고 그 결과 DNS 레이블은 mysts.trafficmanager.net 됩니다. 
   
    ![Traffic Manager 프로필 만들기](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/trafficmanager01.png)
2. **트래픽 라우팅 방법:** Traffic manager에서 사용할 수 있는 세 가지 라우팅 옵션은 다음과 같습니다.
   
   * 우선 순위 
   * 성능
   * 정도
     
     **성능은** 응답성이 높은 AD FS 인프라를 얻기 위해 권장 되는 옵션입니다. 그러나 배포 요구 사항에 가장 적합 한 라우팅 방법을 선택할 수 있습니다. AD FS 기능은 선택한 라우팅 옵션의 영향을 받지 않습니다. 자세한 내용은 [Traffic Manager 트래픽 라우팅 방법](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-routing-methods) 을 참조 하세요. 위의 샘플 스크린샷에서 **성능** 메서드를 선택 하는 것을 볼 수 있습니다.
3. **끝점 구성:** Traffic manager 페이지에서 끝점을 클릭 하 고 추가를 선택 합니다. 그러면 아래 스크린샷 처럼 끝점 추가 페이지가 열립니다.
   
   ![끝점 구성](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/eastfsendpoint.png)
   
   다른 입력의 경우 아래 지침을 따르세요.
   
   **유형:** Azure 공용 IP 주소를 가리킬 때 Azure 끝점을 선택 합니다.
   
   **Name:** 끝점과 연결 하려는 이름을 만듭니다. Dns 이름이 아니므로 DNS 레코드에 대 한 관계가 없습니다.
   
   **대상 리소스 유형:** 이 속성의 값으로 공용 IP 주소를 선택 합니다. 
   
   **대상 리소스:** 이렇게 하면 구독에서 사용할 수 있는 여러 DNS 레이블 중에서 선택할 수 있는 옵션이 제공 됩니다. 구성 하는 끝점에 해당 하는 DNS 레이블을 선택 합니다.
   
   Azure Traffic Manager에서 트래픽을 라우팅하는 데 사용할 각 지역에 대해 끝점을 추가 합니다.
   Traffic manager에서 끝점을 추가/구성 하는 방법에 대 한 자세한 내용 및 자세한 단계는 [끝점 추가, 사용 안 함, 사용 또는 삭제](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-manage-endpoints) 를 참조 하세요.
4. **프로브 구성:** Traffic manager 페이지에서 구성을 클릭 합니다. 구성 페이지에서 HTTP 포트 80 및 상대 경로/adfs/probe을 프로브로 모니터 설정을 변경 해야 합니다.
   
    ![프로브 구성](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/mystsconfig.png) 
   
   > [!NOTE]
   > **구성이 완료 되 면 끝점의 상태가 온라인 인지 확인**합니다. 모든 끝점이 ' 저하 됨 ' 상태 이면 Azure Traffic Manager는 진단이 올바르지 않으며 모든 끝점에 연결할 수 있다고 가정 하 여 트래픽을 라우팅하는 가장 좋은 시도를 합니다.
   > 
   > 
5. **Azure Traffic Manager에 대 한 DNS 레코드 수정:** 페더레이션 서비스는 Azure Traffic Manager DNS 이름의 CNAME 이어야 합니다. 페더레이션 서비스에 대 한 연결을 시도 하는 사람이 실제로 Azure Traffic Manager에 도달 하도록 공용 DNS 레코드에 CNAME을 만듭니다.
   
    예를 들어 페더레이션 서비스 fs.fabidentity.com Traffic Manager를 가리키도록 DNS 리소스 레코드를 다음과 같이 업데이트 해야 합니다.
   
    <code>fs.fabidentity.com IN CNAME mysts.trafficmanager.net</code>

## <a name="test-the-routing-and-ad-fs-sign-in"></a>라우팅 및 AD FS 로그인 테스트
### <a name="routing-test"></a>라우팅 테스트
라우팅에 대 한 매우 기본적인 테스트는 각 지역의 컴퓨터에서 페더레이션 서비스 DNS 이름을 ping 하는 것입니다. 선택한 라우팅 방법에 따라 실제로 ping 된 끝점이 ping 표시에 반영 됩니다. 예를 들어 성능 라우팅을 선택한 경우 클라이언트 지역에 가장 가까운 끝점에 도달 하 게 됩니다. 다음은 두 개의 서로 다른 지역 클라이언트 컴퓨터의 두 ping에 대 한 스냅숏입니다. 하나는 EastAsia 지역에 있고 다른 하나는 미국 서 부입니다. 

![라우팅 테스트](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/pingtest.png)

### <a name="ad-fs-sign-in-test"></a>AD FS 로그인 테스트
AD FS를 테스트 하는 가장 쉬운 방법은 Idpinitiatedsignon.aspx 페이지를 사용 하는 것입니다. 이 작업을 수행 하려면 AD FS 속성에 대해 Idpinitiatedsignon.aspx를 사용 하도록 설정 해야 합니다. 아래 단계에 따라 AD FS 설치를 확인 합니다.

1. PowerShell을 사용 하 여 AD FS 서버에서 아래 cmdlet을 실행 하 여 사용으로 설정 합니다. 
   Set-adfsproperties-EnableIdPInitiatedSignonPage $true
2. 모든 외부 컴퓨터 액세스 https://에서\<yourfederationservicedns>/adfs/ls/IdpInitiatedSignon.aspx
3. 다음과 같이 AD FS 페이지가 표시 됩니다.
   
    ![ADFS 테스트-인증 챌린지](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/adfstest1.png)
   
    성공적으로 로그인 하면 아래와 같은 성공 메시지가 표시 됩니다.
   
    ![ADFS 테스트-인증 성공](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/adfstest2.png)

## <a name="related-links"></a>관련 링크
* [Azure의 기본 AD FS 배포](how-to-connect-fed-azure-adfs.md)
* [Microsoft Azure Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/)
* [트래픽 라우팅 방법 Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-routing-methods)

## <a name="next-steps"></a>다음 단계
* [Azure Traffic Manager 프로필 관리](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-manage-profiles)
* [끝점 추가, 사용 안 함, 사용 또는 삭제](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-manage-endpoints) 

