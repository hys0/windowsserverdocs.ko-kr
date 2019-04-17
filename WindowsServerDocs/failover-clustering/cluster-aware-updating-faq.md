---
ms.assetid: 6416d125-bcaf-433d-971a-2f0283bca2c2
title: "클러스터 인식 업데이트-자주 묻는 질문"
ms.topic: article
ms.prod: storage-failover-clustering
manager: dongill
ms.author: jgerend
author: JasonGerend
ms.date: 4/28/2017
description: "Windows Server에서 클러스터 업데이트에 대 한 질문과 대답입니다."
ms.openlocfilehash: 8417ea8b6b76e16c3f4db3bac5062d90a8da3ff2
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2017
---
# <a name="cluster-aware-updating-frequently-asked-questions"></a>클러스터 업데이트: 질문과 대답

> 에 해당: (세미콜론 연간 채널) Windows Server, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

[클러스터 인식 업데이트](cluster-aware-updating.md) \(CAU\) 클러스터 노드에서의 계획된 장애 조치 이상 서비스 사용 가능성 영향을 미칠 하지 않는 방식으로 장애 조치가 클러스터의 모든 서버에서 소프트웨어 업데이트를 조정 하는 기능입니다. 지속적인 가용성 기능으로 일부 응용 프로그램에 대 한 \ (Hyper\ V 실시간 마이그레이션으로) 또는 SMB 3.x 파일 서버 SMB 투명 Failover\와 같은 CAU 자동화 된 클러스터 서비스 사용 가능성에 영향을 주지로 업데이트 조정할 수 있습니다.

## <a name="does-cau-support-updating-storage-spaces-direct-clusters"></a>CAU 업데이트 Storage Spaces Direct 클러스터 지원 되나요?  
예입니다. 업데이트 CAU 지원 [Storage Spaces Direct](../storage/storage-spaces/storage-spaces-direct-overview.md) 클러스터 배포 유형에 상관 없이: 하이퍼 수렴 또는 수렴 합니다. 특히, CAU 오케스트레이션 정상적인 기본 클러스터 저장소 공간에 대 한 대기 각 클러스터 노드에서 일시 중지 하는 보장 합니다.

## <a name="does-cau-work-with-windows-server-2008-r2-or-windows-7"></a>CAU는 Windows Server 2008 R2 또는 Windows 7 함께 작동 하나요?  
아니요. Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows 10,.1, Windows 8 또는 Windows 8을 실행 중인 컴퓨터 에서만에서 작동 업데이트 클러스터 CAU을 조정 합니다. Windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012 업데이트 되 고 장애 클러스터 실행 해야 합니다.
  
## <a name="is-cau-limited-to-specific-clustered-applications"></a>CAU 클러스터 특정 응용 프로그램 제한 되어 있나요?  
아니요. CAU 클러스터 응용 프로그램의 종류에 알 수 없는 경우 CAU는 Api 및 PowerShell cmdlet 클러스터링 위로 중첩 된 외부 cluster\ 업데이트 솔루션입니다. 따라서 CAU 클러스터 장애 조치 Windows Server 클러스터에서 구성 된 응용 프로그램에 대 한 업데이트를 조정할 수 있습니다.  
  
> [!NOTE]  
> 다음 클러스터 작업 테스트 되 고 CAU 용으로 인증 현재: SMB Hyper\ V, Dfs, DFS 네임 스페이스, iSCSI, 및 NFS 합니다.  
  
## <a name="does-cau-support-updates-from-microsoft-update-and-windows-update"></a>Microsoft 업데이트에서 업데이트 및 Windows 업데이트를 CAU 지원 되나요?  
예입니다. 기본적으로 CAU 클러스터 노드에서 Windows 업데이트 에이전트 \(WUA\) 유틸리티 Api를 사용 하 여 plug\ 기능과 구성 됩니다. Microsoft 업데이트 및 Windows 업데이트 또는 Windows Server Update Services \(WSUS\) 업데이트 원본으로 가리키도록 WUA 인프라를 구성할 수 있습니다.  
  
## <a name="does-cau-support-wsus-updates"></a>WSUS 업데이트를 CAU 지원 되나요?  
예입니다. 기본적으로 CAU 클러스터 노드에서 Windows 업데이트 에이전트 \(WUA\) 유틸리티 Api를 사용 하 여 plug\ 기능과 구성 됩니다. 로컬 Windows Server Update Services \(WSUS\) 서버 또는 Microsoft 업데이트 및 Windows 업데이트에 업데이트가 원본으로 가리키도록 WUA 인프라를 구성할 수 있습니다.  
  
## <a name="can-cau-apply-limited-distribution-release-updates"></a>CAU 제한 배포 릴리스 업데이트를 적용할 수 있나요?  
예입니다. 하도록 Windows 업데이트 에이전트 \(WUA\) plug\ 하 여 다운로드할 수 없습니다 Microsoft 업데이트 또는 Windows 업데이트를 통해 핫픽스 라고도 제한 배포 릴리스 \(LDR\) 업데이트를 게시 되지 않은-CAU 기본적으로 사용 하는 합니다.  
  
그러나 CAU에서을 포함 한 두 번째 plug\-핫픽스 업데이트 적용을 선택할 수 있습니다. 도이 핫픽스 plug\에서 non\ Microsoft 드라이버, 펌웨어 및 BIOS 업데이트 적용을 사용자 지정할 수 있습니다.  
  
## <a name="can-i-use-cau-to-apply-cumulative-updates"></a>누적 업데이트를 적용 CAU를 사용할 수 있나요?  
예입니다. 누적 업데이트는 일반 배포 출시 업데이트 또는 LDR 업데이트를 CAU을 적용할 수 있습니다.  
  
## <a name="can-i-schedule-updates"></a>업데이트를 예약할 수 있나요?  
예입니다. CAU는 업데이트를 예약 수 있도록 두 가지는 다음과 같은 업데이트 모드를 지원 합니다.  
  
**Self\ 업데이트** 클러스터 자체에 따라 업데이트 정의 된 프로필 및 주기적으로와 같은 월별 유지 관리 기간 동안를 사용할 수 있습니다. Self\ 업데이트 실행 필요할 때 언제 든 지 시작할 수 있습니다. Self\ 업데이트 모드를 사용 하려면 CAU 클러스터 역할 클러스터에 추가 해야 합니다. CAU self\ 업데이트 기능은 같은 다른 클러스터 작업을 수행 하 고 업데이트 coordinator 컴퓨터의 예정 된 조치와 계획 되지 않은으로 원활 하 게 사용할 수 있습니다.  
  
**Remote\ 업데이트** 실행 업데이트는 Windows 또는 Windows Server를 실행 하는 컴퓨터에서 언제 든 지 시작할 수 있습니다. 클러스터 인식 업데이트 창 또는 사용 하 여 실행 하는 업데이트를 시작할 수 있는 **Invoke\ CauRun** PowerShell cmdlet 합니다. Remote\ 업데이트 기본 모드 CAU에 대 한 업데이트입니다. 작업 스케줄러를 사용 하 여 실행 하 고 [호출 CauRun](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/invoke-caurun) 클러스터 노드에서 중 하나 하지 않은 원격 컴퓨터에서 원하는 일정에 따라 cmdlet 합니다.  
  
## <a name="can-i-schedule-updates-to-apply-during-a-backup"></a>백업 하는 동안 적용에 대 한 업데이트를 예약할 수 있나요?  
예입니다. CAU 제한 이런 점과 부과 되지 않습니다. 그러나 수행 하 여 소프트웨어 업데이트 서버에 \ (관련된 잠재적인 restarts\) 서버 백업에 있는 동안 진행 된 하지 IT 가장 좋은 방법은 합니다. CAU 리소스가 장애 장애; 확인 하는 Api 클러스터링에 의존는 주의 따라서 CAU 서버 백업 상태를 인식 하지입니다.  
  
## <a name="can-cau-work-with-system-center-configuration-manager"></a>CAU는 System Center Configuration Manager 사용할 수 있나요?  
CAU는 클러스터 노드에서 소프트웨어 업데이트를 조정 하는 도구 및 Configuration Manager도 서버 소프트웨어 업데이트를 수행 합니다. 것이 서로 다른 Windows Server Update Services 서버를 사용 하는 등 모든 datacenter 배포에서 동일한 서버 보도 겹치는 없는 수 있도록이 도구를 구성 하는 것이 중요 합니다. 이렇게 하면 클러스터 인식 통합 하지 구성 Manager\ 기반 업데이트 때문에 CAU를 사용 하 여 뒤 목표 실수로 패 않습니다.  
  
## <a name="do-i-need-administrative-credentials-to-run-cau"></a>관리자 자격 증명 CAU 실행할 필요 한가요?  
예입니다. CAU 도구를 실행 하는 데 CAU 필요 로컬 서버 관리 자격 증명 하거나 필요한 것은 **클라이언트 인증 후 가장** 로컬 서버 또는 실행 되는 클라이언트 컴퓨터에 올바르게 사용자 합니다. 그러나 클러스터 노드에서 소프트웨어 업데이트를 조정 하는 데 CAU 마다 노드에서 클러스터 관리 자격 증명을 필요 합니다. 으로 자격 증명을 않고도 CAU UI를 시작할 수 있지만 표시 클러스터 관리 자격에 대 한 업데이트를 적용 하거나 미리 클러스터 인스턴스에 연결할 때입니다.  
  
## <a name="can-i-script-cau"></a>CAU 스크립트 수 있나요?  
예입니다. CAU 풍부한 스크립팅 옵션을 제공 하는 PowerShell cmdlet 함께 제공 됩니다. CAU UI 호출 CAU 작업을 수행 하는 동일한 cmdlet입니다.  

## <a name="what-happens-to-active-clustered-roles"></a>현재 클러스터 역할을 어떻게 될까요?

클러스터 역할 \ (응용 프로그램 및 services\ 이전의 함) 노드에서 활성화 되어 있는, 장애 조치 통하지 전에 소프트웨어 업데이트를 시작할 수 있습니다. CAU 일시 중지 되는 모든 활동 클러스터 역할 노드 드레이닝 유지 관리 모드를 사용 하 여 이러한 장애 조치를 조정 합니다. 소프트웨어 업데이트가 완료 되 면 CAU 노드 다시 시작 하 고 업데이트 된 노드에서 클러스터 역할 장애 합니다. 이렇게 하면는 노드를 기준으로 역할 클러스터 배포 그대로 전체 클러스터의 CAU 업데이트 실행 합니다.  
  
## <a name="how-does-cau-select-target-nodes-for-clustered-roles"></a>CAU 대상 노드의 클러스터 역할를 선택 하는 방법

CAU 클러스터링 Api 조정는 장애 조치를 기반으로 합니다. 클러스터링 API 구현 내부 메트릭 및 지능형 추론에 의존 하 여 대상 노드 선택 \ (예: 작업 levels\) 대상 노드에서 합니다.  
  
## <a name="does-cau-load-balance-the-clustered-roles"></a>CAU 로드 클러스터 역할 균형 되나요?

CAU 부하 분산 배포 클러스터 역할 유지 하기 위해 클러스터 노드가 하지만 시도 하지 않습니다. 실패 하려고 CAU 클러스터 노드에서 업데이트 완료 되 면 뒤로 이전에 해당 노드에서 클러스터 역할 호스트 합니다. CAU 일시 중지 프로세스가 시작 하는 데 리소스 다시 실패 하는 Api 클러스터링에 의존 합니다. 따라서 담당자 기본 설정 및 예상치 못한 장애 조치 없는 경우, 클러스터 역할 메일은 그대로 유지 됩니다.  
  
## <a name="how-does-cau-select-the-order-of-nodes-to-update"></a>CAU 노드 순서 업데이트를 선택 하는 방법  
기본적으로 CAU를 노드 순서 업데이트 활동이 수준에 따라 선택 합니다. 적은 클러스터 역할 호스트 하는 노드 먼저 업데이트 됩니다. 그러나 관리자 노드 CAU UI에서 업데이트 실행 매개 변수를 지정 하거나 PowerShell cmdlet 사용 하 여 업데이트에 대 한 특정 순서를 지정할 수 있습니다.  
  
## <a name="what-happens-if-a-cluster-node-is-offline"></a>클러스터 노드에서 오프 라인 상태인 경우 어떻게 되나요?

관리자가 업데이트 실행 시작 노드 오프 라인 상태일 수 있는 횟수에 대 한도 괜찮나요 임계값을 지정할 수 있습니다. 따라서 모든 클러스터 노드에서 온라인 없는 경우에 업데이트 실행 클러스터에서 진행할 수 있습니다.  
  
## <a name="can-i-use-cau-to-update-only-a-single-node"></a>CAU 단일 노드만 업데이트를 사용할 수 있나요?  
아니요. CAU는 cluster\ 범위 업데이트 도구를 이므로 클러스터 업데이트를 선택할 수만 있습니다. 업데이트 단일 노드 하려는 경우 기존 서버 도구 CAU 독립적으로 업데이트를 사용할 수 있습니다.  
  
## <a name="can-cau-report-updates-that-are-initiated-from-outside-cau"></a>CAU 외부 CAU에서 시작 되어 있는 업데이트를 보고할 수 있나요?  
아니요. CAU 수만 보고서 업데이트 된 실행 CAU 내부에서 시작 됩니다. 그러나 시작 되는 이후 CAU 업데이트를 실행 non\ CAU 메서드를 통해 설치 된 업데이트 각 클러스터 노드에서에 적용할 수 있는 추가 업데이트를 확인 하려면 간주 적절 하 게 됩니다.  
  
## <a name="can-cau-support-my-unique-it-process-needs"></a>내 고유한 IT 프로세스 환경을 CAU 지원할 수 있나요?  
예입니다. CAU 다음 엔터프라이즈 고유한 IT 프로세스는 고객의 요구에 맞게 유연 하 게 크기를 제공 합니다.  
  
**스크립트** pre\ 업데이트 PowerShell 스크립트를와 post\ 업데이트 PowerShell 스크립트를 지정할 수 업데이트를 실행 합니다. 업데이트 pre\ 스크립트 노드 일시 중지 하기 전에 각 클러스터 노드에서 실행 됩니다. 업데이트 post\ 스크립트 노드 업데이트가 설치 된 후 각 클러스터 노드에서 실행 됩니다.  
  
> [!NOTE]  
> .NET framework 4.6 또는 4.5 및 PowerShell pre\ 업데이트와 post\ 업데이트 스크립트를 실행할 하려는 각 클러스터 노드에서 설치 해야 합니다. 클러스터 노드에서 PowerShell 원격을 활성화 해야 합니다. 자세한 시스템 요구 사항에 대 한 참고 [요구 사항 및 모범 사례 클러스터 업데이트에 대 한](cluster-aware-updating-requirements.md)합니다.  
  
**고급 옵션을 업데이트를 실행** 관리자 다양 한 각 노드에서 업데이트 프로세스를 다시 시도 하는 시간을 최대 등 실행 업데이트 고급 옵션에서에서 추가적으로 지정할 수 있습니다. 이러한 옵션 CAU UI 또는 CAU PowerShell cmdlet 사용 하 여 지정할 수 있습니다. 이러한 사용자 지정 설정 업데이트를 실행 프로필에 저장 하 고 이상의 업데이트 실행 다시 사용할 수 있습니다.  
  
**공용 plug\ 아키텍처** CAU 등록 등록을 취소 하는 기능을 포함 하 고 선택 plug\ 기능 CAU 두 가지 기본 plug\ 기능와 함께 제공: Windows 업데이트 에이전트 \(WUA\) Api 각 클러스터 노드에서 조정 하나 두 번째 클러스터 노드에서에 액세스할 수 있는 파일 공유를 수동으로 복사 핫픽스 적용 됩니다. 엔터프라이즈에으로 이러한 두 가지 plug\ 기능 충족할 수 없는 고유한 요구를 엔터프라이즈 plug\에서 공개 API 사양에 따라 새 CAU 빌드할 수 있습니다. 자세한 내용은 참조 [Cluster\ 인식 업데이트 Plug\에서 참조](http://msdn.microsoft.com/library/hh418084(VS.85).aspx)합니다.  
  
CAU 사용자 지정 하 고 구성에 대 한 정보에 대 한 다른 지원 하기 위해 plug\ 기능 표시 시나리오를 업데이트 [Plug\ 기능의 작동 방식을](assetId:///847b571b-12b3-473c-953f-75a5a1f51333)합니다.  
  
## <a name="how-can-i-export-the-cau-preview-and-update-results"></a>미리 보기 CAU 내보내려면 고 결과 업데이트 수 어떻게 하나요?  
CAU는 command\ 줄 인터페이스를 통해 및 UI를 통해 내보내기 옵션을 제공 합니다.  
  
**Command\ 줄 인터페이스 옵션:**  
  
-   결과 PowerShell cmdlet 사용 하 여 미리 보기 **Invoke\ CauScan | ConvertTo\ Xml**합니다. 출력: XML  
  
-   결과 PowerShell cmdlet 사용 하 여 보고 **Invoke\ CauRun | ConvertTo\ Xml**합니다. 출력: XML  
  
-   결과 PowerShell cmdlet 사용 하 여 보고 **Get\ CauReport | Export\ CauReport**합니다. 출력: HTML CSV  
  
**UI 옵션:**  
  
-   복사 보고서 결과 **업데이트의 미리 보기** 화면 합니다. 출력: CSV  
  
-   복사 보고서 결과 **보고서가 생성** 화면 합니다. 출력: CSV  
  
-   내보내기 보고서 결과 **보고서가 생성** 화면 합니다. 출력: HTML  
  
## <a name="how-do-i-install-cau"></a>CAU 설치 하려면 어떻게 하나요?  
CAU 설치 클러스터링 기능으로 원활 하 게 통합 되어 있습니다. CAU 다음과 같이 설치 됩니다.  
  
-   클러스터 노드에서에 설치 되어 클러스터링, CAU WMI(Windows Management Instrumentation) \(WMI\) 공급자 자동으로 설치 됩니다.  
  
-   장애 클러스터링 도구 기능 서버 또는 클라이언트 컴퓨터에 설치 되 면 업데이트 클러스터 인식 UI와 PowerShell cmdlet 자동으로 설치 됩니다.
  
## <a name="does-cau-need-components-running-on-the-cluster-nodes-that-are-being-updated"></a>CAU 업데이트 되는 클러스터 노드에서 실행 구성 요소가 필요 합니까?  
CAU는 클러스터 노드에서 실행 되는 서비스가 필요 하지 않습니다. 그러나 CAU 필요한 소프트웨어 구성 요소 \ (WMI provider\) 클러스터 노드에서 설치 합니다. 이 구성 요소 클러스터링 기능과 함께 설치 되어 있습니다.  
  
Self\ 업데이트 모드를 사용 하려면 CAU 클러스터 역할 클러스터에 추가 해야 합니다.  
  
## <a name="what-is-the-difference-between-using-cau-and-vmm"></a>CAU 및 VMM 사용 하 여 간의 차이점 무엇 인가요?  
  
-   System Center 가상 컴퓨터의 관리자 \(VMM\)는 CAU 모든 종류의 지원 되는 장애 클러스터, Hyper\ V 클러스터 포함 하 여 업데이트할 수 있지만 Hyper\ V 클러스터 업데이트에 초점을 합니다.  
  
-   VMM은 CAU 모든 Windows Server에 대 한 라이선스는 반면 추가 라이선싱 필요 합니다. CAU 기능, 도구 및 UI 구성 요소 클러스터링와 설치 됩니다.  
  
-   System Center 라이선스를 이미 소유 VMM Hyper\ V 클러스터 통합된 관리 및 소프트웨어 업데이트 경험을 제공 하기 때문에 업데이트를 사용 하 여 계속 수 있습니다.  
  
-   CAU는 클러스터 Windows Server 2016, Windows Server 2012 R2 및 Windows Server 2012를 실행 하는 경우에 지원 됩니다. 또한 VMM Windows Server 2008 R2 및 Windows Server 2008 실행 하는 컴퓨터에서 Hyper\ V 클러스터를 지원 합니다.  
  
## <a name="can-i-use-remote-updating-on-a-cluster-that-is-configured-for-self-updating"></a>사용할 수 있습니까 remote\ 업데이트 구성 된 클러스터 self\ 업데이트에 대 한?  
예입니다. 업데이트가 자동으로 설치 하도록 Windows 업데이트 구성 된 경우에 컴퓨터에서 언제 든 지 Windows 업데이트 스캔 하도록 할 수 있습니다 처럼 remote\ 업데이트 on\ 요청을 통해 self\ 업데이트 구성을 클러스터 장애 조치를 업데이트할 수 있습니다. 그러나, 업데이트 실행 아닌지 이미 진행 중인 있는지 확인 해야 할 수도 있습니다.  
  
## <a name="can-i-reuse-my-cluster-update-settings-across-clusters"></a>클러스터 간에 내 클러스터 업데이트 설정을 다시합니다  
예입니다. CAU 다양 한 업데이트 실행 시 작동 방식을 클러스터 업데이트를 결정 하는 업데이트를 실행 하는 옵션을 지원 합니다. 이러한 옵션으로는 업데이트를 실행 프로필을 저장할 수 하 고 모든 클러스터 전체 다시 사용할 수 있습니다. 저장 하 고 비슷한 업데이트 요구 사항을 있는 클러스터 장애 조치 간에 설정을 다시 사용 하는 것이 좋습니다. 예를 들어, "Business\ 중요 SQL Server 클러스터 업데이트 실행"에 대 한 프로필 business\ 중요 한 서비스를 지 원하는 모든 Microsoft SQL Server 클러스터 만들 수 있습니다.  
  
## <a name="where-is-the-cau-plug-in-specification"></a>CAU plug\의 사양이 어디 일까요?  
  
-   [Cluster\ 인식 Plug\에서 참조 업데이트](http://msdn.microsoft.com/library/hh418084(VS.85).aspx)  
  
-   [클러스터 샘플 plug\에서 인식 업데이트](http://code.msdn.microsoft.com/windowsdesktop/Cluster-Aware-Updating-6a8854c9)  
  
## <a name="see-also"></a>참조 하십시오  
  
-   [Cluster\ 인식 업데이트 개요](cluster-aware-updating.md)  
  
