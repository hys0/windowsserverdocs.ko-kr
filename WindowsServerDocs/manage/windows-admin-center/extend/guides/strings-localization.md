---
title: 문자열과 Windows Admin Center 지역화
description: Windows Admin Center sdk (프로젝트 브라 티) 지역화를 위한 준비 문자열에 알아봅니다
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 06/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: fb328f86c98141a5a2a1c4fd05ec1d4c96a7bc5f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59845404"
---
# <a name="strings-and-localization-in-windows-admin-center"></a>문자열과 Windows Admin Center 지역화 #

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

자세한 Windows Admin Center 확장 SDK에 서 문자열 및 지역화에 설명 합니다.

프레젠테이션 계층을 활용 /src/resources/strings-에서 strings.resjson 파일에서 렌더링 되는 모든 문자열의 지역화를 사용 하도록 이미 설정 됩니다. 확장 프로그램에 새 문자열을 추가 해야 할 때 추가이 resjson 파일에 새 항목으로 합니다. 기존 구조에는이 형식은 다음과 같습니다.

``` ts
"<YourExtensionName>_<Component>_<Accessor>": "Your string value goes here.",
```

문자열에 대해 원하는 모든 형식을 사용할 수 있지만 (resjson를 사용 하 고 사용할 수 있는 TypeScript 클래스를 출력 하는 프로세스) 생성 프로세스를 마침표 (.)를 밑줄 (_)을 변환 한다는 주의 합니다.

이 항목의 예를 들어:
``` ts
"HelloWorld_cim_title": "CIM Component",
```
다음 접근자 구조를 생성 합니다.
``` ts
MsftSme.resourcesStrings<Strings>().HelloWorld.cim.title;
```
