# <a name="rename-or-delete-an-article"></a>이름 바꾸기 또는 문서 삭제

아티클을 삭제 하거나 이름을 변경 하기 전에 방지 또는 끊어진된 링크 수가 감소 하는이 프로세스를 수행 해야 합니다. 끊어진된 링크를 싫어합니다 고객과 하나 세션이 될 해제 발음이 물어보면 합니다. 이름 바꾸기 또는 아티클을 삭제 합니다.이 프로세스의 마지막 단계는 첫 번째 없습니다.


## <a name="step-1-manage-inbound-links"></a>1단계: 인바운드 링크 관리

블로그, 포럼 및 기타 콘텐츠는 웹에서 같은 콘텐츠에, 타사 인바운드 링크가 있는지 확인 합니다. 다음이 링크를 변경 하려면 블로그 소유자에 게 문의할 제거 하거나 포럼 게시물에서 링크를 업데이트 합니다. 웹 분석 도구를 이러한 방식으로 관리 해야 할 수 있습니다 트래픽이 높은 인바운드 링크를 식별할 수 있습니다.

## <a name="step-2-remove-all-crosslinks-to-the-article-from-the-windowsserverdocs-pr-repository"></a>2단계: WindowsServerDocs pr 리포지토리에서 문서를 모든 교차 연결 제거

1. 로컬 새로 고침 실행 분기 – `git pull upstream <branch>`, ie를 마스터에서 새로 고침 실행 `git pull upstream master`

2.  이름을 바꾸거나 사용 중지 하려는 문서에 대 한 링크가 있는 문서를 검색 하려면 WindowsServerDocs pr 폴더를 검사 한 다음 링크를 제거 하거나 다른 문서에 대 한 링크를 사용 하 여 교체할 문서를 업데이트 합니다. 검색을 사용 하 고 바꾸기 유틸리티 설치 되어 있는 교차 링크를 찾을 수 있습니다. 이렇게 하지 않으면 Windows PowerShell을 사용할 수 있습니다.

 a. Windows PowerShell을 시작합니다.

 b. PowerShell 프롬프트에서 WindowsServerDocs pr 폴더로 변경 합니다.

 `cd WindowsServerDocs-pr\WindowsServerDocs-pr`

 다. 이름 바꾸기 또는 삭제 하기 위해 문서에 대 한 링크를 포함 하는 모든 파일을 나열 하는 명령을 실행 합니다.

 `Get-ChildItem -Recurse -Include *.md* | Select-String "<the name of the topic you are deleting>" | group path | select name`

  파일 이름 목록 (이 예제의 경우 라는 psoutput.txt)에 텍스트 파일에 보내려면 다음을 실행 합니다.

  `Get-ChildItem -Recurse -Include *.md* | Select-String "<the name of the topic you are deleting>" | group path | select name | Out-File C:\Users\<your account>\psoutput.txt`

3. 추가 및 모든 변경 내용을 커밋합니다, 그리고 포크, 포크에 푸시합니다. 그리고 및 끌어오기 요청을 여세요. 자세한 내용은 [만들거나 문서를 업데이트 합니다. Git 명령을](git-steps-create-update-content.md)합니다.

## <a name="step-3-update-fwlinks"></a>3단계: FWLinks를 업데이트 합니다.

문서를 가리키는 모든 FWLinks FWLink 도구를 확인 합니다. 대체 콘텐츠를 모든 FWLinks 가리키는 링크를 소유 하는 별칭에 있지 않다면 조인 합니다. 소유자 않습니다 링크를 업데이트 하는 경우 MSCOM 변경 링크를 사용 하 여 티켓을 제출 합니다. 자세한 내용은- [내부 wiki](http://sharepoint/sites/azurecontentguidance/wiki/Pages/Manage%20inbound%20links%20to%20retired%20topics.aspx)합니다.

## <a name="step-4-remove-crosslinks-to-the-article-from-table-of-contents"></a>4단계: 목차에서 문서 교차 연결 제거

ToC.md 파일을 유지 관리 담당자를 사용 하 여 작동 합니다. 이 파일은 기술 라이브러리의 내용의 왼쪽 테이블을 채웁니다. 누구에 게 작업을 모르는 경우 전자 메일을 보내 wssc-pra@microsoft.com합니다.

## <a name="step-5-add-redirects"></a>5단계: 리디렉션을 추가합니다
파일을 삭제 하는 자세한, 이름을 변경 하는 경우 기존 링크를 중단 하지 않도록 있도록 리디렉션을 추가 합니다.

1. 오래 된 파일이 기존 파일 이름 사용 하 여 기존 위치에 둡니다.
2. 이 부분은 메타 데이터 파일의 콘텐츠를 바꿉니다.
   ```
   ---
   redirect_url: <redirection-URL-or-file>
   ---
   ```
   \<리디렉션 URL-또는-파일 > 다른 위치에 전체 url 또는 경로 + 파일 이름입니다. 동일한 OPS 리포지토리의 다른 항목입니다.

   예를 들어 전체 파일을 사용이 됩니다.

   ```
   ---
   redirect_url: ../../failover-clustering/whats-new-in-failover-clustering
   ---
   ```

3. 후 리디렉션, PR-리디렉션 작동 하는 경우에 대 한 설명 링크 대상 항목으로 가져와야 하는 클릭에 대 한 PR을 만드는 중입니다.

## <a name="step-6-rename-or-delete-the-article"></a>6단계: 이름 바꾸기 또는 문서 삭제

리디렉션을 사용 하지 않는 경우 이전 단계를 완료 한 후이 단계를 수행 하 고 영향을 받는 모든 아티클에 게시 됩니다. 리디렉션을 사용 하는 경우 문서 삭제 또는 이름 바꾸기이 실행 취소 끊어진된 링크 발생 합니다. 파일 이름 바꾸기, 파일 시스템에서 이름을 바꿀 다음 추가, 커밋 및 변경 내용을 푸시 및 끌어오기 요청을 엽니다.
파일을 삭제 하려면 먼저 알아야 할 것 때문에이 소스 제어 시스템을 주세요.이 작업을 수행 하는 데 필요한 파일 시스템에서 파일을 삭제 하려면 작동 하지 않습니다. 그렇지 않은 경우 삭제 된 파일 다시 아마도 나타납니다.
이때 다음과 같은 두 가지 방법을 사용할 수 있습니다.

- 파일 시스템 및 git의 경우: 파일 시스템에서 파일을 삭제 합니다. 그런 다음 git 도구에서 다음 중 하나를 실행합니다  ```Git add -A``` | ```Git add --all``` | ```Git add -u```
- 단순히 git의 경우:   ```git rm foo.md```를 실행합니다.

    자세한 내용은 [ http://stackoverflow.com/questions/2047465/how-can-i-delete-a-file-from-git-repo ](http://stackoverflow.com/questions/2047465/how-can-i-delete-a-file-from-git-repo) 및 [https://git-scm.com/docs/git-rm](https://git-scm.com/docs/git-rm) 

## <a name="step-7-find-and-fix-straggler-broken-links"></a>7단계: 찾기 및 straggler 끊어진된 링크 수정

콘텐츠 QA 도구를 사용 하 여 이전 단계를 하지 않은 catch 한 다음 제거 하거나 연결을 수정할는 끊어진된 링크를 찾을 수 있습니다.

## <a name="step-8-remove-cached-pages-from-search-engines"></a>8단계: 검색 엔진에서 캐시 된 페이지를 제거 합니다.

검색 엔진에서 캐시 된 웹 페이지를 제거 하려면 이러한 웹 페이지로 이동 합니다. [Bing](https://www.bing.com/webmaster/tools/content-removal?rflid=1)
[Google](https://www.google.com/webmasters/tools/removals?pli=1)


### <a name="contributors-guide-links"></a>참여자 가이드 링크

- [지침 문서 인덱스](./contributor-guide-index.md)

