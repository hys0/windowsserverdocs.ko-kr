---
title: prnmngr
description: 추가, 삭제 및 나열할 프린터와 연결 하는 방법에 알아봅니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 39eee1a8-4b41-4c9f-941e-486495135eb8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: f0e3af7b05b77400d3d8a04d048b34b8c553438d
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66436237"
---
# <a name="prnmngr"></a>prnmngr

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

추가, 삭제 하 고, 프린터 또는 프린터 연결 설정 및 기본 프린터를 표시 하는 것 외에도 나열 합니다.

## <a name="syntax"></a>구문
```
cscript Prnmngr {-a | -d | -x | -g | -t | -l | -?}[c] [-s <ServerName>] 
[-p <printerName>] [-m <printermodel>] [-r <PortName>] [-u <UserName>] 
[-w <Password>]
```

## <a name="parameters"></a>매개 변수

|           매개 변수           |                                                                                                                                                                                        설명                                                                                                                                                                                        |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|              -A               |                                                                                                                                                                             로컬 프린터 연결을 추가합니다.                                                                                                                                                                              |
|              -d               |                                                                                                                                                                               프린터 연결을 삭제합니다.                                                                                                                                                                               |
|              -x               |                                                                                                               지정 된 서버에서 모든 프린터를 삭제 합니다 **-s** 매개 변수입니다. 서버를 지정 하지 않으면 Windows 로컬 컴퓨터에서 모든 프린터를 삭제 합니다.                                                                                                               |
|              -g               |                                                                                                                                                                               기본 프린터를 표시합니다.                                                                                                                                                                               |
|              -t               |                                                                                                                                                        로 지정 된 프린터를 기본 프린터로 설정의 **-p** 매개 변수입니다.                                                                                                                                                         |
|              -l               |                                                                                                         지정한 서버에 설치 된 모든 프린터를 나열 합니다 **-s** 매개 변수입니다. 서버를 지정 하지 않으면 Windows 로컬 컴퓨터에 설치 된 프린터를 나열 합니다.                                                                                                         |
|               c               |                                                                                                                                      프린터 연결에 매개 변수가 적용 되도록 지정 합니다. 와 함께 사용할 수는 **-** 및 **-x** 매개 변수입니다.                                                                                                                                      |
|        -s <ServerName>        |                                                                                                                  프린터를 관리 하려면를 호스트 하는 원격 컴퓨터의 이름을 지정 합니다. 컴퓨터를 지정 하지 않으면 로컬 컴퓨터가 사용 됩니다.                                                                                                                  |
|       -p \<printerName>       |                                                                                                                                                                관리 하려는 프린터의 이름을 지정 합니다.                                                                                                                                                                 |
|     -m \<DrivermodelName>     |                                                                                                          이름을 사용 하 여 드라이버를 설치 하려면 지정 합니다. 드라이버가 지 원하는 프린터 모델에 대 한 자주 라고 합니다. 자세한 내용은 프린터 설명서를 참조 하십시오.                                                                                                           |
|        -r \<PortName>         |                                                                         프린터가 연결 되어 있는 포트를 지정 합니다. 포트의 ID를 사용 하 여 병렬 또는 직렬 포트 인 경우 (예를 들어 LPT1: 또는 c o m 1:). TCP/IP 포트 이면 포트를 추가할 때 지정 된 포트 이름을 사용 합니다.                                                                          |
| -u \<사용자 이름 >-w \<암호 > | 프린터를 관리 하려면를 호스트 하는 컴퓨터에 연결할 수 있는 권한이 있는 계정을 지정 합니다. 대상 컴퓨터의 로컬 관리자 그룹의 모든 구성원이 이러한 권한이 있지만 사용 권한을 다른 사용자에 게 부여 될 수도 있습니다. 계정을 지정 하지 않으면, 작동 하려면 명령에 대 한 이러한 사용 권한이 있는 계정으로 로그온 해야 합니다. |
|              /?               |                                                                                                                                                                           명령 프롬프트에 도움말을 표시합니다.                                                                                                                                                                            |

## <a name="remarks"></a>설명
-   합니다 **prndrvr** 명령입니다는 %WINdir%\System32\printing_Admin_Scripts에 있는 Visual Basic 스크립트\\ <language> 디렉터리입니다. 명령 프롬프트에서이 명령을 사용 하려면 입력 **cscript** 뒤에 대 한 전체 경로 **prnmngr** 파일 또는 디렉터리 적절 한 폴더로 변경 합니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.
    ```
    cscript %WINdir%\System32\printing_Admin_Scripts\en-US\prnmngr
    ```
-   텍스트 주위에 따옴표를 사용 하 여 사용자가 제공한 정보에 공백이 있으면 (예를 들어 `"computer Name"`).

## <a name="BKMK_examples"></a>예제
로컬 컴퓨터에서 p t 1에 연결 되 고 색 프린터 Driver1 라는 프린터 드라이버가 필요한 colorprinter_2 라는 프린터를 추가 하려면 다음을 입력 합니다.
```
cscript prnmngr -a -p colorprinter_2 -m "color printer Driver1" -r lpt1:
```
Colorprinter_2 HRServer 라는 원격 컴퓨터에서 명명 된 프린터를 삭제 하려면 다음을 입력 합니다.
```
cscript prnmngr -d -s HRServer -p colorprinter_2 
```

#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)
[인쇄 명령 참조](print-command-reference.md)
