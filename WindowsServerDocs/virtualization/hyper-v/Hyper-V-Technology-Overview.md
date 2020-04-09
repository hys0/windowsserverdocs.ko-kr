---
title: Hyper-v 기술 개요
description: Hyper-v에 대해 설명 하 고,이를 가져오는 방법, 주요 기능 및 일반적인 용도를 설명 합니다.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.topic: article
ms.assetid: ac069fed-7bf5-4cc3-aff5-25a2766040b8
author: kbdazure
ms.author: kathydav
ms.date: 11/29/2016
ms.openlocfilehash: d21bec24a22607213771bdad0b48df18fd88eb4d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80853246"
---
# <a name="hyper-v-technology-overview"></a>Hyper-v 기술 개요

>적용 대상: Windows Server 2016, Microsoft Hyper-V Server 2016, Windows Server 2019, Microsoft Hyper-V Server 2019

Hyper-v는 Microsoft의 하드웨어 가상화 제품입니다. *가상 컴퓨터*라는 컴퓨터의 소프트웨어 버전을 만들고 실행할 수 있습니다. 각 가상 컴퓨터는 운영 체제 및 프로그램을 실행 하는 전체 컴퓨터 처럼 작동 합니다. 컴퓨팅 리소스를 필요로 하는 경우 가상 머신은 더 많은 유연성을 제공 하 고, 시간과 비용을 절감 하는 데 도움이 되며, 물리적 하드웨어에서 한 운영 체제를 실행 하는 것 보다 더 효율적으로 하드웨어를 사용할 수 있습니다.

Hyper-v는 각각의 격리 된 공간에서 각 가상 컴퓨터를 실행 합니다. 즉, 동일한 하드웨어에서 두 개 이상의 가상 컴퓨터를 동시에 실행할 수 있습니다. 다른 작업에 영향을 미치는 충돌 등의 문제를 방지 하기 위해이 작업을 수행 하거나 다른 사용자, 그룹 또는 서비스에 다른 시스템에 대 한 액세스 권한을 부여 하는 것이 좋습니다.

## <a name="some-ways-hyper-v-can-help-you"></a>Hyper-v를 통해 수행할 수 있는 몇 가지 방법은 다음과 같습니다.

Hyper-v를 통해 다음을 수행할 수 있습니다.

- **사설 클라우드 환경을 설정 하거나 확장 합니다.** 공유 리소스 사용을 전환 하거나 확장 하 고 수요 변화에 따라 사용률을 조정 하 여 더 유연 하 고 주문형 IT 서비스를 제공 합니다.

- **하드웨어를 보다 효율적으로 사용 합니다.** 서버와 워크 로드를 더 저렴 하 고 강력한 물리적 컴퓨터에 통합 하 여 전원 및 물리적 공간을 줄입니다.

- **비즈니스 연속성 개선.** 워크 로드의 예정 된 가동 중지 시간과 예정 되지 않은 가동 중지 시간의 영향을 최소화 합니다.

- **VDI (가상 데스크톱 인프라)를 설정 하거나 확장 합니다.** VDI를 통해 중앙 집중식 데스크톱 전략을 사용 하면 비즈니스 민첩성과 데이터 보안을 높이고 규정 준수를 간소화 하 고 데스크톱 운영 체제 및 응용 프로그램을 관리할 수 있습니다. Hyper-v와 원격 데스크톱 가상화 호스트 (RD 가상화 호스트)를 동일한 서버에 배포 하 여 사용자가 개인용 가상 데스크톱 또는 가상 데스크톱 풀을 사용할 수 있도록 합니다.

- **개발 및 테스트를 보다 효율적으로 수행 합니다.** 물리적 시스템만 사용 하는 경우 필요한 모든 하드웨어를 구입 하거나 유지 관리 하지 않고도 다양 한 컴퓨팅 환경을 재현할 수 있습니다.

## <a name="hyper-v-and-other-virtualization-products"></a>Hyper-v 및 기타 가상화 제품

Windows 및 Windows Server의 hyper-v는 Microsoft Virtual PC, Microsoft Virtual Server 및 Windows Virtual PC와 같은 이전 하드웨어 가상화 제품을 대체 합니다. Hyper-v는 이러한 이전 제품에서 사용할 수 없는 네트워킹, 성능, 저장소 및 보안 기능을 제공 합니다.

Hyper-v와 동일한 프로세서 기능을 필요로 하는 대부분의 타사 가상화 응용 프로그램은 호환 되지 않습니다. 하드웨어 가상화 확장 이라고 하는 프로세서 기능을 공유 하지 않도록 설계 했기 때문입니다. 자세한 내용은 [가상화 응용 프로그램은 hyper-v, Device Guard 및 Credential guard와 함께 작동 하지 않습니다](https://support.microsoft.com/kb/3204980).

## <a name="what-features-does-hyper-v-have"></a>Hyper-v에는 어떤 기능이 있나요?

Hyper-v는 다양 한 기능을 제공 합니다. 이 개요는 기능이 제공 하거나 작업을 수행 하는 방법에 따라 그룹화 되어 있습니다.

**컴퓨팅 환경** -hyper-v 가상 컴퓨터는 물리적 컴퓨터 (예: 메모리, 프로세서, 저장소 및 네트워킹)와 동일한 기본 파트를 포함 합니다. 이러한 모든 부분에는 서로 다른 요구 사항을 충족 하는 다양 한 방법을 구성할 수 있는 기능 및 옵션이 있습니다. 저장소 및 네트워킹을 구성 하는 여러 가지 방법으로 저장소와 네트워킹을 각각 고유한 범주로 간주할 수 있습니다.

**재해 복구 및 백업** -재해 복구를 위해 hyper-v 복제본은 가상 컴퓨터의 복사본을 만들어 다른 물리적 위치에 저장 하기 때문에 복사본에서 가상 컴퓨터를 복원할 수 있습니다. 백업의 경우 Hyper-v는 두 가지 유형을 제공 합니다. 하나는 저장 된 상태를 사용 하 고 다른 하나는 vss (볼륨 섀도 복사본 서비스)를 사용 하므로 VSS를 지 원하는 프로그램에 대해 응용 프로그램 일치 백업을 수행할 수 있습니다.

**최적화** -지원 되는 각 게스트 운영 체제에는 hyper-v 가상 컴퓨터에서 운영 체제를 쉽게 사용할 수 있도록 하는 *통합 서비스*라는 사용자 지정 된 서비스 및 드라이버 집합이 있습니다.

**이식성** -실시간 마이그레이션, 저장소 마이그레이션 및 가져오기/내보내기와 같은 기능을 통해 가상 컴퓨터를 쉽게 이동 하거나 배포할 수 있습니다.

**원격 연결** -hyper-v에는 Windows 및 Linux 모두에서 사용할 원격 연결 도구인 가상 컴퓨터 연결이 포함 됩니다. 원격 데스크톱과 달리이 도구는 콘솔 액세스를 제공 하므로 운영 체제가 아직 부팅 되지 않은 경우에도 게스트에서 발생 하는 상황을 확인할 수 있습니다.

**보안** 보안 부팅 및 보호 된 가상 컴퓨터는 가상 컴퓨터 및 해당 데이터에 대 한 맬웨어 및 기타 무단 액세스를 보호 하는 데 도움이 됩니다.

이 버전에 도입 된 기능에 대 한 요약은 [Windows Server에서 hyper-v의 새로운](What-s-new-in-Hyper-V-on-Windows.md)기능을 참조 하세요. 일부 기능 또는 파트에는 구성할 수 있는 수에 대 한 제한이 있습니다. 자세한 내용은 [Windows Server 2016의 hyper-v 확장성에 대 한 계획](plan/Plan-for-Hyper-V-scalability-in-Windows-Server-2016.md)을 참조 하세요.

## <a name="how-to-get-hyper-v"></a>Hyper-v를 가져오는 방법

Hyper-v는 windows server 및 Windows에서 x64 버전의 Windows Server에서 사용할 수 있는 서버 역할로 사용할 수 있습니다. 서버 지침은 [Windows server에 hyper-v 역할 설치](get-started/Install-the-Hyper-V-role-on-Windows-Server.md)를 참조 하세요. Windows에서는 일부 64 비트 버전의 Windows에서 [기능](https://docs.microsoft.com/virtualization/hyper-v-on-windows/index) 으로 사용할 수 있습니다. 다운로드 가능 하 고 독립 실행형 서버 제품 [Microsoft Hyper-V 서버](https://www.microsoft.com/evalcenter/evaluate-hyper-v-server-2019)이기도 합니다.

## <a name="supported-operating-systems"></a>지원되는 운영 체제

많은 운영 체제가 가상 컴퓨터에서 실행 됩니다. 일반적으로 x86 아키텍처를 사용 하는 운영 체제는 Hyper-v 가상 머신에서 실행 됩니다. 그러나 Microsoft에서 실행할 수 있는 모든 운영 체제를 테스트 하 고 지원 하는 것은 아닙니다. 지원 되는 항목 목록은 다음을 참조 하세요.

- [Windows의 Hyper-v에 대해 지원 되는 Linux 및 FreeBSD 가상 컴퓨터](Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md)

- [Windows Server에서 Hyper-v에 대해 지원 되는 Windows 게스트 운영 체제](Supported-Windows-guest-operating-systems-for-Hyper-V-on-Windows.md)

## <a name="how-hyper-v-works"></a>Hyper-v 작동 방법

Hyper-v는 하이퍼바이저 기반 가상화 기술입니다. Hyper-v는 특정 기능을 사용 하는 실제 프로세서를 필요로 하는 Windows 하이퍼바이저를 사용 합니다. 하드웨어 세부 정보는 [Windows Server의 hyper-v에 대 한 시스템 요구 사항](System-requirements-for-Hyper-V-on-Windows.md)을 참조 하세요.

대부분의 경우 하이퍼바이저는 하드웨어와 가상 컴퓨터 간의 상호 작용을 관리 합니다. 하드웨어에 대 한이 하이퍼바이저 제어 액세스는 가상 머신이 실행 되는 격리 된 환경을 제공 합니다. 일부 구성에서는 가상 컴퓨터 또는 가상 컴퓨터에서 실행 되는 운영 체제에서 그래픽, 네트워킹 또는 저장소 하드웨어에 직접 액세스할 수 있습니다.

## <a name="what-does-hyper-v-consist-of"></a>Hyper-v는 어떻게 구성 되나요?

Hyper-v에는 함께 작동 하는 필수 부분이 있으므로 가상 컴퓨터를 만들고 실행할 수 있습니다. 이러한 부분은 모두 가상화 플랫폼 이라고 합니다. Hyper-v 역할을 설치할 때 집합으로 설치 됩니다. 필요한 부분에는 Windows 하이퍼바이저, Hyper-v 가상 컴퓨터 관리 서비스, 가상화 WMI 공급자, VMbus (가상 컴퓨터 버스), VSP (가상화 서비스 공급자) 및 VID (가상 인프라 드라이버)가 포함 됩니다.

Hyper-v에는 관리 및 연결 도구도 있습니다. Hyper-v 역할이 설치 된 컴퓨터와 Hyper-v 역할이 설치 되어 있지 않은 컴퓨터에 이러한 컴퓨터를 설치할 수 있습니다. 이러한 도구는 다음과 같습니다.

- Hyper-V 관리자
- [Windows PowerShell 용 hyper-v 모듈](https://docs.microsoft.com/powershell/module/hyper-v/index)
- [가상 컴퓨터 연결](https://docs.microsoft.com/windows-server/virtualization/hyper-v/learn-more/hyper-v-virtual-machine-connect) \(VMConnect 라고도\)
- [Windows PowerShell Direct](manage/Manage-Windows-virtual-machines-with-PowerShell-Direct.md)

## <a name="related-technologies"></a>관련 기술

다음은 Hyper-v에서 자주 사용 되는 Microsoft의 기술입니다.

- [장애 조치 클러스터링](../../failover-clustering/whats-new-in-failover-clustering.md)
- [원격 데스크톱 서비스](../../remote/remote-desktop-services/Host-desktops-and-apps-in-Remote-Desktop-Services.md)
- [System Center Virtual Machine Manager](https://docs.microsoft.com/system-center/vmm/overview)

다양 한 저장소 기술: 클러스터 공유 볼륨, SMB 3.0, 저장소 공간 다이렉트

Windows 컨테이너는 다른 가상화 방법을 제공 합니다. MSDN의 [Windows 컨테이너](https://docs.microsoft.com/virtualization/windowscontainers/index) 라이브러리를 참조 하십시오.
