---
title: bitsadmin setproxysettings
description: Windows 명령 항목에 대 한 **bitsadmin setproxysettings** -지정된 된 된 작업에 대 한 프록시 설정을 지정 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: be8edb1b-614e-4d0b-a8f8-64b4bde3e64b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a3503aab55f5650cb9283ce8a9f1a17359bfd48b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59825594"
---
# <a name="bitsadmin-setproxysettings"></a>bitsadmin setproxysettings



지정된 된 작업에 대 한 프록시 설정을 지정 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /SetProxySettings <Job> <Usage> [List] [Bypass]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|
|사용법|다음 값 중 하나입니다.</br>-미리-소유자의 Internet Explorer 기본값을 사용 합니다.</br>-NO_PROXY-프록시 서버를 사용 하지 마십시오.</br>-재정의-명시적 프록시 목록을 사용 하 고 바이패스 목록입니다. 프록시 및 프록시 무시 목록 수행 해야 합니다.</br>자동 감지-프록시 설정 자동 검색 합니다.|
|목록|때 사용 합니다 *사용량* 재정의 매개 변수는 설정-사용할 프록시 서버의 쉼표로 구분 된 목록을 포함 합니다.|
|사용 안 함|때 사용 되는 합니다 *사용* 재정의 매개 변수는 설정-공백으로 구분 된 목록이 호스트 이름 또는 IP 주소 또는 둘 다에는 전송에 프록시를 통해 라우팅될를 하지. 이 수  **\<로컬 >** 동일한 LAN에 있는 모든 서버를 가리키도록 합니다. NULL 값 또는 ""는 빈 프록시 무시 목록에 사용할 수 있습니다.|

## <a name="BKMK_examples"></a>예제

다음 예제에서는 명명 된 작업에 대 한 프록시 설정을 *myDownloadJob*합니다.

```
C:\>bitsadmin /SetProxySettings myDownloadJob PRECONFIG
```

일부의 예는 다음과 같습니다.

```
bitsadmin /setproxysettings myDownloadJob NO_PROXY
bitsadmin /setproxysettings myDownloadJob OVERRIDE proxy1:80 ""
bitsadmin /setproxysettings myDownloadJob OVERRIDE proxy1,proxy2,proxy3 NULL
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)