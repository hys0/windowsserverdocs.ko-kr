<properties pageTitle="새 문서를 만들거나 기존 문서를 업데이트 하기 위한 Git 명령" description="만들고 WindowsServerDocs pr에서 문서를 업데이트 하는 단계입니다." metaKeywords="" services="" solutions="" documentationCenter="" authors="Kathy Davies" videoId="" scriptId="" manager="dongill" />

<tags ms.service="contributor-guide" ms.devlang="" ms.topic="article" ms.tgt_pltfrm="" ms.workload="" ms.date="08/24/16" ms.author="kathydav" />

# <a name="git-commands-to-create-or-update-an-article"></a>Git 명령을 만들거나 문서를 업데이트 합니다.

>! 참고: 이러한 명령은 가정에서 파일을 수집할 수 있는 기본 리포지토리를 지정 하는 Github를 구성 했습니다. Github에서 파일을 수집할 수 있는 용어는 사용자 *업스트림*합니다. 파일을 푸시 위치에 *원본*합니다. 리포지토리 및 워크플로 설계 하는 방법에 따라 업스트림 사용자로 설정 해야 Microsoft 조직-아래에 있는 리포지토리에서 https://github.com/Microsoft/WindowsServerDocs-pr 원본 사용자 고유의 Github 계정에서이 리포지토리를 포크 해야 합니다. 예를 들어, 저는 https://github.com/KBDAzure/WindowsServerDocs-pr 

>설정을 확인 하려면 다음을 입력 ```git config -l```합니다. 의도 한 위치를 참조 하는지 확인 하도록 Url을 살펴봅니다.

## <a name="add-or-update-an-article"></a>추가 하거나 문서를 업데이트 합니다.

로컬 분기를 만들고 변경 내용을 저장 한 다음 원격 포크에 푸시합니다 하는 방법을 다음과 같습니다.

1. Git Bash (또는 Git를 사용 하는 명령줄 도구)를 시작 합니다.

2. WindowsServerDocs pr를 변경 합니다.

        cd WindowsServerDocs-pr

3. 로컬 마스터를 유지 하는 것이 좋습니다 분기 및 원격 마스터 분기와 동기화 된 리포지토리의 마스터 분기에서 분기 합니다. 시간--손실 가능성이 조기에 문제를 좋은, 알려진 작동 상태에 유지할 및 노력이 많이 절약할 수 있습니다이. 다음을 실행합니다.

        git checkout master
        git pull upstream master
        git push origin master

4. 작업을 수행 하는 분기를 만들 준비가 되었습니다. 이제 여 일별 또는 결과물 기반에서 작동 합니다. 릴리스 분기에서 로컬 작업 분기 만들기를 실행 하는 데는 가장 좋은 방법은:

        git checkout upstream/upstream-branch-name -b your-local-branch-name

   이 업스트림 분기에서 직접 로컬 분기 만들고 새 로컬 분기에 잘못 된 파일을 병합을 방지할 수 있습니다. 예를 들어, ga 임계값 분기에 따라 작업 분기를 만들려면 다음과 같은 명령을 실행할 수 있습니다.
      
        git checkout upstream/master -b working-11-18

   없는 분기에 병합 해야 하는 콘텐츠에 대해 작업 하는 경우         

5. 포크에 로컬 작업 분기를 추가 합니다.

        git push origin <working branch>

6. 새 문서를 만들거나 기존 아티클을 변경 합니다. Windows 탐색기를 사용 하 여 markdown 파일을 열고 markdown 편집기를 만들고 파일을 편집 합니다. 기본 서식 지정 도움말을 참조 하세요 [문서](https://help.github.com/articles/getting-started-with-writing-and-formatting-on-github/) Github에 있습니다.

7. 추가 필수 메타 데이터 및 버전 정보에 따라 [메타 데이터 및 제품 버전 관리](metadata-OSversioning-and-trademarks.md)합니다.

8. 상태 확인, 그런 다음 추가 하 고 변경 내용을 커밋하십시오.

        git status

   나열 된 파일은 변경 되도록 결과 검토 합니다. 모든 파일을 추가 하려면이 명령을 실행 하는 모든 파일을 정확 하 게 살펴보기:

        git add .
        git commit –m "<comment>"

   특정 파일만 추가할 (경우에 예를 들어 ```git status``` 전송할 원하지 않는 파일을 나열), 대신 실행 해야 합니다.

        git add <file path>
        git commit –m "<comment>"

   >[!IMPORTANT]
   >이 명령은 ```git add .``` 에서 보고 하는 모든 보류 중인 변경 내용 추가 ```git status```합니다. 즉 ```git status``` 추가를 사용 하 여 원하지 않는 추적 되지 않은 업데이트가 표시 ```git add <file path>``` 대신 합니다.  

9. 업스트림 리포지토리의 변경 내용으로 로컬 작업 분기를 업데이트 합니다.

        git pull upstream master

10. 변경 내용의 github 포크에 푸시하십시오.

        git push origin <working branch>

## <a name="submit-your-changes"></a>변경 내용을 제출합니다

스테이징, 유효성 검사 및/또는 게시에 대 한 콘텐츠를 전송할 준비 된 경우 끌어오기 요청을 만들려면 GitHub UI를 사용 합니다. 

PR (끌어오기 요청)를 열면이 테스트 패스를 트리거합니다, 그리고 프로젝트를 빌드하고 내부 스테이징 사이트를 게시 합니다. 준비가 되지 테스트 패스를 가져올 및 스테이징 사이트에서 업데이트를 확인 하는 방법 이기 때문에 병합 하는 끌어오기 요청을 열려면 괜찮습니다. 빌드 정보 및 스테이징 링크 주석으로 PR에 게시 된 

다음을 수행 해야 하는 것 **병합 하 여 변경 하기 전에**:
  - 검토 빌드 오류가 포함 되어 있는지 확인 하려면 자세한 정보. 
  - 스테이징 사이트에서 업데이트를 검토 합니다.

이 작업을 수행한 후으로 나타냅니다.
- "병합 준비" 레이블이 PR에 추가 \(클릭 **레이블을** 또는 PR에서 주석 스트림에 오른쪽에 있는 기어 아이콘)
- 병합 준비 주석을 추가 하 고 검토자가 끌어오기 WSSC 별칭으로 전자 메일 보내기: wssc pra가

PR 검토자는 변경 내용을 확인 하 고 문제 또는 질문 사항이 없다면 PR을 허용 합니다. 의견이 나 문제를 해결 하는 요청은 주석으로 추가 됩니다. 검토 [품질 기준에 대 한 끌어오기 요청 검토](contributor-guide-pr-criteria.md) 에 예상 되는 결과 알아봅니다.

## <a name="publishing"></a>Publishing

- 약 10 오전 및 오후 3 시에 문서가 게시 되 태평양 표준시, 월요일-금요일입니다. 끌어오기 요청 검토자를 검토 하 고 동의 가능 하기 전에 변경 내용을 병합 하는 데 시간이 필요 하는 점을 염두에 두십시오. 예약 된 다음 게시 주기에서 선택 하도록 변경 내용은 병합 해야 합니다. 특정 게시 주기에 대 한 게시 된 아티클에 해야 하는 경우를 미리 알지 끌어오기 요청 검토자를 사용 수 있습니다. PR을 수락 하면 변경 내용을 리포지토리에 병합 되 고 번 게시 실행에 포함 됩니다. 게시 후 온라인으로 표시 하는 문서에 대 한 최대 30 분 정도 걸릴 수 있습니다. 
