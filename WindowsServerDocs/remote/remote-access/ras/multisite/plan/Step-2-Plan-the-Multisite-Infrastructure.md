---
title: 2 단계 계획 멀티 사이트 인프라
description: 이 가이드의 일부인이 항목에서는 여러 원격 액세스 서버 배포 Windows Server 2016에서 멀티 사이트 배포에서 합니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 64c10107-cb03-41f3-92c6-ac249966f574
ms.author: pashort
author: shortpatti
ms.openlocfilehash: a2655f4de83576ef62b113419a69badaacc868f9
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67281002"
---
# <a name="step-2-plan-the-multisite-infrastructure"></a>2 단계 계획 멀티 사이트 인프라

>적용 대상: Windows Server (반기 채널), Windows Server 2016

원격 액세스 멀티 사이트 토폴로지에 배포 하는 다음 단계는; 멀티 사이트 인프라 계획을 완료 하는 것 포함 하 여 Active Directory 보안 그룹, 그룹 정책 개체입니다.  
## <a name="bkmk_2_1_AD"></a>2.1 Active Directory 계획  
다양 한 토폴로지는 원격 액세스 멀티 사이트 배포를 구성할 수 있습니다.  
  
-   **단일 Active Directory 사이트, 여러 진입점**-이 토폴로지에서 단일 Active Directory 사이트, 사이트 전체에 걸쳐 고속 인트라넷 링크와 함께 전체 조직에 대해 있지만 각 역할 진입점을 조직 전체에 걸쳐 배포 하는 여러 원격 액세스 서버가 있는 합니다. 이 토폴로지는 지리적 예는 미국 동부 및 서 부 해안 진입점에 대 한 단일 Active Directory 사이트를 것입니다.  
  
    ![멀티 사이트 인프라](../../../../media/Step-2-Plan-the-Multisite-Infrastructure/RAMultisiteTopo1.png)  
  
-   **여러 Active Directory 사이트, 여러 진입점**-이 토폴로지에 있는 두 개 이상의 Active Directory 사이트 각 사이트에 대 한 진입점으로 배포 하는 원격 액세스 서버입니다. 각 원격 액세스 서버는 사이트에 대 한 Active Directory 도메인 컨트롤러와 연결 됩니다. 이 토폴로지의 지리적 예 각 사이트에 대 한 단일 액세스 지점을 미국에 대 한 Active Directory 사이트 및 유럽의 경우 하나 있는 것입니다. Active Directory 사이트가 여러 개인 경우 수행 하지 할 경우 각 사이트와 연결 된 진입점을 참고 합니다. 또한 일부 Active Directory 사이트에 연결 된 둘 이상의 진입점이 있을 수 있습니다.  
  
    ![멀티 사이트 토폴로지](../../../../media/Step-2-Plan-the-Multisite-Infrastructure/RAMultisiteTopo2.png)  
  
멀티 사이트 진입점에서 단일 원격 액세스 서버에 여러 원격 액세스 서버를 구성할 수 또는 원격 액세스 서버를 클러스터 합니다.   
  
### <a name="active-directory-best-practices-and-recommendations"></a>Active Directory 모범 사례 및 권장 사항  
다음 권장 사항 및 Active Directory 배포는 멀티 사이트 시나리오에 대 한 제약 조건을 note:  
  
1.  각 Active Directory 사이트에는 하나 이상의 원격 액세스 서버 또는 클라이언트 컴퓨터에 대 한 멀티 사이트 진입점으로 작동 하는 서버 클러스터 포함 될 수 있습니다. 그러나 Active Directory 사이트는 진입점을 가질 필요가 없습니다.  
  
2.  멀티 사이트 진입점만 단일 Active Directory 사이트와 연결할 수 있습니다. Windows 8을 실행 하는 클라이언트 컴퓨터가 특정 진입점에 연결, 해당 진입점과 연결 된 Active Directory 사이트에 속하는 것으로 간주 됩니다.  
  
3.  각 Active Directory 사이트에 도메인 컨트롤러는 것이 좋습니다. 읽기 전용 도메인 컨트롤러 수 있습니다.  
  
4.  도메인 컨트롤러를 포함 하는 각 Active Directory 사이트, 진입점의 서버에 대 한 The GPO는 끝점과 연결 된 Active Directory 사이트에 도메인 컨트롤러 중 하나에 의해 관리 됩니다. 이 사이트에 있는 쓰기 가능한 도메인 컨트롤러가 없는 경우 가장 가까운 진입점에 구성 된 첫 번째 원격 액세스 서버에 있는 쓰기 가능한 도메인 컨트롤러에는 서버에 대 한 GPO 관리 됩니다. 가장 가까운 링크 비용 계산에 의해 결정 됩니다. 이 시나리오에서는 변경한 후 구성이 있을 수 있습니다 지연 GPO를 관리 하는 도메인 컨트롤러와 서버의 Active Directory 사이트에 읽기 전용 도메인 컨트롤러 간에 복제할 때는 note 합니다.  
  
5.  클라이언트 Gpo 및 선택적 응용 프로그램 서버 Gpo는 주 도메인 컨트롤러 (PDC) 에뮬레이터와 실행 중인 도메인 컨트롤러에서 관리 됩니다. 즉, Gpo 반드시 진입점을 포함 하는 Active Directory 사이트에 관리 되지 않는 클라이언트는 클라이언트에 연결 합니다.  
  
6.  Active Directory 사이트에 대 한 도메인 컨트롤러에 연결할 수 없는 경우 원격 액세스 서버 (있는 경우)는 사이트의 다른 도메인 컨트롤러에 연결 됩니다. 그렇지 않으면 다른 사이트는 업데이트 된 GPO를 검색 하 고 클라이언트를 인증 하는 도메인 컨트롤러에 연결 합니다. 두 경우 모두 원격 액세스 관리 콘솔 및 PowerShell cmdlet를 검색 하거나 구성 설정을 수정 하 여 도메인 컨트롤러를 사용할 때까지 사용할 수 없습니다. 다음에 유의하세요.  
  
    1.  PDC 에뮬레이터 역할을 실행 하는 서버에 사용할 수 없는 경우이 Gpo는 PDC 에뮬레이터 역할을 업데이트 하는 사용 가능한 도메인 컨트롤러를 지정 해야 합니다.  
  
    2.  서버 GPO를 관리 하는 도메인 컨트롤러를 사용할 수 없는 경우 새 도메인 컨트롤러를 진입점에 연결할 Set-daentrypointdc PowerShell cmdlet을 사용 합니다. 새 도메인 컨트롤러에는 cmdlet을 실행 하기 전에 최신 Gpo 있어야 합니다.  
  
## <a name="bkmk_2_2_SG"></a>2.2 보안 그룹 계획  
고급 설정으로는 단일 서버 배포 하는 동안 DirectAccess 통해 내부 네트워크에 액세스 하는 모든 클라이언트 컴퓨터 보안 그룹으로 수집 되었습니다. 멀티 사이트 배포에서는이 보안 그룹은 Windows 8 클라이언트 컴퓨터에 사용 됩니다. 멀티 사이트 배포에 대 한 Windows 7 클라이언트 컴퓨터에서 멀티 사이트 배포의 각 진입점에 대 한 별도 보안 그룹으로 수집 됩니다. 예를 들어 이전에 DA_Clients 그룹의 모든 클라이언트 컴퓨터를 그룹화 하면 이제 해당 그룹에서 모든 Windows 7 컴퓨터를 제거 하며 다른 보안 그룹에 배치 합니다. 예를 들어, 여러 Active Directory 사이트의 여러 진입점 토폴로지에서는 미국 진입점 (DA_Clients_US)에 대 한 보안 그룹 및 유럽 진입점 (DA_Clients_Europe)에 대 한 하나 만듭니다. DA_Clients_US 그룹에서 위해서 및 DA_Clients_Europe 그룹에서에 있는 모든 유럽에 있는 모든 Windows 7 클라이언트 컴퓨터를 배치 합니다. Windows 7 클라이언트 컴퓨터를 하지 않은 경우 Windows 7 컴퓨터에 대 한 보안 그룹 계획 필요가 없습니다.  
  
필요한 보안 그룹은 다음과 같습니다.  
  
-   모든 Windows 8 클라이언트 컴퓨터에 대 한 하나의 보안 그룹입니다. 각 도메인에 대 한 이러한 클라이언트에 대 한 고유한 보안 그룹을 만드는 것이 좋습니다.  
  
-   각 진입점에 대 한 Windows 7 클라이언트 컴퓨터를 포함 하는 고유한 보안 그룹입니다. 각 도메인에 대 한 고유한 그룹을 만드는 것이 좋습니다. 예를 들어 다음과 같은 가치를 제공해야 합니다. Domain1\DA_Clients_Europe; Domain2\DA_Clients_Europe; Domain1\DA_Clients_US; Domain2\DA_Clients_US 합니다.  
  
## <a name="bkmk_2_3_GPO"></a>2.3 그룹 정책 개체 계획  
원격 액세스 배포 중 구성 된 DirectAccess 설정은 Gpo에 수집 됩니다. DirectAccess 클라이언트의 원격 액세스 서버 및 필요에 따라 응용 프로그램 서버에 대 한 Gpo를 사용 하는 이미 단일 서버 배포 합니다. 멀티 사이트 배포에는 다음 Gpo 사항이 필요합니다.  
  
-   각 진입점에 대 한 서버 GPO입니다.  
  
-   Windows 8을 실행 하는 클라이언트 컴퓨터를 포함 하는 각 도메인에 대 한 GPO입니다.  
  
-   각 진입점과 Windows 7 클라이언트 컴퓨터를 포함 하는 각 도메인에 대 한 GPO입니다.  
  
Gpo는 다음과 같이 구성할 수 있습니다.  
  
-   **자동으로**-Gpo 원격 액세스에서 자동으로 생성 됩니다 지정할 수 있습니다. 기본 이름은 각 GPO에 대해 지정 되며 수정할 수 있습니다.  
  
-   **수동으로**-Active Directory 관리자가 수동으로 만든 Gpo를 사용할 수 있습니다.  
  
> [!NOTE]  
> DirectAccess가 특정 Gpo를 사용 하도록 구성 되어, 다른 Gpo를 사용 하도록 구성할 수 없습니다.  
  
### <a name="231-automatically-created-gpos"></a>2.3.1 자동으로 만들어진 Gpo  
자동으로 만들어진 GPO를 사용할 때 주의할 사항은 다음과 같습니다.  
  
-   자동으로 만들어진 GPO는 다음과 같이 위치 및 연결 대상 매개 변수에 따라 적용됩니다.  
  
    -   서버 GPO에 대 한 위치와 연결 매개 변수는 원격 액세스 서버를 포함 하는 도메인을 가리킵니다.  
  
    -   클라이언트 Gpo에 대 한 링크 대상 GPO가 만들어진 도메인의 루트에 설정 됩니다. 클라이언트 컴퓨터가 포함 된 각 도메인에 대 한 GPO 만들어지고 GPO를 각 도메인의 루트에 연결 됩니다. .  
  
-   자동으로 만들어진 Gpo에 대 한 원격 액세스 DirectAccess 설정을 적용 하려면 서버 관리자는 다음 권한이 필요 합니다.  
  
    -   GPO 만들기의 필수 도메인에 대 한 권한입니다.  
  
    -   선택한 모든 클라이언트 도메인 루트에 대한 연결 권한  
  
    -   DirectAccess는 모바일 컴퓨터에만 작동 하도록 구성 된 gpo WMI 필터를 만들 수 있는 권한이 필요 합니다.  
  
    -   진입점 (서버 GPO 도메인)와 연결 된 도메인의 루트에 대 한 링크 사용  
  
    -   원격 액세스 관리자에게 필요한 각 도메인에 대한 GPO 읽기 권한이 있는 것이 좋습니다. 따라서 원격 액세스 멀티 사이트 배포에 대 한 Gpo를 만들 때 이름이 중복 된 Gpo 존재 하지 않는 확인할 수 있습니다.  
  
    -   Active Directory 복제에 대 한 권한 진입점와 연결 된 도메인 즉, 진입점으로 가장 가까운 도메인 컨트롤러에서 서버 GPO의 진입점에 대 한 진입점을 처음 추가할 때 만들어집니다. 그러나 링크 만들기에서는 PDC 에뮬레이터를 사용할 경우에 지원 하므로 GPO는 만든 링크를 만들기 전에 PDC 에뮬레이터 역할을 실행 하는 도메인 컨트롤러에 도메인 컨트롤러에서 복제 되어야 합니다.  
  
Note 복제 및 Gpo 연결에 대 한 올바른 사용 권한이 존재 하지 않는 경우 경고가 발생 됩니다. 원격 액세스 작업은 계속 되지만 복제 및 연결 발생 하지 않습니다. 발급 경고 링크 하는 경우 링크 권한은 원위치 계측 한 후에 자동으로 생성 되지 않습니다. 대신 관리자가 수동으로 연결을 만들어야 합니다.  
  
### <a name="232-manually-created-gpos"></a>2.3.2 수동으로 만든 Gpo  
수동으로 만든 GPO를 사용할 때 주의할 사항은 다음과 같습니다.  
  
-   다음 Gpo 멀티 사이트 배포에 대해 수동으로 만들어야 합니다.  
  
    -   **서버 GPO**-도메인의 서버 GPO 각 진입점에 대 한 (에 진입점의 위치를 가리키는). 이 GPO는 각 원격 액세스 서버를 진입점에 적용 됩니다.  
  
    -   **클라이언트 GPO (Windows 7)** -A GPO 각 진입점 및 멀티 사이트 배포에서 진입점에 연결 하는 Windows 7 클라이언트 컴퓨터를 포함 하는 각 도메인에 대 한 합니다. 예를 들어 Domain1\DA_W7_Clients_GPO_Europe; Domain2\DA_W7_Clients_GPO_Europe; Domain1\DA_W7_Clients_GPO_US; Domain2\DA_W7_Clients_GPO_US 합니다. Windows 7 클라이언트 컴퓨터에 없는 진입점에 연결 됩니다, Gpo 필요 하지 않습니다.  
  
-   필요는 없습니다 추가 Gpo에 대 한 Windows 8 클라이언트 컴퓨터를 만들 수 있습니다. 단일 원격 액세스 서버 배포 될 때 클라이언트 컴퓨터를 포함 하는 각 도메인에 대 한 GPO는 이미 만들었습니다. 멀티 사이트 배포에서 이러한 클라이언트 Gpo는 Gpo에 대 한 Windows 8 클라이언트로 작동할 됩니다.  
  
-   멀티 사이트 배포 마법사에서 실행 단추를 클릭 하기 전에 Gpo가 존재 해야 합니다.  
  
-   수동으로 만든 GPO를 사용할 때는 전체 도메인에서 GPO에 대한 연결이 검색됩니다. GPO가 도메인에 연결되지 않은 경우 자동으로 도메인 루트에 연결이 만들어집니다. 연결을 만드는 데 필요한 권한이 없으면 경고가 발생합니다.  
  
-   때 사용 하 여 수동으로 만든 Gpo, DirectAccess 설정을 적용 하려면 원격 액세스 서버 관리자가 전체 GPO 사용 권한 (보안 편집, 삭제, 수정) 수동으로 만든 Gpo에 필요 합니다.  
  
Note 복제 및 Gpo 연결에 대 한 올바른 사용 권한이 존재 하지 않는 경우 경고가 발생 됩니다. 원격 액세스 작업은 계속 되지만 복제 및 연결 발생 하지 않습니다. 발급 경고 링크 하는 경우 링크 권한은 원위치 계측 한 후에 자동으로 생성 되지 않습니다. 대신 관리자가 수동으로 연결을 만들어야 합니다.  
  
### <a name="233-managing-gpos-in-a-multi-domain-controller-environment"></a>2.3.3 다중 도메인 컨트롤러 환경에서 Gpo 관리  
다음과 같이 각 GPO는 특정 도메인 컨트롤러에서 관리 됩니다.  
  
-   서버와 연결 된 Active Directory 사이트에 도메인 컨트롤러 중 하나에 의해 관리 되는 서버 GPO 또는 지점 항목의 첫 번째 서버에 가장 가까운 쓰기 가능한 도메인 컨트롤러에서 해당 사이트에 도메인 컨트롤러가 읽기 전용인 경우.  
  
-   클라이언트 Gpo는 PDC 에뮬레이터 역할을 실행 하는 도메인 컨트롤러에서 관리 됩니다.  
  
수동으로 하려는 경우에 GPO 설정을 참고를 다음 수정 합니다.  
  
-   서버 Gpo에 대 한 특정 진입점과 연결 된 도메인 컨트롤러를 식별 하기 위해 PowerShell cmdlet을 실행 `Get-DAEntryPointDC -EntryPointName <name of entry point>`합니다.  
  
-   네트워킹 PowerShell cmdlet 또는 그룹 정책 관리 콘솔을 사용 하 여 변경 하는 경우에 기본적으로 도메인 컨트롤러는 PDC 에뮬레이터 역할을 사용 됩니다.  
  
-   진입점 (서버 Gpo) 또는 PDC 에뮬레이터 (클라이언트에 대 한 Gpo)와 연결 된 도메인 컨트롤러를 도메인 컨트롤러에서 설정을 수정 하면 다음 note:  
  
    1.  설정을 수정 하기 전에 도메인 컨트롤러는 최신 GPO로 복제를 확인 하 고 [GPO 설정을 백업](https://go.microsoft.com/fwlink/?LinkID=257928), 전에 변경 합니다. GPO 업데이트 되지 않은 경우 복제 하는 동안 병합 충돌이 발생할 수 있습니다, 원격 액세스 구성이 손상 결과.  
  
    2.  설정을 수정한 후 변경 내용을 연결 된 Gpo는 도메인 컨트롤러에 복제 대기 해야 합니다. 복제가 완료 될 때까지 원격 액세스 관리 콘솔 또는 원격 액세스 PowerShell cmdlet을 사용 하 여 추가로 변경 안 됩니다. 복제가 완료 되기 전에 두 명의 서로 다른 도메인 컨트롤러에서 GPO를 편집, 병합 충돌이 발생할 수 있습니다, 구성이 손상 결과  
  
-   사용 하 여 기본 설정을 변경할 수 또는 **도메인 컨트롤러 변경** 대화 상자는 그룹 정책 관리 콘솔에서 또는 사용 하는 **Open-netgpo** PowerShell cmdlet, 변경 내용이 콘솔을 사용 하 여 만든 또는 네트워킹 cmdlet은 지정한 도메인 컨트롤러를 사용 합니다.  
  
    1.  이를 위해 그룹 정책 관리 콘솔에서 도메인 또는 사이트 컨테이너를 마우스 오른쪽 단추로 클릭 하 고 클릭 **도메인 컨트롤러 변경**합니다.  
  
    2.  PowerShell에서 이렇게 하려면 Open-netgpo cmdlet에 대 한 도메인 컨트롤러 매개 변수를 지정 합니다. 예를 들어 유럽 하려면 도메인 컨트롤러를 사용 하 여 domain1\DA_Server_GPO 이라는 GPO에서 Windows 방화벽에서 프라이빗 및 공용 프로필을 사용 하려면 다음을 수행 합니다.  
  
        ```  
        $gpoSession = Open-NetGPO -PolicyStore "domain1\DA_Server_GPO _Europe" -DomainController "europe-dc.corp.contoso.com"  
        Set-NetFirewallProfile -GpoSession $gpoSession -Name @("Private","Public") -Enabled True  
        Save-NetGPO -GpoSession $gpoSession  
        ```  
  
#### <a name="modifying-domain-controller-association"></a>도메인 컨트롤러 연결 수정  
멀티 사이트 배포에서 구성 일관성을 유지하려면 각 GPO를 한 도메인 컨트롤러로 관리하는 것이 중요합니다. 일부 시나리오에서는 GPO에 대 한 다른 도메인 컨트롤러를 할당 하려면 필요한 수 있습니다.  
  
-   **도메인 컨트롤러가 유지 관리 및 가동 중지 시간**-서로 다른 도메인 컨트롤러에 GPO를 관리 해야 할 수 있습니다 GPO를 관리 하는 도메인 컨트롤러를 사용할 수 없습니다.  
  
-   **구성 배포의 최적화**-네트워크 인프라 변경 후의 진입점으로 동일한 Active Directory 사이트에 도메인 컨트롤러에는 진입점의 서버 GPO를 관리 하는 데 필요한 수 있습니다.   
  
## <a name="bkmk_2_4_DNS"></a>2.4 DNS 계획  
멀티 사이트 배포에 대 한 DNS를 계획할 때 다음 note:  
  
1.  클라이언트 컴퓨터는 원격 액세스 서버에 연결 하기 위해 ConnectTo 주소를 사용 합니다. 배포의 각 진입점에 다른 ConnectTo 주소가 필요합니다. 각 항목 지점 ConnectTo 주소는 공용 DNS에서 사용할 수 있어야 하 고 선택 하는 주소는 IP-HTTPS 연결에 대 한 배포 하는 IP-HTTPS 인증서의 주체 이름 일치 해야 합니다.   
  
2.  또한 원격 액세스 적용 대칭 라우팅; 따라서 멀티 사이트 배포 사용 하는 경우 Teredo 및 IP-HTTPS 클라이언트 중 하나만 연결할 수 있습니다. 기본 IPv6 클라이언트 연결을 허용 하려면 ConnectTo 주소 (IP HTTPS URL) 모두의 외부 (인터넷) IPv6 및 IPv4 주소에 원격 액세스 서버 확인 되어야 합니다.  
  
3.  원격 액세스는 DirectAccess 클라이언트 컴퓨터에서 내부 네트워크에 대한 연결을 확인하는 데 사용하는 기본 웹 검색을 만듭니다. 단일 서버 구성 중 DNS에 다음 이름은 등록 해야 합니다.  
  
    1.  directaccess WebProbeHost 해야 해결 원격 액세스 서버의 내부 IPv4 주소 또는 IPv6 전용 환경의 IPv6 주소입니다.  
  
    2.  localhost (루프백) 주소에 대 한 해결 directaccess CorpConnectivityHost 해야 (중 하나:: 1 또는 i p v 6이 회사 네트워크에 배포 되었는지 여부에 따라 127.0.0.1).  
  
    멀티 사이트 배포에서 Directaccess-webprobehost에 대 한 추가 DNS 항목이 각 진입점에 대 한 생성 되어야 합니다. 진입점을 추가할 때 자동으로이 항목을 만들려면 추가 Directaccess-webprobehost 원격 액세스 시도 합니다. 그러나 실패 하는 경우 경고가 표시 되며 항목을 수동으로 만들어야 합니다.  
  
    > [!NOTE]  
    > DNS 청소, DNS 인프라에서 사용할 때 원격 액세스에서 자동으로 생성 하는 DNS 항목에 청소를 사용 하지 않도록 설정 하는 것이 좋습니다.  
  

  



