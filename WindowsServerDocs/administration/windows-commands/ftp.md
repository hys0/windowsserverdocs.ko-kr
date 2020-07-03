---
title: ftp
description: Ftp (파일 전송 프로토콜) 서버 서비스를 실행 하는 컴퓨터에서 파일을 전송 하는 ftp 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 758335e1-fd8d-448c-a654-993126239dd9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e78148e1e7dc4f402d80bb4ebfbcbdac52249407
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85925615"
---
# <a name="ftp"></a>ftp

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ftp (파일 전송 프로토콜) 서버 서비스를 실행 하는 컴퓨터에서 파일을 전송 합니다. 이 명령은 ASCII 텍스트 파일을 처리 하 여 대화형으로 또는 일괄 처리 모드에서 사용할 수 있습니다.

## <a name="syntax"></a>구문

```
ftp [-v] [-d] [-i] [-n] [-g] [-s:<filename>] [-a] [-A] [-x:<sendbuffer>] [-r:<recvbuffer>] [-b:<asyncbuffers>][-w:<windowssize>][<host>] [-?]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ----------| ----------- |
| -v | 원격 서버 ' 응답 수를 표시를 하지 않습니다. |
| -d | 디버깅을 사용 하도록 설정 하 여 FTP 클라이언트와 FTP 서버 간에 전달 되는 모든 명령을 표시 합니다. |
| -i | 여러 파일을 전송 하는 동안 대화형 프롬프트를 사용 하지 않도록 설정 합니다. |
| -n | 초기 연결 시 자동 로그온을 표시 하지 않습니다. |
| -g | 파일 이름에 와일드 카드 사용을 해제합니다.  **Glob** 로컬 파일 및 경로 이름에 와일드 카드 문자로 별표 (*) 및 물음표 (?)의 사용을 허용 합니다. |
| 삭제`<filename>` | 포함 된 텍스트 파일을 지정 **ftp** 명령입니다. 이 명령은 실행 후 자동으로 **ftp** 시작 합니다. 이 매개 변수는 공백이 없어야 합니다. 이 매개 변수를 사용 하 여 리디렉션 대신 (`<`). **참고:** Windows 8 및 Windows Server 2012 또는 이후 운영 체제에서 텍스트 파일을 u t F-8에서 작성 해야 합니다. |
| 지정하지 않을 경우 | Ftp 데이터 연결을 바인딩할 때 모든 로컬 인터페이스를 사용할 수 있도록 지정 합니다. |
| -A | 익명으로 ftp 서버에 로그온 합니다. |
| .x`<sendbuffer> `| 8192의 기본 SO_SNDBUF 크기를 재정의합니다. |
| &`<recvbuffer>` | 8192의 기본 SO_RCVBUF 크기를 재정의합니다. |
| b`<asyncbuffers>` | 기본 비동기 버퍼 수가 3 재정의합니다. |
| w`<windowssize>` | 전송 버퍼의 크기를 지정합니다. 기본 창 크기는 4096 바이트입니다. |
| `<host>` | 연결할 ftp 서버의 컴퓨터 이름, IP 주소 또는 IPv6 주소를 지정 합니다. 호스트 이름이 나 주소를 지정 하는 경우 마지막 줄에 매개 변수 이어야 합니다. |
| -? | 명령 프롬프트에 도움말을 표시합니다. |

#### <a name="remarks"></a>설명

- **Ftp** 명령줄 매개 변수는 대/소문자를 구분 합니다.

- 이 명령은 네트워크 연결에서 네트워크 어댑터의 속성에 구성 요소로 **인터넷 프로토콜 (tcp/ip)** 프로토콜을 설치 하는 경우에만 사용할 수 있습니다.

- **Ftp** 명령은 대화형으로 사용할 수 있습니다. 시작 된 후 **ftp** 사용할 수 있는 하위 환경을 만들고 **ftp** 명령입니다. 명령 프롬프트를 입력 하 여 돌아갈 수는 **종료** 명령입니다. **Ftp** 하위 환경이 실행 되는 경우 명령 프롬프트에 표시 됩니다 `ftp >` . 자세한 내용은 **ftp** 명령을 참조 하십시오.

- Ftp 명령은 IPv6 프로토콜이 설치 될 때 i **p** v 6을 사용할 수 있도록 지원 합니다.

### <a name="examples"></a>예

이라는 ftp 서버에 로그온 하려면 `ftp.example.microsoft.com` 다음을 입력 합니다.

```
ftp ftp.example.microsoft.com
```

이라는 ftp 서버에 로그온 하 `ftp.example.microsoft.com` 고 *resync.txt*이라는 파일에 포함 된 **ftp** 명령을 실행 하려면 다음을 입력 합니다.

```
ftp -s:resync.txt ftp.example.microsoft.com
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [추가 FTP 지침](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))

- [IP 버전 6](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc738636(v=ws.10))

- [IPv6 애플리케이션](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc782509(v=ws.10))
