---
title: nslookup
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 41516932-7833-434a-aa92-b4cf0f9a7ef7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 84e3e9ee920f458ca775dd7b76d892f10ba2f992
ms.sourcegitcommit: ee8e0b217be6f6b2532ee7265fb4be00c106e124
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70878111"
---
# <a name="nslookup"></a>nslookup

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

도메인 이름 시스템 (DNS) 인프라를 진단 하는 데 사용할 수 있는 정보를 표시 합니다. 이 도구를 사용 하기 전에 DNS의 작동 원리에 대해 잘 알고 있어야 합니다. Nslookup 명령줄 도구는 TCP/IP 프로토콜을 설치한 경우에만 사용할 수 있습니다.
## <a name="syntax"></a>구문

```
nslookup [<-SubCommand ...>] [{<computerTofind> | -<Server>}]
nslookup /exit
nslookup /finger [<UserName>] [{[>] <FileName>|[>>] <FileName>}]
nslookup /{help | ?}
nslookup /ls [<Option>] <DNSDomain> [{[>] <FileName>|[>>] <FileName>}]
nslookup /lserver <DNSDomain> 
nslookup /root 
nslookup /server <DNSDomain>
nslookup /set <KeyWord>[=<Value>]
nslookup /set all 
nslookup /set class=<Class>
nslookup /set [no]d2
nslookup /set [no]debug
nslookup /set [no]defname
nslookup /set domain=<DomainName>
nslookup /set [no]ignore
nslookup /set port=<Port>
nslookup /set querytype=<ResourceRecordtype>
nslookup /set [no]recurse
nslookup /set retry=<Number>
nslookup /set root=<RootServer>
nslookup /set [no]search
nslookup /set srchlist=<DomainName>[/...]
nslookup /set timeout=<Number>
nslookup /set type=<ResourceRecordtype>
nslookup /set [no]vc
nslookup /view <FileName>
```

## <a name="parameters"></a>매개 변수

|                       매개 변수                       |                                                                                                         설명                                                                                                         |
|-------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   [nslookup exit Command](nslookup-exit-command.md)   |                                                                                                     종료 **nslookup**합니다.                                                                                                     |
| [nslookup finger Command](nslookup-finger-command.md) |                                                                                  현재 컴퓨터에서 손가락 서버와 연결합니다.                                                                                   |
|           [nslookup help](nslookup-help.md)           |                                                                                    간단한 요약이 표시 되며 **nslookup** 하위 명령입니다.                                                                                    |
|             [nslookup ls](nslookup-ls.md)             |                                                                                             DNS 도메인에 대 한 정보를 나열합니다.                                                                                             |
|        [nslookup lserver](nslookup-lserver.md)        |                                                                                   지정 된 DNS 도메인의 기본 서버를 변경합니다.                                                                                   |
|           [nslookup root](nslookup-root.md)           |                                                                     DNS 도메인 네임 스페이스의 루트에 대 한 서버에 기본 서버를 변경합니다.                                                                     |
|         [nslookup server](nslookup-server.md)         |                                                                                   지정 된 DNS 도메인의 기본 서버를 변경합니다.                                                                                   |
|            [nslookup set](nslookup-set.md)            |                                                                              구성 설정에 영향을 주는 변경 방법을 조회 함수입니다.                                                                               |
|        [nslookup set all](nslookup-set-all.md)        |                                                                                  구성 설정의 현재 값을 인쇄합니다.                                                                                   |
|      [nslookup set class](nslookup-set-class.md)      |                                                                     쿼리 클래스를 변경 합니다. 클래스는 프로토콜 그룹 정보를 지정합니다.                                                                     |
|         [nslookup set d2](nslookup-set-d2.md)         |                                                                     철저 한 디버깅 모드를 설정 하거나 해제 합니다. 모든 패킷이 모든 필드를 표시 합니다.                                                                      |
|      [nslookup set debug](nslookup-set-debug.md)      |                                                                                               디버깅 모드를 설정 하거나 해제 합니다.                                                                                               |
|                 nslookup/set defname                 |                                            단일 구성 요소 조회 요청에 기본 DNS 도메인 이름을 추가합니다. 단일 구성 요소에는 마침표가 없는 구성 요소가입니다.                                            |
|     [nslookup set domain](nslookup-set-domain.md)     |                                                                                 지정 된 이름과 기본 DNS 도메인 이름을 변경 합니다.                                                                                  |
|                 nslookup/set 무시                  |                                                                                              패킷 잘림 오류를 무시합니다.                                                                                              |
|       [nslookup set port](nslookup-set-port.md)       |                                                                          지정 된 값으로 기본 TCP/UDP DNS 이름 서버 포트를 변경 합니다.                                                                           |
|  [nslookup set querytype](nslookup-set-querytype.md)  |                                                                                       쿼리에 대 한 리소스 레코드 종류를 변경합니다.                                                                                       |
|    [nslookup set recurse](nslookup-set-recurse.md)    |                                                                    정보가 없는 경우 다른 서버를 쿼리 하는 DNS 이름 서버를 알려 줍니다.                                                                    |
|      [nslookup set retry](nslookup-set-retry.md)      |                                                                                                 재시도 횟수를 설정합니다.                                                                                                 |
|       [nslookup set root](nslookup-set-root.md)       |                                                                                    쿼리에 사용 되는 루트 서버 이름을 변경 합니다.                                                                                    |
|     [nslookup set search](nslookup-set-search.md)     | 응답을 받을 때까지 요청에 DNS 도메인 검색 목록에 DNS 도메인 이름을 추가 합니다. 집합과 조회 요청 하나 이상의 기간을 포함 하는 경우에 적용 됩니다 있지만 뒤에 마침표 종료 하지 마십시오. |
|   [nslookup set srchlist](nslookup-set-srchlist.md)   |                                                                                    기본 DNS 도메인 이름 및 검색 목록을 변경합니다.                                                                                     |
|    [nslookup set timeout](nslookup-set-timeout.md)    |                                                                           초기 요청에 회신을 기다릴 시간 (초) 수를 변경 합니다.                                                                           |
|       [nslookup set type](nslookup-set-type.md)       |                                                                                       쿼리에 대 한 리소스 레코드 종류를 변경합니다.                                                                                       |
|         [nslookup set vc](nslookup-set-vc.md)         |                                                                     가상 회로 보낼 때 서버에 요청을 사용 하지 않는 또는 사용 하도록 지정 합니다.                                                                      |
|           [nslookup view](nslookup-view.md)           |                                                                          정렬 하 고는 이전 출력 나열 **ls** 하위 명령 또는 명령입니다.                                                                          |

## <a name="remarks"></a>설명
- *Computertofind* 가 IP 주소이 고 쿼리가 A 또는 PTR 리소스 레코드 종류에 대 한 것 이면 컴퓨터 이름이 반환 됩니다. *Computertofind* 가 이름이 고 마침표가 없으면 기본 DNS 도메인 이름이 이름에 추가 됩니다. 이 동작은 다음의 상태에 따라 **설정** 하위 명령: **도메인**, **srchlist**, **defname**, 및 **검색**합니다.
- *Computertofind*대신 하이픈 (-)을 입력 하면 명령 프롬프트가 **nslookup** 대화형 모드로 변경 됩니다.
- 명령줄 길이 256 자 미만 이어야 합니다.
- **nslookup** 에는 대화형 및 비 대화형 모드의 두 가지 모드가 있습니다.
  데이터의 단일 부분을 조회 해야 하는 경우에는 비 대화형 모드를 사용 합니다. 첫 번째 매개 변수 이름 또는 조회 하려고 하는 컴퓨터의 IP 주소를 입력 합니다. 두 번째 매개 변수 이름 또는 DNS 이름 서버의 IP 주소를 입력 합니다. 두 번째 인수를 생략 하면 **nslookup** 기본 DNS 이름 서버를 사용 합니다.
  둘 이상의 데이터를 조회 해야 하는 경우 대화형 모드를 사용할 수 있습니다. 첫 번째 매개 변수에 하이픈 (-)을 입력 하 고 두 번째 매개 변수에 대해 DNS 이름 서버의 이름 또는 IP 주소를 입력 합니다. 또는 매개 변수 모두 생략 하 고 **nslookup** 기본 DNS 이름 서버를 사용 합니다. 다음은 대화형 모드에서 작업 하는 방법에 대 한 몇 가지 팁입니다.
  -   대화형 명령을 언제 든 지를 중단 하려면 CTRL + B를 누릅니다.
  -   를 종료 하려면 다음을 입력 **종료**합니다.
  -   컴퓨터 이름으로 기본 제공 명령으로 처리 하려면 앞에 이스케이프 문자 (\\).
  -   인식할 수 없는 명령에는 컴퓨터 이름으로 해석 됩니다.
- 조회 요청에 실패 하면 **nslookup** 오류 메시지를 인쇄 합니다. 다음 표에서 가능한 오류 메시지를 나열합니다.
  |**오류 메시지**|**설명**|
  |-----------|----------|
  |`timed out`|특정 시간 동안 특정 횟수의 재시도 후 서버 요청에 응답 하지 않았습니다. 와 제한 시간을 설정할 수는 **제한 시간 설정** 하위 명령. 와 재시도 횟수를 설정할 수는 **집합 재시도** 하위 명령.|
  |`No response from server`|DNS 이름 서버는 서버 컴퓨터에서 실행 됩니다.|
  |`No records`|DNS 이름 서버에 리소스 레코드는 컴퓨터에 대 한 현재 쿼리 형식의 없는 컴퓨터 이름이 올바른지 있지만. 쿼리 형식이 지정 된 고 **querytype 설정** 명령입니다.|
  |`Nonexistent domain`|컴퓨터 또는 DNS 도메인 이름이 존재 하지 않습니다.|
  |`Connection refused`<br /><br />또는<br /><br />`Network is unreachable`|DNS 이름 서버 또는 손가락 서버에 연결할 수 없습니다. 이 오류가 자주 발생 하면 **ls** 및 **손가락** 요청 합니다.|
  |`Server failure`|DNS 이름 서버 데이터베이스의 내부 불일치를 발견 하 고 유효한 응답을 반환할 수 없습니다.|
  |`Refused`|DNS 이름 서버 요청을 거부 했습니다.|
  |`format error`|DNS 이름 서버 요청 패킷의 형식이 없음을 발견 합니다. 에 오류가 있다는 의미일 수 있습니다 **nslookup**합니다.|
- 에 대 한 자세한 내용은 **nslookup** 명령 및 DNS를 다음 리소스를 참조 합니다.
  - Lee, T., Davies, j. 2000. *Microsoft Windows 2000 TCP/IP 프로토콜 및 서비스 기술 참조*합니다. Redmond, 워싱턴: Microsoft를 누릅니다.
  - Albitz, P., Loukides, M. 및 C. Liu입니다. 2001. *DNS 및 바인드, 4 번째 버전* Sebastopol, 캘리포니아: O'Reilly 및 연결, i n c.
  - Larson, M. 및 C. Liu입니다. 2001. *Windows 2000에서 DNS*합니다. Sebastopol, 캘리포니아: O'Reilly 및 연결, i n c.
    #### <a name="examples"></a>예
    각 명령줄 옵션은 명령 이름으로, 일부 경우, 등호 (=) 및 값에 바로 뒤에 오는 하이픈 (-)으로 구성 됩니다. 예를 들어, 기본 쿼리 형식을 호스트 (컴퓨터) 정보 및 초기 제한 시간을 10 초를 변경 하려면 입력: **nslookup-querytype = hinfo-timeout = 10**
    ## <a name="see-also"></a>관련 항목
    [명령줄 구문 키](command-line-syntax-key.md)
