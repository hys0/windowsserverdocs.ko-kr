---
title: 도구 확장에 iFrame 추가
description: Windows Admin Center SDK (프로젝트 브라 티) 도구 확장을 개발-도구 확장에 iFrame을 추가 합니다.
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: da3850b75a0e069f9153d3c66baef9f00b67d61c
ms.sourcegitcommit: 48bb3e5c179dc520fa879b16c9afe09e07c87629
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66452591"
---
# <a name="add-an-iframe-to-a-tool-extension"></a>도구 확장에 iFrame 추가

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

이 문서에서는 iFrame Windows Admin Center CLI를 사용 하 여 만든 새로운 빈 도구 확장에 추가 합니다.

## <a name="prepare-your-environment"></a>사용자 환경 준비 ##

이미 않았다면의 지시를 따릅니다 [개발 도구 확장](../develop-tool.md) 환경을 준비 하 고 새 빈 도구 확장 합니다.

## <a name="add-a-module-to-your-project"></a>프로젝트에 모듈을 추가 합니다. ##

새 [빈 모듈](add-module.md) 프로젝트에는 다음 단계에서 iFrame 추가 됩니다.  

## <a name="add-an-iframe-to-your-module"></a>IFrame 모듈에 추가 ##

이제 iFrame 우리가 방금 만들었던는 새로 만든 빈 모듈에 추가 합니다.

\Src\app에서\, 에 모듈 폴더를 찾은 다음 파일을 엽니다 ```{!module-name}.component.html```다음 명명 규칙을 사용 하 여 발견 되었습니다.

| 값 | 설명 | 예제 파일 이름 |
| ----- | ----------- | ------- |
| ```{!module-name}``` | 모듈 이름(소문자, 공백을 파선으로 대체) | ```manage-foo-works-portal.component.html``` |
    
Html 파일에 다음 콘텐츠를 추가 합니다.

``` html
<div>
  <iframe  style="height: 850px;" src="https://www.bing.com"></iframe>
</div>
```

, 확장 프로그램에 iFrame을 추가 했습니다.  어 있습니다 [빌드 및 부하 쪽](../develop-tool.md#build-and-side-load-your-extension) Windows Admin Center 결과를 보려면 확장 합니다.

> [!Note]
> 콘텐츠 보안 정책 (CSP) 설정을 Windows Admin Center 내에서 iFrame 렌더링에서 일부 사이트 되지 않을 수 있습니다. 이 대해 알아보십시오 [여기](https://content-security-policy.com/)합니다. 
