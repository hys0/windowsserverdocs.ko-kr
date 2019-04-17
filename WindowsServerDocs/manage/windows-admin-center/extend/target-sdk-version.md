---
title: Windows Admin Center SDK의 다른 버전을 대상으로 지정
description: Windows Admin Center SDK (Project Honolulu)의 다른 버전을 대상으로 지정
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 47ae669e517f963762ee6267594e18f3413a72ff
ms.sourcegitcommit: be0144eb59daf3269bebea93cb1c467d67e2d2f1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/20/2018
ms.locfileid: "4081040"
---
# Windows Admin Center SDK의 다른 버전을 대상으로 지정

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

확장 SDK와 변경 내용이 플랫폼을 사용 하 여 최신 상태로 유지 하는 것은 쉽습니다.  [NPM 태그](https://www.npmjs.com/package/@microsoft/windows-admin-center-sdk) SDK 버전으로의 새로운 기능 릴리스 구성에 사용 합니다.

세 가지 SDK 버전에서 선택할 수 있습니다.

* ```latest``` -Windows Admin Center의 현재 GA 릴리스를 사용 하 여이 SDK 패키지 맞춥니다.
* ```insider``` –이 SDK 패키지에 맞춰 현재 미리 보기 릴리스의 Windows Admin Center (Windows Server Insider Preview에서 사용 가능)
* ```next``` -최신 기능을 포함 하는이 SDK 패키지

> [!NOTE]
> 여러 [버전](https://aka.ms/WACDownloadPage) 을 다운로드할 수 있는 Windows Admin Center에 대해 자세히 알아보세요.

## 새 프로젝트에 SDK 버전을 대상 으로합니다.

새 확장을 만드는 경우 포함할 수 있습니다는 ```--version``` 매개 변수를 다른 버전의 SDK 대상으로 지정 합니다.

```
wac create --company "{!Company Name}" --tool "{!Tool Name}" --version {!version}
```

| 값 | 설명 | 예 |
| ----- | ----------- | ------- |
| ```{!Company Name}``` | 회사 이름 (공백 포함) | ```Contoso Inc``` |
| ```{!Tool Name}``` | 사용자 도구 이름 (공백 포함) | ```Manage Foo Works``` |
| ```{!version}``` | SDK 버전 | ```latest``` |

다음은 새로운 확장 대상 만드는 예 ```insider```:

```
wac create --company "Contoso Inc" --tool "Manage Foo Works" --version insider
```

## 기존 프로젝트에서 SDK 버전을 대상 으로합니다.

다음 줄을 수정 다른 SDK 버전을 대상으로 기존 프로젝트를 수정 하려면 ```package.json```:

```
"@microsoft/windows-admin-center-sdk": "latest",
```
이 예제에서는 바꾸기 ```latest``` 원하는 SDK 버전, 즉 ```insider```:

```
"@microsoft/windows-admin-center-sdk": "insider",
```

그런 다음 ```npm install``` 프로젝트 전체에 대 한 참조를 업데이트 합니다.