# <a name="contributing-to-windows-server-technical-documentation"></a>Windows Server 기술 설명서에 기여

Windows Server 기술 설명서에 관심을 가져을 주셔서 감사 합니다! 우리의 문서에 대한 피드백, 편집, 및 추가해주셔서 감사합니다. Windows Server 기술 콘텐츠 저장 했 고 두 개의 별도 위치 있습니다. 위치 중 하나는 공용 반면 개인 (windowsserverdocs) (windowsserverdocs pr). 사용자에 기여 하는 위치를 결정 합니다.

- **Microsoft 직원이 아닙니다.** 타사 직원으로 공용 위치에 기여 해야 합니다. 그렇게 하는 방법에 대 한 내용은이 문서를 계속 합니다.

- **저는 Microsoft 직원입니다.** Microsoft 직원을 기반으로 수행 하려는 옵션을 수 있습니다.

    - **새 문서를 만듭니다.** 전혀 새로운 패러다임과 새로운 문서를 만들려면 만들어야 하며 GitHub 계정 및 도구를 설정 포크 및 복제 windowsserverdocs pr 리포지토리 원격 분기를 설정, 문서를 만들고 마지막 승인 및 게시에 대 한 새 끌어오기 요청을 합니다. 이러한 지침은 합니다 [GitHub 및 Visual Studio Code를 사용 하 여 새 Windows Server 문서를 만들](https://github.com/MicrosoftDocs/windowsserverdocs/blob/master/Contributor-guide/create-new-using-github.md) 문서.

    - **큰 변경 내용을 기존 문서를 확인 합니다.** 기존 문서를 크게 변경,의 지침에 따르면 합니다 [GitHub 및 Visual Studio Code를 사용 하 여 기존 Windows Server 문서를 편집](https://github.com/MicrosoftDocs/windowsserverdocs/blob/master/Contributor-guide/edit-existing-using-github.md) 문서.

    - **사소한 변경 내용을 기존 문서를 확인 합니다.** 기존 문서를 약간 변경 하려면의 지침에 따르면 합니다 [웹 브라우저와 GitHub를 사용 하 여 기존 Windows Server 문서를 업데이트](https://github.com/MicrosoftDocs/windowsserverdocs/blob/master/Contributor-guide/github-browser-updates.md) 문서.

## <a name="sign-a-cla"></a>CLA 서명

모든 참가자 ***되지*** Microsoft 직원이 해야 [로그인 된 Microsoft 라이선스 계약 (CLA)](https://cla.microsoft.com/) 모든 Microsoft 리포지토리를 편집 하기 전에 합니다. 축 하 합니다. 이전에 이미 Microsoft 리포지토리 내에서 편집 했습니다!
이 단계를 이미 완료 했다고 합니다.

## <a name="editing-topics"></a>항목 편집

파일을 편집 하면 기존에 공용 가능한 간단 하 게 확인 했습니다.

### <a name="to-edit-a-topic"></a>항목을 편집 하려면

1. 페이지를 이동할 https://docs.microsoft.com/windows-server 업데이트 및 선택 하려는 **편집**합니다.

    ![GitHub 웹에서 편집 링크를 표시 합니다.](media/contribute-link.png)

2. 에 로그인 (또는 등록)는 GitHub 계정.

    항목을 편집할 수 있도록 페이지를 표시 하려면 GitHub 계정이 있어야 합니다.

3. 선택 합니다 **연필** 아이콘 (빨간색 상자) 내용을 편집할 수 있습니다.

    ![GitHub 웹, 빨간색 상자에 있는 연필 아이콘을 보여 주는](media/pencil-icon.png)

4. Markdown 언어를 사용 하는 항목에 변경 내용을 확인 합니다. 편집 하는 방법에 대 한 정보에 대 한 Markdown을 사용 하 여 콘텐츠를 참조 하십시오.

    - **GitHub의 Microsoft 조직에 연결 하는 경우:** [Windows Server 참여자 가이드](https://github.com/MicrosoftDocs/windowsserverdocs-pr/tree/master/Contributor-guide)

    - **Microsoft 외부 경우:** [마스터 Markdown](https://guides.github.com/features/mastering-markdown/)

5. 제안 된 변경 내용을 확인 한 다음 선택 **변경 내용 미리 보기** 올바르게 표시 되도록 합니다.

    ![GitHub 웹, 변경 내용 미리 보기 탭을 보여 주는](media/preview-changes.png)

6. 완료 되 면 페이지의 아래쪽으로 스크롤하여, 포크, 포크에 대 한 설명이 포함 된 이름을 입력 한 다음 항목을 편집 **파일 변경 내용 제안** 개인 GitHub 계정에 포크를 만들려고 합니다.

    ![GitHub 웹, Propose 파일 변경 단추를 보여 주는](media/propose-file-change.png)

    합니다 **변경 내용 비교** 포크에서 원래 콘텐츠 사이의 변경 내용이 확인 화면이 나타납니다.

7. 에 **변경 내용 비교** 화면 표시에서 확인 하는 파일을 사용 하 여 문제가 있는 경우.

    문제가 없는 경우 메시지를 볼 **병합할 수**입니다.

    ![GitHub 웹의 비교를 보여 주는 화면을 변경](media/compare-changes.png)

8. 선택 **끌어오기 요청 만들기**합니다.

    끌어오기 요청 github 리포지토리에서 분기에 푸시되는 변경에 대 한 다른 사용자를 알 수 있습니다. 끌어오기 요청을 연 후에 대해 설명 하 고 공동 작업자를 사용 하 여 잠재적 변경 사항을 검토 추가 하는 후속 커밋 전에 변경 내용을 기본 분기에 병합 됩니다. 자세한 내용은 참조 하세요. [끌어오기 요청에 대 한](https://help.github.com/articles/about-pull-requests)

9. 제목 및 승인자가 요청에 포함 된 내용에 대 한 적절 한 컨텍스트를 제공 하는 설명을 입력 합니다.

10. 이 끌어오기 요청에 변경 된 파일만 있도록 페이지의 아래쪽으로 스크롤하십시오. 그렇지 않은 경우 다른 사람이 변경한 내용을 덮어쓸 수 있습니다.

11. 선택 **끌어오기 요청 만들기** 실제로 끌어오기 요청을 제출 하려면 다시 합니다.

    끌어오기 요청 항목의 작성기로 보내고 편집 검토 됩니다. 요청을 수락 하는 경우 업데이트 게시 됩니다.

## <a name="resources"></a>리소스

- Markdown을 편집 하려면 원하는 텍스트 편집기를 사용할 수 있습니다. 것이 좋습니다 [Visual Studio Code](https://code.visualstudio.com/), Microsoft에서 무료 경량 오픈 소스 편집기입니다.