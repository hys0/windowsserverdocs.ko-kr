---
title: ftp
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 758335e1-fd8d-448c-a654-993126239dd9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b64e6831fcf8930c62b2a3f04022dc49d5297683
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375864"
---
# <a name="ftp"></a>ftp

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ftp (파일 전송 프로토콜) 서버 서비스를 실행 하는 컴퓨터에서 파일을 전송 합니다. **ftp** 는 ASCII 텍스트 파일을 처리 하 여 대화형으로 또는 일괄 처리 모드에서 사용할 수 있습니다. 
## <a name="syntax"></a>구문
```
ftp [-v] [-d] [-i] [-n] [-g] [-s:<FileName>] [-a] [-A] [-x:<SendBuffer>] [-r:<RecvBuffer>] [-b:<AsyncBuffers>][-w:<WindowsSize>]  [-?] [<Host>]
```
### <a name="parameters"></a>매개 변수

|     매개 변수     |                                                                                                                                                      설명                                                                                                                                                      |
|-------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|        -v         |                                                                                                                                    원격 서버 ' 응답 수를 표시를 하지 않습니다.                                                                                                                                     |
|        -d         |                                                                                                               디버깅을 사용 하도록 설정 하 여 FTP 클라이언트와 FTP 서버 간에 전달 되는 모든 명령을 표시 합니다.                                                                                                                |
|        -i         |                                                                                                                            여러 파일을 전송 하는 동안 대화형 프롬프트를 사용 하지 않도록 설정 합니다.                                                                                                                             |
|        -n         |                                                                                                                                    초기 연결 시 자동 로그온을 표시 하지 않습니다.                                                                                                                                     |
|        -g         |                                         파일 이름에 와일드 카드 사용을 해제합니다.  **Glob** 는 로컬 파일 및 경로 이름에서 별표 (\*) 및 물음표 (?)를 와일드 카드 문자로 사용할 수 있도록 허용 합니다. 자세한 내용은 [추가 참조](ftp.md#BKMK_additionalRef)를 참조 하세요.                                          |
|   -s: <FileName>   | 포함 된 텍스트 파일을 지정 **ftp** 명령입니다. 이 명령은 실행 후 자동으로 **ftp** 시작 합니다. 이 매개 변수는 공백이 없어야 합니다. 이 매개 변수를 사용 하 여 리디렉션 대신 ( **<** ). **참고:** Windows 8 및 Windows Server 2012 이상 운영 체제에서 텍스트 파일은 u t f-8로 작성 되어야 합니다. |
|        -A         |                                                                                                                 Ftp 데이터 연결을 바인딩할 때 모든 로컬 인터페이스를 사용할 수 있도록 지정 합니다.                                                                                                                  |
|        -A         |                                                                                                                                        익명으로 ftp 서버에 로그온 합니다.                                                                                                                                         |
|  -x: <SendBuffer>  |                                                                                                                                     8192의 기본 SO_SNDBUF 크기를 재정의합니다.                                                                                                                                     |
|  -r: <RecvBuffer>  |                                                                                                                                     8192의 기본 SO_RCVBUF 크기를 재정의합니다.                                                                                                                                     |
| -b: <AsyncBuffers> |                                                                                                                                    기본 비동기 버퍼 수가 3 재정의합니다.                                                                                                                                     |
| -w: <WindowsSize>  |                                                                                                                   전송 버퍼의 크기를 지정합니다. 기본 창 크기는 4096 바이트입니다.                                                                                                                   |
|        -?         |                                                                                                                                         명령 프롬프트에 도움말을 표시합니다.                                                                                                                                          |
|      <host>       |                                                                    연결할 ftp 서버의 컴퓨터 이름, IP 주소 또는 IPv6 주소를 지정 합니다. 호스트 이름이 나 주소를 지정 하는 경우 마지막 줄에 매개 변수 이어야 합니다.                                                                    |

## <a name="remarks"></a>설명
- Windows Server 2003의 **ftp** 명령에 대 한 자세한 내용은 [ftp](https://technet.microsoft.com/library/cc756013(v=ws.10).aspx)를 참조 하십시오.
- **ftp** 명령줄 매개 변수는 대/소문자를 구분 합니다.
- 사용할 경우에만 **인터넷 프로토콜 (TCP/IP)** 프로토콜 네트워크 연결에서 네트워크 어댑터의 속성에는 구성 요소로 설치 됩니다.
- **ftp** 는 대화형으로 사용할 수 있습니다. 시작 된 후 **ftp** 사용할 수 있는 하위 환경을 만들고 **ftp** 명령입니다. 명령 프롬프트를 입력 하 여 돌아갈 수는 **종료** 명령입니다. 때는 **ftp** 으로 표시 됩니다 하위 환경이 실행 되는 **ftp >** 명령 프롬프트입니다. 자세한 내용은 참조는 **ftp** 명령입니다.
- **ftp** 는 ipv6 프로토콜이 설치 될 때 i p v 6의 사용을 지원 합니다. 자세한 내용은 [추가 참조](ftp.md#BKMK_additionalRef)를 참조 하세요.
  ## <a name="BKMK_Examples"></a>예와
  Ftp.example.microsoft.com 라는 ftp 서버에 로그온 하려면 다음을 입력 합니다.
  ```
  ftp ftp.example.microsoft.com
  ```
  Ftp.example.microsoft.com 라는 ftp 서버에 로그온 하 고 라는 파일에 포함 된 **ftp** 명령을 실행 하려면 다음을 입력 합니다.
  ```
  ftp -s:resync.txt ftp.example.microsoft.com
  ```
  ## <a name="BKMK_additionalRef"></a>추가 참조
- [IP 버전 6](https://technet.microsoft.com/library/cc738636(v=ws.10).aspx)
- [IPv6 응용 프로그램](https://technet.microsoft.com/library/cc782509(v=ws.10).aspx)
- [명령줄 구문 키](command-line-syntax-key.md)
