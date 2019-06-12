---
title: bootcfg dbg1394
description: Windows 명령 항목에 대 한 **bootcfg dbg1394** -지정된 된 운영 체제 항목에 대 한 구성 1394 포트 디버깅
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 35724697-90dd-4dbe-85b0-337fbd369dcc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 85a554e25d1553ea4cd9415bb180df4751966926
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66434838"
---
# <a name="bootcfg-dbg1394"></a>bootcfg dbg1394

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

지정된 된 운영 체제 항목에 대 한 1394 포트 디버깅을 구성 합니다.

## <a name="syntax"></a>구문
```
bootcfg /dbg1394 {ON | OFF}[/s <computer> [/u <Domain>\<User> /p <Password>]] [/ch <Channel>] /id <OSEntryLineNum>
```
## <a name="parameters"></a>매개 변수

|      매개 변수       |                                                                                                                                           설명                                                                                                                                            |
|----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   {ON &#124; OFF}    | 1394 포트 디버깅에 대 한 값을 지정합니다.<br /><br />-   **ON** -지정 된/dbg1394 옵션을 추가 하 여 원격 디버깅 지원을 통해 <OSEntryLineNum>합니다.<br />-   **OFF** -지정 된 위치 에서/dbg1394 옵션을 제거 하 여 원격 디버깅 지원을 해제 <OSEntryLineNum>합니다. |
|    /s <computer>     |                                                                                        이름 또는 원격 컴퓨터의 IP 주소를 지정 합니다 (백슬래시를 사용 하지 않습니다). 기본값은 로컬 컴퓨터입니다.                                                                                        |
| /u <Domain>\\<User>  |                                               지정한 사용자의 계정 권한으로 명령을 실행 <User> 나 <Domain> \\ <User>합니다. 기본값은 현재 로그온 된 명령을 실행 하는 컴퓨터에서 사용자의 사용 권한.                                               |
|    /p <Password>     |                                                                                                      에 지정 된 사용자 계정의 암호를 지정 된 **/u** 매개 변수입니다.                                                                                                       |
|     /ch 채널      |                                                           디버깅에 사용할 채널을 지정 합니다. 유효한 값은 1에서 64 사이의 정수입니다. 사용 하지 않는 합니다 **/ch** <Channel> 1394 포트 디버깅은 사용 하지 않는 경우 매개 변수입니다.                                                           |
| /id <OSEntryLineNum> |                                  1394 포트 디버깅 옵션 추가 되는 Boot.ini 파일의 [운영 체제] 섹션에 운영 체제 항목 줄 번호를 지정 합니다. [운영 체제] 섹션 헤더 후 첫 번째 줄은 1입니다.                                  |
|          /?          |                                                                                                                               명령 프롬프트에 도움말을 표시합니다.                                                                                                                               |

## <a name="BKMK_examples"></a>예제
다음 예제에서는 사용 하는 방법을 보여는 **bootcfg /dbg1394**명령:
```
bootcfg /dbg1394 /id 2 
bootcfg /dbg1394 on /ch 1 /id 3 
bootcfg /dbg1394 edit /ch 8 /id 2 
bootcfg /s srvmain /u maindom\hiropln /p p@ssW23 /dbg1394 off /id 2
```
#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)
