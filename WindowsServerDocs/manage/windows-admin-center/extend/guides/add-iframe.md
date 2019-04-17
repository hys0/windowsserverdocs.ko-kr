---
title: IFrame 도구 확장 추가
description: Windows Admin Center SDK (Project Honolulu) 도구 확장 개발-iFrame 도구 확장 추가
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 7b4a7b688e4b2d9f52e44395c19211b91b964578
ms.sourcegitcommit: be0144eb59daf3269bebea93cb1c467d67e2d2f1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/20/2018
ms.locfileid: "4080930"
---
# IFrame 도구 확장 추가

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

이 문서의 iFrame Windows Admin Center CLI를 사용 하 여 만든 새, 빈 도구 확장을 추가 하겠습니다.

## 사용자 환경 준비 ##

이미 하지 않은 경우 새, 빈 도구 확장을 만들고 환경을 준비 [도구 확장 개발](..\develop-tool.md) 에서 지침을 따릅니다.

## 프로젝트에 모듈을 추가 합니다. ##

다음 단계에서 iFrame 추가 프로젝트에 새 [빈 모듈](add-module.md) 을 추가 합니다.  

## 모듈에 iFrame 추가 ##

이제 방금 만든 해당 새 빈 모듈에 iFrame 추가 하겠습니다.

\Src\app\, 모듈 폴더로 찾아보기 다음 파일을 열고 ```{!module-name}.component.html```, 다음 명명 규칙을 따라 찾은:

| 값 | 설명 | 예제 파일 이름 |
| ----- | ----------- | ------- |
| ```{!module-name}``` | 모듈 이름(소문자, 공백을 파선으로 대체) | ```manage-foo-works-portal.component.html``` |
    
Html 파일에 다음 콘텐츠를 추가 합니다.

``` html
<div>
  <iframe  style="height: 850px;" src="https://www.bing.com"></iframe>
</div>
```

정말 간단 하죠, 확장을 iFrame를 추가 했습니다.  다음으로 하면 [빌드 및 사이드 로드](..\develop-tool.md#build-and-side-load-your-extension) 결과 확인을 위해 Windows Admin Center 확장 됩니다.
