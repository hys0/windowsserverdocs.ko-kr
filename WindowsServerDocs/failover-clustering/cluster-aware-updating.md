---
title: 클러스터 인식 업데이트 개요
ms.topic: article
ms.prod: windows-server
ms.manager: dongill
author: JasonGerend
ms.author: jgerend
ms.technology: storage-failover-clustering
ms.date: 08/06/2018
description: CAU (클러스터 인식 업데이트)는 Windows Server를 실행 하는 클러스터에서 소프트웨어 업데이트 설치를 자동화 합니다.
ms.assetid: 3c2993b4-aa81-452b-a5c3-3724ad95d892
ms.openlocfilehash: e96223e0b4b44e87ade9dc8eb875f9aa7104f451
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71361247"
---
# <a name="cluster-aware-updating-overview"></a>클러스터 인식 업데이트 개요

> 적용 대상: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 가용성을 유지 하면서 클러스터 된 서버의 소프트웨어 업데이트 프로세스를 자동화 하는 기능인 Cluster @ no__t-0Aware 업데이트 \(CAU @ no__t-2에 대 한 개요를 제공 합니다.

> [!NOTE]
> [스토리지 공간 다이렉트](../storage/storage-spaces/storage-spaces-direct-overview.md) 클러스터를 업데이트할 때 클러스터 인식 업데이트를 사용 하는 것이 좋습니다.
  
## <a name="BKMK_OVER"></a>기능 설명  
클러스터 인식 업데이트는 [장애 조치 (failover) 클러스터](failover-clustering-overview.md) 의 서버를 업데이트 하는 동안 가용성을 거의 또는 전혀 손실 하지 않고 업데이트할 수 있는 자동화 된 기능입니다. 업데이트를 실행 하는 동안 클러스터 인식 업데이트는 다음 작업을 투명 하 게 수행 합니다.  

1. 클러스터의 각 노드를 노드 유지 관리 모드로 전환 합니다.
2. 클러스터 된 역할을 노드 밖으로 이동 합니다.
3. 업데이트 및 모든 종속 업데이트를 설치 합니다.
4. 필요한 경우 다시 시작을 수행 합니다.
5. 노드를 유지 관리 모드에서 제외 합니다.
6. 노드에서 클러스터 된 역할을 복원 합니다.
7. 를 이동 하 여 다음 노드를 업데이트 합니다.

클러스터에 있는 클러스터된 많은 역할의 경우 자동 업데이트 프로세스를 통해 계획된 장애 조치(failover)가 시작됩니다. 이로 인해 연결된 클라이언트에 대한 서비스가 일시적으로 중단될 수 있습니다. 그러나 실시간 마이그레이션을 사용 하는 Hyper-v 또는 SMB (투명 한 장애 조치)를 사용 하는 파일 서버와 같이 지속적으로 사용 가능한 워크 로드의 경우 클러스터 인식 업데이트는 서비스 가용성에 영향을 주지 않고 클러스터 업데이트를 조정할 수 있습니다.    
  
## <a name="practical-applications"></a>유용한 팁  
  
-   CAU는 클러스터 된 서비스의 서비스 중단을 줄이고, 수동 업데이트 해결 방법이 필요 하지 않으며, 관리자가 end @ no__t-0to @ no__t-1end 클러스터 업데이트 프로세스의 안정성을 더욱 안정적으로 만듭니다. CAU 기능을 지속적으로 사용 가능한 클러스터 워크 로드와 함께 사용 하는 경우 (예: SMB 투명 장애 조치 (Failover)를 사용 하는 파일 서버 작업 @no__t SMB 투명 장애 조치 (Failover) @ no__t 또는 Hyper-v no__t-2V) 클러스터 업데이트를 수행할 수 있습니다. 클라이언트의 서비스 가용성에 영향을 주지 않습니다.  
  
-   CAU는 기업 전체에서 일관된 IT 프로세스를 도입합니다. 여러 장애 조치 (failover) 클러스터 클래스에 대해 업데이트 실행 프로필을 만든 다음 파일 공유에서 중앙 집중식으로 관리 하면 클러스터를 다른 방식으로 관리 하는 경우에도 IT 조직 전체의 CAU 배포에서 업데이트를 일관 되 게 적용할 수 있습니다. @ no__t의 @ no__t-1 줄은 비즈니스 또는 관리자입니다.  
  
-   CAU는 정기적인 간격(매일, 매주, 매월)으로 업데이트 실행을 예약할 수 있어 다른 IT 관리 프로세스를 통한 클러스터 업데이트를 쉽게 조정할 수 있습니다.  
  
-   CAU는 클러스터에서 클러스터 소프트웨어 인벤토리를 업데이트 하기 위한 확장 가능한 아키텍처를 제공 합니다. @ no__t-0. 게시자가 Windows 업데이트 또는 Microsoft 업데이트에 게시 되지 않았거나 Microsoft에서 제공 하지 않는 소프트웨어 업데이트 (예: @ no__t-0이 아닌 Microsoft 장치 드라이버 업데이트)의 설치를 조정 하는 데 사용할 수 있습니다.  
  
-   CAU self @ no__t-0updating 모드를 사용 하면 일반적으로 하나의 섀시 @ no__t-2에 패키지 된 클러스터 된 물리적 컴퓨터의 "어플라이언스 \(a" 어플라이언스 집합을 업데이트할 수 있습니다. 일반적으로 이러한 장비는 최소한의 로컬 IT 지원이 제공되는 지점에서 클러스터를 관리할 수 있도록 배포됩니다. Self @ no__t-0updating 모드는 이러한 배포 시나리오에서 뛰어난 가치를 제공 합니다.  
  
## <a name="important-functionality"></a>중요 기능  
다음은 중요 한 클러스터 인식 업데이트 기능에 대 한 설명입니다.  
  
-   사용자 인터페이스 \(UI @ no__t-1-클러스터 인식 업데이트 창-업데이트를 미리 보고 적용 하 고 모니터링 하 고 보고 하는 데 사용할 수 있는 cmdlet 집합  
  
-   End @ no__t-0to @ no__t-1end automation cluster @ no__t 업데이트 작업 \( 업데이트 실행 @ no__t-4, 오케스트레이션 하나 이상의 업데이트 코디네이터 컴퓨터  
  
-   에서 기존 Windows 업데이트 에이전트 \(WUA @ no__t-2 및 Windows Server Update Services \(WSUS @ no__t-4 인프라와 통합 되어 중요 한 Microsoft 업데이트를 적용 하는 기본 플러그 @ no__t-0  
  
-   Microsoft 핫픽스를 적용 하는 데 사용할 수 있으며 @ no__t-1Microsoft 업데이트를 적용 하도록 사용자 지정할 수 있는 두 번째 플러그 @ no__t-0in  
  
-   노드당 업데이트를 다시 시도할 최대 횟수와 같은 업데이트 실행 옵션에 대한 설정을 사용하여 구성하는 업데이트 실행 프로필. 업데이트 실행 프로필을 사용하면 여러 업데이트 실행 간에 동일한 설정을 빠르게 다시 사용하고 다른 장애 조치(failover) 클러스터와 업데이트 설정을 쉽게 공유할 수 있습니다.  
  
-   사용자 지정 소프트웨어 설치 관리자, BIOS 업데이트 도구, 네트워크 어댑터 또는 호스트 버스 어댑터 \(HBA @ no__t-3과 같이 클러스터에서 다른 노드 @ no__t-1updating 도구를 조정 하기 위해 개발 중에 새 플러그 @ no__t-0in 지 원하는 확장 가능한 아키텍처입니다. 업데이트 도구.  
  
클러스터 인식 업데이트는 다음 두 가지 모드로 전체 클러스터 업데이트 작업을 조정할 수 있습니다.  
  
-   **Self @ no__t-1 업데이트 모드** 이 모드에서는 CAU 클러스터 된 역할이 업데이트할 장애 조치 (failover) 클러스터에서 작업으로 구성 되 고 연결 된 업데이트 일정이 정의 됩니다. 클러스터는 기본 또는 사용자 지정 업데이트 실행 프로필을 사용하여 예약된 시간에 자동 업데이트됩니다. 업데이트 실행 중에는 CAU 업데이트 코디네이터 프로세스가 현재 CAU 클러스터된 역할을 소유하고 있는 노드에서 시작되고, 각 클러스터 노드에서 후속 업데이트가 수행됩니다. 현재 클러스터 노드를 업데이트하기 위해 CAU 클러스터된 역할이 다른 클러스터 노드로 장애 조치(failover)되고 해당 노드의 새 업데이트 코디네이터 프로세스가 업데이트 실행을 제어합니다. Self @ no__t-0updating 모드에서 CAU는 완전히 자동화 된 end @ no__t-1 ~ @ no__t-2end 업데이트 프로세스를 사용 하 여 장애 조치 (failover) 클러스터를 업데이트할 수 있습니다. 관리자는이 모드에서 @ no__t-0demand에 대 한 업데이트를 트리거하거나 원하는 경우 원격 @ no__t-1 업데이트 방법을 사용할 수도 있습니다. Self @ no__t-0updating 모드에서 관리자는 클러스터에 연결 하 고 **get @ no__t-2CauRun** Windows PowerShell cmdlet을 실행 하 여 진행 중인 업데이트 실행에 대 한 요약 정보를 가져올 수 있습니다.  
  
-   **원격 @ no__t-1 업데이트 모드** 이 모드의 경우 업데이트 코디네이터 라는 원격 컴퓨터가 CAU 도구를 사용 하 여 구성 됩니다. 업데이트 코디네이터는 업데이트 실행 중에 업데이트되는 클러스터의 구성원이 아닙니다. 관리자는 원격 컴퓨터에서 기본 또는 사용자 지정 업데이트 실행 프로필을 사용 하 여 @ no__t-0demand 업데이트 실행 시를 트리거합니다. Remote @ no__t-0updating 모드는 업데이트 실행 중 및 Server Core 설치에서 실행 되는 클러스터에 대 한 실제 @ no__t-1 시간 진행률을 모니터링 하는 데 유용 합니다.  
  
## <a name="hardware-and-software-requirements"></a>하드웨어 및 소프트웨어 요구 사항  

CAU는 Server Core 설치를 포함 하 여 모든 버전의 Windows Server에서 사용할 수 있습니다. 자세한 요구 사항 정보는 [클러스터 인식 업데이트 요구 사항 및 모범 사례](cluster-aware-updating-requirements.md)를 참조 하세요.

### <a name="installing-cluster-aware-updating"></a>클러스터 인식 업데이트 설치
CAU를 사용 하려면 Windows Server에 장애 조치 (Failover) 클러스터링 기능을 설치 하 고 장애 조치 (failover) 클러스터를 만듭니다. CAU 기능을 지원하는 구성 요소는 각 클러스터 노드에 자동으로 설치됩니다.

다음 도구를 사용하여 장애 조치(faillover) 클러스터링 기능을 설치할 수 있습니다.
- 서버 관리자의 역할 및 기능 추가 마법사
- 1Windows PowerShell cmdlet을 @no__t [설치](https://docs.microsoft.com/powershell/module/servermanager/Install-WindowsFeature?view=winserver2012r2-ps&viewFallbackFrom=win10-ps)합니다.
- DISM(배포 이미지 서비스 및 관리) 명령줄 도구

자세한 내용은 [장애 조치 (Failover) 클러스터링 기능 설치](create-failover-cluster.md#install-the-failover-clustering-feature)를 참조 하세요.

또한 원격 서버 관리 도구의 일부인 장애 조치 (failover) 클러스터링 도구를 설치 해야 하며, 서버 관리자에 장애 조치 (Failover) 클러스터링 기능을 설치할 때 기본적으로 설치 됩니다. 장애 조치 (Failover) 클러스터링 도구에는 클러스터 인식 업데이트 사용자 인터페이스 및 PowerShell cmdlet이 포함 됩니다. 

다른 CAU 업데이트 모드를 지원하려면 다음과 같이 장애 조치(failover) 클러스터링 도구를 설치해야 합니다.

- Self @ no__t-0updating 모드에서 CAU를 사용 하려면 각 클러스터 노드에 장애 조치 (Failover) 클러스터링 도구를 설치 합니다.   
  
- Remote @ no__t-0updating 모드를 사용 하도록 설정 하려면 장애 조치 (failover) 클러스터에 네트워크로 연결 된 컴퓨터에 장애 조치 (Failover) 클러스터링 도구를 설치 합니다.  
  
> [!NOTE]  
> -   Windows Server 2012의 장애 조치 (Failover) 클러스터링 도구를 사용 하 여 최신 버전의 Windows Server에서 클러스터 인식 업데이트를 관리할 수 없습니다. 
> -   원격 @ no__t-0updating 모드 에서만 CAU를 사용 하려면 클러스터 노드에 장애 조치 (Failover) 클러스터링 도구를 설치 해야 합니다. 그러나 특정 CAU 기능을 사용할 수 없게 됩니다. 자세한 내용은 [클러스터 @ no__t-1 인식 업데이트에 대 한 요구 사항 및 모범 사례](cluster-aware-updating-requirements.md)를 참조 하세요.  
> -   자체 @ no__t-0updating 모드 에서만 CAU를 사용 하는 경우가 아니면 CAU 도구가 설치 되 고 업데이트를 조정 하는 컴퓨터는 장애 조치 (failover) 클러스터의 구성원이 될 수 없습니다.  
  
### <a name="enabling-self-updating-mode"></a>자동 업데이트 모드 사용
자동 업데이트 모드를 사용 하도록 설정 하려면 클러스터 인식 업데이트 클러스터 된 역할을 장애 조치 (failover) 클러스터에 추가 해야 합니다. 이렇게 하려면 다음 방법 중 하나를 사용 합니다.
- 서버 관리자에서 **도구** > **클러스터 인식 업데이트**를 선택 하 고 클러스터 인식 업데이트 창에서 **클러스터 자동 업데이트 옵션 구성**을 선택 합니다. 
- PowerShell 세션에서 [add-cauclusterrole](https://docs.microsoft.com/powershell/module/clusterawareupdating/Add-CauClusterRole?view=win10-ps) cmdlet을 실행 합니다.  
  
CAU를 제거 하려면 서버 관리자, [uninstall](https://docs.microsoft.com/powershell/module/servermanager/Uninstall-WindowsFeature?view=win10-ps) CMDLET 또는 DISM 명령 @ no__t-1line 도구를 사용 하 여 장애 조치 (Failover) 클러스터링 기능 또는 장애 조치 (Failover) 클러스터링 도구를 제거 합니다.  
  
### <a name="additional-requirements-and-best-practices"></a>추가 요구 사항 및 모범 사례  

CAU로 클러스터 노드를 성공적으로 업데이트하고 CAU를 사용하도록 장애 조치(failover) 클러스터 환경을 구성하기 위한 추가 지침을 보려면 CAU 모범 사례 분석기를 실행할 수 있습니다.  
  
CAU 사용에 대 한 자세한 요구 사항 및 모범 사례와 CAU 모범 사례 분석기를 실행 하는 방법에 대 한 자세한 내용은 [클러스터 @ no__t-1 인식 업데이트에 대 한 요구 사항 및 모범 사례](cluster-aware-updating-requirements.md)를 참조 하세요.  
  
### <a name="starting-cluster-aware-updating"></a>클러스터 인식 업데이트 시작  
  
##### <a name="to-start-cluster-aware-updating-from-server-manager"></a>서버 관리자에서 클러스터 인식 업데이트를 시작 하려면  
  
1.  서버 관리자를 시작합니다.  
  
2.  다음 중 하나를 수행합니다.  
  
    -   **도구** 메뉴에서 **Cluster @ No__t-2aware 업데이트**를 클릭 합니다.  
  
    -   하나 이상의 클러스터 노드 또는 클러스터가 서버 관리자에 추가 되는 경우 **모든 서버** 페이지에서 @no__t 노드 이름을 마우스 오른쪽 단추로 클릭 하 고 no__t를 클릭 한 다음 클러스터의 이름 (@ no__t-3)을 클릭 하 고 **클러스터 업데이트**를 클릭 합니다.  
  
## <a name="see-also"></a>참조  
다음 링크는 클러스터 인식 업데이트를 사용 하는 방법에 대 한 자세한 정보를 제공 합니다.  
  
-   [클러스터 @ no__t-1 인식 업데이트에 대 한 요구 사항 및 모범 사례](cluster-aware-updating.md)  
  
-   [Cluster @ no__t-1 인식 업데이트: 질문과 대답](cluster-aware-updating-faq.md)  
  
-   [CAU에 대 한 고급 옵션 및 업데이트 실행 프로필](cluster-aware-updating-options.md)  
  
-   [CAU 플러그 인 @ no__t-1의 작동 방식](cluster-aware-updating-plug-ins.md)  
  
-   [Windows PowerShell의 Cluster @ no__t-1Aware 업데이트 Cmdlet](https://docs.microsoft.com/powershell/module/clusterawareupdating/?view=win10-ps&viewFallbackFrom=winserverr2-ps)  
  
-   [Cluster @ no__t-1Aware 업데이트 플러그 @ no__t-2in 참조](https://docs.microsoft.com/previous-versions/windows/desktop/mscs/cluster-aware-update-plug-in-interfaces-and-classes)  
  

