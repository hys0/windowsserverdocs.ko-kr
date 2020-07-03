---
title: bitsadmin addfile
description: 지정 된 작업에 파일을 추가 하는 bitsadmin addfile 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1b31aa93-0364-465b-af36-754968825989
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 817a6d3af81d88e571db17c3f57dc129130b2783
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85927101"
---
# <a name="bitsadmin-addfile"></a>bitsadmin addfile

지정된 된 작업에 파일을 추가 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /addfile <job> <remoteURL> <localname>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |
| remoteURL | 서버에서 파일의 URL입니다. |
| localname | 로컬 컴퓨터에 있는 파일의 이름입니다. *Localname* 은 파일에 대 한 절대 경로를 포함 해야 합니다. |

## <a name="examples"></a>예

작업에 파일을 추가 하려면 다음을 수행 합니다.

```
bitsadmin /addfile myDownloadJob http://downloadsrv/10mb.zip c:\10mb.zip
```

추가할 각 파일에 대해이 호출을 반복 합니다. 여러 작업을 사용 하는 경우 *myDownloadJob* 해당 이름으로 바꿔야 *myDownloadJob* 작업을 고유 하 게 식별 하는 작업의 GUID를 가진 합니다.

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
