---
title: Azure Traffic Manager를 사용 하 여 Azure에서 고가용성 교차 지리적 AD FS 배포 | Microsoft Docs
description: 이 문서에서는 고가용성을 위해 Azure에서 AD FS를 배포 하는 방법을 배웁니다.
keywords: Azure traffic manager Azure Traffic Manager, 지리적, 다중 데이터 센터, 지리적 데이터 센터, 다중 지리적 데이터 센터를 사용 하 여 adfs 사용 하 여 ad fs에서 azure AD FS 배포, azure adfs, azure adfs, azure ad fs를 배포, adfs 배포, ad fs, azure에서 adfs 배포 adfs 배포 azure에 adfs 이동 azure, azure adfs, AD FS, Azure, azure에서 iaas, ADFS, AD FS에 대 한 소개에서 AD FS 배포, azure에서
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
ms.openlocfilehash: 4af0386ef97694baa9ba7f1e5e7163554d79734a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59874124"
---
# <a name="high-availability-cross-geographic-ad-fs-deployment-in-azure-with-azure-traffic-manager"></a>Azure Traffic Manager를 사용 하 여 Azure에서 고가용성 교차 지리적 AD FS 배포
[Azure에서 AD FS 배포](how-to-connect-fed-azure-adfs.md) Azure의 조직에 대 한 간단한 AD FS 인프라를 배포 하는 것에 대 한 단계별 지침을 제공 합니다. 이 문서에서는 사용 하 여 Azure에서 교차 지리적 AD FS 배포를 만들려면 다음 단계 [Azure Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/)합니다. Azure Traffic Manager 지리적으로 분배 된 고가용성 및 고성능 AD FS 인프라 조직에 대 한 하 여 만들기는 인프라에서 서로 다른 요구 사항에 맞게 사용할 수 있는 라우팅 방법의 범위를 사용 합니다.

항상 사용 가능한 교차 지리적 AD FS 인프라를 사용 하도록 설정 합니다.

* **단일 실패 지점 제거 합니다.** Azure Traffic Manager의 장애 조치 기능을 사용 하 여 얻을 수는 부분에서는 전 세계 데이터 센터 중 하나가 중단 하는 경우에 항상 사용 가능한 AD FS 인프라를
* **성능 개선된:** 사용자가 더 빠르게 인증할 수 있는 고성능 AD FS 인프라를 제공 하려면이 문서의 제안된 된 배포를 사용할 수 있습니다. 

## <a name="design-principles"></a>디자인 원칙
![전체 디자인](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/blockdiagram.png)

기본 디자인 원칙은 Azure에서 AD FS 배포 문서의 디자인 원칙에 나열 된 동일 합니다. 위의 다이어그램에는 다른 지역에 기본 배포의 단순한 확장을 보여 줍니다. 새 지역에 배포를 확장할 때 고려해 야 할 사항은 다음과 같습니다.

* **가상 네트워크:** 추가 AD FS 인프라를 배포 하려는 지리적 지역에 새 가상 네트워크를 만들어야 합니다. 위의 다이어그램에 각 지역의 두 가상 네트워크로 Geo1 VNET과 Geo2 VNET를 참조 합니다.
* **도메인 컨트롤러 및 새 지역 VNET에 AD FS 서버:** 도메인 인증 및 성능 향상을 완료 하려면 네트워크에서 멀리 떨어진 다른 도메인 컨트롤러에 연결할 새 지역에서 AD FS 서버 없는 되도록 새 지역에서 컨트롤러를 배포 하는 것이 좋습니다.
* **저장소 계정:** 저장소 계정에 있는 지역과 연결 됩니다. 새 지역에 컴퓨터를 배포 하 고는, 때문에 지역에서 사용할 새 저장소 계정을 만들 해야 합니다.  
* **네트워크 보안 그룹:** 처럼 다른 지리적 지역에 저장소 계정에 지역에서 만든 네트워크 보안 그룹을 사용할 수 없습니다. 따라서 새 네트워크 보안 그룹을 만드는 INT 및 DMZ 서브넷에 대 한 첫 번째 지역에서와 비슷한 새 지역에서 해야 합니다.
* **공용 IP 주소에 대 한 DNS 레이블:** Azure Traffic Manager 끝점을 참조할 수 있습니다 DNS 레이블 통해서만 합니다. 따라서 해야 외부 부하 분산 장치의 공용 IP 주소에 대 한 DNS 레이블을 만들어야 합니다.
* **Azure Traffic Manager:** Microsoft Azure Traffic Manager를 사용 하면 전 세계 여러 데이터 센터에서 실행 중인 서비스 끝점에 대 한 사용자 트래픽의 배포를 제어할 수 있습니다. Azure Traffic Manager는 DNS 수준에서 작동합니다. 전역으로 분산 된 끝점에 대 한 최종 사용자 트래픽을 DNS 응답을 사용 합니다. 그러면 클라이언트 해당 끝점에 직접 연결 합니다. 다양 한 성능, 가중치 및 우선 순위 라우팅 옵션을 사용 하 여 조직의 요구에 가장 적합 한 라우팅 옵션을 쉽게 선택할 수 있습니다. 
* **두 지역 간에 vnet에 vnet 연결:** 자체 가상 네트워크 간의 연결을 사용할 필요가 없습니다. 각 가상 네트워크는 도메인 컨트롤러에 대 한 액세스 권한이 하 고 AD FS 및 WAP 서버를 자체에, 다른 지역에서 가상 네트워크 간의 연결 없이 작업할 수 있습니다. 

## <a name="steps-to-integrate-azure-traffic-manager"></a>Azure Traffic Manager를 통합 하는 단계
### <a name="deploy-ad-fs-in-the-new-geographical-region"></a>새 지역에서 AD FS 배포
단계 및 지침에 따릅니다 [Azure에서 AD FS 배포](how-to-connect-fed-azure-adfs.md) 새 지역에서 동일한 토폴로지를 배포 합니다.

### <a name="dns-labels-for-public-ip-addresses-of-the-internet-facing-public-load-balancers"></a>인터넷 연결 (공용) 부하 분산 장치의 공용 IP 주소에 대 한 DNS 레이블
위에서 설명한 대로 Azure Traffic Manager DNS 레이블을 끝점으로만 참조할 수 있습니다 이며 따라서 외부 부하 분산 장치의 공용 IP 주소에 대 한 DNS 레이블을 만들어야 합니다. 아래 스크린샷은 공용 IP 주소에 대 한 DNS 레이블을 구성 하는 방법을 보여 줍니다. 

![DNS 레이블](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/eastfabstsdnslabel.png)

### <a name="deploying-azure-traffic-manager"></a>Azure Traffic Manager를 배포합니다.
Traffic manager 프로필을 만들려면 다음 단계를 수행 합니다. 자세한 내용은 참조할 수도 있습니다를 [Azure Traffic Manager 프로필 관리](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-manage-profiles)합니다.

1. **Traffic Manager 프로필을 만듭니다.** 트래픽 관리자 프로필에 고유한 이름을 지정 합니다. 이 프로필의 DNS 이름의 일부인 이름과 Traffic Manager 도메인 이름 레이블에 대 한 접두사로 역할입니다. 이름 / 접두사에 추가 됩니다. trafficmanager.net manager 트래픽에 대 한 DNS 레이블을 만들려면. 아래 스크린샷은 traffic manager DNS 접두사 mysts로 설정 되 고 그 결과 DNS 레이블이 mysts.trafficmanager.net 합니다. 
   
    ![Traffic Manager 프로필 만들기](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/trafficmanager01.png)
2. **트래픽 라우팅 방법:** Traffic manager에서 사용 가능한 가지 라우팅 세 가지 옵션이 있습니다.
   
   * 우선 순위 
   * 성능
   * 가 중
     
     **성능** 응답성이 높은 AD FS 인프라를 달성 하기 위해 권장 되는 옵션입니다. 그러나 배포 요구 사항에 가장 적합 한 라우팅 방법을 선택할 수 있습니다. 라우팅 옵션을 선택 하 여 AD FS 기능을 받지 않습니다. 참조 [Traffic Manager 트래픽 라우팅 방법](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-routing-methods) 자세한 내용은 합니다. 샘플에서 위의 스크린샷에서 볼 수는 **성능** 메서드를 선택 합니다.
3. **끝점을 구성 합니다.** Traffic manager 페이지에서 끝점을 클릭 하 고 추가 선택 합니다. 아래 스크린샷과 유사한 추가 끝점 페이지가 열립니다.
   
   ![끝점 구성](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/eastfsendpoint.png)
   
   다른 입력의 경우 아래 지침을 따르세요.
   
   **형식:** Azure 공용 IP 주소를 가리키는 것 처럼 Azure 끝점을 선택 합니다.
   
   **이름:** 끝점과 연결 하려는 이름을 만듭니다. 이 DNS 이름이 아니며 DNS 레코드는 관련이 없습니다.
   
   **대상 리소스 유형:** 이 속성에 값으로 공용 IP 주소를 선택 합니다. 
   
   **대상 리소스:** 이 구독에서 사용할 수 있는 다른 DNS 레이블에서 선택할 수 있는 옵션이 제공 됩니다. 구성 하는 끝점에 해당 되는 DNS 레이블을 선택 합니다.
   
   Azure Traffic Manager에서 트래픽 라우팅 하려는 각 지역에 대 한 끝점을 추가 합니다.
   자세한 내용과 추가 / traffic manager에서 끝점을 구성 하는 방법에 대 한 자세한 단계에 대 한 참조 [끝점을 추가, 사용 안 함, 사용 또는 삭제](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-manage-endpoints)
4. **프로브를 구성 합니다.** Traffic manager 페이지에서 구성을 클릭 합니다. 구성 페이지에서 HTTP 포트 80 및 상대 경로 /adfs/probe의 프로브 모니터링 설정을 변경 해야
   
    ![프로브 구성](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/mystsconfig.png) 
   
   > [!NOTE]
   > **구성이 완료 되 면 끝점의 상태는 온라인 확인**합니다. 모든 끝점이 '성능이 저하 된' 상태에 있는 경우 Azure Traffic Manager는 진단 잘못 되 고 모든 끝점에 연결할 수는 트래픽을 가정 라우트 하려고 하는 최대한 수행 합니다.
   > 
   > 
5. **Azure Traffic Manager에 대 한 DNS 레코드를 수정 합니다.** 페더레이션 서비스는 Azure Traffic Manager DNS 이름에 CNAME 이어야 합니다. Azure Traffic Manager에 도달 하면 실제로 모든 사용자가 페더레이션 서비스를 연결 하려는 있도록 공용 DNS 레코드에서 CNAME을 만들어야 합니다.
   
    예를 들어, 페더레이션 서비스 fs.fabidentity.com Traffic Manager로 가리킵니다, 해야 다음 되도록 DNS 리소스 레코드를 업데이트 하려면:
   
    <code>fs.fabidentity.com IN CNAME mysts.trafficmanager.net</code>

## <a name="test-the-routing-and-ad-fs-sign-in"></a>라우팅 및 AD FS 로그인 테스트
### <a name="routing-test"></a>테스트 라우팅
라우팅에 대 한 기본적인 테스트 각 지역에 있는 컴퓨터에서 페더레이션 서비스 DNS 이름을 ping 하는 것입니다. 선택한 라우팅 방법에 따라 실제로 ping 한 끝점은 ping 디스플레이에 반영 됩니다. 예를 들어 성능 라우팅을 선택한 경우 클라이언트 영역을 가장 가까운 끝점은 수에 도달 했습니다. 다음 두 개의 다른 지역 클라이언트 컴퓨터에서 두 ping의 스냅숏입니다, EastAsia 지역와 미국 서 부에 각각 하나씩은입니다. 

![테스트 라우팅](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/pingtest.png)

### <a name="ad-fs-sign-in-test"></a>AD FS 로그인 테스트
AD FS를 테스트 하는 가장 쉬운 방법은 IdpInitiatedSignon.aspx 페이지를 사용 하 여 됩니다. 점을 할 수 있도록 AD FS 속성에 IdpInitiatedSignOn을 사용 하도록 설정 해야 합니다. AD FS 설치를 확인 하려면 다음 단계를 수행 합니다.

1. 실행을 사용 하도록 설정 하려면 PowerShell을 사용 하 여 AD FS 서버의 cmdlet 아래. 
   Set-AdfsProperties -EnableIdPInitiatedSignonPage $true
2. 모든 외부 컴퓨터 액세스 https://에서<yourfederationservicedns>/adfs/ls/IdpInitiatedSignon.aspx
3. AD FS 페이지를 참조 해야 아래와 같은:
   
    ![ADFS 테스트-인증 질문](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/adfstest1.png)
   
    및에서 성공적으로 로그인 하면 성공 메시지를 사용 하 여 아래와 같이:
   
    ![ADFS 테스트-인증 성공](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/adfstest2.png)

## <a name="related-links"></a>관련 링크
* [Azure에서 기본 AD FS 배포](how-to-connect-fed-azure-adfs.md)
* [Microsoft Azure Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/)
* [Traffic Manager 트래픽 라우팅 방법](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-routing-methods)

## <a name="next-steps"></a>다음 단계
* [Azure Traffic Manager 프로필 관리](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-manage-profiles)
* [추가, 사용 안 함, 사용 또는 끝점 삭제](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-manage-endpoints) 

