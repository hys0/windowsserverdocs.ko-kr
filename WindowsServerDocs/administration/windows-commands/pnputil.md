---
title: pnputil
description: Pnputil.exe 유틸리티를 사용 하 여 드라이버 저장소를 관리 하는 방법을 알아봅니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fab686b8-09d3-4f6c-afa2-630e6036f44c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 5bde78d97be8def9f8594572869c34ef213db480
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59862544"
---
# <a name="pnputil"></a>pnputil

Pnputil.exe는 드라이버 저장소를 관리 하는 데 사용할 수 있는 명령줄 유틸리티입니다. Pnputil 드라이버 패키지를 추가 저장소에 있는 목록 드라이버 패키지 및 드라이버 패키지 제거를 사용할 수 있습니다.

## <a name="syntax"></a>구문

```
pnputil.exe [-f | -i] [ -? | -a | -d | -e ] <INF name>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|-A|식별된 된 INF 파일을 추가 하도록 지정 합니다.|
|-d|식별된 된 INF 파일을 삭제 하도록 지정 합니다.|
|-e|모든 타사 INF 파일을 열거 하도록 지정 합니다.|
|-f|식별된 된 INF 파일의 삭제를 적용 하도록 지정 합니다. 와 함께에서 사용할 수 없습니다는 **– i** 매개 변수입니다.|
|-i|식별된 된 INF 파일을 설치 하도록 지정 합니다. 와 함께에서 사용할 수 없습니다는 **-f** 매개 변수입니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|


## <a name="examples"></a>예

-   pnputil.exe a:\usbcam\USBCAM- INF는 USBCAM에 지정 된 INF 파일을 추가 합니다. INF
-   pnputil.exe c:\drivers-\*.inf c:\drivers\에서 모든 INF 파일에 추가
-   pnputil.exe-i-a a:\usbcam\USBCAM 합니다. INF 추가 하 고 지정된 된 드라이버를 설치 합니다.
-   pnputil.exe – e 모든 타사 드라이버를 열거합니다.
-   pnputil.exe-d oem0.inf 삭제를 지정 합니다.
-   pnputil.exe-f-d oem0.inf 강제로 지정된 된 INF 파일의 삭제를 수행합니다.

## <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)

[popd](popd.md)