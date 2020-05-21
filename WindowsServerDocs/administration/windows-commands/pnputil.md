---
title: pnputil
description: Pnputil 유틸리티를 사용 하 여 드라이버 저장소를 관리 하는 방법을 알아봅니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fab686b8-09d3-4f6c-afa2-630e6036f44c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 4c6bcb138e8bd7308c01c2c53fba83b69362298a
ms.sourcegitcommit: bf887504703337f8ad685d778124f65fe8c3dc13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/16/2020
ms.locfileid: "83436368"
---
# <a name="pnputil"></a>pnputil

Pnputil은 드라이버 저장소를 관리 하는 데 사용할 수 있는 명령줄 유틸리티입니다. Pnputil을 사용 하 여 드라이버 패키지를 추가 하 고 드라이버 패키지를 제거 하 고 저장소에 있는 드라이버 패키지를 나열할 수 있습니다.

## <a name="syntax"></a>구문

```
pnputil.exe [-f | -i] [ -? | -a | -d | -e ] <INF name>
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|지정하지 않을 경우|식별 된 INF 파일을 추가 하도록 지정 합니다.|
|-d|식별 된 INF 파일을 삭제 하도록 지정 합니다.|
|-E|모든 타사 INF 파일을 열거 하도록 지정 합니다.|
|-f|식별 된 INF 파일을 강제로 삭제 하도록 지정 합니다. **– I** 매개 변수와 함께 사용할 수 없습니다.|
|-i|식별 된 INF 파일을 설치 하도록 지정 합니다. 는 **-f** 매개 변수와 함께 사용할 수 없습니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|


## <a name="examples"></a>예

-   pnputil-a a:\usbcam\USBCAM. INF USBCAM에 지정 된 INF 파일을 추가 합니다. DEVICE.INF
-   perfmon.exe-a c l a c e r i d e \*
-   pnputil-i-a a:\usbcam\USBCAM. INF 지정 된 드라이버를 추가 하 고 설치 합니다.
-   pnputil – e는 모든 타사 드라이버를 열거 합니다.
-   pnputil-d oem0는 지정 된를 삭제 합니다.
-   pnputil-f-d oem0는 지정 된 INF 파일을 강제로 삭제 합니다.

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

[Popd](popd.md)