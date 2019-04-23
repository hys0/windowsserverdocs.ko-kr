---
ms.assetid: 6416d125-bcaf-433d-971a-2f0283bca2c2
title: 클러스터 인식 업데이트-질문과 대답
ms.topic: article
ms.prod: windows-server-threshold
manager: dongill
ms.author: jgerend
author: JasonGerend
ms.date: 04/28/2017
description: Windows Server의 클러스터 인식 업데이트에 대 한 자주 묻는 질문에 답변 합니다.
ms.openlocfilehash: f9009811093823554f16295cc1205f1b99ead93f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882524"
---
# <a name="cluster-aware-updating-frequently-asked-questions"></a>클러스터 인식 업데이트: 질문과 대답

> 적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

[Cluster-aware Updating](cluster-aware-updating.md) \(CAU\) 계획된 된 장애 조치 클러스터 노드의 모든 보다 서비스 가용성에 영향을 주지는 방식으로 장애 조치 클러스터의 모든 서버에 소프트웨어를 조정 하는 기능 업데이트 됩니다. 일부 응용 프로그램의 지속적인 가용성 기능을 사용 하 여 \(하이퍼 등\-SMB 투명 장애 조치를 사용 하 여 실시간 마이그레이션 또는 SMB 3.x 파일 서버를 사용 하 여 V\), CAU에서 영향을 미치지 자동화 된 클러스터 업데이트를 조정할 수 있습니다 서비스 가용성입니다.

## <a name="does-cau-support-updating-storage-spaces-direct-clusters"></a>CAU 업데이트 저장소 공간 다이렉트 클러스터를 지원 하나요?  
예 CAU는 업데이트를 지원 [저장소 공간 다이렉트](../storage/storage-spaces/storage-spaces-direct-overview.md) 배포 유형에 관계 없이 클러스터: 하이퍼 수렴 형 또는 수렴 형입니다. 특히, CAU 오케스트레이션 상태가 정상이 되려면 기본 클러스터 된 저장소 공간에 대 한 대기 하는 각 클러스터 노드를 일시 중단 되도록 합니다.

## <a name="does-cau-work-with-windowsserver-2008r2-or-windows7"></a>CAU는 Windows Server 2008 R2 또는 Windows 7에서 작동합니까?  
아니요. CAU는 클러스터 업데이트 Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows 10, Windows 8.1 또는 Windows 8을 실행 하는 컴퓨터 에서만에서 작업을 조정 합니다. 장애 조치 클러스터 업데이트 중 Windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012를 실행 해야 합니다.
  
## <a name="is-cau-limited-to-specific-clustered-applications"></a>CAU는 클러스터 된 특정 응용 프로그램에 제한 됩니다?  
아니요. CAU는 클러스터된 응용 프로그램의 유형에 관계없이 사용할 수 있습니다. CAU는 클러스터를 외부\-클러스터링 Api 및 PowerShell cmdlet을 기반으로 계층화 되는 솔루션을 업데이트 합니다. 따라서 CAU는 Windows Server 장애 조치 클러스터에 구성 된 클러스터 된 응용 프로그램에 대 한 업데이트를 조정할 수 있습니다.  
  
> [!NOTE]  
> 현재 다음과 같은 클러스터 된 작업은 테스트 및 CAU에 대 한 인증: SMB, 하이퍼\-V, DFS 복제, DFS 네임 스페이스, iSCSI 및 NFS 합니다.  
  
## <a name="does-cau-support-updates-from-microsoft-update-and-windows-update"></a>CAU는 Microsoft 업데이트 및 Windows Update의 업데이트를 지원합니까?  
예 기본적으로 CAU는 플러그 인을 사용 하 여 구성 됩니다\-는 Windows Update 에이전트를 사용 하 여 \(WUA\) 클러스터 노드에서 유틸리티 Api. WUA 인프라는 Windows Server Update Services 또는 Microsoft Update 및 Windows Update를 가리키도록 구성할 수 있습니다 \(WSUS\) 업데이트 원본으로 합니다.  
  
## <a name="does-cau-support-wsus-updates"></a>CAU는 WSUS 업데이트를 지원합니까?  
예 기본적으로 CAU는 플러그 인을 사용 하 여 구성 됩니다\-는 Windows Update 에이전트를 사용 하 여 \(WUA\) 클러스터 노드에서 유틸리티 Api. WUA 인프라는 로컬 Windows Server Update Services 또는 Microsoft Update 및 Windows Update를 가리키도록 구성할 수 있습니다 \(WSUS\) 업데이트 원본으로는 서버입니다.  
  
## <a name="can-cau-apply-limited-distribution-release-updates"></a>CAU는 제한된 배포 릴리스 업데이트를 적용할 수 있습니까?  
예 릴리스 배포를 제한 \(LDR\) 핫픽스 라고도 내 업데이트를 Microsoft 업데이트 또는 Windows 업데이트를 통해 게시 되지 않으므로 Windows 업데이트 에이전트에서 다운로드할 수 없습니다 \(WUA\) 플러그인\-CAU는 기본적으로 사용 합니다.  
  
CAU는 두 번째 플러그 인을 포함 하는 반면\-는 핫픽스 업데이트를 적용 하도록 선택할 수 있습니다. 이 핫픽스 플러그 인\-에 사용자 지정할 수 있습니다 아닌 적용할\-Microsoft 드라이버, 펌웨어 및 BIOS 업데이트 합니다.  
  
## <a name="can-i-use-cau-to-apply-cumulative-updates"></a>CAU를 사용하여 누적 업데이트를 적용할 수 있나요?  
예 누적 업데이트가 일반 배포 릴리스 업데이트 또는 LDR 업데이트인 경우 CAU가 해당 업데이트를 적용할 수 있습니다.  
  
## <a name="can-i-schedule-updates"></a>업데이트를 예약할 수 있습니까?  
예 CAU는 다음과 같은 업데이트 모드를 지원하며, 두 모드에서 모두 업데이트를 예약할 수 있습니다.  
  
**Self\-업데이트** 업데이트 되도록 정의 된 프로필과 정기적인 일정에 따라 같은 매월 유지 관리 기간 동안 클러스터를 사용 하도록 설정 합니다. 자체를 시작할 수도 있습니다\-언제 든 지 요청 시 실행을 업데이트 합니다. 자체를 사용 하도록 설정 하려면\-업데이트 모드를 추가 해야 CAU 클러스터 된 역할 클러스터에 있습니다. CAU 자체\-다른 클러스터 된 작업과 같은 수행 기능을 업데이트 하 고 업데이트 코디네이터 컴퓨터의 계획 되거나 계획 되지 않은 장애 조치를 사용 하 여 원활 하 게 작업할 수 있습니다.  
  
**원격\-업데이트** Windows 또는 Windows Server를 실행 하는 컴퓨터에서 언제 든 지 업데이트 실행을 시작할 수 있습니다. 업데이트를 사용 하 여 또는 Cluster-aware Updating 창을 통해 실행을 시작할 수 있습니다 합니다 **Invoke\-CauRun** PowerShell cmdlet. 원격\-기본값인 CAU에 대 한 업데이트 모드를 업데이트 합니다. 클러스터 노드가 아닌 원격 컴퓨터에서는 작업 스케줄러를 사용하여 원하는 일정으로 [Invoke-CauRun](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/invoke-caurun) cmdlet을 실행할 수 있습니다.  
  
## <a name="can-i-schedule-updates-to-apply-during-a-backup"></a>백업 중에 적용할 업데이트를 예약할 수 있습니까?  
예 CAU에는 이런 점에서 제약 조건을 두지 않습니다. 그러나 서버에서 소프트웨어 업데이트를 수행 \(다시 시작 되는 연결 된 가능성이 있는\) 서버 백업 되는 동안 진행률 IT 모범 사례는 아닙니다. CAU는 클러스터링 API만을 사용하여 리소스 장애 조치(failover) 및 장애 복구(failback)를 결정하므로 서버 백업 상태는 알지 못합니다.  
  
## <a name="can-cau-work-with-system-center-configuration-manager"></a>CAU를 System Center Configuration Manager를 사용 하 여 작업할 수 있습니까?  
CAU는 클러스터 노드에서 소프트웨어 업데이트를 조정 하는 도구 이며 Configuration Manager 역시 서버 소프트웨어 업데이트를 수행 합니다. 겹치는 서로 다른 Windows Server Update Services 서버를 사용 하는 등 모든 데이터 센터 배포에서 동일한 서버의 범위 있지 않아도 되도록 이러한 도구를 구성 하는 것이 반드시 합니다. 이렇게 하면 CAU를 사용 하는 목적은 실수로 수 인지 하기 때문에 Configuration Manager\-기반 업데이트 클러스터 인식 기능을 통합 하지 않습니다.  
  
## <a name="do-i-need-administrative-credentials-to-run-cau"></a>CAU를 실행하려면 관리 자격 증명이 필요합니까?  
예 CAU 도구를 실행하려면 CAU에 로컬 서버에 대한 관리 자격 증명이 필요합니다. 또는 CAU가 실행되는 클라이언트 컴퓨터 또는 로컬 서버에 대한 **인증 후 클라이언트 가장** 사용자 권한이 필요합니다. 그러나 클러스터 노드에서 소프트웨어 업데이트를 조정하려면 모든 노드에서 CAU에 클러스터 관리 자격 증명이 필요합니다. 으로 자격 증명이 없어도 CAU UI를 시작할 수 있지만 클러스터 관리 자격 증명을 물을 미리 보거나 업데이트를 적용 하려면 클러스터 인스턴스에 연결할 때.  
  
## <a name="can-i-script-cau"></a>CAU를 스크립팅할 수 있습니까?  
예 CAU는 다양 한 스크립팅 옵션을 제공 하는 PowerShell cmdlet을 사용 하 여 제공 됩니다. 이러한 cmdlet은 CAU UI가 CAU 작업을 수행하기 위해 호출하는 cmdlet과 동일합니다.  

## <a name="what-happens-to-active-clustered-roles"></a>활성 클러스터 된 역할을 어떻게 되나요?

클러스터 된 역할이 \(이전의 응용 프로그램 및 서비스\) 노드에서 활성화 되는, 장애 조치 다른 노드 전에 소프트웨어 업데이트를 시작할 수 있습니다. CAU는 모든 활성 클러스터된 역할의 노드를 일시 중지하고 드레이닝하는 유지 관리 모드를 사용하여 이러한 장애 조치(Failover)를 조정합니다. 소프트웨어 업데이트가 완료되면 CAU는 노드를 다시 시작하며 클러스터된 역할은 업데이트된 노드로 장애 복구(failback)됩니다. 따라서 노드를 기준으로 하는 클러스터 역할 배포가 클러스터의 CAU 업데이트 실행 전체에서 동일하게 유지됩니다.  
  
## <a name="how-does-cau-select-target-nodes-for-clustered-roles"></a>CAU는 클러스터 된 역할에 대 한 대상 노드를 선택 하는 방법

CAU는 클러스터링 API를 사용하여 장애 조치(Failover)를 조정합니다. 내부 메트릭 및 지능적 배치 추론 하 여 대상 노드를 선택 하는 클러스터링 API 구현 \(예: 작업 수준\) 대상 노드에서 합니다.  
  
## <a name="does-cau-load-balance-the-clustered-roles"></a>클러스터 된 역할을 CAU 부하 분산은?

CAU 부하를 분산 하지만 클러스터 노드를 클러스터 된 역할 분산 유지 하려고 하지 않습니다. CAU는 클러스터 노드 업데이트를 완료한 후 이전에 호스트된 클러스터된 역할을 해당 노드로 장애 복구(Failback)하려고 합니다. CAU는 클러스터링 API를 사용하여 일시 중지 프로세스의 시작 부분으로 리소스를 장애 복구(failback)합니다. 따라서 계획되지 않은 장애 조치(Failover) 및 기본 소유자 설정이 없으면 클러스터된 역할의 분산은 변경되지 않은 상태로 유지됩니다.  
  
## <a name="how-does-cau-select-the-order-of-nodes-to-update"></a>CAU는 업데이트할 노드의 순서를 어떻게 선택합니까?  
기본적으로 CAU는 작업 수준에 따라 업데이트할 노드의 순서를 선택합니다. 가장 적은 수의 클러스터된 역할을 호스팅하는 노드가 첫 번째로 업데이트됩니다. 그러나 관리자는 CAU UI에서 업데이트 실행에 대 한 매개 변수를 지정 하거나 PowerShell cmdlet을 사용 하 여 노드를 업데이트할 특정 순서를 지정할 수 있습니다.  
  
## <a name="what-happens-if-a-cluster-node-is-offline"></a>클러스터 노드를 오프 라인 상태인 경우 어떻게 되나요?

업데이트 실행을 시작하는 관리자는 오프라인 상태가 될 수 있는 노드 수에 대한 적절한 임계값을 지정할 수 있습니다. 따라서 모든 클러스터 노드가 온라인 상태가 아니어도 클러스터에서 업데이트 실행을 진행할 수 있습니다.  
  
## <a name="can-i-use-cau-to-update-only-a-single-node"></a>CAU 업데이트 노드를 하나만 사용할 수 있나요?  
아니요. CAU는 클러스터\-범위가 지정 된 클러스터 업데이트를 선택할 수만 있습니다 있도록 도구를 업데이트 합니다. 단일 노드를 업데이트하려면 CAU와 독립적인 기존 서버 업데이트 도구를 사용하면 됩니다.  
  
## <a name="can-cau-report-updates-that-are-initiated-from-outside-cau"></a>CAU는 CAU 외부에서 시작 되는 업데이트를 보고할 수 있습니다?  
아니요. CAU는 CAU 내부에서 시작된 업데이트 실행만 보고할 수 있습니다. 그러나 후속 CAU 업데이트 실행 시작 될 때, 비를 통해 설치 된 업데이트\-CAU 메서드는 적절 하 게 각 클러스터 노드에 적용 될 수 있는 추가 업데이트가 확인 하는 것으로 간주 됩니다.  
  
## <a name="can-cau-support-my-unique-it-process-needs"></a>내 고유한 IT 프로세스 요구 하는 CAU 지원 수 있습니까?  
예 CAU는 기업 고객의 고유한 IT 프로세스 요구 사항에 맞는 다음과 같은 유동적 차원 옵션을 제공합니다.  
  
**스크립트** 업데이트 실행 사전 지정할 수 있습니다\-PowerShell 스크립트 및 게시물 업데이트\-PowerShell 스크립트를 업데이트 합니다. 사전\-업데이트 스크립트는 노드는 일시 중지 하기 전에 각 클러스터 노드에서 실행 합니다. 게시물\-노드 업데이트를 설치한 후 각 클러스터 노드에서 업데이트 스크립트를 실행 합니다.  
  
> [!NOTE]  
> 사전 실행 하려는 각 클러스터 노드에.NET framework 4.6 및 4.5 PowerShell을 설치 합니다\-업데이트 및 게시\-스크립트를 업데이트 합니다. 클러스터 노드에서 PowerShell remoting도 활성화 해야 합니다. 자세한 시스템 요구 사항을 참조 하세요 [요구 사항 및 클러스터 인식 업데이트에 대 한 모범 사례](cluster-aware-updating-requirements.md)합니다.  
  
**고급 업데이트 실행 옵션** 관리자는 각 노드에서 업데이트 프로세스가 다시 시도 하는 최대 횟수와 같은 고급 업데이트 실행 옵션의 큰 집합을 추가로 지정할 수 있습니다. CAU UI 또는 CAU PowerShell cmdlet을 사용 하 여 이러한 옵션을 지정할 수 있습니다. 이러한 사용자 지정 설정을 업데이트 실행 프로필에 저장하고 이후 업데이트 실행에 다시 사용할 수 있습니다.  
  
**공용 플러그\-아키텍처에서** 플러그 인 선택 및 CAU에 등록, 등록 취소, 기능이\-기능입니다. CAU는 두 개의 기본 플러그 인을 사용 하 여\-기능: Windows Update 에이전트 조정 하나 \(WUA\) Api에서 각 클러스터 노드, 두 번째 클러스터 노드에 액세스할 수 있는 파일 공유를 수동으로 복사 된 핫픽스를 적용 합니다. 기업의 고유한 요구 사항을 이러한 충족할 수 없는 경우 두 개의 플러그\-기능, 엔터프라이즈는 새로운 CAU 플러그 인을 빌드할 수\-공용 API 사양에 따라 합니다. 자세한 내용은 [클러스터\-인식 업데이트 플러그\-참조에서](https://msdn.microsoft.com/library/hh418084(VS.85).aspx)합니다.  
  
구성 및 CAU를 사용자 지정 하는 방법에 대 한 정보에 대 한 플러그\-다양 한 지원 기능 업데이트 시나리오를 참조 하세요 [연결 하는 방법\-기능 작동](assetId:///847b571b-12b3-473c-953f-75a5a1f51333)합니다.  
  
## <a name="how-can-i-export-the-cau-preview-and-update-results"></a>CAU 미리 보기 및 업데이트 결과를 내보내려면 어떻게 해야 합니까?  
CAU 제품 내보내기 옵션 명령을 통해\-명령줄 인터페이스 및 UI를 통해.  
  
**명령\-명령줄 인터페이스 옵션:**  
  
-   PowerShell cmdlet을 사용 하 여 결과 미리 **Invoke\-CauScan | ConvertTo\-Xml**합니다. 출력: XML  
  
-   PowerShell cmdlet을 사용 하 여 결과 보고 **Invoke\-CauRun | ConvertTo\-Xml**합니다. 출력: XML  
  
-   PowerShell cmdlet을 사용 하 여 결과 보고 **가져올\-CauReport | 내보낼\-CauReport**합니다. 출력: HTML, CSV  
  
**UI 옵션:**  
  
-   **업데이트 미리 보기** 화면에서 보고서 결과를 복사합니다. 출력: CSV  
  
-   **보고서 생성** 화면에서 보고서 결과를 복사합니다. 출력: CSV  
  
-   **보고서 생성** 화면에서 보고서 결과를 내보냅니다. 출력: HTML  
  
## <a name="how-do-i-install-cau"></a>CAU는 어떻게 설치합니까?  
CAU 설치는 장애 조치(Failover) 클러스터링 기능과 원활하게 통합됩니다. CAU는 다음과 같은 방법으로 설치됩니다.  
  
-   CAU Windows Management Instrumentation 클러스터 노드에서 장애 조치 클러스터링은 설치 하는 경우 \(WMI\) 공급자는 자동으로 설치 합니다.  
  
-   서버 또는 클라이언트 컴퓨터에서 장애 조치 클러스터링 도구 기능이 설치 된 클러스터 인식 업데이트 UI 및 PowerShell cmdlet은 자동으로 설치 됩니다.
  
## <a name="does-cau-need-components-running-on-the-cluster-nodes-that-are-being-updated"></a>CAU 업데이트 되는 클러스터 노드에서 실행 중인 구성 요소에 필요 합니까?  
CAU는 클러스터 노드에서 실행 되는 서비스를 필요 하지 않습니다. CAU 소프트웨어 구성 요소를 해야 하는 반면 \(WMI 공급자\) 클러스터 노드에 설치 합니다. 이 구성 요소는 장애 조치(failover) 클러스터링 기능과 함께 설치됩니다.  
  
자체를 사용 하도록 설정 하려면\-업데이트 모드에서 CAU 클러스터 된 역할도 추가 해야 클러스터에 있습니다.  
  
## <a name="what-is-the-difference-between-using-cau-and-vmm"></a>CAU와 VMM을 사용 하 여 간의 차이 무엇입니까?  
  
-   System Center Virtual Machine Manager \(VMM\) 업데이트만 하이퍼에 포커스가\-V 클러스터에 CAU는 모든 유형의 지원 되는 장애 조치 클러스터를 하이퍼를 포함 하 여 업데이트할 수 있습니다 하는 반면\-V 클러스터.  
  
-   VMM에 CAU는 모든 Windows Server에 대 한 사용이 허가 하는 반면 추가 라이선스가 필요 합니다. CAU 기능, 도구 및 UI는 장애 조치(failover) 클러스터링 구성 요소와 함께 설치됩니다.  
  
-   이미 System Center 라이선스를 소유 하는 경우 VMM을 사용 하 여 하이퍼 업데이트 할 수 있습니다\-V는 통합된 관리 및 소프트웨어 업데이트 환경이 제공 하기 때문에 클러스터.  
  
-   CAU는 Windows Server 2016, Windows Server 2012 R2 및 Windows Server 2012를 실행 하는 클러스터 에서만 지원 됩니다. VMM에서는 하이퍼\-V Windows Server 2008 R2 및 Windows Server 2008을 실행 하는 컴퓨터에서 클러스터.  
  
## <a name="can-i-use-remote-updating-on-a-cluster-that-is-configured-for-self-updating"></a>사용할 수 있는 원격\-자체에 대해 구성 된 클러스터에서 업데이트\-업데이트?  
예 자동에서 장애 조치 클러스터\-원격을 통해 구성 업데이트를 업데이트할 수 있습니다\-에서 업데이트\-Windows 업데이트가 구성 된 경우에 컴퓨터에서 언제 든 지 Windows 업데이트 검사를 강제로 수 있습니다 하는 것 처럼 요청 업데이트를 자동으로 설치 합니다. 그러나 이 경우 업데이트 실행이 이미 진행되지 않았는지 확인해야 합니다.  
  
## <a name="can-i-reuse-my-cluster-update-settings-across-clusters"></a>여러 클러스터 간에 클러스터 업데이트 설정을 다시 사용할 수 있습니까?  
예 CAU에서는 클러스터 업데이트 시 업데이트 실행 동작이 서로 다른 여러 업데이트 실행 옵션을 사용할 수 있습니다. 이러한 옵션을 업데이트 실행 프로필로 저장하여 어느 클러스터에서나 다시 사용할 수 있습니다. 설정을 저장하여 업데이트 요구 사항이 비슷한 장애 조치(failover) 클러스터에서 다시 사용하는 것이 좋습니다. 예를 들어, 만들 수 있습니다를 "비즈니스\-중요 한 SQL Server 클러스터 업데이트 실행 프로필" 비즈니스를 지 원하는 모든 Microsoft SQL Server 클러스터에 대 한\-중요 한 서비스입니다.  
  
## <a name="where-is-the-cau-plug-in-specification"></a>CAU 플러그 인\-사양에서?  
  
-   [클러스터\-인식 업데이트 플러그 인\-참조](https://msdn.microsoft.com/library/hh418084(VS.85).aspx)  
  
-   [클러스터 인식 업데이트 플러그 인\-샘플](https://code.msdn.microsoft.com/windowsdesktop/Cluster-Aware-Updating-6a8854c9)  
  
## <a name="see-also"></a>참조  
  
-   [클러스터\-인식 업데이트 개요](cluster-aware-updating.md)  
  
