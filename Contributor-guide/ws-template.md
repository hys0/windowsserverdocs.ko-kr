---
title:
- 문서 제목
description: ''
author:
- GITHUB USERNAME
ms.author:
- MICROSOFT ALIAS
ms.date:
- DATE
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: ''
ms.localizationpriority:
- high/medium/low
ms.openlocfilehash: 4f885680426c0bfa55d5f73a7ef0c2143a8dd5a9
ms.sourcegitcommit: e0479b0114eac7f232e8b1e45eeede96ccd72b26
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/22/2018
ms.locfileid: "2082445"
---
# <a name="metadata-and-markdown-template"></a>메타 데이터 및 Markdown 서식 파일

이 작업 서식 파일을 사용 하면 Markdown 구문, 메타 데이터 설정에 대 한 지침의 예제가 있습니다. 최대한의 [원시 Markdown](https://raw.githubusercontent.com/Microsoft/WindowsServerDocs-pr/master/Contributor-guide/ws-template.md?token=AG1vEhARRHNLtPgKXP35BGjNZGajKOArks5YLNIwwA%3D%3D) 및 [보기에서 렌더링](https://github.com/Microsoft/WindowsServerDocs-pr/blob/master/Contributor-guide/ws-template.md)를 표시 해야 합니다. (원시 Markdown 이표시되고 메타 데이터 블록은 렌더링 된 보기는 그렇지 않습니다.)

Markdown 파일을 만들 때 새 파일을이 서식 파일을 복사 하 고, 문서의 제목에 위의 H1 제목을 설정 아래에 지정된 된 대로 메타 데이터 내용을 입력 하 고, 콘텐츠를 삭제 해야 있습니다 합니다. CAPS 대괄호에서에 들어 있는 개체 주의 해야합니다.


## <a name="metadata"></a>메타데이터 

전체 메타 데이터 블록은 위에입니다. 일부 주요 참고 사항:

- 콜론 (:)과 메타 데이터 요소에 대 한 값 사이 공백이 포함 **해야** 합니다.
- 값 (예: 제목)에 콜론 메타 데이터 파서를 중단 합니다. 자신의 전체에서의 콜론에 대 한 HTML 인코딩을 사용 하 여 `&#58;` (예를들어, `"title: Azure Rights Management&#58; the basics | Azure RMS"`).
- **제목**:이 제목 검색 엔진 결과에 표시 됩니다. 
- **만든이**: 만든이 필드의 만든이가 별칭 하지 **GitHub username** 포함 되어야 합니다.
- **ms.prod**, **ms.technology**: ms.prod (또는 w10 Windows 10에 대 한 콘텐츠를 만들려면이 서식 파일을 사용 하는 경우)에 대 한 "windows 서버 임계값"을 사용 합니다. Ms.technology 값을 가져오려면 CX 상대에 게 문의 합니다.

## <a name="basic-markdown-gfm-and-special-characters"></a>기본 Markdown, GFM, 및 특수 문자

모든 기본 및 GitHub flavored Markdown 지원 됩니다. 여기에 대 한 자세한 내용은 다음을 참조 합니다.

- [초기 계획 Markdown 구문](https://daringfireball.net/projects/markdown/syntax)
- [GitHub flavored Markdown (GFM) 설명서](https://guides.github.com/features/mastering-markdown)

Markdown와 같은 특수 문자를 사용 합니다 \ *, \', 및 \ 서식 지정을 위한 # 합니다. 콘텐츠에 이러한 문자 중 하나를 포함 하려는 경우 두 작업 중 하나를 수행 해야 합니다.

- 특수 문자 "이스케이프"를 앞에 백슬래시를 배치 (등 \\\ *에 대 한 프로그램 \ *)
- [HTML 엔터티 코드](http://www.ascii.cl/htmlcodes.htm) 를 사용 하 여 문자에 대 한 (등 \ & \#42\;에 대 한 프로그램 & #42;).

## <a name="headings"></a>머리글

머리글을 수행 해야 atx 스타일을 사용 하 여, 즉, 문자를 사용할 1-6 해시 (#) 줄의 시작 부분에 HTML 제목 수준까지 H1부터 h 6 통해 해당 프로그램 머리글을 표시 합니다. 첫번째 및 두번째 수준의 헤더의 예는 위의 사용 됩니다. 

다음과 같은 페이지에 제목으로 표시 될 대화 항목에 하나만 수준 1 머리글 (H1) 이어야 **합니다** .  

두번째 수준의 머리글에 페이지 제목 아래 "이 문서의" 섹션에 표시 되는 페이지에 목차가 생성 됩니다.

### <a name="third-level-heading"></a>세번째 수준의 제목
#### <a name="fourth-level-heading"></a>네번째 수준 제목
##### <a name="fifth-level-heading"></a>다섯번째 수준 제목
###### <a name="sixth-level-heading"></a>사용자 중 6 번째 수준 제목

## <a name="text-styling"></a>텍스트 스타일

*기울임꼴* 

**Bold** 

~~취소선~~

## <a name="links"></a>링크

### <a name="internal-links"></a>내부 링크

동일한 Markdown 파일에서 머리글 연결할 게시 된 문서의 원본을 봅니다, 헤드의 ID를 찾습니다 (예 `id="blockquote"`), # + id를 사용 하 여 링크 (등 `#blockquote`).

- 예: [Blockquotes](#blockquote)

동일한 repo에서 Markdown 파일에 연결 하려면 [상대 링크](https://www.w3.org/TR/WD-html40-970917/htmlweb.html#h-5.1.2), 파일 이름 끝에 ".md"를 포함 하 여 사용 합니다.

- 예: [팁 및 주의 사항이](tips-gotchas.md)
- 예: [도구 및 참가자 (영문)에 대 한 설치](../readme.md)

동일한 repo에서 Markdown 파일에서 머리글에 연결할 상대 연결 + 태그 연결을 사용 합니다.

- 예: [파일 삭제](tips-gotchas.md#deleting-files)

### <a name="external-links"></a>외부 링크

외부 파일에 연결할 링크로 전체 URL을 사용 합니다.

- 예: [GitHub](http://www.github.com)

URL을 Markdown 파일에 나타나는 경우, 클릭 가능한 링크로 변환 됩니다.

- 예:http://www.github.com

## <a name="lists"></a>목록

### <a name="ordered-lists"></a>순서가 지정 된 목록

1. 이 
1. 은
1. 는
1. 정렬
1. List  


#### <a name="ordered-list-with-an-embedded-list"></a>포함 된 목록으로 목록 정렬

1. 여기서
1. 제공
1. 는
1. 포함 된
    1. 누락 Scarlett
    1. 교수가 진한 보라
1. 정렬
1. list


### <a name="unordered-lists"></a>순서 없는 목록

- 이
- 이 
- a
- 글머리 기호
- list


##### <a name="unordered-list-with-an-embedded-list"></a>포함 된 목록으로 순서 없는 목록

- 이 
- 글머리 기호 
- list
    - Mrs. 광택
    - 님 녹색
- 포함  
- 기타
    1. 대령 Mustard
    1. Mrs. 흰색
- 목록


## <a name="horizontal-rule"></a>수평선

---

## <a name="tables"></a>테이블

거의 모든 인스턴스에 MD 테이블에 대 한 서식을 사용 합니다. HTML 테이블 더 큰 유연성을 제공 하는 동안 콘텐츠에 사용할는 하지 마십시오. 사용자 문서를 HTML 테이블에 있는 해당 문서를 병합 하지 않습니다.

| 테이블        | 는           | 매우 편리한  |
| ------------- |:-------------:| -----:|
| col 3은      | 오른쪽 맞춤 | $ 1600 |
| col 2는      | 가운데 맞춤      |   $12 |
| 열 1은 기본값 | 왼쪽 맞춤     |    $ 1 |


## <a name="code"></a>Code

### <a name="generic-codeblock"></a>일반 codeblock

일반 codeblock을 코딩 하기 위한 코드 4 공간을 들여씁니다.

    function fancyAlert(arg) {
      if(arg) {
        $.docs({div:'#foo'})
      }
    }


### <a name="codeblocks-with-language-identifier"></a>언어 식별자를 가진 Codeblocks

세 backticks (& #96; & #96; & #96;)을 사용 하 여 특정 언어 관련 색을 적용 하는 언어 ID 코드 블록을 코딩 + 합니다.  다음은 [GitHub Flavored Markdown (GFM) 언어 Id의](https://github.com/jmm/gfm-lang-ids/wiki/GitHub-Flavored-Markdown-(GFM)-language-IDs)전체 목록입니다.

##### <a name="c9839"></a>& #9839;

```c#
using System;
namespace HelloWorld
{
    class Hello 
    {
        static void Main() 
        {
            Console.WriteLine("Hello World!");

            // Keep the console window open in debug mode.
            Console.WriteLine("Press any key to exit.");
            Console.ReadKey();
        }
    }
}
```
#### <a name="python"></a>Python

```python
friends = ['john', 'pat', 'gary', 'michael']
for i, name in enumerate(friends):
    print "iteration {iteration} is {name}".format(iteration=i, name=name)
```
#### <a name="powershell"></a>PowerShell

```powershell
Clear-Host
$Directory = "C:\Windows\"
$Files = Get-Childitem $Directory -recurse -Include *.log `
-ErrorAction SilentlyContinue
```

### <a name="inline-code"></a>인라인 코드

Backticks (& #96;) 사용에 대 한 `inline code`합니다.

## <a name="blockquotes"></a>Blockquotes

> 가뭄이 10 백만 년에 대 한 지금 지속 명의 및 무시 무시 한 도마뱀의 시대 오래 끝난 합니다. 여기는 아프리카,으로 1 일을 알려진 것 대륙에는 적도에서 불과합니다 존재 여부에 대 한 명의 도달 ferocity의 새로운 climax와는 빅터가 시각에서 아직 없습니다. 이 barren 및 desiccated 랜드에서 작은 또는 swift는 피어스 수 장식, 또는 살아남기 하고자 합니다.

## <a name="images"></a>이미지

### <a name="static-image"></a>정적 이미지

![대체 텍스트입니다.](../windowsserverdocs/get-started/media/wsbanner.png)

### <a name="linked-image"></a>연결 된 이미지

[![a연결 된 이미지에 대 한 텍스트를 lt](../windowsserverdocs/get-started/nano.png)](../windowsserverdocs/get-started/getting-started-with-nano-server.md) 

## <a name="alerts"></a>경고

### <a name="note"></a>참고

> [!NOTE]
> 이 메모

### <a name="warning"></a>Warning

> [!WARNING]
> 이 경고는

### <a name="tip"></a>팁

> [!TIP]
> 이것은 팁

### <a name="important"></a>Important

> [!IMPORTANT]
> 이것은 중요

