---
title: lpr
description: 인쇄 준비 과정에서 LPD (Line printer Daemon) 서비스를 실행 하는 컴퓨터 또는 프린터 공유 장치에 파일을 전송 하는 lpr 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: afc8790b-8b52-45c4-acdf-be0ffa9da534
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d11b72ee807869613505052cfb51e80a89a80d70
ms.sourcegitcommit: 29bc8740e5a8b1ba8f73b10ba4d08afdf07438b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/30/2020
ms.locfileid: "84223030"
---
# <a name="lpr"></a>lpr

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

인쇄 준비 과정에서 LPD (Line printer Daemon) 서비스를 실행 하는 컴퓨터 또는 프린터 공유 장치에 파일을 보냅니다.

## <a name="syntax"></a>구문

```
lpr [-S <servername>] -P <printername> [-C <bannercontent>] [-J <jobname>] [-o | -o l] [-x] [-d] <filename>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| -S`<servername>` | 컴퓨터 또는 디바이스를 표시 하려는 상태와 함께 LPD 인쇄 큐를 호스팅하는 공유 프린터 이름 또는 IP 주소) (으로 지정 합니다.  이 매개 변수는 필수 이며 대문자 여야 합니다. |
| -P`<printername> `| 표시 하려는 상태와 함께 인쇄 큐에 대 한 프린터 이름을 사용 하 여 지정 합니다. **프린터 이름을 찾으려면 프린터 폴더를** 엽니다. 이 매개 변수는 필수 이며 대문자 여야 합니다. |
| -C`<bannercontent>` | 인쇄 작업의 배너 페이지에 인쇄 하려면 콘텐츠를 지정 합니다. 이 매개 변수를 포함 하지 않으면 인쇄 작업이 전송 된 컴퓨터의 이름이 배너 페이지에 나타납니다. 이 매개 변수는 대문자 여야 합니다. |
| -J`<jobname>` | 배너 페이지에 인쇄 되는 인쇄 작업 이름을 지정 합니다. 이 매개 변수를 포함 하지 않는 경우 인쇄 되는 파일의 이름이 배너 페이지에 나타납니다. 이 매개 변수는 대문자 여야 합니다. |
| `[-o | -o l]` | 인쇄 하려는 파일의 유형을 지정 합니다. 매개 변수 **-o** 텍스트 파일을 인쇄 하도록 지정 합니다. 매개 변수 **-o l** 은 이진 파일 (예: PostScript 파일)을 인쇄 하도록 지정 합니다. |
| -d | 데이터 파일 제어 파일 전에 보내야 한다고 지정 합니다. 프린터에 필요한 데이터 파일을 먼저 보내도록 하는 경우이 매개 변수를 사용 합니다. 자세한 내용은 프린터 설명서를 참조 합니다. |
| -X | 4_u1 4.1을 포함 하 여 Microsystems에 대 한 릴리스를 위해 **lpr** 명령이 Sun 운영 체제 (sunos)와 호환 되어야 함을 지정 합니다. |
| `<filename>` | 인쇄할 파일 이름을 사용 하 여 지정 합니다. 이 매개 변수는 필수입니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

### <a name="examples"></a>예

*에서 10.0.0.45*에서 LPD 호스트의 *Laserprinter1* 프린터 큐에 *문서 .txt* 텍스트 파일을 인쇄 하려면 다음을 입력 합니다.

```
lpr -S 10.0.0.45 -P Laserprinter1 -o Document.txt
```

*에서 10.0.0.45*에서 LPD 호스트의 *Laserprinter1* 프린터 큐에 PostScript_file를 인쇄 하려면 다음을 입력 *합니다* .

```
lpr -S 10.0.0.45 -P Laserprinter1 -o l PostScript_file.ps
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [인쇄 명령 참조](print-command-reference.md)
