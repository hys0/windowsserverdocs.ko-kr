---
title: lpr
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: afc8790b-8b52-45c4-acdf-be0ffa9da534 jpjofre
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e853933e368f181866963fdcbc1eca5b84bb8c09
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71374158"
---
# <a name="lpr"></a>lpr

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

인쇄 준비 과정에서 LPD (Line printer Daemon) 서비스를 실행 하는 컴퓨터 또는 프린터 공유 장치에 파일을 보냅니다.  

## <a name="syntax"></a>구문  
```  
lpr [-S <ServerName>] -P <printerName> [-C <BannerContent>] [-J <JobName>] [-o | "-o l"] [-x] [-d] <filename>  
```  
## <a name="parameters"></a>매개 변수  

|     매개 변수      |                                                                                                           설명                                                                                                           |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  -S <ServerName>   |                                    컴퓨터 또는 장치를 표시 하려는 상태와 함께 LPD 인쇄 큐를 호스팅하는 공유 프린터 이름 또는 IP 주소) (으로 지정 합니다. 필수.                                    |
|  -P <printerName>  |                                                              표시 하려는 상태와 함께 인쇄 큐에 대 한 프린터 이름을 사용 하 여 지정 합니다. 필수 사항입니다.                                                              |
| -C <BannerContent> |                인쇄 작업의 배너 페이지에 인쇄 하려면 콘텐츠를 지정 합니다. 이 매개 변수를 포함 되지 않은 경우 인쇄 작업을 보낸 컴퓨터의 이름이 배너 페이지에 나타납니다.                 |
|    -J <JobName>    |                           배너 페이지에 인쇄 되는 인쇄 작업 이름을 지정 합니다. 이 매개 변수를 포함 되지 않은 경우 인쇄 되는 파일의 이름이 배너 페이지에 나타납니다.                            |
| [-o &#124; "-o l"]  | 인쇄 하려는 파일의 유형을 지정 합니다. 매개 변수 **-o** 텍스트 파일을 인쇄 하도록 지정 합니다. 매개 변수 **"-o l"** 이진 파일 (예: PostScript 파일)를 인쇄 하도록 지정 합니다. |
|         -d         |              데이터 파일 제어 파일 전에 보내야 한다고 지정 합니다. 프린터에 필요한 데이터 파일을 먼저 보내도록 하는 경우이 매개 변수를 사용 합니다. 자세한 내용은 프린터 설명서를 참조 합니다.               |
|         -x         |                               **Lpr** 명령이 4.1.4 _u1을 포함 하는 릴리스에 대 한 Sun Microsystems 운영 체제 (sunos)와 호환 되어야 함을 지정 합니다.                                |
|     <FileName>     |                                                                                      인쇄할 파일 이름을 사용 하 여 지정 합니다. 필수 사항입니다.                                                                                      |
|         /?         |                                                                                              명령 프롬프트에 도움말을 표시합니다.                                                                                               |

## <a name="remarks"></a>설명  
- 프린터 이름을 찾으려면 프린터 폴더를 엽니다.  
- **-S**, **-P**, **-C**, 및 **-J** 매개 변수는 대/소문자 구분 및 대문자로 입력 해야 합니다.  
  ## <a name="BKMK_examples"></a>예와  
  이 예제에서는에서 10.0.0.45에서 LPD 호스트의 Laserprinter1 프린터 큐에 "문서 .txt" 텍스트 파일을 인쇄 하는 방법을 보여 줍니다.  
  ```  
  lpr -S 10.0.0.45 -P Laserprinter1 -o Document.txt  
  ```  
  이 예제에서는에서 10.0.0.45에서 LPD 호스트의 Laserprinter1 프린터 큐에 "PostScript_file" Adobe PostScript 파일을 인쇄 하는 방법을 보여 줍니다.  
  ```  
  lpr -S 10.0.0.45 -P Laserprinter1 "-o l" PostScript_file.ps  
  ```  

#### <a name="additional-references"></a>추가 참조  
-   [명령줄 구문 키](command-line-syntax-key.md)  
-   [인쇄 명령 참조](print-command-reference.md)  
