---
title: Windows Server 버전 1903의 새로운 기능
description: 이 항목에서는 반기 채널 릴리스는 버전 1903, Windows Server의 새로운 기능 중 일부를 설명 합니다.
ms.prod: windows-server-threshold
ms.technology: server-general
ms.topic: article
author: jasongerend
ms.author: jgerend
ms.date: 05/21/2019
ms.openlocfilehash: 2aa84df1ca162cb6e2dfa580b4b0744ff08cc95a
ms.sourcegitcommit: c8cc0b25ba336a2aafaabc92b19fe8faa56be32b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/21/2019
ms.locfileid: "65983443"
---
# <a name="whats-new-in-windows-server-version-1903"></a>Windows Server 버전 1903의에서 새로운 기능

>적용 대상: Windows Server(반기 채널)

이 항목에서는 반기 채널 릴리스는 버전 1903, Windows Server의 새로운 기능 중 일부를 설명 합니다. 이러한 기능은 실행 및 컨테이너, Server Core 설치에서 작업에 대 한 도구 및 Linux 장치에서 저장소를 마이그레이션하는 기능을 관리 하기 위한 향상 된 기능을 포함 합니다.

참조 대신 최신 장기 서비스 채널 (LTSC) 릴리스의 Windows Server의 새로운 기능 확인을 참조 하세요 [What's New in Windows Server 2019](../get-started-19/whats-new-19.md)합니다. 도 참조 하세요 [Windows 10에서 IT 전문가 콘텐츠 버전이 1903 새로운](https://docs.microsoft.com/windows/whats-new/whats-new-windows-10-version-1903)합니다.

이 릴리스에 대 한 시스템 요구 사항은 Windows Server 2019와 동일-참조 [시스템 요구 사항](../get-started-19/sys-reqs-19.md) 자세한 정보에 대 한 합니다. 최근에 제거 된 항목을 보려면 [Features Removed or Windows Server 버전 1903부터 대체에 대 한 계획 됨](../get-started-19/removed-features-1903.md)

> [!NOTE]
> Windows 컨테이너 호스트 서버와 동일한 버전의 Windows 사용 해야 합니다 또는 *이전* 버전입니다. 예를 들어, Windows Server의 릴리스 버전을 실행 하는 호스트 서버를 버전 1903 (18342 빌드) 수 같거나 이전 버전을 사용 하 여 Windows Server 컨테이너를 실행 및 빌드 번호 (경우에 컨테이너는 Insider Preview 버전의 Windows에서 사용). 자세한 내용은 참조 하세요. [Windows 컨테이너 버전 호환성](https://docs.microsoft.com/virtualization/windowscontainers/deploy-containers/version-compatibility)합니다.

## <a name="enhanced-support-for-non-microsoft-container-services"></a>타사 컨테이너 서비스에 대 한 향상 된 지원

Azure container service 및 Microsoft 이외의 컨테이너 서비스를 지원 하기 위해 플랫폼 기능을 개선 되었습니다.

- 사용 하 여 호스트 계산 서비스 (HCS)에 Windows (LCOW) Azure에서 Windows 컨테이너 및 Linux 컨테이너의 pod를 지원 하기 위해 CRI containerd 통합 했습니다.
- Windows 컨테이너 지원을 사용 하려면 Kubernetes 커뮤니티와 협력 했습니다. Kubernetes v1.14의 릴리스를 사용 하 여 Windows Server 노드 지원 공식적으로 안정적인에 베타 버전에서 졸업 합니다. 자세한 내용은 참조 하세요. [이제 Kubernetes에서 지원 되는 Windows 컨테이너](https://cloudblogs.microsoft.com/opensource/2019/03/25/windows-server-containers-now-supported-kubernetes/)합니다.
- Windows에 대 한 Tigera Calico Tigera Essentials 구독에 포함 및 제품으로 출시 되었습니다. 비 오버레이 네트워킹 및 네트워크 정책에서 상호 운용 가능한 Linux/Windows 환경을 혼합 합니다.
- 확장성 향상 오버레이 네트워킹 Flannel 및 Kubernetes v1.14의 최신 릴리스를 통해 Kubernetes 사용 하 여 통합을 비롯 한 Windows 컨테이너에 대 한 지원 향상를 전달 했습니다. 자세한 내용은 참조 하세요. [Kubernetes에서 Windows 지원에 대 한 소개](https://kubernetes.io/docs/setup/windows/)합니다.

## <a name="directx-hardware-acceleration-in-containers"></a>컨테이너에서 DirectX 하드웨어 가속

에서는 로컬 그래픽 처리 유닛 (GPU) 하드웨어를 사용 하 여 Machine Learning (ML) 추론 등의 Windows 컨테이너 tp 지원 시나리오에서 DirectX Api의 하드웨어 가속에 대 한 지원을 사용 하도록 설정 합니다. 자세한 내용은 참조 하세요. [Windows 컨테이너에 가져오는 GPU 가속](https://techcommunity.microsoft.com/t5/Containers/Bringing-GPU-acceleration-to-Windows-containers/ba-p/393939)합니다.

## <a name="updated-container-identity-and-group-managed-service-account-documentation"></a>업데이트 된 컨테이너 id 및 그룹 관리 서비스 계정 설명서

예제 및 호환성 정보를 더 추가한를 [그룹 관리 서비스 계정](https://docs.microsoft.com/virtualization/windowscontainers/manage-containers/manage-serviceaccounts) 설명서를 하 고는 [자격 증명 사양 PowerShell 모듈](https://www.powershellgallery.com/packages/CredentialSpec) PowerShell 갤러리에서 사용할 수 있습니다. 자세한 내용은 참조는 [컨테이너 id에 대 한 새로운](https://techcommunity.microsoft.com/t5/Containers/What-s-new-for-container-identity/ba-p/389151) 블로그 게시물.

## <a name="add-task-scheduler-and-hyper-v-manager-to-server-core-installations"></a>Server Core 설치에 작업 Scheduler 및 Hyper-v 관리자 추가

아시다시피, Windows Server, 프로덕션 환경에서 반기 채널을 사용 하는 경우 Server Core 설치 옵션을 사용 하는 것이 좋습니다. 그러나 기본적으로 Server Core는 여러 가지 유용한 관리 도구를 생략합니다. 가장 많은 일반적으로 도구는 응용 프로그램 호환성 기능을 설치 하 여 사용 되지만 여전히 사항이 일부 누락 된 도구를 추가할 수 있습니다.

이 버전의 응용 프로그램 호환성 기능에 따라서 두 도구를 더 추가한 고객 피드백에 따라: 작업 스케줄러 (taskschd.msc) 및 Hyper-v 관리자 (virtmgmt.msc).

자세한 내용은 참조 하세요. [Server Core 응용 프로그램 호환성 기능](../get-started-19/install-fod-19.md)합니다.

## <a name="storage-migration-service-now-migrates-local-accounts-clusters-and-linux-servers"></a>로컬 계정, 클러스터 및 Linux 서버에 이제 storage Migration Service 마이그레이션

저장소 마이그레이션 서비스를 사용 하면 쉽게 서버를 Windows Server의 최신 버전으로 마이그레이션할 수입니다. 서버에서 데이터를 인벤토리에 포함 하 고 데이터 및 구성을 새 서버로 전송 하는 그래픽 도구를 제공, 앱 또는 사용자가 아무 것도 변경할 필요가 없이 합니다.

이 버전의 Windows Server 마이그레이션을 오케스트레이션 하기 위해 사용 하는 경우에 다음과 같은 기능을 추가 했습니다.

- 새 서버에 로컬 사용자 및 그룹 마이그레이션
- 장애 조치 클러스터에서 저장소를 마이그레이션
- Samba를 사용 하는 Linux 서버에서 저장소를 마이그레이션하십시오.
- 보다 쉽게 Azure File Sync를 사용 하 여 Azure로 마이그레이션된 공유를 동기화
- Azure와 같은 새 네트워크로 마이그레이션

저장소 마이그레이션 서비스에 대 한 자세한 내용은 참조 하세요. [저장소 마이그레이션 서비스 개요](../storage/storage-migration-service/overview.md)합니다.

## <a name="system-insights-disk-anomaly-detection"></a>시스템 Insights 디스크 변칙 검색

[시스템 Insights](../manage/system-insights/overview.md) 로컬 Windows Server 시스템 데이터를 분석 하 고 서버의 기능에 대 한 정보를 제공 하는 예측 분석 기능입니다. 많은 기본 제공 기능을 제공 하지만 디스크 변칙 검색부터 Windows Admin Center 통해 추가 기능을 설치 하는 기능 추가 했습니다.

변칙 검색 디스크는 디스크 동작 하는 경우를 강조 표시 하는 새로운 기능 *다르게* 평소 보다 합니다. 다른 반드시 하는 동안 시스템에서 문제를 해결할 때에 이러한 비정상적인 분 표시 나쁘지 유용할 수 있습니다.

이 기능은 Windows Server 2019를 실행 하는 서버를 사용할 수도 있습니다.

## <a name="windows-admin-center-enhancements"></a>Windows Admin Center 향상 된 기능

Windows Admin Center 새 릴리스가, Windows Server에 새 기능을 추가 합니다. 최신 기능에 대 한 정보를 참조 하세요 [Windows Admin Center](../manage/windows-admin-center/understand/windows-admin-center.md)합니다.

## <a name="security-baseline-for-windows-10-and-windows-server"></a>Windows 10 및 Windows Server에 대 한 보안 기준

초안 릴리스를 [보안 구성 기준 설정을](https://blogs.technet.microsoft.com/secguide/2019/04/24/security-baseline-draft-for-windows-10-v1903-and-windows-server-v1903/) 1903 버전은 Windows Server 및 Windows 10 버전이 1903에 대 한 합니다.

## <a name="setupdiag"></a>설정 플래그
[SetupDiag](https://docs.microsoft.com/windows/deployment/upgrade/setupdiag) 1.4.1 버전이 사용 가능 합니다.

SetupDiag는 Windows 업데이트 하지 못했습니다. 이유를 진단 하는 데 도움이 되는 명령줄 도구입니다. SetupDiag는 Windows 설치 로그 파일을 검색하여 작동합니다. 로그 파일을 검색할 때 SetupDiag는 알려진 문제에 맞게 규칙 집합을 사용합니다. 53 규칙이 rules.xml 파일에 포함 된 SetupDiag의 현재 버전에서는 SetupDiag 실행 될 때 추출 됩니다. rules.xml 파일은 SetupDiag의 새 버전에서 업데이트됩니다.

## <a name="update-rollback-improvements"></a>업데이트 롤백 개선 사항

서버 수 이제 자동으로 복구 시작 오류에서 최신 드라이버 또는 품질 업데이트의 설치 후 시작 실패를 도입 하는 경우 업데이트를 제거 하 여 합니다. 장치 드라이버 업데이트 품질의 최근 설치가 제대로 시작할 수 없는 경우 Windows는 이제 자동으로 장치를 다시 시작 하는 업데이트 및 제거 정상적으로 실행 합니다.

이 기능을 사용 하려면 서버를 사용 하 여 Server Core 설치 옵션을 사용 하 여 수를 [Windows 복구 환경](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-recovery-environment--windows-re--technical-reference) 파티션 합니다.

## <a name="microsoft-defender-advanced-threat-protection-atp-improvements"></a>Microsoft Defender Advanced Threat Protection (ATP) 향상 된 기능

Windows Server에 포함 된 Microsoft Defender 고급 스레드 Protection (자세한 내용은 참조 하세요. [Windows Server에서 Windows Defender 바이러스 백신](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-antivirus/windows-defender-antivirus-on-windows-server-2016)). 이 릴리스에 다음과 같은 개선 사항이 포함 되어 있습니다.

- [공격 노출 영역 축소](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/overview-attack-surface-reduction) – IT 관리자가 구성할 수를 정의할 수 있도록 하는 고급 웹 보호를 사용 하 여 장치 허용 및 거부 목록을 특정 URL 및 IP 주소에 대 한 합니다.
- [다음 세대 보호](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-antivirus/windows-defender-antivirus-in-windows-10) – 컨트롤 랜 섬 웨어, 자격 증명이 오용 및 이동식 저장소를 통해 전송 되는 공격 으로부터 보호 하도록 확장 되었습니다.
    - 무결성 적용 기능 – 사용 원격 런타임 증명 합니다.
    - 변조 방지 기능 – OS와 공격자가 중요 한 ATP 보안 기능 격리를 사용 하 여 가상화 기반 보안.
- Microsoft Defender ATP 차세대 보호 기술:
    - **고급 기계 학습**: 고급 기계 학습 및 혁신적인 취약점으로 인 한 공격 기술, 도구 및 맬웨어를 사용 하 여 apex 공격자 로부터 보호할 수 있게 하는 AI 모델을 사용 하 여 향상 되었습니다.
    - **긴급 사건 보호**: 새 공격이 검색 된 경우 새로운 인텔리전스를 사용 하 여 장치를 업데이트 자동으로 긴급 사건 보호를 제공 합니다.
    - **ISO 27001 인증 준수**: 위협, 취약성 및 영향에 대 한 클라우드 서비스의 분석 하 고 위험 관리 및 보안 제어 충족 되는지 확인 합니다.
    - **지리적 위치 지원**: 지리적 위치 및 구성 가능한 보존 정책 뿐만 아니라 샘플 데이터 주권 지원 합니다.