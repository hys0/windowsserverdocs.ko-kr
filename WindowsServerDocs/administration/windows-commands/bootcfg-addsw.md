---
title: bootcfg addsw
description: Windows 명령 항목에 대 한 **bootcfg addsw** -지정된 된 운영 체제 항목에 대 한 운영 체제 로드 옵션을 추가 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d8389293-ecd9-42f0-b84b-b9ead4cf52e6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a056cec15bf804dafed4c4d39a80386e58c87fea
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66434879"
---
# <a name="bootcfg-addsw"></a>bootcfg addsw

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

지정된 된 운영 체제 항목에 대 한 운영 체제 로드 옵션을 추가합니다.

## <a name="syntax"></a>구문
```
bootcfg /addsw [/s <computer> [/u <Domain>\<User> /p <Password>]] [/mm <MaximumRAM>] [/bv] [/so] [/ng] /id <OSEntryLineNum>
```
## <a name="parameters"></a>매개 변수

|         용어         |                                                                                                            정의                                                                                                            |
|----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    /s <computer>     |                                                        이름 또는 원격 컴퓨터의 IP 주소를 지정 합니다 (백슬래시를 사용 하지 않습니다). 기본값은 로컬 컴퓨터입니다.                                                        |
| /u <Domain>\\<User>  |               지정한 사용자의 계정 권한으로 명령을 실행 <User> 나 <Domain> \\ <User>합니다. 기본값은 현재 로그온 된 명령을 실행 하는 컴퓨터에서 사용자의 사용 권한.               |
|    /p <Password>     |                                                                      에 지정 된 사용자 계정의 암호를 지정 된 **/u** 매개 변수입니다.                                                                       |
|   /mm <MaximumRAM>   |                                          운영 체제에서 사용할 수 있는 (메가바이트) ram, 최대 크기를 지정 합니다. 32mb 보다 크거나 같은 값 이어야 합니다.                                          |
|         /bv          |                                    추가 된 **/basevideo** 옵션을 지정 된 <OSEntryLineNum>, 운영 체제가 설치 된 비디오 드라이버에 대 한 표준 VGA 모드를 사용 하도록 합니다.                                     |
|         /so          |                                      추가 된 **동안** 옵션을 지정 된 *OSEntryLineNum*, 운영 체제가 로드 되는 동안 장치 드라이버의 이름을 표시 하도록 합니다.                                      |
|         /ng          |                                         추가 된 **/noguiboot** 옵션을 지정 된 <OSEntryLineNum>, 앞에 표시 되는 CTRL + ALT + del 로그온 프롬프트는 진행률 표시줄을 사용 하지 않도록 설정 합니다.                                          |
| /id <OSEntryLineNum> | 운영 체제 로드 옵션 추가 되는 Boot.ini 파일의 [운영 체제] 섹션에 운영 체제 항목 줄 번호를 지정 합니다. [운영 체제] 섹션 헤더 후 첫 번째 줄은 1입니다. |
|          /?          |                                                                                               명령 프롬프트에 도움말을 표시합니다.                                                                                               |

## <a name="BKMK_examples"></a>예제
다음 예제에서는 사용 하는 방법을 보여는 **bootcfg /addsw** 명령:
```
bootcfg /addsw /mm 64 /id 2 
bootcfg /addsw /so /id 3 
bootcfg /addsw /so /ng /s srvmain /u hiropln /id 2 
bootcfg /addsw /ng /id 2 
bootcfg /addsw /mm 96 /ng /s srvmain /u maindom\hiropln /p p@ssW23 /id 2
```
#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)
