---
ms.assetid: 0f21951c-b1bf-43bb-a329-bbb40c58c876
title: 복제 오류 1753 엔드포인트 매퍼에서 사용할 수 있는 엔드포인트이 더 이상 없음
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 2e63d177abd0a6880c1825b821d265c8fa233a22
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80823166"
---
# <a name="replication-error-1753-there-are-no-more-endpoints-available-from-the-endpoint-mapper"></a>복제 오류 1753 엔드포인트 매퍼에서 사용할 수 있는 엔드포인트이 더 이상 없음

>Windows Server에 적용 됩니다.

이 문서에서는 Win32 오류 1753로 실패 하는 Active Directory 작업에 대 한 증상, 원인 및 해결 단계를 설명 합니다. "끝점 매퍼에서 사용할 수 있는 끝점이 더 이상 없습니다."

DCDIAG는 1753 오류: "끝점 매퍼에서 사용할 수 있는 끝점이 더 이상 없습니다."와 함께 연결 테스트, Active Directory 복제 테스트 또는 KnowsOfRoleHolders 테스트가 실패 한 것을 보고 합니다.

```
Testing server: <site><DC Name>
Starting test: Connectivity
* Active Directory LDAP Services Check
* Active Directory RPC Services Check
[<DC Name>] DsBindWithSpnEx() failed with error 1753,
There are no more endpoints available from the endpoint mapper..
Printing RPC Extended Error Info:
Error Record 1, ProcessID is <process ID> (DcDiag)
System Time is: <date> <time>
Generating component is 2 (RPC runtime)
Status is 1753: There are no more endpoints available from the endpoint mapper. Detection location is 500
NumberOfParameters is 4
Unicode string: ncacn_ip_tcp
Unicode string: <source DC object GUID>._msdcs.contoso.com
Long val: -481213899
Long val: 65537
Error Record 2, ProcessID is 700 (DcDiag)
System Time is: <date> <time>
Generating component is 2 (RPC runtime)
Status is 1753: There are no more endpoints available from the endpoint mapper.
NumberOfParameters is 1
Unicode string: 1025
[Replications Check,<DC Name>] A recent replication attempt failed:
From <source DC> to <destination DC>
Naming Context: <DN path of directory partition>
The replication generated an error (1753):
There are no more endpoints available from the endpoint mapper.
The failure occurred at <date> <time>.
The last success occurred at <date> <time>.
3 failures have occurred since the last success.
The directory on <DC name> is in the process.
of starting up or shutting down, and is not available.
Verify machine is not hung during boot.
```

REPADMIN. EXE가 복제 시도가 실패 했으며 상태 1753을 보고 합니다.
일반적으로 1753 상태를 나타내는 REPADMIN 명령에는 다음이 포함 되지만이에 국한 되지 않습니다.

* REPADMIN/REPLSUM
* REPADMIN/SHOWREPL
* REPADMIN/SHOWREPS
* REPADMIN /SYNCALL

"REPADMIN/SHOWREPS"의 샘플 출력 "복제 액세스가 거부 되었습니다." 오류가 발생 하 여 CONTOSO-DC2에서 CONTOSO-DC1으로의 인바운드 복제가 실패 하는 것을 보여 줍니다.

```
Default-First-Site-NameCONTOSO-DC1
DSA Options: IS_GC 
Site Options: (none)
DSA object GUID: b6dc8589-7e00-4a5d-b688-045aef63ec01
DSA invocationID: b6dc8589-7e00-4a5d-b688-045aef63ec01
==== INBOUND NEIGHBORS ======================================
DC=contoso,DC=com
Default-First-Site-NameCONTOSO-DC2 via RPC
DSA object GUID: 74fbe06c-932c-46b5-831b-af9e31f496b2
Last attempt @ <date> <time> failed, result 1753 (0x6d9):
There are no more endpoints available from the endpoint mapper.
<#> consecutive failure(s).
Last success @ <date> <time>.
```

Active Directory 사이트 및 서비스의 **복제 토폴로지 확인** 명령은 "끝점 매퍼에서 사용할 수 있는 끝점이 더 이상 없습니다."를 반환 합니다.

원본 DC에서 연결 개체를 마우스 오른쪽 단추로 클릭 하 고 **복제 토폴로지 확인** 을 선택 하면 "끝점 매퍼에서 사용할 수 있는 끝점이 더 이상 없습니다."가 발생 합니다. 화면에 표시 되는 오류 메시지는 다음과 같습니다.

대화 상자 제목 텍스트: 복제 토폴로지 확인 대화 상자 메시지 텍스트: 도메인 컨트롤러에 연결 하는 동안 다음 오류가 발생 했습니다. 끝점 매퍼에서 사용할 수 있는 끝점이 더 이상 없습니다.

Active Directory 사이트 및 서비스의 **지금 복제** 명령은 "끝점 매퍼에서 사용할 수 있는 끝점이 더 이상 없습니다."를 반환 합니다.
원본 DC에서 연결 개체를 마우스 오른쪽 단추로 클릭 하 고 **지금 복제** 를 선택 하면 "끝점 매퍼에서 사용할 수 있는 끝점이 더 이상 없습니다."가 발생 합니다.
화면에 표시 되는 오류 메시지는 다음과 같습니다.

대화 상자 제목 텍스트: 지금 복제 대화 상자 메시지 텍스트: 명명 컨텍스트 \<% directory 파티션 이름% >을 (를) 도메인 컨트롤러 \<원본 DC >에서 도메인 컨트롤러 \<대상 DC > 동기화 하는 동안 다음 오류가 발생 했습니다.

끝점 매퍼에서 사용할 수 있는 끝점이 더 이상 없습니다.
작업을 계속할 수 없습니다.

-2146893022 상태를 포함 하는 ntds KCC, NTDS 일반 또는 Microsoft-ActiveDirectory_DomainService 이벤트는 이벤트 뷰어의 디렉터리 서비스 로그에 기록 됩니다.

일반적으로-2146893022 상태를 인용 하는 Active Directory 이벤트는 다음으로 제한 되지 않습니다.

| 이벤트 ID | 이벤트 원본 | 이벤트 문자열|
| --- | --- | --- |
| 1655 | NTDS 일반 | Active Directory가 다음 글로벌 카탈로그와 통신 하려고 하 고는 시도 되지 않았습니다. |
| 1925 | NTDS KCC | 다음 쓰기 가능한 디렉터리 파티션의 복제 링크를 설정 하려고 했으나 실패 했습니다. |
| 1265 | NTDS KCC | 지식 일관성 검사기 (KCC)가 다음 디렉터리 파티션 및 원본 도메인 컨트롤러에 대 한 복제 규약을 추가 하려고 했지만 실패 했습니다. |

## <a name="cause"></a>원인

아래 단계에서는 7 단계에서 rpc 클라이언트에서 클라이언트 응용 프로그램으로 데이터를 전달 하는 데 1 단계에서 RPC 끝점 매퍼 (EPM)를 사용 하 여 서버 응용 프로그램을 등록 하는 것으로 시작 하는 RPC 워크플로를 보여 줍니다.

### <a name="adds-rpc-workflow"></a>RPC 워크플로 추가

1. 서버 앱이 RPC 끝점 매퍼 (EPM)를 사용 하 여 해당 끝점을 등록 합니다.
1. 클라이언트는 RPC 호출을 수행 합니다 (사용자, OS 또는 응용 프로그램 시작 작업 대신).
1. 클라이언트 쪽 RPC는 대상 컴퓨터 EPM에 연결 하 고 끝점을 요청 하 여 클라이언트 호출을 완료 합니다.
1. 서버 컴퓨터의 EPM이 끝점으로 응답
1. 클라이언트 쪽 RPC가 서버 앱에 연결
1. 서버 앱에서 호출을 실행 하 고 결과를 클라이언트 RPC로 반환 합니다.
1. 클라이언트 쪽 RPC가 결과를 다시 클라이언트 앱에 전달 합니다.

오류 1753는 #3 단계와 #4 간에 실패 하 여 생성 됩니다. 특히 오류 1753은 RPC 클라이언트 (대상 DC)가 포트 135을 통해 RPC 서버 (원본 DC)에 연결할 수 있었지만 RPC 서버 (원본 DC)의 EPM은 대상 RPC 응용 프로그램을 찾을 수 없어 서버 쪽 오류 1753를 반환 했음을 의미 합니다. 1753 오류가 있으면 RPC 클라이언트 (대상 DC)가 네트워크를 통해 RPC 서버 (AD 복제 원본 DC)에서 서버 쪽 오류 응답을 받았음을 나타냅니다.

1753 오류에 대 한 특정 근본 원인은 다음과 같습니다.

* 서버 앱이 시작 되지 않은 경우 (즉, 위에 있는 "추가 정보" 다이어그램의 #1 단계를 시도 하지 않았습니다.)
* 서버 앱을 시작 했지만, 초기화 하는 동안 일부 오류가 발생 하 여 RPC 끝점 매퍼를 등록할 수 없습니다. 즉, 위의 "추가 정보" 다이어그램에서 단계 #1 시도 했지만 실패 했습니다.
* 서버 앱이 시작 되었지만 이후에는 종료 되었습니다. (위의 "추가 정보" 다이어그램에 있는 단계 #1 성공적으로 완료 되었지만 서버가 종료 되었기 때문에 나중에 취소 되었습니다.)
* 서버 앱에서 수동으로 해당 끝점의 등록을 취소 했습니다. 3과 유사 합니다. 그렇지는 않지만 완전성을 위해 포함 됩니다.)
* DNS, WINS 또는 호스트/Lmhosts 파일의 이름에 IP 매핑 오류가 발생 하 여 RPC 클라이언트 (대상 DC)가 의도 한 것과 다른 RPC 서버에 연결 했습니다.

오류 1753은 다음에 의해 발생 하지 않습니다.

* 포트 135을 통한 rpc 클라이언트 (대상 DC)와 RPC 서버 (원본 DC) 사이에 네트워크 연결이 부족 합니다.
* 포트 135 및 RPC 클라이언트 (대상 DC)를 사용 하 여 사용 후 삭제 포트를 통해 RPC 서버 (원본 DC) 간의 네트워크 연결이 부족 합니다.
* 암호가 일치 하지 않거나 원본 DC에서 Kerberos 암호화 된 패킷을 해독 하지 못하는 경우

## <a name="resolutions"></a>해결 방법

끝점 매퍼를 사용 하 여 서비스를 등록 하는 서비스가 시작 되었는지 확인 합니다.

* Windows 2000 및 Windows Server 2003 Dc: 원본 DC가 표준 모드로 부팅 되는지 확인 합니다.
* Windows Server 2008 또는 Windows Server 2008 r 2의 경우: 원본 DC의 콘솔에서 서비스 관리자 (services.msc)를 시작 하 고 Active Directory Domain Services 서비스가 실행 중인지 확인 합니다.

RPC 클라이언트 (대상 DC)가 의도 한 RPC 서버 (원본 DC)에 연결 되어 있는지 확인 합니다.

공통 Active Directory 포리스트의 모든 Dc는 _msdcs 도메인 컨트롤러 CNAME 레코드를 등록 합니다. 포리스트 내에 상주 하는 도메인에 관계 없이 포리스트 루트 도메인 > DNS 영역을 \<합니다. DC CNAME 레코드는 각 도메인 컨트롤러에 대 한 NTDS 설정 개체의 objectGUID 특성에서 파생 됩니다.

복제 기반 작업을 수행할 때 대상 DC는 DNS에서 원본 Dc CNAME 레코드를 쿼리 합니다. CNAME 레코드에는 DNS 클라이언트 캐시 조회, 호스트/LMHost 파일 조회, DNS의 호스트 A/AAAA 레코드 또는 WINS를 통해 원본 dc IP 주소를 파생 시키는 데 사용 되는 원본 DC의 정규화 된 컴퓨터 이름이 포함 됩니다.

DNS, WINS, 호스트 및 LMHOST 파일에 잘못 된 NTDS 설정 개체와 잘못 된 이름-IP 매핑이 있으면 RPC 클라이언트 (대상 DC)가 잘못 된 RPC 서버 (원본 DC)에 연결할 수 있습니다. 또한 잘못 된 이름-IP 매핑으로 인해 rpc 클라이언트 (대상 DC)에서 RPC 서버 응용 프로그램 (이 경우에는 Active Directory 역할)이 설치 되어 있지 않은 컴퓨터에 연결할 수 있습니다. 예: d c 2에 대 한 오래 된 호스트 레코드에는 DC3 또는 구성원 컴퓨터의 IP 주소가 포함 됩니다.

Active Directory의 대상 Dc 복사본에 있는 원본 DC의 objectGUID가 Active Directory의 원본 dc 복사본에 저장 된 원본 DC objectGUID와 일치 하는지 확인 합니다. 불일치가 있는 경우 ntds 설정 개체에 대해 repadmin/showobjmeta와 유사를 사용 하 여 원본 DC의 마지막 승격에 해당 하는 것을 확인 합니다 (힌트: 원본 dc dcpromo.exe 파일의 마지막 프로 모션 날짜에 대해/showobjmeta와 유사에서 만든 날짜와 NTDS 설정 개체에 대 한 날짜 스탬프 비교). DCPROMO의 마지막 수정/생성 날짜를 사용 해야 할 수도 있습니다. 로그 파일 자체). 개체 Guid가 동일 하지 않은 경우 대상 DC에는 CNAME 레코드가 IP 매핑의 잘못 된 이름을 가진 호스트 레코드를 참조 하는 원본 DC에 대해 오래 된 NTDS 설정 개체가 있을 수 있습니다.

대상 dc에서 IPCONFIG/ALL을 실행 하 여 대상 DC가 이름 확인을 위해 사용 하는 DNS 서버를 확인 합니다.

```
c:>ipconfig /all
```

대상 DC에서 원본 Dc 정규화 된 DC CNAME 레코드에 대해 NSLOOKUP을 실행 합니다.

```
c:>nslookup -type=cname <fully qualified cname of source DC> <destination DCs primary DNS Server IP >
c:>nslookup -type=cname <fully qualified cname of source DC> <destination DCs secondary DNS Server IP>
```

NSLOOKUP에서 반환 된 IP 주소가 원본 DC의 호스트 이름/보안 id를 소유 하 고 있는지 확인 합니다.

```
C:>NBTSTAT -A <IP address returned by NSLOOKUP in the step above>
```

원본 DC의 콘솔에 로그온 하 여 CMD 프롬프트에서 "IPCONFIG"를 실행 하 고 원본 DC가 위의 NSLOOKUP 명령에서 반환 된 IP 주소를 소유 하 고 있는지 확인 합니다.

DNS의 IP 매핑에 대 한 부실/중복 호스트 확인

```
NSLOOKUP -type=hostname <single label hostname of source DC> <primary DNS Server IP on destination DC>
NSLOOKUP -type=hostname <single label hostname of source DC> <secondary DNS Server IP on destination DC>

NSLOOKUP -type=hostname <fully qualified computer name of source DC> <primary DNS Server IP on destination DC>
NSLOOKUP -type=hostname <fully qualified computer name of source DC> <secondary DNS Server IP on dest. DC>
```

호스트 레코드에 잘못 된 IP 주소가 있는 경우 DNS 청소를 사용 하도록 설정 하 고 올바르게 구성 했는지 확인 합니다.

위의 테스트 또는 네트워크 추적에서 잘못 된 IP 주소를 반환 하는 이름 쿼리를 표시 하지 않는 경우 호스트 파일, LMHOSTS 파일 및 WINS 서버에서 부실 항목을 고려 하십시오. DNS 서버는 WINS 대체 이름 확인을 수행 하도록 구성 될 수도 있습니다.

* 서버 응용 프로그램 (Active Directory et al)이 RPC 서버 (원본 DC)에서 끝점 매퍼를 사용 하 여 등록 되었는지 확인 합니다.
* Active Directory는 잘 알려져 있고 동적으로 등록 된 포트를 혼합 하 여 사용 합니다. 이 표에서는 Active Directory 도메인 컨트롤러에서 사용 하는 잘 알려진 포트 및 프로토콜을 보여 줍니다.

| RPC 서버 응용 프로그램 | 포트 | TCP | UDP |
| --- | --- | --- | --- |
| DNS 서버 | 53 | X | X |
| Kerberos | 88 | X | X |
| LDAP 서버 | 389 | X | X |
| Microsoft-DS | 445 | X | X |
| LDAP SSL | 636 | X | X |
| 글로벌 카탈로그 서버 | 3268 | X |   |
| 글로벌 카탈로그 서버 | 3269 | X |   |

잘 알려진 포트는 끝점 매퍼를 사용 하 여 등록 되지 않습니다.

또한 Active Directory 및 기타 응용 프로그램은 RPC 임시 포트 범위에서 동적으로 할당 된 포트를 수신 하는 서비스를 등록 합니다. 이러한 RPC 서버 응용 프로그램은 windows Server 49152 및 Windows Server 65535 R2 컴퓨터의 2008 및 2008 범위 간 windows 2003 2000의 1024과 5000 사이에 TCP 포트를 동적으로 할당 합니다. [KB 문서 224196](https://support.microsoft.com/kb/224196)에 설명 된 단계를 사용 하 여 복제에 사용 되는 RPC 포트를 레지스트리에 하드 코딩할 수 있습니다. Active Directory는 하드 코드 된 포트를 사용 하도록 구성 된 경우에도 EPM으로 등록 됩니다.

원하는 RPC 서버 응용 프로그램이 RPC 서버 (AD 복제의 경우 원본 DC)의 RPC 끝점 매퍼를 사용 하 여 자신을 등록 했는지 확인 합니다.

이 작업을 수행 하는 방법에는 여러 가지가 있지만, 다음 구문을 사용 하 여 원본 DC의 콘솔에 있는 관리자 권한 CMD 프롬프트에서 PORTQRY를 설치 하 고 실행 하는 방법 중 하나입니다.

```
portquery -n <source DC> -e 135 > file.txt
```

Portqry 출력에서 ncacn_ip_tcp 프로토콜에 대해 "MS NT 디렉터리 DRS 인터페이스" (UUID = 351 ...)에 의해 동적으로 등록 된 포트 번호를 확인 합니다. 아래 코드 조각에서는 Windows Server 2008 R2 DC의 샘플 portquery 출력을 보여 줍니다.

```
UUID: e3514235-4b06-11d1-ab04-00c04fc2dcd2 MS NT Directory DRS Interface
ncacn_np:CONTOSO-DC01[\pipe\lsass] 
UUID: e3514235-4b06-11d1-ab04-00c04fc2dcd2 MS NT Directory DRS Interface
ncacn_np:CONTOSO-DC01[\PIPE\protected_storage] 
UUID: e3514235-4b06-11d1-ab04-00c04fc2dcd2 MS NT Directory DRS Interface
ncacn_ip_tcp:CONTOSO-DC01[49156] 
UUID: e3514235-4b06-11d1-ab04-00c04fc2dcd2 MS NT Directory DRS Interface
ncacn_http:CONTOSO-DC01[49157] 
UUID: e3514235-4b06-11d1-ab04-00c04fc2dcd2 MS NT Directory DRS Interface
ncacn_http:CONTOSO-DC01[6004]
```

이 오류를 해결 하는 다른 가능한 방법은 다음과 같습니다.

* 원본 DC가 정상 모드에서 부팅 되 고 원본 DC의 OS 및 DC 역할이 완전히 시작 되었는지 확인 합니다.
* Active Directory 도메인 서비스가 실행 중인지 확인 합니다. 서비스가 현재 중지 되었거나 기본 시작 값으로 구성 되지 않은 경우 기본 시작 값을 다시 설정 하 고 수정 된 DC를 다시 부팅 한 후 작업을 다시 시도 하십시오.
* Rpc 서비스 및 RPC 로케이터에 대 한 시작 값과 서비스 상태가 rpc 클라이언트 (대상 DC) 및 RPC 서버 (원본 DC)의 OS 버전에 대해 올바른지 확인 합니다. 서비스가 현재 중지 되었거나 기본 시작 값으로 구성 되지 않은 경우 기본 시작 값을 다시 설정 하 고 수정 된 DC를 다시 부팅 한 후 작업을 다시 시도 하십시오.
   * 또한 서비스 컨텍스트가 다음 표에 나열 된 기본 설정과 일치 하는지 확인 합니다.

      | Service | Windows Server 2003 이상 버전의 기본 상태 (시작 유형) | Windows Server 2000의 기본 상태 (시작 유형) |
      | --- | --- | --- |
      | 원격 프로시저 호출 | 시작 됨 (자동) | 시작 됨 (자동) |
      | 원격 프로시저 호출 로케이터 | Null 또는 중지 됨 (수동) | 시작 됨 (자동) |

* 동적 포트 범위의 크기가 제한 되지 않았는지 확인 합니다. RPC 포트 범위를 열거 하는 Windows Server 2008 및 Windows Server 2008 R2 NETSH 구문은 다음과 같습니다.

   ```
   netsh int ipv4 show dynamicport tcp
   netsh int ipv4 show dynamicport udp
   netsh int ipv6 show dynamicport tcp
   netsh int ipv6 show dynamicport udp
   ```

* KB 224196에 정의 된 하드 코딩 된 포트 정의가 원본 Dc OS 버전에 대 한 동적 포트 범위 내에 있는지 확인 합니다. [KB 문서 224196](https://support.microsoft.com/kb/224196) 을 검토 하 고 하드 코드 된 포트가 원본 DC의 운영 체제 버전에 대 한 임시 포트 범위 내에 있는지 확인 하십시오.

* ClientProtocols 키가 HKLM\Software\Microsoft\Rpc 아래에 있고 다음 5 개의 기본값을 포함 하는지 확인 합니다.

   ```
   ncacn_http REG_SZ rpcrt4.dll
   ncacn_ip_tcp REG_SZ rpcrt4.dll
   ncacn_nb_tcp REG_SZ rpcrt4.dll
   ncacn_np REG_SZ rpcrt4.dll
   ncacn_ip_udp REG_SZ rpcrt4.dll
   ```

## <a name="more-information"></a>추가 정보

IP 매핑에 대 한 잘못 된 이름의 예: RPC 오류 1753 및-2146893022: 대상 사용자 이름이 잘못 되었습니다.

Contoso.com 도메인은 IP 주소 x. x. 1.1 및 x. x. x. x. x. x. x. x. x. x. x. D c 2에 대 한 호스트 "A"/"AAAA" 레코드가 d c 2에 대해 구성 된 모든 DNS 서버에 올바르게 등록 되어 있습니다. 또한 DC1의 HOSTS 파일에는 IP 주소 DC2s에 대 한 정규화 된 호스트 이름에 대 한 항목이 포함 되어 있습니다. 나중에 DC2's IP 주소가 X. X. x. x. x. x. x. x. x. x. x. x. x. x. x. x. x. x. x. x. x. 다음 추적에 표시 된 것 처럼 Active Directory 사이트 및 서비스 스냅인의 **지금 복제** 명령에 의해 트리거되는 AD 복제 시도가 오류 1753와 함께 실패 합니다.

```
F# SRC    DEST    Operation
1 x.x.1.1 x.x.1.2 ARP:Request, x.x.1.1 asks for x.x.1.2
2 x.x.1.2 x.x.1.1 ARP:Response, x.x.1.2 at 00-13-72-28-C8-5E
3 x.x.1.1 x.x.1.2 TCP:Flags=......S., SrcPort=50206, DstPort=DCE endpoint resolution(135)
4 x.x.1.2 x.x.1.1 ARP:Request, x.x.1.2 asks for x.x.1.1
5 x.x.1.1 x.x.1.2 ARP:Response, x.x.1.1 at 00-15-5D-42-2E-00
6 x.x.1.2 x.x.1.1 TCP:Flags=...A..S., SrcPort=DCE endpoint resolution(135)
7 x.x.1.1 x.x.1.2 TCP:Flags=...A...., SrcPort=50206, DstPort=DCE endpoint resolution(135)
8 x.x.1.1 x.x.1.2 MSRPC:c/o Bind: UUID{E1AF8308-5D1F-11C9-91A4-08002B14A0FA} EPT(EPMP)
9 x.x.1.2 x.x.1.1 MSRPC:c/o Bind Ack: Call=0x2 Assoc Grp=0x5E68 Xmit=0x16D0 Recv=0x16D0
10 x.x.1.1 x.x.1.2 EPM:Request: ept_map: NDR, DRSR(DRSR) {E3514235-4B06-11D1-AB04-00C04FC2DCD2} [DCE endpoint resolution(135)]
11 x.x.1.2 x.x.1.1 EPM:Response: ept_map: 0x16C9A0D6 - EP_S_NOT_REGISTERED
```

프레임 **10**에서 대상 dc는 Active Directory 복제 서비스 클래스 UUID E351에 대 한 포트 135을 통해 원본 dc 끝점 매퍼를 쿼리 합니다.

프레임 **11**에서 원본 dc에서 아직 dc 역할을 호스팅하지 않으므로 E351를 등록 하지 않은 구성원 컴퓨터입니다. 로컬 EPM이 있는 복제 서비스의 UUID는 10 진수 오류 1753, 16 진수 오류 0x6d9 및 친숙 한 오류 (끝점 매퍼에서 사용할 수 있는 끝점이 더 이상 없음)에 매핑되는 기호화 된 오류 EP_S_NOT_REGISTERED 응답 합니다.

나중에 IP 주소가 x. x. 1.2 인 구성원 컴퓨터가 contoso.com 도메인의 "MayberryDC" 복제본으로 승격 됩니다. 다시 **복제 명령이 복제를 트리거하는 데** 사용 되지만이 시간은 "대상 사용자 이름이 잘못 되었습니다." 화면 오류와 함께 실패 합니다. 네트워크 어댑터에 할당 된 IP 주소에는 IP 주소 x. x. 1.2.1.2는 도메인 컨트롤러 이며, 현재 표준 모드로 부팅 되어 E351 ... 복제 서비스 UUID를 로컬 EPM으로 사용 하는 경우에는 DC2의 이름 또는 보안 id를 소유 하 고 있지 않으며 DC1에서 Kerberos 요청을 해독할 수 없으므로 "대상 사용자 이름이 잘못 되었습니다." 라는 오류와 함께 요청이 실패 합니다. 오류는 10 진수 오류-2146893022/16 진수 오류 0x80090322에 매핑됩니다.

이러한 잘못 된 호스트-IP 매핑은 호스트/lmhost 파일, DNS의 호스트 A/AAAA 등록 또는 WINS의 부실 항목으로 인해 발생할 수 있습니다.

요약: 잘못 된 호스트-IP 매핑 (이 경우 호스트 파일)에서 Active Directory Domain Services 서비스가 실행 되지 않는 "원본" DC로 확인 되어 (또는 해당 문제에 대해 설치 된 경우에도), 복제 SPN이 아직 등록 되지 않았고 원본 DC에서 오류 1753를 반환 했기 때문에이 예는 실패 했습니다. 두 번째 경우에는 호스트에서 IP로의 잘못 된 매핑 (호스트 파일에 다시 연결)이 발생 하 여 대상 DC가 E351를 등록 한 DC에 연결 했습니다. 복제 SPN을 사용 하지만 원본 DC와 다른 호스트 이름 및 보안 id가 있기 때문에 오류-2146893022: 대상 사용자 이름이 잘못 되었습니다.

## <a name="related-topics"></a>관련 항목

* [1753 오류로 인해 실패 하는 Active Directory 작업 문제 해결: 끝점 매퍼에서 사용할 수 있는 끝점이 더 이상 없습니다.](https://support.microsoft.com/kb/2089874)
* [KB 문서 839880 제품 CD의 Windows Server 2003 지원 도구를 사용 하 여 RPC 끝점 매퍼 오류 문제 해결](https://support.microsoft.com/kb/839880)
* [KB 문서 832017 Windows Server 시스템의 서비스 개요 및 네트워크 포트 요구 사항](https://support.microsoft.com/kb/832017/)
* [KB 문서 224196 Active Directory 복제 트래픽 및 클라이언트 RPC 트래픽을 특정 포트로 제한](https://support.microsoft.com/kb/224196/)
* [KB 문서 154596 방화벽에서 작동 하도록 RPC 동적 포트 할당을 구성 하는 방법](https://support.microsoft.com/kb/154596)
* [RPC 작동 방법](https://msdn.microsoft.com/library/aa373935(VS.85).aspx)
* [서버에서 연결을 준비 하는 방법](https://msdn.microsoft.com/library/aa373938(VS.85).aspx)
* [클라이언트에서 연결을 설정 하는 방법](https://msdn.microsoft.com/library/aa373937(VS.85).aspx)
* [인터페이스 등록](https://msdn.microsoft.com/library/aa375357(VS.85).aspx)
* [네트워크에서 서버를 사용할 수 있도록 설정](https://msdn.microsoft.com/library/aa373974(VS.85).aspx)
* [끝점 등록](https://msdn.microsoft.com/library/aa375255(VS.85).aspx)
* [클라이언트 호출 수신 대기](https://msdn.microsoft.com/library/aa373966(VS.85).aspx)
* [클라이언트에서 연결을 설정 하는 방법](https://msdn.microsoft.com/library/aa373937(VS.85).aspx)
* [특정 포트에 대 한 Active Directory 복제 트래픽 및 클라이언트 RPC 트래픽 제한](https://support.microsoft.com/kb/224196)
* [AD DS에서 대상 DC에 대 한 SPN](https://msdn.microsoft.com/library/dd207688(PROT.13).aspx)
