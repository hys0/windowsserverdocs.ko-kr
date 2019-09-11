---
title: Windows 관리 센터의 문자열 및 지역화
description: Windows 관리 센터 SDK (Project Honolulu)에서 지역화를 위한 문자열을 준비 하는 방법에 대해 알아봅니다.
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 06/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 4cc624dcc985f13f97b7bbc767de6bbb9c72217a
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70869706"
---
# <a name="strings-and-localization-in-windows-admin-center"></a>Windows 관리 센터의 문자열 및 지역화 #

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

Windows 관리 센터 확장 SDK에 대해 자세히 살펴보고 문자열과 지역화에 대해 알아봅니다.

프레젠테이션 계층에서 렌더링 되는 모든 문자열에 대 한 지역화를 사용 하도록 설정 하려면/sv/sv/sv/sv\sources에서 문자열. resjson 파일을 활용 합니다 .이는 이미 설정 되어 있습니다. 확장에 새 문자열을 추가 해야 하는 경우이 resjson 파일에 새 항목으로 추가 합니다. 기존 구조는 다음 형식을 따릅니다.

``` ts
"<YourExtensionName>_<Component>_<Accessor>": "Your string value goes here.",
```

문자열에 대해 원하는 형식을 사용할 수 있지만 생성 프로세스 (resjson을 사용 하 고 사용 가능한 TypeScript 클래스를 출력 하는 프로세스)는 밑줄 (_)을 마침표 (.)로 변환 합니다.

예를 들어 다음과 같은 항목이 있습니다.
``` ts
"HelloWorld_cim_title": "CIM Component",
```
는 다음과 같은 접근자 구조를 생성 합니다.
``` ts
MsftSme.resourcesStrings<Strings>().HelloWorld.cim.title;
```

## <a name="add-other-languages-for-localization"></a>지역화를 위한 다른 언어 추가 ## 

다른 언어에 대 한 지역화의 경우 각 언어에 대해 문자열. resjson 파일을 만들어야 합니다. 이러한 파일은에 ```\loc\output\{!ExtensionName}\{!LanguageFolder}\strings.resjson```배치 해야 합니다. 해당 폴더에 사용 가능한 언어는 다음과 같습니다.

| 언어      | Folder      |
| ------------- |-------------|
| Čeština | cs-CZ |
| Deutsch | de-DE |
| 영어 | ko-KR |
| Español | es-ES |
| Français | fr-FR | 
| Magyar | hu-HU | 
| Italiano | it-IT |
| 日本語 | ja-JP | 
| 한국어 | ko-KR | 
| Nederlands | nl-NL |
| Polski | pl-PL |
| Português(브라질) | pt-BR |
| Português(포르투갈) | pt-PT |
| Русский | ru-RU |
| Svenska | sv-SE |
| Türkçe    | tr-TR |
| 中文(简体) | zh-CN |
| 中文(繁體) | zh-TW |
> [!NOTE]
> 파일 구조 요구가 loc/output 내에서 다른 경우 gulpfile에 있는 gulp 작업 ' localeOffset 지역화 됨 '의 작업을 조정 해야 합니다. 이 오프셋은 문자열을 검색 하기 시작 하는 loc 폴더의 깊이입니다. resjson 파일.

각 문자열. resjson 파일은이 가이드의 맨 위에서 설명한 것과 같은 방식으로 형식이 지정 됩니다. 

예를 들어 Español에 대 한 지역화를 포함 하려면에 ```\loc\output\HelloWorld\es-ES\strings.resjson```이 항목이 포함 되어 있습니다. 
```json
"HelloWorld_cim_title": "CIM Componente",
```
지역화 된 문자열을 추가할 때마다 gulp 생성을 다시 실행 하 여 표시 되도록 해야 합니다. 실행:
``` cmd
gulp generate 
```

문자열이 생성 되었는지 확인 하려면로 ```\src\app\assets\strings\{!LanguageFolder}\strings.resjson```이동 합니다. 새로 추가 된 항목이이 파일에 표시 됩니다.
이제 Windows 관리 센터에서 언어 옵션을 전환 하는 경우 확장에서 지역화 된 문자열을 볼 수 있습니다. 
