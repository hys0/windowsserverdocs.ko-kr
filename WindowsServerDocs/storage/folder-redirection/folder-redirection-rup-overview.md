---
title: 폴더 리디렉션, 오프라인 파일 및 로밍 사용자 프로필 개요
description: 폴더 리디렉션, 오프라인 파일 및 로밍 사용자 프로필 기술 개요
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 04/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5f2e8a0816fdd78491c18e196a57a38734e3368e
ms.sourcegitcommit: 5bc5aaf341c711113ca03d1482f933b05b146007
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2020
ms.locfileid: "85094509"
---
# <a name="folder-redirection-offline-files-and-roaming-user-profiles-overview"></a>폴더 리디렉션, 오프라인 파일 및 로밍 사용자 프로필 개요

>적용 대상: Windows 10, Windows 8, Windows 8.1, Windows Server 2019, Windows Server 2016, Windows Server 2012, Windows Server 2012 R2

이 항목에서는 폴더 리디렉션, 오프라인 파일(클라이언트 쪽 캐싱 또는 CSC) 및 로밍 사용자 프로필(RUP라고도 함) 기술에 대해 설명하며, 이와 관련된 새로운 기술과 추가 정보 링크가 포함되어 있습니다.

## <a name="technology-description"></a>기술 설명

폴더 리디렉션과 오프라인 폴더를 함께 사용하면 문서 폴더와 같은 로컬 폴더의 경로를 네트워크 위치로 리디렉션할 수 있으며, 콘텐츠는 속도 및 가용성을 향상시키기 위해 로컬로 캐시됩니다. 로밍 사용자 프로필은 사용자 프로필을 네트워크 위치로 리디렉션하는 데 사용됩니다. 이러한 기능을 Intellimirror라고 합니다.

- **폴더 리디렉션**을 통해 사용자나 관리자는 수동으로 또는 그룹 정책을 사용해 알려진 폴더의 경로를 새 위치로 리디렉션할 수 있습니다. 새 위치는 로컬 컴퓨터의 폴더이거나 파일 공유의 디렉터리일 수 있습니다. 사용자는 리디렉션된 폴더의 파일이 마치 로컬 드라이브에 존재하는 것처럼 상호 작용할 수 있습니다. 예를 들어 로컬 드라이브에서 주로 저장되는 문서 폴더를 리디렉션할 수 있습니다. 사용자가 네트워크상의 모든 컴퓨터에서 폴더의 파일을 사용할 수 있습니다.
- **오프라인 파일** 을 통해 서버에 대한 네트워크 연결이 너무 느리거나 사용할 수 없더라도 사용자가 네트워크 파일을 사용할 수 있습니다. 온라인에서 작업할 때 파일 액세스 성능은 네트워크 및 서버 속도에 따라 달라집니다. 오프라인에서 작업할 경우 파일은 오프라인 파일 폴더에서 로컬 액세스 속도로 검색됩니다. 컴퓨터는 다음과 같은 경우 오프라인 모드로 전환됩니다.
  - **항상 오프라인** 모드가 사용하도록 설정된 경우
  - 서버를 사용할 수 없는 경우
  - 네트워크 연결이 구성 가능한 임계값보다 느린 경우
  - 사용자가 Windows 탐색기의 **오프라인으로 작업** 단추를 사용하여 오프라인 모드로 수동 전환한 경우
- **로밍 사용자 프로필**을 통해 사용자 프로필을 파일 공유로 리디렉션하여 사용자가 여러 컴퓨터에서 동일한 운영 체제 및 애플리케이션 설정을 받을 수 있도록 합니다. 사용자가 파일 공유를 통해 설정된 계정을 프로필 경로로 사용하여 컴퓨터에 로그인하면 이 사용자의 프로필이 로컬 컴퓨터에 다운로드되어 로컬 프로필(제공되는 경우)과 합쳐집니다. 사용자가 컴퓨터에서 로그오프하면 사용자 프로필의 로컬 복사본이 그동안 변경된 내용을 포함하여 프로필의 서버 복사본과 합쳐집니다. 일반적으로 네트워크 관리자는 도메인 계정에서 로밍 사용자 프로필을 사용하도록 설정합니다.

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
| 항상 오프라인 모드 | 새로 만들기 | 고속 네트워크 연결 기능을 통해 연결된 경우라도 항상 오프라인으로 작업해 파일 액세스 속도를 높이고 대역폭 사용량을 줄일 수 있습니다. |
| 비용 인식 동기화 | 새로 만들기 | 사용 한도가 있는 요금제 연결을 사용하거나 다른 공급자의 네트워크에서 로밍하는 동안 동기화로 인해 과도한 데이터를 사용하지 않도록 방지할 수 있습니다. |
| 기본 컴퓨터 지원 | 새로 만들기 | 폴더 리디렉션, 로밍 사용자 프로필 또는 이 두 가지를 모두 사용자의 기본 컴퓨터에 한해 사용하도록 제한할 수 있습니다. |

## <a name="always-offline-mode"></a>항상 오프라인 모드

Windows 8 및 Windows Server 2012부터 관리자는 사용자가 고속 네트워크 연결을 통해 연결되어 있더라도 항상 오프라인에서 작업할 수 있도록 오프라인 파일 사용자의 환경을 구성할 수 있습니다. Windows는 기본적으로 1시간마다 백그라운드 방식으로 동기화하여 오프라인 파일 캐시의 파일을 업데이트합니다.

### <a name="what-value-does-always-offline-mode-add"></a>항상 오프라인 모드에서 추가되는 값은 무엇인가요?

항상 오프라인 모드의 이점은 다음과 같습니다.

- 사용자는 문서 폴더 등 리디렉션된 폴더의 파일에 더 빠르게 액세스할 수 있습니다.
- 네트워크 대역폭이 줄어들어 값비싼 WAN 연결 비용이나 4G 모바일 네트워크 등의 요금제 연결 비용을 절감할 수 있습니다.

### <a name="how-has-always-offline-mode-changed-things"></a>항상 오프라인 모드를 변경하는 방법은 무엇인가요?

Windows 8, Windows Server 2012 이전에 사용자는 느린 링크 모드(저속 연결 모드라고도 함)가 사용되고 대기 시간 임계값이 1밀리초로 설정되었더라도 네트워크의 가용성과 상태에 따라 온라인 모드와 오프라인 모드를 전환했습니다.

항상 오프라인 모드를 사용하면 컴퓨터가 **느린 링크 모드 구성** 그룹 정책 설정이 구성되고 **대기 시간** 임계값 매개 변수가 1밀리초로 설정되어 있으면 온라인 모드로 전환되지 않습니다. 변경 내용은 기본적으로 120분마다 백그라운드에서 동기화됩니다. 동기화는 **Configure Background Sync** 그룹 정책 설정을 사용하여 구성할 수 있습니다.

자세한 내용은 [Enable the Always Offline Mode to Provide Faster Access to Files](enable-always-offline.md)를 참조하세요.

## <a name="cost-aware-synchronization"></a>비용 인식 동기화

비용 인식 동기화를 통해 Windows는 사용자가 4G 모바일 네트워크 등의 요금제 네트워크 연결을 사용하고 가입자가 자신의 대역폭 한계에 이르렀거나 이를 넘어선 경우 또는 다른 공급자의 네트워크에서 로밍하는 경우 백그라운드 동기화를 사용하지 않도록 설정합니다.

> [!NOTE]
> 요금제 네트워크 연결의 왕복 네트워크 대기 시간은 일반적으로 Windows 8, Windows Server 2019, Windows Server 2016 및 Windows Server 2012의 오프라인(저속 연결) 모드로 전환하기 위한 대기 시간의 기본값인 35밀리초보다 느립니다. 따라서 이러한 연결은 대개 오프라인(저속 연결) 모드로 자동 전환됩니다.

### <a name="what-value-does-cost-aware-synchronization-add"></a>비용 인식 동기화에 추가되는 값은 무엇인가요?

비용 인식 동기화 기능을 통해 사용자는 사용량이 제한된 요금제 연결을 사용하거나 다른 공급자의 네트워크에서 로밍하는 동안 데이터 사용료가 예기치 않게 많이 발생하는 일을 방지할 수 있습니다.

### <a name="how-has-cost-aware-synchronization-changed-things"></a>비용 인식 동기화를 변경하는 방법은 무엇인가요?

Windows 8 및 Windows Server 2012 이전에 요금제 네트워크 연결에서 오프라인 파일을 사용하는 동안 요금을 절감하려는 사용자는 모바일 네트워크 공급자의 도구를 사용해 데이터 사용량을 추적해야 했습니다. 그런 다음 자신의 대역폭 한계 부근이나 이를 넘어서는 곳에서 로밍하게 되면 오프라인 모드로 직접 전환해야 했습니다.

비용 인식 동기화를 통해 요금제 연결이 사용되는 동안 로밍 및 대역폭 사용 한도가 Windows에서 자동으로 추적됩니다. 사용자가 대역폭 한계 부근이나 이를 넘어서는 곳에서 로밍하면 Windows에서 오프라인 모드로 전환해 모든 동기화가 발생되지 않도록 합니다. 사용자가 직접 동기화를 시작할 수 있으며, 관리자는 회사 임원 등 특정 사용자의 비용 인식 동기화를 차단할 수 있습니다.

자세한 내용은 [Enable Background File Synchronization on Metered Networks](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj127408(v%3dws.11))를 참조하세요.

## <a name="primary-computers-for-folder-redirection-and-roaming-user-profiles"></a>폴더 리디렉션 및 로밍 사용자 프로필의 기본 컴퓨터

이제 도메인 사용자별로 기본 컴퓨터라는 컴퓨터 세트를 지정하여 폴더 리디렉션, 로밍 사용자 프로필 또는 이 두 가지를 모두 사용할 컴퓨터를 제어할 수 있습니다. 기본 컴퓨터 지정은 사용자 데이터와 설정을 특정 컴퓨터나 디바이스에 연결하여 관리자에게 편리한 관리 환경을 제공하고, 데이터 보안 성능을 향상시키며, 사용자 프로필이 손상되지 않도록 보호할 수 있는 간편하고 확실한 방법입니다.

### <a name="what-value-do-primary-computers-add"></a>기본 컴퓨터에 추가되는 값은 무엇인가요?

사용자의 기본 컴퓨터를 지정하면 다음과 같은 네 가지 이점을 누릴 수 있습니다.

- 관리자는 사용자가 리디렉션된 데이터와 설정에 액세스할 때 사용할 컴퓨터를 지정할 수 있습니다. 예를 들어 관리자는 데스크톱과 랩톱 중에서 사용자의 데이터와 설정이 로밍될 컴퓨터를 선택하고 사용자가 회의실 컴퓨터 등의 기타 컴퓨터에 로그온하면 정보를 로밍하지 않도록 선택할 수 있습니다.
- 기본 컴퓨터를 지정해 사용자가 로그온한 컴퓨터에 개인 또는 회사 데이터가 남아 있게 되는 보안 및 개인 정보 노출 위험을 줄일 수 있습니다. 예를 들어 일반 관리자가 직원 컴퓨터에 임시로 로그온하여 사용할 경우 어떤 개인 데이터나 회사 데이터도 남기지 않고 사용할 수 있습니다.
- 관리자는 기본 컴퓨터를 지정하여 x86 기반 컴퓨터와 x64 기반 컴퓨터처럼 서로 다르게 구성된 시스템 사이를 로밍하다가 부적절하게 구성되거나 프로필이 손상되는 위험을 줄일 수 있습니다.
- 사용자가 서버와 같이 기본 컴퓨터가 아닌 컴퓨터에 처음 로그인하면 사용자의 로밍 사용자 프로필 및/또는 리디렉션된 폴더가 다운로드되지 않으므로 더 빨리 로그인할 수 있습니다. 또한 변경된 사용자 프로필을 파일 공유에 업로드할 필요가 없으므로 로그아웃 시간도 단축됩니다.

### <a name="how-have-primary-computers-changed-things"></a>기본 컴퓨터는 어떻게 변경됩니까?

기본 컴퓨터에만 사용자 개인 데이터를 다운로드할 수 있도록 제한하기 위해 폴더 리디렉션 및 로밍 사용자 프로필 기술을 통해 사용자가 컴퓨터에 로그인할 때 다음과 같은 논리 점검을 수행합니다.

1. Windows 운영 체제는 새로운 그룹 정책 설정(**기본 컴퓨터에만 로밍 프로필 다운로드**와 **기본 컴퓨터에서만 폴더 리디렉션**)을 점검하여 AD DS(Active Directory Domain Services)의 **msDS-Primary-Computer** 특성에 따라 사용자 프로필이 로밍되고 폴더 리디렉션이 적용되도록 할 것인지 확인합니다.
2. 이 정책 설정에서 기본 컴퓨터가 지원되는 경우 Windows는 AD DS 스키마에서 **msDS-Primary-Computer** 특성을 지원하는 것으로 확인합니다. 또한 다음과 같이 사용자가 로그온한 컴퓨터가 기본 컴퓨터로 지정되어 있는지 확인합니다.
    1. 이 컴퓨터가 사용자의 기본 컴퓨터인 경우 Windows는 로밍 사용자 프로필과 폴더 리디렉션 설정을 적용합니다.
    2. 이 컴퓨터가 사용자의 기본 컴퓨터가 아닌 경우에는 사용자의 캐시된 로컬 프로필(있는 경우)을 로드하거나 새로운 로컬 프로필을 만듭니다. 또한 Windows는 로컬 폴더 리디렉션 구성에 그대로 남아 있는 경우 이전에 적용한 그룹 정책 설정에서 지정된 제거 작업에 따라 리디렉션된 기존 폴더를 모두 제거합니다.

자세한 내용은 [Deploy Primary Computers for Folder Redirection and Roaming User Profiles](deploy-primary-computers.md)를 참조하세요.

## <a name="hardware-requirements"></a>하드웨어 요구 사항

폴더 리디렉션, 오프라인 파일 및 로밍 사용자 프로필은 x64 기반 또는 x86 기반 컴퓨터에서만 지원되며, WOA(Windows on ARM) 기반 컴퓨터의 Windows에서는 지원되지 않습니다.

## <a name="software-requirements"></a>소프트웨어 요구 사항

기본 컴퓨터를 지정하려면 환경이 다음의 요구 사항을 충족해야 합니다.

- Windows Server 2012 스키마 및 조건이 포함되도록 AD DS(Active Directory Domain Services) 스키마를 업데이트해야 합니다(Windows Server 2012 이상 도메인 컨트롤러를 설치하면 스키마가 자동으로 업데이트됨). AD DS 스키마 업그레이드에 대한 자세한 내용은 [Windows Server 2016으로 도메인 컨트롤러 업그레이드](../../identity/ad-ds/deploy/upgrade-domain-controllers.md)를 참조하세요.
- 클라이언트 컴퓨터는 Windows 10, Windows 8.1, Windows 8, Windows Server 2019, Windows server 2016, Windows Server 2012 R2 또는 Windows Server 2012를 실행하고 관리하는 Active Directory 도메인에 가입해야 합니다.

## <a name="more-information"></a>자세한 정보

자세한 내용은 다음 리소스를 참조하세요.

| 콘텐츠 유형 | 참조 |
| --- | --- |
| 제품 평가 | [신뢰할 수 있는 파일 서비스와 스토리지로 정보 근로자 지원](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831495(v%3dws.11)>)<br>[오프라인 파일의 새로운 기능](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff183315(v=ws.10)>)(Windows 7 및 Windows Server 2008 R2)<br>[Windows Vista용 오프라인 파일의 새로운 기능](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-vista/cc749449(v=ws.10)>)<br>[Windows Vista의 오프라인 파일 변경 내용](<https://technet.microsoft.com/library/2007.11.offline.aspx>)(TechNet 매거진) |
| 배포 | [폴더 리디렉션, 오프라인 파일 및 로밍 사용자 프로필 배포](deploy-folder-redirection.md)<br>[최종 사용자 데이터 일원화 솔루션 구현: 폴더 리디렉션 및 오프라인 파일 기술 유효성 검사 및 배포](https://download.microsoft.com/download/3/0/1/3019A3DA-2F41-4F2D-BBC9-A6D24C4C68C4/Implementing%20an%20End-User%20Data%20Centralization%20Solution.docx)<br>[로밍 사용자 데이터 배포 관리 가이드](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-vista/cc766489(v=ws.10)>)<br>[Windows 7 컴퓨터에 대한 새로운 오프라인 파일 기능 구성 단계별 가이드](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff633429(v=ws.10)>)<br>[폴더 리디렉션 사용](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753996(v=ws.11)>)<br>[폴더 리디렉션 구현](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc737434(v=ws.10)>)(Windows Server 2003) |
| 도구 및 설정 | [MSDN의 오프라인 파일](https://msdn.microsoft.com/library/cc296092.aspx)<br>[오프라인 파일 그룹 정책 참조](https://msdn.microsoft.com/library/ms878937.aspx)(Windows 2000) |
| 커뮤니티 리소스 | [파일 및 스토리지 서비스 포럼](https://social.technet.microsoft.com/forums/windowsserver/home?forum=winserverfiles)<br>[Hey, Scripting Guy! Windows에서 오프라인 파일 기능을 사용하여 작업하는 방법을 알려주세요.](<https://blogs.technet.microsoft.com/heyscriptingguy/2009/06/02/hey-scripting-guy-how-can-i-enable-and-disable-offline-files/>)<br>[Hey, Scripting Guy! 오프라인 파일을 사용하거나 사용하지 않도록 설정하는 방법을 알려주세요.](<https://blogs.technet.microsoft.com/heyscriptingguy/2009/06/02/hey-scripting-guy-how-can-i-enable-and-disable-offline-files/>) |
| 관련 기술|[Windows Server의 ID 및 액세스](../../identity/identity-and-access.yml)<br>[Windows Server의 스토리지](../storage.yml)<br>[원격 액세스 및 서버 관리](../../remote/index.md) |
