---
title: 다른 버전의 Windows Admin Center SDK를 대상
description: 다른 버전을 대상으로 Windows Admin Center SDK (프로젝트 브라 티)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 47ae669e517f963762ee6267594e18f3413a72ff
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59833624"
---
# <a name="target-a-different-version-of-the-windows-admin-center-sdk"></a>다른 버전의 Windows Admin Center SDK를 대상

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

확장 SDK 변경 내용 및 플랫폼 변경 내용을 사용 하 여 최신 상태로 유지 하는 것은 쉽습니다.  사용 하 여 [NPM 태그](https://www.npmjs.com/package/@microsoft/windows-admin-center-sdk) SDK 버전으로 새 기능 릴리스를 구성할 수 있습니다.

다음 세 가지 SDK 버전에서 선택할 수 있습니다.

* ```latest``` -이 SDK 패키지 현재 GA 릴리스의 Windows Admin Center 사용 하 여 정렬
* ```insider``` -이 SDK 패키지는 현재 미리 보기 릴리스의 Windows Admin Center (Windows Server Insider Preview에서 사용 가능)를 사용 하 여 정렬
* ```next``` -이 SDK 패키지에는 최신 기능이 포함 되어 있습니다.

> [!NOTE]
> 다양 한 자세히 알아보려면 [버전](https://aka.ms/WACDownloadPage) 다운로드에 사용할 수 있는 Windows Admin Center입니다.

## <a name="targeting-sdk-version-on-a-new-project"></a>새 프로젝트에 대해 SDK 버전 대상 지정

새 확장을 만들 때 포함할 수 있습니다는 ```--version``` 매개 변수를 다른 버전의 SDK 대상으로 합니다.

```
wac create --company "{!Company Name}" --tool "{!Tool Name}" --version {!version}
```

| 값 | 설명 | 예제 |
| ----- | ----------- | ------- |
| ```{!Company Name}``` | 회사 이름 (공백 포함) | ```Contoso Inc``` |
| ```{!Tool Name}``` | 사용자 도구 이름 (공백 포함) | ```Manage Foo Works``` |
| ```{!version}``` | SDK 버전 | ```latest``` |

새 확장 대상 만들기 예로 ```insider```:

```
wac create --company "Contoso Inc" --tool "Manage Foo Works" --version insider
```

## <a name="targeting-sdk-version-on-an-existing-project"></a>기존 프로젝트의 SDK 버전 대상 지정

다른 SDK 버전을 대상으로 기존 프로젝트를 수정 하려면에서 다음 줄을 수정 ```package.json```:

```
"@microsoft/windows-admin-center-sdk": "latest",
```
이 예제에서는 대체 ```latest``` 원하는 SDK 버전을 사용 하 여 즉, ```insider```:

```
"@microsoft/windows-admin-center-sdk": "insider",
```

그런 다음 ```npm install``` 프로젝트 전체에서 참조를 업데이트 합니다.