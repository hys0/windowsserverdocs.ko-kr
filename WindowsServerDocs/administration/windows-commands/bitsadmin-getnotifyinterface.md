---
title: bitsadmin getnotifyinterface
description: '**Bitsadmin getnotifyinterface** 에 대 한 Windows 명령 항목-다른 프로그램에서 지정 된 작업에 대해 COM 콜백 인터페이스를 등록 했는지 여부를 확인 합니다.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 40bf9dd8-b167-406a-80a6-a5a6f1b8cf7f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 826e13cf8a3e54935ceb5a72ff82647cacfc3be5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381470"
---
# <a name="bitsadmin-getnotifyinterface"></a>bitsadmin getnotifyinterface

다른 프로그램에서 지정 된 작업에 대 한 COM 콜백 인터페이스 (알림 인터페이스)를 등록 했는지 여부를 확인 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /GetNotifyInterface <Job>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|

## <a name="remarks"></a>설명

등록 또는 등록 취소를 표시 합니다.

> [!NOTE]
> 콜백 인터페이스를 등록 한 프로그램은 확인할 수 없습니다.

## <a name="BKMK_examples"></a>예와

다음 예제에서는 명명 된 작업에 대 한 알림 인터페이스를 검색 *Mydownloadjob*합니다.
```
C:\>bitsadmin /GetNotifyInterface myDownloadJob
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)