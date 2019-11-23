---
title: 도구 확장에 iFrame 추가
description: 도구 확장 개발 Windows 관리 센터 SDK (Project Honolulu)-도구 확장에 iFrame 추가
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 0833b2fd92f2bf4b512120783bb71295a3112745
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406893"
---
# <a name="add-an-iframe-to-a-tool-extension"></a>도구 확장에 iFrame 추가

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

이 문서에서는 Windows 관리 센터 CLI를 사용 하 여 만든 새로운 빈 도구 확장에 iFrame을 추가 합니다.

## <a name="prepare-your-environment"></a>사용자 환경 준비 ##

아직 하지 않은 경우 [도구 확장 개발](../develop-tool.md) 의 지시에 따라 환경을 준비 하 고 비어 있는 새 도구 확장을 만듭니다.

## <a name="add-a-module-to-your-project"></a>프로젝트에 모듈 추가 ##

프로젝트에 새 [빈 모듈](add-module.md) 을 추가 합니다. 그러면 다음 단계에서 iFrame을 추가 합니다.  

## <a name="add-an-iframe-to-your-module"></a>모듈에 iFrame 추가 ##

이제 방금 만든 비어 있는 새 모듈에 iFrame을 추가 합니다.

\Src\app app에서 모듈 폴더로 이동한 후 다음 명명 규칙을 사용 하 여 파일 ```{!module-name}.component.html```를 엽니다.\,

| 값 | 설명 | 예제 파일 이름 |
| ----- | ----------- | ------- |
| ```{!module-name}``` | 모듈 이름(소문자, 공백을 파선으로 대체) | ```manage-foo-works-portal.component.html``` |
    
Html 파일에 다음 콘텐츠를 추가 합니다.

``` html
<div>
  <iframe  style="height: 850px;" src="https://www.bing.com"></iframe>
</div>
```

이제 확장에 iFrame을 추가 했습니다.  다음으로 Windows 관리 센터에서 확장을 [빌드하고 로드](../develop-tool.md#build-and-side-load-your-extension) 하 여 결과를 볼 수 있습니다.

> [!Note]
> CSP (콘텐츠 보안 정책) 설정으로 인해 일부 사이트가 Windows 관리 센터 내 iFrame에서 렌더링 되지 않을 수 있습니다. [여기](https://content-security-policy.com/)에서 자세히 알아볼 수 있습니다. 
