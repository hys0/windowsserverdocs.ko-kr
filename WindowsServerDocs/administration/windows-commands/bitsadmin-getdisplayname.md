---
title: bitsadmin getdisplayname
description: '**Bitsadmin getdisplayname** 에 대 한 Windows 명령 항목-지정 된 작업의 표시 이름을 검색 합니다.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e5c0e76c-4cc6-42d8-ac30-30bf3dc11b9b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 229bd245f9e810fc6aeb856bbfba253b9ab8a9f0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381633"
---
# <a name="bitsadmin-getdisplayname"></a>bitsadmin getdisplayname



지정 된 작업의 표시 이름을 검색 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /GetDisplayName <Job>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|

## <a name="BKMK_examples"></a>예와

다음 예제에서는 명명 된 작업에 대 한 표시 이름을 검색 *Mydownloadjob*합니다.
```
C:\>bitsadmin /GetDisplayName myDownloadJob
```
추가 참조

[명령줄 구문 키](command-line-syntax-key.md)