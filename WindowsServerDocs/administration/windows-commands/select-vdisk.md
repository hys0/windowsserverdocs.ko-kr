---
title: vdisk 선택
description: '* * * *에 대 한 참조 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8808872a-3523-4205-a6c6-83fa738ee37a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 23741d9211ebdf98ac198af2ae1c562724a1955b
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83821083"
---
# <a name="select-vdisk"></a>vdisk 선택

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

지정 된 가상 하드 디스크 VHD를 선택 하 \( \) 고 포커스를 이동 합니다.

> [!NOTE]
> 이 명령은 Windows 7과 Windows Server 2008 r 2에 적용 됩니다.

## <a name="syntax"></a>구문

```
select vdisk file=<full path> [noerr]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|-------|--------|
|파일과\=<full path>|기존 VHD 파일의 전체 경로 파일 이름을 지정합니다.|
|noerr|스크립팅에 사용 합니다. 오류가 발생 하면 오류가 발생 하지 않은 경우에 따라 명령을 처리 하도록 DiskPart 계속 합니다. 이 매개 변수를 크기는 오류 코드를 수행 합니다.|

## <a name="examples"></a>예
포커스를 Test.vhd 라는 VHD에를 입력 합니다.

```
select vdisk file=c:\test\test.vhd
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

-   [연결 vdisk](attach-vdisk.md)

-   [compact vdisk](compact-vdisk.md)



-   [Vdisk를 분리 합니다.](detach-vdisk.md)

-   [세부 정보 vdisk](detail-vdisk.md)

-   [vdisk 확장](expand-vdisk.md)

-   [Vdisk를 병합 합니다.](merge-vdisk.md)

-   [list_1](list_1.md)


