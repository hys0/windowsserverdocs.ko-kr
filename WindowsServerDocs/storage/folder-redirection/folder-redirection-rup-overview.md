---
title: 폴더 리디렉션, 오프라인 파일 및 로밍 사용자 프로필 개요
description: 폴더 리디렉션, 오프라인 파일 및 로밍 사용자 프로필 기술에 대 한 개요입니다.
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 04/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: a7c37638e25fc0d16447ab57bf369255dab9c859
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/14/2020
ms.locfileid: "75950253"
---
# <a name="folder-redirection-offline-files-and-roaming-user-profiles-overview"></a>폴더 리디렉션, 오프라인 파일 및 로밍 사용자 프로필 개요

>적용 대상: Windows 10, Windows 8, Windows 8.1, Windows Server 2019, Windows Server 2016, windows Server 2012, Windows Server 2012 R2

이 항목에서는 새로운 기능 및 추가 정보를 찾을 수 있는 위치를 포함 하 여 폴더 리디렉션, 오프라인 파일 (클라이언트 쪽 캐싱 또는 CSC) 및 로밍 사용자 프로필 (RUP 라고도 함) 기술에 대해 설명 합니다.

## <a name="technology-description"></a>기술 설명

폴더 리디렉션과 오프라인 폴더를 함께 사용하면 문서 폴더와 같은 로컬 폴더의 경로를 네트워크 위치로 리디렉션할 수 있으며, 콘텐츠는 속도 및 가용성을 향상시키기 위해 로컬로 캐시됩니다. 로밍 사용자 프로필은 사용자 프로필을 네트워크 위치로 리디렉션하는 데 사용됩니다. 이러한 기능을 Intellimirror라고 합니다.

- **폴더 리디렉션** 를 사용 하면 사용자와 관리자가 알려진 폴더의 경로를 수동으로 또는 그룹 정책를 사용 하 여 새 위치로 리디렉션할 수 있습니다. 새 위치는 로컬 컴퓨터의 폴더이거나 파일 공유의 디렉터리일 수 있습니다. 사용자는 리디렉션된 폴더의 파일이 마치 로컬 드라이브에 존재하는 것처럼 상호 작용할 수 있습니다. 예를 들어 로컬 드라이브에서 주로 저장되는 문서 폴더를 리디렉션할 수 있습니다. 사용자가 네트워크상의 모든 컴퓨터에서 폴더의 파일을 사용할 수 있습니다.
- **오프라인 파일** 를 사용 하면 서버에 대 한 네트워크 연결을 사용할 수 없거나 속도가 느릴 때에도 사용자가 네트워크 파일을 사용할 수 있습니다. 온라인에서 작업할 때 파일 액세스 성능은 네트워크 및 서버 속도에 따라 달라집니다. 오프라인에서 작업할 경우 파일은 오프라인 파일 폴더에서 로컬 액세스 속도로 검색됩니다. 컴퓨터는 다음과 같은 경우 오프라인 모드로 전환됩니다.
  - **항상 오프 라인** 모드를 사용 하도록 설정
  - 서버를 사용할 수 없는 경우
  - 네트워크 연결이 구성 가능한 임계값보다 느린 경우
  - 사용자가 Windows 탐색기의 **오프라인으로 작업** 단추를 사용하여 오프라인 모드로 수동 전환한 경우
- **로밍 사용자 프로필** 사용자 프로필을 파일 공유로 리디렉션하여 사용자가 여러 컴퓨터에서 동일한 운영 체제 및 응용 프로그램 설정을 받을 수 있도록 합니다. 사용자가 파일 공유를 통해 설정 된 계정을 프로필 경로로 사용 하 여 컴퓨터에 로그인 하면 해당 사용자의 프로필이 로컬 컴퓨터에 다운로드 되어 로컬 프로필 (있는 경우)과 병합 됩니다. 사용자가 컴퓨터에서 로그오프하면 사용자 프로필의 로컬 복사본이 그동안 변경된 내용을 포함하여 프로필의 서버 복사본과 합쳐집니다. 일반적으로 네트워크 관리자는 도메인 계정에서 로밍 사용자 프로필을 사용 하도록 설정 합니다.

## <a name="practical-applications"></a>유용한 팁

관리자는 폴더 리디렉션, 오프라인 파일 및 로밍 사용자 프로필을 사용해 사용자 데이터와 설정이 저장되는 스토리지를 일원화하며, 네트워크 또는 서버의 가동이 중지되거나 오프라인 상태가 되더라도 사용자가 데이터에 액세스할 수 있도록 합니다. 아래 몇 가지 구체적인 팁이 나와 있습니다.

- 서버 기반 백업 도구를 사용하여 사용자 폴더와 설정을 백업하는 등의 관리 작업을 일원화할 수 있도록 클라이언트 컴퓨터의 데이터를 한곳으로 모읍니다.
- 네트워크나 서버의 가동이 중지되더라도 사용자는 계속해서 네트워크 파일에 액세스할 수 있습니다.
- 대역폭의 사용을 최적화하고, 오프사이트에 있는 회사 서버에서 호스팅되는 파일 및 폴더에 액세스하는 지점 사용자의 작업 환경을 향상시킵니다.
- 모바일 사용자가 오프라인으로 또는 속도가 느린 네트워크를 통해 작업하면서 네트워크 파일에 액세스할 수 있습니다.

## <a name="new-and-changed-functionality"></a>새로운 기능 및 변경된 기능

다음 표에서는 이번 릴리스에서 변경된 폴더 리디렉션, 오프라인 파일 및 로밍 사용자 프로필의 주요 기능 중 일부를 설명합니다.

| 기능 | 새로운 기능 또는 업데이트된 기능 | 설명 |
| --- | --- | --- |
| 항상 오프라인 모드 | 신규 항목 | 고속 네트워크 연결 기능을 통해 연결된 경우라도 항상 오프라인으로 작업해 파일 액세스 속도를 높이고 대역폭 사용량을 줄일 수 있습니다. |
| 비용 인식 동기화 | 신규 항목 | 사용자가 사용 한도가 있는 요금제 연결을 사용 하거나 다른 공급자의 네트워크에서 로밍 하는 동안 동기화에서 데이터 사용량이 많은 것을 방지할 수 있습니다. |
| 기본 컴퓨터 지원 | 신규 항목 | 를 사용 하 여 폴더 리디렉션, 로밍 사용자 프로필 또는 둘 다를 사용자의 기본 컴퓨터로 제한할 수 있습니다. |

## <a name="always-offline-mode"></a>항상 오프라인 모드

Windows 8 및 Windows Server 2012부터 관리자는 고속 네트워크 연결을 통해 연결 된 경우에도 항상 오프 라인으로 작업할 오프라인 파일 사용자의 환경을 구성할 수 있습니다. Windows는 기본적으로 1시간마다 백그라운드 방식으로 동기화하여 오프라인 파일 캐시의 파일을 업데이트합니다.

### <a name="what-value-does-always-offline-mode-add"></a>항상 오프 라인 모드에서 추가 되는 값은 무엇 인가요?

항상 오프라인 모드의 이점은 다음과 같습니다.

- 사용자는 문서 폴더 등 리디렉션된 폴더의 파일에 더 빠르게 액세스할 수 있습니다.
- 네트워크 대역폭이 줄어들어 값비싼 WAN 연결 비용이나 4G 모바일 네트워크 등의 요금제 연결 비용을 절감할 수 있습니다.

### <a name="how-has-always-offline-mode-changed-things"></a>항상 오프 라인 모드를 변경 하는 방법은 무엇 인가요?

Windows 8, Windows Server 2012 이전에는 저속 연결 모드 (저속 연결 모드 라고도 함)가 사용 되 고 1 밀리초로 설정 된 경우에도 사용자가 네트워크의 가용성과 상태에 따라 온라인 모드와 오프 라인 모드 사이를 전환 했습니다. 대기 시간 임계값입니다.

항상 오프 라인 모드를 사용 하면 **저속 연결 구성 모드** 그룹 정책 설정이 구성 되 고 **대기 시간** 임계값 매개 변수가 1 밀리초로 설정 된 경우 컴퓨터가 온라인 모드로 전환 되지 않습니다. 변경 내용은 기본적으로 120분마다 백그라운드에서 동기화됩니다. 동기화는 **Configure Background Sync** 그룹 정책 설정을 사용하여 구성할 수 있습니다.

자세한 내용은 [Enable the Always Offline Mode to Provide Faster Access to Files](enable-always-offline.md)를 참조하세요.

## <a name="cost-aware-synchronization"></a>비용 인식 동기화

비용 인식 동기화를 사용 하면 사용자가 4G 모바일 네트워크 등의 요금제 네트워크 연결을 사용 하 고 구독자가 대역폭 제한에 도달 하거나 다른 공급자의 네트워크에서 로밍 하는 경우 백그라운드 동기화를 사용 하지 않도록 설정 합니다.

> [!NOTE]
> 요금제 네트워크 연결에는 일반적으로 Windows 8, Windows Server 2019, Windows Server 2016 및 Windows Server에서 오프 라인 (저속 연결) 모드로 전환 하기 위한 기본 35 밀리초 대기 시간 값 보다 느린 왕복 네트워크 대기 시간이 있습니다. 2012. 따라서 이러한 연결은 대개 오프라인(저속 연결) 모드로 자동 전환됩니다.

### <a name="what-value-does-cost-aware-synchronization-add"></a>비용 인식 동기화에 추가 되는 값

비용 인식 동기화를 사용 하면 사용 한도가 있는 요금제 연결을 사용 하거나 다른 공급자의 네트워크에서 로밍 하는 동안 사용자가 예기치 않게 높은 데이터 사용 비용을 피할 수 있습니다.

### <a name="how-has-cost-aware-synchronization-changed-things"></a>비용 인식 동기화를 변경 하는 방법은 무엇 인가요?

Windows 8 및 Windows Server 2012 이전에는 요금제 네트워크 연결에 오프라인 파일를 사용 하는 동안 요금을 최소화 하려는 사용자는 모바일 네트워크 공급자의 도구를 사용 하 여 데이터 사용량을 추적 해야 했습니다. 그런 다음 자신의 대역폭 한계 부근이나 이를 넘어서는 곳에서 로밍하게 되면 오프라인 모드로 직접 전환해야 했습니다.

비용 인식 동기화를 통해 Windows는 데이터 통신 연결을 사용 하는 동안 로밍 및 대역폭 사용 제한을 자동으로 추적 합니다. 사용자가 대역폭 한계 부근이나 이를 넘어서는 곳에서 로밍하면 Windows에서 오프라인 모드로 전환해 모든 동기화가 발생되지 않도록 합니다. 사용자가 직접 동기화를 시작할 수 있으며, 관리자는 회사 임원 등 특정 사용자의 비용 인식 동기화를 차단할 수 있습니다.

자세한 내용은 [Enable Background File Synchronization on Metered Networks](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj127408(v%3dws.11))를 참조하세요.

## <a name="primary-computers-for-folder-redirection-and-roaming-user-profiles"></a>폴더 리디렉션 및 로밍 사용자 프로필의 기본 컴퓨터

이제 각 도메인 사용자에 대해 기본 컴퓨터 라는 컴퓨터 집합을 지정 하 여 폴더 리디렉션, 로밍 사용자 프로필 또는 둘 다를 사용 하는 컴퓨터를 제어할 수 있습니다. 기본 컴퓨터 지정은 사용자 데이터와 설정을 특정 컴퓨터나 디바이스에 연결하여 관리자에게 편리한 관리 환경을 제공하고, 데이터 보안 성능을 향상시키며, 사용자 프로필이 손상되지 않도록 보호할 수 있는 간편하고 확실한 방법입니다.

### <a name="what-value-do-primary-computers-add"></a>기본 컴퓨터에 추가 되는 값은 무엇 인가요?

사용자의 기본 컴퓨터를 지정하면 다음과 같은 네 가지 이점을 누릴 수 있습니다.

- 관리자는 사용자가 리디렉션된 데이터와 설정에 액세스할 때 사용할 컴퓨터를 지정할 수 있습니다. 예를 들어 관리자는 사용자의 데스크톱 및 랩톱 간에 사용자 데이터와 설정을 로밍 하 고 사용자가 회의실 컴퓨터 등의 다른 컴퓨터에 로그온 할 때 정보를 로밍되지 않도록 선택할 수 있습니다.
- 기본 컴퓨터를 지정해 사용자가 로그온한 컴퓨터에 개인 또는 회사 데이터가 남아 있게 되는 보안 및 개인 정보 노출 위험을 줄일 수 있습니다. 예를 들어 임시 액세스용 직원의 컴퓨터에 로그온 하는 일반 관리자는 개인 데이터 나 회사 데이터를 떠나지 않습니다.
- 관리자는 기본 컴퓨터를 지정하여 x86 기반 컴퓨터와 x64 기반 컴퓨터처럼 서로 다르게 구성된 시스템 사이를 로밍하다가 부적절하게 구성되거나 프로필이 손상되는 위험을 줄일 수 있습니다.
- 사용자의 로밍 사용자 프로필 및/또는 리디렉션된 폴더가 다운로드 되지 않기 때문에 서버와 같이 기본이 아닌 컴퓨터에서 사용자가 처음으로 로그인 하는 데 필요한 시간이 단축 됩니다. 또한 변경된 사용자 프로필을 파일 공유에 업로드할 필요가 없으므로 로그아웃 시간도 단축됩니다.

### <a name="how-have-primary-computers-changed-things"></a>기본 컴퓨터는 어떻게 변경 됩니까?

기본 컴퓨터에만 사용자 개인 데이터를 다운로드할 수 있도록 제한하기 위해 폴더 리디렉션 및 로밍 사용자 프로필 기술을 통해 사용자가 컴퓨터에 로그인할 때 다음과 같은 논리 점검을 수행합니다.

1. Windows 운영 체제는 새로운 그룹 정책 설정 (**기본 컴퓨터에만 로밍 프로필 다운로드** 와 **기본 컴퓨터 에서만 폴더 리디렉션**)을 확인 하 여 Active Directory Domain Services (AD DS)의 **의 msds-primary-computer** 특성이 사용자의 프로필을 로밍 하거나 폴더 리디렉션을 적용 하는 결정에 영향을 미치는지 확인 합니다.
2. 이 정책 설정에서 기본 컴퓨터가 지원되는 경우 Windows는 AD DS 스키마에서 **msDS-Primary-Computer** 특성을 지원하는 것으로 확인합니다. 또한 다음과 같이 사용자가 로그온한 컴퓨터가 기본 컴퓨터로 지정되어 있는지 확인합니다.
    1. 컴퓨터가 사용자의 기본 컴퓨터인 경우 Windows는 로밍 사용자 프로필과 폴더 리디렉션 설정을 적용 합니다.
    2. 컴퓨터가 사용자의 기본 컴퓨터 중 하나가 아닌 경우 Windows는 사용자의 캐시 된 로컬 프로필 (있는 경우)을 로드 하거나 새 로컬 프로필을 만듭니다. 또한 Windows는 로컬 폴더 리디렉션 구성에 그대로 남아 있는 경우 이전에 적용한 그룹 정책 설정에서 지정된 제거 작업에 따라 리디렉션된 기존 폴더를 모두 제거합니다.

자세한 내용은 [Deploy Primary Computers for Folder Redirection and Roaming User Profiles](deploy-primary-computers.md)를 참조하세요.

## <a name="hardware-requirements"></a>하드웨어 요구 사항

폴더 리디렉션, 오프라인 파일 및 로밍 사용자 프로필은 x64 기반 또는 x86 기반 컴퓨터에서만 지원되며, WOA(Windows on ARM) 기반 컴퓨터의 Windows에서는 지원되지 않습니다.

## <a name="software-requirements"></a>소프트웨어 요구 사항

기본 컴퓨터를 지정하려면 환경이 다음의 요구 사항을 충족해야 합니다.

- Windows Server 2012 스키마 및 조건을 포함 하도록 Active Directory Domain Services (AD DS) 스키마를 업데이트 해야 합니다. Windows Server 2012 이상 도메인 컨트롤러를 설치 하면 스키마가 자동으로 업데이트 됩니다. AD DS 스키마를 업그레이드 하는 방법에 대 한 자세한 내용은 [Windows Server 2016로 도메인 컨트롤러 업그레이드](../../identity/ad-ds/deploy/upgrade-domain-controllers.md)를 참조 하세요.
- 클라이언트 컴퓨터는 Windows 10, Windows 8.1, Windows 8, Windows Server 2019, Windows server 2016, Windows Server 2012 R2 또는 Windows Server 2012을 실행 하 고 관리 하는 Active Directory 도메인에 가입 해야 합니다.

## <a name="more-information"></a>추가 정보

자세한 내용은 다음 리소스를 참조하세요.

| 콘텐츠 형식 | 참조 |
| --- | --- |
| 제품 평가 | [신뢰할 수 있는 파일 서비스 및 저장소로 정보 근로자 지원](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831495(v%3dws.11)>)<br>[오프라인 파일의 새로운 기능](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff183315(v=ws.10)>) (windows 7 및 windows Server 2008 R2)<br>[Windows Vista 오프라인 파일의 새로운 기능](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-vista/cc749449(v=ws.10)>)<br>[Windows Vista의 오프라인 파일에 대 한 변경 내용](<https://technet.microsoft.com/library/2007.11.offline.aspx>) (TechNet Magazine) |
| 배포 | [폴더 리디렉션, 오프라인 파일 및 로밍 사용자 프로필 배포](deploy-folder-redirection.md)<br>[최종 사용자 데이터 중앙화 솔루션 구현: 폴더 리디렉션 및 오프라인 파일 기술 유효성 검사 및 배포](https://download.microsoft.com/download/3/0/1/3019A3DA-2F41-4F2D-BBC9-A6D24C4C68C4/Implementing%20an%20End-User%20Data%20Centralization%20Solution.docx)<br>[로밍 사용자 데이터 배포 관리 가이드](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-vista/cc766489(v=ws.10)>)<br>[Windows 7 컴퓨터에 대한 새로운 오프라인 파일 기능 구성 단계별 가이드](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff633429(v=ws.10)>)<br>[폴더 리디렉션 사용](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753996(v=ws.11)>)<br>[폴더 리디렉션 구현](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc737434(v=ws.10)>) (Windows Server 2003) |
| 도구 및 설정 | [MSDN의 오프 라인 파일](https://msdn.microsoft.com/library/cc296092.aspx)<br>[오프라인 파일 그룹 정책 참조](https://msdn.microsoft.com/library/ms878937.aspx) (Windows 2000) |
| 커뮤니티 리소스 | [파일 서비스 및 저장소 포럼](https://social.technet.microsoft.com/forums/windowsserver/home?forum=winserverfiles)<br>[Scripting! Windows에서 오프라인 파일 기능을 사용 하려면 어떻게 해야 하나요?](<https://blogs.technet.microsoft.com/heyscriptingguy/2009/06/02/hey-scripting-guy-how-can-i-enable-and-disable-offline-files/>)<br>[Scripting! 오프라인 파일를 사용 하거나 사용 하지 않도록 설정 하려면 어떻게 해야 하나요?](<https://blogs.technet.microsoft.com/heyscriptingguy/2009/06/02/hey-scripting-guy-how-can-i-enable-and-disable-offline-files/>) |
| 관련 기술|[Windows Server에서 id 및 액세스](../../identity/identity-and-access.md)<br>[Windows Server의 스토리지](../storage.md)<br>[원격 액세스 및 서버 관리](../../remote/index.md) |