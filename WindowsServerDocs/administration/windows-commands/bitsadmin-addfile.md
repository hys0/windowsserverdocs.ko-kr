---
title: bitsadmin addfile
description: 지정 된 작업에 파일을 추가 하는 **bitsadmin addfile**에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1b31aa93-0364-465b-af36-754968825989
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 330e79eb2ba5a824cea54094f64ceb6f9cfd66b9
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850966"
---
# <a name="bitsadmin-addfile"></a>bitsadmin addfile

지정된 된 작업에 파일을 추가 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /AddFile <Job> <RemoteURL> <LocalName>
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| 작업 | 작업의 표시 이름 또는 GUID입니다. |
| RemoteURL | 서버에서 파일의 URL입니다. |
| LocalName | 로컬 컴퓨터에 있는 파일의 이름입니다. *LocalName* 파일에 절대 경로 포함 해야 합니다. |

## <a name="examples"></a><a name=BKMK_examples></a>예와

파일 작업을 추가 합니다. 추가 하려는 각 파일에 대 한이 호출을 반복 합니다. 여러 작업을 사용 하는 경우 *myDownloadJob* 해당 이름으로 바꿔야 *myDownloadJob* 작업을 고유 하 게 식별 하는 작업의 GUID를 가진 합니다.

```
C:\>bitsadmin /addfile myDownloadJob http://downloadsrv/10mb.zip c:\10mb.zip
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)&copy;