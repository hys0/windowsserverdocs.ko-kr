---
title: VDI(가상 데스크톱 인프라) 역할을 위한 Windows 10 버전 1909 최적화
description: VDI 이미지로 사용되는 Windows 10 버전 1909 데스크톱의 오버헤드를 최소화하는 데 추천되는 설정과 구성입니다.
ms.prod: windows-server
ms.reviewer: robsmi
ms.technology: remote-desktop-services
ms.author: helohr
ms.topic: article
author: heidilohr
manager: lizross
ms.date: 02/19/2020
ms.openlocfilehash: 44aa465773674625fa392a644ffb188140138bde
ms.sourcegitcommit: 1c75e4b3f5895f9fa33efffd06822dca301d4835
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/20/2020
ms.locfileid: "77519598"
---
# <a name="optimizing-windows-10-version-1909-for-a-virtual-desktop-infrastructure-vdi-role"></a>VDI(가상 데스크톱 인프라) 역할을 위한 Windows 10 버전 1909 최적화

이 문서는 VDI(가상화된 데스크톱 인프라) 환경에서 최상의 성능을 달성해야 하는 Windows 10 버전 1909(빌드 18363)에 대한 설정을 선택하는 데 도움이 됩니다. 이 가이드의 모든 설정은 고려해야 할 추천 사항이므로 반드시 필요한 것은 아닙니다.

VDI 환경에서 Windows 10 성능을 최적화하는 주요 방법은 앱 그래픽 다시 그리기를 최소화하고, VDI 환경에 중요한 이점을 제공하지 않는 활동을 백그라운드 방식으로 처리하며, 일반적으로 실행되는 프로세스를 최소한으로 줄이는 것입니다. 부수적인 목표는 기본 이미지의 디스크 공간 사용량 최소로 줄이는 것입니다. VDI 구현을 사용할 경우 가능한 가장 작은 기반 또는 "골드" 이미지 크기가 하이퍼바이저의 메모리 사용량을 약간 줄일 뿐만 아니라 소비자에게 데스크톱 이미지를 제공하는 데 필요한 전체 네트워크 작업도 약간 줄일 수 있습니다.

> [!NOTE]
> 이러한 추천 설정은 물리적 또는 다른 가상 머신의 설정을 포함하여 다른 Windows 10 1909 설치에 적용할 수 있습니다. 이 문서의 추천 사항은 Windows 10 1909의 지원 가능성에 영향을 주지 않습니다.

## <a name="vdi-optimization-principles"></a>VDI 최적화 원칙

VDI 환경은 애플리케이션을 포함하는 전체 데스크톱 세션을 네트워크를 통해 컴퓨터 사용자에게 표시합니다. 네트워크 전송 수단은 온-프레미스 네트워크이거나 인터넷일 수 있습니다. VDI 환경은 나중에 사용자에게 제공되는 데스크톱의 기반이 되는 "기본" 운영 체제 이미지입니다. "영구", "비영구" 및 "데스크톱 세션"과 같은 VDI 구현의 변형이 있습니다. 영구 유형은 VDI 데스크톱 OS에 대해 한 세션에서 다음 세션으로 수행된 변경 내용을 유지합니다. 비영구 유형은 VDI 데스크톱 OS에 대해 한 세션에서 다음 세션으로 수행된 변경 내용을 유지하지 않습니다. 사용자 쪽에서 이 데스크톱은 네트워크를 통해 액세스하는 것 외에 다른 가상 또는 물리적 디바이스와 크게 다르지 않습니다.

최적화 설정은 참조 디바이스에서 수행됩니다. VM은 상태를 저장하고 검사점을 만들며 백업을 수행할 수 있으므로 이미지를 빌드하는 데 적합합니다. 기본 OS 설치는 기본 VM에서 수행됩니다. 그런 다음, 불필요한 앱을 제거하고, Windows 업데이트와 다른 업데이트를 설치하고, 임시 파일을 삭제하고, 설정을 적용하여 기본 VM을 최적화합니다.

RDS(원격 데스크톱 세션) 및 최근에 릴리스된 [Windows Virtual Desktop](https://azure.microsoft.com/services/virtual-desktop/)과 같은 다른 유형의 VDI가 있습니다. 이러한 기술에 대한 자세한 설명은 이 문서에서 다루지 않습니다. 이 문서에서는 호스트 최적화와 같은 환경의 다른 요소를 참조하지 않고 Windows 기본 이미지 설정에 대해 집중적으로 설명합니다.

보안과 안정성은 제품 및 서비스와 관련하여 Microsoft의 최우선 순위입니다. 기업 고객은 인터넷을 사용하는지 여부와 관계없이 효율적으로 작동하는 서비스 제품군인 기본 제공 Windows 보안을 활용할 수 있습니다. 인터넷에 연결되지 않은 VDI 환경의 경우 Microsoft에서 하루에 여러 개의 서명 업데이트를 릴리스할 수 있으므로 보안 서명을 하루에 여러 번 다운로드할 수 있습니다. 그런 다음, 이러한 서명을 VDI VM에 제공하고, 영구 또는 비영구 유형에 관계없이 프로덕션 중에 설치되도록 예약할 수 있습니다. 이렇게 하면 VM 보호가 가능한 한 최신 상태로 유지됩니다.

인터넷에 연결되지 않아 클라우드 지원 보안에 참여할 수 없는 VDI 환경에는 적용되지 않는 일부 보안 설정이 있습니다. 클라우드 환경, Windows 스토어 등과 같은 "일반" Windows 디바이스에서 활용할 수 있는 다른 설정이 있습니다. 사용되지 않는 기능에 대한 액세스를 제거하면 공간, 네트워크 대역폭 및 공격 표면이 줄어듭니다.

업데이트와 관련하여 Windows 10은 매월 업데이트 알고리즘을 사용하므로 클라이언트에서 업데이트를 시도할 필요가 없습니다. 대부분의 경우 VDI 관리자는 "마스터" 또는 "골드" 이미지를 기반으로 하여 VM을 종료하고, 읽기 전용인 이미지의 봉인을 해제하고, 이미지를 패치한 다음, 다시 봉인하여 프로덕션 상태로 전환하는 과정을 통해 업데이트 프로세스를 제어합니다. 따라서 VDI VM에서 Windows 업데이트를 확인할 필요가 없습니다. 예를 들어 영구 VDI VM과 같은 특정 경우에는 일반적인 패치 적용 절차가 수행됩니다. Windows 업데이트 또는 Microsoft Intune을 사용할 수도 있습니다. System Center Configuration Manager를 사용하여 업데이트 및 기타 패키지 전송을 처리할 수 있습니다. VDI를 업데이트하는 가장 좋은 방법은 각 조직에서 결정합니다.

> [!TIP]  
> 이 항목에서 설명된 최적화를 구현하는 스크립트 뿐만 아니라 **LGPO.exe**를 사용하여 가져올 수 있는 GPO 내보내기 파일은 GitHub의 [TheVDIGuys](https://github.com/TheVDIGuys)에서 사용할 수 있습니다.

이 스크립트는 사용자 환경과 요구 사항에 맞게 설계되었습니다. 주 코드는 PowerShell이며, LGPO(로컬 그룹 정책 개체) 도구 내보내기 파일과 함께 입력 파일(일반 텍스트)을 사용하여 작업을 수행합니다. 이러한 파일에는 제거할 앱 및 사용하지 않도록 설정할 서비스의 목록이 포함되어 있습니다. 특정 앱을 제거하거나 특정 서비스를 사용하지 않도록 설정하려면 해당 텍스트 파일을 편집하고 항목을 제거합니다. 마지막으로, 디바이스로 가져올 수 있는 로컬 정책 설정이 있습니다. 일부 설정은 다음에 다시 시작하거나 구성 요소를 처음 사용할 때 효과적이므로 그룹 정책을 통해 일부 설정을 적용하는 것보다 기본 이미지 내에서 일부 설정을 사용하는 것이 좋습니다.

### <a name="persistent-vdi"></a>영구적 VDI

영구 VDI는 기본 수준에서 다시 부팅할 때마다 운영 체제 상태를 저장하는 VM입니다. VDI 솔루션의 다른 소프트웨어 계층은 종종 Single Sign-On 솔루션을 사용하여 사용자가 할당된 VM에 쉽고 원활하게 액세스할 수 있도록 합니다.

영구적 VDI는 다음과 같이 다양하게 구현됩니다.

- 기존 가상 머신(자체 가상 디스크 파일이 있고, 정상적으로 시작되고, 한 세션에서 다음 세션으로 변경 내용을 저장하는 VM). 차이점은 사용자가 이 VM에 액세스하는 방법입니다. 사용자가 로그인하며, 하나 이상의 할당된 VDI VM으로 사용자를 자동으로 보내는 웹 포털이 있을 수 있습니다.

- 이미지 기반 영구 가상 머신(필요에 따라 개인 가상 디스크 포함). 이 유형의 구현에는 하나 이상의 호스트 서버에 기본/골드 이미지가 있습니다. VM이 만들어지고 하나 이상의 가상 디스크가 만들어진 후 영구적 스토리지를 위해 이 디스크에 할당됩니다.

    - VM이 시작되면 기본 이미지의 복사본을 해당 VM의 메모리로 읽어들입니다. 이와 동시에 영구 가상 디스크가 해당 VM에 할당되며, 이전 운영 체제 변경 내용이 복잡한 프로세스를 통해 병합됩니다.

    - 이벤트 로그 쓰기, 로그 쓰기 등의 변경 내용은 해당 VM에 할당된 읽기/쓰기 가상 디스크에 리디렉션됩니다.

    - 이 경우 운영 체제 및 앱 서비스는 기존 서비스 소프트웨어(예: Windows Server Update Services ) 또는 기타 관리 기술을 사용하여 정상적으로 작동할 수 있습니다.

    - 영구 VDI 머신과 "정상" 가상 머신의 차이점은 마스터/골드 이미지와의 관계입니다. 업데이트는 특정 시점에 마스터에 적용되어야 합니다. 여기서는 구현에서 사용자의 영구 변경 내용을 처리하는 방법을 결정합니다. 경우에 따라 변경 내용이 있는 디스크가 삭제되거나 다시 설정되며, 이에 따라 새 검사점이 설정됩니다. 또한 사용자가 변경한 내용은 월별 품질 업데이트를 통해 유지되고, 기능 업데이트에 따라 기본 사항이 다시 설정될 수도 있습니다.

### <a name="non-persistent-vdi"></a>비영구적 VDI

비영구적 VDI 구현이 기본 또는 "골드" 이미지를 기준으로 할 경우 최적화가 주로 기본 이미지에서 수행된 후 로컬 설정 및 로컬 정책을 통해 수행됩니다.

이미지 기반 비영구적 VDI를 사용하여 기본 이미지는 읽기 전용입니다. 비영구 VM이 시작되면 기본 이미지의 복사본이 VM으로 스트림됩니다. 시작하는 동안, 그리고 다음 재부팅 이후까지 발생하는 활동은 임시 위치로 리디렉션됩니다. 일반적으로 사용자는 자신의 데이터를 저장할 네트워크 위치를 제공받습니다. 사용자의 프로필이 표준 VM과 병합되어 사용자에게 설정을 제공하는 경우도 있습니다.

단일 이미지를 기반으로 하는 비영구 VDI의 중요한 한 가지 측면은 서비스입니다. 운영 체제 및 구성 요소에 대한 업데이트는 일반적으로 매월 한 번 제공됩니다. 이미지 기반 VDI를 사용하는 경우 다음과 같이 이미지를 업데이트하기 위해 수행해야 하는 일단의 프로세스가 있습니다.

- 지정된 호스트에서는 기본 이미지에서 파생된 모든 VM을 종료하거나 해제해야 합니다. 즉, 사용자는 다른 VM으로 리디렉션됩니다.

- 그런 다음, 기본 이미지가 열린 후 시작됩니다. 다음으로 운영 체제 업데이트, .NET 업데이트, 앱 업데이트 등과 같은 모든 유지 관리 작업이 수행됩니다.

- 이때 적용해야 하는 모든 새 설정이 적용됩니다.

- 또한 이때 다른 모든 유지 관리가 수행됩니다.

- 그런 후 기본 이미지가 종료됩니다.

- 기본 이미지가 봉인된 후 프로덕션으로 되돌아가도록 설정됩니다.

- 사용자가 다시 로그온할 수 있습니다.

> [!NOTE]
> Windows 10에서는 일단의 유지 관리 작업을 정기적으로 자동으로 수행합니다. 기본적으로 매일 오전 3시에 실행되도록 설정된 예약된 작업이 있습니다. 이 예약된 작업은 Windows 업데이트 정리를 비롯한 작업 목록을 수행합니다. 다음 PowerShell 명령을 사용하여 자동으로 수행되는 유지 관리의 모든 범주를 볼 수 있습니다.
>
>```powershell
>Get-ScheduledTask | ? {$_.Settings.MaintenanceSettings}
>```
>

비영구적 VDI의 해결 과제 중 하나는 사용자가 로그오프할 때 거의 모든 운영 체제 활동이 삭제된다는 것입니다. 사용자의 프로필 및/또는 상태는 중앙 위치에 저장될 수 있지만, 가상 머신 자체에서는 마지막 부팅 이후에 수행된 거의 모든 변경 내용을 삭제합니다. 따라서 세션이 바뀔 때 상태를 저장하는 Windows 컴퓨터를 위한 최적화가 적용되지 않습니다.

VDI VM의 아키텍처에 따라, PreFetch 및 SuperFetch와 같은 기능은 VM이 다시 시작될 때 최적화가 삭제되므로 세션이 바뀔 때 도움이 되지 않습니다. 인덱싱도 기존 조각 모음과 같은 디스크 최적화의 마찬가지로 리소스를 부분적으로 낭비할 수 있습니다.

> [!NOTE]
> 가상화를 사용하여 이미지를 준비하는 경우 및 이미지를 만드는 과정에서 인터넷에 연결되는 경우 처음 로그온 할 때 **설정**, **Windows 업데이트**로 차례로 이동하여 기능 업데이트를 연기해야 합니다.

### <a name="to-sysprep-or-not-sysprep"></a>Sysprep 사용 또는 Sysprep 사용 안 함

Windows 10에는 [시스템 준비 도구](https://docs.microsoft.com/windows-hardware/manufacture/desktop/sysprep--system-preparation--overview)(종종 "Sysprep"으로 약칭)라는 기본 제공 기능이 있습니다. Sysprep 도구는 이중화를 위해 사용자 지정된 Windows 10 이미지를 준비하는 데 사용합니다. Sysprep 프로세스는 결과 운영 체제가 프로덕션에서 실행될 수 있게 적절히 고유하게 유지합니다.

Sysprep을 실행하는 경우와 그렇지 않은 경우는 이유가 있습니다. VDI의 경우 이 이미지를 사용하여 로그온하는 후속 사용자를 위한 프로필 템플릿으로 사용할 수 있게 기본 사용자 프로필을 사용자 지정하는 기능을 원할 수도 있습니다. 앱별 설정을 제어할 수 있는 앱을 설치하려고 할 수 있습니다.

대신, 표준 .ISO를 사용하여 설치할 수 있고, 무인 설치 응답 파일을 사용할 수도 있고, 작업 순서를 사용하여 애플리케이션을 설치하거나 애플리케이션을 제거할 수도 있습니다. 작업 순서에서 [LGPO(로컬 그룹 정책 개체) 유틸리티](https://docs.microsoft.com/archive/blogs/secguide/lgpo-exe-local-group-policy-object-utility-v1-0) 도구를 사용하여 이미지에서 로컬 정책 설정을 지정할 수도 있습니다.

### <a name="supportability"></a>지원 가능성

Windows 기본값이 변경될 때마다 지원 가능성에 대한 질문이 발생합니다. VDI 이미지(VM 또는 세션)가 사용자 지정되면 변경 로그에서 이미지에 대한 모든 변경 내용을 추적해야 합니다. 문제를 해결할 때 풀에서 이미지를 격리하고 문제 분석을 위해 구성할 수 있는 경우가 많습니다. 근본 원인에 따라 문제가 추적되면 먼저 해당 변경 내용을 테스트 환경에 롤아웃하고, 궁극적으로 프로덕션 워크로드에 롤아웃할 수 있습니다.

이 문서는 보안에 영향을 주는 시스템 서비스, 정책 또는 작업에 액세스하지 못하도록 의도적으로 방지합니다. 그 후에 Windows 서비스가 제공됩니다. 유지 관리 기간은 *보안 소프트웨어 업데이트를 제외*하고 VDI 환경에서 대부분의 서비스 이벤트가 발생하는 경우이므로 유지 관리 기간 이외의 VDI 이미지를 서비스하는 기능은 제거됩니다. Microsoft는 VDI 환경의 Windows 보안에 대한 지침을 게시했습니다. 자세한 내용은 [VDI(가상 데스크톱 인프라) 환경의 Windows Defender 바이러스 백신 배포 가이드](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-antivirus/deployment-vdi-windows-defender-antivirus)를 참조하세요.

기본 Windows 설정을 변경하는 경우 지원 가능성을 고려합니다. 시스템 서비스, 정책 또는 예약된 작업을 보안 강화, "조명" 등의 이름으로 변경할 때 어려운 문제가 발생할 수 있습니다. 변경된 기본 설정과 관련하여 현재 알려진 문제에 대해서는 Microsoft 기술 자료를 참조합니다. 이 문서의 지침 및 GitHub의 관련 스크립트는 알려진 문제(발생하는 경우)와 관련하여 유지 관리됩니다. 또한 문제는 여러 가지 방법으로 Microsoft에 보고할 수 있습니다.

""시작 값"이 site:support.microsoft.com"인 용어를 사용하여 즐겨찾는 검색 엔진을 통해 서비스의 기본 시작 값과 관련된 알려진 문제를 제기할 수 있습니다.

이 문서 및 GitHub의 관련 스크립트는 기본 권한을 수정하지 않을 수 있습니다. 보안 설정을 늘리려면 **AaronLocker**라는 프로젝트를 시작합니다. 자세한 내용은 [알림: "AaronLocker"를 사용하여 허용 목록에 애플리케이션 지정](https://docs.microsoft.com/archive/blogs/aaron_margosis/announcing-application-whitelisting-with-aaronlocker)을 참조하세요.

#### <a name="vdi-optimization-categories"></a>VDI 최적화 범주

- 글로벌 운영 체제 설정 범주:

    - UWP 앱 정리

    - 선택적 기능 정리

    - 로컬 정책 설정

    - 시스템 서비스

    - 예약형 작업

    - Windows(및 기타) 업데이트 적용

    - 자동 Windows 추적

    - 이미지 종료(봉인) 전 디스크 정리

    - 사용자 설정

    - 하이퍼바이저/호스트 설정

### <a name="universal-windows-platform-uwp-application-cleanup"></a>UWP(유니버설 Windows 플랫폼) 애플리케이션 정리

VDI 이미지의 목표 중 하나는 가능한 한 간소하게 유지하는 것입니다. 이미지의 크기를 줄이는 한 가지 방법은 작업 환경에서 사용되지 않는 UWP 애플리케이션을 제거하는 것입니다. UWP 앱을 사용할 경우 페이로드라고도 하는 기본 애플리케이션 파일이 있습니다. 애플리케이션별 설정의 각 사용자 프로필에 소량의 데이터가 저장되어 있습니다. '모든 사용자'의 프로필에도 작은 양의 데이터가 있습니다.

연결 및 타이밍은 UWP 앱 정리와 관련하여 중요한 요소입니다. 기본 이미지를 네트워크에 연결되지 않은 디바이스에 배포하는 경우 Windows 10에서 Microsoft Store에 연결하여 앱을 다운로드하고 앱을 제거하려고 하는 동시에 해당 앱을 설치할 수 없습니다. 이는 이미지를 사용자 지정한 다음, 이미지 만들기 프로세스의 이후 단계에 남아 있는 항목을 업데이트하는 데 적합한 전략일 수 있습니다.

설치하기 전에 Windows 10을 설치하는데 사용하는 기본 .WIM을 수정하고 .WIM에서 불필요한 UWP 앱을 제거하는 경우 앱이 설치되지 않아 프로필을 만드는 시간이 단축됩니다. 이 섹션의 뒷부분에는 설치 .WIM 파일에서 UWP 앱을 제거하는 방법에 대한 정보가 나와 있습니다.

VDI에 적절한 전략은 원하는 앱을 기본 이미지에서 프로비저닝한 후 그 이후에 Microsoft Store에 대한 액세스를 제한하거나 차단하는 것입니다. Store 앱이 일반 컴퓨터에서는 백그라운드에서 주기적으로 업데이트됩니다. 다른 업데이트가 적용될 때 유지 관리 기간 동안 UWP 앱을 업데이트할 수 있습니다. 자세한 내용은 [유니버설 Windows 플랫폼 앱](https://docs.citrix.com/citrix-virtual-apps-desktops/manage-deployment/applications-manage/universal-apps.html)을 참조하세요.

#### <a name="delete-the-payload-of-uwp-apps"></a>UWP 앱의 페이로드 삭제

필요하지 않은 UWP 앱은 여전히 파일 시스템에 남아 있으면서 소량의 디스크 공간을 계속 사용합니다. 앞으로 절대 필요하지 않을 앱의 경우, PowerShell 명령을 사용하여 원치 않는 UWP 앱의 페이로드를 기본 이미지에서 제거할 수 있습니다.

사실, 이 섹션 뒷부분에 제공되는 링크를 사용하여 설치 .WIM 파일에서 해당 항목을 제거하는 경우 매우 작은 UWP 앱 목록을 사용해서 처음부터 시작할 수 있습니다.

다음 명령을 실행하여 PowerShell의 이 잘린 출력 예제와 같이 실행 중인 운영 체제에서 프로비저닝된 UWP 앱을 열거합니다.

```powershell

    Get-AppxProvisionedPackage -Online

    DisplayName  : Microsoft.3DBuilder
    Version      : 13.0.10349.0  
    Architecture : neutral
    ResourceId   : \~ 
    PackageName  : Microsoft.3DBuilder_13.0.10349.0_neutral_\~_8wekyb3d8bbwe
    Regions      :
    ...
```

시스템에 프로비저닝된 UWP 앱은 작업 순서의 일부로 운영 체제를 설치하는 동안 또는 나중에 운영 체제를 설치한 후에 제거할 수 있습니다. 이 방법은 이미지를 만들거나 유지 관리하는 전체 프로세스를 모듈 방식으로 진행하므로 선호됩니다. 스크립트를 개발한 후 후속 빌드에서 변경된 항목이 있는 경우 프로세스를 처음부터 반복하지 않고 기존 스크립트를 편집합니다. 이 항목에 대한 정보로 연결되는 링크는 다음과 같습니다.

[작업 순서 도중 Windows 10 기본 제공 앱 제거](https://blogs.technet.microsoft.com/mniehaus/2015/11/11/removing-windows-10-in-box-apps-during-a-task-sequence/)

[Powershell - 버전 1.3을 사용하여 Windows 10 WIM-File에서 기본 제공 앱 제거](https://gallery.technet.microsoft.com/Removing-Built-in-apps-65dc387b)

[Windows 10 1607: 기능 업데이트를 배포하는 경우 앱이 복귀되지 않도록 방지](https://blogs.technet.microsoft.com/mniehaus/2016/08/23/windows-10-1607-keeping-apps-from-coming-back-when-deploying-the-feature-update/)

그런 후 다음과 같이 [Remove-AppxProvisionedPackage](https://docs.microsoft.com/powershell/module/dism/remove-appxprovisionedpackage?view=win10-ps) PowerShell 명령을 실행하여 UWP 앱 페이로드를 제거합니다.

```powershell
Remove-AppxProvisionedPackage -Online -PackageName
```

각 UWP 앱은 각 고유 환경에서 적합한지 평가해야 합니다. Windows 10 버전 1909의 기본 설치를 설치한 다음, 실행되어 메모리를 사용하는 앱을 확인합니다. 예를 들어 자동으로 시작되는 앱 또는 사용자 환경에서 사용하지 않을 수 있는 날씨와 뉴스와 같이 시작 메뉴에 정보를 자동으로 표시하는 앱을 제거하려고 고려할 수 있습니다.

>[!NOTE]
>GitHub의 스크립트를 활용하는 경우 스크립트를 실행하기 전에 제거할 앱을 쉽게 제어할 수 있습니다. 스크립트 파일이 다운로드되면 'Win10_1909_AppxPackages.txt' 파일을 찾고, 해당 파일을 편집하고, 유지하려는 앱(예: 계산기, 스티커 메모 등)의 항목을 제거합니다.

### <a name="manage-windows-optional-features-using-powershell"></a>PowerShell을 사용하여 Windows 선택적 기능 관리

Windows 선택적 기능은 PowerShell을 사용하여 관리할 수 있습니다. 자세한 내용은 [Windows 10: PowerShell을 사용하여 선택적 기능 관리](https://social.technet.microsoft.com/wiki/contents/articles/39386.windows-10-managing-optional-features-with-powershell.aspx)를 참조하세요. 현재 설치된 Windows 기능을 열거하려면 다음 PowerShell 명령을 실행합니다.

```powershell
Get-WindowsOptionalFeature -Online
```

다음 예제와 같이 특정 Windows 선택적 기능을 사용하거나 사용하지 않도록 설정할 수 있습니다.

```powershell
Enable-WindowsOptionalFeature -Online -FeatureName "DirectPlay" -All
```

다음 예제와 같이 VDI 이미지에서 기능을 사용하지 않도록 설정할 수 있습니다.

```powershell
Disable-WindowsOptionalFeature -Online -FeatureName “WindowsMediaPlayer”
```

다음으로, Windows Media Player 패키지를 제거하는 것이 좋습니다. Windows 10 1909에는 두 개의 Windows Media Player 패키지가 있습니다.

```powershell
Get-WindowsPackage -Online -PackageName *media*

PackageName       : Microsoft-Windows-MediaPlayer-Package~31bf3856ad364e35~amd64~~10.0.18362.1
Applicable        : True
Copyright        : Copyright (c) Microsoft Corporation. All Rights Reserved
Company         :
CreationTime       :
Description       : Play audio and video files on your local device and on the Internet.
InstallClient      : DISM Package Manager Provider
InstallPackageName    : Microsoft-Windows-MediaPlayer-Package~31bf3856ad364e35~amd64~~10.0.18362.1.mum
InstallTime       : 3/19/2019 6:20:22 AM
...

Features         : {}

PackageName       : Microsoft-Windows-MediaPlayer-Package~31bf3856ad364e35~amd64~~10.0.18362.449
Applicable        : True
Copyright        : Copyright (c) Microsoft Corporation. All Rights Reserved
Company         :
CreationTime       :
Description       : Play audio and video files on your local device and on the Internet.
InstallClient      : UpdateAgentLCU
InstallPackageName    : Microsoft-Windows-MediaPlayer-Package~31bf3856ad364e35~amd64~~10.0.18362.449.mum
InstallTime       : 10/29/2019 5:15:17 AM
...
```

Windows Media Player 패키지를 제거하려면 다음을 수행합니다(이 경우 약 60MB의 디스크 공간 확보).

```powershell
 Remove-WindowsPackage -PackageName Microsoft-Windows-MediaPlayer-Package~31bf3856ad364e35~amd64~~10.0.18362.1 -Online

 Remove-WindowsPackage -PackageName Microsoft-Windows-MediaPlayer-Package~31bf3856ad364e35~amd64~~10.0.18362.1 -Online
```

#### <a name="enable-or-disable-windows-features-using-dism"></a>DISM을 사용하여 Windows 기능 사용 또는 사용 안 함

기본 제공 Dism.exe 도구를 사용하여 Windows 선택적 기능을 열거하고 제어할 수 있습니다. Dism.exe 스크립트는 운영 체제 설치 작업 순서 중에 개발하고 실행할 수 있습니다. 관련 Windows 기술을 [주문형 기능](https://docs.microsoft.com/windows-hardware/manufacture/desktop/features-on-demand-v2--capabilities)이라고 합니다.

#### <a name="default-user-settings"></a>기본 사용자 설정

'C:\Users\Default\NTUSER.DAT'라는 Windows 레지스트리 파일에 수행할 수 있는 사용자 지정이 있습니다. 이 파일에 지정된 모든 설정은 이 이미지를 실행하는 디바이스에서 만든 모든 후속 사용자 프로필에 적용됩니다. 'Win10_1909_DefaultUserSettings.txt' 파일을 편집하여 기본 사용자 프로필에 적용할 설정을 제어할 수 있습니다. 설정 추천 사항의 이러한 반복에 대한 새 설정을 신중하게 고려해야 하는 한 가지 설정은 **TaskbarSmallIcons**입니다. 이 설정을 구현하려면 먼저 사용자 기반을 확인하는 것이 좋습니다. **TaskbarSmallIcons**는 Windows 작업 표시줄을 더 작게 만들고, 화면 공간을 더 적게 사용하며, 아이콘을 더 작게 만들고, 검색 인터페이스를 최소화하며 다음 그림의 앞뒤에 표시됩니다.

그림 1: 정상적인 Windows 10 버전 1909 작업 표시줄

![Windows 10 버전 1909 작업 표시줄의 표준 버전](media/rds-vdi-recommendations-1909/standard-taskbar.png)

그림 2: 작은 아이콘 설정을 사용하는 작업 표시줄

![작은 아이콘 설정을 사용하는 작업 표시줄](media/rds-vdi-recommendations-1909/taskbar-sm-icons.png)

또한 VDI 인프라를 통한 이미지 전송을 줄이기 위해 기본 배경을 기본 Windows 10 이미지 대신 단색으로 설정할 수 있습니다. 로그온 화면을 단색으로 설정하고, 로그온 시 불투명 흐림 효과를 해제할 수도 있습니다.

다음 설정은 주로 애니메이션을 줄이기 위해 기본 사용자 프로필 레지스트리 하이브에 적용됩니다. 이러한 설정 중 일부 또는 전부를 원하지 않는 경우 이 이미지를 기반으로 하는 새 사용자 프로필에 적용되지 않는 설정을 삭제합니다. 이러한 설정의 목표는 다음과 같은 동일한 설정을 사용하도록 설정하는 것입니다.

그림 3: 최적화된 시스템 속성, 성능 옵션

![최적화된 시스템 속성, 성능 옵션](media/rds-vdi-recommendations-1909/performance-options.png)

다음은 성능을 최적화하기 위해 기본 사용자 프로필 레지스트리 하이브에 적용되는 최적화 설정입니다.

```
Delete HKLM\Temp\SOFTWARE\Microsoft\Windows\CurrentVersion\Run /v OneDriveSetup /f
add "HKLM\Temp\Control Panel\Desktop" /v DragFullWindows /t REG_SZ /d 0 /f
add "HKLM\Temp\Control Panel\Desktop" /v WallPaper /t REG_SZ /d "" /f
add "HKLM\Temp\Control Panel\Desktop\WindowMetrics" /v MinAnimate /t REG_DWORD /d 0 /f
add HKLM\Temp\Software\Microsoft\Windows\DWM /v AccentColor /t REG_DWORD /d 4292311040 /f
add HKLM\Temp\Software\Microsoft\Windows\DWM /v ColorizationColor /t REG_DWORD /d 4292311040 /f
add HKLM\Temp\Software\Microsoft\Windows\DWM /v AlwaysHibernateThumbnails /t REG_DWORD /d 0 /f
add HKLM\Temp\Software\Microsoft\Windows\DWM /v EnableAeroPeek /t REG_DWORD /d 0 /f
add HKLM\Temp\Software\Microsoft\Windows\DWM /v AlwaysHibernateThumbnails /t REG_DWORD /d 0 /f
add HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced /v AutoCheckSelect /t REG_DWORD /d 0 /f
add HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced /v HideIcons /t REG_DWORD /d 0 /f
add HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced /v ListviewAlphaSelect /t REG_DWORD /d 0 /f
add HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced /v ListViewShadow /t REG_DWORD /d 0 /f
add HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced /v ShowInfoTip /t REG_DWORD /d 0 /f
add HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced /v TaskbarAnimations /t REG_DWORD /d 0 /f
add HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced /v TaskbarSmallIcons /t REG_DWORD /d 1 /f
add HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced\People /v PeopleBand /t REG_DWORD /d 0 /f
add HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\Explorer\VisualEffects\AnimateMinMax /v DefaultApplied /t REG_DWORD /d 0 /f
add HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\Explorer\VisualEffects\ComboBoxAnimation /v DefaultApplied /t REG_DWORD /d 0 /f
add HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\Explorer\VisualEffects\ControlAnimations /v DefaultApplied /t REG_DWORD /d 0 /f
add HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\Explorer\VisualEffects\DWMAeroPeekEnabled /v DefaultApplied /t REG_DWORD /d 0 /f
add HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\Explorer\VisualEffects\DWMSaveThumbnailEnabled /v DefaultApplied /t REG_DWORD /d 0 /f
add HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\Explorer\VisualEffects\MenuAnimation /v DefaultApplied /t REG_DWORD /d 0 /f
add HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\Explorer\VisualEffects\SelectionFade /v DefaultApplied /t REG_DWORD /d 0 /f
add HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\Explorer\VisualEffects\TaskbarAnimations /v DefaultApplied /t REG_DWORD /d 0 /f
add HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\Explorer\VisualEffects\TooltipAnimation /v DefaultApplied /t REG_DWORD /d 0 /f
add HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\ContentDeliveryManager /v SubscribedContent-338388Enabled /t REG_DWORD /d 0 /f
add HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\ContentDeliveryManager /v SubscribedContent-338389Enabled /t REG_DWORD /d 0 /f
add HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\ContentDeliveryManager /v SystemPaneSuggestionsEnabled /t REG_DWORD /d 0 /f
```

로컬 정책 설정에서 VDI의 배경에 대한 이미지를 사용하지 않도록 설정할 수 있습니다.  이미지를 원하는 경우 이미지 정보 전송에 사용되는 네트워크 대역폭을 제한하기 위해 사용자 지정 배경 이미지를 축소된 색 농도로 만드는 것이 좋습니다. 정책이 설정되면 사용자가 배경색을 변경할 수 없으므로 로컬 정책에서 배경 이미지를 지정하지 않을 경우 로컬 정책을 설정하기 전에 배경색을 먼저 설정하는 것이 좋습니다. 백그라운드 이미지로 "(null)"을 지정하는 것이 더 좋을 수 있습니다. 다음 섹션에는 원격 데스크톱 프로토콜 세션을 통해 백그라운드를 사용하지 않는 다른 정책 설정이 있습니다.

### <a name="local-policy-settings"></a>로컬 정책 설정

Windows 정책을 사용하여 VDI 환경에서 Windows 10에 대한 많은 최적화를 수행할 수 있습니다. 이 섹션의 표에는 기본/골드 이미지에 로컬로 적용할 수 있는 설정이 나와 있습니다. 그룹 정책과 같은 다른 방법으로 동일한 설정을 지정하지 않으면 이러한 설정이 계속 적용됩니다.

일부 결정은 다음과 같은 환경의 특정 세부 정보를 기반으로 할 수 있습니다.

- VDI 환경에서는 인터넷 액세스가 허용되나요?

- VDI 솔루션은 영구적인가요 아니면 비영구적인가요?

다음 설정은 보안과 관련이 있는 설정과 대항하거나 충돌하지 않도록 선택되었습니다. 이러한 설정은 설정을 제거하거나 VDI 환경에 적용할 수 없는 기능을 사용하지 않도록 설정하기 위해 선택되었습니다.

| 정책 설정 | 항목 | 하위 항목 | 가능한 설정 및 설명|
| -------------- | ---- | -------- | ---------------------------- |
| 로컬 컴퓨터 정책 \\ 컴퓨터 구성 \\ Windows 설정 \\ 보안 설정 | | | |
| 네트워크 목록 관리자 정책 | 모든 네트워크 속성 | 네트워크 위치 | 사용자는 위치를 변경할 수 없습니다. |
| 로컬 컴퓨터 정책 \\ 컴퓨터 구성 \\ 관리 템플릿 \\ 제어판 | | | |
| *제어판 | 온라인 팁 허용 | | 사용 안 함. Microsoft 콘텐츠 서비스에 연결하여 팁 및 도움말 콘텐츠를 검색하지 않습니다. |
| *제어판\개인 설정 | 잠금 화면 표시 안 함 | 사용. 사용자에게 잠금 화면을 표시하는지 여부를 제어합니다. 이 정책 설정을 사용하도록 설정하면 PC를 잠근 후에 로그인하기 전에 Ctrl+Alt+Del을 누를 필요가 없는 사용자에게 선택한 타일이 표시됩니다. |
| *제어판\개인 설정 | 특정 기본 잠금 화면 및 로그온 이미지 적용 | [![잠금 화면의 경로를 설정하는 UI](media/lock-screen-image-settings.png)](media/lock-screen-image-settings.png) | 사용. 이 설정을 사용하면 로그인한 사용자가 없을 때 표시되는 기본 잠금 화면 및 로그온 이미지를 지정할 수 있으며, 지정한 이미지를 모든 사용자의 기본값으로 설정합니다(기본 이미지를 바꿈).<p>이미지가 렌더링될 때마다 네트워크를 통해 전송되는 데이터를 줄이기 위해 복잡하지 않은 저해상도 이미지를 사용하는 것이 좋습니다. |
| *제어판\국가 및 언어 옵션\필기 개인 설정 | 자동 학습 사용 안 함 | | 사용. 이 정책 설정을 사용하도록 설정하면 자동 학습이 중지되고 저장된 데이터가 삭제됩니다. 사용자는 제어판에서 이 설정을 구성할 수 없습니다. |
| 로컬 컴퓨터 정책 \\ 컴퓨터 구성 \\ 관리 템플릿 \\ 네트워크 | | | |
| BITS(Background Intelligent Transfer Service) | BITS 클라이언트에 대해 Windows 분기 캐시 사용 허용 안 함 |  | 사용 |
| BITS(Background Intelligent Transfer Service) | 컴퓨터가 BITS 피어캐싱 클라이언트로 작동할 수 없음 |  | 사용 |
| BITS(Background Intelligent Transfer Service) | 컴퓨터가 BITS 피어캐싱 서버로 작동할 수 없음 |  | 사용 |
| BITS(Background Intelligent Transfer Service) | BITS 피어캐싱 허용 |  | 사용 안 함 |
| BranchCache | BranchCache 켜기 |  | 사용 안 함 |
| *글꼴 | 글꼴 공급자 사용 |  | 사용 안 함. Windows에서 온라인 글꼴 공급자에 연결하지 않고 로컬로 설치된 글꼴만 열거합니다. |
| 핫스팟 인증 | 핫스팟 인증 사용 |  | 사용 안 함 |
| Microsoft 피어-투-피어 네트워킹 서비스 | Microsoft 피어-투-피어 네트워킹 서비스 사용 안 함 |  | 사용 |
| 네트워크 연결 상태 표시기 | 패시브 폴링 지정 | 패시브 폴링 사용 안 함(확인란) | 사용. 격리된 네트워크에 있거나 고정 IP 주소를 사용하는 경우 이 설정을 사용합니다. |
| 오프라인 파일 | 오프라인 파일의 사용을 허용하거나 허용하지 않음 |  | 사용 안 함 |
| TCPIP 설정 \\ IPv6 전환 기술 | Teredo 상태 설정 | 사용 안 함 상태 | 사용. 사용 안 함 상태에서는 Teredo 인터페이스가 호스트에 없습니다. |
| WLAN 서비스 \\ WLAN 설정 | Windows에서 제안된 공개 핫스팟, 연락처와 공유되는 네트워크 및 핫스팟 제공 유료 서비스에 자동으로 연결하도록 합니다. |  | 사용 안 함. **추천된 개방 핫스팟에 연결**, **내 연락처가 공유하는 네트워크에 연결** 및 **유료 서비스 사용**이 해제되어 있지만, 이 디바이스의 사용자는 이러한 설정을 사용하도록 설정할 수 있습니다. |
| 로컬 컴퓨터 정책 \\ 컴퓨터 구성 \\ 관리 템플릿 \\ 시작 메뉴 및 작업 표시줄 |  |  |  |
| *알림 | 알림 네트워크 사용 끄기 |  | 사용. 이 설정을 사용하도록 설정하면 앱 및 시스템 기능에서 WNS 또는 알림 폴링 API를 사용하여 네트워크로부터 알림을 받을 수 없습니다. |
| 로컬 컴퓨터 정책 \\ 컴퓨터 구성 \\ 관리 템플릿 \\ 시스템 |  |  |  |
| 장치 설치 | 디바이스에 일반 드라이버가 설치되어 있는 경우 Windows 오류 보고를 보내지 않음 |  | 사용 |
| 장치 설치 | 새 디바이스 드라이버를 설치할 때 시스템 복원 지점 만들지 않음 |  | 사용 |
| 장치 설치 | 인터넷에서 디바이스 메타데이터 검색 금지 |  | 사용 |
| 장치 설치 | 설치 중 디바이스 드라이버에서 추가 소프트웨어를 요구할 경우 Windows 오류 보고서 보내기 금지 |  | 사용 |
| 장치 설치 | 디바이스 설치 동안 **새 하드웨어 발견 풍선** 끄기 |  | 사용 |
| 파일 시스템 \\ NTFS | 짧은 이름 만들기 옵션 | 모든 볼륨에서 사용 안 함 | 사용 |
| *그룹 정책 | 앱 URL 처리기로 웹과 앱 연결 구성 |  | 사용 안 함. 웹-앱 연결을 해제하고, 연결된 앱을 시작하는 대신 기본 브라우저에서 http(s) URI를 엽니다. |
| *그룹 정책 | 이 디바이스에서 계속 실행 |  | 사용 안 함. Windows 디바이스가 다른 디바이스를 통해 검색될 수 없고, 디바이스 간 환경에 참여할 수 없습니다. |
| 인터넷 통신 관리 \\ 인터넷 통신 설정 | 모든 Windows 업데이트 기능에 대한 액세스 끄기 |  |사용. 이 정책 설정을 사용하도록 설정하면 모든 Windows 업데이트 기능이 제거됩니다. 이렇게 하면 시작 메뉴의 Windows 업데이트 하이퍼링크 및 Internet Explorer의 도구 메뉴에서 https://windowsupdate.microsoft.com 의 Windows 업데이트 웹 사이트에 대한 액세스가 차단됩니다. Windows 자동 업데이트도 사용하지 않도록 설정됩니다. 알림을 받지 못할 뿐만 아니라 Windows 업데이트의 중요 업데이트도 받지 못하게 됩니다. 또한 이 정책 설정을 통해 디바이스 관리자에서 Windows 업데이트 웹 사이트로부터 드라이버 업데이트를 자동으로 설치하지 못하게 됩니다. |
| 인터넷 통신 관리 \\ 인터넷 통신 설정 | 자동 루트 인증서 업데이트 끄기 |  |사용. 이 정책 설정을 사용하도록 설정하면 신뢰할 수 없는 루트 기관에서 발급한 인증서가 제공될 때 컴퓨터에서 Windows 업데이트 웹 사이트에 연결하여 Microsoft에서 해당 CA를 신뢰할 수 있는 기관 목록에 추가했는지 확인하지 않습니다. 참고: 최신 인증서 해지 목록의 대안이 있는 경우에만 이 정책을 사용합니다. |
| 인터넷 통신 관리 \\ 인터넷 통신 설정 | 이벤트 뷰어의 "Events.asp" 링크 사용 안 함 |  | 사용 |
| 인터넷 통신 관리 \\ 인터넷 통신 설정 | 필기 개인 설정의 데이터 공유 끄기 |  | 사용 |
| 인터넷 통신 관리 \\ 인터넷 통신 설정 | 필기 인식 오류 보고 사용 안 함 |  | 사용 |
| 인터넷 통신 관리 \\ 인터넷 통신 설정 | 도움말 및 지원 센터의 "알고 계십니까?" 내용을 표시하지 않음 콘텐츠 |  | 사용 |
| 인터넷 통신 관리 \\ 인터넷 통신 설정 | 도움말 및 지원 센터에서 Microsoft 기술 자료 검색 안 함 |  | 사용 |
| 인터넷 통신 관리 \\ 인터넷 통신 설정 | URL 연결이 Microsoft.com을 참조하는 경우 인터넷 연결 마법사 끄기 |  | 사용 |
| 인터넷 통신 관리 \\ 인터넷 통신 설정 | 웹 게시 및 온라인 주문 마법사의 인터넷 다운로드를 금지 |  | 사용 |
| 인터넷 통신 관리 \\ 인터넷 통신 설정 | 인터넷 파일 연결 서비스 사용 안 함 |  | 사용 |
| 인터넷 통신 관리 \\ 인터넷 통신 설정 | URL이 Microsoft.com으로 연결하는 경우 등록 안 함 |  | 사용 |
| 인터넷 통신 관리 \\ 인터넷 통신 설정 | 사진 작업에서 "인화 주문" 사용 안 함 |  | 사용 |
| 인터넷 통신 관리 \\ 인터넷 통신 설정 | 파일 및 폴더 작업에서 "웹에 게시" 항목을 제거 |  | 사용 |
| 인터넷 통신 관리 \\ 인터넷 통신 설정 | Windows Messenger 사용자 환경 개선 프로그램 사용 안 함 |  | 사용 |
| 인터넷 통신 관리 \\ 인터넷 통신 설정 | Windows 사용자 환경 개선 프로그램 끄기 |  | 사용 |
| 인터넷 통신 관리 \\ 인터넷 통신 설정 | Windows 네트워크 연결 상태 표시기의 활성 테스트 끄기 |  | 사용. 이 정책 설정은 컴퓨터가 인터넷 또는 더 제한적인 네트워크에 연결되어 있는지 확인하기 위해 Windows NCSI(네트워크 연결 상태 표시기)에서 수행하는 활성 테스트를 해제합니다. 연결 수준을 확인하는 작업의 일환으로 NCSI는 두 가지 활성 테스트(전용 웹 서버에서 페이지 다운로드 또는 전용 주소에 대한 DNS 요청) 중 하나를 수행합니다. 이 정책 설정을 사용하도록 설정하면 NCSI는 두 활성 테스트 중 어떤 것도 실행하지 않습니다. 이로 인해 NCSI 및 NCSI를 사용하는 다른 구성 요소가 인터넷 연결을 확인하는 기능이 저하될 수 있습니다.) 참고: 이 기능을 원하는 경우 NCSI 테스트를 내부 리소스로 리디렉션할 수 있도록 하는 다른 정책도 사용할 수 있습니다. |
| 인터넷 통신 관리 \\ 인터넷 통신 설정 | Windows 오류 보고 사용 안 함 |  | 사용 |
| 인터넷 통신 관리 \\ 인터넷 통신 설정 | Windows 업데이트 디바이스 드라이버 검색 안 함 |  | 사용 |
| 로그온 | 첫 번째 로그인 애니메이션 표시 |  | 사용 안 함 |
| 로그온 | 잠금 화면에서 앱 알림 끄기 |  | 사용 |
| 로그온 | Windows 시작 소리 끄기 |  | 사용 |
| 전원 관리 | 현재 전원 관리 옵션 선택 | 고성능 | 사용 |
| 복구 | 기본 상태로 시스템 복원 허용 |  | 사용 안 함 |
| *스토리지 상태 | 디스크 오류 예측 모델에 대한 업데이트를 다운로드하도록 허용 |  | 사용 안 함. 디스크 오류 예측 실패 모델에 대한 업데이트가 다운로드되지 않습니다. |
| *Windows 시간 서비스 \\ 시간 공급자 | Windows NTP 클라이언트 사용 |  | 사용 안 함. 이 정책 설정을 사용하지 않도록 설정하거나 구성하지 않으면 로컬 컴퓨터 시계에서 시간을 NTP 서버와 동기화하지 않습니다. 참고: 이 설정은 매우 신중하게 고려하세요. 도메인에 가입된 Windows 디바이스는 **NT5DS**를 사용해야 합니다. DC-부모 도메인 DC는 NTP를 사용할 수 있습니다. PDCe 역할은 NTP를 사용할 수 있습니다. 가상 머신은 종종 "향상된 기능" 또는 "Integration Services"를 사용합니다. |
| 문제 해결 및 진단 \\ 예약된 유지 관리 | 예약된 유지 관리 동작 구성 |   | 사용 안 함 |
| 문제 해결 및 진단 \\ Windows 부팅 성능 진단 | 시나리오 실행 수준 구성 |   | 사용 안 함 |
| 문제 해결 및 진단 \\ Windows 메모리 누수 진단 | 시나리오 실행 수준 구성 |   | 사용 안 함 |
| 문제 해결 및 진단 \\ Windows 리소스 소모 검색 및 해결 | 시나리오 실행 수준 구성 |   | 사용 안 함 |
| 문제 해결 및 진단 \\ Windows 종료 성능 진단 | 시나리오 실행 수준 구성 |   | 사용 안 함 |
| 문제 해결 및 진단 \\ Windows 다시 시작 성능 진단 | 시나리오 실행 수준 구성 |   | 사용 안 함 |
| 문제 해결 및 진단 \\ Windows 시스템 응답 성능 진단 | 시나리오 실행 수준 구성 |   | 사용 안 함 |
| *사용자 프로필 | 광고 ID 끄기 |   | 사용. 이 정책 설정을 사용하도록 설정하면 광고 ID가 해제됩니다. 앱에서 ID를 앱 간 환경에 사용할 수 없습니다. |
| 로컬 컴퓨터 정책 \\ 컴퓨터 구성 \\ 관리 템플릿 \\ Windows 구성 요소 |  |  |  |
| Windows 10에 기능 추가 | 이 마법사가 실행되지 못하게 합니다. |  | 사용 |
| *앱 개인정보처리방침 | 이 마법사가 실행되지 못하게 합니다. |  | 사용 |
| *앱 개인정보처리방침 | Windows 앱에서 계정 정보에 액세스하도록 허용 | 모든 앱의 기본값: 강제 거부 | 사용. **거부 적용** 옵션을 선택하면 Windows 앱에서 계정 정보에 액세스할 수 없으며 조직의 직원이 이 옵션을 변경할 수 없습니다. |
| *앱 개인정보처리방침 | Windows 앱에서 통화 기록에 액세스하도록 허용 | 모든 앱의 기본값: 강제 거부 | 사용. **거부 적용** 옵션을 선택하면 Windows 앱에서 통화 기록에 액세스할 수 없으며 조직의 직원이 이 옵션을 변경할 수 없습니다. |
| *앱 개인정보처리방침 | Windows 앱에서 연락처에 액세스하도록 허용 | 모든 앱의 기본값: 강제 거부 | 사용. **거부 적용** 옵션을 선택하면 Windows 앱에서 연락처에 액세스할 수 없으며 조직의 직원이 이 옵션을 변경할 수 없습니다. |
| *앱 개인정보처리방침 | Windows 앱이 다른 앱에 대한 진단 정보에 액세스할 수 있도록 허용 | 모든 앱의 기본값: 강제 거부 | 사용. 이 정책 설정을 사용하지 않도록 설정하거나 구성하지 않으면 조직의 직원이 디바이스의 설정 > 개인 정보를 사용하여 Windows 앱에서 다른 앱에 대한 진단 정보를 가져올 수 있는지 여부를 결정할 수 있습니다. |
| *앱 개인정보처리방침 | Windows 앱에서 메일에 액세스하도록 허용 | 모든 앱의 기본값: 강제 거부 | 사용. **허용 적용** 옵션을 선택하면 Windows 앱에서 이메일에 액세스할 수 있으며 조직의 직원이 이 옵션을 변경할 수 없습니다. |
| *앱 개인정보처리방침 | Windows 앱에서 위치에 액세스하도록 허용 | 모든 앱의 기본값: 강제 거부 | 사용. **거부 적용** 옵션을 선택하면 Windows 앱에서 위치에 액세스할 수 없으며 조직의 직원이 이 옵션을 변경할 수 없습니다. |
| *앱 개인정보처리방침 | Windows 앱에서 메시징에 액세스하도록 허용 | 모든 앱의 기본값: 강제 거부 | 사용. **거부 적용** 옵션을 선택하면 Windows 앱에서 메시징에 액세스할 수 없으며 조직의 직원이 이 옵션을 변경할 수 없습니다. |
| *앱 개인정보처리방침 | Windows 앱에서 동작에 액세스하도록 허용 | 모든 앱의 기본값: 강제 거부 | 사용. **거부 적용** 옵션을 선택하면 Windows 앱에서 동작 데이터에 액세스할 수 없으며 조직의 직원이 이 옵션을 변경할 수 없습니다. |
| *앱 개인정보처리방침 | Windows 앱에서 알림에 액세스하도록 허용 | 모든 앱의 기본값: 강제 거부 | 사용. **거부 적용** 옵션을 선택하면 Windows 앱에서 알림에 액세스할 수 없으며 조직의 직원이 이 옵션을 변경할 수 없습니다. |
| *앱 개인정보처리방침 | Windows 앱에서 작업에 액세스하도록 허용 | 모든 앱의 기본값: 강제 거부 | 사용. **거부 적용** 옵션을 선택하면 Windows 앱에서 작업에 액세스할 수 없으며 조직의 직원이 이 옵션을 변경할 수 없습니다. |
| *앱 개인정보처리방침 | Windows 앱에서 일정에 액세스하도록 허용 | 모든 앱의 기본값: 강제 거부 | 사용. **거부 적용** 옵션을 선택하면 Windows 앱에서 일정에 액세스할 수 없으며 조직의 직원이 이 옵션을 변경할 수 없습니다. |
| *앱 개인정보처리방침 | Windows 앱에서 카메라에 액세스하도록 허용 | 모든 앱의 기본값: 강제 거부 | 사용. **거부 적용** 옵션을 선택하면 Windows 앱에서 카메라에 액세스할 수 없으며 조직의 직원이 이 옵션을 변경할 수 없습니다. |
| *앱 개인정보처리방침 | Windows 앱에서 마이크에 액세스하도록 허용 | 모든 앱의 기본값: 강제 거부 | 사용. **거부 적용** 옵션을 선택하면 Windows 앱에서 마이크에 액세스할 수 없으며 조직의 직원이 이 옵션을 변경할 수 없습니다. |
| *앱 개인정보처리방침 | Windows 앱에서 신뢰할 수 있는 디바이스에 액세스하도록 허용 | 모든 앱의 기본값: 강제 거부 | 사용. **거부 적용** 옵션을 선택하면 Windows 앱에서 신뢰할 수 있는 디바이스에 액세스할 수 없으며 조직의 직원이 이 옵션을 변경할 수 없습니다. |
| *앱 개인정보처리방침 | Windows 앱에서 페어링되지 않은 디바이스와 통신하도록 허용 | 모든 앱의 기본값: 강제 거부 | 사용. **거부 적용** 옵션을 선택하면 Windows 앱에서 페어링되지 않은 무선 디바이스와 통신할 수 없으며 조직의 직원이 이 옵션을 변경할 수 없습니다. |
| *앱 개인정보처리방침 | Windows 앱에서 무선 송수신 장치에 액세스하도록 허용 | 모든 앱의 기본값: 강제 거부 | 사용. **거부 적용** 옵션을 선택하면 Windows 앱에서 라디오를 제어할 수 없으며 조직의 직원이 이 옵션을 변경할 수 없습니다. |
| *앱 개인정보처리방침 | Windows 앱에서 전화를 걸도록 허용 | 모든 앱의 기본값: 강제 거부 | 사용. **거부 적용** 옵션을 선택하면 Windows 앱에서 전화를 걸 수 없으며 조직의 직원이 이 옵션을 변경할 수 없습니다. |
| *앱 개인정보처리방침 | Windows 앱을 백그라운드에서 실행할 수 있도록 허용 | 모든 앱의 기본값: 강제 거부 | 사용. **거부 적용** 옵션을 선택하면 Windows 앱이 백그라운드에서 실행될 수 없으며 조직의 직원이 이 옵션을 변경할 수 없습니다. |
| 자동 실행 정책 | Set the default behavior for AutoRun(자동 실행의 기본 동작 설정) | 자동 실행 명령을 실행하지 않음 | 사용 |
| *자동 실행 정책 | 자동 실행 끄기 |   | 사용. 이 정책 설정을 사용하도록 설정하면 CD-ROM 및 이동식 미디어 드라이브에서 자동 실행을 사용하지 않도록 설정되거나 모든 드라이브에서 이를 사용하지 않도록 설정됩니다. |
| *클라우드 콘텐츠 | Windows 팁 표시 안 함 | 사용. 이 정책 설정은 Windows 팁이 사용자에게 표시되지 않도록 합니다. |
| *클라우드 콘텐츠 | Microsoft 소비자 환경 해제 | 사용. 이 정책 설정을 사용하도록 설정하면 Microsoft의 맞춤형 추천 사항 및 해당 Microsoft 계정에 대한 알림이 더 이상 사용자에게 표시되지 않습니다. |
| *데이터 수집 및 Preview 빌드 | 원격 분석 허용 | 0 – 보안[Enterprise만 해당] | 사용. 값을 0으로 설정하면 Enterprise, Education, IoT 또는 Windows Server 버전을 실행하는 디바이스에만 적용됩니다. |
| *데이터 수집 및 Preview 빌드 | 피드백 알림 표시 안 함 |  | 사용 |
| *데이터 수집 및 Preview 빌드 | 참가자 빌드에 대한 사용자 정의 컨트롤 설정/해제  |  | 사용 안 함 |
| 배달 최적화 | 다운로드 모드 | 다운로드 모드: 단순(99) | 99 = 피어링 없는 단순한 다운로드 모드입니다. 배달 최적화는 HTTP만 사용하여 다운로드하며, 배달 최적화 클라우드 서비스에 연결하려고 하지 않습니다. |
| 바탕 화면 창 관리자 |  Flip3D 호출 허용 안 함 |  | 사용 |
| 바탕 화면 창 관리자 |  창 애니메이션 허용 안 함 |  | 사용 |
| 바탕 화면 창 관리자 |  시작 배경에 단색 사용 |  | 사용 |
| 가장자리 UI |  가장자리 살짝 밀기 허용 |  | 사용 안 함 |
| 가장자리 UI |  도움말 설명 사용 안 함 |  | 사용 |
| 가장자리 UI | 앱 사용 추적 해제 |  | 사용 |
| *파일 탐색기 |  Windows Defender SmartScreen 구성 |  | 사용 안 함. SmartScreen이 모든 사용자에 대해 해제됩니다. 사용자가 인터넷에서 의심스러운 앱을 실행하려고 하면 경고가 표시되지 않습니다. 참고: 인터넷에 연결되지 않은 경우 컴퓨터는 SmartScreen 정보를 얻기 위해 Microsoft 연결하려고 하지 않습니다. |
| 파일 탐색기 |  **새 애플리케이션이 설치됨** 알림 표시 안 함 |  | 사용 |
| *내 디바이스 찾기 |  내 디바이스 찾기 켜기/끄기 |  | 사용 안 함. 내 디바이스 찾기가 해제되면 디바이스 및 해당 위치가 등록되지 않고 내 디바이스 찾기 기능이 작동하지 않습니다. 또한 사용자는 디바이스에서 활성 디지타이저를 마지막으로 사용한 위치를 볼 수 없습니다. |
| 파일 탐색기 | 미리 보기 그림 캐싱 사용 안 함 |  | 사용 |
| 파일 탐색기 | Turn off display of recent search entries in the File Explorer search box(파일 탐색기 검색 상자에 최근 검색 항목 표시 안 함) |  | 사용 |
| 파일 탐색기 | 숨겨진 thumbs.db 파일에서 미리 보기 캐싱 끄기 |  | 사용 |
| 게임 탐색기 | 게임 정보 다운로드 사용 안 함 |  | 사용 |
| 게임 탐색기 | 게임 업데이트 사용 안 함 |  | 사용 |
| 게임 탐색기 | 게임 폴더에서 마지막 게임 재생 시간 추적 안 함 |  | 사용 |
| 홈 그룹 | 컴퓨터의 홈 그룹 가입 금지 |  | 사용 |
| *Internet Explorer | 사용자가 주소 표시줄에 입력할 때 Microsoft 서비스에서 향상된 제안을 제공할 수 있도록 허용 |  | 사용 안 함. 주소 표시줄에 입력할 때 향상된 제안이 사용자에게 제공되지 않습니다. 또한 사용자는 제안 설정을 변경할 수 없습니다. |
| Internet Explorer | Internet Explorer 소프트웨어 업데이트를 정기적으로 확인 안 함 |  | 사용 |
| Internet Explorer | 시작 화면 표시 안 함 |  | 사용 |
| Internet Explorer | 새 버전의 Internet Explorer 자동 설치 |  | 사용 안 함 |
| Internet Explorer | 사용자 환경 개선 프로그램에 참여할 수 없음 |  | 사용 |
| Internet Explorer | 첫 실행 마법사 실행 방지 | 홈 페이지로 직접 이동 | 사용 |
| Internet Explorer | 탭 프로세스 증가 설정 | 낮음 | 사용 |
| Internet Explorer | 새 탭의 기본 동작 지정 | 새 탭 페이지 | 사용 |
| Internet Explorer | 추가 기능 성능 알림 끄기 |  | 사용 |
| *Internet Explorer | 웹 주소에 자동 완성 기능 끄기 |  | 사용. 이 정책 설정을 사용하도록 설정하면 웹 주소를 입력할 때 일치 항목이 사용자에게 제안되지 않습니다. 사용자는 웹 주소를 설정하기 위한 자동 완성을 변경할 수 없습니다. |
| *Internet Explorer | 브라우저 지리적 위치 끄기 |  | 사용. 이 정책 설정을 사용하도록 설정하면 브라우저의 지리적 위치 지원이 해제됩니다. |
| *Internet Explorer | 마지막 검색 세션 다시 열기 끄기 |  | 사용 |
| Internet Explorer | 마지막 검색 세션 다시 열기 끄기 |  | 사용 |
| *Internet Explorer | 추천 사이트 켜기 |  | 사용 안 함. 이 정책 설정을 사용하지 않도록 설정하면 이 기능과 관련된 진입점 및 기능이 해제됩니다. |
| *Internet Explorer \\ 호환성 보기 | 호환성 보기 끄기 |  | 사용. 이 정책 설정을 사용하도록 설정하면 사용자가 호환성 보기 단추를 사용하거나 호환성 보기 사이트 목록을 관리할 수 없습니다. |
| Internet Explorer \\ 인터넷 제어판 \\ 고급 페이지 | 웹 페이지에서 애니메이션 재생 |  | 사용 안 함 |
| Internet Explorer \\ 인터넷 제어판 \\ 고급 페이지 | 웹 페이지에서 비디오 재생 |  | 사용 안 함 |
| Internet Explorer \\ 인터넷 제어판 \\ 고급 페이지 | 페이지 넘기기(페이지 예측 포함) 기능 끄기 |  | 사용. Microsoft는 페이지 넘기기(페이지 예측 포함) 기능의 성능을 향상하기 위해 검색 기록을 수집합니다. 이 기능은 데스크톱용 Internet Explorer에서 사용할 수 없습니다. 이 정책 설정을 사용하도록 설정하면 페이지 넘기기(페이지 예측 포함) 기능이 해제되며 다음 웹 페이지가 백그라운드에 로드되지 않습니다. |
| Internet Explorer \\ 인터넷 설정 \\ 고급 설정 \\ 검색 | 전화 번호 검색 끄기 |  | 사용 |
| *위치 및 센서 | 위치 끄기 |  | 사용. 이 정책 설정을 사용하도록 설정하면 위치 기능이 해제되고 이 컴퓨터의 모든 프로그램에서 위치 기능의 위치 정보를 사용할 수 없습니다. |
| 위치 및 센서 | 센서 끄기 |  | 사용 |
| 위치 및 센서 \\ Windows 위치 제공자 | Windows 위치 제공자 끄기 |  | 사용 |
| *지도 | 맵 데이터의 자동 다운로드 및 업데이트 끄기 |  | 사용. 이 설정을 사용하도록 설정하면 지도 데이터의 자동 다운로드 및 업데이트가 해제됩니다. |
| *지도 | 오프라인 맵 설정 페이지에서 원하지 않는 네트워크 트래픽 끄기 |  | 사용. 이 정책 설정을 사용하도록 설정하면 오프라인 지도 설정 페이지에서 네트워크 트래픽을 생성하는 기능이 해제됩니다. 참고: 이 경우 전체 설정 페이지가 해제될 수 있습니다. |
| *메시징 | 메시지 서비스 클라우드 동기화 허용 |  | 사용 안 함. 이 정책 설정을 사용하면 휴대폰 문자 메시지를 Microsoft의 클라우드 서비스로 백업 및 복원할 수 있습니다. |
| *Microsoft Edge | 주소 표시줄 드롭다운 목록 제안 허용 |  | 사용 안 함 |
| *Microsoft Edge | 책 라이브러리에 대한 구성 업데이트 허용 |  | 사용 안 함. Microsoft Edge에서 호환성 목록을 해제합니다. |
| *Microsoft Edge | Microsoft 호환성 목록 허용 |  | 사용 안 함. 이 설정을 사용하지 않도록 설정하면 브라우저 탐색 중에 Microsoft 호환성 목록이 사용되지 않습니다. |
| *Microsoft Edge | 새 탭 페이지에서 웹 콘텐츠 허용 |  | 사용 안 함. 새 탭이 열릴 때 Edge에서 빈 콘텐츠로 열도록 지시합니다. |
| *Microsoft Edge | 자동 채우기 구성 |  | 사용 안 함. 주소 표시줄에서 자동 채우기를 사용하지 않도록 설정합니다. |
| *Microsoft Edge | Do Not Track 구성 |  | 사용. 이 설정을 사용하면 Do Not Track 요청이 추적 정보를 요청하는 웹 사이트로 항상 전송됩니다. |
| *Microsoft Edge | 암호 관리자 구성 |  | 사용 안 함. 이 설정을 사용하지 않도록 설정하면 직원이 암호 관리자를 사용하여 암호를 로컬로 저장할 수 없습니다. |
| *Microsoft Edge | 주소 표시줄에서 검색 제안 구성 |  | 사용 안 함. 사용자가 Microsoft Edge의 주소 표시줄에서 검색 제안을 볼 수 없습니다. |
| *Microsoft Edge | 시작 페이지 구성 |  | 사용. 이 설정을 사용하도록 설정하면 하나 이상의 시작 페이지를 구성할 수 있습니다. 이 설정을 사용하도록 설정되는 경우 페이지에 대한 URL도 포함해야 합니다. 여기서는 꺾쇠 괄호를 사용하여 여러 페이지를 <support.contoso.com><support.microsoft.com> 형식으로 구분합니다. Windows 10 버전 1703 이상: 트래픽을 Microsoft에 보내지 않으려는 경우 디바이스가 도메인에 조인했는지 여부에 관계없이 <about:blank> 값이 유일하게 구성된 URL일 때 이 값을 사용하여 해당 디바이스에 적용할 수 있습니다. |
| *Microsoft Edge | Windows Defender SmartScreen 구성 |  | 사용 안 함. Windows Defender SmartScreen이 해제되고 직원이 이를 설정할 수 없습니다. 참고: 환경 내에서 이 설정을 고려하세요. 인터넷에 연결되지 않은 경우 컴퓨터는 SmartScreen 정보를 얻기 위해 Microsoft 연결하려고 하지 않습니다. |
| *Microsoft Edge | Microsoft Edge에서 첫 실행 웹 페이지 표시 금지 |  | 사용. Microsoft Edge를 처음 열 때 첫 실행 페이지가 사용자에게 표시되지 않습니다. |
| OneDrive | 사용자의 다음 번 OneDrive 로그인 때까지 OneDrive의 네트워크 트래픽 생성 방지 |  | 사용. 사용자가 OneDrive에 로그인하거나 파일을 로컬 컴퓨터에 동기화하기 시작할 때까지 OneDrive 동기화 클라이언트(OneDrive.exe)에서 네트워크 트래픽(업데이트 확인 등)을 생성하지 못하도록 하려면 이 설정을 사용하도록 설정합니다. |
| *OneDrive | 파일 스토리지에 OneDrive 사용 방지 |  | 사용. OneDrive를 온-프레미스 또는 오프-프레미스에서 사용하지 않는 경우에 해당됩니다. |
| OneDrive | 기본적으로 OneDrive에 문서 저장 |  | 사용 안 함. OneDrive를 온-프레미스 또는 오프-프레미스에서 사용하지 않는 경우에 해당됩니다. |
| RSS 피드 | 피드 및 웹 조각의 자동 검색 방지 |  | 사용 |
|*RSS 피드 | 피드 및 웹 조각에 대한 백그라운드 동기화 끄기 |  | 사용. 이 정책 설정을 사용하도록 설정하면 백그라운드에서 피드 및 웹 조각을 동기화하는 기능이 해제됩니다. |
|*검색 | Cortana 허용 |  | 사용 안 함. Cortana가 해제되어 있는 경우에도 사용자가 검색을 사용하여 디바이스에서 항목을 찾을 수 있습니다. |
|검색 | 잠금 화면 위에서 Cortana 허용 |   | 사용 안 함 |
|*검색 | 위치를 사용하도록 검색 및 Cortana 허용 |  | 사용 안 함 |
|검색 | 웹 검색 허용 안 함 |   | 사용 |
|*검색 | 검색에서 웹을 검색하거나 웹 결과를 표시하지 않음 |  | 사용. 이 정책 설정을 사용하도록 설정하면 웹에서 쿼리가 수행되지 않고 사용자가 검색에서 쿼리를 수행할 때 웹 결과가 표시되지 않습니다. |
|검색 | 제어판에서 UNC 위치를 색인에 추가 안 함 |  | 사용 |
|검색 | 오프라인 파일 캐시의 파일 색인화 안 함 |  | 사용 |
|*검색 | 익명 정보 검색에서 공유하는 정보 설정 |  | 사용. 사용 정보는 공유하지만, 검색 기록, Microsoft 계정 정보 또는 특정 위치는 공유하지 않습니다. |
|*Software Protection Platform | KMS 클라이언트 온라인 AVC 유효성 검사 끄기 | 사용. 이 설정을 사용하도록 설정하면 이 컴퓨터에서 정품 인증 상태와 관련하여 데이터를 Microsoft에 보내지 않습니다. |
|*음성 | 음성 데이터의 자동 업데이트 허용 |  | 사용 안 함. 업데이트된 음성 모델을 주기적으로 확인하지 않습니다. |
|*저장소 | 업데이트의 자동 다운로드 및 설치 끄기 |  | 사용. 이 설정을 사용하도록 설정하면 앱 업데이트의 자동 다운로드 및 업데이트가 해제됩니다. |
|*저장소 | Win8 디바이스에서 업데이트의 자동 다운로드 끄기 | 사용. 이 설정을 사용하도록 설정하면 앱 업데이트의 자동 다운로드가 해제됩니다. |
| 스토어 | 최신 버전 Windows 업데이트 제안 끄기 |  | 사용 |
|*설정 동기화 | 동기화 안 함 | 동기화를 켤 수 있도록 합니다(선택되지 않음). | 사용. 이 정책 설정을 사용하도록 설정하면 "설정 동기화"가 해제되고 "설정 동기화" 그룹이 이 디바이스에서 동기화되지 않습니다. |
| 텍스트 입력 | 수동 입력 및 입력 인식 개선 |  | 사용 안 함 |
| Windows Defender 바이러스 백신 \\ MAPS | Microsoft MAPS에 가입 |  | 사용 안 함. 이 설정을 사용하지 않도록 설정하거나 구성하지 않으면 Microsoft MAPS에 조인되지 않습니다. |
| Windows Defender 바이러스 백신 \\ MAPS | 추가 분석이 필요할 때 파일 샘플 전송 | 보내지 않음 | 사용. MAPS 진단 데이터에 옵트인하지 않은 경우에만 해당됩니다. |
| Windows Defender 바이러스 백신 \\ 보고 | 향상된 알림 끄기 |  | 사용. 이 설정을 사용하도록 설정하면 Windows Defender 바이러스 백신의 고급 알림이 클라이언트에 표시되지 않습니다. |
| Windows Defender 바이러스 백신 \\ 서명 업데이트 | 정의 업데이트 다운로드용 원본 순서 정의 | FileShares | 사용. 이 설정을 사용하도록 설정하면 지정된 순서로 정의 업데이트 원본에 연결됩니다. 하나의 지정된 원본에서 정의 업데이트가 성공적으로 다운로드되면 목록의 나머지 원본은 연결되지 않습니다. |
| Windows 오류 보고 | 운영 체제에서 생성된 오류 보고서에 대한 메모리 덤프를 자동으로 보내기 |  | 사용 안 함 |
| Windows 오류 보고 | Windows 오류 보고 사용 안 함 |  | 사용 |
| Windows 게임 녹화 및 브로드캐스팅 | Windows 게임 녹화 및 브로드캐스팅 사용 또는 사용하지 않음 | | 사용 안 함 |
| Windows Installer | 기본 파일 캐시의 최대 크기 제어 | 5 | 사용 |
| Windows Installer | 시스템 복원 검사점의 생성을 사용 안 함 |  | 사용 |
| Windows Mail | 커뮤니티 기능 해제 |  | 사용 |
| Windows Media Player | 처음 사용 대화 상자 표시 안 함 |  | 사용 |
| Windows Media Player | 미디어 공유 금지 |  | 사용 |
| Windows 모바일 센터 | Windows 모바일 센터 끄기 |  | 사용 |
| Windows 안정성 분석 | 안정성 WMI 공급자 구성 |  | 사용 안 함 |
| Windows 업데이트 | 자동 업데이트로 바로 설치 허용 |  | 사용 |
| Windows 업데이트 | 모든 Windows 업데이트 인터넷 위치에 연결 하지 마십시오 |  | 사용. 이 정책을 사용하도록 설정하면 해당 기능을 사용하지 않도록 설정되고 Windows 스토어와 같은 퍼블릭 서비스에 대한 연결이 작동하지 않을 수 있습니다. 참고: 이 정책은 디바이스가 "인트라넷 Microsoft 업데이트 서비스 위치 지정" 정책을 사용하여 인트라넷 업데이트 서비스에 연결하도록 구성된 경우에만 적용됩니다. |
| Windows 업데이트 | 모든 Windows 업데이트 기능을 액세스할 수 있는 권한 제거 |   | 사용 |
| *Windows 업데이트 \\ 비즈니스용 Windows 업데이트 | 미리 보기 빌드 관리 | 미리 보기 빌드를 받기 위한 동작을 설정합니다. | 사용. [미리 보기 빌드 사용 안 함]을 선택하면 미리 보기 빌드가 디바이스에 설치되지 않습니다. 그러면 사용자가 설정 -> 업데이트 및 보안을 통해 Windows 참가자 프로그램에 옵트인할 수 없습니다.<br>사용 안 함. 미리 보기 빌드를 사용하지 않도록 설정합니다. |
| *Windows 업데이트 \\ 비즈니스용 Windows 업데이트 | 미리 보기 빌드 및 기능 업데이트를 받는 시기 선택 | 반기 채널<br>연기: 365일<br>일시 중지 시작: yyyy-mm-dd | 사용. 받을 Preview 빌드 또는 기능 업데이트의 수준과 받는 시기를 지정하려면 이 정책을 사용하도록 설정합니다. |
| Windows 업데이트 \\ 비즈니스용 Windows 업데이트 | 품질 업데이트를 받는 경우 선택 | 1. 30일<br>2. 품질 업데이트 일시 중지 시작 yyyy-mm-dd | 사용 |
| Windows 제한된 트래픽 사용자 지정 정책 설정 | 사용자의 다음 번 OneDrive 로그인 때까지 OneDrive의 네트워크 트래픽 생성 방지 |  | 사용. 사용자가 OneDrive에 로그인하거나 파일을 로컬 컴퓨터에 동기화하기 시작할 때까지 OneDrive 동기화 클라이언트(OneDrive.exe)에서 네트워크 트래픽(업데이트 확인 등)을 생성하지 못하도록 하려면 이 설정을 사용하도록 설정합니다. |
| Windows 제한된 트래픽 사용자 지정 정책 설정 | Windows Defender 알림 끄기 |  | 사용. 이 정책 설정을 사용하도록 설정하면 Windows Defender에서 디바이스의 상태 및 보안에 대한 중요한 정보가 포함된 알림을 보내지 않습니다. |
| 로컬 컴퓨터 정책 \\ 사용자 구성 \\ 관리 템플릿  |  |  |
|제어판 \\ 국가 및 언어 옵션 | 텍스트 자동 완성 사용 안 함 |  | 사용 |
| 데스크톱 | 네트워크 위치에 최근에 연 문서의 공유를 추가 안 함 |  | 사용 |
| 데스크톱 | Aero 흔들기 창 최소화 마우스 제스처 사용 안 함 |  | 사용 |
| 데스크톱 \\ Active Directory | Active Directory 검색의 최대 크기 | 2500 | 사용 |
| 시작 메뉴 및 작업 표시줄 | 작업 표시줄에 스토어 앱 고정 허용 안 함 |  | 사용 |
| 시작 메뉴 및 작업 표시줄 | 원격 위치의 항목을 점프 목록에 표시하거나 추적 안 함 |  | 사용 |
| 시작 메뉴 및 작업 표시줄 | 셸 바로 가기를 확인할 때 검색 기반 방법 사용 안 함 |  | 사용. 시스템에서 최종 드라이브 검색을 수행하지 않습니다. 파일을 찾을 수 없다는 메시지만 표시됩니다. |
| 시작 메뉴 및 작업 표시줄 | 작업 표시줄에서 피플 표시줄 제거 |  | 사용. 작업 표시줄에서 사람 아이콘이 제거되고, 작업 표시줄 설정 페이지에서 해당 설정 토글이 제거되며, 사용자가 사람 아이콘을 작업 표시줄에 고정할 수 없습니다. |
| 시작 메뉴 및 작업 표시줄 | 기능을 알리는 풍선 알림 끄기 |  | 사용. 사용자가 스토어 앱을 작업 표시줄에 고정할 수 없습니다. 스토어 앱이 작업 표시줄에 이미 고정되어 있는 경우 다음에 로그인할 때 작업 표시줄에서 제거됩니다. |
| 시작 메뉴 및 작업 표시줄 | 사용자 추적 사용 안 함 |  | 사용 |
| 시작 메뉴 및 작업 표시줄 \\ 알림 | Turn off toast notifications(알림 사용 안 함) |  | 사용 |
| Windows 구성 요소 \\ 클라우드 콘텐츠 | 모든 Windows 추천 기능 끄기 |  | 사용 |

### <a name="notes-about-network-connectivity-status-indicator"></a>네트워크 연결 상태 표시기에 대한 참고 사항

위의 그룹 정책 설정에는 시스템이 인터넷에 연결되어 있는지 확인하기 위한 기능을 끄는 설정이 포함되어 있습니다. 작업 환경이 인터넷에 연결되지 않거나 간접적으로 연결되는 경우 작업 표시줄에서 네트워크 아이콘을 제거하도록 그룹 정책 설정을 설정할 수 있습니다. 작업 표시줄에서 네트워크 아이콘을 제거하려는 이유는 인터넷 연결 확인을 끌 경우 네트워크가 정상적으로 작동하더라도 네트워크 아이콘에 노란색 플래그가 표시되기 때문입니다. 네트워크 아이콘을 그룹 정책 설정으로서 제거하려는 경우 다음 위치에서 찾을 수 있습니다.

| 정책 설정 | 항목 | 하위 항목 | 가능한 설정 및 설명|
| -------------- | ---- | -------- | ---------------------------- |
| Windows 업데이트 또는 비즈니스용 Windows 업데이트 | 품질 업데이트를 받는 경우 선택 | 1. 30일<br>2. 품질 업데이트 일시 중지 시작 yyyy-mm-dd | 사용 |
| 로컬 컴퓨터 정책 \\ 사용자 구성 \\ 관리 템플릿 |  |  |  |
| 시작 메뉴 및 작업 표시줄 | 네트워킹 아이콘 제거 |  | 사용. 네트워킹 아이콘이 시스템 알림 영역에 표시되지 않습니다. |

NCSI(네트워크 연결 상태 표시기)에 대한 자세한 내용은 [Windows 10 Enterprise 버전 1903에 대한 연결 엔드포인트 관리](https://docs.microsoft.com/windows/privacy/manage-windows-1903-endpoints) 및 [Windows 10 운영 체제 구성 요소에서 Microsoft 서비스로의 연결 관리](https://docs.microsoft.com/windows/privacy/manage-connections-from-windows-operating-system-components-to-microsoft-services)를 참조하세요.

### <a name="system-services"></a>시스템 서비스

리소스를 절약하기 위해 시스템 서비스를 사용하지 않도록 설정하는 것을 고려하는 경우 고려되는 서비스가 어떤 방식으로든 다른 서비스의 구성 요소가 아닌지 각별히 주의해야 합니다. 사용 가능한 일부 서비스는 지원되는 방식으로 사용하지 않도록 설정할 수 없으므로 목록에 없습니다.

이러한 추천 사항은 대부분 [데스크톱 환경이 있는 Windows Server 2016에서 시스템 서비스를 사용하지 않도록 설정하기 위한 지침](https://docs.microsoft.com/windows-server/security/windows-services/security-guidelines-for-disabling-system-services-in-windows-server)의 데스크톱 환경이 설치된 Windows Server 2016에 대한 추천 사항을 반영합니다.

사용하지 않도록 설정하는 데 적합한 많은 서비스는 수동 서비스 시작 유형으로 설정되어 있습니다. 즉, 서비스가 자동으로 시작되지 않으며, 프로세스 또는 이벤트에서 사용하지 않도록 설정하려는 서비스에 대한 요청을 트리거하지 않는 경우에도 서비스가 시작되지 않습니다. 시작 유형이 이미 수동으로 설정된 서비스는 일반적으로 여기에 표시되지 않습니다.

> [!NOTE]
> 다음 PowerShell 샘플 코드를 사용하여 실행되는 서비스를 열거하고 서비스 약식 이름만 출력할 수 있습니다.

```powershell
 Get-Service | Where-Object {$_.Status -eq "Running"} | select -ExpandProperty Name
 ```

| Windows 서비스 | 항목 | 설명|
| -------------- | ---- | ---------------------------- |
| CDPUserService | 이 사용자 서비스는 연결된 디바이스 플랫폼 시나리오에 사용됩니다. | 이러한 서비스는 사용자별 서비스이므로 *템플릿 서비스*를 사용하지 않도록 설정해야 합니다. |
| 연결된 사용자 환경 및 원격 분석 | 애플리케이션 내부 및 연결된 사용자 환경을 지원하는 기능을 사용하도록 설정합니다. 또한 이 서비스는 [피드백 및 진단] 아래에서 진단 및 사용 개인 정보 옵션을 사용하도록 설정한 경우 진단 및 사용 정보(Windows 플랫폼의 환경과 품질을 개선하는 데 사용됨)의 이벤트 기반 수집 및 전송을 관리합니다. | 연결이 끊긴 네트워크인 경우 사용하지 않도록 설정하는 것이 좋습니다. |
| 연락처 데이터 | 빠른 연락처 검색을 위해 연락처 데이터를 인덱싱합니다. 이 서비스를 중지하거나 사용하지 않도록 설정할 경우 연락처가 검색 결과에 누락될 수 있습니다. | 이러한 서비스는 사용자별 서비스이므로 *템플릿 서비스*를 사용하지 않도록 설정해야 합니다. |
| 진단 정책 서비스 | Windows 구성 요소에 대한 문제 감지, 문제 해결 과정 및 해결을 사용하도록 설정합니다. 이 서비스를 중지하는 경우 진단이 더 이상 작동하지 않습니다. | |
| 다운로드한 지도 관리자 | 애플리케이션에서 다운로드한 지도에 액세스하기 위한 Windows 서비스입니다. 이 서비스는 애플리케이션에서 다운로드한 지도를 이용할 때 요청에 따라 시작됩니다. 이 서비스를 사용하지 않도록 설정하면 앱에서 지도에 액세스할 수 없게 됩니다. | |
| 지리적 위치 서비스 | 시스템의 현재 위치를 모니터링하고 지오펜스를 관리합니다. | |
| 게임 DVR 및 브래드캐스트 사용자 서비스 | 이 사용자 서비스는 게임 녹음 및 라이브 브로드캐스트에 사용합니다. | 이러한 서비스는 사용자별 서비스이므로 템플릿 서비스를 사용하지 않도록 설정해야 합니다. |
| MessagingService | 문자 메시지 및 관련 기능을 지원하는 서비스입니다. | 이러한 서비스는 사용자별 서비스이므로 *템플릿 서비스*를 사용하지 않도록 설정해야 합니다. |
| 드라이브 최적화 | 스토리지 드라이브의 파일을 최적화하여 컴퓨터가 보다 효율적으로 실행될 수 있도록 합니다. | 일반적으로 VDI 솔루션은 디스크 최적화를 수행해도 큰 혜택이 없습니다. 이러한 "드라이브"는 기존 드라이브가 아니며, 임시 스토리지 할당에 불과합니다. |
| Superfetch | 지속적으로 시스템 성능을 유지하고 향상시킵니다. | 일반적으로 다시 부팅할 때마다 운영 체제 상태가 삭제된다고 가정할 경우 VDI, 특히 비영구적 솔루션에서는 성능이 개선되지 않습니다. |
| 터치 키보드 및 필기 패널 서비스 | 터치 키보드 및 필기 패널의 펜 및 잉크 기능 사용 | |
| Windows 오류 보고 | 프로그램이 작동 또는 응답을 중지할 때 오류가 보고되도록 하고 기존 솔루션이 전달될 수 있도록 허용합니다. 또한 진단 및 복구 서비스에 대해 로그가 생성될 수 있도록 합니다. 이 서비스를 중지하는 경우 오류 보고가 제대로 작동하지 않을 수 있으며 진단 서비스 및 복구 작업의 결과가 표시되지 않을 수 있습니다. | VDI를 사용하면 진단이 주류 프로덕션 환경이 아닌 오프라인 시나리오에서 수행됩니다. 또한 일부 고객은 WER을 사용하지 않도록 설정합니다. WER을 사용하면 디바이스 설치 실패 또는 업데이트 설치 실패와 같은 많은 다양한 경우에 소량의 리소스가 사용됩니다. |
| Windows Media Player 네트워크 공유 서비스 | 유니버설 플러그 앤 플레이를 사용하여 네트워크로 연결된 다른 플레이어 및 미디어 디바이스와 Windows Media Player 라이브러리를 공유합니다. | 고객이 네트워크에서 WMP 라이브러리를 공유하는 경우에만 필요합니다. |
| Windows 모바일 핫스팟 서비스 | 다른 디바이스와 셀룰러 데이터 연결을 공유하는 기능을 제공합니다. | |
| Windows 검색 | 파일, 메일 및 기타 콘텐츠에 대한 콘텐츠 인덱싱, 속성 캐싱 및 검색 결과를 제공합니다.                                                                    | 특히 비영구적 VDI를 사용할 때는 필요하지 않습니다. |

#### <a name="per-user-services-in-windows"></a>Windows의 사용자 단위 서비스

사용자 단위 서비스는 사용자가 Windows 또는 Windows Server에 로그인하면 만들어지고, 해당 사용자가 로그아웃하면 중지되고 삭제되는 서비스입니다. 이러한 서비스는 사용자 계정의 보안 컨텍스트에서 실행됩니다. 즉, 미리 구성한 계정과 연결해서 또는 작업으로서 이러한 종류의 서비스를 실행하는 이전 방식보다 더 나은 리소스 관리를 제공합니다.

[Windows 10 및 Windows Server의 사용자 단위 서비스](https://docs.microsoft.com/windows/application-management/per-user-services-in-windows)

서비스 시작 값을 변경하려는 경우 기본 설정 방법은 관리자 권한 .cmd 프롬프트를 열고 'Sc.exe' 서비스 제어 관리자 도구를 실행하는 것입니다. 'Sc.exe'를 사용하는 방법에 대한 자세한 내용은 [Sc](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/cc754599(v=ws.11))를 참조하세요

### <a name="scheduled-tasks"></a>예약형 작업

Windows의 다른 항목과 마찬가지로 사용하지 않도록 설정하기 전에 항목이 필요하지 않은지 확인합니다.

다음과 같은 작업 목록은 컴퓨터에 대해 최적화 또는 데이터 수집을 수행하여 다시 부팅해도 상태를 그대로 유지하는 작업입니다. VDI VM 작업이 다시 부팅되고, 마지막 부팅 이후의 모든 변경 내용을 취소하면 물리적 컴퓨터를 위한 최적화가 별로 유용하지 않습니다.

다음 PowerShell 코드를 사용하여 현재 예약된 작업(설명 포함)을 모두 가져올 수 있습니다.

```powershell
 Get-ScheduledTask | Select-Object -Property TaskPath,TaskName,State,Description
```

>[!NOTE]
> 관리자 권한으로 실행하는 경우에도 스크립트를 통해 사용하지 않도록 설정할 수 없는 몇 가지 작업이 있습니다. 스크립트를 사용하여 사용하지 않도록 설정할 수 없는 작업을 사용하지 않도록 설정하는 것이 좋습니다.

예약된 작업 이름:

- 셀룰러
- Consolidator
- 진단
- FamilySafetyMonitor
- FamilySafetyRefreshTask
- MaintenanceTasks
- MapsToastTask
- 호환성
- Microsoft-Windows-DiskDiagnosticDataCollector
- MNO
- NotificationTask
- PerformRemediation
- ProactiveScan
- ProcessMemoryDiagnosticEvents
- ProgramDataUpdater
- Proxy (프록시)
- QueueReporting
- RecommendedTroubleshootingScanner
- ReconcileFeatures
- ReconcileLanguageResources
- RefreshCache
- RegIdleBackup
- ResPriStaticDbSync
- RunFullMemoryDiagnostic
- ScanForUpdates
- ScanForUpdatesAsUser
- 예약
- ScheduledDefrag
- sihpostreboot
- SilentCleanup
- SmartRetry
- SpaceAgentTask
- SpaceManagerTask
- SpeechModelDownloadTask
- Sqm-Tasks
- SR
- StartComponentCleanup
- StartupAppTask
- StorageSense
- SyspartRepair
- Sysprep
- UninstallDeviceTask
- UpdateLibrary
- UpdateModelTask
- UsbCeip
- Usb-Notifications
- USO_UxBroker
- WiFi
- WIM-Hash-Management
- WindowsActionDialog
- WinSAT
- 폴더
- WsSwapAssessmentTask
- XblGameSaveTask

### <a name="apply-windows-and-other-updates"></a>Windows(및 기타) 업데이트 적용

Microsoft Update 또는 내부 리소스에서 Windows Defender 서명을 포함한 사용 가능한 업데이트를 적용합니다. 이 경우 Microsoft Office(설치된 경우)를 포함하여 사용 가능한 다른 업데이트 및 기타 소프트웨어 업데이트를 적용하는 것이 좋습니다. PowerShell이 이미지에서 유지되는 경우 [Update-Help](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/update-help?view=powershell-7) 명령을 실행하여 PowerShell에 사용할 수 있는 최신 도움말을 다운로드할 수 있습니다.

#### <a name="servicing-the-operating-system-and-apps"></a>운영 체제 및 앱 서비스

이미지 최적화 프로세스 중 특정 시점에 사용 가능한 Windows 업데이트가 적용됩니다. Windows 10 업데이트 설정에는 추가 업데이트를 제공할 수 있는 설정이 있습니다.

![추가 업데이트](media/rds-vdi-recommendations-1909/servicing.png)

이러한 설정은 Microsoft Office와 같은 Microsoft 애플리케이션을 기본 이미지에 설치하려는 경우에 매우 적합합니다. 이렇게 하면 이미지가 사용될 때 Office가 최신 상태로 유지됩니다. Windows 업데이트를 통해 사용 가능한 업데이트가 있는 .NET 업데이트 및 특정 타사 구성 요소(예: Adobe)도 있습니다.

비영구적 VDI VM에 대한 매우 중요한 고려 사항 중 하나는 보안 소프트웨어 정의 파일을 포함하는 보안 업데이트입니다. 이러한 업데이트는 하루에 한 번 이상 릴리스될 수 있습니다. Windows Defender 및 타사 구성 요소를 포함하여 이러한 업데이트를 유지하는 방법이 있을 수 있습니다.

Windows Defender의 경우 비영구적 VDI에서도 업데이트가 수행되도록 하는 것이 가장 바람직할 수 있습니다. 업데이트가 거의 모든 로그온 세션에 적용되지만, 규모가 작으므로 문제가 되지 않습니다. 또한 사용 가능한 최신 업데이트만 적용되므로 VM은 업데이트 시 최신 상태로 유지됩니다. 타사 정의 파일에 대해서도 마찬가지입니다.

> [!NOTE]
> Windows Store를 통해 앱(UWP 앱) 업데이트를 저장합니다. Office 365와 같은 최신 버전의 Office는 인터넷에 직접 연결되는 경우 고유한 메커니즘을 통해 또는 직접 연결되지 않는 경우 관리 기술을 통해 업데이트됩니다.

### <a name="windows-system-startup-event-traces"></a>Windows 시스템 시작 이벤트 추적

Windows는 기본적으로 제한된 진단 데이터를 수집 및 저장하도록 구성됩니다. 이는 진단을 사용하도록 설정하거나, 추가 문제 해결이 필요한 경우 데이터를 기록하기 위한 것입니다. 자동 시스템 추적은 다음 그림에 표시된 위치에서 확인할 수 있습니다.

![시스템 추적](media/rds-vdi-recommendations-1909/system-traces.png)

**이벤트 추적 세션** 및 **시작 이벤트 추적 세션** 아래에 표시되는 일부 추적은 중지할 수 없을 뿐만 아니라 중지하면 안 됩니다. 'WiFiSession' 추적과 같은 다른 추적은 중지할 수 있습니다. **이벤트 추적 세션**에서 실행 중인 추적을 중지하려면 마우스 오른쪽 단추로 추적을 클릭한 다음, '중지'를 클릭합니다. 시작 시 추적이 자동으로 시작되지 않도록 하려면 다음 절차를 사용합니다.

1. **시작 이벤트 추적 세션** 폴더를 클릭합니다.

2. 관심 있는 추적을 찾은 후 해당 추적을 두 번 클릭합니다.

3. **추적 세션** 탭을 클릭합니다.

4. **사용**이라는 레이블이 지정된 확인란을 클릭하여 확인 표시를 제거합니다.

5. **확인**을 클릭합니다.

다음은 VDI를 사용하기 위해 사용하지 않도록 설정하려는 몇 가지 시스템 추적입니다.

| 이름                    | 설명                       |
| ----------------------- | ----------------------------- |
| AppModel | 추적 컬렉션으로, 휴대폰이 여기에 포함됩니다. |
| CloudExperienceHostOOBE | |
| DiagLog | |
| NtfsLog | |
| TileStore | |
| UBPM | |
| WiFiDriverIHVSession | WiFi 디바이스를 사용하지 않는 경우 |
| WiFiSession | |
| WinPhoneCritical | |

### <a name="windows-defender-optimization-with-vdi"></a>VDI를 사용한 Windows Defender 최적화

Microsoft는 최근에 VDI 환경에서 Windows Defender와 관련된 설명서를 게시했습니다. 자세한 내용은 [VDI(가상 데스크톱 인프라) 환경의 Windows Defender 바이러스 백신 배포 가이드](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-antivirus/deployment-vdi-windows-defender-antivirus)를 참조하세요.

위의 문서에는 '골드' VDI 이미지를 서비스하는 절차와 실행되는 VDI 클라이언트를 유지 관리하는 방법이 포함되어 있습니다. VDI 컴퓨터가 Windows Defender 서명을 업데이트해야 하는 경우 네트워크 대역폭을 줄이려면 재부팅을 스태거하고, 가능한 경우 작업이 없는 시간 동안 다시 부팅하도록 예약합니다. Windows Defender 서명 업데이트를 파일 공유에 내부적으로 포함할 수 있으며, 가능한 경우 해당 파일 공유를 VDI 가상 머신과 동일하거나 가까운 네트워킹 세그먼트에 둘 수 있습니다.

### <a name="client-network-performance-tuning-by-registry-settings"></a>레지스트리 설정별 클라이언트 네트워크 성능 튜닝

네트워크 성능을 향상시킬 수 있는 몇 가지 레지스트리 설정이 있습니다. 이는 주로 네트워크를 기반으로 하는 워크로드가 VDI 또는 컴퓨터에 있는 환경에서 특히 중요합니다. 이 섹션의 설정은 항목(예: 디렉터리 항목)에 대한 추가 버퍼링 및 캐싱을 설정하여 네트워킹의 성능을 향상시키는 것이 좋습니다.

>[!NOTE]
> 이 섹션의 일부 설정은 레지스트리 기반 전용이며, 프로덕션에서 사용하도록 이미지를 배포하기 전에 기본 이미지에 통합해야 합니다.

다음 설정은 Windows 제품 그룹에서 Microsoft.com에 게시한 [Windows Server 2016 성능 튜닝 지침](https://docs.microsoft.com/windows-server/administration/performance-tuning/)에 나와 있습니다.

#### <a name="disablebandwidththrottling"></a>DisableBandwidthThrottling

`HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\DisableBandwidthThrottling`

Windows 10에 적용됩니다. 기본값은 **0**입니다. 기본적으로 SMB 리디렉터는 대기 시간이 긴 네트워크 연결의 처리량을 제한하며, 네트워크 관련 시간 제한을 방지할 목적으로 제한하는 경우도 가끔 있습니다. 이 레지스트리 값을 1로 설정하면 제한이 해제되어 대기 시간이 긴 네트워크 연결을 통해 더 높은 파일 전송 처리량을 사용할 수 있습니다. 이 값을 **1**로 설정하는 것이 좋습니다.

#### <a name="fileinfocacheentriesmax"></a>FileInfoCacheEntriesMax

`HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\FileInfoCacheEntriesMax` Windows 10에 적용됩니다. 기본값은 **64**이며, 유효 범위는 1-65536입니다. 이 값은 클라이언트에서 캐시할 수 있는 파일 메타데이터의 양을 결정하는 데 사용됩니다. 이 값을 늘리면 많은 파일에 액세스할 때 네트워크 트래픽을 줄이고 성능을 높일 수 있습니다. 이 값을 **1024**로 늘려봅니다.

#### <a name="directorycacheentriesmax"></a>DirectoryCacheEntriesMax

`HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\DirectoryCacheEntriesMax`

Windows 10에 적용됩니다. 기본값은 **16**이며, 유효 범위는 1-4096입니다. 이 값은 클라이언트에서 캐시할 수 있는 디렉터리 정보의 양을 결정하는 데 사용됩니다. 이 값을 늘리면 큰 디렉터리에 액세스할 때 네트워크 트래픽을 줄이고 성능을 높일 수 있습니다. 이 값을 **1024**로 늘리는 것이 좋습니다.

#### <a name="filenotfoundcacheentriesmax"></a>FileNotFoundCacheEntriesMax

`HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\FileNotFoundCacheEntriesMax`

Windows 10에 적용됩니다. 기본값은 **128**이며, 유효 범위는 1-65536입니다. 이 값은 클라이언트에서 캐시할 수 있는 파일 이름 정보의 양을 결정하는 데 사용됩니다. 이 값을 늘리면 많은 파일 이름에 액세스할 때 네트워크 트래픽을 줄이고 성능을 높일 수 있습니다. 이 값을 **2048**로 늘리는 것이 좋습니다.

#### <a name="dormantfilelimit"></a>DormantFileLimit

`HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\DormantFileLimit`

Windows 10에 적용됩니다. 기본값은 **1023**입니다. 이 매개 변수는 애플리케이션이 파일을 닫은 후 공유 리소스에서 열어 두어야 하는 최대 파일 수를 지정합니다. 수천 개의 클라이언트가 SMB 서버에 연결하는 경우 이 값을 **256**으로 줄이는 것을 고려합니다.

[Set-SmbClientConfiguration](https://docs.microsoft.com/powershell/module/smbshare/set-smbclientconfiguration?view=win10-ps) 및 [Set-SmbServerConfiguration](https://docs.microsoft.com/powershell/module/smbshare/set-smbserverconfiguration?view=win10-ps) Windows PowerShell cmdlet을 사용하여 이러한 여러 SMB 설정을 구성할 수 있습니다. 다음 예제와 같이 Windows PowerShell을 사용하여 레지스트리 전용 설정을 구성할 수도 있습니다.

```powershell
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters" RequireSecuritySignature -Value 0 -Force
```

Windows Restricted Traffic Limited Functionality Baseline 지침에서 제공하는 추가 설정이 있습니다. Microsoft는 인터넷에 직접 연결되지 않았거나 Microsoft 및 기타 서비스로 보내는 데이터를 줄이려는 환경을 위해 [Windows 보안 기준](https://docs.microsoft.com/powershell/module/smbshare/set-smbserverconfiguration?view=win10-ps)과 동일한 절차를 사용하여 만든 기준을 릴리스했습니다.

[Windows Restricted Traffic Limited Functionality Baseline](https://docs.microsoft.com/windows/privacy/manage-connections-from-windows-operating-system-components-to-microsoft-services) 설정은 그룹 정책 설정 표에서 별표로 표시되어 있습니다.

#### <a name="disk-cleanup-including-using-the-disk-cleanup-wizard"></a>디스크 정리(디스크 정리 마법사 사용 포함)

디스크 정리는 골드/마스터 이미지 VDI 구현에 특히 유용할 수 있습니다. 이미지가 준비, 업데이트 및 구성되면 마지막으로 수행할 작업 중 하나는 디스크 정리입니다. 디스크 공간을 절약할 수 있는 대부분의 잠재적인 영역을 정리하는 데 도움이 되는 "디스크 정리 마법사"라는 기본 제공 도구가 있습니다. 거의 설치되지 않았지만 완전히 패치된 VM에서는 일반적으로 디스크 정리를 실행하여 약 4GB의 디스크 공간을 확보할 수 있습니다.

다음은 다양한 디스크 정리 작업에 대한 제안 사항입니다. 구현하기 전에 모두 테스트해야 하는 제안 사항은 다음과 같습니다.

1. 모든 업데이트가 적용되면 관리자 권한으로 디스크 정리 마법사를 실행합니다. '배달 최적화' 및 'Windows 업데이트 정리' 범주를 포함시킵니다. 이 프로세스는 `/SAGESET:11` 옵션이 포함된 `Cleanmgr.exe` 명령줄을 사용하여 자동화할 수 있습니다. `/SAGESET` 옵션은 디스크 정리 마법사에서 나중에 사용 가능한 모든 옵션을 사용하여 디스크 정리를 자동화하는 데 사용할 수 있는 레지스트리 값을 설정합니다.

    1. 테스트 VM에서 새로 설치할 때 `Cleanmgr.exe /SAGESET:11`을 실행하면 기본적으로 다음 두 가지 자동 디스크 정리 옵션만 사용하도록 설정된 것으로 나타납니다.
    
        - 다운로드한 프로그램 파일

        - 임시 인터넷 파일

    2. 더 많은 옵션 또는 모든 옵션을 설정하는 경우 이러한 옵션은 이전 명령(`Cleanmgr.exe /SAGESET:11`)에서 제공하는 **인덱스** 값에 따라 레지스트리에 기록됩니다. 이 경우 후속 자동화 디스크 정리 절차에서 `11` 값을 인덱스로 사용합니다.

    3. `Cleanmgr.exe /SAGESET:11`이 실행되면 몇 가지 범주의 디스크 정리 옵션이 표시됩니다. 모든 옵션을 확인한 다음, **확인**을 클릭합니다. 디스크 정리 마법사가 사라지고 설정이 레지스트리에 저장됩니다.

2. 볼륨 섀도 복사본 스토리지를 사용하고 있는 경우 이 스토리지를 정리합니다.

    - 관리자 권한으로 명령 프롬프트를 열고, `vssadmin list shadows`, `vssadmin list shadowstorage` 명령을 차례로 실행합니다.
    
        이러한 명령의 출력이 **쿼리를 만족하는 항목이 없습니다.** 이면 사용하는 VSS 스토리지가 없는 것입니다.

3. 임시 파일 및 로그를 정리합니다. 관리자 권한 명령 프롬프트에서 `Del C:\*.tmp /s`, `Del C:\Windows\Temp\.` 및 `Del %temp%\.` 명령을 실행합니다.

4. `wmic path win32_UserProfile where LocalPath="c:\users\<user>" Delete`를 사용하여 시스템에서 사용하지 않은 프로필을 삭제합니다.

### <a name="remove-onedrive-components"></a>OneDrive 구성 요소 제거

OneDrive가 제거되면 패키지를 제거하고, 설치 제거를 수행하고, *.lnk 파일을 제거해야 합니다. 다음 PowerShell 코드 샘플을 사용하여 이미지에서 OneDrive를 제거하도록 지원할 수 있으며, 이는 GitHub VDI 최적화 스크립트에 포함되어 있습니다.

```azurecli

Taskkill.exe /F /IM "OneDrive.exe"
Taskkill.exe /F /IM "Explorer.exe"` 
    if (Test-Path "C:\\Windows\\System32\\OneDriveSetup.exe")`
     { Start-Process "C:\\Windows\\System32\\OneDriveSetup.exe"`
         -ArgumentList "/uninstall"`
         -Wait }
    if (Test-Path "C:\\Windows\\SysWOW64\\OneDriveSetup.exe")`
     { Start-Process "C:\\Windows\\SysWOW64\\OneDriveSetup.exe"`
         -ArgumentList "/uninstall"`
         -Wait }
Remove-Item -Path
"C:\\Windows\\ServiceProfiles\\LocalService\\AppData\\Roaming\\Microsoft\\Windows\\Start Menu\\Programs\\OneDrive.lnk" -Force
Remove-Item -Path "C:\\Windows\\ServiceProfiles\\NetworkService\\AppData\\Roaming\\Microsoft\\Windows\\Start Menu\\Programs\\OneDrive.lnk" -Force \# Remove the automatic start item for OneDrive from the default user profile registry hive
Start-Process C:\\Windows\\System32\\Reg.exe -ArgumentList "Load HKLM\\Temp C:\\Users\\Default\\NTUSER.DAT" -Wait
Start-Process C:\\Windows\\System32\\Reg.exe -ArgumentList "Delete HKLM\\Temp\\SOFTWARE\\Microsoft\\Windows\\CurrentVersion\\Run /v OneDriveSetup /f" -Wait
Start-Process C:\\Windows\\System32\\Reg.exe -ArgumentList "Unload HKLM\\Temp" -Wait Start-Process -FilePath C:\\Windows\\Explorer.exe -Wait
```

이 페이지에 제공되는 정보에 대해 질문이나 의견이 있는 경우 Microsoft 계정 팀에 문의하거나, Microsoft VDI 블로그를 살펴보거나, Microsoft 포럼에 메시지를 게시하거나, Microsoft에 질문이나 의견을 제공하세요.

## <a name="turn-windows-update-back-on"></a>Windows 업데이트 다시 설정

영구 VDI의 경우와 같이 Windows 업데이트를 다시 설정하려면 다음 단계를 수행합니다.

- 다음 그룹 정책 설정을 사용하도록 다시 설정합니다.

    - 로컬 컴퓨터 정책 \\ 컴퓨터 구성 \\ 관리 템플릿 \\ 시스템 \\ 인터넷 통신 관리 \\ 인터넷 통신 설정

        - 모든 Windows 업데이트 기능에 대한 액세스를 해제합니다(**사용**에서 **구성되지 않음**으로 변경).

    - 로컬 컴퓨터 정책 \\ 컴퓨터 구성 \\ 관리 템플릿 \\ Windows 구성 요소 \\ Windows 업데이트

        - 모든 Windows 업데이트 기능에 대한 액세스를 제거합니다(**사용**에서 **구성되지 않음**으로 변경).

        - Windows 업데이트 인터넷 위치에는 연결하지 않습니다(**사용**에서 **구성되지 않음**으로 변경).

    - 로컬 컴퓨터 정책 \\ 컴퓨터 구성 \\ 관리 템플릿 \\ Windows 구성 요소 \\ Windows 업데이트 \\ 비즈니스용 Windows 업데이트

        - 품질 업데이트를 받는 시기를 선택합니다('사용'에서 '구성되지 않음'으로 변경).

    -   로컬 컴퓨터 정책 \\ 컴퓨터 구성 \\ 관리 템플릿 \\ Windows 구성 요소 \\ Windows 업데이트 \\ 비즈니스용 Windows 업데이트

        - Preview 빌드 및 기능 업데이트 시기를 선택합니다(**사용**에서 **구성되지 않음**으로 변경).

-  서비스 다시 사용

    - Orchestrator 서비스를 업데이트합니다(**사용 안 함**에서 **자동(지연된 시작)** 으로 변경).

    - 다음 Windows 레지스트리 설정을 편집합니다.

        - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsUpdate\UpdatePolicy\PolicyState

            - DeferQualityUpdates(**1**에서 **0**으로 변경)

        - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsUpdate\UpdatePolicy\Settings

            - PausedQualityDate(기존 값 삭제)

        - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\Explorer\WAU

            - 사용 안 함

-  예약된 작업 다시 사용

    - 작업 스케줄러 라이브러리 \\ Microsoft \\ Windows \\ InstallService \\ ScanForUpdates

    - 작업 스케줄러 라이브러리 \\ Microsoft \\ Windows \\ InstallService \\ ScanForUpdatesAsUser

이러한 설정을 모두 적용하려면 디바이스를 다시 시작합니다. 이 디바이스에서 기능 업데이트를 제공하지 않으려면 설정 \\ Windows 업데이트 \\ 고급 옵션 \\ 업데이트 설치 시기 선택으로 이동하고, 다음 옵션을 수동으로 설정합니다. **기능 업데이트에는 새로운 기능과 개선이 포함됩니다. 다음 기간(일) 동안 180, 365 등과 같은 일부 0이 아닌 값으로 연기할 수 있습니다.**

### <a name="references"></a>참조

- [VDI(가상 데스크톱 인프라)란?](https://www.citrix.com/glossary/vdi.html)

- [기본 제공 Windows 이미지가 포함된 Microsoft Store 앱을 제거하거나 업데이트한 후 Sysprep이 실패함](https://support.microsoft.com/help/2769827/sysprep-fails-after-you-remove-or-update-windows-store-apps-that-inclu)
