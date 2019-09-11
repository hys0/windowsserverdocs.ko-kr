---
title: GitHub 및 Visual Studio Code를 사용 하 여 기존 Windows Server 문서 편집
description: GitHub 및 Visual Studio Code를 사용 하 여 기존 Windows Server 관련 문서를 Microsoft 직원으로 편집 하는 방법입니다.
author: eross-msft
ms.author: lizross
ms.date: 05/06/2019
ms.openlocfilehash: d681d2fc2b69898e841932a95738b89515ffb51a
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70865075"
---
# <a name="edit-an-existing-windows-server-article-using-github-and-visual-studio-code"></a>GitHub 및 Visual Studio Code를 사용 하 여 기존 Windows Server 문서 편집

Windows Server 기술 콘텐츠를 보관 하는 별도의 두 위치가 있습니다. 위치 중 하나는 공용 (windowsserverdocs)이 고 다른 하나는 개인 (windowsserverdocs-pr)입니다. 참가 하는 위치를 결정 하는 사용자:

- **저는 Microsoft 직원입니다.** Microsoft 직원은 수행 하려는 작업에 따라 다음과 같은 옵션을 사용할 수 있습니다.

    - **새 문서를 만듭니다.** 새 문서를 만들려면 GitHub 계정 및 도구를 만들고 설정 하 고, windowsserverdocs-pr 리포지토리를 포크 및 복제 하 고, 원격 분기를 설정 하 고, 문서를 만들고, 마지막으로 승인 및 게시에 대 한 새 끌어오기 요청을 만들어야 합니다. 이러한 지침에 대해서는 [GitHub 및 Visual Studio Code를 사용 하 여 새 Windows Server 문서 만들기](create-new-using-github.md) 문서에 설명 된 지침을 따를 수 있습니다.

    - **기존 문서를 크게 변경 합니다.** 기존 문서를 크게 변경 하려면이 문서의 지침을 따를 수 있습니다.

    - **기존 아티클의 사소한 변경을 수행 합니다.** 기존 문서에 대 한 사소한 변경을 수행 하려면 [웹 브라우저 및 GitHub를 사용 하 여 기존 Windows Server 문서 업데이트](github-browser-updates.md) 문서에 있는 지침을 따르세요.

- **저는 Microsoft 직원이 아닙니다.** Microsoft 이외의 직원은 공용 위치에 참여 해야 합니다. 이 작업을 수행 하는 방법에 대 한 자세한 내용은 [Windows Server 기술 문서에 기여](https://github.com/MicrosoftDocs/windowsserverdocs/blob/master/CONTRIBUTING.md) 문서를 참조 하세요.

## <a name="switch-your-repo-and-create-a-new-branch"></a>리포지토리를 전환 하 고 새 분기를 만듭니다.

기존 문서를 편집 하려면 다음 단계를 수행 합니다.

### <a name="create-a-new-branch-and-locate-the-file-you-want-to-update"></a>새 분기를 만들고 업데이트 하려는 파일을 찾습니다.

콘텐츠에 대 한 작업을 시작 하려면 먼저 windowsserverdocs-pr 리포지토리로 변경한 다음 업데이트 하려는 문서를 찾아야 합니다.

#### <a name="to-create-a-new-branch-in-git-bash"></a>Git Bash에서 새 분기를 만들려면

- Git Bash를 열고 명령을 입력 합니다 (한 번에 하나씩).

    ```markdown
    cd windowsserverdocs-pr

    git checkout –B <name_of_your_new_branch>

    git push origin <name_of_your_new_branch>
    ```

    >[!Note]
    >분기의 이름을 명확 하 고 고유 하 게 지정 하 여 나중에 다시 찾을 수 있도록 하는 것이 좋습니다.

    명령이 완료 되 면 새 분기에 있게 되 고 파일을 편집할 준비가 됩니다.

#### <a name="to-locate-your-article-and-make-your-edits"></a>문서를 찾고 편집 하려면

1. Visual Studio Code를 열고 **파일**로 이동한 다음 **폴더 열기**를 선택 하 고 편집할 아티클이 있는 폴더의 GitHub 위치로 이동 합니다.

2. **탐색기** 창에서 파일을 선택 합니다.

3. 페이지의 정보를 업데이트 한 다음 **파일** > **저장**을 선택 합니다.

### <a name="preview-your-text"></a>텍스트 미리 보기

텍스트를 업데이트 한 후에는 변경 내용을 미리 보고 올바르게 표시 되는지 확인 해야 합니다.

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

업데이트를 완료 한 후에는 작성자 (이 경우 일정 시간 허용)에서 게시에 대 한 승인을 받아야 합니다.

#### <a name="to-submit-your-pull-request"></a>끌어오기 요청을 제출 하려면

1. 로 https://github.com/MicrosoftDocs/windowsserverdocs-pr 이동 하 여 **끌어오기 요청** 탭을 선택 합니다.

2. 오른쪽 창의 **검토자** 영역에서 기어 아이콘을 선택 하 고 검토할 _windowsservercontent_ 별칭을 입력 합니다.

    _Windowsservercontent_ 별칭의 구성원은 변경 내용을 검토 하거나 병합이 발생 하기 전에 변경 해야 하는 항목에 대 한 설명을 추가 합니다.

3. 검토자가 검토 및 게시를 모두 처리 하는 것을 알 수 있도록 주석에 **#sign 기능** 을 입력 합니다. **#Sign** 설명:

    - 끌어오기 요청에 대 한 레이블을 **업데이트 하지 않음에서 병합** **으로 업데이트 합니다.**

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