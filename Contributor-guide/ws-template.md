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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59879564"
---
# <a name="metadata-and-markdown-template"></a>메타 데이터 및 Markdown 템플릿

이 OPS 템플릿 메타 데이터 설정에 대 한 지침 뿐만 아니라 Markdown 구문에 대 한 예가 포함 되어 있습니다. 대부분의 가져오려는 모두 확인 해야 합니다 있습니다는 [원시 Markdown](https://raw.githubusercontent.com/Microsoft/WindowsServerDocs-pr/master/Contributor-guide/ws-template.md?token=AG1vEhARRHNLtPgKXP35BGjNZGajKOArks5YLNIwwA%3D%3D) 하며 [뷰를 렌더링](https://github.com/Microsoft/WindowsServerDocs-pr/blob/master/Contributor-guide/ws-template.md). (원시 Markdown 표시는 메타 데이터 블록이 하는 반면 렌더링 된 보기에는 않습니다.)

Markdown 파일을 만들 때이 템플릿을 새 파일을 복사 해야, 위의 H1 제목을 문서의 제목 아래 지정 된 집합으로 메타 데이터 입력 및 콘텐츠를 삭제 합니다. 대문자로 대괄호 안에 있는 모든 항목에 주의가 필요합니다.


## <a name="metadata"></a>메타데이터 

전체 메타 데이터 블록을 초과 합니다. 몇 가지 주요 참고 사항:

- 있습니다 **해야** 콜론 (:) 사이 공백이 있어야 합니다. 및 메타 데이터 요소에 대 한 값입니다.
- 값 (예: 제목)에 콜론을 사용할 메타 데이터 파서가 중단 됩니다. 그 대신에서의 콜론 HTML 인코딩을 사용 하 여 `&#58;` (예를 들어 `"title: Azure Rights Management&#58; the basics | Azure RMS"`).
- **title**: 이 제목은 검색 엔진 결과에 표시 됩니다. 
- **author**: 작성자 필드를 포함 해야 합니다 **GitHub 사용자 이름** 는 별칭이 아니라 작성자의 합니다.
- **ms.prod**, **ms.technology**: "Windows server 임계값"을 사용 하 여 ms.prod (또는 w10 Windows 10에 대 한 콘텐츠를 만들려면이 템플릿을 사용 하는 경우). Ms.technology 값을 검색할 CX 담당자에 게 설명 합니다.

## <a name="basic-markdown-gfm-and-special-characters"></a>기본 Markdown, GFM 및 특수 문자

모든 기본 및 GitHub 지원 Markdown이 지원 됩니다. 에 대 한 자세한 내용은 다음을 참조 하세요.

- [기준 Markdown 구문](https://daringfireball.net/projects/markdown/syntax)
- [GitHub 지원 Markdown (GFM) 설명서](https://guides.github.com/features/mastering-markdown)

Markdown와 같은 특수 문자를 사용 합니다 \*, \`, 및 \# 서식 지정에 대 한 합니다. 콘텐츠에 다음이 문자 중 하나를 포함 하려는 경우 두 가지 중 하나를 수행 해야 합니다.

- 특수 문자를 "이스케이프" 앞에 백슬래시를 넣어 (예를 들어 \\ \* 에 대 한는 \*)
- 사용 합니다 [HTML 엔터티 코드](http://www.ascii.cl/htmlcodes.htm) 문자 (예를 들어 \& \#42\; 에 대 한를 &#42;).

## <a name="headings"></a>머리글

머리글 해야 H6 통해 HTML 제목 수준 H1에 해당 머리글을 나타내는 줄의 시작 부분에 1 ~ 6 해시 문자 (#)를 사용, atx 스타일을 사용 합니다. 첫 번째 및 두 번째 수준 헤더의 예는 위에서 사용 됩니다. 

있습니다 **해야** 페이지 제목으로 표시 되는 항목에 하나만 첫 번째 수준 제목 (H1) 수입니다.  

두 번째 수준 제목은 페이지 제목 아래에 있는 "이 문서의" 섹션에 표시 되는 페이지 상 TOC를 생성 합니다.

### <a name="third-level-heading"></a>세 번째 수준 제목
#### <a name="fourth-level-heading"></a>네 번째 수준 제목
##### <a name="fifth-level-heading"></a>다섯 번째 수준 제목
###### <a name="sixth-level-heading"></a>여섯 번째 수준 제목

## <a name="text-styling"></a>텍스트 스타일

*기울임꼴* 

**굵게** 

~~취소선~~

## <a name="links"></a>링크

### <a name="internal-links"></a>내부 링크

동일한 Markdown 파일의 헤더에 연결 하려면 게시 된 문서의 소스를 보고, 헤드의 ID를 찾을 (예를 들어 `id="blockquote"`), # + id를 사용 하 여 연결 하 고 (예를 들어 `#blockquote`).

- 예: [Blockquotes](#blockquote)

동일한 리포지토리에 있는 Markdown 파일에 연결 하려면 사용 하 여 [상대 링크](https://www.w3.org/TR/WD-html40-970917/htmlweb.html#h-5.1.2), 파일 이름 끝에 ".md"를 포함 합니다.

- 예: [팁 및 문제](tips-gotchas.md)
- 예: [도구 및 참가자에 대 한 설정](../readme.md)

동일한 리포지토리에 있는 Markdown 파일의 헤더에 연결 하려면 상대 연결 + 해시 태그 연결을 사용 합니다.

- 예: [파일 삭제](tips-gotchas.md#deleting-files)

### <a name="external-links"></a>외부 링크

외부 파일에 연결 하려면 전체 URL을 링크로 사용 합니다.

- 예: [GitHub](http://www.github.com)

URL에 표시 되 면 Markdown 파일을 링크로 변환 됩니다.

- 예: http://www.github.com

## <a name="lists"></a>목록

### <a name="ordered-lists"></a>정렬 된 목록

1. 이 
1. 예
1. 두 번째 유형은
1. 정렬
1. 목록  


#### <a name="ordered-list-with-an-embedded-list"></a>정렬 된 목록이 포함 된 목록 사용 하 여

1. 여기
1. 제공
1. 는
1. 포함 된
    1. 누락 Scarlett
    1. 교수 진한 보라
1. 정렬
1. 목록


### <a name="unordered-lists"></a>순서가 지정 되지 않은 목록

- 이
- 이
- a
- 글머리 기호
- 목록


##### <a name="unordered-list-with-an-embedded-list"></a>포함 된 목록 사용 하 여 순서가 지정 되지 않은 목록

- 이 
- 글머리 기호 
- 목록
    - Mrs. 김덕훈
    - Mr. 녹색
- 포함  
- 기타
    1. 대령이 Mustard
    1. Mrs. 백서
- 목록


## <a name="horizontal-rule"></a>가로줄

---

## <a name="tables"></a>테이블

거의 모든 경우에서 테이블에 대 한 서식 지정 MD를 사용 합니다. 더 많은 유연성을 제공 하는 HTML 테이블 콘텐츠에서 사용 하지. 에서는 HTML 테이블을 문서에 있는 경우 해당 문서를 병합 되지 않습니다.

| 테이블        | 는           | 쿨  |
| ------------- |:-------------:| -----:|
| col 3      | 오른쪽 맞춤 | $1600 |
| col 2      | 가운데 맞춤      |   $12 |
| col 1 기본값입니다. | 왼쪽 맞춤     |    $1 |


## <a name="code"></a>코드

### <a name="generic-codeblock"></a>제네릭 codeblock

제네릭 codeblock 코딩 하는 것에 대 한 코드 4 개 공간을 들여씁니다.

    function fancyAlert(arg) {
      if(arg) {
        $.docs({div:'#foo'})
      }
    }


### <a name="codeblocks-with-language-identifier"></a>언어 식별자를 사용 하 여 Codeblocks

3 개의 backtick를 사용 하 여 (&#96;&#96;&#96;) + 코드 블록에 언어별 색을 적용할 언어 ID를 코딩 합니다.  전체 목록은 다음과 같습니다 [Flavored Markdown GFM (GitHub) 언어 Id](https://github.com/jmm/gfm-lang-ids/wiki/GitHub-Flavored-Markdown-(GFM)-language-IDs)합니다.

##### <a name="c9839"></a>C&#9839;

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

사용할 backtick (&#96;)에 대 한 `inline code`합니다.

## <a name="blockquotes"></a>Blockquotes

> 가뭄이 지속 10 백만 년 및를 지배는 오래 전에 통치 공룡의 종료 된 합니다. 여기서는 1 일 이라고 아프리카 대륙, 적도에서 있는지 전쟁 했습니다에 도달 ferocity의 예 전에 없었습니다 아직에. 이 척박 하 고 메 마른 땅에서는 오직 작고 또는 swift의 열렬 수 다양성이, 또는 효력을 유지 하 합니다.

## <a name="images"></a>이미지

### <a name="static-image"></a>정적 이미지

![대체 텍스트입니다.](../windowsserverdocs/get-started/media/wsbanner.png)

### <a name="linked-image"></a>연결 된 이미지

[![연결 된 이미지에 대 한 대체 텍스트](../windowsserverdocs/get-started/nano.png)](../windowsserverdocs/get-started/getting-started-with-nano-server.md) 

## <a name="alerts"></a>,

### <a name="note"></a>참고

> [!NOTE]
> 이것은 참고

### <a name="warning"></a>경고

> [!WARNING]
> 이 값이 WARNING

### <a name="tip"></a>팁

> [!TIP]
> 이 팁

### <a name="important"></a>중요

> [!IMPORTANT]
> 이것은 중요 합니다.

