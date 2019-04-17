---
title: 폴더 리디렉션, 오프 라인 파일 및 로밍 사용자 프로필 개요
description: 폴더 리디렉션, 오프 라인 파일 및 로밍 사용자 프로필 기술 개요입니다.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 04/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4e3cf32cd718b906f16fc09901284d8520177df8
ms.sourcegitcommit: 375e94dc70c76e7aa5679c32f0f4dbc26cf7dd83
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2018
ms.locfileid: "2233499"
---
# <a name="folder-redirection-offline-files-and-roaming-user-profiles-overview"></a>폴더 리디렉션, 오프 라인 파일 및 로밍 사용자 프로필 개요

>적용 대상: 10 Windows, Windows 8, Windows 8.1, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016

폴더 리디렉션, (클라이언트쪽 캐싱 또는 CSC), 오프 라인 파일 및 로밍 사용자 프로필 (RUP 라고도 함) 기술, 새로운 기능 및 추가 정보를 찾을 수 있는 위치를 포함 하 여이 항목에 설명 합니다.

## <a name="technology-description"></a>기술 설명

폴더 리디렉션과 오프라인 폴더를 함께 사용하면 문서 폴더와 같은 로컬 폴더의 경로를 네트워크 위치로 리디렉션할 수 있으며, 콘텐츠는 속도 및 가용성을 향상시키기 위해 로컬로 캐시됩니다. 로밍 사용자 프로필은 사용자 프로필을 네트워크 위치로 리디렉션하는 데 사용됩니다. 이러한 기능 Intellimirror 라고 하는 데 사용 됩니다.

- **폴더 리디렉션** 사용자 및 관리자가 그룹 정책을 사용 하 여 수동으로 또는 알려진된 폴더의 경로 새 위치로 리디렉션할 수 있습니다. 새 위치는 로컬 컴퓨터의 폴더 또는 파일 공유에 디렉터리를 수 있습니다. 사용자가 로컬 드라이브에 여전히 존재 하는 경우에 따라 리디렉션된 폴더의 파일와 상호작용 합니다. 예, 네트워크 위치에 일반적으로 로컬 드라이브에 저장 되는 문서 폴더를 리디렉션할 수 있습니다. 폴더의 파일은 다음 사용할 수 있는 사용자에 게 네트워크에 있는 모든 컴퓨터에서 합니다.
- **오프 라인 파일** 네트워크 파일을 사용할 수 있도록 사용자, 서버에 네트워크 연결을 사용할 수 없음 또는 저속 하는 경우에 있습니다. 온라인에서 작업 하는 경우 네트워크 및 서버 속도 수준의 파일 액세스 성능이 제공 됩니다. 오프 라인으로 작업 하는 경우 파일에 있는 오프 라인 파일 폴더에 대 한 로컬 액세스 속도에서 검색 됩니다. 오프 라인 모드를 전환 하는 컴퓨터는 경우:
  - **항상 오프 라인** 모드를 사용 하도록 설정 된
  - 서버를 사용할 수 없는 경우
  - 네트워크 연결이 구성 가능한 임계값 보다 속도가 느린
  - 사용자 수동으로 전환 하는 오프 라인 모드를 Windows 탐색기에서 **오프 라인으로 작업** 단추를 사용 하 여
- **로밍 사용자 프로필을** 는 같은 운영 체제 및 응용 프로그램 설정을 여러 대의 컴퓨터에서 사용자가 받을 수 있도록 파일 공유에 사용자 프로필을 리디렉션합니다. 사용자에 로그인 할 때 컴퓨터에 프로필 경로와 파일 공유를 사용 하 여 설정 되는 계정을 사용 하 여, 사용자의 프로필 로컬 컴퓨터에 다운로드를 업데이트 하 고 (있는 경우) 로컬 프로필로 병합 됩니다. 사용자 컴퓨터에서 로그인을 할 때 변경 내용을 포함 하 여 사용자 프로필의 로컬 복사본과 서버 복사본 프로필의 병합 됩니다. 일반적으로 네트워크 관리자가 도메인 계정에서 로밍 사용자 프로필 수 있습니다.

## <a name="practical-applications"></a>유용한 팁

사용자 데이터 및 설정에 대 한 저장소를 중앙 집중화 하 고 사용자가 오프 라인 또는 네트워크 또는 서버 중단 발생 시 하는 동안 자신의 데이터에 액세스 하는 기능 들에 게 관리자는 폴더 리디렉션, 오프 라인 파일 및 로밍 사용자 프로필을 사용할 수 있습니다. 일부 특정 응용 프로그램은 다음과 같습니다.

- 서버 기반 백업 도구를 사용 하 여 사용자 폴더 및 설정을 백업 등의 관리 작업에 대 한 클라이언트 컴퓨터에서 데이터를 중앙 집중화 합니다.
- 네트워크 또는 서버 중단 경우에 계속 네트워크 파일에 액세스 하는 사용자를 사용 하도록 설정 합니다.
- 대역폭 사용량을 최적화 하 고 파일 및 폴더에 있는 회사 서버 오프 사이트에서 호스팅하는 액세스 하는 지사에 있는 사용자 환경을 향상.
- 저속 네트워크를 통해 오프 라인으로 작업 하는 동안 네트워크 파일에 액세스 하는 모바일 사용자를 사용 하도록 설정 합니다.

## <a name="new-and-changed-functionality"></a>새로운 기능 및 변경된 기능

다음 표에서에서는 폴더 리디렉션, 오프 라인 파일 및이 버전에서 사용할 수 있는 로밍 사용자 프로필의 주요 변경 중 일부에 대해 설명 합니다.

|기능|새로운 기능 또는 업데이트된 기능|설명|
|---|---|---|
|항상 오프 라인 모드|신규|고속 네트워크 연결을 통해 연결 하는 경우에 항상 오프 라인으로 작업 하 여 파일 및 낮은 대역폭 사용량에 대 한 빠른 액세스를 제공 합니다.|
|비용을 인식 동기화|신규|사용 현황 제한이 있는 측정 기능이 연결을 사용 하는 동안 또는 다른 공급자 네트워크에서 로밍 하는 동안 동기화에서 높은 데이터 사용 비용을 방지 하기 위한 하는데 도움이 됩니다.|
|기본 컴퓨터 지원|신규|폴더 리디렉션, 로밍 사용자 프로필 또는 둘 모두를 사용자의 기본 컴퓨터만 사용을 제한할 수 있습니다.|

## <a name="always-offline-mode"></a>항상 오프 라인 모드

관리자가 Windows 8 및 Windows Server 2012 부터는 항상 오프 라인으로 작업, 고속 네트워크 연결을 통해 연결 때도 오프 라인 파일의 사용자의 경험을 구성할 수 있습니다. Windows는 백그라운드에서 기본적으로 1 시간 마다 동기화 하 여 오프 라인 파일 캐시에서 파일을 업데이트 합니다.

### <a name="what-value-does-always-offline-mode-add"></a>어떤 값은 항상 오프 라인 모드 추가?

항상 오프 라인 모드에는 다음과 같은 이점이 있습니다.

- 사용자가 문서 폴더와 같은 리디렉션된 폴더의 파일에 빠르게 액세스할을 경험이 있어야 합니다.
- 네트워크 대역폭 reduced, 비용이 많이 드는 WAN 연결 또는 4 G 모바일 네트워크와 같은 측정 기능이 연결에 대해 비용 감소 합니다.

### <a name="how-has-always-offline-mode-changed-things"></a>항상 오프 라인 모드는 작업을 변경 하는 방법

Windows 8, Windows Server 2012 하기 전에 사용자가 사이 전환 온라인 및 오프 라인 모드에 따라 네트워크 가용성 및 조건, 느린 링크 모드 (저속 연결 모드 라고도 함)가 사용 하도록 설정 하 고 1 밀리초로 설정 하는 경우에 대기 시간 임계값입니다.

항상 오프 라인 모드와 컴퓨터 하지 전환 온라인 모드에 **느린 링크 모드를 구성** 하는 그룹 정책 설정 구성 된 **대기 시간** 임계값 매개 변수는 1 밀리초로 설정 된 경우. 변경 내용이 동기화는 백그라운드에서 120 분 마다 기본적으로 하지만 **배경 동기화 구성** 그룹 정책 설정을 사용 하 여 동기화가 구성할 수 있습니다.

자세한 내용은 [항상 오프 라인 모드를 제공 속도에 대 한 액세스 파일을 사용 하도록 설정](enable-always-offline.md)을 참조 하십시오.

## <a name="cost-aware-synchronization"></a>비용을 인식 동기화

비용을 인식 동기화와 Windows 사용자와 같이 4 G 모바일 네트워크와 구독자 근처 또는 자신의 대역폭 제한을 초과 측정 기능이 네트워크 연결을 사용 하 여 되었거나 다른 공급자 네트워크에서 로밍 하는 경우 배경 동기화를 비활성화 합니다.

>[!NOTE]
>측정 기능이 네트워크 연결에는 일반적으로 Windows 8, Windows Server 2012 및 Windows Server 2016에서 오프 라인 (저속 연결) 모드를 전환에 대 한 기본 35 밀리초 대기 시간 값 보다 속도가 느릴 수 있는 왕복 네트워크 대기 시간이 합니다. 따라서 이러한 연결은 일반적으로 전환 오프 라인 (저속 연결) 모드를 자동으로 합니다.

### <a name="what-value-does-cost-aware-synchronization-add"></a>어떤 값은 비용을 인식 동기화 추가 (영문)

비용을 인식 동기화 사용 현황 제한이 있는 측정 기능이 연결을 사용 하는 동안 또는 다른 공급자 네트워크에서 로밍 하는 동안 예기치 않게 높은 데이터 사용 비용을 방지 하기 위한 도움이 됩니다.

### <a name="how-has-cost-aware-synchronization-changed-things"></a>비용을 인식 동기화 작업을 변경 하는 방법을?

Windows 8 및 Windows Server 2012 하기 전에 사용자에 게 측정 기능이 네트워크 연결에서 오프 라인 파일을 사용 하는 동안 요금을 최소화 하는 이와 더불어 모바일 네트워크 공급자에서 도구를 사용 하 여 자신의 데이터 사용 추적 해야 했습니다. 사용자 수 다음 수동으로 전환 로밍 된 대로 때 오프 라인 모드, 대역폭 제한 자신의 근처 자신의 한도 초과 합니다.

비용을 인식 동기화와 Windows 측정 기능이 연결에 대 한 로밍 및 대역폭 사용 현황 제한은 자동으로 추적 합니다. 사용자 로밍 자신의 대역폭 제한 근처 또는 해당 제한을 초과 하는 경우 Windows 오프 라인 모드를 전환 하 고 모든 동기화 되지 않습니다. 사용자 동기화를 수동으로 시작할 수 있습니다 및 관리자가 임원 등의 특정 사용자에 대 한 비용을 인식 동기화를 재정의할 수 있습니다.

자세한 내용은 [계측 네트워크에 배경 파일 동기화를 사용 하도록 설정](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj127408(v%3dws.11))을 참조 하십시오.

## <a name="primary-computers-for-folder-redirection-and-roaming-user-profiles"></a>폴더 리디렉션 및 로밍 사용자 프로필에 대 한 기본 컴퓨터

이제 제어 폴더 리디렉션, 로밍 사용자 프로필 또는 모두를 사용 하는 컴퓨터에 수 있는 각 도메인 사용자에 대 한 기본 컴퓨터 라고 하는 컴퓨터의 집합을 지정할 수 있습니다. 지정 하는 기본 컴퓨터 이며 사용자 데이터 및 설정을 특정 컴퓨터 또는 장치를 연결 하는 간단 하 고 강력한 방법 관리자 감독 단순화, 데이터 보안을 향상 시킬 손상에서 사용자 프로필을 보호 합니다.

### <a name="what-value-do-primary-computers-add"></a>기본 컴퓨터 어떤 값을 추가 하려면?

지정 하는 사용자에 대 한 기본 컴퓨터에 대 한 4 개의 주요 장점 가지가 있습니다.

- 관리자가 사용자가 자신의 리디렉션된 데이터 및 설정에 액세스 하는데 사용할 수 있는 컴퓨터를 지정할 수 있습니다. 등 관리자가 사용자의 데스크톱 및 랩톱 사이의 사용자 데이터 및 설정 로밍 하 고 해당 사용자가 전화 회의 룸 컴퓨터 등의 다른 컴퓨터에 로그온 할 때 정보를 로밍 안함 선택할 수 있습니다.
- 기본 컴퓨터를 지정 하는 보안 및 개인정보 보호 위험에 사용자가 로그온 하는 컴퓨터에 남아 있는 개인 또는 회사 데이터를 유지 줄어듭니다. 예, 개인 또는 회사 데이터 뒤에 임시 액세스에 대 한 직원의 컴퓨터에 로그온 하는 일반 관리자 남지 않습니다.
- 잘못 구성 된 위험을 완화 하기 위해 관리자를 사용 하는 기본 컴퓨터 하거나 그렇지 않은 경우 다르게 로밍 사이 발생할 수 있는 손상 된 프로필 구성 시스템을 같은 x86 및 x64 기반 컴퓨터 간에.
- 사용자의 로밍 사용자 프로필 및/또는 리디렉션된 폴더 다운로드 되지 않으므로 사용자의 첫번째 로그인에 서버와 같은 기본이 아닌 컴퓨터에 필요한 시간이 빠릅니다. 사용자 프로필의 변경 내용은 파일 공유로 업로드 필요가 없습니다 때문에 로그 아웃 시간이 감소 됩니다.

### <a name="how-have-primary-computers-changed-things"></a>기본 컴퓨터 작업을 어떻게 변경 되었는지를?

기본 컴퓨터로 다운로드 하는 개인 사용자 데이터를 제한 하려면 폴더 리디렉션 및 로밍 사용자 프로필 기술 사용자 컴퓨터에 로그인 할 때 다음과 같은 논리 검사를 수행 합니다.

1. 활성의 특성 **기본 컴퓨터** 하는 경우를 확인 하려면 새 그룹 정책 설정 (**기본 컴퓨터 에서만 다운로드 로밍 프로필** 및 **기본 컴퓨터 에서만 리디렉션 폴더**)를 확인 하는 Windows 운영 체제 Directory 도메인 서비스 (AD DS) 로밍 사용자 프로필 또는 폴더 리디렉션을 적용할를 결정을 해야 영향을 줍니다.
2. 정책 설정의 기본 컴퓨터 지원을 사용 하도록 설정 하는 경우 Windows AD DS 스키마는 **주 컴퓨터** 특성을 지원 하는지 확인 합니다. 오류가 있으면 사용자가 로그온 하는 컴퓨터의 사용자에 대 한 기본 컴퓨터도 다음과 같은 지정 된 경우 Windows 결정 합니다.
    1. 컴퓨터가 사용자의 기본 컴퓨터 중 하나에 하는 경우 Windows에서 로밍 사용자 프로필 및 폴더 리디렉션 설정을 적용 합니다.
    2. 컴퓨터 사용자의 기본 컴퓨터 중 하나가 아닌 경우 Windows 사용자의 캐시 된 로컬 프로필을 로드 하는 경우이 매개 변수 또는 새 로컬 프로필을 만듭니다. 또한 Windows 로컬 폴더 리디렉션을 구성에서 보존 되는 이전에 적용 된 그룹 정책 설정에 의해 지정 된 제거 작업에 따라 모든 기존 리디렉션된 폴더를 제거 합니다.

자세한 내용은 [폴더 리디렉션 및 로밍 사용자 프로필에 대 한 기본 컴퓨터 배포](deploy-primary-computers.md) 를 참조 하십시오.

## <a name="hardware-requirements"></a>하드웨어 요구 사항

폴더 리디렉션, 오프 라인 파일 및 로밍 사용자 프로필에는 x86 기반 또는 x64 기반 컴퓨터 필요 하 고는 지원 되지 않으므로 Windows에서 ARM WOA 기반 컴퓨터에서 키를 누릅니다.

## <a name="software-requirements"></a>소프트웨어 요구 사항

기본 컴퓨터를 지정 하려면 환경의 다음 요구 사항을 충족 해야 합니다.

- Windows Server 2012 스키마와 조건을 포함 하도록 Active Directory 도메인 서비스 (AD DS) 스키마를 업데이트 해야 합니다 (스키마 업데이트는 Windows Server 2012 또는 이상 도메인 컨트롤러를 자동으로 설치). AD DS 스키마를 업그레이드 하는 방법에 대 한 자세한 내용은 [Windows Server 2016 하기 위해 도메인 컨트롤러 업그레이드](../../identity/ad-ds/deploy/upgrade-domain-controllers.md)를 참조 하십시오.
- 클라이언트 컴퓨터 Windows 10, Windows 8.1, Windows 8, Windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012를 실행 해야 하 고 관리 하는 Active Directory 도메인에 가입 합니다.

## <a name="more-information"></a>자세한 정보

자세한 내용은 다음 리소스를 참조하세요.

|콘텐츠 유형|참조|
|---|---|
|제품 평가|[신뢰할 수 있는 파일 서비스 및 저장소 정보 근로자 지원](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831495(v%3dws.11)>)<br>[오프 라인 파일의 새로운 란](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff183315(v=ws.10)>) (Windows 7 및 Windows Server 2008 R2)<br>[Windows Vista에 대 한 오프 라인 파일의 새 소식](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-vista/cc749449(v=ws.10)>)<br>[Windows Vista에서 오프 라인 파일의 변경](<https://technet.microsoft.com/library/2007.11.offline.aspx>) (TechNet Magazine) (영문)|
|배포|[폴더 리디렉션, 오프 라인 파일 및 로밍 사용자 프로필을 배포 합니다.](deploy-folder-redirection.md)<br>[최종 사용자 데이터 중앙 집중화 솔루션을 구현: 폴더 리디렉션 및 오프 라인 파일 기술 유효성 검사 및 배포](http://download.microsoft.com/download/3/0/1/3019A3DA-2F41-4F2D-BBC9-A6D24C4C68C4/Implementing%20an%20End-User%20Data%20Centralization%20Solution.docx)<br>[로밍 사용자 데이터 배포 가이드 관리](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-vista/cc766489(v=ws.10)>)<br>[Windows 7 컴퓨터에 대 한 단계별 가이드에 대 한 기능 파일을 새로운 오프 라인으로 구성](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff633429(v=ws.10)>)<br>[폴더 리디렉션 사용](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753996(v=ws.11)>)<br>[폴더 리디렉션 구현](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc737434(v=ws.10)>) (Windows Server 2003)|
|도구 및 설정|[MSDN에서 오프 라인 파일](https://msdn.microsoft.com/library/cc296092.aspx)<br>[오프 라인 파일 그룹 정책 참조 (영문)](https://msdn.microsoft.com/library/ms878937.aspx) (Windows 2000)|
|커뮤니티 리소스|[파일 및 저장소 서비스 포럼](https://social.technet.microsoft.com/forums/windowsserver/home?forum=winserverfiles)<br>[안녕하세요, Scripting Guy! Windows에서 오프 라인 파일 기능을 어떻게 작업할 수 있습니까?](<https://blogs.technet.microsoft.com/heyscriptingguy/2009/06/02/hey-scripting-guy-how-can-i-enable-and-disable-offline-files/>)<br>[안녕하세요, Scripting Guy! 활성화 및 오프 라인 파일을 비활성화할 수 어떻게 합니까?](<https://blogs.technet.microsoft.com/heyscriptingguy/2009/06/02/hey-scripting-guy-how-can-i-enable-and-disable-offline-files/>)|
관련 기술|[Id 및 Windows Server에 액세스](../../identity/identity-and-access.md)<br>[WindowsServer의 저장소](../storage.md)<br>[원격 액세스 및 서버 관리](../../remote/index.md)|