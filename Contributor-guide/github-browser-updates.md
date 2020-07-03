---
title: 웹 브라우저 및 GitHub를 사용 하 여 기존 Windows Server 문서를 편집 합니다.
description: 웹 브라우저 및 GitHub를 사용 하 여 기존 Windows Server 설명서를 Microsoft 직원으로 신속 하 게 편집 하는 방법입니다.
author: eross-msft
ms.author: lizross
ms.date: 07/02/2020
ms.openlocfilehash: 61ceb05b6cb9602faaa4d17b4dc2d978cb571ddb
ms.sourcegitcommit: d754f9e39fc28e4c8768b77bcc9d02ffe2fa6535
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85911225"
---
# <a name="update-existing-windows-server-and-azure-stack-hci-articles-using-a-web-browser-and-github"></a>웹 브라우저 및 GitHub를 사용 하 여 기존 Windows Server 및 Azure Stack HCI 문서 업데이트

Windows Server 기술 콘텐츠를 보관 하는 별도의 두 위치가 있습니다. 위치 중 하나는 공용 (windowsserverdocs)이 고 다른 하나는 개인 (windowsserverdocs-pr)입니다. 참가 하는 위치를 결정 하는 사용자:

- **저는 Microsoft 직원이 아닙니다.** Microsoft 이외의 직원은 공용 위치에 참여 해야 합니다. 이 작업을 수행 하는 방법에 대 한 자세한 내용은 [Contributing.md](https://github.com/MicrosoftDocs/windowsserverdocs/blob/master/CONTRIBUTING.md) 파일을 참조 하세요.

- **저는 Microsoft 직원입니다.** Microsoft 직원은 수행 하려는 작업에 따라 다음과 같은 옵션을 사용할 수 있습니다.

    - **새 문서를 만듭니다.** 새 문서를 만들려면 GitHub 계정 및 도구를 만들고 설정 하 고, windowsserverdocs-pr 리포지토리를 포크 및 복제 하 고, 원격 분기를 설정 하 고, 문서를 만들고, 마지막으로 승인 및 게시에 대 한 새 끌어오기 요청을 만들어야 합니다. 이러한 지침은 [GitHub 및 Visual Studio Code를 사용 하 여 새 Windows Server 문서 만들기](create-new-using-github.md) 문서를 참조 하세요.

    - **기존 문서를 크게 변경 합니다.** 기존 문서를 크게 변경 하려면 [GitHub 및 Visual Studio Code를 사용 하 여 기존 Windows Server 문서 편집 문서의](edit-existing-using-github.md) 지침을 따르세요.

    - **기존 아티클의 사소한 변경을 수행 합니다.** 기존 문서에 대 한 사소한 변경을 수행 하려면이 문서의 지침을 따르세요.

    > [!IMPORTANT]
    > docs.microsoft.com에 게시하는 모든 리포지토리는 [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/)(Microsoft 오픈 소스 규정) 또는 [.NET Foundation Code of Conduct](https://dotnetfoundation.org/code-of-conduct)(.NET Foundation 규정)를 준수합니다. 자세한 내용은 [준수 사항 FAQ](https://opensource.microsoft.com/codeofconduct/faq/)를 참조하세요. 또는 [opencode@microsoft.com](mailto:opencode@microsoft.com)이나 [conduct@dotnetfoundation.org](mailto:conduct@dotnetfoundation.org)에 궁금한 사항을 문의하거나 의견을 제시하세요.
    >
    > 공용 리포지토리의 설명서 및 코드 예제에 대한 사소한 수정 또는 확인 내용은 [docs.microsoft.com 사용 약관](https://docs.microsoft.com/legal/termsofuse)에서 다룹니다. 변경 내용이 새롭거나 중요한 내용일 경우 Microsoft 직원이 아닌 경우에 한해 끌어오기 요청에서 온라인 CLA(참가 라이선스 계약)를 제출하도록 요청하는 주석이 생성됩니다. 온라인 양식을 먼저 작성한 후 Microsoft에서 끌어오기 요청을 검토하거나 수락할 수 있습니다.

## <a name="quick-edits-to-existing-articles-using-github-and-a-web-browser"></a>GitHub 및 웹 브라우저를 사용 하 여 기존 문서에 대 한 빠른 편집

빠른 편집은 문서의 사소한 오류 및 누락을 보고하고 수정하는 프로세스를 간소화합니다. 오류를 최소화하려는 모든 노력에도 불구하고 게시되는 문서에서 사소한 문법 및 맞춤법 _오류가 발견될 수 있습니다_.

1. [GitHub 계정 설정](https://review.docs.microsoft.com/en-us/help/contribute/contribute-get-started-setup-github?branch=master)의 지침을 따릅니다.

1. [Windows Server](https://github.com/MicrosoftDocs/windowsserverdocs-pr/tree/master/WindowsServerDocs) 또는 [Azure Stack HCI](https://github.com/MicrosoftDocs/azure-stack-docs-pr/tree/master/azure-stack/hci) 개인 리포지토리로 이동 합니다. 개인 리포지토리는 더 자주 모니터링 되므로 승인 시간이 단축 되 고 품질 검사가 증가 하는 이점을 누릴 수 있으며, 라이브 사이트에 표시 되는 대로 준비 중인 콘텐츠를 볼 수 있는 기능이 제공 됩니다.

2. 편집 하려는 문서로 이동한 다음 **이 파일 편집** 단추를 선택 합니다.

   ![이 파일 편집 단추](media/github-browser-updates/edit-this-file.png)

3. 항목을 편집 하 고 아래쪽으로 스크롤한 다음 변경 내용을 간략하게 설명 하 고 **변경 내용 커밋**을 선택 합니다.

    ![제목 정보를 사용 하 여 변경 내용 커밋](media/github-browser-updates/commit-changes.png)

## <a name="submit-the-pull-request"></a>끌어오기 요청 제출

끌어오기 요청을 만든 후에는 승인 및 게시를 위해 제출 해야 합니다.

### <a name="to-submit-your-pull-request"></a>끌어오기 요청을 제출 하려면

1. **끌어오기 요청 열기** 페이지에서 PR에 더 적합 하도록 커밋 메시지를 업데이트 합니다. 예: 첫 번째 단락의 오타가 수정 합니다.

2. 포함 될 것으로 간주 되는 커밋 및 파일만 포함 되는지 확인 합니다. 또한 PR이 업스트림 리포지토리의 master (일반적으로) 또는 릴리스 분기 (경우에 따라)의 올바른 분기로 이동 하는지 확인 합니다.

3. 오른쪽 창의 **검토자** 영역에서 기어 아이콘을 선택 하 고 _windowsservercontent_를 입력 합니다. 별칭의 멤버는 변경 내용을 검토 하 고 끌어오기 요청을 병합 하거나 병합 하기 전에 변경할 항목에 대 한 의견을 추가 하는 지점에 있습니다.

4. **끌어오기 요청 만들기**를 선택합니다. 새 PR은 포크의 작업 분기에 연결 됩니다. PR이 병합 될 때까지 포크에서 동일한 작업 분기에 푸시하는 모든 새 커밋이 PR에 자동으로 포함 됩니다. 새 레이블은 끌어오기 요청에 추가 되며 **병합 되지**않습니다. 즉, 콘텐츠는 아직 진행 중 이며 라이브 사이트로 검토 하거나 푸시 되어서는 안 됩니다.

5. 별칭의 누군가가 콘텐츠를 검토할 준비가 되 면 텍스트 **#sign** 를 주석에 추가 해야 합니다. 설명:

    - 끌어오기 요청에 대 한 레이블을 **업데이트 하지 않음에서 병합** **으로 업데이트 합니다.**

    - 별칭 및 작성자가 콘텐츠를 검토할 준비가 되었음을 알 수 있습니다.

    - 관리자가 승인 후 콘텐츠가 준비 되었음을 알 수 있습니다.
