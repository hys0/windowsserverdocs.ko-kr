---
title: GitHub 및 Visual Studio Code를 사용 하 여 새 Windows Server 문서 만들기
description: GitHub 및 Visual Studio Code를 사용 하 여 Microsoft 직원으로 새 Windows Server 관련 문서를 만드는 방법입니다.
author: eross-msft
ms.author: lizross
ms.date: 05/02/2019
ms.openlocfilehash: f5e7e3d0cd17c64175fddaaac73c12daa2c2a32c
ms.sourcegitcommit: ffd9c42374c7448deb5f53f7a865cb427b5e4e9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69887955"
---
# <a name="create-new-windows-server-articles-using-github-and-visual-studio-code"></a>GitHub 및 Visual Studio Code를 사용 하 여 새 Windows Server 문서 만들기

Windows Server 기술 콘텐츠를 보관 하는 별도의 두 위치가 있습니다. 위치 중 하나는 공용 (windowsserverdocs)이 고 다른 하나는 개인 (windowsserverdocs-pr)입니다. 참가 하는 위치를 결정 하는 사용자:

- **저는 Microsoft 직원입니다.** Microsoft 직원은 수행 하려는 작업에 따라 다음과 같은 옵션을 사용할 수 있습니다.

    - **새 문서를 만듭니다.** 새 문서를 만들려면 GitHub 계정 및 도구를 만들고 설정 하 고, windowsserverdocs-pr 리포지토리를 포크 및 복제 하 고, 원격 분기를 설정 하 고, 문서를 만들고, 마지막으로 승인 및 게시에 대 한 새 끌어오기 요청을 만들어야 합니다. 이러한 지침에 대해서는이 문서를 계속 읽어 보십시오.

    - **기존 문서를 크게 변경 합니다.** 기존 문서를 크게 변경 하려면 [GitHub 및 Visual Studio Code를 사용 하 여 기존 Windows Server 문서 편집 문서의](edit-existing-using-github.md) 지침을 따르세요.

    - **기존 아티클의 사소한 변경을 수행 합니다.** 기존 문서에 대 한 사소한 변경을 수행 하려면 [웹 브라우저 및 GitHub를 사용 하 여 기존 Windows Server 문서 업데이트](github-browser-updates.md) 문서에 있는 지침을 따르세요.

- **저는 Microsoft 직원이 아닙니다.** Microsoft 이외의 직원은 공용 위치에 참여 해야 합니다. 이 작업을 수행 하는 방법에 대 한 자세한 내용은 [Windows Server 기술 문서에 기여](https://github.com/MicrosoftDocs/windowsserverdocs/blob/master/CONTRIBUTING.md) 문서를 참조 하세요.

## <a name="prerequisites"></a>사전 요구 사항

리포지토리에서 작업을 시작 하려면 먼저 GitHub 계정을 만들고 설정 하 고, 2 단계 인증을 설정 하 고, 필요한 모든 도구를 설치 하 고 구성 해야 합니다. 이미이 작업을 수행한 경우이 문서의 [저장소로 분기 섹션](#fork-the-repository) 으로 건너뛸 수 있습니다.

1. [GitHub 계정 및 프로필 만들기](https://review.docs.microsoft.com/help/contribute/contribute-get-started-setup-github?branch=master#create-a-github-account-and-set-up-your-profile)

2. [사용자 Microsoft 계정 및 Microsoft 및 MicrosoftDocs 조직에 계정 연결](https://review.docs.microsoft.com/help/contribute/contribute-get-started-setup-github?branch=master#link-your-github-and-microsoft-accounts)

3. [2 단계 인증 설정](https://review.docs.microsoft.com/help/contribute/contribute-get-started-setup-github?branch=master#enable-two-factor-authentication-and-create-an-access-token)

4. [빌드 시스템에 GitHub 계정에 대 한 액세스 권한 부여](https://review.docs.microsoft.com/help/contribute/contribute-get-started-setup-github?branch=master#authorize-the-ops-build-system-to-access-your-github-account)

5. [Visual Studio Code 설치](https://review.docs.microsoft.com/help/contribute/contribute-get-started-setup-tools?branch=master#install-visual-studio-code)

6. [GitHub 및 해당 도구 설치](https://review.docs.microsoft.com/help/contribute/contribute-get-started-setup-tools?branch=master#install-git-client-tools)

7. [Docs Authoring Pack 설치](https://review.docs.microsoft.com/help/contribute/contribute-get-started-setup-tools?branch=master#install-the-docs-authoring-pack)

## <a name="set-up-your-own-version-of-the-repo"></a>리포지토리의 고유한 버전 설정

GitHub 계정과 도구를 만들고 설정한 후에는 리포지토리의 개인 버전을 만들 수 있습니다. 여기서는 분기를 만들고 모든 변경 작업을 수행 합니다.

### <a name="fork-the-repository"></a>리포지토리 분기

분기에서 프로덕션 리포지토리로 끌어오기 요청을 만들 수 있도록 원본 파일의 로컬 복사본이 필요 합니다.

#### <a name="to-fork-the-repository"></a>리포지토리를 분기 하려면

1. GitHub 계정에 로그인 하 고로 이동 https://github.com/microsoftdocs/windowsserverdocs-pr 합니다.

2. **포크**를 선택 합니다.

    ![페이지에서 분기 단추가 강조 표시 됨](media/create-new-using-github/fork-button.png)

3. 사용자의 GitHub 계정을 포크 위치로 선택 합니다.

    ![페이지에서 분기 단추가 강조 표시 됨](media/create-new-using-github/fork-location.png)

### <a name="clone-the-repository"></a>리포지토리 복제

리포지토리의 로컬 복사본을 로컬 장치에 가져오는 리포지토리를 복제 해야 합니다.

#### <a name="to-clone-the-repository"></a>리포지토리를 복제 하려면

1. 로 https://github.com/settings/developers 이동한 다음 왼쪽 창에서 **개인용 액세스 토큰** 을 선택 합니다.

2. **새 토큰 생성**을 선택 하 고, 토큰에 의미 있고 고유한 이름을 지정 하 고, 사용 가능한 모든 범위를 선택 하 고 나 서, **토큰 생성**을 선택 합니다.

3. 토큰을 복사 하 고 안전한 위치에 배치 합니다. 프로세스의 나머지 부분에는이 작업이 필요 하 고 페이지를 벗어나면 다시 가져올 수 없습니다.

4. Git Bash 명령을 열고 리포지토리를 저장 하려는 위치로 디렉터리를 변경 합니다. ,를 사용 하 `C:\users\<your_name>\GitHub`는 것이 좋습니다.

5. 특정 정보를 한 번에 하나씩 사용 하 여 다음 명령을 입력 하 여 리포지토리를 복제 하 고 원격 분기를 설정 합니다.

    ```markdown

    git clone https://<your_github_username>:<your_personal_access_token>@github.com/<your_github_username>/windowsserverdocs-pr.git

    cd windowsserverdocs-pr

    git remote add upstream https://<your_github_username>:<your_personal_access_token>@github.com/MicrosoftDocs/windowsserverdocs-pr.git

    git fetch upstream master
    ```

6. 다음 명령을 실행 하 여 원격이 제대로 설정 되었는지 확인 합니다.

    `git remote -v`

7. 다음과 같은 출력이 표시 됩니다.

    ```markdown
    $ git remote -v

    origin https://github.com/<your_github_username>/windowsserverdocs-pr.git (fetch)
    origin https://github.com/<your_github_username>/windowsserverdocs-pr.git (push)
    upstream https://github.com/MicrosoftDocs/windowsserverdocs-pr.git (fetch)
    upstream https://github.com/MicrosoftDocs/windowsserverdocs-pr.git (push)
    ```

    원격 출력이 다음과 같을 경우 먼저를 실행 `git remote remove upstream`하 여 다시 시도할 수 있습니다.

## <a name="create-a-branch-and-a-new-article"></a>분기 및 새 문서 만들기

문서를 만들려면 다음 단계를 따르세요.

### <a name="create-a-new-branch-and-a-new-file"></a>새 분기 및 새 파일 만들기

콘텐츠 작업을 시작 하려면 로컬 리포지토리에서 새 분기를 만들어야 합니다.

#### <a name="to-create-a-new-branch-in-git-bash"></a>Git Bash에서 새 분기를 만들려면

- Git Bash를 열고 명령을 입력 합니다 (한 번에 하나씩).

    ```markdown
    cd windowsserverdocs-pr

    git checkout –B <name_of_your_new_branch>

    git push origin <name_of_your_new_branch>
    ```

    >[!Note]
    >분기의 이름을 명확 하 고 고유 하 게 지정 하 여 나중에 다시 찾을 수 있도록 하는 것이 좋습니다.

    명령이 완료 되 면 새 분기에 새 파일을 만들 준비가 된 것입니다. Git Bash 인스턴스당 한 번만 windowsserverdocs-pr 리포지토리를 변경 해야 합니다. Git Bash를 닫은 경우에는 디렉터리를 연 후 다시 변경 해야 합니다.

#### <a name="to-create-a-new-file-in-your-branch"></a>분기에 새 파일을 만들려면

1. Windows 탐색기를 열고 GitHub 디렉터리로 이동 하 여 폴더 구조에 새 텍스트 파일을 만듭니다. 파일 이름은 모두 소문자 여야 하며 하이픈으로 구분 되어야 합니다. 예를 들면 _what-is-windows-server.md_입니다.

     파일 확장명을 .txt로 변경 해야 합니다. 표시 되는 오류 메시지에서 **예** 를 선택 하 여 새 파일 확장명으로 파일을 저장 합니다.

2. Visual Studio Code를 열고 **파일**로 이동한 다음 **폴더 열기**를 선택 하 고 1 단계에서 만든 파일의 GitHub 위치로 이동 합니다.

3. **탐색기** 창에서 새 파일을 선택 합니다.

4. 페이지에 텍스트를 추가 합니다. 새 문서를 만드는 경우 [Windows Server 관련 문서에 필요한 메타 데이터 태그를 추가](metadata-requirements-for-articles.md)해야 합니다.

5. **파일** > **저장**을 선택 합니다.

### <a name="preview-your-text"></a>텍스트 미리 보기

새 파일에 텍스트를 추가한 후에는 변경 내용을 미리 확인 하 여 올바르게 표시 되는지 확인 해야 합니다.

#### <a name="to-preview-your-text"></a>텍스트를 미리 보려면

1. Visual Studio Code의 오른쪽 위 모서리에서 **미리 보기** 단추 중 하나를 선택 합니다.

    ![미리 보기 단추 아이콘](media/create-new-using-github/preview-button-full-page.png): 콘텐츠의 전체 페이지 미리 보기로 전환 합니다.

    ![미리 보기 단추 아이콘](media/create-new-using-github/preview-button-side-by-side.png): 작업 페이지 옆에 있는 미리 보기 페이지를 나란히 엽니다.

2. 문서에서 원하는 모양을 확인 합니다.

    올바른 것으로 확인 되 면 변경 내용을 커밋하고 게시에 대 한 끌어오기 요청을 만들 수 있습니다.

### <a name="commit-your-changes"></a>변경 내용 커밋

텍스트가 올바르게 표시 되는지 확인 한 후에는 리포지토리의 로컬 버전에 대 한 변경 내용을 커밋할 수 있습니다.

#### <a name="to-commit-your-changes"></a>변경 내용을 커밋하려면

- Git Bash를 열고 명령을 입력 합니다 (선택적 태그 제거).

    ```markdown
    OPTIONAL: git status

    git add .

    git commit -m “public comment about what change is”

    OPTIONAL: git pull upstream master

    git push origin <name_of_your_new_branch>

    ```

    선택적 git 상태 명령은이 커밋의 일부로 수정 된 파일을 보여 줍니다. 선택적 git 끌어오기 업스트림 마스터는 MicrosoftDocs master 분기에서 최신 콘텐츠 변경 내용을 가져와서 로컬 콘텐츠를 기본 마스터 콘텐츠와 동기화 합니다. 그러면 PR 단계로 이동 하기 전에 수정할 수 있도록 잠재적 병합 충돌을 미리 보여 줄 수 있습니다.

### <a name="submit-a-pull-request-for-review-and-publication"></a>검토 및 게시에 대 한 끌어오기 요청 제출

문서를 완료 한 후에는 작성자 (이 경우 일정 시간 허용)에서 게시에 대 한 승인을 받아야 합니다.

#### <a name="to-submit-your-pull-request"></a>끌어오기 요청을 제출 하려면

1. 로 https://github.com/MicrosoftDocs/windowsserverdocs-pr 이동 하 여 **끌어오기 요청** 탭을 선택 합니다.

2. 오른쪽 창의 **검토자** 영역에서 기어 아이콘을 선택 하 고 검토할 _windowsservercontent_ 별칭을 입력 합니다.

    _Windowsservercontent_ 별칭의 구성원은 변경 내용을 검토 하거나 병합이 발생 하기 전에 변경 해야 하는 항목에 대 한 설명을 추가 합니다.

3. 검토자가 검토 및 게시를 모두 처리 하는 것을 알 수 있도록 주석에 **#sign 기능** 을 입력 합니다. **#Sign** 설명:

    - 끌어오기 요청에 대 한 레이블을 업데이트 하지 않음에서 병합으로 업데이트 합니다.

    - 별칭 및 작성자가 콘텐츠를 검토할 준비가 되었음을 알 수 있습니다.

    - 관리자가 승인 후 콘텐츠가 준비 되었음을 알 수 있습니다.

    >[!Important]
    >#Sign 해제 주석을 추가한 후에는 windowsservercontent 팀의 구성원이 텍스트를 검토 하 고 마스터에 푸시하여 다음에 예약 된 다음 게시 (오전 10 시 30 분 및 3:30am 평일)로 전환 됩니다.
    >
    >PR에 대 한 최종 주석으로 #sign를 추가 하지 않으면 콘텐츠는 마스터에 푸시되 고 궁극적으로 라이브 상태로 유지 되지 않고 큐에 유지 됩니다.

## <a name="related-information"></a>관련 정보

GitHub 및 markdown 언어에 대 한 자세한 내용은 다음을 참조 하세요.

### <a name="git-concepts"></a>Git 개념

- [GitHub 가이드-Git 안내서 소개](https://guides.github.com/introduction/git-handbook/)

- [GitHub 가이드-분기 프로젝트](https://guides.github.com/activities/forking/)

- [GitHub 가이드-GitHub 흐름 이해](https://guides.github.com/introduction/flow/)

- [Git 분기 배우기] (https://learngitbranching.js.org/ (시각적 학습자에 게 적합 합니다.))

### <a name="markdown"></a>Markdown

- [내부 markdown 지침](https://review.docs.microsoft.com/help/contribute/markdown-reference?branch=master)

- [외부, GitHub 자습서](https://www.markdowntutorial.com/)
