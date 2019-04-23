---
title: assign
description: Windows 명령 항목에 대 한 **할당** -포커스가 있는 볼륨에 드라이브 문자 또는 탑재 지점을 할당 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 57912b73-622e-489b-b053-a369021ba8e1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0d830f9b1ec894c1bc136a99e7beb5703f840dc4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889294"
---
# <a name="assign"></a>assign

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

포커스가 있는 볼륨에 드라이브 문자 또는 탑재 지점을 할당합니다.

## <a name="syntax"></a>구문
```
assign [{letter=<d> | mount=<path>}] [noerr]
```
## <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|letter=<d>|볼륨에 할당 하려는 드라이브 문자입니다.|
|mount=<path>|볼륨에 할당 하려면 탑재 지점 경로입니다.<br /><br />이 명령을 사용 하는 방법에 대 한 지침은 [드라이브에 탑재 지점 폴더 경로 지정할](https://go.microsoft.com/fwlink/?LinkId=207059) (https://go.microsoft.com/fwlink/?LinkId=207059)합니다.|
|noerr|만 스크립팅 합니다. 오류가 발생 하면 오류가 발생 하지 않은 경우에 따라 명령을 처리 하도록 DiskPart 계속 합니다. 이 매개 변수를 크기는 오류 코드를 수행 합니다.|
## <a name="remarks"></a>설명
-   드라이브 문자 또는 탑재 지점을 지정 하지 않으면, 다음 사용 가능한 드라이브 문자가 할당 됩니다. 드라이브 문자 또는 탑재 지점을 사용 하 여에 이미 있으면 오류가 생성 됩니다.
-   Assign 명령을 사용 하 여 이동식 드라이브에 연결 된 드라이브 문자를 변경할 수 있습니다.
-   시스템 볼륨, 부팅 볼륨 또는 페이징 파일을 포함 하는 볼륨에 드라이브 문자를 할당할 수 없습니다. 또한 원래 장비 제조업체 (OEM) 파티션 또는 기본 데이터 파티션 이외의 모든 GUID 파티션 테이블 (gpt) 파티션 드라이브 문자를 할당할 수 없습니다.
-   이 작업을 수행 하려면 볼륨을 선택 해야 합니다. 사용 하 여는 **볼륨 선택** 볼륨을 선택 하 고 포커스를 이동 하는 명령입니다.
## <a name="BKMK_examples"></a>예제
E 포커스 볼륨에 할당 하려면 다음을 입력 합니다.
```
assign letter=e
```

