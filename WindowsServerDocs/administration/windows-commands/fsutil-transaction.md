---
ms.assetid: f2eefaaf-2817-4ac7-abac-d2b65fa971dc
title: Fsutil 트랜잭션
ms.prod: windows-server-threshold
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 93c981d077dbb027400a1eb2e2c662f72c14cc44
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59825214"
---
# <a name="fsutil-transaction"></a>Fsutil 트랜잭션
>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows 7, Windows 2008, Windows Vista

NTFS 트랜잭션을 관리합니다.

이 명령을 사용 하는 방법의 예제를 보려면 [예제](#BKMK_examples) 합니다.

## <a name="syntax"></a>구문

```
fsutil transaction [commit] <GUID>
fsutil transaction [fileinfo] <Filename>
fsutil transaction [list]
fsutil transaction [query] [{Files|All}] <GUID>
fsutil transaction [rollback] <GUID>

```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|-------------|---------------|
|커밋(commit)|성공적인 암시적 또는 명시적 지정 된 트랜잭션 끝을 표시 합니다.|
|<GUID>|트랜잭션을 나타내는 GUID 값을 지정 합니다.|
|fileinfo|지정된 된 파일에 대 한 트랜잭션 정보를 표시합니다.|
|<Filename>|전체 경로 파일 이름을 지정합니다.|
|목록|현재 실행 중인 트랜잭션을의 목록이 표시 됩니다.|
|쿼리|지정된 된 트랜잭션에 대 한 정보를 표시합니다.<br /><br />- **Fsutil 트랜잭션 쿼리 파일** 지정, 파일 정보에 지정된 된 트랜잭션에 대해서만 표시 됩니다.<br />- **Fsutil 트랜잭션 쿼리** 지정, 트랜잭션에 대 한 모든 정보가 표시 됩니다.|
|롤백|시작 부분에는 지정 된 트랜잭션을 롤백합니다.|

### <a name="remarks"></a>설명

-   트랜잭션 NTFS는 Windows Server 2008에서 도입 되었습니다.

### <a name="BKMK_examples"></a>예제
파일 c:\test.txt에 대 한 트랜잭션 정보를 표시 하려면 다음을 입력 합니다.

```
fsutil transaction fileinfo c:\test.txt  
```

### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)

[트랜잭션 NTFS](https://go.microsoft.com/fwlink/?LinkID=165402)


