---
title: 클러스터 인식 업데이트 개요
ms.topic: article
ms.prod: windows-server-threshold
ms.manager: dongill
author: JasonGerend
ms.author: jgerend
ms.technology: storage-failover-clustering
ms.date: 08/06/2018
description: CAU 클러스터 인식 업데이트 ()는 Windows Server를 실행 하는 클러스터에서 소프트웨어 업데이트 설치를 자동화 합니다.
ms.assetid: 3c2993b4-aa81-452b-a5c3-3724ad95d892
ms.openlocfilehash: 77ccfe7dc9a769d602ff069d5f1d8e77522aa001
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59827424"
---
# <a name="cluster-aware-updating-overview"></a>클러스터 인식 업데이트 개요

> 적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 클러스터의 개요를 제공\-인식 업데이트 \(CAU\), 가용성을 유지 하면서 클러스터 된 서버 소프트웨어에서 업데이트 프로세스를 자동화 하는 기능입니다.

> [!NOTE]
> 업데이트할 때 [저장소 공간 다이렉트](../storage/storage-spaces/storage-spaces-direct-overview.md) 클러스터를 사용 하 여 좋습니다 클러스터 인식 업데이트 합니다.
  
## <a name="BKMK_OVER"></a>기능 설명  
클러스터 인식 업데이트는에서 서버를 업데이트할 수 있는 자동화 된 기능을 [장애 조치 클러스터](failover-clustering-overview.md) 업데이트 프로세스 중 가용성 거의 또는 전혀 손실 합니다. 업데이트 실행 중 다음 작업을 수행 투명 하 게 클러스터 인식 업데이트:  

1. 각 노드의 클러스터 노드 유지 관리 모드에 넣습니다.
2. 노드 외부로 클러스터 된 역할을 이동합니다.
3. 업데이트 및 모든 종속 업데이트를 설치합니다.
4. 필요한 경우 다시 시작을 수행 합니다.
5. 유지 관리 모드에서 노드를 제공합니다.
6. 노드에서 클러스터 된 역할을 복원합니다.
7. 업데이트를 다음 노드로 이동 합니다.

클러스터에 있는 클러스터된 많은 역할의 경우 자동 업데이트 프로세스를 통해 계획된 장애 조치(failover)가 시작됩니다. 이로 인해 연결된 클라이언트에 대한 서비스가 일시적으로 중단될 수 있습니다. 그러나 하이퍼 등의 지속적으로 사용 가능한 워크 로드의 경우\-V 실시간 마이그레이션 또는 파일 서버를 사용 하 여 SMB 투명 장애 조치 클러스터 인식 업데이트를 사용 하 여 서비스 가용성에 영향을 주지 않고 클러스터 업데이트를 조정할 수 있습니다.    
  
## <a name="practical-applications"></a>유용한 팁  
  
-   CAU 클러스터 된 서비스의 서비스 중단, 수동, 업데이트에 대 한 필요를 줄여 대 한 줄어들고 끝\-에\-최종 클러스터 관리자에 대 한 더 신뢰할 수 있는 프로세스를 업데이트 합니다. CAU 기능은 지속적으로 사용 가능한 파일 서버 등의 지속적으로 사용 가능한 클러스터 워크 로드와 함께 사용 하면 \(SMB 투명 장애 조치를 사용 하 여 파일 서버 워크 로드\) 또는 하이퍼\-V, 클러스터 클라이언트에 대 한 서비스 가용성에 전혀 영향을 사용 하 여 업데이트를 수행할 수 있습니다.  
  
-   CAU는 기업 전체에서 일관된 IT 프로세스를 도입합니다. 장애 조치 클러스터의 다른 클래스에 대 한 생성 및 다음는 IT 조직 전체의 CAU 배포에서 업데이트를 일관성 있게 적용할 클러스터 다른 줄으로 관리 되는 경우에 파일 공유에서 중앙에서 관리할 수 업데이트 실행 프로필 \-의\-비즈니스 또는 관리자입니다.  
  
-   CAU는 정기적인 간격(매일, 매주, 매월)으로 업데이트 실행을 예약할 수 있어 다른 IT 관리 프로세스를 통한 클러스터 업데이트를 쉽게 조정할 수 있습니다.  
  
-   CAU는 클러스터에서 클러스터 소프트웨어 인벤토리를 업데이트 하는 확장 가능한 아키텍처를 제공\-방식으로 인식 합니다. 이 Windows Update 나 Microsoft Update에 게시 되지 않습니다 또는 microsoft의 예를 들어 업데이트에 대 한 제공 되지 않는 소프트웨어 업데이트의 설치를 조정 하려면 게시자에서 사용 될 수 없는\-Microsoft 장치 드라이버입니다.  
  
-   CAU 셀프\-"형 클러스터" 어플라이언스를 통해 업데이트 모드 \(일반적으로 하나의 섀시에 패키지를 클러스터 된 실제 컴퓨터 집합\) 업데이트 되도록 합니다. 일반적으로 이러한 장비는 최소한의 로컬 IT 지원이 제공되는 지점에서 클러스터를 관리할 수 있도록 배포됩니다. 자체\-업데이트 모드 이러한 배포 시나리오에서 뛰어난 가치를 제공 합니다.  
  
## <a name="important-functionality"></a>중요 기능  
다음은 중요 한 클러스터 인식 업데이트 기능에 대 한 설명을입니다.  
  
-   사용자 인터페이스 \(UI\) -미리 보기, 적용, 모니터링 하는 데 및 업데이트를 보고할 수 있는 cmdlet 집합과 클러스터 인식 업데이트 창-  
  
-   끝\-하\-클러스터의 자동화를 종료\-업데이트 작업 \(업데이트 실행\), 하나 이상의 업데이트 코디네이터 컴퓨터에서 오케스트레이션  
  
-   기본 플러그\-는 기존 Windows Update 에이전트를 사용 하 여 통합 \(WUA\) 및 Windows Server Update Services \(WSUS\) 중요 한 Microsoft를 적용 하려면 Windows Server의 인프라 업데이트  
  
-   두 번째 플러그\-으로 Microsoft 핫픽스를 적용 하려면 사용할 수 있으며 비 적용할 사용자 지정할 수 있습니다\-Microsoft 업데이트  
  
-   노드당 업데이트를 다시 시도할 최대 횟수와 같은 업데이트 실행 옵션에 대한 설정을 사용하여 구성하는 업데이트 실행 프로필. 업데이트 실행 프로필을 사용하면 여러 업데이트 실행 간에 동일한 설정을 빠르게 다시 사용하고 다른 장애 조치(failover) 클러스터와 업데이트 설정을 쉽게 공유할 수 있습니다.  
  
-   새 플러그 인을 지 원하는 확장 가능한 아키텍처\-다른 노드를 조정 하는 개발에서\-BIOS 업데이트 도구 및 네트워크 어댑터나 호스트 버스 어댑터 클러스터에사용자지정소프트웨어설치관리자와같은도구업데이트\( HBA\) 도구를 업데이트 합니다.  
  
클러스터 인식 업데이트는 업데이트 작업 두 가지 모드로 전체 클러스터를 조정할 수 있습니다.  
  
-   **Self\-업데이트 모드** 이 모드에서는 CAU 클러스터 된 역할이 업데이트 해야 하는 장애 조치 클러스터에서 워크 로드로 구성 되 고는 연결 된 업데이트 일정이 정의 됩니다. 클러스터는 기본 또는 사용자 지정 업데이트 실행 프로필을 사용하여 예약된 시간에 자동 업데이트됩니다. 업데이트 실행 중에는 CAU 업데이트 코디네이터 프로세스가 현재 CAU 클러스터된 역할을 소유하고 있는 노드에서 시작되고, 각 클러스터 노드에서 후속 업데이트가 수행됩니다. 현재 클러스터 노드를 업데이트하기 위해 CAU 클러스터된 역할이 다른 클러스터 노드로 장애 조치(failover)되고 해당 노드의 새 업데이트 코디네이터 프로세스가 업데이트 실행을 제어합니다. 자체\-업데이트 모드에서 CAU 있습니다 완전히 자동화를 사용 하 여 장애 조치 클러스터를 업데이트, 종료\-에\-종료 프로세스를 업데이트 합니다. 관리자에서 업데이트를 트리거할 수도 있습니다\-이 모드에서 요구 하거나 원격 사용 하 여\-접근 방식을 원하는 경우 업데이트 합니다. 자체\-업데이트 모드를 관리자 정보를 얻을 수 요약 업데이트 실행에 대 한 중에서 클러스터에 연결 하 고 실행 하 여 합니다 **가져올\-CauRun** Windows PowerShell cmdlet.  
  
-   **원격\-업데이트 모드** 이 모드에서는 업데이트 코디네이터 라는 원격 컴퓨터에는 CAU 도구를 사용 하 여 구성 합니다. 업데이트 코디네이터는 업데이트 실행 중에 업데이트되는 클러스터의 구성원이 아닙니다. 원격 컴퓨터에서 관리자가 트리거는에서\-기본 또는 사용자 지정 업데이트 실행 프로필을 사용 하 여 업데이트 실행을 요청 합니다. 원격\-모드를 업데이트 하는 것은 실시간 모니터링을 위한 유용\-진행률 업데이트 실행 중, Server Core 설치에서 실행 중인 클러스터에 대 한 시간입니다.  
  
## <a name="hardware-and-software-requirements"></a>하드웨어 및 소프트웨어 요구 사항  

CAU는 Server Core 설치를 포함 하 여 Windows Server의 모든 버전에서 사용할 수 있습니다. 자세한 요구 사항 정보를 참조 하세요. [클러스터 인식 업데이트 요구 사항 및 모범 사례](cluster-aware-updating-requirements.md)합니다.

### <a name="installing-cluster-aware-updating"></a>클러스터 인식 업데이트 설치
CAU를 사용 하려면 Windows server에서 장애 조치 클러스터링 기능을 설치 하 고 장애 조치 클러스터를 만듭니다. CAU 기능을 지원하는 구성 요소는 각 클러스터 노드에 자동으로 설치됩니다.

다음 도구를 사용하여 장애 조치(faillover) 클러스터링 기능을 설치할 수 있습니다.
- 서버 관리자의 역할 및 기능 추가 마법사
- [Install-windowsfeature](https://docs.microsoft.com/powershell/module/servermanager/Install-WindowsFeature?view=winserver2012r2-ps&viewFallbackFrom=win10-ps) Windows PowerShell cmdlet
- DISM(배포 이미지 서비스 및 관리) 명령줄 도구

자세한 내용은 [장애 조치 클러스터링 기능 설치](create-failover-cluster.md#install-the-failover-clustering-feature)합니다.

또한 원격 서버 관리 도구의 일부인 서버 관리자에서 장애 조치 클러스터링 기능을 설치할 때 기본적으로 설치 되어 있으며 장애 조치 클러스터링 도구를 설치 해야 합니다. 장애 조치 클러스터링 도구는 클러스터 인식 업데이트 사용자 인터페이스 및 PowerShell cmdlet을 포함 합니다. 

다른 CAU 업데이트 모드를 지원하려면 다음과 같이 장애 조치(failover) 클러스터링 도구를 설치해야 합니다.

- CAU를 사용 하 여 자체를\-각 클러스터 노드에 장애 조치 클러스터링 도구를 설치 모드를 업데이트 합니다.   
  
- 원격을 사용 하도록 설정 하려면\-장애 조치 클러스터에 네트워크 연결 되어 있는 컴퓨터에 장애 조치 클러스터링 도구를 설치 모드를 업데이트 합니다.  
  
> [!NOTE]  
> -   최신 버전의 Windows Server의 클러스터 인식 업데이트를 관리 하려면 Windows Server 2012에서 장애 조치 클러스터링 도구를 사용할 수 없습니다. 
> -   원격 에서만에서 CAU를 사용 하려면\-업데이트 모드를 클러스터 노드에서 장애 조치 클러스터링 도구 설치 필요 없음. 그러나 특정 CAU 기능을 사용할 수 없게 됩니다. 자세한 내용은 [요구 사항 및 클러스터에 대 한 모범 사례\-인식 업데이트](cluster-aware-updating-requirements.md)합니다.  
> -   자체 에서만 CAU를 사용 하는 경우\-모드 업데이트는 CAU 도구가 설치 및 업데이트를 조정 하는 컴퓨터 일 수 없습니다 장애 조치 클러스터의 멤버인입니다.  
  
### <a name="enabling-self-updating-mode"></a>자동 업데이트 모드를 사용 하도록 설정
자동 업데이트 모드를 사용 하려면 장애 조치 클러스터에 클러스터 인식 업데이트 클러스터 된 역할을 추가 해야 합니다. 이렇게 하려면 다음 방법 중 하나를 사용 합니다.
- 서버 관리자에서 선택 **도구가** > **Cluster-aware Updating**, 클러스터 인식 업데이트 창에서 선택한 **구성 클러스터 자동 업데이트 옵션**. 
- PowerShell 세션에서 실행 합니다 [Add-cauclusterrole](https://docs.microsoft.com/powershell/module/clusterawareupdating/Add-CauClusterRole?view=win10-ps) cmdlet.  
  
CAU를 제거 하려면 서버 관리자를 사용 하 여 장애 조치 클러스터링 기능 또는 장애 조치 클러스터링 도구를 제거 합니다 [Uninstall-windowsfeature](https://docs.microsoft.com/powershell/module/servermanager/Uninstall-WindowsFeature?view=win10-ps) cmdlet 또는 DISM 명령을\-명령줄 도구입니다.  
  
### <a name="additional-requirements-and-best-practices"></a>추가 요구 사항 및 모범 사례  

CAU로 클러스터 노드를 성공적으로 업데이트하고 CAU를 사용하도록 장애 조치(failover) 클러스터 환경을 구성하기 위한 추가 지침을 보려면 CAU 모범 사례 분석기를 실행할 수 있습니다.  
  
CAU는 CAU 모범 사례 분석기를 실행 하는 방법에 대 한 정보를 사용 하는 것에 대 한 모범 사례와 자세한 요구 사항에 대 한 참조 [요구 사항 및 클러스터에 대 한 모범 사례\-인식 업데이트](cluster-aware-updating-requirements.md)합니다.  
  
### <a name="starting-cluster-aware-updating"></a>클러스터 인식 업데이트 시작  
  
##### <a name="to-start-cluster-aware-updating-from-server-manager"></a>서버 관리자에서 클러스터 인식 업데이트 시작 하려면  
  
1.  서버 관리자를 시작합니다.  
  
2.  다음 중 하나를 수행합니다.  
  
    -   에 **도구** 메뉴에서 클릭 **클러스터\-인식 업데이트**합니다.  
  
    -   하나 이상의 클러스터 노드 또는 클러스터에서 서버 관리자에 추가 되 면 합니다 **모든 서버** 페이지에서 오른쪽\-노드의 이름을 클릭 \(또는 클러스터의 이름을\), 클릭 하 고  **클러스터 업데이트**합니다.  
  
## <a name="see-also"></a>참조  
다음 링크를 클러스터 인식 업데이트를 사용 하는 방법에 대 한 자세한 정보를 제공 합니다.  
  
-   [요구 사항 및 클러스터에 대 한 모범 사례\-인식 업데이트](cluster-aware-updating.md)  
  
-   [클러스터\-인식 업데이트: 질문과 대답](cluster-aware-updating-faq.md)  
  
-   [고급 옵션 및 cau 업데이트 실행된 프로필](cluster-aware-updating-options.md)  
  
-   [CAU 플러그 인을 어떻게\-기능 작업](cluster-aware-updating-plug-ins.md)  
  
-   [클러스터\-인식 업데이트 Windows PowerShell의 Cmdlet](https://docs.microsoft.com/powershell/module/clusterawareupdating/?view=win10-ps&viewFallbackFrom=winserverr2-ps)  
  
-   [클러스터\-인식 업데이트 플러그 인\-참조](https://docs.microsoft.com/previous-versions/windows/desktop/mscs/cluster-aware-update-plug-in-interfaces-and-classes)  
  

