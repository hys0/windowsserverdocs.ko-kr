---
title: Windows Server 버전 1903의 새로운 기능
description: 이 항목에서는 Windows Server 버전 1903(반기 채널 릴리스)의 새로운 기능 중 일부를 설명합니다.
ms.prod: windows-server-threshold
ms.technology: server-general
ms.topic: article
author: jasongerend
ms.author: jgerend
ms.date: 05/21/2019
ms.openlocfilehash: cde394cd4e626466f17a27a68660e85f9fe55553
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70868526"
---
# <a name="whats-new-in-windows-server-version-1903"></a>Windows Server 버전 1903의 새로운 기능

>적용 대상: Windows Server(반기 채널)

이 항목에서는 Windows Server 버전 1903(반기 채널 릴리스)의 새로운 기능 중 일부를 설명합니다. 이러한 기능에는 컨테이너 실행 및 관리 기능 향상, Server Core 설치 작업 도구 및 Linux 디바이스에서 스토리지를 마이그레이션하는 기능이 포함됩니다.

Windows Server의 최신 LTSC(장기 서비스 채널) 릴리스에서 새로운 기능을 찾는 대신, [Windows Server 2019의 새로운 기능](../get-started-19/whats-new-19.md)을 참조하세요. [Windows 10 버전 1903 IT 전문가 콘텐츠의 새로운 내용](https://docs.microsoft.com/windows/whats-new/whats-new-windows-10-version-1903)도 참조하세요.

이 릴리스의 시스템 요구 사항은 Windows Server 2019와 동일합니다 자세한 내용은 [시스템 요구 사항](../get-started-19/sys-reqs-19.md)을 참조하세요. 최근에 어떤 항목이 제거되었는지 확인하려면 [Windows Server 버전 1903부터 제거되었거나 교체 예정인 기능](../get-started-19/removed-features-1903.md)을 참조하세요.

> [!NOTE]
> Windows 컨테이너는 호스트 서버와 동일한 버전의 Windows 또는 이전 버전을 사용해야 합니다.  예를 들어, Windows Server 버전 1903(빌드 18342)을 실행하는 호스트 서버는(컨테이너가 Insider Preview 버전의 Windows를 사용하더라도 동일 또는 이전 버전 및 빌드 번호의 Windows Server 컨테이너를 실행할 수 있습니다. 자세한 내용은 [Windows 컨테이너 버전 호환성](https://docs.microsoft.com/virtualization/windowscontainers/deploy-containers/version-compatibility)을 참조하세요.

## <a name="enhanced-support-for-non-microsoft-container-services"></a>타사 컨테이너 서비스에 대한 지원 향상

Azure 컨테이너 서비스 및 타사 컨테이너 서비스를 지원하도록 플랫폼 기능이 향상되었습니다.

- Azure의 LCOW(Linux containers on Windows) 및 Windows 컨테이너 Pod를 지원하도록 HCS(호스트 컴퓨팅 서비스)와 CRI-컨테이너가 통합되었습니다.
- Windows 컨테이너 지원이 가능하도록 Kubernetes 커뮤니티와 협력하고 있습니다. Kubernetes v1.14 릴리스와 함께, Windows Server 노드 지원이 베타 버전에서 안정적인 버전으로 공식 업데이트되었습니다. 자세한 내용은 [Kubernetes에서 Windows 컨테이너 지원](https://cloudblogs.microsoft.com/opensource/2019/03/25/windows-server-containers-now-supported-kubernetes/)을 참조하세요.
- Windows용 Tigera Calico는 Tigera Essentials 구독의 일부로 일반 공급되며 혼합형 Linux/Windows 환경에서 비 오버레이 네트워킹 및 네트워크 정책을 상호 운용할 수 있습니다.
- 확장성이 개선되어 Windows 컨테이너에 대한 오버레이 네트워킹 지원이 향상되었습니다. 여기에는 Flannel 및 Kubernetes v1.14의 최신 릴리스를 통한 Kubernetes와의 통합이 포함됩니다. 자세한 내용은 [Kubernetes에서 Windows 지원에 대한 소개](https://kubernetes.io/docs/setup/windows/)를 참조하세요.

## <a name="directx-hardware-acceleration-in-containers"></a>컨테이너에서 DirectX 하드웨어 가속

로컬 GPU(그래픽 처리 장치) 하드웨어를 사용하는 ML(Machine Learning) 추론과 같은 Windows 컨테이너 tp 지원 시나리오에서 DirectX API의 하드웨어 가속을 지원할 수 있습니다. 자세한 내용은 [Bringing GPU acceleration to Windows containers](https://techcommunity.microsoft.com/t5/Containers/Bringing-GPU-acceleration-to-Windows-containers/ba-p/393939)(Windows 컨테이너에서 GPU 가속화)를 참조하세요.

## <a name="updated-container-identity-and-group-managed-service-account-documentation"></a>컨테이너 ID 및 그룹 관리 서비스 계정 설명서 업데이트

[그룹 관리 서비스 계정](https://docs.microsoft.com/virtualization/windowscontainers/manage-containers/manage-serviceaccounts) 설명서에 더 많은 예제와 호환성 정보가 추가되었으며, PowerShell 갤러리에서 [자격 증명 사양 PowerShell 모듈](https://www.powershellgallery.com/packages/CredentialSpec)을 사용할 수 있습니다. 자세한 내용은 [What's new for container identity](https://techcommunity.microsoft.com/t5/Containers/What-s-new-for-container-identity/ba-p/389151)(컨테이너 ID의 새로운 기능) 블로그 게시물을 참조하세요.

## <a name="add-task-scheduler-and-hyper-v-manager-to-server-core-installations"></a>Server Core 설치에 작업 스케줄러 및 Hyper-V 관리자 추가

아시다시피, 프로덕션 환경에서 Windows Server, 반기 채널을 사용할 때는 Server Core 설치 옵션을 사용하는 것이 좋습니다. 하지만 Server Core는 기본적으로 여러 가지 유용한 관리 도구를 생략합니다. 앱 호환성 기능을 설치하여 가장 일반적으로 사용되는 도구를 많이 추가할 수 있지만 여전히 누락되는 도구가 있습니다.

따라서 고객 피드백을 기반으로, 이 버전의 앱 호환성 기능에 두 가지 도구 즉, 작업 스케줄러(taskschd.msc) 및 Hyper-V 관리자(virtmgmt.msc)가 더 추가되었습니다.

자세한 내용은 [Server Core 앱 호환성 기능](../get-started-19/install-fod-19.md)을 참조하세요.

## <a name="storage-migration-service-now-migrates-local-accounts-clusters-and-linux-servers"></a>스토리지 마이그레이션 서비스로 로컬 계정, 클러스터 및 Linux 서버 마이그레이션 가능

스토리지 마이그레이션 서비스를 사용하면 서버를 Windows Server의 최신 버전으로 쉽게 마이그레이션할 수 있습니다. 서버의 데이터를 조사한 다음, 데이터 및 구성을 새로운 서버로 전송하는 그래픽 도구가 제공됩니다. 앱이나 사용자가 아무것도 변경할 필요가 없습니다.

이 버전의 Windows Server를 사용하여 마이그레이션을 오케스트레이션하는 경우, 다음과 같은 기능이 추가됩니다.

- 새 서버로 로컬 사용자 및 그룹 마이그레이션
- 장애 조치 (failover) 클러스터에서 스토리지 마이그레이션
- 삼바를 사용하는 Linux 서버에서 스토리지 마이그레이션
- Azure 파일 동기화를 사용하여 마이그레이션된 공유를 Azure에 쉽게 동기화
- Azure와 같은 신규 네트워크로 마이그레이션

스토리지 마이그레이션 서비스에 대한 자세한 내용은 [스토리지 마이그레이션 서비스 개요](../storage/storage-migration-service/overview.md)를 참조하세요.

## <a name="system-insights-disk-anomaly-detection"></a>시스템 인사이트 디스크 이상 탐지

[시스템 인사이트](../manage/system-insights/overview.md)는 Windows Server 시스템 데이터를 로컬에서 분석하고 서버의 기능에 대한 인사이트를 제공하는 예측 분석 기능입니다. 여기에는 여러 가지 기본 제공 기능이 있지만 Windows Admin Center를 통해 디스크 이상 탐지를 비롯한 추가 기능을 설치할 수 있는 기능이 추가되었습니다.

디스크 이상 탐지는 디스크가 평소와 다르게 작동할 때 강조 표시하는 새로운 기능입니다.  다르게 작동한다고 꼭 나쁜 것은 아니지만, 비정상적인 순간을 보면 시스템 문제를 해결할 때 도움이 될 수 있습니다.

이 기능은 Windows Server 2019를 실행하는 서버에서도 사용할 수 있습니다.

## <a name="windows-admin-center-enhancements"></a>Windows Admin Center 고급 기능

Windows Admin Center의 새로운 릴리스가 출시되면서 Windows Server에 새로운 기능이 추가되었습니다. 최신 기능에 대한 자세한 내용은 [Windows Admin Center](../manage/windows-admin-center/understand/windows-admin-center.md)를 참조하세요.

## <a name="security-baseline-for-windows-10-and-windows-server"></a>Windows 10 및 Windows Server의 보안 기준

Windows 10 버전 1903 및 Windows Server 버전 1903의 [보안 구성 기준 설정](https://blogs.technet.microsoft.com/secguide/2019/04/24/security-baseline-draft-for-windows-10-v1903-and-windows-server-v1903/) 초안 릴리스를 사용할 수 있습니다.

## <a name="setupdiag"></a>SetupDiag
[SetupDiag](https://docs.microsoft.com/windows/deployment/upgrade/setupdiag) 1.4.1 버전이 출시되었습니다.

SetupDiag는 Windows 업데이트가 실패하는 이유를 진단하는 데 사용할 수 있는 명령줄 도구입니다. SetupDiag는 Windows 설치 프로그램 로그 파일을 검색하여 작동합니다. 로그 파일을 검색할 때 SetupDiag는 알려진 문제에 맞게 규칙 세트를 사용합니다. 현재 버전의 SetupDiag에는 SetupDiag가 실행될 때 추출되는 rules.xml 파일에 포함된 53개의 규칙이 있습니다. rules.xml 파일은 SetupDiag의 새 버전에서 업데이트됩니다.

## <a name="update-rollback-improvements"></a>업데이트 롤백 개선 사항

최근 드라이버 또는 품질 업데이트를 설치한 후 시작 오류가 발생하는 경우, 이제 서버가 업데이트를 제거하고 시작 오류에서 자동으로 복구될 수 있습니다. 최근 드라이버 품질 업데이트를 설치한 후 디바이스를 제대로 시작할 수 없는 경우에는, Windows가 자동으로 업데이트를 제거하여 디바이스를 정상적으로 다시 실행합니다.

이 기능을 사용하려면 서버에서 [Windows 복구 환경](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-recovery-environment--windows-re--technical-reference) 파티션과 함께 Server Core 설치 옵션을 사용해야 합니다.

## <a name="microsoft-defender-advanced-threat-protection-atp-improvements"></a>Microsoft Defender ATP(Advanced Threat Protection) 개선 사항

Windows Server에 Microsoft Defender Advanced Thread Protection이 포함됩니다. (자세한 내용은 [Windows Server의 Windows Defender 바이러스 백신](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-antivirus/windows-defender-antivirus-on-windows-server-2016)을 참조하세요). 이 릴리스에는 다음과 같은 개선 사항이 포함되어 있습니다.

- [공격 노출 영역 감소](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/overview-attack-surface-reduction) – IT 관리자는 특정 URL 및 IP 주소에 대한 허용 및 거부 목록을 정의할 수 있는 고급 웹 보호 기능을 사용하여 디바이스를 구성할 수 있습니다.
- [차세대 보호](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-antivirus/windows-defender-antivirus-in-windows-10) – 랜섬웨어, 자격 증명 악용, 이동식 스토리지를 통해 전송되는 공격으로부터 보호하기 위해 컨트롤이 확장되었습니다.
    - 무결성 적용 기능 - 원격 런타임 증명이 가능합니다.
    - 변조 방지 기능 - 가상화 기반 보안을 사용하여 중요한 ATP 보안 기능을 OS 및 공격자로부터 격리합니다.
- Microsoft Defender ATP 차세대 보호 기술:
    - **고급 기계 학습**: 혁신적인 취약점 악용 기법, 도구 및 맬웨어를 사용하는 최상위 공격자로부터 보호할 수 있는 고급 기계 학습 및 AI 모델로 개선되었습니다.
    - **긴급 상황 보호**: 새로운 상황이 탐지되는 경우 새로운 인텔리전스로 디바이스를 자동 업데이트하는 긴급 상황 보호 기능이 제공됩니다.
    - **ISO 27001 준수 인증**: 클라우드 서비스가 위협, 취약점 및 영향을 분석하고 있는지, 위험 관리 및 보안 제어가 제대로 수행되는지 확인합니다.
    - **지리적 위치 지원**: 샘플 데이터의 지리적 위치와 주권은 물론 구성 가능한 보존 정책을 지원합니다.