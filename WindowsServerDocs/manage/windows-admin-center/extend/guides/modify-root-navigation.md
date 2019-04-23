---
title: 루트 탐색 동작 수정
description: 솔루션 확장 Windows Admin Center SDK (프로젝트 브라 티) 개발-루트 탐색 동작을 수정
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 08/07/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 4a5cba228aa3a0afed99c0d853c3720a5b46f650
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59861734"
---
# <a name="modify-root-navigation-behavior-for-a-solution-extension"></a>솔루션 확장에 대 한 루트 탐색 동작을 수정

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

이 가이드에서 숨기 거 나 도구 목록을 표시 하는 방법 뿐만 아니라 다른 연결 목록 동작 솔루션에 대 한 루트 탐색 동작을 수정 하는 방법을 배웁니다.

## <a name="modifying-root-navigation-behavior"></a>루트 탐색 동작 수정

{0} 확장 루트} \src에서은 manifest.json 파일을 열고 "rootNavigationBehavior" 속성을 찾을 수 있습니다. 이 속성은 두 유효한 값: "연결" 또는 "경로"입니다. 설명서의 뒷부분에 나오는 "연결" 동작을 자세히 설명 되어 있습니다.

### <a name="setting-path-as-a-rootnavigationbehavior"></a>rootNavigationBehavior로 경로 설정

값을 설정 ```rootNavigationBehavior``` 를 ```path```, 한 다음 삭제를 ```requirements``` 속성 및 연결 해제를 ```path``` 속성을 빈 문자열로 합니다. 솔루션 확장 프로그램을 빌드하려면 최소한의 필요한 구성을 완료 했습니다. 파일을 저장 하 고 gulp 빌드에서 gulp 역할을 하는 도구 및 다음 쪽 확장을 로드 하면 로컬 Windows Admin Center 확장이-> 키를 누릅니다.

올바른 매니페스트 진입점 배열은 다음과 같습니다.
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

이 종류의 구조를 사용 하 여 빌드한 도구를 로드 하는 필요 하지 않습니다 연결할은 있으 나 없습니다 노드 연결 기능 중 하나입니다.

### <a name="setting-connections-as-a-rootnavigationbehavior"></a>rootNavigationBehavior 연결 설정

설정한 경우는 ```rootNavigationBehavior``` 속성을 ```connections```, 것에 연결 해야 하는 연결 된 노드 (항상 일부 형식의 서버) Windows Admin Center Shell에 지시 하 고 연결 상태를 확인 합니다. 이 사용 하 여 2 단계의 경우 연결 확인 1) Windows Admin Center (에 대 한 원격 PowerShell 세션을 설정), 자격 증명을 사용 하 여 노드에 로그인 하 여 하려고 시도가 및 노드 연결 가능한 상태 인지 확인 하 고 제공한 PowerShell 스크립트 실행 2).

연결을 사용 하 여 올바른 솔루션 정의 다음과 같이 표시 됩니다.

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

rootNavigationBehavior "연결"로 설정 된 경우 매니페스트에서 연결 정의 구축 해야 합니다. 여기에 "헤더" 속성 (사용할 메뉴에서 선택 하는 경우에 솔루션 머리글에 표시할), connectionTypes 배열 (지정는 connectionTypes 솔루션에 사용 됩니다. 자세한 내용은 connectionProvider 설명서에서 해당.).

## <a name="enabling-and-disabling-the-tools-menu"></a>설정 및 도구 메뉴를 사용 하지 않도록 설정 ##

솔루션 정의에서 사용할 수 있는 다른 속성은 "도구" 속성입니다. 이 로드 되는 도구 뿐만 아니라 도구 메뉴가 표시 될 경우에 따라 결정 됩니다. 사용 하도록 설정 하면 Windows Admin Center 왼쪽 도구 메뉴를 렌더링 합니다. DefaultTool를 사용 하 여 필요할 때 적절 한 리소스를 로드 하기 위해 매니페스트 진입점을 도구를 추가 합니다. 매니페스트에서 정의 된 대로 도구의 "name" 속성으로 "defaultTool"의 값이 필요 합니다.
