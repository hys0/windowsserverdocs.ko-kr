---
title: 클러스터 인식 업데이트 개요
description: CAU (클러스터 인식 업데이트)는 Windows Server를 실행 하는 클러스터에서 소프트웨어 업데이트 설치를 자동화 합니다.
ms.topic: article
ms.prod: windows-server
manager: lizross
author: JasonGerend
ms.author: jgerend
ms.technology: storage-failover-clustering
ms.date: 08/06/2018
ms.assetid: 3c2993b4-aa81-452b-a5c3-3724ad95d892
ms.openlocfilehash: bd3c15d08b0d4b6f174fd9c790f0dacb2457472e
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85473290"
---
# <a name="cluster-aware-updating-overview"></a>클러스터 인식 업데이트 개요

> 적용 대상: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 \- \( 가용성을 \) 유지 하면서 클러스터 된 서버의 소프트웨어 업데이트 프로세스를 자동화 하는 기능인 CAU 업데이트 CAU의 개요를 제공 합니다.

> [!NOTE]
> [스토리지 공간 다이렉트](../storage/storage-spaces/storage-spaces-direct-overview.md) 클러스터를 업데이트할 때 클러스터 인식 업데이트를 사용 하는 것이 좋습니다.

## <a name="feature-description"></a><a name="BKMK_OVER"></a>기능 설명
클러스터 인식 업데이트는 [장애 조치 (failover) 클러스터](failover-clustering-overview.md) 의 서버를 업데이트 하는 동안 가용성을 거의 또는 전혀 손실 하지 않고 업데이트할 수 있는 자동화 된 기능입니다. 업데이트를 실행 하는 동안 클러스터 인식 업데이트는 다음 작업을 투명 하 게 수행 합니다.

1. 클러스터의 각 노드를 노드 유지 관리 모드로 전환 합니다.
2. 클러스터 된 역할을 노드 밖으로 이동 합니다.
3. 업데이트 및 모든 종속 업데이트를 설치 합니다.
4. 필요한 경우 다시 시작을 수행 합니다.
5. 노드를 유지 관리 모드에서 제외 합니다.
6. 노드에서 클러스터 된 역할을 복원 합니다.
7. 를 이동 하 여 다음 노드를 업데이트 합니다.

클러스터에 있는 클러스터된 많은 역할의 경우 자동 업데이트 프로세스를 통해 계획된 장애 조치(failover)가 시작됩니다. 이로 인해 연결된 클라이언트에 대한 서비스가 일시적으로 중단될 수 있습니다. 그러나 실시간 마이그레이션 기능이 포함 된 Hyper-v 또는 SMB 투명 장애 조치 (Failover)를 사용 하는 파일 서버와 같이 지속적으로 사용 가능한 워크 로드의 경우 \- 클러스터 인식 업데이트는 서비스 가용성에 영향을 주지 않고 클러스터 업데이트를 조정할 수 있습니다.

## <a name="practical-applications"></a>유용한 팁

-   CAU는 클러스터 된 서비스의 서비스 중단을 줄이고 수동 업데이트 해결 방법의 필요성을 줄이고 관리자를 \- \- 위한 종단 간 클러스터 업데이트 프로세스의 안정성을 향상 시킵니다. CAU 기능을 지속적으로 사용 가능한 클러스터 워크 로드와 함께 사용 하는 경우 (예: \( SMB 투명 장애 조치 (Failover) 또는 hyper-v를 사용 하 여 지속적으로 사용 가능한 파일 서버 파일 서버 작업 \) \- ) 클라이언트에 대 한 서비스 가용성에 영향을 주지 않고 클러스터 업데이트를 수행 합니다.

-   CAU는 기업 전체에서 일관된 IT 프로세스를 도입합니다. 여러 다른 유형의 장애 조치 (failover) 클러스터에 대해 업데이트 실행 프로필을 만든 다음 파일 공유에서 중앙에서 관리 하 여, 다른 \- 비즈니스 또는 관리자가 클러스터를 관리 하더라도 IT 조직 전체의 CAU 배포에서 업데이트를 일관 되 게 적용할 수 있습니다 \- .

-   CAU는 정기적인 간격(매일, 매주, 매월)으로 업데이트 실행을 예약할 수 있어 다른 IT 관리 프로세스를 통한 클러스터 업데이트를 쉽게 조정할 수 있습니다.

-   CAU는 클러스터를 인식 하는 방식으로 클러스터 소프트웨어 인벤토리를 업데이트 하기 위한 확장 가능한 아키텍처를 제공 \- 합니다. 게시자가 Windows 업데이트 또는 Microsoft 업데이트에 게시 되지 않았거나 microsoft에서 제공 하지 않는 소프트웨어 업데이트 (예: 타사 장치 드라이버 업데이트)의 설치를 조정 하는 데 사용할 수 있습니다 \- .

-   CAU 자동 \- 업데이트 모드에서는 \( 일반적으로 하나의 섀시에 패키지 자체를 업데이트 하는 클러스터 된 물리적 컴퓨터 집합을 "box에서 클러스터" 어플라이언스를 사용할 수 있습니다 \) . 일반적으로 이러한 장비는 최소한의 로컬 IT 지원이 제공되는 지점에서 클러스터를 관리할 수 있도록 배포됩니다. 자동 \- 업데이트 모드는 이러한 배포 시나리오에서 우수한 가치를 제공 합니다.

## <a name="important-functionality"></a>중요 기능
다음은 중요 한 클러스터 인식 업데이트 기능에 대 한 설명입니다.

-   사용자 인터페이스 \( UI \) -클러스터 인식 업데이트 창-업데이트를 미리 보고 적용 하 고 모니터링 하 고 보고 하는 데 사용할 수 있는 cmdlet 집합

-   하나 이상의 \- \- \- \( \) 업데이트 코디네이터 컴퓨터에서 오케스트레이션 업데이트 실행 인 클러스터 업데이트 작업의 종단 간 자동화

-   \-기존 Windows 업데이트 Agent \( WUA와 통합 되 \) 고 \( \) Windows Server의 WSUS 인프라 Windows Server Update Services 중요 한 Microsoft 업데이트를 적용 하는 기본 플러그 인

-   \-Microsoft 핫픽스를 적용 하는 데 사용할 수 있고 타사 업데이트를 적용 하도록 사용자 지정할 수 있는 두 번째 플러그 인입니다. \-

-   노드당 업데이트를 다시 시도할 최대 횟수와 같은 업데이트 실행 옵션에 대한 설정을 사용하여 구성하는 업데이트 실행 프로필. 업데이트 실행 프로필을 사용하면 여러 업데이트 실행 간에 동일한 설정을 빠르게 다시 사용하고 다른 장애 조치(failover) 클러스터와 업데이트 설정을 쉽게 공유할 수 있습니다.

-   \- \- 사용자 지정 소프트웨어 설치 관리자, BIOS 업데이트 도구, 네트워크 어댑터 또는 호스트 버스 어댑터 \( HBA 업데이트 도구 등의 다른 노드 업데이트 도구를 클러스터 전체에서 조정 하기 위한 새 플러그 인 개발을 지 원하는 확장 가능한 아키텍처입니다 \) .

클러스터 인식 업데이트는 다음 두 가지 모드로 전체 클러스터 업데이트 작업을 조정할 수 있습니다.

-   **자동 \- 업데이트 모드** 이 모드에서는 CAU 클러스터 된 역할이 업데이트할 장애 조치 (failover) 클러스터에서 작업으로 구성 되 고 연결 된 업데이트 일정이 정의 됩니다. 클러스터는 기본 또는 사용자 지정 업데이트 실행 프로필을 사용하여 예약된 시간에 자동 업데이트됩니다. 업데이트 실행 중에는 CAU 업데이트 코디네이터 프로세스가 현재 CAU 클러스터된 역할을 소유하고 있는 노드에서 시작되고, 각 클러스터 노드에서 후속 업데이트가 수행됩니다. 현재 클러스터 노드를 업데이트하기 위해 CAU 클러스터된 역할이 다른 클러스터 노드로 장애 조치(failover)되고 해당 노드의 새 업데이트 코디네이터 프로세스가 업데이트 실행을 제어합니다. 자동 \- 업데이트 모드에서 CAU는 완전히 자동화 된 종단 \- 간 업데이트 프로세스를 사용 하 여 장애 조치 (failover) 클러스터를 업데이트할 수 있습니다 \- . 관리자는 \- 이 모드에서 요청 시 업데이트를 트리거하거나 \- 원하는 경우 원격 업데이트 방법을 사용할 수도 있습니다. 자동 \- 업데이트 모드에서 관리자는 클러스터에 연결 하 고 **get \- invoke-caurun** Windows PowerShell cmdlet을 실행 하 여 진행 중인 업데이트 실행에 대 한 요약 정보를 가져올 수 있습니다.

-   **원격 \- 업데이트 모드** 이 모드에서는 업데이트 코디네이터 라는 원격 컴퓨터가 CAU 도구를 사용 하 여 구성 됩니다. 업데이트 코디네이터는 업데이트 실행 중에 업데이트되는 클러스터의 구성원이 아닙니다. 관리자는 원격 컴퓨터에서 \- 기본 또는 사용자 지정 업데이트 실행 프로필을 사용 하 여 요청 시 업데이트 실행을 트리거합니다. 원격 \- 업데이트 모드는 \- 업데이트 실행 중에 실시간 진행률을 모니터링 하거나 Server Core 설치에서 실행 되는 클러스터에 유용 합니다.

## <a name="hardware-and-software-requirements"></a>하드웨어 및 소프트웨어 요구 사항

CAU는 Server Core 설치를 포함 하 여 모든 버전의 Windows Server에서 사용할 수 있습니다. 자세한 요구 사항 정보는 [클러스터 인식 업데이트 요구 사항 및 모범 사례](cluster-aware-updating-requirements.md)를 참조 하세요.

### <a name="installing-cluster-aware-updating"></a>클러스터 인식 업데이트 설치
CAU를 사용 하려면 Windows Server에 장애 조치 (Failover) 클러스터링 기능을 설치 하 고 장애 조치 (failover) 클러스터를 만듭니다. CAU 기능을 지원하는 구성 요소는 각 클러스터 노드에 자동으로 설치됩니다.

다음 도구를 사용하여 장애 조치(faillover) 클러스터링 기능을 설치할 수 있습니다.
- 서버 관리자의 역할 및 기능 추가 마법사
- [설치-add-windowsfeature](https://docs.microsoft.com/powershell/module/servermanager/Install-WindowsFeature?view=winserver2012r2-ps&viewFallbackFrom=win10-ps)   Windows PowerShell cmdlet
- DISM(배포 이미지 서비스 및 관리) 명령줄 도구

자세한 내용은 [장애 조치 (Failover) 클러스터링 기능 설치](create-failover-cluster.md#install-the-failover-clustering-feature)를 참조 하세요.

또한 원격 서버 관리 도구의 일부인 장애 조치 (failover) 클러스터링 도구를 설치 해야 하며, 서버 관리자에 장애 조치 (Failover) 클러스터링 기능을 설치할 때 기본적으로 설치 됩니다. 장애 조치 (Failover) 클러스터링 도구에는 클러스터 인식 업데이트 사용자 인터페이스 및 PowerShell cmdlet이 포함 됩니다.

다른 CAU 업데이트 모드를 지원하려면 다음과 같이 장애 조치(failover) 클러스터링 도구를 설치해야 합니다.

- 자동 업데이트 모드에서 CAU를 사용 하려면 \- 각 클러스터 노드에 장애 조치 (Failover) 클러스터링 도구를 설치 합니다.

- 원격 업데이트 모드를 사용 하도록 설정 하려면 장애 조치 (failover) \- 클러스터에 네트워크로 연결 된 컴퓨터에 장애 조치 (Failover) 클러스터링 도구를 설치 합니다.

> [!NOTE]
> -   Windows Server 2012의 장애 조치 (Failover) 클러스터링 도구를 사용 하 여 최신 버전의 Windows Server에서 클러스터 인식 업데이트를 관리할 수 없습니다.
> -   CAU를 원격 업데이트 모드 에서만 사용 하려면 \- 클러스터 노드에 장애 조치 (Failover) 클러스터링 도구를 설치 해야 합니다. 그러나 특정 CAU 기능을 사용할 수 없게 됩니다. 자세한 내용은 [클러스터 \- 인식 업데이트에 대 한 요구 사항 및 모범 사례](cluster-aware-updating-requirements.md)를 참조 하세요.
> -   자동 업데이트 모드 에서만 CAU를 사용 하는 경우가 아니면 \- cau 도구가 설치 되 고 업데이트를 조정 하는 컴퓨터는 장애 조치 (failover) 클러스터의 구성원이 될 수 없습니다.

### <a name="enabling-self-updating-mode"></a>자동 업데이트 모드 사용
자동 업데이트 모드를 사용 하도록 설정 하려면 클러스터 인식 업데이트 클러스터 된 역할을 장애 조치 (failover) 클러스터에 추가 해야 합니다. 이렇게 하려면 다음 방법 중 하나를 사용 합니다.
- 서버 관리자에서 **도구**  >  **클러스터 인식 업데이트**를 선택 하 고 클러스터 인식 업데이트 창에서 **클러스터 자동 업데이트 옵션 구성**을 선택 합니다.
- PowerShell 세션에서 [add-cauclusterrole](https://docs.microsoft.com/powershell/module/clusterawareupdating/Add-CauClusterRole?view=win10-ps) cmdlet을 실행 합니다.

CAU를 제거 하려면 서버 관리자, [uninstall-add-windowsfeature](https://docs.microsoft.com/powershell/module/servermanager/Uninstall-WindowsFeature?view=win10-ps) CMDLET 또는 DISM 명령줄 도구를 사용 하 여 장애 조치 (Failover) 클러스터링 기능 또는 장애 조치 (Failover) 클러스터링 도구를 제거 \- 합니다.

### <a name="additional-requirements-and-best-practices"></a>추가 요구 사항 및 모범 사례

CAU로 클러스터 노드를 성공적으로 업데이트하고 CAU를 사용하도록 장애 조치(failover) 클러스터 환경을 구성하기 위한 추가 지침을 보려면 CAU 모범 사례 분석기를 실행할 수 있습니다.

CAU 사용에 대 한 자세한 요구 사항 및 모범 사례와 CAU 모범 사례 분석기를 실행 하는 방법에 대 한 자세한 내용은 [클러스터 \- 인식 업데이트에 대 한 요구 사항 및 모범 사례](cluster-aware-updating-requirements.md)를 참조 하세요.

### <a name="starting-cluster-aware-updating"></a>클러스터 인식 업데이트 시작

##### <a name="to-start-cluster-aware-updating-from-server-manager"></a>서버 관리자에서 클러스터 인식 업데이트를 시작 하려면

1.  서버 관리자를 시작합니다.

2.  다음 중 하나를 수행합니다.

    -   **도구** 메뉴에서 **클러스터 \- 인식 업데이트**를 클릭 합니다.

    -   하나 이상의 클러스터 노드 또는 클러스터가 서버 관리자에 추가 된 경우 **모든 서버** 페이지에서 \- 노드의 이름 또는 클러스터의 이름을 마우스 오른쪽 단추로 클릭 하 \( \) 고 **클러스터 업데이트**를 클릭 합니다.

## <a name="additional-references"></a>추가 참조
다음 링크는 클러스터 인식 업데이트를 사용 하는 방법에 대 한 자세한 정보를 제공 합니다.

-   [클러스터 인식 업데이트에 대 한 요구 사항 및 모범 사례 \-](cluster-aware-updating.md)

-   [클러스터 \- 인식 업데이트: 질문과 대답](cluster-aware-updating-faq.md)

-   [CAU에 대한 고급 옵션 및 업데이트 실행 프로필](cluster-aware-updating-options.md)

-   [CAU 플러그 인의 \- 작동 방법](cluster-aware-updating-plug-ins.md)

-   [\-Windows PowerShell의 클러스터 인식 업데이트 cmdlet](https://docs.microsoft.com/powershell/module/clusterawareupdating/?view=win10-ps&viewFallbackFrom=winserverr2-ps)

-   [클러스터 \- 인식 업데이트 플러그 인 \- 참조](https://docs.microsoft.com/previous-versions/windows/desktop/mscs/cluster-aware-update-plug-in-interfaces-and-classes)


