---
title: bitsadmin getnotifyflags
description: '**Bitsadmin getnotifyflags** 에 대 한 Windows 명령 항목-지정 된 작업에 대 한 알림 플래그를 검색 합니다.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d4657e6c-8959-4db7-a4af-e73d3f80ecf8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 56ee3a30050b6cc934b35bab24e9508911ea250e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381484"
---
# <a name="bitsadmin-getnotifyflags"></a>bitsadmin getnotifyflags



지정 된 작업에 대 한 알림 플래그를 검색 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /GetNotifyFlags <Job>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|

## <a name="remarks"></a>설명

작업은 다음 알림 플래그 중 하나 이상을 포함할 수 있습니다.

|-----|-----| | 0x001 | 작업의 모든 파일이 전송 되 면 이벤트를 생성 합니다. | | 0x002 | 오류가 발생 하면 이벤트를 생성 합니다. | | 0x004 | 알림을 사용 하지 않도록 설정 합니다. | | 0x008 | 작업을 수정 하거나 진행 중인 전송 작업을 수행할 때 이벤트를 생성 합니다. |

## <a name="BKMK_examples"></a>예와

다음 예제에서는 명명 된 작업에 대 한 알림 플래그를 검색 *Mydownloadjob*합니다.
```
C:\>bitsadmin /GetNotifyFlags myDownloadJob
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)