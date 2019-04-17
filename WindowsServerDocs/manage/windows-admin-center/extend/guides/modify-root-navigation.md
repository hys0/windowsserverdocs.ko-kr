---
title: 루트 탐색 동작을 수정
description: Windows Admin Center SDK (Project Honolulu) 솔루션 확장 개발-루트 탐색 동작을 수정
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 08/07/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 4a5cba228aa3a0afed99c0d853c3720a5b46f650
ms.sourcegitcommit: 546229d6b5fa7e16f725c6c35f4dcc272711b811
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/18/2018
ms.locfileid: "4905043"
---
# 솔루션 확장에 대 한 루트 탐색 동작을 수정

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

이 가이드에서는에서는 숨기 거 나 도구 목록을 표시 하는 방법 뿐만 아니라 다른 연결 목록 동작 솔루션에 대 한 루트 탐색 동작을 수정 하는 방법을 알아봅니다.

## 루트 탐색 동작을 수정

{확장 루트} \src에서 manifest.json 파일을 열고 "rootNavigationBehavior" 속성을 찾습니다. 이 속성은 두 가지 유효한 값: "연결" 또는 "path". "연결" 동작 설명서 뒷부분에서 자세히 설명 됩니다.

### 경로 rootNavigationBehavior로 설정

값을 설정 ```rootNavigationBehavior``` 를 ```path```, 후 삭제는 ```requirements``` 속성과 나가기는 ```path``` 속성을 빈 문자열로 합니다. 솔루션 확장을 빌드하는 데 필요한 최소한의 구성을 완료 합니다. 파일을 저장 하 고 gulp 빌드 gulp 역할을 하는 도구 및 다음 사이드 로드 확장 로컬 Windows Admin Center 확장-> 합니다.

유효한 매니페스트 진입점 배열은 다음과 같습니다.
```
    "entryPoints": [
        {
          "entryPointType": "solution",
          "name": "main",
          "urlName": "testsln",
          "displayName": "resources:strings:displayName",
          "description": "resources:strings:description",
          "icon": "sme-icon:icon-win-powerShell",
          "path": "",
          "rootNavigationBehavior": "path"
        }
    ],
```

이러한 종류의 구조를 사용 하 여 빌드된 도구는 필요 하지 않음 연결을 로드 하려면 있지만 하거나 노드 연결 기능을 사용할 수 없습니다.

### rootNavigationBehavior로 연결 설정

설정 하는 경우는 ```rootNavigationBehavior``` 속성을 ```connections```, 지시 Windows Admin Center 셸 것을 연결 해야 하는 연결 된 노드 (항상 일부 유형의 서버) 및 연결 상태를 확인 합니다. 이 경우는 2 단계 연결을 확인 하는 데입니다. 1) Windows Admin Center 노드 (에 대 한 원격 PowerShell 세션을 설정), 자격 증명으로 로그인 하려고 시도 하며 2)이 노드가 가능한 상태 이면를 식별 하기 위해 제공 PowerShell 스크립트를 실행 됩니다.

연결을 사용 하 여 유효한 솔루션 정의 다음과 같습니다.

``` json
        {
          "entryPointType": "solution",
          "name": "example",
          "urlName": "solutionexample",
          "displayName": "resources:strings:displayName",
          "description": "resources:strings:description",
          "icon": "sme-icon:icon-win-powerShell",
          "rootNavigationBehavior": "connections",
          "connections": {
            "header": "resources:strings:connectionsListHeader",
            "connectionTypes": [
                "msft.sme.connection-type.example"
                ]
            },
            "tools": {
                "enabled": false,
                "defaultTool": "solution"
            }
        },
```

rootNavigationBehavior "연결"로 설정 된 경우 매니페스트에 연결 정의 구축 해야 합니다. 이때 (사용할 메뉴에서 사용자가 선택할 때 솔루션 헤더에 표시할) "헤더" 속성, connectionTypes 배열 (이 지정 어떤 connectionTypes 솔루션에서 사용 됩니다. 자세한 connectionProvider 설명서.).

## 설정 및 해제 도구 메뉴 ##

솔루션 정의에 사용할 수 있는 다른 속성의 "도구" 속성이입니다. 이 로드 되는 도구 뿐만 아니라 도구 메뉴 표시는 경우 결정 됩니다. 사용 하면 Windows Admin Center 왼쪽 도구 메뉴를 렌더링 합니다. DefaultTool를 사용 하 여 필요할 때 적절 한 리소스를 로드 하기 위해 매니페스트 진입점을 도구를 추가 합니다. "DefaultTool"의 값은 매니페스트에 정의 된 대로 "name" 속성의 도구 수 있어야 합니다.
