---
ms.assetid: f2eefaaf-2817-4ac7-abac-d2b65fa971dc
title: Fsutil 트랜잭션
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: aa6692dbb8af1ec832650971c6723c060fc2cd56
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80844016"
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

#### <a name="parameters"></a>매개 변수

| 매개 변수  |                                                                                                                                                     설명                                                                                                                                                     |
|------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   커밋(commit)   |                                                                                                                      성공적인 암시적 또는 명시적 지정 된 트랜잭션 끝을 표시 합니다.                                                                                                                      |
|   <GUID>   |                                                                                                                               트랜잭션을 나타내는 GUID 값을 지정 합니다.                                                                                                                               |
|  fileinfo  |                                                                                                                              지정된 된 파일에 대 한 트랜잭션 정보를 표시합니다.                                                                                                                               |
| <Filename> |                                                                                                                                         전체 경로 파일 이름을 지정합니다.                                                                                                                                          |
|    list    |                                                                                                                                 현재 실행 중인 트랜잭션을의 목록이 표시 됩니다.                                                                                                                                  |
|   query    | 지정된 된 트랜잭션에 대 한 정보를 표시합니다.<p>- **Fsutil 트랜잭션 쿼리 파일** 지정, 파일 정보에 지정된 된 트랜잭션에 대해서만 표시 됩니다.<br />- **Fsutil 트랜잭션 쿼리** 지정, 트랜잭션에 대 한 모든 정보가 표시 됩니다. |
|  롤백  |                                                                                                                                시작 부분에는 지정 된 트랜잭션을 롤백합니다.                                                                                                                                 |

### <a name="remarks"></a>주의

-   트랜잭션 NTFS는 Windows Server 2008에서 도입 되었습니다.

### <a name="examples"></a><a name="BKMK_examples"></a>예와
C:\test.txt 파일에 대 한 트랜잭션 정보를 표시 하려면 다음을 입력 합니다.

```
fsutil transaction fileinfo c:\test.txt  
```

### <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md)

[Fsutil](Fsutil.md)

[트랜잭션 NTFS](https://go.microsoft.com/fwlink/?LinkID=165402)


