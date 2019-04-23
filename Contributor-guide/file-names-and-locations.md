<properties title="" pageTitle="파일 이름 및 Windows Server 2016 기술 문서에 대 한 위치" description="문서와 새 문서를 만들 때 따라야 하는 명명 규칙에 대 한 파일 구조를 설명 합니다." metaKeywords="" services="" solutions="" documentationCenter="" authors="Kathy-Davies" videoId="" scriptId="" manager="required" />

<tags ms.service="contributor-guide" ms.devlang="" ms.topic="article" ms.tgt_pltfrm="" ms.workload="" ms.date="03/14/2016" ms.author="jimpark; tysonn" />

# <a name="file-names-and-locations-for-windows-server-technical-articles"></a>파일 이름 및 Windows Server 기술 문서에 대 한 위치

파악 하 고 규칙에 따라 될 수 더 빠르게 수락 끌어오기 요청이 있습니다.

+ [규칙]
+ [패턴]
+ [파일 이름 승인]

## <a name="rules"></a>규칙

- 모든 파일 markdown 및.md 파일 확장명을 사용 해야 합니다.
- 가능한 경우 파일 이름은 3 ~ 5 단어 유지-10 단어는 실제로 가독성 및 SEO에 너무 깁니다.
- 소문자로 변환 하 고 문자, 숫자 및 하이픈만 사용 합니다.
- 공백 또는 문장 부호 문자가 없습니다. 단어와 파일 이름에 번호를 구분 하려면 하이픈을 사용 합니다.
- 사용할 동사를의 약식 형태는 '-ing' 양식: `deploy-nano-server` 없습니다 `Deploying-Nano-Server`
- a, 및와 같은, 작은 단어 유지 또는 합니다.
- 맞춤법 단어입니다. 파일 이름에 승인 되지 않은 또는 불필요 한 머리 글자어를 방지 합니다.
- 파일 이름은 고유-해야 대신 `overview.md` 사용 `storage-spaces-overview.md`

머리 글자어와 파일 이름-특정 지침의에서 두문자어 정의:

- 허용 가능한 이름 약어에 대 한 기존 Microsoft 지침
- 업계 표준 약어 파일 이름에 필요에 따라 사용할 수 있습니다.

## <a name="pattern"></a>무늬

기존 이름 파악 하 고 저장소에서 기사 목록을 검토 합니다. 다음은 일반적인 패턴이입니다.

 **component-topic-title.md**
 
예를 들어 IPv4 주소를 사용하는 경우 `storage-spaces-direct-overview.md`

## <a name="file-name-approval"></a>파일 이름 승인

새 파일을 제출 하는 경우 끌어오기 요청 검토자 이름을 검토 하 고 변경이 필요한 경우 끌어오기 요청 주석 스트림을 통해 피드백을 제공 합니다. 파일 이름을 끌어오기 요청을 수락 하기 전에 수정 해야 합니다. 참가자는 보류 중인 끌어오기 요청에 업데이트를 간단히 푸시할 수 있습니다.

## <a name="folders-in-the-repo"></a>리포지토리에서 폴더

기존 폴더 구조를 사용 합니다. 저장소 관리자의 승인 없이 폴더를 만들지 않습니다 새 폴더를 해야 하는 것이 생각 하는 경우에 대해 설명 합니다.

GitHub 리포지토리를 간단한 폴더 구조 – 비교적 플랫 \<영역 >\\\<기술 >-예제 storage\data-중복 제거에 대 한 합니다. 그러면 다음과 같은 이점이 있습니다.
 - 매우 간단합니다.
 - Azure.com의 작동 원리에 가깝도록
 - 쉽게 신속 하 게 찾을 항목의 – 특정 기술의 중첩 된 위치를 찾고 다른 폴더에서 관련 살펴볼 필요도 없을 기록기/Pm에 대 한 합니다.
 - 적합 한 SEO URL 짧게 유지 하 고 사용자 환경을 고객에 게 경우에 따라 큐에 대 한 URL 확인 합니다.

## <a name="changing-case-in-file-names"></a>파일 이름에서 대/소문자 바꾸기

Windows 운영 체제는 대/소문자 구분. 대/소문자를 해결 하려면 파일 이름을 변경 해야 할 경우 것이 좋습니다 파일의 내용을 변경 하는 Linux 또는 Mac. 아니라면 예를 들어 다음과 같은 가치를 제공해야 합니다.

  biztalk-administration-and-Development-Task-List-in-BizTalk-Services biztalk-services-administration-and-development-task-list-->

사용 된 `git mv` 명령 파일 이름을 바꾸려면:
```
  git mv <WindowsServerDocs/tech-area/subarea/current-file-name.md> <WindowsServerDocs/tech-area/subarea/new-file-name.md>
```

### <a name="contributors-guide-links"></a>참여자 가이드 링크

- [지침 문서 인덱스](./contributor-guide-index.md)


<!--Anchors-->
[규칙]: #rules
[패턴]: #pattern
[파일 이름 승인]: #file-name-approval
