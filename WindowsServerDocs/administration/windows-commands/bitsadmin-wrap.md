---
title: bitsadmin wrap
description: Bitsadmin 줄 바꿈에 대 한 Windows 명령 항목으로, 명령 창의 가장 오른쪽 가장자리를 벗어나 확장 되는 출력 텍스트 줄을 다음 줄로 래핑합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 14e57522-539d-4621-ad15-09f7a44ccab7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 009a0452f44c4944ae110ca6b9e0570793c32a72
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80848756"
---
# <a name="bitsadmin-wrap"></a>bitsadmin wrap

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

명령 창의 가장 오른쪽 가장자리를 벗어나 확장 되는 출력 텍스트 줄을 다음 줄로 래핑합니다.

## <a name="syntax"></a>구문

```
bitsadmin /Wrap Job
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|-------|--------|
|작업|작업의 표시 이름 또는 GUID|

## <a name="remarks"></a>주의

다른 스위치 앞에를 지정 합니다. 기본적으로 [bitsadmin 모니터](bitsadmin-monitor.md) 스위치를 제외한 모든 스위치는 출력을 래핑합니다.

## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예제에서는 이름이 *Mydownloadjob* 인 작업에 대 한 정보를 검색 하 고 출력을 래핑합니다.

```
C:\>bitsadmin /Wrap /Info myDownloadJob /verbose
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
