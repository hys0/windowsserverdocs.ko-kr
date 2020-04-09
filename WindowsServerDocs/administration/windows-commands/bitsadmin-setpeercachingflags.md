---
title: bitsadmin setpeercachingflags
description: Bitsadmin setpeercachingflags에 대 한 Windows 명령 항목-작업의 파일을 캐시 하 고 동료에 게 제공할 수 있는지 여부와 작업에서 피어에서 콘텐츠를 다운로드할 수 있는지 여부를 결정 하는 플래그를 설정 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3f54a127-fb68-49a5-b843-664ec833df67
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d19e4d14b47e4aa96e9ad9d4367e872350ad4d43
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849246"
---
# <a name="bitsadmin-setpeercachingflags"></a>bitsadmin setpeercachingflags

피어에서 콘텐츠는 작업의 파일을 캐시 하 고 동료에 게 제공 하 고 작업을 다운로드할 수 하는 경우를 결정 하는 플래그를 설정 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /SetPeerCachingFlags <Job> <value> 
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|
|값|값은 이진 표현에서 비트에 대 한 다음 해석 부호 없는 정수입니다.</br>1-작업에서 피어에서 콘텐츠를 다운로드할 수 있습니다.</br>2-작업의 파일을 캐시 하 고 동료에 게 제공할 수 있습니다.|

## <a name="examples"></a><a name=BKMK_examples></a>예와

명명 된 작업에 대 한 플래그를 설정 하는 다음 예제에서는 *myJob* 피어에서 콘텐츠를 다운로드할 수 있는 합니다.
```
C:\>bitsadmin / SetPeerCachingFlags myJob 1 
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)