---
title: 루트 탐색 동작 수정
description: 솔루션 확장 개발 Windows 관리 센터 SDK (Project Honolulu)-루트 탐색 동작 수정
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 08/07/2018
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 78c94f3ea13f54ac31f9de9dd60873b93eba2c17
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71385281"
---
# <a name="modify-root-navigation-behavior-for-a-solution-extension"></a>솔루션 확장에 대 한 루트 탐색 동작 수정

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

이 가이드에서는 다양 한 연결 목록 동작을 포함 하도록 솔루션에 대 한 루트 탐색 동작을 수정 하는 방법 및 도구 목록을 숨기 거 나 표시 하는 방법에 대해 설명 합니다.

## <a name="modifying-root-navigation-behavior"></a>루트 탐색 동작 수정

{Extension root} \src에서 .manifest 파일을 열고 "rootNavigationBehavior" 속성을 찾습니다. 이 속성에는 "connections" 또는 "path"의 두 가지 유효한 값이 있습니다. "연결" 동작은 설명서의 뒷부분에 자세히 설명 되어 있습니다.

### <a name="setting-path-as-a-rootnavigationbehavior"></a>RootNavigationBehavior로 경로 설정

@No__t-0 값을 ```path```로 설정한 다음 ```requirements``` 속성을 삭제 하 고 ```path``` 속성은 빈 문자열로 둡니다. 솔루션 확장을 빌드하는 데 필요한 최소한의 구성을 완료 했습니다. 파일을 저장 하 고 gulp gulp를 도구와 같은 방식으로 > 사용 하 고 확장을 로컬 Windows 관리 센터 확장으로 로드 합니다.

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

이러한 종류의 구조를 사용 하 여 빌드된 도구는 로드에 대 한 연결이 필요 하지 않지만 노드 연결 기능을 사용할 수 없습니다.

### <a name="setting-connections-as-a-rootnavigationbehavior"></a>RootNavigationBehavior로 연결 설정

@No__t-0 속성을 ```connections```로 설정 하면 연결 된 노드 (항상 일종의 서버)가 연결 되 고 연결 상태를 확인 하는 Windows 관리 센터 셸에 표시 됩니다. 이를 사용 하는 경우 연결을 확인 하는 2 단계가 있습니다. 1) Windows 관리 센터는 자격 증명을 사용 하 여 노드에 로그인을 시도 하 고 (원격 PowerShell 세션을 설정 하는 경우) 2) 사용자가 제공 하는 PowerShell 스크립트를 실행 하 여 노드가 연결 가능 상태 인지 확인 합니다.

연결이 있는 유효한 솔루션 정의는 다음과 같습니다.

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

RootNavigationBehavior를 "연결"로 설정 하면 매니페스트에서 연결 정의를 작성 해야 합니다. 여기에는 "헤더" 속성이 포함 됩니다 (사용자가 메뉴에서 선택할 때 솔루션 헤더에 표시 하는 데 사용 됨). connectionTypes array (이는 솔루션에서 사용 되는 connectionTypes를 지정 합니다. 자세한 내용은 connectionProvider 설명서를 참조 하세요.)

## <a name="enabling-and-disabling-the-tools-menu"></a>도구 메뉴 사용 및 사용 안 함 ##

솔루션 정의에서 사용할 수 있는 다른 속성은 "tools" 속성입니다. 그러면 도구 메뉴가 표시 되 고 로드 되는 도구가 표시 됩니다. Windows 관리 센터를 사용 하도록 설정 하면 왼쪽 도구 메뉴가 렌더링 됩니다. DefaultTool을 사용 하면 적절 한 리소스를 로드 하기 위해 매니페스트에 도구 진입점을 추가 해야 합니다. "DefaultTool"의 값은 매니페스트에 정의 된 도구의 "이름" 속성 이어야 합니다.
