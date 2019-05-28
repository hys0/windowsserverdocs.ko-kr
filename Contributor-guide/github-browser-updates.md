---
title: 웹 브라우저 및 GitHub를 사용 하 여 기존 Windows Server 문서를 편집 합니다.
description: 웹 브라우저와 GitHub를 사용 하 여 Microsoft 직원으로 기존 Windows Server 설명서를 빠른 편집을 확인 하는 방법.
author: eross-msft
ms.author: lizross
ms.date: 05/02/2019
ms.openlocfilehash: d4574de7774a43092815a3d154020559c50fdcf9
ms.sourcegitcommit: 29ad32b9dea298a7fe81dcc33d2a42d383018e82
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65624592"
---
# <a name="update-existing-windows-server-articles-using-a-web-browser-and-github"></a>웹 브라우저 및 GitHub를 사용 하 여 기존 Windows Server 문서를 업데이트 합니다.

Windows Server 기술 콘텐츠 저장 했 고 두 개의 별도 위치 있습니다. 위치 중 하나는 공용 반면 개인 (windowsserverdocs) (windowsserverdocs pr). 사용자에 기여 하는 위치를 결정 합니다.

- **Microsoft 직원이 아닙니다.** 타사 직원으로 공용 위치에 기여 해야 합니다. 그렇게 하는 방법에 대 한 내용은 참조는 [있는 Contributing.md](https://github.com/MicrosoftDocs/windowsserverdocs/blob/master/CONTRIBUTING.md) 파일입니다.

- **저는 Microsoft 직원입니다.** Microsoft 직원을 기반으로 수행 하려는 옵션을 수 있습니다.

    - **새 문서를 만듭니다.** 전혀 새로운 패러다임과 새로운 문서를 만들려면 만들어야 하며 GitHub 계정 및 도구를 설정 포크 및 복제 windowsserverdocs pr 리포지토리 원격 분기를 설정, 문서를 만들고 마지막 승인 및 게시에 대 한 새 끌어오기 요청을 합니다. 이러한 지침은 합니다 [GitHub 및 Visual Studio Code를 사용 하 여 새 Windows Server 문서를 만들](create-new-using-github.md) 문서.

    - **큰 변경 내용을 기존 문서를 확인 합니다.** 기존 문서를 크게 변경,의 지침에 따르면 합니다 [GitHub 및 Visual Studio Code를 사용 하 여 기존 Windows Server 문서를 편집](edit-existing-using-github.md) 문서.

    - **사소한 변경 내용을 기존 문서를 확인 합니다.** 기존 문서를 약간 변경 하려면이 문서의 지침을 따라 수 있습니다.

    > [!IMPORTANT]
    > Docs.microsoft.com에 게시 하는 모든 리포지토리는 채택한 합니다 [Microsoft 오픈 소스 준수 사항](https://opensource.microsoft.com/codeofconduct/) 또는 [.NET Foundation 규정](https://dotnetfoundation.org/code-of-conduct)합니다. 자세한 내용은 참조는 [준수 사항 FAQ](https://opensource.microsoft.com/codeofconduct/faq/)합니다. 보거나 [ opencode@microsoft.com ](mailto:opencode@microsoft.com), 또는 [ conduct@dotnetfoundation.org ](mailto:conduct@dotnetfoundation.org) 질문이 나 의견을 사용 하 여 합니다.
    >
    > 사소한 수정 또는 확인 내용은 공용 리포지토리의 설명서 및 코드 예제에 적용 되는 [docs.microsoft.com 사용 약관](https://docs.microsoft.com/legal/termsofuse)합니다. Microsoft 직원이 아닌 경우 온라인 라이선스 계약 (CLA)을 제출 하 라는 메시지가 끌어오기 요청에 주석을 생성 하는 변경 내용이 새롭거나 중요 합니다. 검토 또는 끌어오기 요청을 수락할 수 있습니다 온라인 양식을 완료 해야 합니다.

## <a name="quick-edits-to-existing-articles-using-github-and-a-web-browser"></a>GitHub 및 웹 브라우저를 사용 하 여 기존 아티클에 대 한 빠른 편집

빠른 편집 보고 하 고 문서의 사소한 오류 및 누락을 수정 하는 프로세스를 간소화 합니다. 모든 작업, 사소한 문법 및 맞춤법 오류 불구 하 고 _수행_ 해당 방식으로 게시 되는 문서를 만듭니다.

1. [https://partnercenter.microsoft.com/partner/support](https://github.com/MicrosoftDocs/windowsserverdocs-pr/tree/master/WindowsServerDocs)로 이동하세요.

2. 편집 하려는 문서를 탐색 한 다음 선택 합니다 **이 파일을 편집** 단추입니다.

   ![이 파일 단추를 편집 합니다.](media/github-browser-updates/edit-this-file.png)

3. 항목 편집 후 맨 아래로 스크롤하여, 변경 내용을 간략하게 설명 및 선택한 **변경 내용 커밋**합니다.

    ![제목 정보를 사용 하 여 변경 내용 커밋](media/github-browser-updates/commit-changes.png)

## <a name="submit-the-pull-request"></a>끌어오기 요청 제출

끌어오기 요청을 만든 후 승인 및 게시를 위해 제출 해야 합니다.

### <a name="to-submit-your-pull-request"></a>끌어오기 요청을 제출 하려면

1. 에 **끌어오기 요청 열기** 페이지에서 커밋 메시지를 확인 하세요. 더 적합 하도록 업데이트 예를 들어 다음과 같은 가치를 제공해야 합니다. 첫 번째 단락에서 오타를 수정 합니다.

2. 커밋 및 예상 되는 포함 하는 파일 포함 되어 있는지 확인 합니다. PR (일반적으로) 올바른 업스트림 리포지토리의 마스터 분기를 이동 하는 확인 또는 릴리스 분기 (경우에 따라).

3. 에 **검토자** 오른쪽 창의 영역 기어 아이콘을 선택한 다음 입력 _windowsservercontent_합니다. 변경 내용을 검토 하는 지점에서 별칭의 멤버인 되며에 끌어오기를 병합 하거나 요청 하거나 병합 하기 전에 변경 사항에 대 한 설명을 추가 합니다.

4. 선택 **끌어오기 요청 만들기**합니다. 새 PR 분기에서 작업 분기에 연결 됩니다. 포크를 동일한 작업 분기를 푸시 하면 새 커밋이 PR이 병합 될 때까지 PR에 자동으로 포함 됩니다. 새 레이블을 끌어오기 요청에 추가 됩니다 **수행-not-병합**입니다. 단순히 즉 콘텐츠 아직 진행 중입니다 및 해서는 안 됩니다 수 검토 라이브 사이트에 푸시됩니다.

5. 콘텐츠를 검토 하려면 별칭에서 다른 사용자에 대 한 준비 된 경우 텍스트를 추가 해야 합니다 **#sign 오프** 주석을 합니다. 이 설명:

    - 끌어오기 요청에 대 한 레이블을 업데이트 **수행-not-병합** 하 **준비 간 병합**입니다.

    - 별칭 및 기록기에 콘텐츠를 검토 준비가 알고 있습니다.

    - 관리자 승인 후에 콘텐츠를 알 수 있습니다. 준비 라이브입니다.