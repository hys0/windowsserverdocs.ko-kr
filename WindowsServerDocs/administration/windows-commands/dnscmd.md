---
title: dnscmd
description: DNS 서버를 관리 하는 명령줄 인터페이스인 dnscmd 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e7f31cb5-a426-4e25-b714-88712b8defd5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 47be29e55c4626f5c05498074f10418730c6a6f3
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931302"
---
# <a name="dnscmd"></a>Dnscmd

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

DNS 서버를 관리 하기 위한 명령줄 인터페이스입니다. 이 유틸리티는 배치 파일 DNS의 일상적인 관리 작업을 자동화 하기 위해 네트워크에 간단한 무인된 설치 및 구성을 새 DNS 서버를 수행 하려면 스크립팅에 유용 합니다.

## <a name="syntax"></a>구문

```
dnscmd <servername> <command> [<command parameters>]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<servername>` | 원격 또는 로컬 DNS 서버의 IP 주소 또는 호스트 이름입니다. |

## <a name="dnscmd-ageallrecords-command"></a>dnscmd/ageallrecords 명령

지정 된 영역 또는 노드는 DNS 서버에서 리소스 레코드에 타임 스탬프에 현재 시간을 설정합니다.

### <a name="syntax"></a>구문

```
dnscmd [<servername>] /ageallrecords <zonename>[<nodename>] | [/tree]|[/f]
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ---------- | ----------- |
| `<servername>` | IP 주소나 정규화 된 도메인 이름 (FQDN)으로 호스트 이름으로 표시는 관리자는 계획을 관리 하는 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다. |
| `<zonename>` | 영역의 FQDN을 지정합니다. |
| `<nodename>` | 다음을 사용 하 여 영역에서 특정 노드 또는 하위 트리를 지정 합니다.<ul><li>**@** 루트 영역 또는 FQDN의 경우</li><li>노드 (끝에 마침표 (.)로 이름)의 FQDN</li><li>영역 루트를 기준으로 하는 이름의 단일 레이블입니다.</li></ul> |
| /tree | 모든 자식 노드는 타임 스탬프를 받을 수도 지정 합니다. |
| /f | 확인을 요청 하지 않고 명령을 실행 합니다. |

##### <a name="remarks"></a>설명

- **ageallrecords** DNS의 현재 버전과 이전 버전의 DNS는 에이징 및 청소 지원 되지 않았습니다 간의 이전 버전과 호환성을 위해 명령입니다. 현재 시간 타임 스탬프가 타임 스탬프를 갖지 않는 리소스 레코드를 추가 하 고 현재 시간 타임 스탬프가 없는 리소스 레코드에 설정 합니다.

- 레코드에 타임 스탬프가 추가 하지 않으면 레코드 청소 발생 하지 않습니다. NS (이름 서버) 리소스 레코드를 (soa) 리소스 레코드의 시작 부분 및 인터넷 이름 서비스 WINS (Windows) 리소스 레코드 청소 프로세스에 포함 되지 않은 고 타임 스탬프가 기록 없는 경우에는 **ageallrecords** 명령 실행 합니다.

- 이 명령은 DNS 서버 및 영역에 대 한 청소를 사용 하지 않으면 실패 합니다. 영역에 대 한 청소를 사용 하도록 설정 하는 방법에 대 한 자세한 내용은이 문서의 명령 구문 내에서 **에이징** 매개 변수를 참조 하세요 `dnscmd /config` .

- DNS 리소스 레코드에 타임 스탬프를 추가 하면 Windows Server 이외의 운영 체제에서 실행 되는 DNS 서버와 호환 되지 않습니다. **Ageallrecords** 명령을 사용 하 여 추가한 타임 스탬프는 되돌릴 수 없습니다.

- 선택적 매개 변수가 아무것도 지정 하지 않으면 하는 경우이 명령은 지정 된 노드에서 모든 리소스 레코드를 반환 합니다. 선택적 매개 변수 중 하나에 대 한 값이 지정 하는 경우 **dnscmd** 값 또는 선택적 매개 변수 또는 매개 변수에서 지정 된 값을 해당 하는 리소스 레코드를 열거 합니다.

### <a name="examples"></a>예

[예제 1: 타임 스탬프에 대 한 현재 시간을 리소스 레코드로 설정](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc784399(v=ws.10)#example-1-set-the-current-time-on-a-time-stamp-to-resource-records)

## <a name="dnscmd-clearcache-command"></a>dnscmd/clearcache 명령

지정된 된 DNS 서버에서 리소스 레코드의 DNS 캐시 메모리를 지웁니다.

### <a name="syntax"></a>구문

```
dnscmd [<servername>] /clearcache
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ---------- | ----------- |
| `<servername>` | IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다. |

### <a name="example"></a>예제

```
dnscmd dnssvr1.contoso.com /clearcache
```

## <a name="dnscmd-config-command"></a>dnscmd/config 명령

DNS 서버 및 개별 영역에 대 한 레지스트리 값을 변경합니다. 이 명령은 지정 된 서버에 대 한 구성도 수정 합니다. 서버 수준 및 영역 수준 설정을 허용 합니다.

> [!CAUTION]
> 대안이 없는 한 레지스트리를 직접 편집 하지 마십시오. 레지스트리 편집기의 성능이 저하, 하면 시스템이 손상 또는 Windows를 다시 설치 해야 할 수 있는 설정을 허용 표준 보호를 무시 합니다. 제어판 또는 mmc (Microsoft Management Console)의 프로그램을 사용 하 여 대부분의 레지스트리 설정을 안전 하 게 변경할 수 있습니다. 레지스트리를 직접 편집 해야 하는 경우 먼저 백업 합니다. 자세한 내용은 레지스트리 편집기 도움말을 참조 하세요.

### <a name="server-level-syntax"></a>서버 수준 구문

```
dnscmd [<servername>] /config <parameter>
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ---------- | ----------- |
| `<servername>` | 로컬 컴퓨터 구문, IP 주소, FQDN 또는 호스트 이름으로 표시 하려고를 관리 하는 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다. |
| `<parameter>` | 설정을 지정 하 고, 필요에 따라 값입니다. 매개 변수 값은 [*value*] *매개 변수* 구문을 사용 합니다. |
| /addressanswerlimit`[0|5-28]` | DNS 서버가 쿼리에 대 한 응답으로 보낼 수 있는 호스트 레코드의 최대 수를 지정 합니다. 값 영 (0) 이거나 28 레코드를 통해 5의 범위에 있을 수 있습니다. 기본값은 영(0)입니다. |
| /bindsecondaries`[0|1]` | 최대 압축 효과 성과 얻을 수 있도록 영역 전송의 형식을 변경 합니다. 다음 값을 허용 합니다.<ul><li>**0** -최대 압축을 사용 하며 BIND 버전 4.9.4 이상에만 호환 됩니다.</li><li>**1** -Microsoft가 아닌 DNS 서버에 메시지당 하나의 리소스 레코드만 보내고 4.9.4 이전의 BIND 버전과 호환 됩니다. 이 값은 기본 설정입니다.</li></ul> |
| /bootmethod`[0|1|2|3]` | DNS 서버를 구성 정보를 가져오는 소스를 결정 합니다. 다음 값을 허용 합니다.<ul><li>**0** -구성 정보의 원본을 지웁니다.</li><li>**1** -기본적으로 DNS 디렉터리에 있는 바인드 파일에서 로드 `%systemroot%\System32\DNS` 합니다.</li><li>**2** -레지스트리에서 로드 합니다.</li><li>**3** -AD DS 및 레지스트리에서 로드 합니다. 이 값은 기본 설정입니다.</li></ul> |
| /defaultagingstate`[0|1]` | 새로 만든된 영역에서 기본적으로 DNS 청소 기능이 사용 되는지 여부를 결정 합니다. 다음 값을 허용 합니다.<ul><li>**0** -청소를 사용 하지 않습니다. 이 값은 기본 설정입니다.</li><li>**1** -청소를 사용 합니다.</li></ul> |
| /defaultnorefreshinterval`[0x1-0xFFFFFFFF|0xA8]` | 동적으로 업데이트 된 레코드에 대 한 없는 새로 고침 허용 되는 기간을 설정 합니다. 서버에 영역이이 값을 자동으로 상속 합니다.<p>기본값을 변경 하려면의 범위에 값을 입력 **0x1 0xFFFFFFFF**합니다. 서버에서 기본값은 **0xA8**합니다. |
| /defaultrefreshinterval`[0x1-0xFFFFFFFF|0xA8]` | DNS 레코드에 대 한 동적 업데이트에 대해 허용 되는 기간을 설정 합니다. 서버에 영역이이 값을 자동으로 상속 합니다.<p>기본값을 변경 하려면의 범위에 값을 입력 **0x1 0xFFFFFFFF**합니다. 서버에서 기본값은 **0xA8**합니다. |
| /disableautoreversezones`[0|1]` | 역방향 조회 영역을 자동 생성을 사용 하지 않도록 설정 하거나 사용 합니다. 역방향 조회 영역 IP (인터넷 프로토콜) 주소를 DNS 도메인 이름 확인을 제공합니다. 다음 값을 허용 합니다.<ul><li>**0** -역방향 조회 영역을 자동으로 만들 수 있습니다. 이 값은 기본 설정입니다.</li><li>**1** -역방향 조회 영역 자동 생성을 사용 하지 않도록 설정 합니다.</li></ul> |
| /disablensrecordsautocreation`[0|1]` | 여부 DNS 서버가 자동으로 NS (이름 서버) 리소스 레코드를 만듭니다 호스팅하는 영역에 대 한을 지정 합니다. 다음 값을 허용 합니다.<ul><li>**0** -DNS 서버에서 호스팅하는 영역에 대 한 NS (이름 서버) 리소스 레코드를 자동으로 만듭니다.</li><li>**1** -DNS 서버에서 호스팅하는 영역에 대 한 NS (이름 서버) 리소스 레코드를 자동으로 만들지 않습니다.</li></ul> |
| /dspollinginterval`[0-30]` | DNS 서버에서 active directory 통합 영역에 대 한 변경 내용을 AD DS 폴링하는 빈도를 지정 합니다. |
| /dstombstoneinterval`[1-30]` |AD DS에서 삭제 된 레코드를 유지 하는 시간 (초) 시간의 양입니다. |
| /ednscachetimeout`[3600-15724800]` | 확장 DNS (EDNS) 정보가 캐시 되는 시간 (초)을 지정 합니다. 최소값은 **3600**이 고 최대값은 **15724800**입니다. 기본값은 **604800** 초 (1 주)입니다. |
| /enableednsprobes`[0|1]` | 사용 하거나 EDNS를 지원 하는지 확인 하기 위해 다른 서버를 검색 하는 서버를 사용 하지 않도록 설정 합니다. 다음 값을 허용 합니다.<ul><li>**0** -EDNS 프로브에 대해 활성 지원을 사용 하지 않도록 설정 합니다.</li><li>**1** -EDNS 프로브에 대해 활성 지원을 사용 하도록 설정 합니다.</li></ul> |
| /enablednssec`[0|1]` | 사용 하거나 지원에 대 한 보안 확장 DNSSEC (DNS)를 사용 하지 않도록 설정 합니다. 다음 값을 허용 합니다.<ul><li>**0** -DNSSEC를 사용 하지 않습니다.</li><li>**1** -DNSSEC를 사용 하도록 설정 합니다.</li></ul> |
| /enableglobalnamessupport`[0|1]` | 사용 하거나 GlobalNames 영역에 대 한 지원을 사용 하지 않도록 설정 합니다. GlobalNames 영역 포리스트에 단일 레이블 DNS 이름 확인을 지원합니다. 다음 값을 허용 합니다.<ul><li>**0** -GlobalNames 영역에 대 한 지원을 사용 하지 않도록 설정 합니다. 이 명령의 값을 설정 하면 0, DNS 서버 서비스가 단일 레이블 이름을 GlobalNames 영역에서 해결 되지 않습니다.</li><li>**1** -GlobalNames 영역에 대 한 지원을 사용 하도록 설정 합니다. 이 명령의 값을 설정 하면 1, DNS 서버 서비스는 단일 레이블 이름을 GlobalNames 영역에서 해결 합니다.</li></ul> |
| /enableglobalqueryblocklist`[0|1]` | 사용 하거나 목록에서 이름에 대 한 이름 확인을 차단 하는 글로벌 쿼리 차단 목록에 대 한 지원을 사용 하지 않도록 설정 합니다. DNS 서버 서비스를 만들고 서비스를 처음 시작할 때 기본적으로 글로벌 쿼리 차단 목록을 사용 합니다. 현재 글로벌 쿼리 차단 목록을 보려면 dnscmd/info **/globalqueryblocklist** 명령을 사용 합니다. 다음 값을 허용 합니다.<ul><li>**0** -전역 쿼리 차단 목록을 지원 하지 않습니다. 이 명령의 값을 설정 하면 0, DNS 서버 서비스가 차단 목록에는 이름에 대 한 쿼리에 응답 합니다.</li><li>**1** -전역 쿼리 차단 목록을 지원 합니다. 이 명령의 값을 설정 하면 1, DNS 서버 서비스가 차단 목록에는 이름에 대 한 쿼리에 응답 하지 않습니다.</li></ul> |
| /eventloglevel`[0|1|2|4]` | 이벤트는 이벤트 뷰어에서 DNS 서버 로그에 기록 됩니다 결정 합니다. 다음 값을 허용 합니다.<ul><li>**0** -이벤트를 기록 하지 않습니다.</li><li>**1** -오류만 로깅합니다.</li><li>**2** -오류 및 경고만 기록 합니다.</li><li>**4** -오류, 경고 및 정보 이벤트를 기록 합니다. 이 값은 기본 설정입니다.</li></ul> |
| /forward위임`[0|1]` | DNS 서버 위임된 subzone에 대 한 쿼리를 처리 하는 방법을 결정 합니다. 이러한 쿼리는 DNS 서버에 대 한 하거나 참조 하는 쿼리에서 subzone 하 라는 전달자 목록에 보낼 수 있습니다. 설정의 항목 전달이 사용 하는 경우에 사용 됩니다. 다음 값을 허용 합니다.<ul><li>**0** -위임 된 하위 영역을 참조 하는 쿼리를 적절 한 하위 영역으로 자동으로 보냅니다. 이 값은 기본 설정입니다.</li><li>**1** -위임 된 하위 영역을 참조 하는 쿼리를 기존 전달자로 전달 합니다.</li></ul> |
| /forwardingtimeout`[<seconds>]` | 다른 전달자를 시도 하기 전에 DNS 서버가 전달자 응답을 대기 하는**시간 (초)을**결정 합니다. 기본값은 **0x5**, 5 초입니다. |
| /globalneamesqueryorder`[0|1]` | 여부 DNS 서버 서비스는 먼저 검색 GlobalNames 영역 또는 로컬 영역에서 이름을 확인할 때 지정 합니다. 다음 값을 허용 합니다.<ul><li>**0** -DNS 서버 서비스는 신뢰할 수 있는 영역을 쿼리 하기 전에 GlobalNames 영역을 쿼리하여 이름을 확인 하려고 시도 합니다.</li><li>**1** -DNS 서버 서비스가 GlobalNames 영역을 쿼리 하기 전에 권한이 있는 영역을 쿼리하여 이름을 확인 하려고 합니다.</li></ul> |
| /globalqueryblocklist`[[<name> [<name>]...]` | 현재 글로벌 쿼리 차단 목록을으로 지정 하는 이름의 목록을 바꿉니다. 모든 이름을 지정 하지 않으면이 명령은 차단 목록을 지웁니다. 기본적으로 글로벌 쿼리 차단 목록은 다음 항목을 포함 합니다.<ul><li>isatap</li><li>wpad</li></ul>DNS 서버 서비스 경우 제거할 수 이러한 이름 중 하나 또는 모두를 처음 시작할 때 기존 영역에서 이러한 이름을 찾습니다. |
| /isslave`[0|1]` | 전달 하는 쿼리 응답을 받지 때 DNS 서버가 응답 하는 방법을 결정 합니다. 다음 값을 허용 합니다.<ul><li>**0** -DNS 서버가 종속 서버가 아닌 것으로 지정 합니다. 전달자 응답 하지 않을 경우에 DNS 서버 쿼리 자체를 확인 하려고 합니다. 이 값은 기본 설정입니다.</li><li>**1** -DNS 서버가 하위 항목이 되도록 지정 합니다. 전달자 응답 하지 않을 경우 DNS 서버 검색을 종료 하 고 해결 프로그램에 오류 메시지를 보냅니다.</li></ul> |
| /localnetpriority`[0|1]` | DNS 서버에 동일한 이름의 여러 호스트 레코드 호스트 레코드가 반환 되는 순서를 결정 합니다. 다음 값을 허용 합니다.<ul><li>**0** -DNS 데이터베이스에 나열 된 순서 대로 레코드를 반환 합니다.</li><li>**1** -유사한 IP 네트워크 주소를 먼저 포함 하는 레코드를 반환 합니다. 이 값은 기본 설정입니다.</li></ul> |
| /logfilemaxsize`[<size>]` | **0x10000**파일의 최대 크기 (바이트)를 지정 합니다. DNS는 파일이 최대 크기에 도달 하면 가장 오래 된 이벤트를 덮어씁니다. 기본 크기는 **0x400000**입니다 .이 크기는 4mb입니다. |
| /logfilepath`[<path+logfilename>]` | Dns.log 파일의 경로 지정합니다. 기본 경로는 `%systemroot%\System32\Dns\Dns.log`입니다. 형식을 사용 하 여 다른 경로를 지정할 수 있습니다 `path+logfilename` . |
| /logipfilterlist`<IPaddress> [,<IPaddress>...]` | 어떤 패킷이 디버그 로그 파일에 기록 됩니다 지정 합니다. 항목은 IP 주소의 목록입니다. 목록에서 IP 주소에서 이동 하는 패킷이 기록 됩니다. |
| /loglevel`[<eventtype>]` | 이벤트의 유형을 Dns.log 파일에 기록 되는지 결정 합니다. 각 이벤트 종류는 16 진수 숫자로 표현 됩니다. 로그에 하나 이상의 이벤트를 하려는 경우 16 진수 추가 사용 하 여 값을 추가 하려면 합계를 입력 합니다. 다음 값을 허용 합니다.<ul><li>**0x0** -DNS 서버는 로그를 만들지 않습니다. 이것이 기본 항목입니다.</li><li>**0x10** -쿼리 및 알림을 로깅합니다.</li><li>**0x20** -업데이트를 로깅합니다.</li><li>**0xFE** -쿼리가 아닌 트랜잭션 로그를 기록 합니다.</li><li>**0x100** -질문 트랜잭션을 로깅합니다.</li><li>**0x200** -답변을 기록 합니다.</li><li>**0x1000** -로그 전송 패킷을 전달 합니다.</li><li>**0x2000** -패킷을 수신 하는 로그입니다.</li><li>**0x4000** -사용자 데이터 그램 프로토콜 (UDP) 패킷을 기록 합니다.</li><li>**0x8000** -TCP (전송 제어 프로토콜) 패킷을 기록 합니다.</li><li>**0xffff** -모든 패킷을 기록 합니다.</li><li>**0x10000** -active directory 쓰기 트랜잭션을 로깅합니다.</li><li>**0x20000** -active directory 업데이트 트랜잭션을 로깅합니다.</li><li>**0x1000000** -전체 패킷을 기록 합니다.</li><li>**0x80000000** -쓰기-쓰기 트랜잭션을 로깅합니다.</li><li></ul> |
| /maxcachesize | DNS 서버 메모리 캐시의 최대 크기 (KB)를 지정 합니다. |
| /maxcachettl`[<seconds>]` | 캐시에 저장 되는 레코드의 수 (**0X0 0xffffffff**)를 결정 합니다. **0x0** 설정을 사용 하는 경우 DNS 서버는 레코드를 캐시 하지 않습니다. 기본 설정은 **0x15180** (86, 400 초 또는 1 일)입니다. |
| /maxnegativecachettl`[<seconds>]` | 쿼리에 음수 대답을 기록 하는 항목을 DNS 캐시에 저장 된 상태로 유지 하는 초 (**0X1 0xffffffff**)의 수를 지정 합니다. 기본 설정은 **0x384** (900 초)입니다. |
| /namecheckflag`[0|1|2|3]` | DNS 이름을 확인할 때 사용 하는 문자 표준 지정 합니다. 다음 값을 허용 합니다.<ul><li>**0** -Rfc (Internet 공학적 작업 force)를 준수 하는 ANSI 문자를 사용 합니다.</li><li>**1** -IETF rfc를 준수 하지 않아도 되는 ANSI 문자를 사용 합니다.</li><li>**2** -멀티 바이트 UCS 변환 형식 8 (utf-8) 문자를 사용 합니다. 이 값은 기본 설정입니다.</li><li>**3** -모든 문자를 사용 합니다.</li></ul> |
| /norecursion`[0|1]` | DNS 서버 재귀적 이름 확인을 수행 하는지 여부를 결정 합니다. 다음 값을 허용 합니다.<ul><li>**0** -쿼리에서 요청 된 경우 DNS 서버에서 재귀적 이름 확인을 수행 합니다. 이 값은 기본 설정입니다.</li><li>**1** -DNS 서버는 재귀적 이름 확인을 수행 하지 않습니다.</li></ul> |
| /notcp | 이 매개 변수는 더 이상 현재 버전의 Windows Server 효과가 없습니다. |
| /recursionretry`[<seconds>]` | DNS 서버가 원격 서버에 연결을 다시 시도 하기 전에 대기 하는**시간 (초)을**결정 합니다. 기본 설정은 **0x3** (3 초)입니다. 재귀 속도가 느린 광역 네트워크 (WAN) 링크를 통해 발생 하는 경우이 값을 늘려야 합니다. |
| /recursiontimeout`[<seconds>]` | 중단가 원격 서버에 연결을 시도 하기 전에 DNS 서버가 대기 하는**시간 (초)을**결정 합니다. 설정 범위에서 **0x1** 통해 **0xFFFFFFFF**합니다. 기본 설정은 **0xF** (15 초)입니다. 재귀 느린 WAN 링크를 통해 발생 하는 경우이 값을 늘려야 합니다. |
| /roundrobin`[0|1]` | 서버에 동일한 이름의 여러 호스트 레코드 때 호스트 레코드가 반환 됩니다 순서를 결정 합니다. 다음 값을 허용 합니다.<ul><li>**0** -DNS 서버에서 라운드 로빈을 사용 하지 않습니다. 대신, 모든 쿼리에 첫 번째 레코드를 반환 합니다.</li><li>**1** -DNS 서버는 반환 되는 레코드를 일치 하는 레코드 목록의 맨 위에서 아래로 회전 합니다. 이 값은 기본 설정입니다.</li></ul> |
| /rpcprotocol`[0x0|0x1|0x2|0x4|0xFFFFFFFF]` | 원격 프로시저 호출 (RPC)은 DNS 서버에서 연결을 사용 하는 프로토콜을 지정 합니다. 다음 값을 허용 합니다.<ul><li>**0x0** -DNS에 대해 RPC를 사용 하지 않도록 설정 합니다.</li><li>**0x01** -Tcp/ip를 사용 합니다.</li><li>**0x2** -명명 된 파이프를 사용 합니다.</li><li>**0x4** -LPC (로컬 프로시저 호출)를 사용 합니다.</li><li>**0xffffffff** -모든 프로토콜입니다. 이 값은 기본 설정입니다.</li></ul> |
| /scavenginginterval`[<hours>]` | DNS 서버에 대 한 청소 기능이 사용 되는지 여부를 확인 하 고 청소 주기 사이의 시간 (**0X0 0xffffffff**) 수를 설정 합니다. 기본 설정은 **0x0**, DNS 서버에 대 한 청소를 해제 합니다. 설정 보다 큰 **0x0** 서버에 대 한 청소 하 고 청소 주기 사이의 시간을 설정 합니다. |
| /secureresponses`[0|1]` | DNS 캐시에 저장 된 레코드를 필터링 하는지 여부를 결정 합니다. 다음 값을 허용 합니다.<ul><li>**0** -이름 쿼리에 대 한 모든 응답을 캐시에 저장 합니다. 이 값은 기본 설정입니다.</li><li>**1** -동일한 DNS 하위 트리에 속한 레코드만 캐시에 저장 합니다.</li></ul> |
| /송신 포트`[<port>]` | DNS가 다른 DNS 서버에 재귀 쿼리를 전송 하는 데 사용 하는 포트 번호 (**0X0 0xffffffff**)를 지정 합니다. 기본 설정은 **0x0**, 즉, 포트 번호 임의로 선택 합니다. |
| /serverlevelplugindll`[<dllpath>]` | 사용자 지정 플러그 인의 경로 지정합니다. Dllpath가 유효한 DNS 서버 플러그 인의 정규화 된 경로 이름을 지정 하는 경우 DNS 서버는 플러그 인의 함수를 호출 하 여 로컬로 호스트 된 모든 영역 범위를 벗어난 이름 쿼리를 확인 합니다. 쿼리 이름이 플러그인의 범위를 벗어난 경우 DNS 서버가 구성 된 대로 전달 또는 재귀를 사용 하 여 이름 확인을 수행 합니다. Dllpath를 지정 하지 않으면 사용자 지정 플러그 인이 이전에 구성 된 경우 DNS 서버에서 사용자 지정 플러그 인을 사용 하지 않습니다. |
| /strictfileparsing`[0|1]` | 영역을 로드 하는 동안 잘못 된 레코드를 발견 한 경우 DNS 서버의 동작을 결정 합니다. 다음 값을 허용 합니다.<ul><li>**0** -서버에서 잘못 된 레코드를 발견 하더라도 DNS 서버가 영역을 계속 로드 합니다. 이 오류는 DNS 로그에 기록 됩니다. 이 값은 기본 설정입니다.</li><li>**1** -dns 서버는 영역 로드를 중지 하 고 dns 로그에 오류를 기록 합니다.</li></ul> |
| /updateoptions`<RecordValue>` | 지정 된 유형의 레코드의 동적 업데이트를 금지합니다. 로그에서 허용 하지 않도록 둘 이상의 레코드 종류를 하려는 경우 16 진수 추가 사용 하 여 값을 추가 하려면 합계를 입력 합니다. 다음 값을 허용 합니다.<ul><li>**0x0** -레코드 형식을 제한 하지 않습니다.</li><li>**0x1** -SOA (권한 시작) 리소스 레코드를 제외 합니다.</li><li>**0x2** -이름 서버 (NS) 리소스 레코드를 제외 합니다.</li><li>**0x4** -이름 서버 (NS) 리소스 레코드의 위임을 제외 합니다.</li><li>**0x8** -서버 호스트 레코드를 제외 합니다.</li><li>**0x100** -보안 동적 업데이트 중 SOA (권한 시작) 리소스 레코드를 제외 합니다.</li><li>**0x200** -보안 동적 업데이트 중 루트 이름 서버 (NS) 리소스 레코드를 제외 합니다.</li><li>**0X30f** -표준 동적 업데이트 중에 이름 서버 (NS) 리소스 레코드, SOA (권한 시작) 리소스 레코드 및 서버 호스트 레코드를 제외 합니다. 보안 동적 업데이트 중 루트 이름 서버 (NS) 리소스 레코드와 SOA (권한 시작) 리소스 레코드를 제외 합니다. 위임 하 고, 서버 업데이트를 호스트 합니다.</li><li>**0x400** -보안 동적 업데이트 중에는 위임 이름 서버 (NS) 리소스 레코드를 제외 합니다.</li><li>**0x800** -보안 동적 업데이트 중 서버 호스트 레코드를 제외 합니다.</li><li>**0x1000000** -위임 서명자 (DS) 레코드를 제외 합니다.</li><li>**0x80000000** -DNS 동적 업데이트를 사용 하지 않도록 설정 합니다.</li></ul> |
| /writeauthorityns`[0|1]` | DNS 서버는 응답의 기관 섹션에 이름 서버 (NS) 리소스 레코드를 기록 하는 시기를 결정 합니다. 다음 값을 허용 합니다.<ul><li>**0** -조회 전용 기관 섹션에 이름 서버 (NS) 리소스 레코드를 씁니다. 이 설정은 Rfc 1034, 도메인 이름 개념 및 기능을 준수 하 고 Rfc 2181을 사용 하 여 DNS 사양에 대해 설명 합니다. 이 값은 기본 설정입니다.</li><li>**1** -모든 성공한 신뢰할 수 있는 응답의 기관 섹션에 이름 서버 (NS) 리소스 레코드를 씁니다.</li></ul> |
| /xfrconnecttimeout`[<seconds>]` | 주 DNS 서버가 보조 서버의 전송 응답을 대기 하는**시간 (초)을 결정**합니다. 기본값은 **0x1E** (30 초)입니다. 시간 제한 값이 만료 되 면 연결이 종료 됩니다. |

### <a name="zone-level-syntax"></a>영역 수준 구문

지정된 된 영역의 구성을 수정합니다. 영역 이름 매개 변수 영역 수준에 대해서만 지정 되어야 합니다.

```
dnscmd /config <parameters>
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ---------- | ----------- |
| `<parameter>` | 영역 이름 및 값을 옵션으로는 설정을 지정 합니다. 매개 변수 값은 구문을 사용 `zonename parameter [value]` 합니다. |
| /aging`<zonename>`| 사용 하거나 특정 영역에 청소를 사용 하지 않도록 설정 합니다. |
| /allownsrecordsautocreation `<zonename>``[value]` | DNS 서버 이름 서버 (NS) 리소스 레코드 autocreation 설정 보다 우선 합니다. 이 영역에 대 한 이전에 등록 된 이름 서버 (NS) 리소스 레코드의 영향을 받지 않습니다. 따라서를 수동으로 제거 해야 하지 않을 경우 해당 합니다. |
| /allowupdate`<zonename>` | 지정된 된 영역 동적 업데이트를 허용 하는지 여부를 결정 합니다. |
| /forwarderslave`<zonename>` | DNS 서버 재정의 **/isslave** 설정 합니다. |
| /forwardertimeout`<zonename>` | 초 단위 시간 전달자 다른 전달자를 시도 하기 전에 응답을 기다리는 DNS 영역 결정 합니다. 이 값은 서버 수준에서 설정 하는 값을 재정의 합니다. |
| /norefreshinterval`<zonename>` | 이때 없는 새로 고침 동적으로 업데이트할 수는 지정 된 영역에서 DNS 레코드를 영역에 대 한 시간 간격을 설정 합니다. |
| /refreshinterval`<zonename>` | 새로 고침 동적으로 업데이트할 수는 지정 된 영역에서 DNS 레코드를 영역에 대 한 시간 간격을 설정 합니다. |
| /securesecondaries`<zonename>` | 이 영역에 대 한 마스터 서버에서 영역 업데이트를 받을 수 있는 보조 서버를 결정 합니다. |

## <a name="dnscmd-createbuiltindirectorypartitions-command"></a>dnscmd/createbuiltindirectorypartitions 명령

DNS 애플리케이션 디렉터리 파티션을 만듭니다. DNS가 설치 되는 서비스에 대 한 애플리케이션 디렉터리 파티션은 포리스트 및 도메인 수준에서 생성 됩니다. 이 명령을 사용 하 여 삭제 되거나 생성 되지 않고 된 DNS 애플리케이션 디렉터리 파티션을 만들 수 있습니다. 사용 하 여,이 명령은 도메인에 대 한 기본 제공 DNS 디렉터리 파티션을 만듭니다.

### <a name="syntax"></a>구문

```
dnscmd [<servername>] /createbuiltindirectorypartitions [/forest] [/alldomains]
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ---------- | ----------- |
| `<servername>` | IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다. |
| /forest | 포리스트에 대 한 DNS 디렉터리 파티션을 만듭니다. |
| /alldomains | 포리스트의 모든 도메인에 대 한 DNS 파티션을 만듭니다. |

## <a name="dnscmd-createdirectorypartition-command"></a>dnscmd/createdirectorypartition 명령

DNS 애플리케이션 디렉터리 파티션을 만듭니다. DNS가 설치 되는 서비스에 대 한 애플리케이션 디렉터리 파티션은 포리스트 및 도메인 수준에서 생성 됩니다. 이 작업에는 추가 DNS 애플리케이션 디렉터리 파티션을 만듭니다.

### <a name="syntax"></a>구문

```
dnscmd [<servername>] /createdirectorypartition <partitionFQDN>
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ---------- | ----------- |
| `<servername>` | IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다. |
| `<partitionFQDN>` | 생성 되는 DNS 애플리케이션 디렉터리 파티션의 FQDN입니다. |

## <a name="dnscmd-deletedirectorypartition-command"></a>dnscmd/deletedirectorypartition 명령

기존 DNS 애플리케이션 디렉터리 파티션을 제거합니다.

### <a name="syntax"></a>구문

```
dnscmd [<servername>] /deletedirectorypartition <partitionFQDN>
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ---------- | ----------- |
| `<servername>` | IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다. |
| `<partitionFQDN>` | DNS 애플리케이션 디렉터리 파티션 제거 될의 FQDN입니다. |

## <a name="dnscmd-directorypartitioninfo-command"></a>dnscmd/directorypartitioninfo 명령

지정 된 DNS 애플리케이션 디렉터리 파티션에 대 한 정보를 나열합니다.

### <a name="syntax"></a>구문

```
dnscmd [<servername>] /directorypartitioninfo <partitionFQDN> [/detail]
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ---------- | ----------- |
| `<servername>` | IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다. |
| `<partitionFQDN>` | DNS 애플리케이션 디렉터리 파티션에의 FQDN입니다. |
| /detail | 애플리케이션 디렉터리 파티션에 대 한 모든 정보를 나열합니다. |

## <a name="dnscmd-enlistdirectorypartition-command"></a>dnscmd/enlistdirectorypartition 명령

지정 된 디렉터리 파티션의 복제 세트에 DNS 서버를 추가합니다.

### <a name="syntax"></a>구문

```
dnscmd [<servername>] /enlistdirectorypartition <partitionFQDN>
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ---------- | ----------- |
| `<servername>` | IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다. |
| `<partitionFQDN>` | DNS 애플리케이션 디렉터리 파티션에의 FQDN입니다. |

## <a name="dnscmd-enumdirectorypartitions-command"></a>dnscmd/enumdirectorypartitions 명령

지정된 된 서버에 대 한 DNS 애플리케이션 디렉터리 파티션을 나열합니다.

### <a name="syntax"></a>구문

```
dnscmd [<servername>] /enumdirectorypartitions [/custom]
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ---------- | ----------- |
| `<servername>` | IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다. |
| / 사용자 지정 | 사용자가 만든 디렉터리 파티션으로 나열합니다. |

## <a name="dnscmd-enumrecords-command"></a>dnscmd/enumrecords 명령

DNS 영역에 있는 지정 된 노드의 리소스 레코드를 나열합니다.

### <a name="syntax"></a>구문

```
dnscmd [<servername>] /enumrecords <zonename> <nodename> [/type <rrtype> <rrdata>] [/authority] [/glue] [/additional] [/node | /child | /startchild<childname>] [/continue | /detail]
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ---------- | ----------- |
| `<servername>` | IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다. |
| /enumrecords | 지정된 된 영역에서 리소스 레코드를 나열합니다. |
| `<zonename>` | 리소스 레코드가 속해 있는 영역의 이름을 지정 합니다. |
| `<nodename>` | 리소스 레코드의 노드 이름을 지정합니다. |
| `[/type <rrtype> <rrdata>]` | 나열 될 리소스 레코드의 유형 및 예상 되는 데이터의 유형을 지정 합니다. 다음 값을 허용 합니다.<ul><li>`<rrtype>`-나열 될 리소스 레코드의 유형을 지정 합니다.</li><li>`<rrdata>`-예상 레코드가 되는 데이터의 형식을 지정 합니다.</li></ul> |
| /authority | 신뢰할 수 있는 데이터를 포함합니다. |
| /glue | 붙이기 데이터가 포함 됩니다. |
| 추가 / | 나열 된 리소스 레코드에 대 한 모든 추가 정보를 포함 합니다. |
| /node | 지정 된 노드의 리소스 레코드를 나열합니다. |
| /child | 지정 된 하위 도메인의 리소스 레코드를 나열합니다. |
| /startchild`<childname>` | 위에 있는 목록에서 지정한 자식 도메인을 시작합니다. |
| 계속 해 서 / | 유형 및 데이터는 리소스 레코드를 나열합니다. |
| /detail | 리소스 레코드에 대 한 모든 정보를 나열합니다. |

#### <a name="example"></a>예제

```
dnscmd /enumrecords test.contoso.com test /additional
```

## <a name="dnscmd-enumzones-command"></a>dnscmd/sumzones 명령

지정된 된 DNS 서버에 존재 하는 영역을 나열 합니다. **enumzones** 매개 변수 영역 목록에 대 한 필터로 작동 합니다. 필터가 지정 된 영역의 전체 목록이 반환 됩니다. 필터를 지정 하는 경우 해당 필터 조건을 충족 하는 영역만 영역의 반환된 목록에 포함 됩니다.

### <a name="syntax"></a>구문

```
dnscmd [<servername>] /enumzones [/primary | /secondary | /forwarder | /stub | /cache | /auto-created] [/forward | /reverse | /ds | /file] [/domaindirectorypartition | /forestdirectorypartition | /customdirectorypartition | /legacydirectorypartition | /directorypartition <partitionFQDN>]
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ---------- | ----------- |
| `<servername>` | IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다. |
| /primary | 표준 기본 영역 또는 active directory 통합 영역인 모든 영역을 나열 합니다. |
| 보조 / | 모든 표준 보조 영역을 나열합니다. |
| /forwarder | 다른 DNS 서버에 해결 되지 않은 쿼리를 전달 하는 영역을 나열 합니다. |
| /stub | 모든 스텁 영역을 나열합니다. |
| 캐시 / | 캐시에 로드 되는 영역을 나열 합니다. |
| /자동 생성] | DNS 서버를 설치할 때 자동으로 생성 된 영역을 나열 합니다. |
| / 앞으로 | 정방향 조회 영역을 나열 합니다. |
| 역방향 / | 역방향 조회 영역을 나열 합니다. |
| /ds | Active directory 통합 영역을 나열 합니다. |
| /file | 파일에 백업 하는 영역을 나열 합니다. |
| /domaindirectorypartition | 도메인 디렉터리 파티션에 저장 된 영역을 나열 합니다. |
| /forestdirectorypartition | 포리스트의 DNS 애플리케이션 디렉터리 파티션에 저장 된 영역을 나열 합니다. |
| /customdirectorypartition | 사용자 정의 애플리케이션 디렉터리 파티션에 저장 된 모든 영역을 나열 합니다. |
| /legacydirectorypartition | 도메인 디렉터리 파티션에 저장 된 모든 영역을 나열 합니다. |
| /directorypartition`<partitionFQDN>` | 지정된 된 디렉터리 파티션에 저장 된 모든 영역을 나열 합니다. |

#### <a name="examples"></a>예

- [예 2: DNS 서버에 전체 영역 목록 표시](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc784399(v=ws.10)#example-2-display-a-complete-list-of-zones-on-a-dns-server)

- [예 3: DNS 서버에서 자동 생성 된 영역 목록 표시](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc784399(v=ws.10)#example-3-display-a-list-of-autocreated-zones-on-a-dns-server)

## <a name="dnscmd-exportsettings-command"></a>dnscmd/exportsettings 명령

DNS 서버 구성 세부 정보를 나열 하는 텍스트 파일을 만듭니다. 텍스트 파일의 이름은 *DnsSettings.txt*입니다. `%systemroot%\system32\dns`서버 디렉터리에 있습니다. 파일에 정보를 사용할 수 있는 **dnscmd /exportsettings** 구성 문제를 해결 하거나 여러 서버를 동일 하 게 구성 되도록 만듭니다.

### <a name="syntax"></a>구문

```
dnscmd [<servername>] /exportsettings
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ---------- | ----------- |
| `<servername>` | IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다. |

## <a name="dnscmd-info-command"></a>dnscmd/info 명령

지정 된 서버 레지스트리의 DNS 섹션에서 설정을 표시 `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\DNS\Parameters` 합니다. 영역 수준 레지스트리 설정을 표시 하려면 `dnscmd zoneinfo` 명령을 사용 합니다.

### <a name="syntax"></a>구문

```
dnscmd [<servername>] /info [<settings>]
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ---------- | ----------- |
| `<servername>` | IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다. |
| `<settings>` | 값으로 설정 하는 **정보** 명령 반환을 개별적으로 지정할 수 있습니다. 설정을 지정 하지 않으면 일반 설정에 대 한 보고서를 반환 됩니다. |

#### <a name="example"></a>예제

- [예 4: DNS 서버에서 IsSlave 설정 표시](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc784399(v=ws.10)#example-4-display-the-isslave-setting-from-a-dns-server)

- [예 5: DNS 서버에서 RecursionTimeout 설정 표시](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc784399(v=ws.10)#example-5-display-the-recursiontimeout-setting-from-a-dns-server)

## <a name="dnscmd-ipvalidate-command"></a>dnscmd/ipvalidate 명령

작동 중인 DNS 서버 또는 DNS 서버 역할을 전달자, 루트 힌트 서버 또는 특정 영역에 대 한 마스터 서버 할 수 있는지 여부를 식별 하는 IP 주소 인지 테스트 합니다.

### <a name="syntax"></a>구문

```
dnscmd [<servername>] /ipvalidate <context> [<zonename>] [[<IPaddress>]]
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ---------- | ----------- |
| `<servername>` | IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다. |
| `<context>` | 수행 하는 테스트의 유형을 지정 합니다. 다음 테스트를 지정할 수 있습니다.<ul><li>**/dnsservers** -지정한 주소를 가진 컴퓨터가 DNS 서버에서 작동 하는지 테스트 합니다.</li><li>**/cers** -지정 하는 주소가 전달자 역할을 할 수 있는 DNS 서버를 식별 하는지 테스트 합니다.</li><li>**/roothints** -지정한 주소가 루트 힌트 이름 서버 역할을 할 수 있는 DNS 서버를 식별 하는지 테스트 합니다.</li><li>**/zonemers** -지정한 주소가 *zonename*의 마스터 서버인 DNS 서버를 식별 하는지 테스트 합니다. |
| `<zonename>` | 영역을 식별합니다. 이 매개 변수를 사용 하는 **/zonemasters** 매개 변수입니다. |
| `<IPaddress>` | 이 명령은 테스트 하는 IP 주소를 지정 합니다. |

#### <a name="examples"></a>예

```
nscmd dnssvr1.contoso.com /ipvalidate /dnsservers 10.0.0.1 10.0.0.2
dnscmd dnssvr1.contoso.com /ipvalidate /zonemasters corp.contoso.com 10.0.0.2
```

## <a name="dnscmd-nodedelete-command"></a>dnscmd/nodedelete 명령

지정된 된 호스트에 대 한 모든 레코드를 삭제합니다.

### <a name="syntax"></a>구문

```
dnscmd [<servername>] /nodedelete <zonename> <nodename> [/tree] [/f]
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ---------- | ----------- |
| `<servername>` | IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다. |
| `<zonename>` |  영역 이름을 지정합니다. |
| `<nodename>` | 삭제할 노드의 호스트 이름을 지정 합니다. |
| /tree | 모든 자식 레코드를 삭제 합니다. |
| /f | 확인을 요청 하지 않고 명령을 실행 합니다. |

#### <a name="example"></a>예제

[예제 6: 노드에서 레코드 삭제](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc784399(v=ws.10)#example-6-delete-the-records-from-a-node)

## <a name="dnscmd-recordadd-command"></a>dnscmd/recordadd 명령

DNS 서버에 지정된 된 시간대에 레코드를 추가합니다.

### <a name="syntax"></a>구문

```
dnscmd [<servername>] /recordadd <zonename> <nodename> <rrtype> <rrdata>
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ---------- | ----------- |
| `<servername>` | IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다. |
| `<zonename>` |  레코드가 있는 영역을 지정 합니다. |
| `<nodename>` |  영역에서 특정 노드를 지정합니다. |
| `<rrtype>` |  레코드를 추가 하려면 유형을 지정 합니다.  |
| `<rrdata>` | 예상 되는 데이터의 형식을 지정 합니다. |

> [!NOTE]
> 레코드를 추가한 후 올바른 데이터 형식 및 데이터 형식을 사용 하는지 확인 합니다. 리소스 레코드 유형 및 적합 한 데이터 형식 목록은 [Dnscmd 예](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc784399(v=ws.10))를 참조 하세요.

#### <a name="examples"></a>예

```
dnscmd dnssvr1.contoso.com /recordadd test A 10.0.0.5
dnscmd /recordadd test.contoso.com test MX 10 mailserver.test.contoso.com
```

## <a name="dnscmd-recorddelete-command"></a>dnscmd/recorddelete 명령

지정 된 영역에 대 한 리소스 레코드를 삭제 합니다.

### <a name="syntax"></a>구문

```
dnscmd [<servername>] /recorddelete <zonename> <nodename> <rrtype> <rrdata> [/f]
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ---------- | ----------- |
| `<servername>` | IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다. |
| `<zonename>` |  리소스 레코드가 있는 영역을 지정 합니다. |
| `<nodename>` | 호스트의 이름을 지정 합니다. |
| `<rrtype>` |  삭제할 리소스 레코드 종류를 지정 합니다. |
| `<rrdata>` | 예상 되는 데이터의 형식을 지정 합니다. |
| /f | 확인을 요청 하지 않고 명령을 실행 합니다. 노드가 둘 이상의 리소스 레코드를 가질 수 있기 때문에이 명령을 사용 하려면 삭제할 리소스 레코드의 형식에 대해 매우 구체적 이어야 합니다. 데이터 형식을 지정 하 고 리소스 레코드 데이터의 형식을 지정 하지 않으면 지정 된 노드에 대 한 특정 데이터 형식의 모든 레코드가 삭제 됩니다. |

#### <a name="examples"></a>예

```
dnscmd /recorddelete test.contoso.com test MX 10 mailserver.test.contoso.com
```

## <a name="dnscmd-resetforwarders-command"></a>dnscmd/resetforwarders 명령

DNS 서버를 전달 하 DNS 쿼리에 로컬에서 확인할 수 없는 경우 IP 주소를 다시 설정 하거나 선택 합니다.

### <a name="syntax"></a>구문

```
dnscmd [<servername>] /resetforwarders <IPaddress> [,<IPaddress>]...][/timeout <timeout>] [/slave | /noslave]
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ---------- | ----------- |
| `<servername>` | IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다. |
| `<IPaddress>` | DNS 서버에서 확인 되지 않은 쿼리를 전달 하는 IP 주소를 나열 합니다. |
| /timeout`<timeout>` | DNS 서버가 전달자의 응답을 기다리는 시간 (초)을 설정 합니다. 기본적으로이 값은 5 초입니다. |
| 슬레이브/ | 전달 자가 쿼리를 확인 하지 못하는 경우 DNS 서버가 자체 반복 쿼리를 수행 하지 않도록 합니다. |
| /noslave | DNS 서버가 전달자 쿼리를 해결 하지 못하는 경우 자체 반복 쿼리를 수행할 수 있습니다. 이 값은 기본 설정입니다. |
| /f | 확인을 요청 하지 않고 명령을 실행 합니다. 노드가 둘 이상의 리소스 레코드를 가질 수 있기 때문에이 명령을 사용 하려면 삭제할 리소스 레코드의 형식에 대해 매우 구체적 이어야 합니다. 데이터 형식을 지정 하 고 리소스 레코드 데이터의 형식을 지정 하지 않으면 지정 된 노드에 대 한 특정 데이터 형식의 모든 레코드가 삭제 됩니다. |

##### <a name="remarks"></a>설명

- 기본적으로 DNS 서버는 쿼리를 확인할 수 없을 때 반복 쿼리를 수행 합니다.

- **Resetforwarders** 명령을 사용 하 여 IP 주소를 설정 하면 dns 서버가 지정 된 IP 주소의 dns 서버에 대 한 재귀 쿼리를 수행 합니다. 전달 자가 쿼리를 확인 하지 않으면 DNS 서버에서 자체 반복 쿼리를 수행할 수 있습니다.

- **슬레이브/** 매개 변수를 사용 하는 경우 DNS 서버는 자체 반복 쿼리를 수행 하지 않습니다. 즉, DNS 서버 목록에서 DNS 서버에만 확인할 수 없는 쿼리를 전달 하 고 전달자에서 해결 되지 않으면 반복 쿼리를 시도 하지 않습니다. 전달자 DNS 서버에 대 한 IP 주소를 설정 하는 더 효율적입니다. 사용할 수는 **resetforwarders** 의 해결 되지 않은 쿼리는 외부에 연결 하는 DNS 서버를 전달 하는 네트워크의 내부 서버에 대 한 도움말입니다.

- 전달자의 IP 주소를 두 번 나열 하면 DNS 서버가 해당 서버를 두 번 전달 하려고 시도 합니다.

#### <a name="examples"></a>예

```
dnscmd dnssvr1.contoso.com /resetforwarders 10.0.0.1 /timeout 7 /slave
dnscmd dnssvr1.contoso.com /resetforwarders /noslave
```

## <a name="dnscmd-resetlistenaddresses-command"></a>dnscmd/resetlistenaddresses 명령

DNS 클라이언트 요청을 수신 하는 서버의 IP 주소를 지정 합니다. 기본적으로 DNS 서버의 모든 IP 주소는 클라이언트 DNS 요청을 수신 대기 합니다.

### <a name="syntax"></a>구문

```
dnscmd [<servername>] /resetlistenaddresses <listenaddress>
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ---------- | ----------- |
| `<servername>` | IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다. |
| `<listenaddress>` | DNS 클라이언트 요청을 수신 하는 DNS 서버의 IP 주소를 지정 합니다. 없는 수신 주소를 지정 하는 경우 모든 IP 주소가 서버에서 클라이언트 요청을 기다리고 있습니다. |

#### <a name="examples"></a>예

```
dnscmd dnssvr1.contoso.com /resetlistenaddresses 10.0.0.1
```

## <a name="dnscmd-startscavenging-command"></a>dnscmd/start청소 명령

지정 된 DNS 서버에서 부실 리소스 레코드에 대 한 즉시 검색을 시도 하도록 DNS 서버를 알려 줍니다.

### <a name="syntax"></a>구문

```
dnscmd [<servername>] /startscavenging
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ---------- | ----------- |
| `<servername>` | IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다. |

##### <a name="remarks"></a>설명

- 이 명령이 성공적으로 완료 되 면 청소를 즉시 시작 합니다. 청소에 실패 하는 경우 경고 메시지가 표시 되지 않습니다.

- 청소를 시작 하는 명령이 성공적으로 완료 된 것 처럼 보이지만 다음 사전 조건을 충족 하지 않으면 청소를 시작 하지 않습니다.

    - 서버와 영역 모두에 대해 청소를 사용할 수 있습니다.

    - 영역이 시작 됩니다.

    - 리소스 레코드에는 타임 스탬프가 있습니다.

- 서버에 대 한 청소를 사용 하도록 설정 하는 방법에 대 한 자세한 내용은 **/config** 섹션의 **서버 수준 구문** 에서 **scavenginginterval** 매개 변수를 참조 하세요.

- 영역에 대 한 청소를 사용 하도록 설정 하는 방법에 대 한 자세한 내용은 **/config** 섹션의 **영역 수준 구문** 에서 **에이징을** 매개 변수를 참조 하세요.

- 일시 중지 된 영역을 다시 시작 하는 방법에 대 한 자세한 내용은이 문서의 **zoneresume** 매개 변수를 참조 하세요.

- 타임 스탬프에 대 한 리소스 레코드를 확인 하는 방법에 대 한 자세한 내용은이 문서의 **ageallrecords** 매개 변수를 참조 하세요.

#### <a name="examples"></a>예

```
dnscmd dnssvr1.contoso.com /startscavenging
```

## <a name="dnscmd-statistics-command"></a>dnscmd/statistics 명령

표시 하거나 지정 된 DNS 서버에 대 한 데이터를 지웁니다.

### <a name="syntax"></a>구문

```
dnscmd [<servername>] /statistics [<statid>] [/clear]
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ---------- | ----------- |
| `<servername>` | IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다. |
| `<statid>` |  통계 또는 표시 하는 통계의 조합을 지정 합니다. **Statistics** 명령은 시작 되거나 다시 시작 될 때 DNS 서버에서 시작 하는 카운터를 표시 합니다. Id 번호는 통계를 식별 하는 데 사용 됩니다. 없는 통계 ID 번호를 지정 하면 모든 통계가 표시 됩니다. 표시 되는 해당 통계와 함께 지정할 수 있는 숫자는 다음을 포함할 수 있습니다.<ul><li>**00000001** -시간</li><li>**00000002** -쿼리</li><li>**00000004** -쿼리 2</li><li>**00000008** -재귀</li><li>**00000010** -마스터</li><li>**00000020** -보조</li><li>**00000040** -WINS</li><li>**00000100** -업데이트</li><li>**00000200** -SkwanSec</li><li>**00000400** -Ds</li><li>**00010000** -메모리</li><li>**00100000** -PacketMem</li><li>**00040000** -Dbase</li><li>**00080000** -레코드</li><li>**00200000** -NbstatMem</li><li>**/clear** -지정 된 통계 카운터를 0으로 다시 설정 합니다.</li></ul> |

#### <a name="examples"></a>예

- [예 7:](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc784399(v=ws.10)#example-7-display-time-statistics-for-a-dns-server)

- [예 8: DNS 서버에 대 한 NbstatMem 통계 표시](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc784399(v=ws.10)#example-8-display-nbstatmem-statistics-for-a-dns-server)

## <a name="dnscmd-unenlistdirectorypartition-command"></a>dnscmd/unenlistdirectorypartition 명령

지정 된 디렉터리 파티션의 복제 세트에서 DNS 서버를 제거합니다.

### <a name="syntax"></a>구문

```
dnscmd [<servername>] /unenlistdirectorypartition <partitionFQDN>
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ---------- | ----------- |
| `<servername>` | IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다. |
| `<partitionFQDN>` | DNS 애플리케이션 디렉터리 파티션 제거 될의 FQDN입니다. |

## <a name="dnscmd-writebackfiles-command"></a>dnscmd/writebackfiles 명령

변경 내용에 대한 DNS 서버 메모리를 확인하고 영구 스토리지에 씁니다. **Writebackfiles** 명령은 모든 더티 영역 또는 지정 된 영역을 업데이트 합니다. 영구적 저장소에 아직 기록 되지 않은 메모리에 변경 내용이 있는 경우 영역은 변경 되지 않습니다. 모든 영역을 확인 하는 서버 수준 작업입니다. 이 작업에 한 영역을 지정 하거나 사용할 수는 **zonewriteback** 작업 합니다.

### <a name="syntax"></a>구문

```
dnscmd [<servername>] /writebackfiles <zonename>
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ---------- | ----------- |
| `<servername>` | IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다. |
| `<zonename>` | 업데이트할 영역의 이름을 지정 합니다. |

#### <a name="examples"></a>예

```
dnscmd dnssvr1.contoso.com /writebackfiles
```

## <a name="dnscmd-zoneadd-command"></a>dnscmd/zoneadd 명령

DNS 서버에 영역을 추가합니다.

### <a name="syntax"></a>구문

```
dnscmd [<servername>] /zoneadd <zonename> <zonetype> [/dp <FQDN> | {/domain | enterprise | legacy}]
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ---------- | ----------- |
| `<servername>` | IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다. |
| `<zonename>` |  영역 이름을 지정합니다. |
| `<zonetype>` |  만들 영역 유형을 지정 합니다. **/전달자** 또는 **/dsforwarder** 영역 형식을 지정 하면 조건부 전달을 수행 하는 영역이 생성 됩니다. 각 영역 유형에는 다음과 같은 다른 필수 매개 변수가 있습니다.<ul><li>**/dsprimary** -active directory 통합 영역을 만듭니다.</li><li>**/기본/file `<filename>` ** -표준 기본 영역을 만들고 영역 정보를 저장 하는 파일의 이름을 지정 합니다.</li><li>**/보조 `<masterIPaddress> [<masterIPaddress>...]` ** -표준 보조 영역을 만듭니다.</li><li>**/stub `<masterIPaddress> [<masterIPaddress>...]` /file `<filename>` ** -파일 지원 스텁 영역을 만듭니다.</li><li>**/dsstub `<masterIPaddress> [<masterIPaddress>...]` ** -Active directory 통합 스텁 영역을 만듭니다.</li><li>**/ch... `<masterIPaddress> [<masterIPaddress>]` /file `<filename>` ** -생성 된 영역에서 확인 되지 않은 쿼리를 다른 DNS 서버로 전달 하도록 지정 합니다.</li><li>**/dsforwarder** -생성 된 active directory 통합 영역에서 확인 되지 않은 쿼리를 다른 DNS 서버에 전달 하도록 지정 합니다.</li></ul> |
| `<FQDN>` | 디렉터리 파티션의 FQDN을 지정 합니다. |
| /domain | 도메인 디렉터리 파티션에 영역을 저장 합니다. |
| /enterprise | 엔터프라이즈 디렉터리 파티션에 영역을 저장 합니다. |
| /legacy | 레거시 디렉터리 파티션에서 영역을 저장합니다. |

#### <a name="examples"></a>예

```
dnscmd dnssvr1.contoso.com /zoneadd test.contoso.com /dsprimary
dnscmd dnssvr1.contoso.com /zoneadd secondtest.contoso.com /secondary 10.0.0.2
```

## <a name="dnscmd-zonechangedirectorypartition-command"></a>dnscmd/zonechangedirectorypartition 명령

지정된 된 영역 상주 하는 디렉터리 파티션을 변경 합니다.

### <a name="syntax"></a>구문

```
dnscmd [<servername>] /zonechangedirectorypartition <zonename> {[<newpartitionname>] | [<zonetype>]}
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ---------- | ----------- |
| `<servername>` | IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다. |
| `<zonename>` |  영역 상주 하는 현재 디렉터리 파티션의 FQDN입니다. |
| `<newpartitionname>` |  영역 이동할 수 있는 디렉터리 파티션의 FQDN입니다. |
| `<zonetype>` | 영역을 이동할 디렉터리 파티션의 유형을 지정 합니다. |
| /domain | 영역을 기본 제공 도메인 디렉터리 파티션으로 이동 합니다. |
| /forest | 기본 제공 포리스트 디렉터리 파티션으로 영역을 이동 합니다. |
| /legacy | Active directory 도메인 컨트롤러에 대해 만들어진 디렉터리 파티션으로 영역을 이동 합니다. 이 디렉터리 파티션을 기본 모드에 대 한 필요 하지 않습니다. |

## <a name="dnscmd-zonedelete-command"></a>dnscmd/zonedelete 명령

지정 된 영역을 삭제합니다.

### <a name="syntax"></a>구문

```
dnscmd [<servername>] /zonedelete <zonename> [/dsdel] [/f]
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ---------- | ----------- |
| `<servername>` | IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다. |
| `<zonename>` | 삭제할 영역의 이름을 지정 합니다. |
| /dsdel | AD DS (Azure Directory 도메인 서비스)에서 영역을 삭제 합니다. |
| /f | 확인을 요청 하지 않고 명령을 실행 합니다. |

#### <a name="examples"></a>예

- [예 9: DNS 서버에서 영역 삭제](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc784399(v=ws.10)#example-9-delete-a-zone-from-a-dns-server)

## <a name="dnscmd-zoneexport-command"></a>dnscmd/zoneexport 명령

지정 된 영역의 리소스 레코드를 나열 하는 텍스트 파일을 만듭니다. **Zoneexport** 작업은 문제 해결을 위해 active directory 통합 영역에 대 한 리소스 레코드 파일을 만듭니다. 기본적으로이 명령이 만드는 파일은 DNS 디렉터리 (기본적으로 디렉터리)에 배치 됩니다 `%systemroot%/System32/Dns` .

### <a name="syntax"></a>구문

```
dnscmd [<servername>] /zoneexport <zonename> <zoneexportfile>
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ---------- | ----------- |
| `<servername>` | IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다. |
| `<zonename>` |  영역 이름을 지정합니다. |
| `<zoneexportfile>` | 만들려는 파일의 이름을 지정 합니다. |

#### <a name="examples"></a>예

- [예 10: 영역 리소스 레코드 목록을 파일로 내보내기](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc784399(v=ws.10)#example-10-export-zone-resource-records-list-to-a-file)

## <a name="dnscmd-zoneinfo"></a>dnscmd /zoneinfo

지정 된 영역의 레지스트리 섹션에서 설정을 표시 합니다.`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\DNS\Parameters\Zones\<zonename>`

### <a name="syntax"></a>구문

```
dnscmd [<servername>] /zoneinfo <zonename> [<setting>]
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ---------- | ----------- |
| `<servername>` | IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다. |
| `<zonename>` |  영역 이름을 지정합니다. |
| `<setting>` | **Zoneinfo** 명령이 반환 하는 설정을 개별적으로 지정할 수 있습니다. 설정을 지정 하지 않으면 모든 설정이 반환 됩니다. |

##### <a name="remarks"></a>설명

- 서버 수준 레지스트리 설정을 표시 하려면 **/sinfo** 명령을 사용 합니다.

- 이 명령을 사용 하 여 표시할 수 있는 설정 목록을 보려면 **/config** 명령을 참조 하세요.

#### <a name="examples"></a>예

- [예 11: 레지스트리에서 RefreshInterval 설정 표시](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc784399(v=ws.10)#example-11-display-refreshinterval-setting-from-the-registry)

- [예 12: 레지스트리에서 에이징 설정 표시](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc784399(v=ws.10)#example-12-display-aging-setting-from-the-registry)

## <a name="dnscmd-zonepause-command"></a>dnscmd/zonepause 명령

다음 쿼리 요청을 무시 하는 지정된 된 영역을 일시 중지 합니다.

### <a name="syntax"></a>구문

```
dnscmd [<servername>] /zonepause <zonename>
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ---------- | ----------- |
| `<servername>` | IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다. |
| `<zonename>` | 일시 중지 하려면 영역의 이름을 지정 합니다. |

##### <a name="remarks"></a>설명

- 영역을 다시 시작 하 고 일시 중지 된 후에도 사용할 수 있게 하려면 **/zoneresume** 명령을 사용 합니다.

#### <a name="examples"></a>예

```
dnscmd dnssvr1.contoso.com /zonepause test.contoso.com
```

## <a name="dnscmd-zoneprint-command"></a>dnscmd/zoneprint 명령

영역에 있는 레코드를 나열합니다.

### <a name="syntax"></a>구문

```
dnscmd [<servername>] /zoneprint <zonename>
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ---------- | ----------- |
| `<servername>` | IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다. |
| `<zonename>` | 나열할 영역의 이름을 지정 합니다. |







## <a name="dnscmd-zonerefresh-command"></a>dnscmd/zonerefresh 명령

마스터 영역에서 업데이트를 수행 하도록 보조 DNS 영역입니다.

### <a name="syntax"></a>구문

```
dnscmd [<servername>] /zonerefresh <zonename>
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ---------- | ----------- |
| `<servername>` | IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다. |
| `<zonename>` | 새로 고칠 영역의 이름을 지정 합니다. |

##### <a name="remarks"></a>설명

- **Zonerefresh** 명령은 마스터 서버의 SOA (권한 시작) 리소스 레코드에서 버전 번호를 확인 합니다. 마스터 서버에 버전 번호는 보조 서버의 버전 번호 보다 높은 경우 보조 서버를 업데이트 하는 영역 전송이 시작 됩니다. 버전 번호가 동일한 경우 영역 전송이 수행 되지 발생 합니다.

- 강제 검사는 기본적으로 15 분 마다 발생 합니다. 기본값을 변경 하려면 `dnscmd config refreshinterval` 명령을 사용 합니다.

#### <a name="examples"></a>예

```
dnscmd dnssvr1.contoso.com /zonerefresh test.contoso.com
```

## <a name="dnscmd-zonereload-command"></a>dnscmd/zonereload 명령

복사본에 정보 소스에서 영역입니다.

### <a name="syntax"></a>구문

```
dnscmd [<servername>] /zonereload <zonename>
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ---------- | ----------- |
| `<servername>` | IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다. |
| `<zonename>` | 영역 다시 로드 될 이름을 지정 합니다. |

##### <a name="remarks"></a>설명

- 영역이 active directory 통합 인 경우 Active Directory Domain Services (AD DS)에서 다시 로드 됩니다.

- 영역이 표준 파일 지원 영역인 경우 파일에서 다시 로드 됩니다.

#### <a name="examples"></a>예

```
dnscmd dnssvr1.contoso.com /zonereload test.contoso.com
```

## <a name="dnscmd-zoneresetmasters-command"></a>dnscmd/zoneresetmasters 명령

보조 영역에 대 한 영역 전송 정보를 제공 하는 마스터 서버의 IP 주소를 다시 설정 합니다.

### <a name="syntax"></a>구문

```
dnscmd [<servername>] /zoneresetmasters <zonename> [/local] [<IPaddress> [<IPaddress>]...]
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ---------- | ----------- |
| `<servername>` | IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다. |
| `<zonename>` | 다시 설정할 영역의 이름을 지정 합니다. |
| 로컬 / | 로컬 마스터 목록을 설정 합니다. 이 매개 변수는 active directory 통합 영역에 사용 됩니다. |
| `<IPaddress>` | 보조 영역 마스터 서버의 IP 주소. |

##### <a name="remarks"></a>설명

- 이 값은 원래 보조 영역을 만들 때 설정 됩니다. 사용 된 **zoneresetmasters** 보조 서버에서 명령입니다. 마스터 DNS 서버에 설정 된 경우에이 값 효과가 없습니다.

#### <a name="examples"></a>예

```
dnscmd dnssvr1.contoso.com /zoneresetmasters test.contoso.com 10.0.0.1
dnscmd dnssvr1.contoso.com /zoneresetmasters test.contoso.com /local
```

## <a name="dnscmd-zoneresetscavengeservers-command"></a>dnscmd/zoneresetscavengeservers 명령

지정된 된 영역 청소할 하는 서버의 IP 주소를 변경 합니다.

### <a name="syntax"></a>구문

```
dnscmd [<servername>] /zoneresetscavengeservers <zonename> [/local] [<IPaddress> [<IPaddress>]...]
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ---------- | ----------- |
| `<servername>` | IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다. |
| `<zonename>` | 청소할 영역을 지정 합니다. |
| 로컬 / | 로컬 마스터 목록을 설정 합니다. 이 매개 변수는 active directory 통합 영역에 사용 됩니다. |
| `<IPaddress>` | 청소를 수행할 수 있는 서버의 IP 주소를 나열 합니다. 이 매개 변수를 생략 하면이 영역을 호스팅하는 모든 서버 청소할 것입니다. |

##### <a name="remarks"></a>설명

- 기본적으로 영역을 호스트 하는 모든 서버는 해당 영역을 청소할 수 있습니다.

- 하나 이상의 DNS 서버에서 영역을 호스트 하는 경우이 명령을 사용 하 여 영역이 청소 되는 횟수를 줄일 수 있습니다.

- 청소는이 명령의 영향을 받는 DNS 서버 및 영역에서 사용 하도록 설정 해야 합니다.

#### <a name="examples"></a>예

```
dnscmd dnssvr1.contoso.com /zoneresetscavengeservers test.contoso.com 10.0.0.1 10.0.0.2
```

## <a name="dnscmd-zoneresetsecondaries-command"></a>dnscmd/zoneresetsecondaries 명령

응답 하는 마스터 서버 영역 전송 물으면 보조 서버의 IP 주소 목록을 지정 합니다.

### <a name="syntax"></a>구문

```
dnscmd [<servername>] /zoneresetsecondaries <zonename> {/noxfr | /nonsecure | /securens | /securelist <securityIPaddresses>} {/nonotify | /notify | /notifylist <notifyIPaddresses>}
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ---------- | ----------- |
| `<servername>` | IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다. |
| `<zonename>` | 보조 서버를 다시 설정 하는 영역 이름을 지정 합니다. |
| 로컬 / | 로컬 마스터 목록을 설정 합니다. 이 매개 변수는 active directory 통합 영역에 사용 됩니다. |
| /noxfr | 영역 전송이 허용 되지 않도록 지정 합니다. |
| /nonsecure | 모든 영역 전송 요청을 허용 하도록 지정 합니다. |
| /securens | 영역에 대 한 NS (이름 서버) 리소스 레코드에 나열 된 서버만 전송을 허용 하도록 지정 합니다. |
| /securelist | 영역 전송이 서버 목록에만 부여 되도록 지정 합니다. IP 주소 또는 주소 마스터 서버를 사용 하 여이 매개 변수를 따라야 합니다. |
| `<securityIPaddresses>` |  마스터 서버에서 영역 전송의 받을 IP 주소를 나열 합니다. 이 매개 변수는 **/seclist** 매개 변수 에서만 사용 됩니다. |
| /nonotify | 보조 서버에 전송 되는 변경 알림이 없도록 지정 합니다. |
| 알림/ | 모든 보조 서버에 변경 알림을 보내도록 지정 합니다. |
| /notifylist | 변경 알림이 서버 목록에만 전송 되도록 지정 합니다. 이 명령은 IP 주소 또는 주소 마스터 서버를 사용 하 여 따라야 합니다. |
| `<notifyIPaddresses>` |  IP 주소 또는 보조 서버 또는 서버 변경 알림이 전송 되는 주소를 지정 합니다. 이 목록은 **/notifylist** 매개 변수 에서만 사용 됩니다. |

##### <a name="remarks"></a>설명

- 마스터 서버에서 **zoneresetsecondaries** 명령을 사용 하 여 보조 서버의 영역 전송 요청에 응답 하는 방법을 지정 합니다.

#### <a name="examples"></a>예

```
dnscmd dnssvr1.contoso.com /zoneresetsecondaries test.contoso.com /noxfr /nonotify
dnscmd dnssvr1.contoso.com /zoneresetsecondaries test.contoso.com /securelist 11.0.0.2
```

## <a name="dnscmd-zoneresettype-command"></a>dnscmd/zoneresettype 명령

영역 종류를 변경합니다.

### <a name="syntax"></a>구문

```
dnscmd [<servername>] /zoneresettype <zonename> <zonetype> [/overwrite_mem | /overwrite_ds]
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ---------- | ----------- |
| `<servername>` | IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다. |
| `<zonename>` |  형식을 변경할 수는 영역을 식별 합니다. |
| `<zonetype>` |  만들 영역 유형을 지정 합니다. 각 형식에는 다음과 같은 다른 필수 매개 변수가 있습니다.<ul><li>**/dsprimary** -active directory 통합 영역을 만듭니다.</li><li>**/기본/file `<filename>` ** -표준 기본 영역을 만듭니다.</li><li>**/보조 `<masterIPaddress> [,<masterIPaddress>...]` ** -표준 보조 영역을 만듭니다.</li><li>**/stub `<masterIPaddress>[,<masterIPaddress>...]` /file `<filename>` ** -파일 지원 스텁 영역을 만듭니다.</li><li>**/dsstub `<masterIPaddress>[,<masterIPaddress>...]` ** -Active directory 통합 스텁 영역을 만듭니다.</li><li>**/ch... `<masterIPaddress[,<masterIPaddress>]` /file `<filename>` ** -생성 된 영역에서 확인 되지 않은 쿼리를 다른 DNS 서버로 전달 하도록 지정 합니다.</li><li>**/dsforwarder** -생성 된 active directory 통합 영역에서 확인 되지 않은 쿼리를 다른 DNS 서버에 전달 하도록 지정 합니다.</li></ul> |
| /overwrite_mem | AD DS의 데이터에서 DNS 데이터를 덮어씁니다. |
| /overwrite_ds | AD DS에 기존 데이터를 덮어씁니다. |

##### <a name="remarks"></a>설명

- 영역 유형을 **/dsforwarder** 로 설정 하면 조건부 전달을 수행 하는 영역이 만들어집니다.

#### <a name="examples"></a>예

```
dnscmd dnssvr1.contoso.com /zoneresettype test.contoso.com /primary /file test.contoso.com.dns
dnscmd dnssvr1.contoso.com /zoneresettype second.contoso.com /secondary 10.0.0.2
```

## <a name="dnscmd-zoneresume-command"></a>dnscmd/zoneresume 명령

이전에 일시 중지 하는 지정 된 영역을 시작 합니다.

### <a name="syntax"></a>구문

```
dnscmd [<servername>] /zoneresume <zonename>
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ---------- | ----------- |
| `<servername>` | IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다. |
| `<zonename>` | 다시 시작 하려면 영역의 이름을 지정 합니다. |

##### <a name="remarks"></a>설명

- 이 작업을 사용 하 여 **/zonepause** 작업에서 다시 시작할 수 있습니다.

#### <a name="examples"></a>예

```
dnscmd dnssvr1.contoso.com /zoneresume test.contoso.com
```

## <a name="dnscmd-zoneupdatefromds-command"></a>dnscmd/zoneupdatefromds 명령

AD DS에서 지정 된 active directory 통합 영역을 업데이트 합니다.

### <a name="syntax"></a>구문

```
dnscmd [<servername>] /zoneupdatefromds <zonename>
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ---------- | ----------- |
| `<servername>` | IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다. |
| `<zonename>` | 업데이트 하려면 영역의 이름을 지정 합니다. |

##### <a name="remarks"></a>설명

- Active directory 통합 영역은 기본적으로 5 분 마다이 업데이트를 수행 합니다. 이 매개 변수를 변경 하려면 `dnscmd config dspollinginterval` 명령을 사용 합니다.

#### <a name="examples"></a>예

```
dnscmd dnssvr1.contoso.com /zoneupdatefromds
```

## <a name="dnscmd-zonewriteback-command"></a>dnscmd/zonewriteback 명령

지정된 시간대에 관련된 변경 내용에 대한 DNS 서버 메모리를 확인하고 영구 스토리지에 씁니다.

### <a name="syntax"></a>구문

```
dnscmd [<servername>] /zonewriteback <zonename>
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ---------- | ----------- |
| `<servername>` | IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다. |
| `<zonename>` | 업데이트 하려면 영역의 이름을 지정 합니다. |

##### <a name="remarks"></a>설명

- 영역 수준 작업입니다. **/Writebackfiles** 작업을 사용 하 여 DNS 서버의 모든 영역을 업데이트할 수 있습니다.

#### <a name="examples"></a>예

```
dnscmd dnssvr1.contoso.com /zonewriteback test.contoso.com
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)