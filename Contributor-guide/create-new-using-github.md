---
title: GitHub 및 Visual Studio Code를 사용 하 여 새 Windows Server 문서 만들기
description: Microsoft 직원으로 GitHub 및 Visual Studio Code를 사용 하 여 새 Windows Server 관련 문서를 만드는 방법입니다.
author: eross-msft
ms.author: lizross
ms.date: 05/02/2019
ms.openlocfilehash: d75bf135266a4783ab2617977b344782cea679ef
ms.sourcegitcommit: 29ad32b9dea298a7fe81dcc33d2a42d383018e82
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65624566"
---
# <a name="create-new-windows-server-articles-using-github-and-visual-studio-code"></a>GitHub 및 Visual Studio Code를 사용 하 여 새 Windows Server 문서 만들기

Windows Server 기술 콘텐츠 저장 했 고 두 개의 별도 위치 있습니다. 위치 중 하나는 공용 반면 개인 (windowsserverdocs) (windowsserverdocs pr). 사용자에 기여 하는 위치를 결정 합니다.

- **저는 Microsoft 직원입니다.** Microsoft 직원을 기반으로 수행 하려는 옵션을 수 있습니다.

    - **새 문서를 만듭니다.** 전혀 새로운 패러다임과 새로운 문서를 만들려면 만들어야 하며 GitHub 계정 및 도구를 설정 포크 및 복제 windowsserverdocs pr 리포지토리 원격 분기를 설정, 문서를 만들고 마지막 승인 및 게시에 대 한 새 끌어오기 요청을 합니다. 이러한 지침은이 문서를 계속 합니다.

    - **큰 변경 내용을 기존 문서를 확인 합니다.** 기존 문서를 크게 변경,의 지침에 따르면 합니다 [GitHub 및 Visual Studio Code를 사용 하 여 기존 Windows Server 문서를 편집](edit-existing-using-github.md) 문서.

    - **사소한 변경 내용을 기존 문서를 확인 합니다.** 기존 문서를 약간 변경 하려면의 지침에 따르면 합니다 [웹 브라우저와 GitHub를 사용 하 여 기존 Windows Server 문서를 업데이트](github-browser-updates.md) 문서.

- **Microsoft 직원이 아닙니다.** 타사 직원으로 공용 위치에 기여 해야 합니다. 그렇게 하는 방법에 대 한 내용은 참조는 [Windows Server 기술 설명서에 영향을 주는](https://github.com/MicrosoftDocs/windowsserverdocs/blob/master/CONTRIBUTING.md) 문서.

## <a name="prerequisites"></a>사전 요구 사항

리포지토리에서 작업을 시작 하기 전에 해야 GitHub 계정 설정, 2 단계 확인을 설정 및 설치 만들고 필요한 모든 도구를 구성 합니다. 이렇게 이미 한 경우로 건너뛸 수 있습니다 합니다 [분기 리포지토리 섹션](#fork-the-repository) 이 문서의.

1. [GitHub 계정 및 프로필 만들기](https://review.docs.microsoft.com/help/contribute/contribute-get-started-setup-github?branch=master#create-a-github-account-and-set-up-your-profile)

2. [Microsoft 및 MicrosoftDocs 조직에 계정을 Microsoft 계정에 연결](https://review.docs.microsoft.com/help/contribute/contribute-get-started-setup-github?branch=master#link-your-github-and-microsoft-accounts)

3. [2 단계 인증 설정](https://review.docs.microsoft.com/help/contribute/contribute-get-started-setup-github?branch=master#enable-two-factor-authentication-and-create-an-access-token)

4. [GitHub 계정에 액세스 하려면 빌드 시스템 인증](https://review.docs.microsoft.com/help/contribute/contribute-get-started-setup-github?branch=master#authorize-the-ops-build-system-to-access-your-github-account)

5. [Visual Studio Code 설치](https://review.docs.microsoft.com/help/contribute/contribute-get-started-setup-tools?branch=master#install-visual-studio-code)

6. [GitHub 및 해당 도구를 설치 합니다.](https://review.docs.microsoft.com/help/contribute/contribute-get-started-setup-tools?branch=master#install-git-client-tools)

7. [Docs Authoring Pack을 설치 합니다.](https://review.docs.microsoft.com/help/contribute/contribute-get-started-setup-tools?branch=master#install-the-docs-authoring-pack)

## <a name="set-up-your-own-version-of-the-repo"></a>리포지토리의 고유한 버전 설정

만든 GitHub 계정 및 도구를 설정 한 후에 리포지토리의 개인 버전을 만들 수 있습니다. 분기를 작성 하 고 모든 변경을 있는 경우

### <a name="fork-the-repository"></a>리포지토리 분기

프로덕션 저장소에 포크에서 끌어오기 요청을 만들 수 있도록 원본 파일의 로컬 복사본을 해야 합니다.

#### <a name="to-fork-the-repository"></a>리포지토리를 분기 하려면

1. GitHub 계정에 로그인 하 고 이동 https://github.com/microsoftdocs/windowsserverdocs-pr합니다.

2. 선택 **포크**합니다.

    ![페이지에서 강조 표시 하는 포크 단추](media/create-new-using-github/fork-button.png)

3. GitHub 계정에 포크 위치로 선택 합니다.

    ![페이지에서 강조 표시 하는 포크 단추](media/create-new-using-github/fork-location.png)

### <a name="clone-the-repository"></a>리포지토리 복제

리포지토리 가져오기 로컬 장치에 리포지토리의 로컬 복사본을 복제 해야 합니다.

#### <a name="to-clone-the-repository"></a>리포지토리 복제

1. 로 이동 https://github.com/settings/developers를 선택한 후 **개인용 액세스 토큰** 왼쪽된 창에서.

2. 선택 **새 토큰 생성**, 토큰에 의미 있고 고유한 이름을 지정, 모든 사용 가능한 범위를 선택한 후 **토큰 생성**합니다.

3. 토큰을 복사한 후 어딘가에 안전 합니다. 프로세스의 나머지 부분에 대 한 필요 하 고 페이지를 나간 후에 블레이드로 돌아가려면 수 없습니다.

4. Git Bash 명령을 열고 리포지토리에 저장 하려는 디렉터리를 변경 합니다. 를 사용 하는 것이 좋습니다 `C:\users\<your_name>\GitHub`합니다.

5. 한 번에 하나씩 자신의 특정 정보를 사용 하 여 리포지토리를 복제 하 고 원격 분기를 설정 하는 다음 명령을 입력 합니다.

    ```markdown

    git clone https://<your_github_username>:<your_personal_access_token>@github.com/<your_github_username>/windowsserverdocs-pr.git

    cd windowsserverdocs-pr

    git remote add upstream https://<your_github_username>:<your_personal_access_token>@github.com/MicrosoftDocs/windowsserverdocs-pr.git

    git fetch upstream master
    ```

6. 원격이 제대로 설정 되어 있는지 확인 하려면이 명령을 실행 합니다.

    `git remote -v`

7. 이 출력 같이 표시 됩니다.

    ```markdown
    $ git remote -v

    origin https://github.com/<your_github_username>/windowsserverdocs-pr.git (fetch)
    origin https://github.com/<your_github_username>/windowsserverdocs-pr.git (push)
    upstream https://github.com/MicrosoftDocs/windowsserverdocs-pr.git (fetch)
    upstream https://github.com/MicrosoftDocs/windowsserverdocs-pr.git (push)
    ```

    원격 출력 다음과 같이 표시 하지 않습니다, 경우 다시 시도할 수 있습니다 첫 번째 실행 하 여 `git remote remove upstream`입니다.

## <a name="create-a-branch-and-a-new-article"></a>분기를 만들고 새 문서

아티클을 만들려면 다음이 단계를 수행 합니다.

### <a name="create-a-new-branch-and-a-new-file"></a>새 분기를 만들고 새 파일

콘텐츠의 작동 하려면 먼저 로컬 리포지토리에 새 분기를 만들어야 합니다.

#### <a name="to-create-a-new-branch-in-git-bash"></a>Git Bash에서 새 분기를 만들려면

- Git Bash를 열고 명령을 입력 합니다 (한 번에 하나씩).

    ```markdown
    cd windowsserverdocs-pr

    git checkout –B <name_of_your_new_branch>

    git push origin <name_of_your_new_branch>
    ```

    >[!Note]
    >나중에 다시 찾을 수 있도록 분기 명확한와 고유한 명명 하는 것이 좋습니다.

    명령이 완료 된 후 새로운 분기에 하 고 새 파일을 만들 준비가 되었습니다. 에 Git Bash의 인스턴스당 한 번 windowsserverdocs pr 리포지토리로 변경 해야 합니다. Git Bash를 닫으면 열린 후 디렉터리를 다시 변경 해야 합니다.

#### <a name="to-create-a-new-file-in-your-branch"></a>분기에서 새 파일을 만들려면

1. Windows 탐색기를 열고 GitHub 디렉터리로 이동 폴더 구조에 새 텍스트 파일을 만듭니다. 모든 소문자 및 하이픈으로 구분 된 파일 이름 이어야 합니다. 예를 들어 _가상-는-windows-server.md_합니다.

     파일 확장명을.txt에서 변경 해야 합니다. md 합니다. 표시 되는 오류 메시지에서 선택 **예** 새 파일 확장명을 사용 하 여 파일을 저장 합니다.

2. Visual Studio Code를 열고 다음으로 이동 **파일**를 선택 **폴더 열기**, 1 단계에서에서 만든 파일의 GitHub 위치로 이동 합니다.

3. **탐색기** 창에 새 파일을 선택 합니다.

4. 페이지에서 텍스트를 추가 하 고 선택한 **파일** > **저장**합니다.

### <a name="preview-your-text"></a>텍스트 미리 보기

새 파일에 텍스트를 추가한 후 올바르게 표시 되도록 변경 내용을 미리 보아야 합니다.

#### <a name="to-preview-your-text"></a>텍스트를 미리 보려면

1. Visual Studio Code에서 중 하나를 선택 합니다 **미리 보기** 오른쪽 위 모서리에서 단추입니다.

    ![미리 보기 단추 아이콘](media/create-new-using-github/preview-button-full-page.png): 콘텐츠의 전체 페이지 미리 보기를 전환 합니다.

    ![미리 보기 단추 아이콘](media/create-new-using-github/preview-button-side-by-side.png): Side-by-side-작업 페이지 옆에 있는 미리 보기 페이지를 엽니다.

2. 문서를 확인 하기 위해 원하는 방법을 나타나는지 확인 합니다.

    올바르게 보이도록 라면 후 변경 내용을 커밋할 수 있으며 게시에 대 한 끌어오기 요청을 만들 수 있습니다.

### <a name="commit-your-changes"></a>변경 내용을 커밋합니다

텍스트가 올바르게 나타나는지 변경한 후에 리포지토리의 로컬 버전에 변경 내용을 커밋할 수 있습니다.

#### <a name="to-commit-your-changes"></a>변경 내용을 적용 하려면

- Git Bash를 열고 명령을 입력 합니다 (선택적 태그를 제거 합니다. 한 번에 하나씩).

    ```markdown
    OPTIONAL: git status

    git add .

    git commit -m “public comment about what change is”

    OPTIONAL: git pull upstream master

    git push origin <name_of_your_new_branch>

    ```

    선택적 git status 명령 파일을이 커밋의 일부로 수정한 보여 줍니다. 선택적 git 업스트림 마스터 끌어오기 주 마스터 콘텐츠를 사용 하 여 로컬 콘텐츠 동기화 MicrosoftDocs 마스터 분기에서 최신 콘텐츠 변경 내용 아래로 끌어옵니다. 이렇게 하면 모든 잠재적인 병합 충돌을 미리 보여 PR 단계에 도달 하기 전에 해결할 수 있도록 합니다.

### <a name="submit-a-pull-request-for-review-and-publication"></a>검토 및 게시에 대 한 끌어오기 요청 제출

승인에 기록기에서 가져와야 문서를 완료 한 후 (이 대 한 어느 정도의 시간을 허용 합니다.) 게시에 대 한 합니다.

#### <a name="to-submit-your-pull-request"></a>끌어오기 요청을 제출 하려면

1. 로 이동 https://github.com/MicrosoftDocs/windowsserverdocs-pr 하 고 선택 합니다 **끌어오기 요청** 탭 합니다.

2. 에 **검토자** 오른쪽 창의 영역 기어 아이콘을 선택 하 고 enter를 _windowsservercontent_ 검토에 대 한 별칭입니다.

    멤버는 _windowsservercontent_ 별칭은 변경 내용을 검토 또는 발생할 수 있습니다 병합 하기 전에 변경 되어야 하는 작업에 대 한 설명을 추가 합니다.

3. 형식 **#sign 오프** 를 주석으로 검토자가 알 수 있도록 하는 넘긴 검토 및 게시에 대 한 합니다. 합니다 **#sign 오프** 주석:

    - 끌어오기 요청에 대 한 레이블을 업데이트 **수행-not-병합** 하 **준비 간 병합**입니다.

    - 별칭 및 기록기에 콘텐츠를 검토 준비가 알고 있습니다.

    - 관리자 승인 후에 콘텐츠를 알 수 있습니다. 준비 라이브입니다.

    >[!Important]
    >Windowsservercontent 팀의 멤버인 텍스트를 검토 하 고 다음을 사용 하 여 이동 되므로 마스터에 푸시 #sign 오프 주석에 추가한 후 예약 된 (10시 30분 분 및 오후 3:30 평일) 라이브에 게시 합니다.
    >
    >마스터에 밀어 넣는 없이 내용을 큐에 남아 PR을 최종 주석으로 #sign 오프 추가 하지 않으면, 궁극적으로 to Live입니다.

## <a name="related-information"></a>관련된 정보

GitHub 및 markdown 언어에 대 한 자세한 내용은 다음을 참조 하세요.

### <a name="git-concepts"></a>Git 개념

- [GitHub 가이드-Git Handbook 소개](https://guides.github.com/introduction/git-handbook/)

- [프로젝트 GitHub 가이드 분기](https://guides.github.com/activities/forking/)

- [GitHub 가이드-GitHub flow 이해](https://guides.github.com/introduction/flow/)

- [Git 분기에 대해 알아봅니다](https://learngitbranching.js.org/ (그려보는 적합!))

### <a name="markdown"></a>Markdown

- [내부 markdown 지침](https://review.docs.microsoft.com/help/contribute/markdown-reference?branch=master)

- [외부 GitHub 자습서](https://www.markdowntutorial.com/)
