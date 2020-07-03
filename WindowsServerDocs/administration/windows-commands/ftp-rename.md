---
title: ftp rename
description: 원격 파일의 이름을 바꾸는 ftp 이름 바꾸기 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 977b7c95-6428-4980-80ec-79c3ae7e8c4d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f46caa4394be9edc80da018d88809a0dd6e91862
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85925733"
---
# <a name="ftp-rename"></a>ftp rename

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

원격 파일을 이름을 바꿉니다.

## <a name="syntax"></a>구문

```
rename <filename> <newfilename>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<filename>` | 이름을 바꿀 파일을 지정 합니다. |
| `<newfilename>` | 새 파일 이름을 지정합니다. |

### <a name="examples"></a>예

원격 파일의 이름을example1.txt*example.txt* 하려면 * *다음을 입력 합니다.

```
rename example.txt example1.txt
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [추가 FTP 지침](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
