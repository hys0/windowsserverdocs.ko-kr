---
title: ftp put
description: FTP-put에 대 한 Windows 명령 항목
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 95cc1e3f-523d-4374-98b8-16e6c276b2ca vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/30/2020
ms.openlocfilehash: ecd579a313fe1cad1b8a5b4a622aaaec2d6a6d63
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80843136"
---
# <a name="ftp-put"></a>ftp: put

> 적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

현재 파일 전송 형식을 사용 하 여 원격 컴퓨터에 로컬 파일을 복사 합니다.
## <a name="syntax"></a>구문
```
put <LocalFile> [<remoteFile>]
```
#### <a name="parameters"></a>매개 변수

|    매개 변수     |                    설명                    |
|------------------|---------------------------------------------------|
|   `<LocalFile>`  |         복사할 로컬 파일을 지정 합니다.         |
| `[<remoteFile>]` | 원격 컴퓨터에서 사용 하 여 이름을 지정 합니다. |

## <a name="remarks"></a>주의
- **배치** 명령은 동일 합니다는 **보낼** 명령입니다.
- *Remotefile* 을 지정 하지 않으면 파일에 *localfile* 이름이 지정 됩니다.
  ## <a name="examples"></a><a name="BKMK_Examples"></a>예와
  로컬 파일 **test.txt** 를 복사 하 고 원격 컴퓨터에서 이름을 **test1** 로 설정 합니다.
  ```
  put test.txt test1.txt
  ```
  로컬 파일 **프로그램** 을 원격 컴퓨터에 복사 합니다.
  ```
  put program.exe
  ```
  ## <a name="additional-references"></a>추가 참조
- [ftp: ascii](ftp-ascii.md)
- [ftp: 이진](ftp-binary.md)
- - [명령줄 구문 키](command-line-syntax-key.md)
