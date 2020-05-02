---
title: wbadmin delete 카탈로그
description: 로컬 컴퓨터에 저장 된 백업 카탈로그를 삭제 하는 wbadmin delete catalog에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d3041407-4577-4716-a39f-2c8ab48818d1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 73f6f44fb343d3347d18cf2c86913aea59613e07
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720207"
---
# <a name="wbadmin-delete-catalog"></a>wbadmin delete 카탈로그



로컬 컴퓨터에 저장 된 백업 카탈로그를 삭제 합니다. 백업 카탈로그에 손상 된 경우를 사용 하 여 복원할 수 없습니다이 명령을 사용 하 여 **wbadmin 복원 카탈로그**합니다.

이 하위 명령으로 백업 카탈로그를 삭제 하려면의 구성원 이어야는 **백업 운영자** 그룹 또는 **관리자** 그룹 또는 사용자 받아야 적절 한 권한을 위임 합니다. 또한 실행 해야 **wbadmin** 상승된 된 명령 프롬프트에서. (관리자 권한 명령 프롬프트를 열려면 **명령 프롬프트**를 마우스 오른쪽 단추로 클릭 한 다음 **관리자 권한으로 실행**을 클릭 합니다.)

## <a name="syntax"></a>구문

```
wbadmin delete catalog
[-quiet]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|-quiet|사용자에 게 하위 명령 프롬프트 없이 실행 됩니다.|

## <a name="remarks"></a>설명

컴퓨터에 대 한 백업 카탈로그를 삭제 하면 Windows Server 백업 스냅인을 사용 하 여 해당 컴퓨터에서 만든 백업에 액세스할 수 없습니다. 이 경우 다른 백업 위치에 액세스할 수 있는 경우 사용 하 여 **wbadmin 복원 카탈로그** 해당 위치에서 백업 카탈로그를 복원 하려면. 백업 카탈로그를 삭제 한 후에 새 백업을 만들어야 합니다.

## <a name="additional-references"></a>추가 참조

-   - [명령줄 구문 키](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   [WBCatalog 제거](https://technet.microsoft.com/library/jj902445.aspx)