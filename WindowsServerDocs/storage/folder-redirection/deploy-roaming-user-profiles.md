---
title: 로밍 사용자 프로필 배포
TOCTitle: Deploying Roaming User Profiles
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.date: 06/07/2019
ms.author: jgerend
ms.openlocfilehash: 8feed2adb606edfb6068d7fe10c18baf142077ac
ms.sourcegitcommit: 07c9d4ea72528401314e2789e3bc2e688fc96001
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/29/2020
ms.locfileid: "76822346"
---
# <a name="deploying-roaming-user-profiles"></a>로밍 사용자 프로필 배포

>적용 대상: Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Server 2019, Windows Server 2016, Windows Server(반기 채널), Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

이 토픽에서는 Windows Server를 사용하여 Windows 클라이언트 컴퓨터에 [로밍 사용자 프로필](folder-redirection-rup-overview.md)을 배포하는 방법에 대해 설명합니다. 로밍 사용자 프로필은 사용자가 여러 컴퓨터에서 동일한 운영 체제 및 애플리케이션 설정을 받을 수 있도록 사용자 프로필을 파일 공유로 리디렉션합니다.

이 토픽의 최근 변경 내용 목록은 이 항목의 [변경 내용](#change-history) 섹션을 참조하세요.

> [!IMPORTANT]
> [MS16-072](https://support.microsoft.com/help/3163622/ms16-072-security-update-for-group-policy-june-14%2c-2016)의 보안 변경으로 인해 이 토픽의 [4단계: 로밍 사용자 프로필에 대한 GPO 만들기(선택 사항)](#step-4-optionally-create-a-gpo-for-roaming-user-profiles)가 업데이트되었습니다. 이는 Windows에서 로밍 사용자 프로필을 올바르게 적용할 수 있도록(그리고 영향을 받은 PC에서 로컬 정책으로 되돌리지 않도록) 보장하기 위한 조치입니다.

> [!IMPORTANT]
>  다음 구성에서 OS의 현재 위치 업그레이드 후 시작에 대한 사용자 지정 항목이 손실됩니다.
> - 로밍 프로필에 대한 사용자가 구성됨
> - 사용자가 시작을 변경할 수 있음
>
> 결과적으로 시작 메뉴는 OS 현재 위치 업그레이드 후 새 OS 버전의 기본값으로 다시 설정됩니다. 해결 방법은 [부록 C: 업그레이드 후 시작 메뉴 레이아웃을 다시 설정하는 작업 수행](#appendix-c-working-around-reset-start-menu-layouts-after-upgrades)을 참조하세요.

## <a name="prerequisites"></a>필수 구성 요소

### <a name="hardware-requirements"></a>하드웨어 요구 사항

로밍 사용자 프로필에는 x64 기반 또는 x86 기반 컴퓨터가 필요하며, 이는 Windows RT에서 지원되지 않습니다.

### <a name="software-requirements"></a>소프트웨어 요구 사항

로밍 사용자 프로필에 대한 소프트웨어 요구 사항은 다음과 같습니다.

- 기존 로컬 사용자 프로필이 있는 환경에 폴더 리디렉션과 함께 로밍 사용자 프로필을 배포하는 경우 로밍 사용자 프로필 전에 폴더 리디렉션을 배포하여 로밍 프로필의 크기를 최소화합니다. 기존 사용자 폴더가 리디렉션되고 나면 로밍 사용자 프로필을 배포할 수 있습니다.
- 로밍 사용자 프로필을 관리하려면 Domain Administrators 보안 그룹, Enterprise Administrators 보안 그룹 또는 Group Policy Creator Owners 그룹의 구성원으로 로그인해야 합니다.
- 클라이언트 컴퓨터에서 Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Vista, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 또는 Windows Server 2008을 실행해야 합니다.
- 현재 관리 중인 AD DS(Active Directory 도메인 서비스)에 클라이언트 컴퓨터가 가입되어 있어야 합니다.
- 그룹 정책 관리 및 설치된 Active Directory 관리 센터에서 컴퓨터를 사용할 수 있어야 합니다.
- 파일 서버를 사용하여 로밍 사용자 프로필을 호스트할 수 있어야 합니다.

    - 파일 공유에서 DFS 네임스페이스를 사용하는 경우 사용자가 서로 다른 서버에서 충돌하는 편집 작업을 수행하지 못하도록 DFS 폴더(링크)에 단일 대상이 있어야 합니다.
    - 파일 공유에서 DFS 복제를 사용하여 다른 서버에 콘텐츠를 복제하는 경우 사용자가 서로 다른 서버에서 충돌하는 편집 작업을 수행하지 못하도록 원본 서버에만 액세스할 수 있도록 해야 합니다.
    - 파일 공유가 클러스터된 경우 성능 문제를 방지하려면 파일 공유에서 지속적인 가용성을 사용하지 않도록 설정합니다.
- 로밍 사용자 프로필의 기본 컴퓨터 지원을 사용하려면 추가적인 클라이언트 컴퓨터 및 Active Directory 스키마 요구 사항을 충족해야 합니다. 자세한 내용은 [폴더 리디렉션 및 로밍 사용자 프로필용 기본 컴퓨터 배포](deploy-primary-computers.md)를 참조하세요.
- PC, 원격 데스크톱 세션 호스트 또는 VDI(가상 데스크톱 인프라) 서버를 여러 대 사용하는 경우 사용자의 시작 메뉴 레이아웃이 Windows 10, Windows Server 2019 또는 Windows Server 2016에서 로밍되지 않습니다. 이 토픽에 설명된 대로 시작 레이아웃을 지정하여 문제를 해결할 수 있습니다. 또는 원격 데스크톱 세션 호스트 서버 또는 VDI 서버와 함께 사용하면 시작 메뉴 설정을 적절하게 로밍하는 사용자 프로필 디스크를 사용해도 됩니다. 자세한 내용은 [Windows Server 2012에서 사용자 프로필 디스크를 사용하여 보다 쉽게 사용자 데이터 관리](https://blogs.technet.microsoft.com/enterprisemobility/2012/11/13/easier-user-data-management-with-user-profile-disks-in-windows-server-2012/)를 참조하세요.

### <a name="considerations-when-using-roaming-user-profiles-on-multiple-versions-of-windows"></a>여러 버전의 Windows에서 로밍 사용자 프로필을 사용할 때의 고려 사항

여러 버전의 Windows에서 로밍 사용자 프로필을 사용하려는 경우 다음 작업을 수행하는 것이 좋습니다.

- 각 운영 체제 버전에 대한 별도의 프로필 버전을 유지하도록 Windows를 구성합니다. 이는 프로필 손상과 같은 원치 않고 예측할 수 없는 문제를 방지하는 데 도움이 됩니다.
- 폴더 리디렉션을 사용하여 문서 및 사진과 같은 사용자 파일을 사용자 프로필 외부에 저장합니다. 이렇게 하면 동일한 파일을 여러 운영 체제 버전에서 사용할 수 있습니다. 또한 프로필이 작은 크기로 유지되고 로그인 속도가 빨라집니다.
- 로밍 사용자 프로필에 대한 충분한 스토리지를 할당합니다. 두 운영 체제 버전을 지원하는 경우 각 운영 체제 버전에 대해 별도의 프로필이 유지되므로 프로필 수가 두 배로 증가하며, 따라서 사용된 총 공간도 두 배로 증가합니다.
- Windows Vista/Windows Server 2008 및 Windows 7/Windows Server 2008 R2를 실행하는 컴퓨터에서는 로밍 사용자 프로필을 사용하지 마세요. 이러한 운영 체제 버전 간의 로밍은 프로필 버전의 비호환성으로 인해 지원되지 않습니다.
- 한 운영 체제 버전에서 적용된 변경 내용이 다른 운영 체제 버전으로 로밍되지 않는다는 점을 사용자에게 알려주세요.
- 다른 프로필 버전을 사용하는 Windows 버전으로 환경을 이동하는 경우(예를 들어 Windows 10에서 Windows 10 버전 1607로 이동하는 경우 [부록 B: 프로필 버전 참조 정보](#appendix-b-profile-version-reference-information)의 목록 참조) 사용자는 비어 있는 새 로밍 사용자 프로필을 받게 됩니다. 폴더 리디렉션을 사용하여 공통 폴더를 리디렉션하면 새 프로필을 가져올 때 발생하는 영향을 최소화할 수 있습니다. 한 프로필 버전에서 다른 프로필 버전으로 로밍 사용자 프로필을 마이그레이션할 수 있는 방법은 없습니다.

## <a name="step-1-enable-the-use-of-separate-profile-versions"></a>1단계: 별도 프로필 버전 사용

Windows 8.1, Windows 8, Windows Server 2012 R2 또는 Windows Server 2012를 실행하는 컴퓨터에 로밍 사용자 프로필을 배포하려는 경우에는 배포 전에 Windows 환경을 약간 변경하는 것이 좋습니다. 이러한 변경 내용은 향후 운영 체제 업그레이드를 원활하게 하고, 로밍 사용자 프로필과 함께 여러 버전의 Windows를 보다 쉽게 동시에 실행하도록 해줍니다.

이러한 변경 내용을 적용하려면 다음 절차를 사용합니다.

1. 로밍, 필수, 상위 필수 또는 도메인 기본 프로필을 사용하려는 모든 컴퓨터에 적절한 소프트웨어 업데이트를 다운로드하여 설치합니다.

    - Windows 8.1 또는 Windows Server 2012 R2: Microsoft 기술 자료 문서 [2887595](https://support.microsoft.com/kb/2887595)에 설명된 소프트웨어 업데이트를 설치합니다.
    - Windows 8 또는 Windows Server 2012: Microsoft 기술 자료 문서 [2887239](https://support.microsoft.com/kb/2887239) 에 설명된 소프트웨어 업데이트를 설치합니다.

2. Windows 8.1, Windows 8, Windows Server 2012 R2 또는 Windows Server 2012를 실행하는 모든 컴퓨터 중 로밍 사용자 프로필을 사용할 컴퓨터에서 레지스트리 편집기 또는 그룹 정책을 사용하여 다음 레지스트리 키 DWORD 값을 만들고 `1`로 설정합니다. 그룹 정책을 사용하여 레지스트리 키를 만드는 방법에 대한 자세한 내용은 [레지스트리 항목 구성](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753092(v=ws.11)>)을 참조하세요.

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

로밍 사용자 프로필에 대한 보안 그룹을 만드는 방법은 다음과 같습니다.

1. Active Directory 관리 센터가 설치된 컴퓨터에서 서버 관리자를 엽니다.
2. **도구** 메뉴에서 **Active Directory 관리 센터**를 선택합니다. Active Directory 관리 센터가 표시됩니다.
3. 해당 도메인이나 OU를 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 선택한 다음, **그룹**을 선택합니다.
4. **그룹 만들기** 창의 **그룹** 섹션에서 다음 설정을 지정합니다.

    - **그룹 이름**에 보안 그룹의 이름(예: **Roaming User Profiles Users and Computers**)을 입력합니다.
    - **그룹 범위**에서 **보안**을 선택한 다음, **글로벌**을 선택합니다.

5. **구성원** 섹션에서 **추가**를 선택합니다. 사용자, 연락처, 컴퓨터, 서비스 계정 또는 그룹 선택 대화 상자가 나타납니다.
6. 이 보안 그룹에 컴퓨터 계정을 포함하려면 **개체 유형**을 클릭하고 **컴퓨터** 확인란을 선택한 다음, **확인**을 선택합니다.
7. 로밍 사용자 프로필을 배포할 사용자, 그룹 및/또는 컴퓨터의 이름을 입력하고 **확인**을 선택한 다음. **확인** 을 다시 선택합니다.

## <a name="step-3-create-a-file-share-for-roaming-user-profiles"></a>3단계: 로밍 사용자 프로필에 대한 파일 공유 만들기

로밍 사용자 프로필에 대한 별도의 파일 공유(로밍 프로필 폴더를 의도치 않게 캐싱하는 일을 방지하기 위한 리디렉션된 폴더의 공유와는 별개)가 아직 없는 경우 다음 절차에 따라 Windows Server를 실행하는 서버에 파일 공유를 만듭니다.

> [!NOTE]
> 사용 중인 Windows Server 버전에 따라 일부 기능이 다르거나 사용하지 못할 수 있습니다.

Windows Server에 파일 공유를 만드는 방법은 다음과 같습니다.

1. 서버 관리자 탐색 창에서 **파일 및 스토리지 서비스**를 선택한 다음, **공유**를 선택하여 공유 페이지를 표시합니다.
2. [공유] 타일에서 **작업**을 선택한 다음, **새 공유**를 선택합니다. 새 공유 마법사가 나타납니다.
3. **프로필 선택** 페이지에서 **SMB 공유 – 빠른**을 선택합니다. 파일 서버 리소스 관리자가 설치되어 있고 폴더 관리 속성을 사용하는 경우에는 대신 **SMB 공유 - 고급**을 선택합니다.
4. **공유 위치** 페이지에서 공유를 만들 서버 및 볼륨을 선택합니다.
5. **공유 이름** 페이지의 **공유 이름**상자에 공유 이름(예: **User Profiles$** )을 입력합니다.

    > [!TIP]
    > 공유를 만들 때 공유 이름 뒤에 ```$``` 를 붙여 공유를 숨깁니다. 그러면 일반 브라우저에서 공유가 숨겨집니다.

6. **기타 설정** 페이지에서 **지속적인 가용성 사용** 확인란(있는 경우)을 선택 취소하고 필요에 따라 **액세스 기반 열거 사용** 및 **데이터 액세스 암호화** 확인란을 선택합니다.
7. **사용 권한** 페이지에서 **사용 권한 사용자 지정**을 선택합니다. 고급 보안 설정 대화 상자가 나타납니다.
8. **상속 사용 안 함**을 선택한 다음, **상속된 사용 권한을 이 개체에 대한 명시적 사용 권한으로 변환합니다.** 를 선택합니다.
9. [로밍 사용자 프로필을 호스트하는 파일 공유에 필요한 권한](#required-permissions-for-the-file-share-hosting-roaming-user-profiles)에 설명되고 다음 스크린샷에 표시된 대로, 나열되지 않은 그룹 및 계정에 대한 권한을 제거하고 1단계에서 만든 로밍 사용자 프로필 사용자 및 컴퓨터 그룹에 특정 권한을 추가하여 사용 권한을 설정합니다.
    
    ![표1에 설명된 대로 사용 권한을 보여주는 고급 보안 설정 창](media/advanced-security-user-profiles.jpg)
    
    **그림 1** 로밍 사용자 프로필 공유에 대한 권한 설정
10. **SMB 공유 - 고급** 프로필을 선택한 경우 **관리 속성** 페이지에서 **사용자 파일** 폴더 사용량 값을 선택합니다.
11. **SMB 공유 - 고급** 프로필을 선택한 경우 **할당량** 페이지에서 필요에 따라 공유의 사용자에게 적용할 할당량을 선택합니다.
12. **확인** 페이지에서 **만들기**를 선택합니다.

### <a name="required-permissions-for-the-file-share-hosting-roaming-user-profiles"></a>로밍 사용자 프로필을 호스트하는 파일 공유에 필요한 권한

| 사용자 계정 | 액세스 | 적용 대상 |
|   -   |   -   |   -   |
|   System    |  모든 권한     |  이 폴더, 하위 폴더 및 파일     |
|  Administrators     |  모든 권한     |  이 폴더만     |
|  만든 이/소유자     |  모든 권한     |  하위 폴더 및 파일만     |
| 공유에 데이터를 저장해야 하는 사용자의 보안 그룹(Roaming User Profiles Users and Computers)      |  폴더 나열/데이터 읽기 *(고급 권한)* <br />폴더 만들기/데이터 추가 *(고급 권한)* |  이 폴더만     |
| 다른 그룹 및 계정   |  없음(제거)     |       |

## <a name="step-4-optionally-create-a-gpo-for-roaming-user-profiles"></a>4단계: 로밍 사용자 프로필에 대한 GPO 만들기(선택 사항)

로밍 사용자 프로필 설정에 대해 만든 GPO가 아직 없는 경우 다음 절차를 사용하여 로밍 사용자 프로필에서 사용할 빈 GPO를 만듭니다. 이 GPO를 사용하여 로밍 사용자 프로필 설정(예: 기본 컴퓨터 지원(별도 설명 참조))을 구성할 수 있으며, 컴퓨터에서 로밍 사용자 프로필을 사용하도록 설정(가상화된 데스크톱 환경에서 배포하거나 원격 데스크톱 서비스를 사용하는 경우에 일반적)할 수 있습니다.

로밍 사용자 프로필에 대한 GPO를 만드는 방법은 다음과 같습니다.

1. 그룹 정책 관리가 설치된 컴퓨터에서 서버 관리자를 엽니다.
2. **도구** 메뉴에서 **그룹 정책 관리**를 선택합니다. 그룹 정책 관리가 나타납니다.
3. 로밍 사용자 프로필을 설치할 도메인 또는 OU를 마우스 오른쪽 단추로 클릭한 다음, **이 도메인에서 GPO를 만들어 여기에 연결**을 선택합니다.
4. **새 GPO** 대화 상자에서 GPO 이름(예: **로밍 사용자 프로필 설정**)을 입력하고 **확인**을 선택합니다.
5. 새로 만든 GPO를 마우스 오른쪽 단추로 클릭하고 **연결 사용** 확인란의 선택을 취소합니다. 그러면 구성을 마칠 때까지 GPO가 적용되지 않습니다.
6. GPO를 선택합니다. **범위** 탭의 **보안 필터링** 섹션에서 **인증된 사용자**를 선택하고 **제거**를 선택하여 GPO가 모든 사용자에게 적용되지 않도록 합니다.
7. **보안 필터링** 섹션에서 **추가**를 선택합니다.
8. **사용자, 컴퓨터 또는 그룹 선택** 대화 상자에서 1단계에서 만든 보안 그룹의 이름(예: **로밍 사용자 프로필 사용자 및 컴퓨터**)을 입력하고 **확인**을 선택합니다.
9. **위임** 탭을 선택하고 **추가**를 선택하고 **인증된 사용자**를 입력한 다음, **확인**을 선택하고 다시 **확인**을 선택하여 기본 읽기 권한을 적용합니다.
    
    [MS16-072](https://support.microsoft.com/help/3163622/ms16-072-security-update-for-group-policy-june-14%2c-2016)의 보안 변경으로 인해 이 단계가 필요합니다.

>[!IMPORTANT]
>[MS16-072A](https://support.microsoft.com/help/3163622/ms16-072-security-update-for-group-policy-june-14%2c-2016)의 보안 변경으로 인해, 이제 인증된 사용자 그룹에 GPO에 대한 읽기 권한을 위임해야 합니다. 그렇지 않으면 GPO가 사용자에게 적용되지 않거나, 이미 적용된 경우 GPO가 제거되고 사용자 프로필이 다시 로컬 PC로 리디렉션됩니다. 자세한 내용은 [그룹 정책 보안 업데이트 MS16-072 배포](https://blogs.technet.microsoft.com/askds/2016/06/22/deploying-group-policy-security-update-ms16-072-kb3163622/)를 참조하세요.

## <a name="step-5-optionally-set-up-roaming-user-profiles-on-user-accounts"></a>5단계: 사용자 계정에 로밍 사용자 프로필 설치(선택 사항)

사용자 계정에 로밍 사용자 프로필을 배포하려면 다음 절차를 사용하여 Active Directory Domain Services의 사용자 계정에 대한 로밍 사용자 프로필을 지정합니다. 원격 데스크톱 서비스 또는 가상화된 데스크톱 배포에서 일반적으로 하던 것처럼 컴퓨터에 로밍 사용자 프로필을 배포하려면 [6단계: 컴퓨터에 로밍 사용자 프로필 설치(선택 사항)](#step-6-optionally-set-up-roaming-user-profiles-on-computers)에 설명된 절차를 따릅니다.

> [!NOTE]
> Active Directory를 사용하여 사용자 계정에 로밍 사용자 프로필을 설치하고, 그룹 정책을 사용하여 컴퓨터에 로밍 사용자 프로필을 설치한 경우 컴퓨터 기반 정책 설정이 우선적으로 적용됩니다.

사용자 계정에 로밍 사용자 프로필을 설치하는 방법은 다음과 같습니다.

1. Active Directory 관리 센터에서 적절한 도메인의 **사용자** 컨테이너(또는 OU)로 이동합니다.
2. 로밍 사용자 프로필을 할당할 모든 사용자를 선택하고 마우스 오른쪽 단추로 클릭한 다음, **속성**을 선택합니다.
3. **프로필** 섹션에서 **프로필 경로:** 확인란을 선택하고 사용자의 로밍 사용자 프로필을 저장할 파일 공유의 경로를 입력합니다(경로 맨 뒤에 사용자가 처음 로그인하면 자동으로 사용자 이름으로 바뀌는 `%username%` 추가). 예:
    
    `\\fs1.corp.contoso.com\User Profiles$\%username%`
    
    필수 로밍 사용자 프로필을 지정하려면 경로를 이전에 만든 NTuser.man 파일의 경로(예: `fs1.corp.contoso.comUser Profiles$default`)로 지정합니다. 자세한 내용은 [필수 사용자 프로필 만들기](https://docs.microsoft.com/windows/client-management/mandatory-user-profile)를 참조하세요.
4. **확인**을 선택합니다.

> [!NOTE]
> 로밍 사용자 프로필을 사용할 때는 기본적으로 모든 Windows® 런타임 기반(Windows 스토어) 앱의 배포가 허용됩니다. 그러나 특수 프로필을 사용할 때는 앱이 기본적으로 배포되지 않습니다. 특수 프로필은 사용자가 로그아웃한 후 변경 내용이 삭제되는 사용자 프로필입니다.
> <br><br>특수 프로필에 대한 앱 배포 제한을 제거하려면 **Allow deployment operations in special profiles** 정책 설정(컴퓨터 구성\정책\관리 템플릿\앱 패키지 배포에 있음)을 사용합니다. 그러나 이 시나리오에서 배포된 앱은 일부 데이터가 컴퓨터에 그대로 남아 있으므로 단일 컴퓨터의 사용자가 수백 명인 경우 누적될 수 있습니다. 앱을 정리하려면 [CleanupPackageForUserAsync](https://msdn.microsoft.com/library/windows/apps/windows.management.deployment.packagemanager.cleanuppackageforuserasync.aspx) API를 사용하는 도구를 찾거나 개발하여 컴퓨터에 더 이상 프로필이 없는 사용자에 대한 앱 패키지를 정리합니다.
> <br><br>Windows 스토어 앱에 대한 추가 배경 정보는 [Windows 스토어에 대한 클라이언트 액세스 관리](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/hh832040(v=ws.11)>)를 참조하세요.

## <a name="step-6-optionally-set-up-roaming-user-profiles-on-computers"></a>6단계: 컴퓨터에 로밍 사용자 프로필 설치(선택 사항)

컴퓨터에 로밍 사용자 프로필을 배포하려면 원격 데스크톱 서비스 또는 가상화된 데스크톱 배포에 일반적인 방식대로 다음 절차를 사용합니다. 사용자 계정에 로밍 사용자 프로필을 배포하려면 [5단계: 사용자 계정에 로밍 사용자 프로필 설치(선택 사항)](#step-5-optionally-set-up-roaming-user-profiles-on-user-accounts)에 설명된 절차를 따릅니다.

그룹 정책을 사용하여 Windows 8.1, Windows 8, Windows 7, Windows Vista, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 또는 Windows Server 2008을 실행하는 컴퓨터에 로밍 사용자 프로필을 적용할 수 있습니다.

> [!NOTE]
> 그룹 정책을 사용하여 컴퓨터에 로밍 사용자 프로필을 설치하고, Active Directory를 사용하여 사용자 계정에 로밍 사용자 프로필을 설치한 경우 컴퓨터 기반 정책 설정이 우선적으로 적용됩니다.

컴퓨터에 로밍 사용자 프로필을 설치하는 방법은 다음과 같습니다.

1. 그룹 정책 관리가 설치된 컴퓨터에서 서버 관리자를 엽니다.
2. **도구** 메뉴에서 **그룹 정책 관리**를 선택합니다. 그룹 정책 관리가 나타납니다.
3. 그룹 정책 관리에서, 3단계에서 만든 GPO(예: **로밍 사용자 프로필 설정**)를 마우스 오른쪽 단추로 클릭한 다음, **편집**을 선택합니다.
4. 그룹 정책 관리 편집기 창에서 **컴퓨터 구성**, **정책**, **관리 템플릿**, **시스템**, **사용자 프로필**로 차례로 이동합니다.
5. **이 컴퓨터에 로그온하는 모든 사용자의 로밍 프로필 경로 설정** 을 마우스 오른쪽 단추로 클릭한 다음, **편집**을 선택합니다.
    > [!TIP]
    > 사용자의 홈 폴더(구성된 경우)는 Windows PowerShell과 같은 일부 프로그램에서 사용하는 기본 폴더입니다. AD DS에서 사용자 계정 속성의 **홈 폴더** 섹션을 사용하여 사용자별 대체 로컬 또는 네트워크 위치를 구성할 수 있습니다. 가상 데스크톱 환경에서 Windows 8.1, Windows 8, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012를 실행하는 컴퓨터의 모든 사용자에 대한 홈 폴더 위치를 구성하려면 **사용자 홈 폴더 설정** 정책 설정을 사용하도록 설정한 다음, 매핑할 파일 공유 및 드라이브 문자를 지정합니다(또는 로컬 폴더를 지정). 환경 변수나 줄임표를 사용하지 마세요. 사용자가 로그온한 동안 지정한 경로 끝에 사용자의 별칭이 추가됩니다.
6. **속성** 대화 상자에서 **사용**을 선택합니다.
7. **이 컴퓨터에 로그온하는 사용자는 다음 로밍 프로필 경로를 사용해야 함** 상자에서 사용자의 로밍 사용자 프로필을 저장할 파일 공유의 경로를 입력합니다(경로 맨 뒤에 사용자가 처음 로그인하면 자동으로 사용자 이름으로 바뀌는 `%username%` 추가). 예:

    `\\fs1.corp.contoso.com\User Profiles$\%username%`

    사용자가 영구적으로 변경할 수 없는(사용자가 로그아웃하면 변경 내용이 다시 설정됨) 미리 구성된 프로필인 필수 로밍 사용자 프로필을 지정하려면 경로를 이전에 만든 NTuser.man 파일의 경로(예: `\\fs1.corp.contoso.com\User Profiles$\default`)로 지정합니다. 자세한 내용은 [필수 사용자 프로필 만들기](https://docs.microsoft.com/windows/client-management/mandatory-user-profile)를 참조하세요.
8. **확인**을 선택합니다.

## <a name="step-7-optionally-specify-a-start-layout-for-windows-10-pcs"></a>7단계: Windows 10 PC의 시작 레이아웃 지정(선택 사항)

사용자가 모든 PC에서 동일한 시작 레이아웃을 볼 수 있도록 그룹 정책을 사용하여 특정 시작 메뉴 레이아웃을 적용할 수 있습니다. 사용자가 두 대 이상의 PC에서 로그인하고 모든 PC에서 일관적인 시작 레이아웃을 사용자에게 제공하려면 사용자의 모든 PC에 GPO를 적용해야 합니다.

시작 레이아웃을 지정하려면 다음을 수행합니다.

1. Windows 10 PC를 Windows 10 버전 1607(1주년 업데이트라고도 함) 이상으로 업데이트하고, 2017년 3월 14일 누적 업데이트([KB4013429](https://support.microsoft.com/kb/4013429)) 이상을 설치합니다.
2. 전체 또는 부분 시작 메뉴 레이아웃 XML 파일을 만듭니다. 이렇게 하려면 [시작 레이아웃 사용자 지정 및 내보내기](https://docs.microsoft.com/windows/configuration/customize-and-export-start-layout)를 참조하세요.
    * *전체* 시작 레이아웃을 지정하면 사용자가 시작 메뉴의 어떤 부분도 사용자 지정할 수 없습니다. *부분* 시작 레이아웃을 지정하면 사용자는 관리자가 지정하는 잠긴 타일 그룹을 제외한 모든 항목을 사용자 지정할 수 있습니다. 그러나 부분 시작 레이아웃을 사용하는 경우 시작 메뉴에 대한 사용자 지정이 다른 PC로 로밍되지 않습니다.
3. 그룹 정책을 사용하여 로밍 사용자 프로필에 대해 만든 GPO에 사용자 지정된 시작 레이아웃을 적용할 수 있습니다. 이렇게 하려면 [그룹 정책을 사용하여 도메인에서 사용자 지정된 시작 화면 레이아웃 적용](https://docs.microsoft.com/windows/configuration/customize-windows-10-start-screens-by-using-group-policy#bkmk-domaingpodeployment)을 참조하세요.
4. 그룹 정책을 사용하여 Windows 10 PC에서 다음 레지스트리 값을 설정합니다. 이렇게 하려면 [레지스트리 항목 구성](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753092(v=ws.11)>)을 참조하세요.

| **작업**   | **업데이트**                  |
| ------------ | ------------                |
| Hive         | **HKEY_LOCAL_MACHINE**      |
| 키 경로     | **Software\Microsoft\Windows\CurrentVersion\Explorer** |
| 값 이름   | **SpecialRoamingOverrideAllowed** |
| 값 유형   | **REG_DWORD**               |
| 값 데이터   | **1**(또는 사용하지 않으려면 **0**) |
| 기준         | **10진수**                 |

5. (선택 사항) 사용자가 더 빠르게 로그인할 수 있도록 최초 로그온 최적화를 사용하도록 설정합니다. 이렇게 하려면 [로그인 시간을 줄이는 정책 적용](https://docs.microsoft.com/windows/client-management/mandatory-user-profile#apply-policies-to-improve-sign-in-time)을 참조하세요.
6. (선택 사항) 클라이언트 PC를 배포하는 데 사용하는 Windows 10 기본 이미지에서 불필요한 앱을 제거하여 로그인 시간을 더욱 줄일 수 있습니다. Windows Server 2019 및 Windows Server 2016에는 미리 프로비저닝된 앱이 없으므로 서버 이미지에서 이 단계를 건너뛰어도 됩니다.
    - 앱을 제거하려면 Windows PowerShell에서 [Remove-AppxProvisionedPackage](https://docs.microsoft.com/powershell/module/dism/remove-appxprovisionedpackage?view=win10-ps) cmdlet을 사용하여 다음 애플리케이션을 제거합니다. PC가 이미 배포되어 있는 경우 [Remove-AppxPackage](https://docs.microsoft.com/powershell/module/appx/remove-appxpackage?view=win10-ps)를 사용하여 이러한 앱의 제거를 스크립팅할 수 있습니다.
    
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
>이러한 앱을 제거하면 로그인 시간이 단축되지만, 배포한 시스템에 이러한 앱이 필요한 경우 설치된 상태로 두면 됩니다.

## <a name="step-8-enable-the-roaming-user-profiles-gpo"></a>8단계: 로밍 사용자 프로필 GPO 사용

그룹 정책을 사용하여 컴퓨터에 로밍 사용자 프로필을 설치하거나 그룹 정책을 사용하여 다른 로밍 사용자 프로필 설정을 사용자 지정한 경우 영향을 받는 사용자에게 적용하도록 허용하는 GPO를 설정해야 합니다.

>[!TIP]
>기본 컴퓨터 지원을 구현할 생각이면 GPO를 사용하도록 설정하기 전에 지금 구현하세요. 그러면 기본 컴퓨터 지원을 사용하기 전에 사용자 데이터가 기본이 아닌 컴퓨터에 복사되는 것이 방지됩니다. 구체적인 정책 설정은 [폴더 리디렉션 및 로밍 사용자 프로필용 기본 컴퓨터 배포](deploy-primary-computers.md)를 참조하세요.

로밍 사용자 프로필 GPO를 사용하도록 설정하는 방법은 다음과 같습니다.

1. 그룹 정책 관리를 엽니다.
2. 앞에서 만든 GPO를 마우스 오른쪽 단추로 클릭한 다음, **연결 사용**을 선택합니다. 메뉴 항목 옆에 확인란이 표시됩니다.

## <a name="step-9-test-roaming-user-profiles"></a>9단계: 로밍 사용자 프로필 테스트

로밍 사용자 프로필을 테스트하려면 로밍 사용자 프로필에 대해 구성된 사용자 계정으로 컴퓨터에 로그인하거나, 로밍 사용자 프로필에 대해 구성된 컴퓨터에 로그인합니다. 그런 다음 프로필이 리디렉션되었는지 확인합니다.

로밍 사용자 프로필을 테스트하는 방법은 다음과 같습니다.

1. 로밍 사용자 프로필을 사용하도록 설정한 사용자 계정으로 기본 컴퓨터(기본 컴퓨터 지원을 사용하도록 설정한 경우)에 로그인합니다. 특정 컴퓨터에서 로밍 사용자 프로필을 사용하도록 설정한 경우 해당 컴퓨터 중 하나에 로그인합니다.
2. 사용자가 이전에 컴퓨터에 로그인한 경우 관리자 권한 명령 프롬프트를 열고 다음 명령을 입력하여 클라이언트 컴퓨터에 최신 그룹 정책 설정이 적용되었는지 확인합니다.
    
    ```PowerShell
    GpUpdate /Force
    ```
3. 사용자 프로필이 로밍 중인지 확인하려면 **제어판**을 열고 **시스템 및 보안**, **시스템**, **고급 시스템 설정**, **설정**(사용자 프로필 섹션)을 차례로 선택한 다음, **유형** 열에서 **로밍**을 확인합니다.

## <a name="appendix-a-checklist-for-deploying-roaming-user-profiles"></a>부록 A: 로밍 사용자 프로필 배포 검사 목록

| 상태                     | 작업                                                |
| ---                        | ------                                                |
| ☐<br>☐<br>☐<br>☐<br>☐   | 1. 도메인 준비<br>- 컴퓨터를 도메인에 조인<br>- 별도 프로필 버전 사용<br>- 사용자 계정 만들기<br>- (선택 사항) 폴더 리디렉션 배포 |
| ☐<br><br><br>             | 2. 로밍 사용자 프로필에 대한 보안 그룹 만들기<br>- 그룹 이름:<br>- 구성원: |
| ☐<br><br>                 | 3. 로밍 사용자 프로필에 대한 파일 공유 만들기<br>- 파일 공유 이름: |
| ☐<br><br>                 | 4. 로밍 사용자 프로필에 대한 GPO 만들기<br>- GPO 이름:|
| ☐                         | 5. 로밍 사용자 프로필 정책 설정 구성    |
| ☐<br>☐<br>☐              | 6. 로밍 사용자 프로필 사용<br>- 사용자 계정에서 AD DS를 사용하도록 설정되었습니까?<br>- 컴퓨터 계정에서 그룹 정책을 사용하도록 설정되었습니까?<br> |
| ☐                         | 7. (선택 사항) Windows 10 PC의 필수 시작 레이아웃 지정 |
| ☐<br>☐<br><br>☐<br><br>☐ | 8. (선택 사항) 기본 컴퓨터 지원 사용<br>- 사용자의 기본 컴퓨터 지정<br>- 사용자 및 기본 컴퓨터 매핑 위치:<br>- (선택 사항) 폴더 리디렉션에 기본 컴퓨터 지원 사용<br>- 컴퓨터 기반인가요 아니면 사용자 기반인가요?<br>- (선택 사항) 로밍 사용자 프로필에 기본 컴퓨터 지원 사용 |
| ☐                        | 9. 로밍 사용자 프로필 GPO 사용                |
| ☐                        | 10. 로밍 사용자 프로필 테스트                         |

## <a name="appendix-b-profile-version-reference-information"></a>부록 B: 프로필 버전 참조 정보

프로필마다 프로필이 사용되는 Windows 버전에 해당하는 프로필 버전이 있습니다. 예를 들어 Windows 10 버전 1703 및 버전 1607은 둘 다 .V6 프로필 버전을 사용합니다. Microsoft는 호환성 유지를 위해 필요한 경우에만 새 프로필 버전을 만듭니다. 따라서 Windows의 모든 버전에 새 프로필 버전이 포함되는 것은 아닙니다.

다음 표에는 여러 Windows 버전의 로밍 사용자 프로필 위치가 나와 있습니다.

| 운영 체제 버전 | 로밍 사용자 프로필 위치 |
| --- | --- |
| Windows XP 및 Windows Server 2003 | ```\\<servername>\<fileshare>\<username>``` |
| Windows Vista 및 Windows Server 2008 | ```\\<servername>\<fileshare>\<username>.V2``` |
| Windows 7 및 Windows Server 2008 R2 | ```\\<servername>\<fileshare>\<username>.V2``` |
| Windows 8 및 Windows Server 2012 | ```\\<servername>\<fileshare>\<username>.V3```(소프트웨어 업데이트 및 레지스트리 키 적용 후)<br>```\\<servername>\<fileshare>\<username>.V2```(소프트웨어 업데이트 및 레지스트리 키 적용 전) |
| Windows 8.1 및 Windows Server 2012 R2 | ```\\<servername>\<fileshare>\<username>.V4```(소프트웨어 업데이트 및 레지스트리 키 적용 후)<br>```\\<servername>\<fileshare>\<username>.V2```(소프트웨어 업데이트 및 레지스트리 키 적용 전) |
| Windows 10 | ```\\<servername>\<fileshare>\<username>.V5``` |
| Windows 10 버전 1703 및 1607 | ```\\<servername>\<fileshare>\<username>.V6``` |

## <a name="appendix-c-working-around-reset-start-menu-layouts-after-upgrades"></a>부록 C: 업그레이드 후 시작 메뉴 레이아웃을 다시 설정하는 작업 수행

다음은 현재 위치 업그레이드 후 시작 메뉴 레이아웃이 초기화되는 문제를 해결하는 몇 가지 방법입니다.

- 사용자 한 명만 디바이스를 사용하고 IT 관리자는 Configuration Manager 같은 관리형 OS 배포 전략을 사용하는 경우 다음을 수행할 수 있습니다.
    
  1. 업그레이드하기 전에 Export-Startlayout을 사용하여 시작 메뉴 레이아웃 내보내기 
  2. OOBE가 끝나고 사용자가 로그인하기 전에 Import-StartLayout을 사용하여 시작 메뉴 레이아웃 가져오기  
 
     > [!NOTE] 
     > StartLayout을 가져오면 기본 사용자 프로필이 수정됩니다. 가져오기를 수행한 이후에 만들어지는 모든 사용자 프로필은 가져온 시작 레이아웃을 갖게 됩니다.
 
- IT 관리자는 그룹 정책을 사용하여 시작 레이아웃을 관리하도록 선택할 수 있습니다. 그룹 정책을 사용하면 사용자에게 표준화된 시작 레이아웃을 적용하는 중앙 집중식 관리 솔루션을 얻게 됩니다. 시작 관리에 그룹 정책을 사용하는 2가지 모드가 있습니다. 하나는 전체 잠금이고, 다른 하나는 부분 잠금입니다. 전체 잠금 시나리오를 사용하면 사용자가 시작 레이아웃을 변경할 수 없습니다. 부분 잠금 시나리오를 사용하면 사용자가 특정 시작 영역을 변경할 수 있습니다. 자세한 내용은 [시작 레이아웃 사용자 지정 및 내보내기](https://docs.microsoft.com/windows/configuration/customize-and-export-start-layout)를 참조하세요.
        
   > [!NOTE]
   > 부분 잠금 시나리오에서 사용자가 변경한 내용은 업그레이드 중에 손실됩니다.

- 시작 레이아웃이 초기화되고 최종 사용자가 시작을 다시 구성할 수 있도록 허용하세요. OS를 업그레이드한 후 영향을 최소화하려면 시작 레이아웃을 다시 설정하라는 알림 이메일 또는 기타 알림을 최종 사용자에게 보낼 수 있습니다. 

## <a name="change-history"></a>변경 기록

다음 표에는 이 항목의 중요한 최근 변경 내용이 요약되어 있습니다.

| 날짜 | 설명 |이유|
| --- | ---         | ---   |
| 2019년 5월 1일 | Windows Server 2019 업데이트 추가 |
| 2018년 4월 10일 | OS 현재 위치 업그레이드 후 시작에 대한 사용자 지정 내용이 손실되는 경우에 대한 정보 추가|설명선의 알려진 문제. |
| 2018년 3월 13일 | Windows Server 2016 업데이트 | 이전 버전의 라이브러리에서 이동하여 현재 버전의 Windows Server로 업데이트되었습니다. |
| 2017년 4월 13일 | Windows 10 버전 1703에 대한 프로필 정보가 추가되었으며, 운영 체제를 업그레이드할 때 로밍 프로필 버전의 작동 방식을 설명했습니다. [여러 버전의 Windows에서 로밍 사용자 프로필을 사용할 때의 고려 사항](#considerations-when-using-roaming-user-profiles-on-multiple-versions-of-windows) 을 참조하세요. | 고객 의견. |
| 2017년 3월 14일 | Windows 10 PC의 필수 시작 레이아웃을 지정하는 선택적 단계가 [부록 A: 로밍 사용자 프로필 배포 검사 목록](#appendix-a-checklist-for-deploying-roaming-user-profiles)에 추가되었습니다. |최신 Windows 업데이트의 기능 변경. |
| 2017년 1월 23일 | [4단계: 로밍 사용자 프로필에 대한 GPO 만들기(선택 사항)](#step-4-optionally-create-a-gpo-for-roaming-user-profiles)에 인증된 사용자에게 읽기 권한을 위임하는 단계가 추가되었습니다. 이번 그룹 정책 보안 업데이트 때문에 이 단계가 필수입니다.|그룹 정책 처리의 보안 변경. |
| 2016년 12월 29일 | [8단계: 로밍 사용자 프로필 GPO 사용](#step-8-enable-the-roaming-user-profiles-gpo)에 기본 컴퓨터의 그룹 정책을 설정하는 방법에 대한 정보를 쉽게 확인할 수 있는 링크가 추가되었습니다. 숫자가 잘못된 5단계 및 6단계에 대한 몇 가지 참조도 수정되었습니다.|고객 의견. |
| 2016년 12월 5일 | 시작 메뉴 설정 로밍 문제를 설명하는 정보가 추가되었습니다. | 고객 의견. |
| 2016년 7월 6일 | Windows 10 프로필 버전 접미사가 [부록 B: 프로필 버전 참조 정보](#appendix-b-profile-version-reference-information)에 추가되었습니다. 또한 지원되는 운영 체제 목록에서 Windows XP 및 Windows Server 2003이 제거되었습니다. | 새 버전의 Windows가 업데이트되고, 더 이상 지원되지 않는 Windows 버전에 대한 정보가 제거되었습니다. |
| 2015년 7월 7일 | 클러스터된 파일 서버를 사용하는 경우 지속적인 가용성을 사용하지 않도록 설정하는 단계 및 요구 사항을 추가했습니다. | 클러스터된 파일 공유는 지속적인 가용성을 사용하지 않는 경우 작은 쓰기(로밍 사용자 프로필에 일반적임)에 비해 우수한 성능을 제공합니다. |
| 2014년 3월 19일 | 프로필 버전 접미사(.V2, .V3, .V4)를 대문자로 변경 - [부록 B: 프로필 버전 참조 정보](#appendix-b-profile-version-reference-information)에 추가되었습니다. | Windows에서는 대/소문자를 구분하기 않지만, 파일 공유에서 NFS를 사용하는 경우 프로필 접미사를 대문자로 처리해야 합니다. |
| 2013년 10월 9일 | Windows Server 2012 R2 및 Windows 8.1이 수정되었고, 몇 가지 사항에 대한 명확한 설명이 추가되었고, [여러 버전의 Windows에서 로밍 사용자 프로필을 사용할 때의 고려 사항](#considerations-when-using-roaming-user-profiles-on-multiple-versions-of-windows) 및 [부록 B: 프로필 버전 참조 정보](#appendix-b-profile-version-reference-information) 섹션이 추가되었습니다. | 새 버전에 대한 업데이트, 고객 의견. |

## <a name="more-information"></a>자세한 정보

- [폴더 리디렉션, 오프라인 파일 및 로밍 사용자 프로필 배포](deploy-folder-redirection.md)
- [폴더 리디렉션 및 로밍 사용자 프로필용 기본 컴퓨터 배포](deploy-primary-computers.md)
- [사용자 상태 관리 구현](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc784645(v=ws.10)>)
- [복제된 사용자 프로필 데이터에 대한 Microsoft의 지원 정책](https://blogs.technet.microsoft.com/askds/2010/09/01/microsofts-support-statement-around-replicated-user-profile-data/)
- [DISM을 사용하여 앱을 테스트용으로 로드](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/hh852635(v=win.10)>)
- [Windows 런타임 기반 앱의 패키징, 배포 및 쿼리 문제 해결](https://msdn.microsoft.com/library/windows/desktop/hh973484.aspx)