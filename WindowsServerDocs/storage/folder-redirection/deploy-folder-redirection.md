---
title: 오프 라인 파일을 사용 하 여 폴더 리디렉션 배포
description: Windows Server 폴더 리디렉션 오프 라인 파일을 사용 하 여 Windows 클라이언트 컴퓨터에 배포를 사용 하는 방법입니다.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 06/06/2019
ms.localizationpriority: medium
ms.openlocfilehash: 4b6c58f0f33b45052e038a9af941297a294d17b2
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812511"
---
# <a name="deploy-folder-redirection-with-offline-files"></a>오프 라인 파일을 사용 하 여 폴더 리디렉션 배포

>적용 대상: Windows 10, Windows 7, Windows 8, Windows 8.1, Windows Vista, Windows Server 2019, Windows Server 2016, Windows Server 2012, Windows Server 2012 R2, Windows Server 2008 R2, Windows Server (반기 채널)

이 항목에서는 Windows Server 폴더 리디렉션 오프 라인 파일을 사용 하 여 Windows 클라이언트 컴퓨터에 배포를 사용 하는 방법을 설명 합니다.

이 항목에서는 최신 변경 내용 목록을 참조 하세요. [변경 내용](#change-history)합니다.

> [!IMPORTANT]
> 보안 변경 내용으로 인해 [MS16 072](https://support.microsoft.com/help/3163622/ms16-072-security-update-for-group-policy-june-14-2016)를 업데이트 했습니다 [3 단계: 폴더 리디렉션에 대 한 GPO를 만들어](#step-3-create-a-gpo-for-folder-redirection) 해당 Windows 고 수 있도록 제대로 폴더 리디렉션 정책 적용 (영향을 받는 Pc에서 리디렉션된 폴더를 전환 되지 않고)이이 항목의 합니다.

## <a name="prerequisites"></a>사전 요구 사항

### <a name="hardware-requirements"></a>하드웨어 요구 사항

폴더 리디렉션 필요는 x64 기반 또는 x86 기반 컴퓨터 Windows® rt 지원 되지 않습니다.

### <a name="software-requirements"></a>소프트웨어 요구 사항

폴더 리디렉션에 다음 소프트웨어 요구 사항:

- 폴더 리디렉션을 관리 하려면 Domain Administrators 보안 그룹, Enterprise Administrators 보안 그룹 또는 Group Policy Creator Owners 보안 그룹의 구성원으로 로그인 해야 합니다.
- 클라이언트 컴퓨터는 Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Server 2019, Windows Server 2016, Windows Server (반기 채널), Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 또는 Windows Server 2008 실행 해야 합니다.
- 현재 관리 중인 AD DS(Active Directory 도메인 서비스)에 클라이언트 컴퓨터가 가입되어 있어야 합니다.
- 그룹 정책 관리 및 설치된 Active Directory 관리 센터에서 컴퓨터를 사용할 수 있어야 합니다.
- 파일 서버는 리디렉션된 폴더를 호스트에 사용할 수 있어야 합니다.
    - 파일 공유에서 DFS 네임스페이스를 사용하는 경우 사용자가 서로 다른 서버에서 충돌하는 편집 작업을 수행하지 못하도록 DFS 폴더(링크)에 단일 대상이 있어야 합니다.
    - 파일 공유에서 DFS 복제를 사용하여 다른 서버에 콘텐츠를 복제하는 경우 사용자가 서로 다른 서버에서 충돌하는 편집 작업을 수행하지 못하도록 원본 서버에만 액세스할 수 있도록 해야 합니다.
    - 클러스터형된 파일 공유를 사용할 때 폴더 리디렉션 및 오프 라인 파일을 사용 하 여 성능 문제를 방지 하려면 파일 공유에서 지속적인 가용성을 사용 하지 않도록 설정 합니다. 또한 오프 라인 파일 수 하지 사용자가 오프 라인 파일의 항상 오프 라인 모드를 사용 하지 않는 사용자가 불편 해질 수는 지속적으로 사용 가능한 파일 공유에 대 한 액세스를 잃어버린 후 3-6 분 동안 오프 라인 모드로 전환 됩니다.

> [!NOTE]
> 일부 최신 폴더 리디렉션에서 기능이 추가 클라이언트 컴퓨터 및 Active Directory 스키마 요구 사항입니다. 자세한 내용은 참조 하세요. [의 기본 컴퓨터 배포](deploy-primary-computers.md)를 [사용 하지 않도록 설정에서 오프 라인 파일 폴더](disable-offline-files-on-folders.md)를 [사용 항상 오프 라인 모드](enable-always-offline.md), 및 [사용 최적화 폴더 이동 ](enable-optimized-moving.md).

## <a name="step-1-create-a-folder-redirection-security-group"></a>1단계: 폴더 리디렉션 보안 그룹 만들기

환경을 설정 하지 않으면 이미 폴더 리디렉션과 함께, 첫 번째 단계는 폴더 리디렉션 정책 설정을 적용 하려는 모든 사용자를 포함 하는 보안 그룹을 만드는 것입니다.

폴더 리디렉션에 대 한 보안 그룹을 만드는 방법은 다음과 같습니다.

1. 설치 된 Active Directory 관리 센터를 사용 하 여 컴퓨터에서 서버 관리자를 엽니다.
2. 에 **도구** 메뉴에서 **Active Directory 관리 센터**합니다. Active Directory 관리 센터가 표시됩니다.
3. 적절 한 도메인 또는 OU를 선택 하는 마우스 오른쪽 단추로 클릭 **새로 만들기**를 선택한 후 **그룹**합니다.
4. **그룹 만들기** 창의 **그룹** 섹션에서 다음 설정을 지정합니다.
    - **그룹 이름**에 보안 그룹의 이름(예: **폴더 리디렉션은 사용자**합니다.
    - **그룹 범위**를 선택 **보안**를 선택한 후 **Global**합니다.
5. 에 **멤버** 섹션에서 **추가**합니다. 사용자, 연락처, 컴퓨터, 서비스 계정 또는 그룹 선택 대화 상자가 나타납니다.
6. 사용자 또는 폴더 리디렉션을 사용을 선택 하려는 그룹의 이름을 입력 **확인**를 선택한 후 **확인** 다시 합니다.

## <a name="step-2-create-a-file-share-for-redirected-folders"></a>2단계: 리디렉션된 폴더에 대 한 파일 공유 만들기

리디렉션된 폴더에 대 한 파일 공유는 아직 없는 경우 Windows Server 2012를 실행 하는 서버에서 파일 공유를 만들려면 다음 절차를 사용 합니다.

> [!NOTE]
> 다른 버전의 Windows Server를 실행하는 서버에서 파일 공유를 만드는 경우 일부 기능이 다르거나 사용하지 못할 수도 있습니다.

Windows Server 2019, Windows Server 2016 및 Windows Server 2012에서 파일 공유를 만드는 방법에는 다음과 같습니다.

1. 서버 관리자 탐색 창에서 선택 **File and Storage Services**를 선택한 후 **공유** 공유 페이지를 표시 합니다.
2. 에 **공유** 타일을 선택 **태스크**를 선택한 후 **새 공유**합니다. 새 공유 마법사가 나타납니다.
3. 에 **프로필 선택** 페이지에서 선택 **SMB 공유 – 빠르게**합니다. 파일 서버 리소스 관리자가 설치 되어 있고 폴더 관리 속성을 사용 하는 경우 대신 선택할 **SMB 공유-고급**합니다.
4. **공유 위치** 페이지에서 공유를 만들 서버 및 볼륨을 선택합니다.
5. 에 **공유 이름** 페이지, 공유에 대 한 이름을 입력 (예를 들어 **사용자 $** )에 **공유 이름** 상자입니다.
    >[!TIP]
    >공유를 만들 때 공유 이름 뒤에 ```$``` 를 붙여 공유를 숨깁니다. 이렇게 하면 일반 브라우저에서 공유가 숨겨집니다.
6. 에 **기타 설정** 페이지에서 있는 경우 사용 지속적인 가용성 확인란의 선택을 취소 하 고 필요에 따라 선택 합니다 **액세스 기반 열거 사용** 및 **데이터액세스암호화** 확인란입니다.
7. 에 **사용 권한** 페이지에서 **사용 권한 사용자 지정 하는 중...** . 고급 보안 설정 대화 상자가 나타납니다.
8. 선택 **상속 사용 안 함**를 선택한 후 **상속 된 사용 권한을이 개체에 대 한 권한이 명시적으로 변환**합니다.
9. 설명된 표 1에 표시 된 그림 1에 나열 되지 않은 그룹 및 계정에 대 한 권한을 제거 하 고 1 단계에서에서 만든 폴더 리디렉션 Users 그룹에 특정 권한을 추가와 사용 권한을 설정 합니다.
    
    ![리디렉션된 폴더 공유에 대 한 사용 권한 설정](media/deploy-folder-redirection/setting-the-permissions-for-the-redirected-folders-share.png)
    
    **그림 1** 리디렉션된 폴더 공유에 대 한 사용 권한을 설정
10. **SMB 공유 - 고급** 프로필을 선택한 경우 **관리 속성** 페이지에서 **사용자 파일** 폴더 사용량 값을 선택합니다.
11. **SMB 공유 - 고급** 프로필을 선택한 경우 **할당량** 페이지에서 필요에 따라 공유의 사용자에게 적용할 할당량을 선택합니다.
12. 에 **확인** 페이지에서 **만들기.**

### <a name="required-permissions-for-the-file-share-hosting-redirected-folders"></a>파일에 필요한 권한을 공유 호스팅 리디렉션된 폴더

| 사용자 계정  | 액세스 권한  | 적용 대상  |
| --------- | --------- | --------- |
| 사용자 계정 | 액세스 권한 | 적용 대상 |
| 시스템     | 모든 권한        |    이 폴더, 하위 폴더 및 파일     |
| Administrators     | 모든 권한       | 이 폴더만        |
| 만든 이/소유자     |   모든 권한      |   하위 폴더 및 파일만      |
| 공유 (폴더 리디렉션 사용자)에 데이터를 저장 해야 하는 사용자의 보안 그룹     |   폴더 나열 / 데이터 읽기 *(고급 권한)* <br /><br />폴더 만들기 / 데이터 추가 *(고급 권한)* <br /><br />특성을 읽을 *(고급 권한)* <br /><br />확장 특성 읽기 *(고급 권한)* <br /><br />읽기 권한이 *(고급 권한)*      |  이 폴더만       |
| 다른 그룹 및 계정     |  없음(제거)       |         |

## <a name="step-3-create-a-gpo-for-folder-redirection"></a>3단계: 폴더 리디렉션에 대 한 GPO 만들기

폴더 리디렉션 설정에 대해 만들어진 GPO 아직 없는 경우 새로 만들려면 다음 절차를 따르십시오.

폴더 리디렉션에 대 한 GPO를 만드는 방법은 다음과 같습니다.

1. 그룹 정책 관리가 설치된 컴퓨터에서 서버 관리자를 엽니다.
2. **도구** 메뉴에서 **그룹 정책 관리**합니다.
3. 도메인 또는 폴더 리디렉션 설정 하 고 선택 하려는 OU를 마우스 오른쪽 단추로 클릭 **이 도메인에서 GPO를 만들어 여기에 연결**합니다.
4. 에 **새 GPO** 대화 상자에 GPO의 이름 입력 (예를 들어 **폴더 리디렉션 설정**)를 선택한 후 **확인**합니다.
5. 새로 만든 GPO를 마우스 오른쪽 단추로 클릭하고 **연결 사용** 확인란의 선택을 취소합니다. 그러면 구성을 마칠 때까지 GPO가 적용되지 않습니다.
6. GPO를 선택합니다. 에 **보안 필터링** 부분을 **범위** 탭을 선택 **Authenticated Users**를 선택한 후 **제거** GPO를 방지 하기 위해 모든 사용자에 게 적용 중입니다.
7. 에 **보안 필터링** 섹션에서 **추가**합니다.
8. 에 **사용자, 컴퓨터 또는 그룹 선택** 대화 상자에서 1 단계에서에서 만든 그룹 보안의 이름 (예를 들어 **폴더 리디렉션은 사용자**)를 선택한 후 **확인**.
9. 선택 합니다 **위임** 탭을 선택 **추가**, 형식 **Authenticated Users**를 선택 **확인**를 선택한 후 **확인** 다시 기본값을 적용 하려면 읽기 권한이 있습니다.
    
    이 단계에서 보안 변경으로 인해 되기 [MS16 072](https://support.microsoft.com/help/3163622/ms16-072-security-update-for-group-policy-june-14-2016)합니다.

> [!IMPORTANT]
> 보안 변경 내용으로 인해 [MS16 072](https://support.microsoft.com/help/3163622/ms16-072-security-update-for-group-policy-june-14-2016), 이제 폴더 리디렉션 GPO에 인증 된 사용자 위임 된 그룹 읽기 권한을 부여 해야 합니다-그렇지 않은 경우 사용자에 게 GPO 적용 되지 않습니다 또는 GPO가 이미 적용 된 경우 제거할 폴더를 로컬 PC 다시 리디렉션됩니다. 자세한 내용은 참조 하세요. [배포 그룹 정책 보안 업데이트 MS16-072](https://blogs.technet.microsoft.com/askds/2016/06/22/deploying-group-policy-security-update-ms16-072-kb3163622/)합니다.

## <a name="step-4-configure-folder-redirection-with-offline-files"></a>4단계: 오프 라인 파일을 사용 하 여 폴더 리디렉션 구성

다음 절차에 설명 된 대로 폴더 리디렉션 설정에 대 한 GPO를 만든 후 활성화 하 고 구성 폴더 리디렉션 그룹 정책 설정을 편집 합니다.

> [!NOTE]
> 오프 라인 파일은 Windows 클라이언트 컴퓨터에서 리디렉션된 폴더는 기본적으로 사용 하도록 설정 및 사용자가 변경 하지 않으면 Windows Server를 실행 하는 컴퓨터에서 사용 하지 않도록 설정 합니다. 를 사용 하려면 그룹 정책 제어를 오프 라인 파일 사용 되는지 여부를 사용 합니다 **허용 하거나 오프 라인 파일 기능을 사용을 허용 하지 않습니다** 정책 설정.
> 다른 오프 라인 파일 그룹 정책 설정 중 일부에 대 한 정보를 참조 하세요 [사용 고급 오프 라인 파일 기능](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn270369(v%3dws.11)>), 및 [오프 라인 파일에 대 한 그룹 정책을 구성](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc759721(v%3dws.10)>)합니다.

폴더 리디렉션 그룹 정책을 구성 하는 방법을 다음과 같습니다.

1. 만든 GPO를 마우스 오른쪽 단추로 클릭 그룹 정책 관리에서 (예를 들어 **폴더 리디렉션 설정을**)를 선택한 후 **편집**합니다.
2. 그룹 정책 관리 편집기 창에서로 이동 **사용자 구성**, 한 다음 **정책을**, 다음 **Windows 설정**를 차례로 **폴더 리디렉션**합니다.
3. 리디렉션하 하려는 폴더를 마우스 오른쪽 단추로 클릭 (예를 들어 **문서**)를 선택한 후 **속성**합니다.
4. 에 **속성** 대화 상자에서를 **설정** 상자에서 **기본-동일한 위치에 모든 사용자의 폴더 리디렉션**.

    > [!NOTE]
    > 폴더 리디렉션 Windows XP 또는 Windows Server 2003을 실행 하는 클라이언트 컴퓨터에 적용 하려면 선택 합니다 **설정을** 탭을 선택 합니다 **Windows 2000, Windows 2000 Server, Windows XP에 리디렉션 정책을 적용할 수도 및 Windows Server 2003 운영 체제** 확인란을 선택 합니다.

5. 에 **대상 폴더 위치** 섹션에서 **루트 경로 아래의 각 사용자에 대 한 폴더를 만듭니다** 한 다음를 **루트 경로** 상자에 저장 하 여 파일 공유에 대 한 경로 입력 합니다. 예를 들어 폴더 리디렉션:  **\\ \\fs1.corp.contoso.com\\사용자 $**
6. 선택 합니다 **설정** 탭 및 합니다 **정책 제거** 섹션에서 필요에 따라 **정책이 제거 될 때 로컬 사용자 프로필 위치로 다시 폴더 리디렉션** (이 설정은 가름 adminisitrators와 사용자에 대해 더 예측 가능 하 게 작동 하는 폴더 리디렉션).
7. 선택 **확인**를 선택한 후 **예** 경고 대화 상자에서.

## <a name="step-5-enable-the-folder-redirection-gpo"></a>5단계: 폴더 리디렉션 GPO 사용

폴더 리디렉션 그룹 정책 설정 구성을 마친 후에 영향을 받는 사용자에 게 적용 되도록 허용 하는 GPO를 사용 하도록 설정 하려면 다음 단계가입니다.

> [!TIP]
> 기본 컴퓨터 지원 또는 다른 정책 설정을 구현하려면 GPO를 사용하도록 설정하기 전에 지금 구현합니다. 그러면 기본 컴퓨터 지원을 사용하기 전에 사용자 데이터가 기본이 아닌 컴퓨터에 복사되는 것이 방지됩니다.

폴더 리디렉션 GPO를 사용 하도록 설정 하는 방법을 다음과 같습니다.

1. 그룹 정책 관리를 엽니다.
2. 생성 하 고 선택 GPO를 마우스 오른쪽 단추로 클릭 **링크가 활성화**합니다. 메뉴 항목 옆에 확인란이 나타납니다.

## <a name="step-6-test-folder-redirection"></a>6단계: 테스트 폴더 리디렉션

폴더 리디렉션을 테스트 하려면에 로그인 하는 컴퓨터 폴더 리디렉션에 대해 구성 된 사용자 계정을 사용 하 여 합니다. 다음 폴더 및 프로필 리디렉션 확인 합니다.

폴더 리디렉션을 테스트 하는 방법을 다음과 같습니다.

1. 에 로그인 하는 기본 컴퓨터 (기본 컴퓨터 지원을 사용 하도록 설정한) 하는 경우 설정한 폴더 리디렉션은 사용자 계정을 사용 하 여 합니다.
2. 사용자가 이전에 컴퓨터에 로그인한 경우 관리자 권한 명령 프롬프트를 열고 다음 명령을 입력하여 클라이언트 컴퓨터에 최신 그룹 정책 설정이 적용되었는지 확인합니다.
    
    ```PowerShell
    gpupdate /force
    ```
3. 파일 탐색기를 엽니다.
4. 리디렉션된 폴더 (예를 들어, 내 문서 폴더에서 문서 라이브러리)를 마우스 오른쪽 단추로 클릭 하 고 선택한 **속성**합니다.
5. 선택 된 **위치** 탭을 통해 로컬 경로 대신 지정 된 파일 공유 경로 표시 되는지 확인 합니다.

## <a name="appendix-a-checklist-for-deploying-folder-redirection"></a>부록 a: 폴더 리디렉션 배포 검사 목록

| 상태           | 작업 |
| ---              | ---    |
| ☐<br>☐<br>☐    | 1. 도메인 준비<br>-도메인에 컴퓨터를 가입 합니다.<br>사용자 계정 만들기 |
| ☐<br><br><br>   | 2. 폴더 리디렉션에 대 한 보안 그룹 만들기<br>그룹 이름:<br>-구성원: |
| ☐<br><br>       | 3. 리디렉션된 폴더에 대 한 파일 공유 만들기<br>파일 공유 이름: |
| ☐<br><br>       | 4. 폴더 리디렉션에 대 한 GPO 만들기<br>GPO 이름: |
| ☐<br><br>☐<br>☐<br>☐<br>☐<br>☐ | 5. 폴더 리디렉션 및 오프 라인 파일 정책 설정을 구성 합니다.<br>-리디렉션된 폴더:<br>-Windows 2000, Windows XP 및 Windows Server 2003 지원이 설정?<br>오프 라인 파일 사용? (Windows 클라이언트 컴퓨터에서 기본적으로 사용)<br>-항상 오프 라인 모드를 사용할 수 있습니까?<br>-백그라운드 파일 동기화가 활성화 되어 있습니까?<br>최적화 사용 하도록 설정 하는 리디렉션된 폴더의 이동? |
| ☐<br><br>☐<br><br>☐<br>☐ | 6. (선택 사항) 기본 컴퓨터 지원 사용<br>컴퓨터 기반 또는 사용자 기반?<br>-사용자의 기본 컴퓨터를 지정 합니다.<br>사용자 및 기본 컴퓨터 매핑 위치:<br>-폴더 리디렉션에 대 한 기본 컴퓨터 지원 (선택 사항) 사용<br>-로밍 사용자 프로필에 대 한 기본 컴퓨터 지원 (선택 사항) 사용 |
| ☐         | 7. 폴더 리디렉션 GPO 사용 |
| ☐         | 8. 테스트 폴더 리디렉션 |

## <a name="change-history"></a>변경 기록

다음 표에는 이 항목의 중요한 최근 변경 내용이 요약되어 있습니다.

| Date | 설명 | Reason|
| --- | --- | --- |
| 2017 년 1 월 18 일 | 추가 하는 단계 [3 단계: 폴더 리디렉션에 대 한 GPO를 만들어](#step-3-create-a-gpo-for-folder-redirection) 현재 인증 된 사용자에 게 읽기 권한을 위임 하려면 그룹 정책 보안 업데이트로 인해 필요 합니다. | 고객 의견 |

## <a name="more-information"></a>자세한 정보

* [폴더 리디렉션, 오프 라인 파일 및 로밍 사용자 프로필](folder-redirection-rup-overview.md)
* [폴더 리디렉션 및 로밍 사용자 프로필에 대 한 기본 컴퓨터 배포](deploy-primary-computers.md)
* [고급 오프 라인 파일 기능을 사용 하도록 설정](enable-always-offline.md)
* [복제 된 사용자 프로필 데이터에 대 한 Microsoft의 지원 정책](https://blogs.technet.microsoft.com/askds/2010/09/01/microsofts-support-statement-around-replicated-user-profile-data/)
* [DISM 사용 하 여 앱을 사이드 로드](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/hh852635(v=win.10)>)
* [패키징, 배포 및 Windows 런타임 기반 앱의 쿼리 문제 해결](https://msdn.microsoft.com/library/windows/desktop/hh973484.aspx)