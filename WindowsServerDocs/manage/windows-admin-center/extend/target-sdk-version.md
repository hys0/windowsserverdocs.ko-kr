---
title: 다른 버전의 Windows 관리 센터 SDK를 대상으로 합니다.
description: 다른 버전의 Windows 관리 센터 SDK를 대상으로 합니다 (Project Honolulu).
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 0d3b7af5229f7b8487aa9f04eaf0d1756d8c02f4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71356973"
---
# <a name="target-a-different-version-of-the-windows-admin-center-sdk"></a>다른 버전의 Windows 관리 센터 SDK를 대상으로 합니다.

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

SDK 변경 및 플랫폼 변경으로 확장을 최신 상태로 유지 하는 것은 쉽습니다.  [NPM 태그](https://www.npmjs.com/package/@microsoft/windows-admin-center-sdk) 를 사용 하 여 새 기능의 릴리스를 SDK 버전으로 구성 합니다.

선택할 수 있는 SDK 버전에는 세 가지가 있습니다.

* ```latest``` –이 SDK 패키지는 Windows 관리 센터의 현재 GA 릴리스에 맞춥니다.
* ```insider``` –이 SDK 패키지는 Windows 관리 센터의 현재 미리 보기 릴리스와 맞춥니다 (Windows Server Insider Preview에서 사용 가능).
* ```next``` –이 SDK 패키지에 최신 기능이 포함 되어 있습니다.

> [!NOTE]
> 다운로드할 수 있는 다른 [버전](https://aka.ms/WACDownloadPage) 의 Windows 관리 센터에 대해 자세히 알아보세요.

## <a name="targeting-sdk-version-on-a-new-project"></a>새 프로젝트에서 SDK 버전을 대상으로 지정

새 확장을 만들 때 ```--version``` 매개 변수를 포함 하 여 다른 버전의 SDK를 대상으로 지정할 수 있습니다.

```
wac create --company "{!Company Name}" --tool "{!Tool Name}" --version {!version}
```

| 값 | 설명 | 예제 |
| ----- | ----------- | ------- |
| ```{!Company Name}``` | 회사 이름 (공백 포함) | ```Contoso Inc``` |
| ```{!Tool Name}``` | 도구 이름 (공백 포함) | ```Manage Foo Works``` |
| ```{!version}``` | SDK 버전 | ```latest``` |

@No__t-0을 대상으로 하는 새 확장을 만드는 예제는 다음과 같습니다.

```
wac create --company "Contoso Inc" --tool "Manage Foo Works" --version insider
```

## <a name="targeting-sdk-version-on-an-existing-project"></a>기존 프로젝트에서 SDK 버전을 대상으로 지정

다른 SDK 버전을 대상으로 하는 기존 프로젝트를 수정 하려면 ```package.json```에서 다음 줄을 수정 합니다.

```
"@microsoft/windows-admin-center-sdk": "latest",
```
이 예제에서는 ```latest```을 원하는 SDK 버전 (예: ```insider```)으로 바꿉니다.

```
"@microsoft/windows-admin-center-sdk": "insider",
```

그런 다음 ```npm install```을 실행 하 여 프로젝트 전체에서 참조를 업데이트 합니다.