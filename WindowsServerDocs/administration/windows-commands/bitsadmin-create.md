---
title: bitsadmin create
description: 지정 된 표시 이름을 사용 하 여 전송 작업을 만드는 bitsadmin create 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9a8c53af-900b-4c24-9265-5b8b08213fac
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 728027eb4680805c1f9a2afc32d8d37a14239597
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718214"
---
# <a name="bitsadmin-create"></a>bitsadmin create

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

지정 된 표시 이름과 함께 전송 작업을 만듭니다.

> [!NOTE]
> **/Upload** 및 **/Upload-Reply** 매개 변수 형식은 BITS 1.2 및 이전 버전에서 지원 되지 않습니다.

## <a name="syntax"></a>구문

```
bitsadmin /create [type] displayname
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
| ------- | -------- |
| type | 작업에는 다음 세 가지 유형이 있습니다.<ul><li>**다운로드할지.** 서버에서 로컬 파일로 데이터를 전송 합니다.</li><li>**업로드할.** 로컬 파일에서 서버로 데이터를 전송 합니다.</li><li>**/Upload-Reply.** 로컬 파일에서 서버로 데이터를 전송 하 고 서버에서 회신 파일을 받습니다.</li></ul>이 매개 변수는 지정 되지 않은 경우 기본적으로 **/Download** 로 설정 됩니다. |
| displayname | 새로 만든된 작업에 할당 된 표시 이름입니다. |

## <a name="examples"></a>예

*Mydownloadjob*이라는 다운로드 작업을 만들려면 다음을 수행 합니다.

```
bitsadmin /create myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin resume 명령](bitsadmin-resume.md)

- [bitsadmin 명령](bitsadmin.md)
