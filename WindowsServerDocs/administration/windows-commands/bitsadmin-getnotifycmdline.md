---
title: bitsadmin getnotifycmdline
description: '**Bitsadmin getnotifycmdline** 에 대 한 Windows 명령 항목-작업에서 데이터 전송을 완료할 때 실행 되는 명령줄 명령을 검색 합니다.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 90fa33e6-aca5-4a23-82bd-19a9f13f8416
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b91d2c71ad4bedaac65e23041ca78a70ade99977
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381492"
---
# <a name="bitsadmin-getnotifycmdline"></a>bitsadmin getnotifycmdline

작업에서 데이터 전송을 완료할 때 실행할 명령줄 명령을 검색 합니다.

**BITS 1.2 및 이전 버전**: 지원되지 않습니다.

## <a name="syntax"></a>구문

```
bitsadmin /GetNotifyCmdLine <Job>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|

## <a name="BKMK_examples"></a>예와

다음 예제에서는 *Mydownloadjob* 이라는 작업이 완료 될 때 서비스에서 사용 하는 명령줄 명령을 검색 합니다.
```
C:\>bitsadmin /GetNotifyCmdLine myDownloadJob
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)