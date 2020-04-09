---
title: bootcfg addsw
description: 지정 된 운영 체제 항목에 대 한 운영 체제 로드 옵션을 추가 하는 bootcfg addsw의 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d8389293-ecd9-42f0-b84b-b9ead4cf52e6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a9ae5175dfc3b068276f6ab95d6823699c96b2b5
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80848716"
---
# <a name="bootcfg-addsw"></a>bootcfg addsw

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

지정된 된 운영 체제 항목에 대 한 운영 체제 로드 옵션을 추가합니다.

## <a name="syntax"></a>구문
```
bootcfg /addsw [/s <computer> [/u <Domain>\<User> /p <Password>]] [/mm <MaximumRAM>] [/bv] [/so] [/ng] /id <OSEntryLineNum>
```
### <a name="parameters"></a>매개 변수

|         용어         |                                                                                                            정의                                                                                                            |
|----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    /s <computer>     |                                                        이름 또는 원격 컴퓨터의 IP 주소를 지정 합니다 (백슬래시를 사용 하지 않습니다). 기본값은 로컬 컴퓨터입니다.                                                        |
| /u <Domain>\\<User>  |               <User> 또는 <Domain>\\<User>에 지정 된 사용자의 계정 권한으로 명령을 실행 합니다. 기본값은 현재 로그온 된 명령을 실행 하는 컴퓨터에서 사용자의 사용 권한.               |
|    /p <Password>     |                                                                      에 지정 된 사용자 계정의 암호를 지정 된 **/u** 매개 변수입니다.                                                                       |
|   /mm<MaximumRAM>   |                                          운영 체제에서 사용할 수 있는 (메가바이트) ram, 최대 크기를 지정 합니다. 32mb 보다 크거나 같은 값 이어야 합니다.                                          |
|         /bv          |                                    지정 된 <OSEntryLineNum>에 **/basevideo** 옵션을 추가 하 여 운영 체제에서 설치 된 비디오 드라이버에 대 한 표준 VGA 모드를 사용 하도록 지시 합니다.                                     |
|         /so          |                                      지정 된 *Osentrylinenum*에 **/sos** 옵션을 추가 하 여 운영 체제를 로드 하는 동안 장치 드라이버 이름을 표시 하도록 지정 합니다.                                      |
|         /ng          |                                         **/noguiboot** 옵션을 지정 된 <OSEntryLineNum>에 추가 하 고 CTRL + ALT + del 로그온 프롬프트 앞에 표시 되는 진행률 표시줄을 사용 하지 않도록 설정 합니다.                                          |
| /id <OSEntryLineNum> | 운영 체제 로드 옵션 추가 되는 Boot.ini 파일의 [운영 체제] 섹션에 운영 체제 항목 줄 번호를 지정 합니다. [운영 체제] 섹션 헤더 후 첫 번째 줄은 1입니다. |
|          /?          |                                                                                               명령 프롬프트에 도움말을 표시합니다.                                                                                               |

## <a name="examples"></a><a name=BKMK_examples></a>예와
다음 예제에서는 사용 하는 방법을 보여는 **bootcfg /addsw** 명령:
```
bootcfg /addsw /mm 64 /id 2 
bootcfg /addsw /so /id 3 
bootcfg /addsw /so /ng /s srvmain /u hiropln /id 2 
bootcfg /addsw /ng /id 2 
bootcfg /addsw /mm 96 /ng /s srvmain /u maindom\hiropln /p p@ssW23 /id 2
```
## <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md)
