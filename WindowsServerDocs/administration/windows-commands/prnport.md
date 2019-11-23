---
title: prnport
description: 프린터 포트를 만들고, 삭제 하 고, 나열 하는 방법에 대해 알아봅니다.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6a0ec638-a21e-4a34-be5c-bd0f7ca89ffe
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c9c162cef2a3ae2f3de1e891691572130ae68f93
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71372547"
---
# <a name="prnport"></a>prnport

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

만들고 삭제 하 고 표시 하 고 포트 구성을 변경 하는 것 외에도 표준 TCP/IP 프린터 포트를 나열 합니다.

## <a name="syntax"></a>구문
```
cscript prnport {-a | -d | -l | -g | -t | -?} [-r <PortName>] 
[-s <ServerName>] [-u <UserName>] [-w <Password>] [-o {raw | lpr}] 
[-h <Hostaddress>] [-q <QueueName>] [-n <PortNumber>] -m{e | d} 
[-i <SNMPIndex>] [-y <CommunityName>] -2{e | -d}
```

## <a name="parameters"></a>매개 변수

|          매개 변수           |                                                                                                                                                                                                                                                                                                     설명                                                                                                                                                                                                                                                                                                      |
|------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|              -A              |                                                                                                                                                                                                                                                                                       표준 TCP/IP 프린터 포트를 만듭니다.                                                                                                                                                                                                                                                                                        |
|              -d              |                                                                                                                                                                                                                                                                                       표준 TCP/IP 프린터 포트를 삭제 합니다.                                                                                                                                                                                                                                                                                        |
|              -l              |                                                                                                                                                                                                                                                             **-s** 매개 변수를 사용 하 여 지정 된 컴퓨터의 모든 표준 tcp/ip 프린터 포트를 나열 합니다.                                                                                                                                                                                                                                                             |
|              -g              |                                                                                                                                                                                                                                                                            표준 TCP/IP 프린터 포트의 구성을 표시합니다.                                                                                                                                                                                                                                                                             |
|              -t              |                                                                                                                                                                                                                                                                           표준 TCP/IP 프린터 포트에 대 한 포트 설정을 구성합니다.                                                                                                                                                                                                                                                                           |
|        -r \<PortName >        |                                                                                                                                                                                                                                                                                프린터 연결 된 포트를 지정 합니다.                                                                                                                                                                                                                                                                                 |
|       -s \<ServerName >       |                                                                                                                                                                                                                               프린터를 관리 하려면를 호스트 하는 원격 컴퓨터의 이름을 지정 합니다. 컴퓨터를 지정 하지 않으면 로컬 컴퓨터가 사용 됩니다.                                                                                                                                                                                                                                |
| -u \<UserName >-w <Password> |                                                                                                              프린터를 관리 하려면를 호스트 하는 컴퓨터에 연결할 수 있는 권한이 있는 계정을 지정 합니다. 대상 컴퓨터의 로컬 관리자 그룹의 모든 구성원이 이러한 권한이 있지만 사용 권한을 다른 사용자에 게 부여 될 수도 있습니다. 계정을 지정 하지 않으면, 작동 하려면 명령에 대 한 이러한 사용 권한이 있는 계정으로 로그온 해야 합니다.                                                                                                               |
|     -o {원시 & #124; lpr}      |                                                                                                                                                                                                              포트에서 사용 하는 프로토콜 (TCP raw 또는 TCP lpr)을 지정 합니다. 포트 번호를 사용 하 여 선택적으로 지정할 수 원시 TCP를 사용 하는 경우는 **-n** 매개 변수입니다. 기본 포트 번호가 9100입니다.                                                                                                                                                                                                              |
|      -h \<Hostaddress >       |                                                                                                                                                                                                                                                                   프린터 포트를 구성 하려면 (IP 주소) 하 여 지정 합니다.                                                                                                                                                                                                                                                                    |
|       -q \<QueueName >        |                                                                                                                                                                                                                                                                                     원시 TCP 포트에 대 한 큐 이름을 지정합니다.                                                                                                                                                                                                                                                                                     |
|       -n \<PortNumber >       |                                                                                                                                                                                                                                                                    원시 TCP 포트에 대 한 포트 번호를 지정합니다. 기본 포트 번호가 9100입니다.                                                                                                                                                                                                                                                                    |
|        -m {&#124; d}        |                                                                                                                                                                                                                                                       SNMP 사용 되는지 여부를 지정 합니다. 매개 변수 **e** SNMP를 사용 합니다. 매개 변수 **d** SNMP를 사용 하지 않도록 설정 합니다.                                                                                                                                                                                                                                                        |
|        -i \<SNMPIndex        |                                                                                                                                                                                                                             Snmp를 사용 하는 경우 SNMP 인덱스를 지정 합니다. 자세한 내용은 [rfc 편집기 웹 사이트](https://go.microsoft.com/fwlink/?LinkId=569)에서 rfc 1759을 참조 하십시오.                                                                                                                                                                                                                              |
|     -y \<CommunityName >      |                                                                                                                                                                                                                                                                                SNMP를 사용 하는 경우 SNMP 커뮤니티 이름을 지정 합니다.                                                                                                                                                                                                                                                                                |
|       {& #124;-d}-2        | TCP lpr 포트에 대해 이중 스풀 (respooling이 라고도 함)을 사용할 수 있는지 여부를 지정 합니다. TCP lpr은 프린터에 전송 된 제어 파일에 정확한 바이트 수를 포함 해야 하지만, 프로토콜은 로컬 인쇄 공급자에서 개수를 가져올 수 없기 때문에 이중 스풀을 필요 합니다. 따라서 파일이 TCP lpr 인쇄 큐에 스풀링 되 면 system32 디렉터리에서 임시 파일로 스풀링 됩니다. TCP lpr은 임시 파일의 크기를 확인 하 고 LPD를 실행 하는 서버로 크기를 보냅니다. 매개 변수 **e** 이중 스풀을 합니다. 매개 변수 **d** 이중 스풀을 사용 하지 않도록 설정 합니다. |
|              /?              |                                                                                                                                                                                                                                                                                         명령 프롬프트에 도움말을 표시합니다.                                                                                                                                                                                                                                                                                         |

## <a name="remarks"></a>설명
-   **Prnport.vbs** 명령은%windir%\system32\ printing_Admin_Scripts\\<language> 디렉터리에 있는 Visual Basic 스크립트입니다. 이 명령을 사용 하려면 명령 프롬프트에서 **cscript** 다음에 prnport.vbs 파일의 전체 경로를 입력 하거나 디렉터리를 적절 한 폴더로 변경 합니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.
    ```
    cscript %WINdir%\System32\printing_Admin_Scripts\en-US\prnport
    ```
-   사용자가 제공 하는 정보에 공백이 포함 된 경우 텍스트에 따옴표를 사용 합니다 (예: `"computer Name"`).
-   TCP 원시 프로토콜은 lpr 프로토콜 보다 Windows에서 더 높은 성능 프로토콜입니다.

## <a name="BKMK_examples"></a>예와
서버에서 모든 표준 TCP/IP 인쇄 포트를 표시 하려면 \\\Server1, 유형:
```
cscript prnport -l -s Server1
```
서버에서 표준 TCP/IP 인쇄 포트를 삭제 하려면 \\\Server1 10.2.3.4, 형식에 네트워크 프린터에 연결 합니다.
```
cscript prnport -d -s Server1 -r IP_10.2.3.4
```
포트를 추가 하려면 표준 TCP/IP 인쇄 서버에서 \\10.2.3.4에 네트워크 프린터에 연결 하 고 포트 9100, 형식에서 원시 TCP 프로토콜을 사용 하는 \Server1:
```
cscript prnport -a -s Server1 -r IP_10.2.3.4 -h 10.2.3.4 -o raw -n 9100
```
SNMP를 사용 하려면 "공용" 커뮤니티 이름을 지정 하 고 서버에서 공유 10.2.3.4 네트워크 프린터에서 SNMP 인덱스 1로 설정 \\\Server1, 유형:
```
cscript prnport -t -s Server1 -r IP_10.2.3.4 -me -y public -i 1 -n 9100
```
표준 TCP/IP 인쇄 포트 10.2.3.4에 네트워크 프린터에 연결 하 고 프린터에서 장치 설정을 자동으로 가져오기는 로컬 컴퓨터에를 추가 하려면 다음을 입력 합니다.
```
cscript prnport -a -r IP_10.2.3.4 -h 10.2.3.4
```

#### <a name="additional-references"></a>추가 참조
명령줄 [구문 키](command-line-syntax-key.md)
[인쇄 명령 참조](print-command-reference.md)
