---
title: 문자열 및 지역화를 Windows Admin Center
description: Windows Admin Center SDK (Project Honolulu)에 지역화 준비 문자열에 알아보기
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 06/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: f0671160bd790d80e35f6d6c1586a07969939070
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/12/2019
ms.locfileid: "9296735"
---
# 문자열 및 지역화를 Windows Admin Center #

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

Windows Admin Center 확장 SDK에 더 자세히 살펴보겠습니다 및 문자열 및 지역화에 설명 합니다.

/Src/resources/strings-strings.resjson 파일을 활용 프레젠테이션 계층에 렌더링 되는 모든 문자열을 지역화를 사용 하도록 설정 하려면 이미 설정 되어 있습니다. 새 문자열 확장을 추가 해야 할 때 추가이 resjson 파일에 새 항목으로 합니다. 기존 구조에는이 형식은 다음과 같습니다.

``` ts
"<YourExtensionName>_<Component>_<Accessor>": "Your string value goes here.",
```

원하는 모든 형식 문자열을 사용할 수 있지만 마침표 (.)에 밑줄 (_)를 변환 하는 생성 프로세스 (는 resjson를 사용 하 고 사용 가능한 TypeScript 클래스를 출력 하는 프로세스) 해야 합니다.

예를 들어이 항목:
``` ts
"HelloWorld_cim_title": "CIM Component",
```
다음 접근자 구조를 생성합니다.
``` ts
MsftSme.resourcesStrings<Strings>().HelloWorld.cim.title;
```

## 다른 언어로 지역화에 대 한 추가 ## 

다른 언어로 지역화를 위한 strings.resjson 파일 각 언어에 대해 작성 해야 합니다. 이러한 파일의 위치에 필요한 ```\loc\output\{!ExtensionName}\{!LanguageFolder}\strings.resjson```. 해당 폴더를 통해 사용할 수 있는 언어는:

| Language      | Folder      |
| ------------- |-------------|
| Čeština | cs-CZ |
| 독일어 | de-DE |
| 영어 | en-US |
| 스페인어 | es-ES |
| Français | fr-FR | 
| Magyar | hu-HU | 
| 이탈리아 | it-IT |
| 日本語 | ja-JP | 
| 한국어 | ko-KR | 
| 네덜란드 | nl-NL |
| Polski | pl-PL |
| Português (Brasil) | pt-BR |
| Português (포르투갈) | pt-PT |
| РУССКИЙ | ru-RU |
| Svenska | sv-SE |
| Türkçe    | tr-TR |
| 中文(简体) | zh-CN |
| 中文(繁體) | zh-TW |
> [!NOTE]
> 파일 구조 요구 위치/출력의 다른 내부 인 경우는 gulpfile.js에 있는 ' 생성 한 resjson-json-지역화 ' gulp 작업에 대 한 localeOffset 조정 해야 합니다. 이 오프셋 strings.resjson 파일에 대 한 검색 시작 위치 폴더에 깊이입니다.

각 strings.resjson 파일에이 가이드의 맨 위에 설명한 대로 동일한 방식으로 포맷 됩니다. 

예를 들어이 항목에서 포함할 스페인어에 대 한 지역화를 포함 하도록 ```\loc\output\HelloWorld\es-ES\strings.resjson```: 
```json
"HelloWorld_cim_title": "CIM Componente",
```
언제 든 지 지역화 된 문자열을 추가, gulp 생성 해야 표시 되도록 할 하기 위해 다시 실행 됩니다. 다음을 실행합니다.
``` cmd
gulp generate 
```

문자열을 생성 된 것을 확인 하려면로 이동 ```\src\app\assets\strings\{!LanguageFolder}\strings.resjson```. 새로 추가 된 항목을이 파일에 표시 됩니다.
이제 Windows Admin Center에서 언어 옵션으로 전환 하면 확장의 지역화 된 문자열을 볼 수 됩니다. 
