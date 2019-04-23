---
title: Hyper-v 기술 개요
description: Hyper-v가 무엇 인지 설명, 주요 기능 및 일반적으로 사용 하는 방법입니다.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ac069fed-7bf5-4cc3-aff5-25a2766040b8
author: KBDAzure
ms.author: kathydav
ms.date: 11/29/2016
ms.openlocfilehash: 9ae3c9dce36ad7d67a19ce167c9cb875b3c91810
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59864314"
---
# <a name="hyper-v-technology-overview"></a>Hyper-v 기술 개요

>적용 대상: Windows Server 2016, Microsoft Hyper-V Server 2016, Windows Server 2019, Microsoft Hyper-V Server 2019

Hyper-v는 Microsoft의 하드웨어 가상화 제품입니다. 만들고 라고 하는 컴퓨터의 소프트웨어 버전을 실행할 수 있습니다는 *가상 머신*합니다. 각 가상 머신에 운영 체제 및 프로그램을 실행 하는 전체 컴퓨터 처럼 작동 합니다. 컴퓨팅 리소스를 해야 하는 경우 virtual machines 하면 보다 유연성, 시간과 비용을 절약 있으며 실제 하드웨어에서 실행 한 운영 체제 보다 하드웨어를 사용 하는 더욱 효율적인 방법입니다.

Hyper-v는 동시에 동일한 하드웨어에서 하나 이상의 가상 컴퓨터를 실행할 수 있습니다 즉 자체 격리 된 공간에서 각 가상 컴퓨터를 실행 합니다. 다른 워크 로드에 영향을 주는 충돌 같은 문제를 방지 하려면 또는 다른 시스템에 다른 사용자, 그룹 또는 서비스 액세스할 수 있도록이 작업을 수행 하는 것이 좋습니다.

## <a name="some-ways-hyper-v-can-help-you"></a>일부의 Hyper-v 도움이 될 수 있습니다.

Hyper-v가 도움이 될 수 있습니다.

- **설정 하거나 사설 클라우드 환경을 확장 하 고 있습니다.** 이동 하거나 공유 리소스의 사용을 확장 하 여 더욱 유연 하 고 주문형 IT 서비스를 제공 하 고 수요가 바뀜에 따라 사용률을 조정 합니다.

- **하드웨어를 보다 효과적으로 사용 합니다.** 서버와 적은 전력, 물리적 공간을 사용 하려면 물리적 컴퓨터를 더 적은 수의 더 강력한 워크 로드를 통합 합니다.

- **비즈니스 연속성을 향상 합니다.** 워크 로드의 예약 된 백업과 예약 되지 않은 가동 중지의 영향을 최소화 합니다.

- **설정 하거나 가상 데스크톱 인프라 (VDI)를 확장 합니다.** VDI 사용 하 여 중앙 집중식된 데스크톱 전략을 사용 하 여 비즈니스 민첩성을 늘리고 데이터 보안 및 규정 준수를 간소화할 뿐 데스크톱 운영 체제 및 응용 프로그램을 관리 하면 도움이 됩니다. 개인용 가상 데스크톱 또는 가상 데스크톱 풀 사용할 수 있도록 사용자에 게 동일한 서버에 Hyper-v 및 원격 데스크톱 가상화 호스트 (RD 가상화 호스트)를 배포 합니다.

- **개발 작업을 수행 하 고 더 효율적으로 테스트 합니다.** 구입 또는 실제 시스템에만 사용 해야 하는 모든 하드웨어를 유지 관리 하지 않고도 다양 한 컴퓨팅 환경을 재현 합니다.

## <a name="hyper-v-and-other-virtualization-products"></a>Hyper-v 및 기타 가상화 제품

Windows 및 Windows Server의 Hyper-v는 Microsoft Virtual PC, Microsoft Virtual Server 및 Windows Virtual PC와 같은 이전 하드웨어 가상화 제품을 대체합니다. Hyper-v는 이러한 이전 제품에서 사용할 수 없는 네트워킹, 성능, 저장소 및 보안 기능을 제공합니다.

Hyper-v와 동일한 프로세서 기능을 필요로 하는 대부분의 타사 가상화 응용 프로그램에는 호환 되지 않습니다. 하드웨어 가상화 확장 이라고 하는 프로세서 기능을 공유 하지 하도록 설계 되었습니다. 자세한 내용은 참조 하세요 [virtualization Hyper-v, Device Guard 및 Credential Guard 함께 작동 하지 않습니다](https://support.microsoft.com/kb/3204980)합니다.

## <a name="what-features-does-hyper-v-have"></a>Hyper-v에는 기능에 있습니까?

Hyper-v는 다양 한 기능을 제공합니다. 기능 제공 하거나 수행할 수 있도록 그룹화 하는 개요입니다.

**컴퓨팅 환경** -는 Hyper-v 가상 컴퓨터 메모리, 프로세서, storage, 네트워킹 등의 물리적 컴퓨터와 동일한 기본 부분이 포함 됩니다. 이러한 모든 부분에 기능 있고 다른 요구 사항에 맞게 다른 방법으로 구성할 수 있는 옵션입니다. 저장소 및 네트워킹 각 간주할 수는 고유한 범주, 여러 가지 방법으로 인해 구성할 수 있습니다.

**재해 복구 및 백업을** -Hyper-v 복제본 재해 복구에 대 한 복사본에서 가상 컴퓨터를 복원할 수 있도록 다른 물리적 위치에 저장 하는 데 가상 머신의 복사본을 만듭니다. 백업의 경우 Hyper-v는 두 가지 종류를 제공합니다. 저장 된 상태를 사용 하 여 하나 및 VSS를 지원 하는 프로그램에 대 한 응용 프로그램 일치 백업의 내릴 수 있도록 볼륨 섀도 복사본 서비스 (VSS)을 사용 하 여 다른

**최적화** -각 지원 되는 게스트 운영 체제 서비스 및 드라이버와 호출의 사용자 지정 된 집합이 *integration services*, Hyper-v 가상 컴퓨터에서 운영 체제를 사용 하기 쉽게 만들어 주는 합니다.

**이식성** -같은 기능 실시간 저장소 마이그레이션, 마이그레이션 및 가져오기/내보내기 쉽게 이동 하거나 가상 컴퓨터를 배포 합니다.

**원격 연결** -Hyper-v 가상 머신을 연결, Windows 및 Linux 둘 다 사용에 대 한 원격 연결 도구를 포함 합니다. 원격 데스크톱 액세스를 콘솔이 도구에서는 달리 그래서에서 발생 하는 게스트 운영 체제가 아직 부팅 되지 않습니다 하는 경우에 합니다.

**보안** -보안 부팅 및 차폐 가상 컴퓨터 맬웨어 및 가상 컴퓨터 및 해당 데이터에 대 한 다른 무단된 액세스 로부터 보호할 수 있습니다.

이 버전에 도입 된 기능의 요약을 참조 하세요 [Windows Server에서 Hyper-v의 새로운 기능](What-s-new-in-Hyper-V-on-Windows.md)합니다. 일부 기능이 나 부분에는 구성할 수 있습니다 제한이 있습니다. 자세한 내용은 참조 하세요 [Windows Server 2016의 Hyper-v 확장성에 대 한 계획](plan/Plan-for-Hyper-V-scalability-in-Windows-Server-2016.md)합니다.

## <a name="how-to-get-hyper-v"></a>Hyper-v를 가져오는 방법

X64에 대 한 사용 가능한 서버 역할로 Hyper-v는 Windows Server 및 Windows를 사용할 수 있는 Windows Server의 버전입니다. 서버 지침은 [Windows 서버에 Hyper-v 역할 설치](get-started/Install-the-Hyper-V-role-on-Windows-Server.md)합니다. Windows,이 제품은 [기능](https://docs.microsoft.com/virtualization/hyper-v-on-windows/index) 일부 64 비트 버전의 Windows에서. 를 다운로드할 수 있는 독립 실행형 서버 제품에 사용할 수 있는 이기도 [Microsoft Hyper-v Server](https://www.microsoft.com/evalcenter/evaluate-hyper-v-server-2019)합니다.

## <a name="supported-operating-systems"></a>지원되는 운영 체제

대부분의 운영 체제는 가상 머신에서 실행 됩니다. 일반적으로 운영 체제를 사용 하는 x86 아키텍처 Hyper-v 가상 머신에서 실행 됩니다. 하지만 실행할 수 있는 모든 운영 체제 테스트 되며 Microsoft에서 지원 됩니다. 지원 되는 기능 목록을 참조 하세요.

- [Windows의 Hyper-v에 대 한 지원 되는 Linux 및 FreeBSD 가상 컴퓨터](Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md)

- [Windows Server에서 Hyper-v에 대 한 지원 되는 Windows 게스트 운영 체제](Supported-Windows-guest-operating-systems-for-Hyper-V-on-Windows.md)

## <a name="how-hyper-v-works"></a>Hyper-v의 작동 원리

Hyper-v는 하이퍼바이저 기반 가상화 기술입니다. Hyper-v는 특정 기능을 사용 하 여 실제 프로세서를 해야 하는 Windows 하이퍼바이저를 사용 합니다. 하드웨어 정보를 참조 하세요 [Windows Server에서 Hyper-v에 대 한 시스템 요구 사항](System-requirements-for-Hyper-V-on-Windows.md)합니다.

대부분의 경우 하이퍼바이저는 하드웨어 및 가상 컴퓨터 간의 상호 작용을 관리합니다. 가상 컴퓨터를 실행 하는 격리 된 환경을 제공 하는 하드웨어에이 하이퍼바이저 제어 됩니다. 일부 구성에서는 가상 컴퓨터 또는 가상 머신에서 실행 중인 운영 체제에 그래픽, 네트워킹 또는 저장소 하드웨어에 직접 액세스할 수 있습니다.

## <a name="what-does-hyper-v-consist-of"></a>Hyper-v의 이루어진

Hyper-v가 필요한 만들고 virtual machines를 실행할 수 있도록 함께 작동 하는 부분입니다. 함께 이러한 파트는 가상화 플랫폼을 호출 됩니다. 설치 된 집합으로 Hyper-v 역할을 설치 합니다. 필수 요소는 Windows 하이퍼바이저, Hyper-v 가상 컴퓨터 관리 서비스, 가상화 WMI 공급자, 가상 머신 버스 (VMbus), 가상화 서비스 공급자 (/VID) 및 가상 인프라 드라이버 (VID).

Hyper-v에는 다음과 같은 관리 및 연결을 위한 도구가 있습니다. Hyper-v 역할이 설치 되어 있는지 및 컴퓨터에 Hyper-v 역할이 설치 하지 않고 동일한 컴퓨터에 설치할 수 있습니다. 이러한 도구는:

- Hyper-V 관리자
- [Windows PowerShell 용 Hyper-v 모듈](https://docs.microsoft.com/powershell/module/hyper-v/index)
- [가상 컴퓨터 연결](https://docs.microsoft.com/windows-server/virtualization/hyper-v/learn-more/hyper-v-virtual-machine-connect) \(VMConnect 라고도 함\)
- [Windows PowerShell Direct](manage/Manage-Windows-virtual-machines-with-PowerShell-Direct.md)

## <a name="related-technologies"></a>관련 기술

이 Microsoft에서 HYPER-V를 사용 하 여 자주 사용 되는 일부 기술

- [장애 조치 클러스터링](../../failover-clustering/whats-new-in-failover-clustering.md)
- [원격 데스크톱 서비스](../../remote/remote-desktop-services/Host-desktops-and-apps-in-Remote-Desktop-Services.md)
- [System Center Virtual Machine Manager](https://docs.microsoft.com/system-center/vmm/overview)

다양 한 저장소 기술: 저장소 공간 다이렉트 클러스터 공유 볼륨, SMB 3.0

Windows 컨테이너는 다른 방법 가상화를 제공합니다. 참조 된 [Windows 컨테이너](https://docs.microsoft.com/virtualization/windowscontainers/index) MSDN의 라이브러리입니다.
