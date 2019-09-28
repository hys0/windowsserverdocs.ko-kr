---
ms.assetid: 6416d125-bcaf-433d-971a-2f0283bca2c2
title: 클러스터 인식 업데이트-질문과 대답
ms.topic: article
ms.prod: windows-server
manager: dongill
ms.author: jgerend
author: JasonGerend
ms.date: 04/28/2017
description: Windows Server에서 클러스터 인식 업데이트에 대 한 자주 묻는 질문에 대 한 대답입니다.
ms.openlocfilehash: a08366c7e64d9612d63e348d4cecdb4b2389737a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71361352"
---
# <a name="cluster-aware-updating-frequently-asked-questions"></a>클러스터 인식 업데이트: 질문과 대답

> 적용 대상: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

[클러스터 인식 업데이트](cluster-aware-updating.md) \(cau @ no__t-2는 장애 조치 (failover) 클러스터의 모든 서버에서 소프트웨어 업데이트를 조정 하는 기능으로, 클러스터 노드의 계획 된 장애 조치 (failover)를 통해 서비스 가용성에 영향을 주지 않는 방식으로 작동 합니다. 지속적인 가용성 @no__t 기능이 있는 일부 응용 프로그램의 경우 (예: 실시간 마이그레이션을 사용 하는 Hyper-v no__t) 또는 SMB 3.x 파일 서버 (SMB 투명 장애 조치 (Failover) @ no__t-2 포함) CAU는 서비스에 영향을 주지 않고 자동화 된 클러스터 업데이트를 조정할 수 있습니다. 가용성.

## <a name="does-cau-support-updating-storage-spaces-direct-clusters"></a>CAU는 스토리지 공간 다이렉트 클러스터 업데이트를 지원 하나요?  
예. CAU는 배포 유형 (하이퍼 수렴 형 또는 수렴 됨)에 관계 없이 [스토리지 공간 다이렉트](../storage/storage-spaces/storage-spaces-direct-overview.md) 클러스터 업데이트를 지원 합니다. 특히 CAU 오케스트레이션은 각 클러스터 노드를 일시 중단 하면 기본 클러스터 된 저장소 공간이 정상 상태가 될 때까지 대기 합니다.

## <a name="does-cau-work-with-windowsserver-2008r2-or-windows7"></a>CAU는 Windows Server 2008 R2 또는 Windows 7에서 작동합니까?  
아니요. CAU는 Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows 10, Windows 8.1 또는 Windows 8을 실행 하는 컴퓨터 에서만 클러스터 업데이트 작업을 조정 합니다. 업데이트 되는 장애 조치 (failover) 클러스터는 Windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012를 실행 해야 합니다.
  
## <a name="is-cau-limited-to-specific-clustered-applications"></a>CAU는 특정 클러스터형 응용 프로그램으로 제한 됩니까?  
아니요. CAU는 클러스터된 응용 프로그램의 유형에 관계없이 사용할 수 있습니다. CAU는 클러스터링 Api 및 PowerShell cmdlet 위에 계층화 된 외부 클러스터 @ no__t-0updating 솔루션입니다. 따라서 CAU는 Windows Server 장애 조치 (failover) 클러스터에 구성 된 모든 클러스터 된 응용 프로그램에 대 한 업데이트를 조정할 수 있습니다.  
  
> [!NOTE]  
> 현재 다음과 같은 클러스터 된 워크 로드를 테스트 하 고 CAU에 대해 인증 합니다. SMB, 하이퍼 @ no__t-0V, DFS 복제, DFS 네임 스페이스, iSCSI 및 NFS  
  
## <a name="does-cau-support-updates-from-microsoft-update-and-windows-update"></a>CAU는 Microsoft 업데이트 및 Windows Update의 업데이트를 지원합니까?  
예. 기본적으로 CAU는 클러스터 노드의 Windows 업데이트 에이전트 \(WUA @ no__t-2 유틸리티 Api를 사용 하는 플러그 @ no__t-0in으로 구성 됩니다. Microsoft 업데이트 및 Windows 업데이트를 가리키도록 WUA infrastructure를 구성 하 고 업데이트의 원본으로 \(WSUS @ no__t-1을 Windows Server Update Services 수 있습니다.  
  
## <a name="does-cau-support-wsus-updates"></a>CAU는 WSUS 업데이트를 지원합니까?  
예. 기본적으로 CAU는 클러스터 노드의 Windows 업데이트 에이전트 \(WUA @ no__t-2 유틸리티 Api를 사용 하는 플러그 @ no__t-0in으로 구성 됩니다. Microsoft 업데이트 및 Windows 업데이트 또는 로컬 Windows Server Update Services \(WSUS @ no__t 서버를 업데이트 원본으로 가리키도록 WUA 인프라를 구성할 수 있습니다.  
  
## <a name="can-cau-apply-limited-distribution-release-updates"></a>CAU는 제한된 배포 릴리스 업데이트를 적용할 수 있습니까?  
예. 제한 된 배포 릴리스 \(LDR @ no__t-1 업데이트 (핫픽스 라고도 함)는 Microsoft 업데이트 또는 Windows 업데이트를 통해 게시 되지 않으므로 CAU가 기본적으로 사용 하는 Windows 업데이트 에이전트 \(WUA @ no__t-3 플러그 @ no__t-4에서 다운로드할 수 없습니다. .  
  
그러나 CAU에는 핫픽스 업데이트를 적용 하도록 선택할 수 있는 두 번째 플러그 인 @ no__t-0in 포함 되어 있습니다. @ No__t-1Microsoft 드라이버, 펌웨어 및 BIOS 업데이트를 적용 하도록이 핫픽스 플러그 인을 사용자 지정할 수도 있습니다.  
  
## <a name="can-i-use-cau-to-apply-cumulative-updates"></a>CAU를 사용하여 누적 업데이트를 적용할 수 있나요?  
예. 누적 업데이트가 일반 배포 릴리스 업데이트 또는 LDR 업데이트인 경우 CAU가 해당 업데이트를 적용할 수 있습니다.  
  
## <a name="can-i-schedule-updates"></a>업데이트를 예약할 수 있나요?  
예. CAU는 다음과 같은 업데이트 모드를 지원하며, 두 모드에서 모두 업데이트를 예약할 수 있습니다.  
  
**Self @ no__t-1 업데이트** 지정 된 프로필 및 정기적인 일정 (예: 월간 유지 관리 기간)에 따라 클러스터 자체를 업데이트할 수 있습니다. 언제 든 지 요청 시 자체 @ no__t-0Updating 실행을 시작할 수도 있습니다. Self @ no__t-0updating 모드를 사용 하도록 설정 하려면 클러스터에 CAU 클러스터 된 역할을 추가 해야 합니다. CAU self @ no__t-0updating 기능은 다른 클러스터 된 워크 로드와 마찬가지로 수행 되며, 업데이트 코디네이터 컴퓨터의 계획 되거나 계획 되지 않은 장애 조치 (failover)와 함께 원활 하 게 작동할 수 있습니다.  
  
**원격 @ no__t-1 업데이트 중** Windows 또는 Windows Server를 실행 하는 컴퓨터에서 언제 든 지 업데이트 실행을 시작할 수 있습니다. 클러스터 인식 업데이트 창이 나 **Invoke @ no__t-1CauRun** PowerShell cmdlet을 사용 하 여 업데이트 실행을 시작할 수 있습니다. Remote @ no__t-0updating는 CAU의 기본 업데이트 모드입니다. 클러스터 노드가 아닌 원격 컴퓨터에서는 작업 스케줄러를 사용하여 원하는 일정으로 [Invoke-CauRun](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/invoke-caurun) cmdlet을 실행할 수 있습니다.  
  
## <a name="can-i-schedule-updates-to-apply-during-a-backup"></a>백업 중에 적용 되도록 업데이트를 예약할 수 있나요?  
예. CAU는 이러한 측면에서 제약 조건을 적용 하지 않습니다. 그러나 서버 백업이 진행 되는 동안 연결 된 잠재적으로 다시 시작 @ no__t-1을 사용 하 여 @no__t 서버에서 소프트웨어 업데이트를 수행 하는 것은 좋은 방법이 아닙니다. CAU는 클러스터링 API만을 사용하여 리소스 장애 조치(failover) 및 장애 복구(failback)를 결정하므로 서버 백업 상태는 알지 못합니다.  
  
## <a name="can-cau-work-with-system-center-configuration-manager"></a>CAU를 System Center Configuration Manager와 함께 사용할 수 있나요?  
CAU는 클러스터 노드에서 소프트웨어 업데이트를 조정 하는 도구 이며 서버 소프트웨어 업데이트도 수행 Configuration Manager 합니다. 다른 Windows Server Update Services 서버를 사용 하는 것을 포함 하 여 데이터 센터 배포에서 동일한 서버에 대해 겹치는 검사를 하지 않도록 이러한 도구를 구성 하는 것이 중요 합니다. 이렇게 하면 Configuration Manager @ no__t-0driven 업데이트는 클러스터 인식 기능을 통합 하지 않으므로 CAU를 사용 하는 경우의 목표가 실수로 방지 되지 않습니다.  
  
## <a name="do-i-need-administrative-credentials-to-run-cau"></a>CAU를 실행하려면 관리 자격 증명이 필요합니까?  
예. CAU 도구를 실행하려면 CAU에 로컬 서버에 대한 관리 자격 증명이 필요합니다. 또는 CAU가 실행되는 클라이언트 컴퓨터 또는 로컬 서버에 대한 **인증 후 클라이언트 가장** 사용자 권한이 필요합니다. 그러나 클러스터 노드에서 소프트웨어 업데이트를 조정하려면 모든 노드에서 CAU에 클러스터 관리 자격 증명이 필요합니다. CAU UI는 자격 증명 없이 시작 될 수 있지만 업데이트를 미리 보거나 적용 하기 위해 클러스터 인스턴스에 연결할 때 클러스터 관리 자격 증명을 묻는 메시지를 표시 합니다.  
  
## <a name="can-i-script-cau"></a>CAU를 스크립팅할 수 있나요?  
예. CAU에는 다양 한 스크립팅 옵션을 제공 하는 PowerShell cmdlet이 제공 됩니다. 이러한 cmdlet은 CAU UI가 CAU 작업을 수행하기 위해 호출하는 cmdlet과 동일합니다.  

## <a name="what-happens-to-active-clustered-roles"></a>활성 클러스터 된 역할은 어떻게 되나요?

클러스터 된 역할 @no__t 이전에는 노드에 활성화 된 응용 프로그램 및 서비스 @ no__t-1이 호출 되 고, 소프트웨어 업데이트를 시작 하기 전에 다른 노드로 장애 조치 (failover) 됩니다. CAU는 모든 활성 클러스터된 역할의 노드를 일시 중지하고 드레이닝하는 유지 관리 모드를 사용하여 이러한 장애 조치(Failover)를 조정합니다. 소프트웨어 업데이트가 완료되면 CAU는 노드를 다시 시작하며 클러스터된 역할은 업데이트된 노드로 장애 복구(failback)됩니다. 따라서 노드를 기준으로 하는 클러스터 역할 배포가 클러스터의 CAU 업데이트 실행 전체에서 동일하게 유지됩니다.  
  
## <a name="how-does-cau-select-target-nodes-for-clustered-roles"></a>CAU는 클러스터 된 역할의 대상 노드를 어떻게 선택 하나요?

CAU는 클러스터링 API를 사용하여 장애 조치(Failover)를 조정합니다. 클러스터링 API 구현에서는 대상 노드 전체에서 작업 수준 @ no__t-1과 같은 \(such 내부 메트릭과 지능형 배치 추론에 의존 하 여 대상 노드를 선택 합니다.  
  
## <a name="does-cau-load-balance-the-clustered-roles"></a>CAU는 클러스터 된 역할을 부하 분산 합니까?

CAU는 클러스터 된 노드의 부하를 분산 하지 않지만 클러스터 된 역할의 배포를 유지 하려고 시도 합니다. CAU는 클러스터 노드 업데이트를 완료한 후 이전에 호스트된 클러스터된 역할을 해당 노드로 장애 복구(Failback)하려고 합니다. CAU는 클러스터링 API를 사용하여 일시 중지 프로세스의 시작 부분으로 리소스를 장애 복구(failback)합니다. 따라서 계획되지 않은 장애 조치(Failover) 및 기본 소유자 설정이 없으면 클러스터된 역할의 분산은 변경되지 않은 상태로 유지됩니다.  
  
## <a name="how-does-cau-select-the-order-of-nodes-to-update"></a>CAU는 업데이트할 노드의 순서를 어떻게 선택합니까?  
기본적으로 CAU는 작업 수준에 따라 업데이트할 노드의 순서를 선택합니다. 가장 적은 수의 클러스터된 역할을 호스팅하는 노드가 첫 번째로 업데이트됩니다. 그러나 관리자는 CAU UI에서 업데이트 실행에 대 한 매개 변수를 지정 하거나 PowerShell cmdlet을 사용 하 여 노드를 업데이트할 특정 순서를 지정할 수 있습니다.  
  
## <a name="what-happens-if-a-cluster-node-is-offline"></a>클러스터 노드가 오프 라인 상태 이면 어떻게 되나요?

업데이트 실행을 시작하는 관리자는 오프라인 상태가 될 수 있는 노드 수에 대한 적절한 임계값을 지정할 수 있습니다. 따라서 모든 클러스터 노드가 온라인 상태가 아니어도 클러스터에서 업데이트 실행을 진행할 수 있습니다.  
  
## <a name="can-i-use-cau-to-update-only-a-single-node"></a>CAU를 사용 하 여 단일 노드만 업데이트할 수 있나요?  
아니요. CAU는 cluster @ no__t-0scoped 업데이트 도구 이므로 업데이트할 클러스터를 선택할 수 있습니다. 단일 노드를 업데이트하려면 CAU와 독립적인 기존 서버 업데이트 도구를 사용하면 됩니다.  
  
## <a name="can-cau-report-updates-that-are-initiated-from-outside-cau"></a>CAU는 CAU 외부에서 시작 된 업데이트를 보고할 수 있나요?  
아니요. CAU는 CAU 내부에서 시작된 업데이트 실행만 보고할 수 있습니다. 그러나 후속 CAU 업데이트 실행을 시작 하면 각 클러스터 노드에 적용할 수 있는 추가 업데이트를 결정 하는 데 @ no__t-0이 아닌 CAU 메서드를 통해 설치 된 업데이트를 적절 하 게 고려 합니다.  
  
## <a name="can-cau-support-my-unique-it-process-needs"></a>CAU는 고유한 IT 프로세스 요구 사항을 지원할 수 있나요?  
예. CAU는 기업 고객의 고유한 IT 프로세스 요구 사항에 맞는 다음과 같은 유동적 차원 옵션을 제공합니다.  
  
**스크립트** 업데이트 실행에서는 사전 @ no__t-1 업데이트 PowerShell 스크립트 및 post @ no__t-2update PowerShell 스크립트를 지정할 수 있습니다. 이전 @ no__t-0update 스크립트는 노드를 일시 중지 하기 전에 각 클러스터 노드에서 실행 됩니다. Post @ no__t-0update 스크립트는 노드 업데이트를 설치한 후에 각 클러스터 노드에서 실행 됩니다.  
  
> [!NOTE]  
> 이전 @ no__t-0update 및 post @ no__t 업데이트 스크립트를 실행할 각 클러스터 노드에 .NET Framework 4.6 또는 4.5 및 PowerShell이 설치 되어 있어야 합니다. 또한 클러스터 노드에서 PowerShell 원격을 사용 하도록 설정 해야 합니다. 자세한 시스템 요구 사항은 [클러스터 인식 업데이트에 대 한 요구 사항 및 모범 사례](cluster-aware-updating-requirements.md)를 참조 하세요.  
  
**고급 업데이트 실행 옵션** 관리자는 각 노드에서 업데이트 프로세스가 다시 시도 되는 최대 횟수와 같은 다양 한 고급 업데이트 실행 옵션을 추가로 지정할 수 있습니다. CAU UI 또는 CAU PowerShell cmdlet 중 하나를 사용 하 여 이러한 옵션을 지정할 수 있습니다. 이러한 사용자 지정 설정을 업데이트 실행 프로필에 저장하고 이후 업데이트 실행에 다시 사용할 수 있습니다.  
  
**공용 플러그 @ no__t-1in 아키텍처** CAU에는 플러그 인 @ no__t-2를 등록, 등록 취소 및 선택할 수 있는 기능이 포함 되어 있습니다. CAU는 두 개의 기본 플러그 인 @ no__t-0ins과 함께 제공 됩니다. 하나는 각 클러스터 노드의 Windows 업데이트 Agent \(WUA @ no__t-2 Api를 조정 하는 것입니다. 두 번째는 클러스터 노드에서 액세스할 수 있는 파일 공유에 수동으로 복사 된 핫픽스를 적용 합니다. 엔터프라이즈에 이러한 두 개의 플러그 @ no__t-0ins을 사용 하 여 충족할 수 없는 고유한 요구 사항이 있는 경우 엔터프라이즈는 공용 API 사양에 따라 새로운 CAU 플러그 인 @ no__t-1in을 빌드할 수 있습니다. 자세한 내용은 [Cluster @ no__t-1Aware 업데이트 플러그 @ no__t-2in 참조](https://msdn.microsoft.com/library/hh418084(VS.85).aspx)를 참조 하세요.  
  
다른 업데이트 시나리오를 지원 하기 위해 CAU 플러그 인 @ no__t-0ins를 구성 하 고 사용자 지정 하는 방법에 대 한 자세한 내용은 [플러그 @ no__t 기능 작동 방식](assetId:///847b571b-12b3-473c-953f-75a5a1f51333)을 참조 하세요.  
  
## <a name="how-can-i-export-the-cau-preview-and-update-results"></a>CAU 미리 보기 및 업데이트 결과를 내보내려면 어떻게 해야 합니까?  
CAU는 명령 @ no__t-0line 인터페이스 및 UI를 통해 내보내기 옵션을 제공 합니다.  
  
**Command @ no__t-1line 인터페이스 옵션:**  
  
-   PowerShell cmdlet을 사용 하 여 결과 미리 보기 **@ no__t-1CauScan | Convertto-html @ no__t-2Xml**. 출력: XML  
  
-   PowerShell cmdlet을 사용 하 여 결과 보고 **@ no__t-1CauRun | Convertto-html @ no__t-2Xml**. 출력: XML  
  
-   PowerShell cmdlet **Get @ no__t-1CauReport |를 사용 하 여 결과를 보고 합니다. Export @ no__t-2CauReport**. 출력: HTML, CSV  
  
**UI 옵션:**  
  
-   **업데이트 미리 보기** 화면에서 보고서 결과를 복사합니다. 출력: CSV  
  
-   **보고서 생성** 화면에서 보고서 결과를 복사합니다. 출력: CSV  
  
-   **보고서 생성** 화면에서 보고서 결과를 내보냅니다. 출력: HTML  
  
## <a name="how-do-i-install-cau"></a>CAU는 어떻게 설치합니까?  
CAU 설치는 장애 조치(Failover) 클러스터링 기능과 원활하게 통합됩니다. CAU는 다음과 같은 방법으로 설치됩니다.  
  
-   클러스터 노드에 장애 조치 (Failover) 클러스터링이 설치 되어 있으면 CAU WMI(Windows Management Instrumentation) \(WMI @ no__t-1 공급자가 자동으로 설치 됩니다.  
  
-   서버 또는 클라이언트 컴퓨터에 장애 조치 (Failover) 클러스터링 도구 기능을 설치 하면 클러스터 인식 업데이트 UI 및 PowerShell cmdlet이 자동으로 설치 됩니다.
  
## <a name="does-cau-need-components-running-on-the-cluster-nodes-that-are-being-updated"></a>CAU는 업데이트 중인 클러스터 노드에서 실행 되는 구성 요소가 필요 한가요?  
CAU는 클러스터 노드에서 실행 되는 서비스가 필요 하지 않습니다. 그러나 CAU에는 클러스터 노드에 설치 된 WMI 공급자 @ no__t-1의 소프트웨어 구성 @no__t 요소가 필요 합니다. 이 구성 요소는 장애 조치(failover) 클러스터링 기능과 함께 설치됩니다.  
  
Self @ no__t-0updating 모드를 사용 하도록 설정 하려면 클러스터에 CAU 클러스터 된 역할도 추가 해야 합니다.  
  
## <a name="what-is-the-difference-between-using-cau-and-vmm"></a>CAU와 VMM을 사용 하는 경우의 차이점은 무엇 인가요?  
  
-   System Center Virtual Machine Manager \(VMM @ no__t-1은 Hyper-v 클러스터를 업데이트 하는 데 초점을 맞춘 반면, CAU는 Hyper-v 클러스터를 포함 하 여 지원 되는 모든 유형의 장애 조치 (failover) 클러스터를 업데이트할 수 있습니다.  
  
-   VMM을 사용 하려면 추가 라이선스가 필요 하지만 CAU는 모든 Windows Server에 대해 사용이 허가 됩니다. CAU 기능, 도구 및 UI는 장애 조치(failover) 클러스터링 구성 요소와 함께 설치됩니다.  
  
-   이미 System Center 라이선스를 소유 하 고 있는 경우 VMM을 사용 하 여 통합 된 관리 및 소프트웨어 업데이트 환경을 제공 하므로 계속 VMM을 사용 하 여 Hyper-v 클러스터를 업데이트할 수 있습니다.  
  
-   CAU는 Windows Server 2016, Windows Server 2012 R2 및 Windows Server 2012를 실행 하는 클러스터 에서만 지원 됩니다. VMM은 Windows Server 2008 R2 및 Windows Server 2008를 실행 하는 컴퓨터에서 Hyper-v 클러스터도 지원 합니다.  
  
## <a name="can-i-use-remote-updating-on-a-cluster-that-is-configured-for-self-updating"></a>Self @ no__t-1updating를 위해 구성 된 클러스터에서 원격 @ no__t-0updating를 사용할 수 있나요?  
예. 사용자가 업데이트를 설치 하도록 구성 된 Windows 업데이트 경우에도 컴퓨터에서 언제 든 지 Windows 업데이트 검색을 강제할 수 있는 것과 마찬가지로, 자체 @ no__t-0updating 구성의 장애 조치 (failover) 클러스터에서 @ no__t 요청 시 원격 @ no__t 업데이트를 통해 업데이트할 수 있습니다. 자동으로. 그러나 이 경우 업데이트 실행이 이미 진행되지 않았는지 확인해야 합니다.  
  
## <a name="can-i-reuse-my-cluster-update-settings-across-clusters"></a>여러 클러스터 간에 클러스터 업데이트 설정을 다시 사용할 수 있습니까?  
예. CAU에서는 클러스터 업데이트 시 업데이트 실행 동작이 서로 다른 여러 업데이트 실행 옵션을 사용할 수 있습니다. 이러한 옵션을 업데이트 실행 프로필로 저장하여 어느 클러스터에서나 다시 사용할 수 있습니다. 설정을 저장하여 업데이트 요구 사항이 비슷한 장애 조치(failover) 클러스터에서 다시 사용하는 것이 좋습니다. 예를 들어 business @ no__t-1 중요 서비스를 지 원하는 모든 Microsoft SQL Server 클러스터에 대해 "Business @ no__t-0Critical SQL Server 클러스터 업데이트 실행 프로필"을 만들 수 있습니다.  
  
## <a name="where-is-the-cau-plug-in-specification"></a>사양의 CAU 플러그 @ no__t-0in 어디에 있나요?  
  
-   [Cluster @ no__t-1Aware 업데이트 플러그 @ no__t-2in 참조](https://msdn.microsoft.com/library/hh418084(VS.85).aspx)  
  
-   [클러스터 인식 업데이트 플러그 @ no__t-1in 샘플](https://code.msdn.microsoft.com/windowsdesktop/Cluster-Aware-Updating-6a8854c9)  
  
## <a name="see-also"></a>참조  
  
-   [Cluster @ no__t-1 인식 업데이트 개요](cluster-aware-updating.md)  
  
