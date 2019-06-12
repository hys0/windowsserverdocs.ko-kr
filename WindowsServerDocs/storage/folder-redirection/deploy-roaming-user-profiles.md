---
Title: 로밍 사용자 프로필 배포
TOCTitle: Deploying Roaming User Profiles
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.date: 06/07/2019
ms.author: jgerend
ms.openlocfilehash: e6e2e32ff9aeb1b3bcfc8fed9027c7e92e13b118
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812489"
---
# <a name="deploying-roaming-user-profiles"></a>로밍 사용자 프로필 배포

>적용 대상: Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Server 2019, Windows Server 2016, Windows Server (반기 채널), Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

이 항목에서는 Windows Server 배포를 사용 하는 방법 설명 [로밍 사용자 프로필](folder-redirection-rup-overview.md) Windows 클라이언트 컴퓨터에 있습니다. 사용자가 동일한 운영 체제 및 여러 컴퓨터에서 응용 프로그램 설정을 받을 수 있도록 사용자 프로필을 파일 공유로 리디렉션하여 로밍 사용자 프로필입니다.

최근의 변경 내용은이 항목의 목록에 대 한 참조를 [변경 내용](#change-history) 이 항목의 섹션입니다.

> [!IMPORTANT]
> 보안 변경 내용으로 인해 [MS16 072](https://support.microsoft.com/help/3163622/ms16-072-security-update-for-group-policy-june-14%2c-2016)를 업데이트 했습니다 [4 단계: 필요에 따라 로밍 사용자 프로필에 대 한 GPO를 만들어](#step-4-optionally-create-a-gpo-for-roaming-user-profiles) 해당 Windows 고 수 있도록 제대로 로밍 사용자 프로필 정책 적용 (영향을 받는 Pc에서 로컬 정책으로 전환 되지 않고)이이 항목의 합니다.

> [!IMPORTANT]
>  사용자 지정 시작 하려면 다음 구성에서 OS의 전체 업그레이드 후 손실 됩니다.
> - 사용자가 로밍 프로필에 대 한 구성
> - 시작을 변경 하려면 사용자 수
>
> 결과적으로, 시작 메뉴는 OS 업그레이드 한 후 새 OS 버전의 기본으로 재설정 됩니다. 해결 방법은 [부록 c: 작업 업그레이드 한 후 시작 메뉴 레이아웃을 약 재설정](#appendix-c-working-around-reset-start-menu-layouts-after-upgrades)합니다.

## <a name="prerequisites"></a>사전 요구 사항

### <a name="hardware-requirements"></a>하드웨어 요구 사항

X64 기반 또는 x86 기반 컴퓨터는 필요한 로밍 사용자 프로필 Windows rt 지원 되지 않습니다.

### <a name="software-requirements"></a>소프트웨어 요구 사항

로밍 사용자 프로필에 대한 소프트웨어 요구 사항은 다음과 같습니다.

- 기존 로컬 사용자 프로필이 있는 환경에 폴더 리디렉션과 함께 로밍 사용자 프로필을 배포하는 경우 로밍 사용자 프로필 전에 폴더 리디렉션을 배포하여 로밍 프로필의 크기를 최소화합니다. 기존 사용자 폴더가 리디렉션되고 나면 로밍 사용자 프로필을 배포할 수 있습니다.
- 로밍 사용자 프로필을 관리하려면 Domain Administrators 보안 그룹, Enterprise Administrators 보안 그룹 또는 Group Policy Creator Owners 그룹의 구성원으로 로그인해야 합니다.
- 클라이언트 컴퓨터는 Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Vista, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 또는 Windows Server 2008 실행 해야 합니다.
- 현재 관리 중인 AD DS(Active Directory 도메인 서비스)에 클라이언트 컴퓨터가 가입되어 있어야 합니다.
- 그룹 정책 관리 및 설치된 Active Directory 관리 센터에서 컴퓨터를 사용할 수 있어야 합니다.
- 파일 서버를 사용하여 로밍 사용자 프로필을 호스트할 수 있어야 합니다.

    - 파일 공유에서 DFS 네임스페이스를 사용하는 경우 사용자가 서로 다른 서버에서 충돌하는 편집 작업을 수행하지 못하도록 DFS 폴더(링크)에 단일 대상이 있어야 합니다.
    - 파일 공유에서 DFS 복제를 사용하여 다른 서버에 콘텐츠를 복제하는 경우 사용자가 서로 다른 서버에서 충돌하는 편집 작업을 수행하지 못하도록 원본 서버에만 액세스할 수 있도록 해야 합니다.
    - 파일 공유가 클러스터된 경우 성능 문제를 방지하려면 파일 공유에서 지속적인 가용성을 사용하지 않도록 설정합니다.
- 로밍 사용자 프로필의 기본 컴퓨터 지원을 사용 하려면은 추가 클라이언트 컴퓨터 및 Active Directory 스키마 요구 사항입니다. 자세한 내용은 [폴더 리디렉션 및 로밍 사용자 프로필에 대 한 기본 컴퓨터 배포](deploy-primary-computers.md)합니다.
- 레이아웃 둘 이상 PC, 원격 데스크톱 세션 호스트 또는 가상화 된 데스크톱 인프라 (VDI) 서버를 사용 하 든 Windows 10, Windows Server 2019 또는 Windows Server 2016에서 메뉴 로밍되지 사용자의 시작입니다. 해결 방법으로이 항목에 설명 된 대로 시작 레이아웃을 지정할 수 있습니다. 할 수 있습니다 또는 제대로 원격 데스크톱 세션 호스트 서버 또는 VDI 서버를 사용 하는 경우 시작 메뉴의 설정 로밍 사용자 프로필 디스크를 사용 합니다. 자세한 내용은 참조 하세요. [Windows Server 2012의 사용자 프로필 디스크를 사용 하 여 사용자 데이터 관리가 쉽습니다](https://blogs.technet.microsoft.com/enterprisemobility/2012/11/13/easier-user-data-management-with-user-profile-disks-in-windows-server-2012/)합니다.

### <a name="considerations-when-using-roaming-user-profiles-on-multiple-versions-of-windows"></a>여러 버전의 Windows에서 로밍 사용자 프로필을 사용할 때의 고려 사항

여러 버전의 Windows에서 로밍 사용자 프로필을 사용하려는 경우 다음 작업을 수행하는 것이 좋습니다.

- 각 운영 체제 버전에 대한 별도의 프로필 버전을 유지하도록 Windows를 구성합니다. 이는 프로필 손상과 같은 원치 않고 예측할 수 없는 문제를 방지하는 데 도움이 됩니다.
- 폴더 리디렉션을 사용하여 문서 및 사진과 같은 사용자 파일을 사용자 프로필 외부에 저장합니다. 이렇게 하면 동일한 파일을 여러 운영 체제 버전에서 사용할 수 있습니다. 또한 프로필이 작은 크기로 유지되고 로그인 속도가 빨라집니다.
- 로밍 사용자 프로필에 대한 충분한 저장소를 할당합니다. 두 운영 체제 버전을 지원하는 경우 각 운영 체제 버전에 대해 별도의 프로필이 유지되므로 프로필 수가 두 배로 증가하며, 따라서 사용된 총 공간도 두 배로 증가합니다.
- Windows Vista/Windows Server 2008 및 Windows 7 또는 Windows Server 2008 R2 실행 하는 컴퓨터에서 로밍 사용자 프로필을 사용 하지 마세요. 이러한 운영 체제 버전 간에 로밍 프로필 버전의 비 호환성으로 인해 지원 되지 않습니다.
- 하나의 운영 체제 버전에서 적용된 변경 내용이 다른 운영 체제 버전으로 로밍되지 않는다는 점을 사용자에게 알려 줍니다.
- 다른 프로필 버전을 사용 하는 Windows 버전으로 환경을 이동 하는 경우 (예: Windows 10 버전 1607 Windows 10-참조 [부록 b: 프로필 버전 참조 정보](#appendix-b-profile-version-reference-information) 목록은), 사용자가 새로 만든 빈 로밍 사용자 프로필을 수신 합니다. 공용 폴더를 리디렉션하도록 폴더 리디렉션을 사용 하 여 새 프로필을 가져오는 영향을 최소화할 수 있습니다. 로밍 사용자 프로필 마이그레이션 프로필을 두 개 버전에서 다른 수 있는 방법은 없습니다.

## <a name="step-1-enable-the-use-of-separate-profile-versions"></a>1단계: 별도 프로필 버전 사용

Windows 8.1, Windows 8, Windows Server 2012 R2 또는 Windows Server 2012를 실행 하는 컴퓨터에 로밍 사용자 프로필을 배포 하는 경우 배포 전에 Windows 환경에 몇 가지 변경 하는 것이 좋습니다. 이러한 변경 내용은 향후 운영 체제 업그레이드를 원활하게 하고, 로밍 사용자 프로필과 함께 여러 버전의 Windows를 보다 쉽게 동시에 실행하도록 해줍니다.

이러한 변경 내용을 적용하려면 다음 절차를 사용합니다.

1. 로밍, 필수, 상위 필수 또는 도메인 기본 프로필을 사용하려는 모든 컴퓨터에 적절한 소프트웨어 업데이트를 다운로드하여 설치합니다.

    - Windows 8.1 또는 Windows Server 2012 R2: 문서에 설명 된 소프트웨어 업데이트를 설치 [2887595](http://support.microsoft.com/kb/2887595) 에서 Microsoft 기술 자료 (릴리스된 경우).
    - Windows 8 또는 Windows Server 2012: Microsoft 기술 자료 문서 [2887239](http://support.microsoft.com/kb/2887239) 에 설명된 소프트웨어 업데이트를 설치합니다.

2. Windows 8.1, Windows 8, Windows Server 2012 R2 또는 Windows Server 2012는 로밍 사용자 프로필을 실행 하는 모든 컴퓨터에서 레지스트리 편집기를 사용 하 여 또는 다음 레지스트리를 만드는 그룹 정책 키 DWORD 값 및 설정 `1`합니다. 그룹 정책을 사용하여 레지스트리 키를 만드는 방법에 대한 자세한 내용은 [레지스트리 항목 구성](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753092(v=ws.11)>)을 참조하세요.

    ```
    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\ProfSvc\Parameters\UseProfilePathExtensionVersion
    ```

    > [!WARNING]
    > 레지스트리를 잘못 편집하면 시스템에 심각한 손상을 줄 수 있습니다. 따라서 레지스트리를 변경하기 전에 컴퓨터의 중요한 데이터를 백업해 두어야 합니다.
3. 컴퓨터를 다시 시작합니다.

## <a name="step-2-create-a-roaming-user-profiles-security-group"></a>2단계: 로밍 사용자 프로필 보안 그룹 만들기

환경에 로밍 사용자 프로필을 아직 설정하지 않은 경우 먼저 로밍 사용자 프로필 정책 설정을 적용할 모든 사용자 및/또는 컴퓨터가 포함된 보안 그룹을 만들어야 합니다.

- 범용 로밍 사용자 프로필 배포 관리자는 일반적으로 사용자에 대한 보안 그룹을 만듭니다.
- 원격 데스크톱 서비스 또는 가상화된 데스크톱 배포 관리자는 일반적으로 사용자 및 공유 컴퓨터에 대한 보안 그룹을 사용합니다.

로밍 사용자 프로필에 대 한 보안 그룹을 만드는 방법은 다음과 같습니다.

1. 설치 된 Active Directory 관리 센터를 사용 하 여 컴퓨터에서 서버 관리자를 엽니다.
2. 에 **도구** 메뉴에서 **Active Directory 관리 센터**합니다. Active Directory 관리 센터가 표시됩니다.
3. 적절 한 도메인 또는 OU를 선택 하는 마우스 오른쪽 단추로 클릭 **새로 만들기**를 선택한 후 **그룹**합니다.
4. **그룹 만들기** 창의 **그룹** 섹션에서 다음 설정을 지정합니다.

    - **그룹 이름**에 보안 그룹의 이름(예: **Roaming User Profiles Users and Computers**)을 입력합니다.
    - **그룹 범위**를 선택 **보안**를 선택한 후 **Global**합니다.

5. 에 **멤버** 섹션에서 **추가**합니다. 사용자, 연락처, 컴퓨터, 서비스 계정 또는 그룹 선택 대화 상자가 나타납니다.
6. 보안 그룹에 컴퓨터 계정을 포함 하려는 경우 선택 **개체 유형**를 선택 합니다 **컴퓨터** 확인란을 선택한 후 **확인**합니다.
7. 사용자, 그룹 및/또는 로밍 사용자 프로필 배포를 선택 하려는 컴퓨터의 이름을 입력 **확인**를 선택한 후 **확인** 다시 합니다.

## <a name="step-3-create-a-file-share-for-roaming-user-profiles"></a>3단계: 로밍 사용자 프로필에 대한 파일 공유 만들기

다음 절차를 사용 하 여 Windows를 실행 하는 서버에서 파일 공유를 만들려면 (별개 로밍 프로필 폴더의 부주의 한 캐싱을 방지 하기 위해 리디렉션된 폴더에 대 한 모든 공유), 사용자 프로필 로밍에 대 한 별도 파일 공유를 아직 없는 수행 하는 경우 서버입니다.

> [!NOTE]
> 일부 기능은 다를 수도 사용 하는 Windows Server의 버전에 따라 사용할 수 없습니다.

Windows Server에서 파일 공유를 만드는 방법에는 다음과 같습니다.

1. 서버 관리자 탐색 창에서 선택 **File and Storage Services**를 선택한 후 **공유** 공유 페이지를 표시 합니다.
2. 공유 타일에서 선택 **태스크**를 선택한 후 **새 공유**합니다. 새 공유 마법사가 나타납니다.
3. 에 **프로필 선택** 페이지에서 선택 **SMB 공유 – 빠르게**합니다. 파일 서버 리소스 관리자가 설치 되어 있고 폴더 관리 속성을 사용 하는 경우 대신 선택할 **SMB 공유-고급**합니다.
4. **공유 위치** 페이지에서 공유를 만들 서버 및 볼륨을 선택합니다.
5. **공유 이름** 페이지의 **공유 이름** 상자에 공유 이름(예: **User Profiles$** )을 입력합니다.

    > [!TIP]
    > 공유를 만들 때 공유 이름 뒤에 ```$``` 를 붙여 공유를 숨깁니다. 그러면 일반 브라우저에서 공유가 숨겨집니다.

6. **기타 설정** 페이지에서 **지속적인 가용성 사용** 확인란(있는 경우)을 선택 취소하고 필요에 따라 **액세스 기반 열거 사용** 및 **데이터 액세스 암호화** 확인란을 선택합니다.
7. 에 **사용 권한** 페이지에서 **사용 권한 사용자 지정 하는 중...** . 고급 보안 설정 대화 상자가 나타납니다.
8. 선택 **상속 사용 안 함**를 선택한 후 **상속 된 사용 권한을이 개체에 대 한 권한이 명시적으로 변환**합니다.
9. 에 설명 된 대로 사용 권한을 설정 [로밍 사용자 프로필을 호스트 파일에 필요한 권한을 공유](#required-permissions-for-the-file-share-hosting-roaming-user-profiles) 특별 한 다음 화면에 나열 되지 않은 그룹 및 계정에 대 한 권한을 제거 하 고 추가에 표시 1 단계에서에서 만든 Roaming User Profiles Users and Computers 그룹에 대 한 권한입니다.
    
    ![고급 보안 설정 창 표 1에 설명 된 대로 사용 권한을 표시 합니다.](media/advanced-security-user-profiles.jpg)
    
    **그림 1** 로밍 사용자 프로필 공유에 대한 권한 설정
10. **SMB 공유 - 고급** 프로필을 선택한 경우 **관리 속성** 페이지에서 **사용자 파일** 폴더 사용량 값을 선택합니다.
11. **SMB 공유 - 고급** 프로필을 선택한 경우 **할당량** 페이지에서 필요에 따라 공유의 사용자에게 적용할 할당량을 선택합니다.
12. 에 **확인** 페이지에서 **만들기.**

### <a name="required-permissions-for-the-file-share-hosting-roaming-user-profiles"></a>파일 공유 호스팅 로밍 사용자 프로필에 필요한 권한

| 사용자 계정 | 액세스 권한 | 적용 대상 |
|   -   |   -   |   -   |
|   시스템    |  모든 권한     |  이 폴더, 하위 폴더 및 파일     |
|  Administrators     |  모든 권한     |  이 폴더만     |
|  만든 이/소유자     |  모든 권한     |  하위 폴더 및 파일만     |
| 공유에 데이터를 저장해야 하는 사용자의 보안 그룹(Roaming User Profiles Users and Computers)      |  폴더 나열 / 데이터 읽기 *(고급 권한)* <br />폴더 만들기 / 데이터 추가 *(고급 권한)* |  이 폴더만     |
| 다른 그룹 및 계정   |  없음(제거)     |       |

## <a name="step-4-optionally-create-a-gpo-for-roaming-user-profiles"></a>4단계: 로밍 사용자 프로필에 대한 GPO 만들기(선택 사항)

로밍 사용자 프로필 설정에 대해 만든 GPO가 아직 없는 경우 다음 절차를 사용하여 로밍 사용자 프로필에서 사용할 빈 GPO를 만듭니다. 이 GPO를 사용하여 로밍 사용자 프로필 설정(예: 기본 컴퓨터 지원(별도 설명 참조))을 구성할 수 있으며, 컴퓨터에서 로밍 사용자 프로필을 사용하도록 설정(가상화된 데스크톱 환경에서 배포하거나 원격 데스크톱 서비스를 사용하는 경우에 일반적)할 수 있습니다.

로밍 사용자 프로필에 대 한 GPO를 만드는 방법은 다음과 같습니다.

1. 그룹 정책 관리가 설치된 컴퓨터에서 서버 관리자를 엽니다.
2. **도구가** 메뉴 선택 **그룹 정책 관리**합니다. 그룹 정책 관리가 나타납니다.
3. 도메인 또는 로밍 사용자 프로필을 설치 하 고 선택 하려는 OU를 마우스 오른쪽 단추로 클릭 **이 도메인에서 GPO를 만들어 여기에 연결**합니다.
4. 에 **새 GPO** 대화 상자에 GPO의 이름 입력 (예를 들어 **Roaming User Profile Settings**)를 선택한 후 **확인**합니다.
5. 새로 만든 GPO를 마우스 오른쪽 단추로 클릭하고 **연결 사용** 확인란의 선택을 취소합니다. 그러면 구성을 마칠 때까지 GPO가 적용되지 않습니다.
6. GPO를 선택합니다. 에 **보안 필터링** 부분을 **범위** 탭을 선택 **Authenticated Users**를 선택한 후 **제거** GPO를 방지 하기 위해 모든 사용자에 게 적용 중입니다.
7. 에 **보안 필터링** 섹션에서 **추가**합니다.
8. 에 **사용자, 컴퓨터 또는 그룹 선택** 대화 상자에서 1 단계에서에서 만든 그룹 보안의 이름 (예를 들어 **Roaming User Profiles Users and Computers**)를 선택한 후 **확인** .
9. 선택 합니다 **위임** 탭을 선택 **추가**, 형식 **Authenticated Users**를 선택 **확인**를 선택한 후 **확인** 다시 기본값을 적용 하려면 읽기 권한이 있습니다.
    
    이 단계에서 보안 변경으로 인해 되기 [MS16 072](https://support.microsoft.com/help/3163622/ms16-072-security-update-for-group-policy-june-14%2c-2016)합니다.

>[!IMPORTANT]
>보안 변경 내용으로 인해 [MS16 072A](https://support.microsoft.com/help/3163622/ms16-072-security-update-for-group-policy-june-14%2c-2016), 이제 GPO에 인증 된 사용자 위임 된 그룹 읽기 권한을 부여 해야 합니다-그렇지 않은 경우 사용자에 게 GPO 적용 되지 않습니다 또는 이미 적용 된 경우 GPO가 제거 되 면 사용자 프로필을 다시 로컬 PC 리디렉션됩니다. 자세한 내용은 참조 하세요. [배포 그룹 정책 보안 업데이트 MS16-072](https://blogs.technet.microsoft.com/askds/2016/06/22/deploying-group-policy-security-update-ms16-072-kb3163622/)합니다.

## <a name="step-5-optionally-set-up-roaming-user-profiles-on-user-accounts"></a>5단계: 사용자 계정에 로밍 사용자 프로필 설치(선택 사항)

사용자 계정에 로밍 사용자 프로필을 배포하려면 다음 절차를 사용하여 Active Directory 도메인 서비스의 사용자 계정에 대한 로밍 사용자 프로필을 지정합니다. 배포 하는 경우 로밍 사용자 프로필 컴퓨터에 원격 데스크톱 서비스 또는 가상화 된 데스크톱 배포에 설명 된 절차를 대신 사용할에 대 한 일반적인 방식 대로 [6 단계: 필요에 따라 컴퓨터에 로밍 사용자 프로필을 설정할](#step-6-optionally-set-up-roaming-user-profiles-on-computers)합니다.

> [!NOTE]
> Active Directory를 사용하여 사용자 계정에 로밍 사용자 프로필을 설치하고, 그룹 정책을 사용하여 컴퓨터에 로밍 사용자 프로필을 설치한 경우 컴퓨터 기반 정책 설정이 우선적으로 적용됩니다.

사용자 계정에 로밍 사용자 프로필을 설정 하는 방법을 다음과 같습니다.

1. Active Directory 관리 센터에서 적절한 도메인의 **사용자** 컨테이너(또는 OU)로 이동합니다.
2. 로밍 사용자 프로필을 할당, 사용자를 마우스 오른쪽 단추로 클릭 한 다음 선택 하려는 모든 사용자 선택 **속성**합니다.
3. **프로필** 섹션을 선택 합니다 **프로필 경로:** 확인란을 다음 경로 입력 파일 공유에 사용자의 로밍 사용자 프로필을 뒤에 저장 하려는 `%username%` ( 자동으로 바꿀 사용자가 로그인 하는 사용자 이름 첫 번째 시간). 예를 들어 다음과 같은 가치를 제공해야 합니다.
    
    `\\fs1.corp.contoso.com\User Profiles$\%username%`
    
    필수 로밍 사용자 프로필을 지정 하려면 이전에 만든, 예를 들어 NTuser.man 파일의 경로 지정 `fs1.corp.contoso.comUser Profiles$default`합니다. 자세한 내용은 [필수 사용자 프로필을 만들](https://docs.microsoft.com/windows/client-management/mandatory-user-profile)합니다.
4. **확인**을 선택합니다.

> [!NOTE]
> 로밍 사용자 프로필을 사용할 때는 기본적으로 모든 Windows® 런타임 기반(Windows 스토어) 앱의 배포가 허용됩니다. 그러나 특수 프로필을 사용할 때는 앱이 기본적으로 배포되지 않습니다. 특수 프로필은 사용자가 로그아웃한 후 변경 내용이 삭제되는 사용자 프로필입니다.
> <br><br>특수 프로필에 대한 앱 배포 제한을 제거하려면 **특수 프로필에서 배포 작업 허용** 정책 설정(컴퓨터 구성\정책\관리 템플릿\앱 패키지 배포에 있음)을 사용합니다. 그러나 이 시나리오에서 배포된 앱은 일부 데이터가 컴퓨터에 그대로 남아 있으므로 단일 컴퓨터의 사용자가 수백 명인 경우 누적될 수 있습니다. 앱을 정리를 찾거나 개발 도구를 사용 하는 [CleanupPackageForUserAsync](https://msdn.microsoft.com/library/windows/apps/windows.management.deployment.packagemanager.cleanuppackageforuserasync.aspx) 프로필을 컴퓨터에 더 이상 사용자 용 앱 패키지를 정리 하는 API입니다.
> <br><br>Windows 스토어 앱에 대한 추가 배경 정보는 [Windows 스토어에 대한 클라이언트 액세스 관리](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/hh832040(v=ws.11)>)를 참조하세요.

## <a name="step-6-optionally-set-up-roaming-user-profiles-on-computers"></a>6단계: 컴퓨터에 로밍 사용자 프로필 설치(선택 사항)

컴퓨터에 로밍 사용자 프로필을 배포하려면 원격 데스크톱 서비스 또는 가상화된 데스크톱 배포에 일반적인 방식대로 다음 절차를 사용합니다. 사용자 계정에 로밍 사용자 프로필을 배포 하는 경우에 설명 된 절차를 대신 사용할 [5 단계: 필요에 따라 사용자 계정에 로밍 사용자 프로필을 설정할](#step-5-optionally-set-up-roaming-user-profiles-on-user-accounts)합니다.

Windows 8.1, Windows 8, Windows 7, Windows Vista, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 또는 Windows Server 2008을 실행 하는 컴퓨터에 로밍 사용자 프로필을 적용할 그룹 정책을 사용할 수 있습니다.

> [!NOTE]
> 그룹 정책을 사용하여 컴퓨터에 로밍 사용자 프로필을 설치하고, Active Directory를 사용하여 사용자 계정에 로밍 사용자 프로필을 설치한 경우 컴퓨터 기반 정책 설정이 우선적으로 적용됩니다.

컴퓨터에 로밍 사용자 프로필을 설정 하는 방법을 다음과 같습니다.

1. 그룹 정책 관리가 설치된 컴퓨터에서 서버 관리자를 엽니다.
2. **도구** 메뉴에서 **그룹 정책 관리**합니다. 그룹 정책 관리 표시 됩니다.
3. 3 단계에서에서 만든 GPO를 마우스 오른쪽 단추로 클릭 그룹 정책 관리에서 (예를 들어 **Roaming User Profiles Settings**)를 선택한 후 **편집**합니다.
4. 그룹 정책 관리 편집기 창에서 **컴퓨터 구성**, **정책**, **관리 템플릿**, **시스템**, **사용자 프로필**로 차례로 이동합니다.
5. 마우스 오른쪽 단추로 클릭 **이 컴퓨터에 로그온 하는 모든 사용자의 로밍 프로필 경로 설정** 선택한 후 **편집**합니다.
    > [!TIP]
    > 사용자의 홈 폴더(구성된 경우)는 Windows PowerShell과 같은 일부 프로그램에서 사용하는 기본 폴더입니다. AD DS에서 사용자 계정 속성의 **홈 폴더** 섹션을 사용하여 사용자별 대체 로컬 또는 네트워크 위치를 구성할 수 있습니다. Windows 8.1, Windows 8, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012 가상 데스크톱 환경에서 실행 하는 컴퓨터의 모든 사용자의 홈 폴더 위치를 구성 하려면 사용 하도록 설정 된 **사용자 홈 폴더**  정책 설정 하 고 매핑하거나 로컬 폴더를 지정 하는 파일 공유 및 드라이브 문자를 지정 합니다. 환경 변수나 줄임표를 사용하지 마세요. 사용자가 로그온한 동안 지정한 경로 끝에 사용자의 별칭이 추가됩니다.
6. 에 **속성** 대화 상자에서 **사용**
7. 에 **이 컴퓨터에 로그온 하는 사용자가 로밍 프로필 경로 사용 해야** 상자에 사용자의 로밍 사용자 프로필을 뒤에 저장 하려는 파일 공유 경로 입력 합니다 `%username%` (하는 자동으로 바뀝니다 사용자는 첫 번째 이름으로 사용자가 로그인)입니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.

    `\\fs1.corp.contoso.com\User Profiles$\%username%`

    필수 로밍 사용자 프로필에는 사용자 수 없습니다 (변경 내용이 사용자가 로그 아웃 하는 경우 다시 설정) 영구적으로 변경, 이전에 만든, 예를 들어 NTuser.man 파일의 경로를 지정 하는 미리 구성 된 프로필을 지정 하려면 `\\fs1.corp.contoso.com\User Profiles$\default`합니다. 자세한 내용은 [필수 사용자 프로필 만들기](https://docs.microsoft.com/windows/client-management/mandatory-user-profile)를 참조하세요.
8. **확인**을 선택합니다.

## <a name="step-7-optionally-specify-a-start-layout-for-windows-10-pcs"></a>7단계: 필요에 따라 Windows 10 Pc에 대 한 시작 레이아웃 지정

모든 Pc에서 동일한 시작 레이아웃을 볼 수 있도록 특정 시작 메뉴 레이아웃 적용 하려면 그룹 정책을 사용할 수 있습니다. 둘 이상의 PC를 사용자가 로그인 하려면 Pc에서 일관 된 시작 레이아웃을 가질 수, GPO 모든 Pc에 적용 되도록 해야 합니다.

시작 레이아웃을 지정 하려면 다음을 수행 합니다.

1. Windows 10 버전 1607 (라고도 1 주년 업데이트)를 Windows 10 Pc를 업데이트 또는 최신, 2017 년 3 월 14 일 누적 업데이트를 설치 하 고 ([KB4013429](https://support.microsoft.com/kb/4013429)) 이상.
2. 전체 또는 일부 시작 메뉴 레이아웃 XML 파일을 만듭니다. 이렇게 하려면 참조 [사용자 지정 및 내보내기 시작 레이아웃](https://docs.microsoft.com/windows/configuration/customize-and-export-start-layout)합니다.
    * 지정 하는 경우는 *전체* 시작 레이아웃 사용자 시작 메뉴의 일부를 사용자 지정할 수 없습니다. 지정 된 *부분* 시작 레이아웃 사용자 지정 타일의 잠금된 그룹을 제외한 모든 합니다. 그러나 부분 시작 레이아웃을 사용 하 여 사용자 지정 시작 메뉴에 다른 Pc에 로밍 없습니다.
3. 그룹 정책을 사용 하 여 로밍 사용자 프로필에 대해 만든 GPO를 사용자 지정된 시작 레이아웃을 적용 합니다. 이렇게 하려면 참조 [도메인의 사용자 지정된 시작 레이아웃을 적용할 그룹 정책을 사용 하 여](https://docs.microsoft.com/windows/configuration/customize-windows-10-start-screens-by-using-group-policy#bkmk-domaingpodeployment)입니다.
4. 그룹 정책을 사용 하 여 Windows 10 Pc에서 다음 레지스트리 값을 설정 합니다. 이렇게 하려면 참조 [레지스트리 항목 구성](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753092(v=ws.11)>)합니다.

| **동작**   | **업데이트**                  |
| ------------ | ------------                |
| Hive         | **HKEY_LOCAL_MACHINE**      |
| 키 경로     | **Software\Microsoft\Windows\CurrentVersion\Explorer** |
| 값 이름   | **SpecialRoamingOverrideAllowed** |
| 값 유형   | **REG_DWORD**               |
| 값 데이터   | **1** (또는 **0** 사용 하지 않도록 설정) |
| 기본         | **10 진수**                 |

5. (선택 사항) 사용자가 더 빠르게 로그인 할 수 있도록 처음 로그온 최적화를 사용 합니다. 이렇게 하려면 참조 [로그인 시간을 개선 하는 정책을 적용할](https://docs.microsoft.com/windows/client-management/mandatory-user-profile#apply-policies-to-improve-sign-in-time)합니다.
6. (선택 사항) 추가 클라이언트 Pc를 배포 하는 Windows 10 기본 이미지에서 불필요 한 앱을 제거 하 여 로그인 시간을 줄입니다. Windows Server 2016 및 Windows Server 2019 기능이 미리 프로 비전 된 모든 앱 서버 이미지에이 단계를 건너뛸 수 있습니다.
    - 앱을 제거 하려면 사용 합니다 [제거 AppxProvisionedPackage](https://docs.microsoft.com/powershell/module/dism/remove-appxprovisionedpackage?view=win10-ps) 다음 응용 프로그램을 제거 하려면 Windows PowerShell cmdlet. Pc에 이미 배포 된 경우 사용 하 여 이러한 앱의 제거를 스크립팅할 수 있습니다 합니다 [제거 AppxPackage](https://docs.microsoft.com/powershell/module/appx/remove-appxpackage?view=win10-ps)합니다.
    
      - Microsoft.windowscommunicationsapps\_8wekyb3d8bbwe
      - Microsoft.BingWeather\_8wekyb3d8bbwe
      - Microsoft.DesktopAppInstaller\_8wekyb3d8bbwe
      - Microsoft.Getstarted\_8wekyb3d8bbwe
      - Microsoft.Windows.Photos\_8wekyb3d8bbwe
      - Microsoft.WindowsCamera\_8wekyb3d8bbwe
      - Microsoft.WindowsFeedbackHub\_8wekyb3d8bbwe
      - Microsoft.WindowsStore\_8wekyb3d8bbwe
      - Microsoft.XboxApp\_8wekyb3d8bbwe
      - Microsoft.XboxIdentityProvider\_8wekyb3d8bbwe
      - Microsoft.ZuneMusic\_8wekyb3d8bbwe

>[!NOTE]
>로그인 시간을 감소 이러한 앱을 제거 하지만 그 중 하나에 배포 해야 하는 경우 설치를 둘 수 있습니다.

## <a name="step-8-enable-the-roaming-user-profiles-gpo"></a>8단계: 로밍 사용자 프로필 GPO 사용

그룹 정책을 사용하여 컴퓨터에 로밍 사용자 프로필을 설치하거나 그룹 정책을 사용하여 다른 로밍 사용자 프로필 설정을 사용자 지정한 경우 영향을 받는 사용자에게 적용하도록 허용하는 GPO를 설정해야 합니다.

>[!TIP]
>기본 컴퓨터 지원을 구현 하려는 경우 지금, GPO를 사용 하기 전에 합니다. 그러면 기본 컴퓨터 지원을 사용하기 전에 사용자 데이터가 기본이 아닌 컴퓨터에 복사되는 것이 방지됩니다. 특정 정책 설정 참조 [폴더 리디렉션 및 로밍 사용자 프로필에 대 한 기본 컴퓨터 배포](deploy-primary-computers.md)합니다.

로밍 사용자 프로필 GPO 사용 방법은 다음과 같습니다.

1. 그룹 정책 관리를 엽니다.
2. 사용자가 만든 GPO를 마우스 오른쪽 단추로 클릭 하 고 선택한 **링크가 활성화**합니다. 메뉴 항목 옆에 확인란이 표시됩니다.

## <a name="step-9-test-roaming-user-profiles"></a>9단계: 로밍 사용자 프로필 테스트

로밍 사용자 프로필을 테스트하려면 로밍 사용자 프로필에 대해 구성된 사용자 계정으로 컴퓨터에 로그인하거나, 로밍 사용자 프로필에 대해 구성된 컴퓨터에 로그인합니다. 그런 다음 프로필이 리디렉션되었는지 확인합니다.

로밍 사용자 프로필을 테스트 하는 방법을 다음과 같습니다.

1. 로밍 사용자 프로필을 사용하도록 설정한 사용자 계정으로 기본 컴퓨터(기본 컴퓨터 지원을 사용하도록 설정한 경우)에 로그인합니다. 특정 컴퓨터에서 로밍 사용자 프로필을 사용하도록 설정한 경우 해당 컴퓨터 중 하나에 로그인합니다.
2. 사용자가 이전에 컴퓨터에 로그인한 경우 관리자 권한 명령 프롬프트를 열고 다음 명령을 입력하여 클라이언트 컴퓨터에 최신 그룹 정책 설정이 적용되었는지 확인합니다.
    
    ```PowerShell
    GpUpdate /Force
    ```
3. 사용자 프로필이 로밍 중인지를 확인 하려면 엽니다 **Control Panel**를 선택 **시스템 및 보안**를 선택 **시스템**선택, **고급 시스템 설정** 를 선택 **설정** 사용자 프로필 섹션 및 다음 검색할 **로밍** 에 **형식** 열.

## <a name="appendix-a-checklist-for-deploying-roaming-user-profiles"></a>부록 a: 로밍 사용자 프로필 배포 검사 목록

| 상태                     | 작업                                                |
| ---                        | ------                                                |
| ☐<br>☐<br>☐<br>☐<br>☐   | 1. 도메인 준비<br>-도메인에 컴퓨터를 가입 합니다.<br>--별도 프로필 버전 사용을 사용 하는 중<br>사용자 계정 만들기<br>-(선택 사항) 폴더 리디렉션을 사용 |
| ☐<br><br><br>             | 2. 로밍 사용자 프로필에 대한 보안 그룹 만들기<br>그룹 이름:<br>-구성원: |
| ☐<br><br>                 | 3. 로밍 사용자 프로필에 대한 파일 공유 만들기<br>파일 공유 이름: |
| ☐<br><br>                 | 4. 로밍 사용자 프로필에 대한 GPO 만들기<br>GPO 이름:|
| ☐                         | 5. 로밍 사용자 프로필 정책 설정 구성    |
| ☐<br>☐<br>☐              | 6. 로밍 사용자 프로필을 사용 하도록 설정<br>-AD DS에서 사용자 계정에 사용?<br>-컴퓨터 계정에서 그룹 정책에서 사용할 수 있습니까?<br> |
| ☐                         | 7. (선택 사항) Windows 10 Pc에 대 한 필수 시작 레이아웃을 지정 합니다. |
| ☐<br>☐<br><br>☐<br><br>☐ | 8. (선택 사항) 기본 컴퓨터 지원 사용<br>-사용자의 기본 컴퓨터를 지정 합니다.<br>사용자 및 기본 컴퓨터 매핑 위치:<br>-폴더 리디렉션에 대 한 기본 컴퓨터 지원 (선택 사항) 사용<br>컴퓨터 기반 또는 사용자 기반?<br>-로밍 사용자 프로필에 대 한 기본 컴퓨터 지원 (선택 사항) 사용 |
| ☐                        | 9. 로밍 사용자 프로필 GPO 사용                |
| ☐                        | 10. 로밍 사용자 프로필 테스트                         |

## <a name="appendix-b-profile-version-reference-information"></a>부록 B: 프로필 버전 참조 정보

각 프로필의 프로필 사용 되는 Windows 버전에 해당 하는 프로필 버전을 있습니다. 예를 들어, Windows 10, 버전 1703 및 버전 1607 둘 다 사용 합니다. V6 프로필 버전입니다. Microsoft은 Windows의 모든 버전 새 프로필 버전을 포함 하는 하지 않는 이유는 호환성을 유지 하기 위해 필요한 경우에 새 프로필 버전을 만듭니다.

다음 표에는 여러 Windows 버전의 로밍 사용자 프로필 위치가 나와 있습니다.

| 운영 체제 버전 | 로밍 사용자 프로필 위치 |
| --- | --- |
| Windows XP 및 Windows Server 2003 | ```\\<servername>\<fileshare>\<username>``` |
| Windows Vista and Windows Server 2008 | ```\\<servername>\<fileshare>\<username>.V2``` |
| Windows 7 및 Windows Server 2008 R2 | ```\\<servername>\<fileshare>\<username>.V2``` |
| Windows 8 및 Windows Server 2012 | ```\\<servername>\<fileshare>\<username>.V3``` (소프트웨어 업데이트 및 레지스트리 키 적용 후)<br>```\\<servername>\<fileshare>\<username>.V2``` (전에 소프트웨어 업데이트 및 레지스트리 키 적용) |
| Windows 8.1 및 Windows Server 2012 R2 | ```\\<servername>\<fileshare>\<username>.V4``` (소프트웨어 업데이트 및 레지스트리 키 적용 후)<br>```\\<servername>\<fileshare>\<username>.V2``` (전에 소프트웨어 업데이트 및 레지스트리 키 적용) |
| Windows 10 | ```\\<servername>\<fileshare>\<username>.V5``` |
| Windows 10, 버전 1703 및 버전 1607 | ```\\<servername>\<fileshare>\<username>.V6``` |

## <a name="appendix-c-working-around-reset-start-menu-layouts-after-upgrades"></a>부록 C: 작업은 업그레이드 한 후 시작 메뉴 레이아웃을 약 재설정

몇 가지 방법으로 전체 업그레이드 한 후 다시 시작 하는 시작 메뉴 레이아웃을 해결할 수는 다음과 같습니다.

- 장치를 그 어느 때 사용 하는 한 명의 사용자 및 IT 관리자는 SCCM와 같은 관리 되는 OS 배포 전략을 사용 하는 경우 다음을 수행할 수 있습니다.
    
  1. 업그레이드 하기 전에 Export-startlayout를 사용 하 여 시작 메뉴 레이아웃을 내보내기 
  2. OOBE 하지만 사용자가 로그인 하기 전에 Import-startlayout을 사용 하 여 시작 메뉴 레이아웃을 가져오기  
 
     > [!NOTE] 
     > 가져오기는 StartLayout 기본 사용자 프로필을 수정 합니다. 모든 사용자 프로필 가져오기 발생 한 후 만든 가져온된 시작 레이아웃을 받게 됩니다.
 
- IT 관리자는 그룹 정책을 사용 하 여 시작의 레이아웃을 관리 하도록 선택할 수 있습니다. 그룹 정책을 사용 하는 표준화 된 시작 레이아웃을 사용자에 게 적용 중앙 집중식된 관리 솔루션을 제공 합니다. 2 모드가 시작 관리에 대 한 그룹 정책을 사용 하는 모드에 있습니다. 전체 잠금 및 잠금 부분입니다. 전체 잠금 시나리오는 사용자 시작의 레이아웃을 변경 하지 못하도록 방지 합니다. 부분 잠금 시나리오를 사용 하면 시작의 특정 영역으로 변경할 수 있습니다. 자세한 내용은 참조 하세요. [사용자 지정 및 내보내기 시작 레이아웃](https://docs.microsoft.com/windows/configuration/customize-and-export-start-layout)합니다.
        
   > [!NOTE]
   > 업그레이드 하는 동안 계속 부분 잠금 시나리오에서 사용자가 변경한 변경 내용이 손실 됩니다.

- 시작을 레이아웃 재설정 발생 하 고 최종 사용자가 시작을 다시 구성할 수 있습니다. 알림 전자 메일 또는 기타 알림은 시작 레이아웃을 영향을 최소화 하려면 OS를 업그레이드 한 후 다시 설정 하도록 최종 사용자에 게 보낼 수 있습니다. 

# <a name="change-history"></a>변경 기록

다음 표에는 이 항목의 중요한 최근 변경 내용이 요약되어 있습니다.

| Date | 설명 |Reason|
| --- | ---         | ---   |
| 2019 년 5 월 1 일부 터 | Windows Server 2019에 대 한 추가 업데이트 |
| 2018 년 4 월 10 일 | 운영 체제 현재 위치 업그레이드 한 후 손실 사용자 지정 시작 하는 경우 추가 토론|설명선 알려진 문제입니다. |
| 2018 년 3 월 13 일 | Windows Server 2016 용 업데이트 | 이전 버전 라이브러리 외부로 이동 하 고 현재 버전의 Windows Server 용으로 업데이트 합니다. |
| 2017 년 4 월 13 일 | Windows 10 버전 1703에 대 한 프로필 정보를 추가 하 고 운영 체제를 업그레이드 하는 경우 어떻게 로밍 프로필 버전 작업 설명이 명시 되었습니다-참조 [여러 버전의 Windows에서 로밍 사용자 프로필을 사용할 때의 고려 사항](#considerations-when-using-roaming-user-profiles-on-multiple-versions-of-windows)합니다. | 고객 의견 |
| 2017 년 3 월 14 일 | Windows 10 Pc에 대 한 필수 시작 레이아웃을 지정 하는 것에 대 한 추가 선택적 단계 [부록 a: 로밍 사용자 프로필 배포 검사 목록](#appendix-a-checklist-for-deploying-roaming-user-profiles)합니다. |최신 Windows 업데이트의 변경 내용 기능입니다. |
| 2017 년 1 월 23 일 | 추가 하는 단계를 [4 단계: 필요에 따라 로밍 사용자 프로필에 대 한 GPO를 만들어](#step-4-optionally-create-a-gpo-for-roaming-user-profiles) 현재 인증 된 사용자에 게 읽기 권한을 위임 하려면 그룹 정책 보안 업데이트로 인해 필요 합니다.|보안 그룹 정책 처리를 변경합니다. |
| 2016 년 12 월 29 일 | 링크를 추가 [8 단계: 로밍 사용자 프로필 GPO 사용](#step-8-enable-the-roaming-user-profiles-gpo) 쉽게 기본 컴퓨터에 대 한 그룹 정책을 설정 하는 방법에 대 한 정보를 가져올 수 있습니다. 또한 수정 단계 5 및 6의 숫자에 잘못 된에 대 한 몇 가지 참조가 되었습니다.|고객 의견 |
| 2016 년 12 월 5 일 | 시작 메뉴 설정 로밍 문제를 설명 하는 추가 정보입니다. | 고객 의견 |
| 2016 년 7 월 6 일 | Windows 10 프로필 버전 접미사를 추가 [부록 b: 프로필 버전 참조 정보](#appendix-b-profile-version-reference-information)합니다. 지원 되는 운영 체제의 목록에서 Windows XP 및 Windows Server 2003 제거 합니다. | 새 버전의 Windows를 및 더 이상 지원 되지 않는 Windows 버전에 대 한 제거 정보에 대 한 업데이트 합니다. |
| 2015년 7월 7일 | 클러스터된 파일 서버를 사용하는 경우 지속적인 가용성을 사용하지 않도록 설정하는 단계 및 요구 사항을 추가했습니다. | 클러스터된 파일 공유는 지속적인 가용성을 사용하지 않는 경우 작은 쓰기(로밍 사용자 프로필에 일반적임)에 비해 우수한 성능을 제공합니다. |
| 2014년 3월 19일 | 프로필 버전 접미사 (합니다. V2 합니다. V3. V4)에서 [부록 b: 프로필 버전 참조 정보](#appendix-b-profile-version-reference-information)합니다. | Windows는 대/소문자 구분, 파일 공유를 사용 하 여 NFS를 사용 하는 경우 이지만 올바른 (대문자) 대/소문자 프로필 접미사에 대 한 것이 중요 합니다. |
| 2013년 10월 9일 | 몇 가지를 설명 했습니다 추가 Windows Server 2012 R2 및 Windows 8.1 대 한 수정 합니다 [여러 버전의 Windows에서 로밍 사용자 프로필을 사용 하는 경우 고려 사항](#considerations-when-using-roaming-user-profiles-on-multiple-versions-of-windows) 고 [부록 b: 프로필 버전 참조 정보](#appendix-b-profile-version-reference-information) 섹션입니다. | 새 버전에 대 한 업데이트 고객 의견 |

## <a name="more-information"></a>자세한 정보

- [폴더 리디렉션, 오프 라인 파일 및 로밍 사용자 프로필 배포](deploy-folder-redirection.md)
- [폴더 리디렉션 및 로밍 사용자 프로필에 대 한 기본 컴퓨터 배포](deploy-primary-computers.md)
- [사용자 상태 관리 구현](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc784645(v=ws.10)>)
- [복제 된 사용자 프로필 데이터에 대 한 Microsoft의 지원 정책](https://blogs.technet.microsoft.com/askds/2010/09/01/microsofts-support-statement-around-replicated-user-profile-data/)
- [DISM 사용 하 여 앱을 사이드 로드](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/hh852635(v=win.10)>)
- [패키징, 배포 및 Windows 런타임 기반 앱의 쿼리 문제 해결](https://msdn.microsoft.com/library/windows/desktop/hh973484.aspx)