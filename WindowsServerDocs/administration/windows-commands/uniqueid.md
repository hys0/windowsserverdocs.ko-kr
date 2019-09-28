---
title: uniqueid
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 64235a4a-b91c-46da-b9b0-68ee90571c2a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 64f097766daa4c87ec84f42dd53f49792a160bb9
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71363913"
---
# <a name="uniqueid"></a>uniqueid



포커스가 있는 디스크에 대 한 GPT (GUID 파티션 테이블) 식별자 또는 MBR (마스터 부트 레코드) 서명을 표시 하거나 설정 합니다.

> [!IMPORTANT]
> 이 DiskPart 명령을 Windows Vista의 모든 버전에서 사용할 수 없는 경우

## <a name="syntax"></a>구문

```
uniqueid disk [id={<dword> | <GUID>}] [noerr]
```

## <a name="parameters"></a>매개 변수

|  매개 변수   |                                                                                             설명                                                                                              |
|--------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id = {\<dword > |                                                                                               <GUID>}                                                                                                |
|    noerr     | 스크립팅 전용입니다. 오류가 발생 하면 오류가 발생 하지 않은 경우에 따라 명령을 처리 하도록 DiskPart 계속 합니다. 이 매개 변수를 크기는 오류 코드를 수행 합니다. |

## <a name="remarks"></a>설명

-   이 명령은 기본 및 동적 디스크에 대해 작동 합니다.
-   이 명령을 성공적으로 디스크를 선택 해야 합니다. 사용 된 **디스크 선택** 디스크를 선택 하 고 포커스를 이동 하는 명령입니다.

## <a name="BKMK_examples"></a>예와

포커스가 있는 MBR 디스크의 서명을 표시 하려면 다음을 입력 합니다.
```
uniqueid disk
```
5f1b2c36에 포커스가 있는 MBR 디스크의 서명을 설정 하려면 다음을 입력 합니다.
```
uniqueid disk id=5f1b2c36
```
Baf784e7-6bbd-4cfb-aaac-e86c96e166ee에 포커스가 있는 GPT 디스크의 식별자를 설정 하려면 다음을 입력 합니다.
```
uniqueid disk id=baf784e7-6bbd-4cfb-aaac-e86c96e166ee
```

#### <a name="additional-references"></a>추가 참조

