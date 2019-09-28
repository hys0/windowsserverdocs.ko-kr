---
title: bitsadmin replaceremoteprefix
description: '**Bitsadmin replaceremoteprefix** 에 대 한 Windows 명령 항목-원격 URL이 *oldprefix* 로 시작 하는 작업의 모든 파일은 *newprefix*를 사용 하도록 변경 됩니다.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d0e0abb1-bdb4-4c74-abbc-16c809f5fd81
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ee896a337b571487797967d3ce0bf1f1b17e7507
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380803"
---
# <a name="bitsadmin-replaceremoteprefix"></a>bitsadmin replaceremoteprefix

해당 원격 URL로 시작 작업의 모든 파일 *OldPrefix* 를 사용 하도록 변경 *NewPrefix*합니다.

## <a name="syntax"></a>구문

```
bitsadmin /ReplaceRemotePrefix <Job> <OldPrefix> <NewPrefix
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|
|OldPrefix|기존 URL 접두사|
|NewPrefix|새 URL 접두사|

## <a name="examples"></a>예

다음 예에서는 원격 URL이- *2 http://stageserver* *@no__t*로 시작 하는 *mydownloadjob* 이라는 작업의 모든 파일을 변경 합니다.

```
C:\>bitsadmin /ReplaceRemotePrefix myDownloadJob http://stageserver http://prodserver
```

## <a name="additional-information"></a>추가 정보

[명령줄 구문 키](command-line-syntax-key.md)