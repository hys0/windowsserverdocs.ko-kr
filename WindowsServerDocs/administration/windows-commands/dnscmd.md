---
title: Dnscmd
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e7f31cb5-a426-4e25-b714-88712b8defd5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 39478e9b7dd8e8c69ed07f5d431486a7ed96b9cb
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59815504"
---
# <a name="dnscmd"></a>Dnscmd

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

DNS 서버를 관리 하기 위한 명령줄 인터페이스입니다. 이 유틸리티는 배치 파일 DNS의 일상적인 관리 작업을 자동화 하기 위해 네트워크에 간단한 무인된 설치 및 구성을 새 DNS 서버를 수행 하려면 스크립팅에 유용 합니다.  
## <a name="syntax"></a>구문  
```  
dnscmd <ServerName> <command> [<command parameters>]  
```  
## <a name="parameters"></a>매개 변수  
|매개 변수|설명|  
|-------|--------|  
|<ServerName>|원격 또는 로컬 DNS 서버의 IP 주소 또는 호스트 이름입니다.|  
## <a name="commands"></a>명령  
|Command|설명|  
|------|--------|  
|[dnscmd /ageallrecords](#BKMK_1)|영역 또는 노드 모든 타임 스탬프에 현재 시간을 설정합니다.|  
|[dnscmd /clearcache](#BKMK_2)|DNS 서버 캐시를 지웁니다.|  
|[dnscmd /config](#BKMK_3)|DNS 서버 또는 영역 구성을 다시 설정합니다.|  
|[dnscmd /createbuiltindirectorypartitions](#BKMK_4)|기본 제공 DNS 응용 프로그램 디렉터리 파티션을 만듭니다.|  
|[dnscmd /createdirectorypartition](#BKMK_5)|DNS 응용 프로그램 디렉터리 파티션을 만듭니다.|  
|[dnscmd /deletedirectorypartition](#BKMK_6)|DNS 응용 프로그램 디렉터리 파티션을 삭제합니다.|  
|[dnscmd /directorypartitioninfo](#BKMK_7)|DNS 응용 프로그램 디렉터리 파티션에 대 한 정보를 나열 합니다.|  
|[dnscmd /enlistdirectorypartition](#BKMK_8)|DNS 응용 프로그램 디렉터리 파티션의 복제 세트에 DNS 서버를 추가합니다.|  
|[dnscmd /enumdirectorypartitions](#BKMK_9)|서버에 대 한 DNS 응용 프로그램 디렉터리 파티션을 나열합니다.|  
|[dnscmd /enumrecords](#BKMK_10)|영역에 리소스 레코드를 나열합니다.|  
|[dnscmd /enumzones](#BKMK_11)|지정 된 서버에서 호스트 된 영역을 나열 합니다.|  
|[dnscmd /exportsettings](#BKMK_25a)|텍스트 파일에 서버 구성 정보를 씁니다.|  
|[dnscmd /info](#BKMK_12)|서버 정보를 가져옵니다.|  
|[dnscmd /ipvalidate](#BKMK_29a)|원격 DNS 서버를 확인합니다.|  
|[dnscmd /nodedelete](#BKMK_13)|영역에 있는 노드에 대 한 모든 레코드를 삭제합니다.|  
|[dnscmd /recordadd](#BKMK_14)|영역에 리소스 레코드를 추가합니다.|  
|[dnscmd /recorddelete](#BKMK_15)|영역에서 리소스 레코드를 제거합니다.|  
|[dnscmd /resetforwarders](#BKMK_16)|재귀 쿼리를 전달 하도록 DNS 서버를 설정 합니다.|  
|[dnscmd /resetlistenaddresses](#BKMK_17)|DNS 요청을 처리 하는 서버 IP 주소를 설정 합니다.|  
|[dnscmd /startscavenging](#BKMK_18)|청소 하는 서버를 시작합니다.|  
|[dnscmd /statistics](#BKMK_19)|쿼리 또는 서버 통계 데이터를 지웁니다.|  
|[dnscmd /unenlistdirectorypartition](#BKMK_20)|DNS 응용 프로그램 디렉터리 파티션의 복제 세트에서 DNS 서버를 제거합니다.|  
|[dnscmd /writebackfiles](#BKMK_21)|영역 또는 루트 힌트에 대 한 모든 데이터 파일에 저장 합니다.|  
|[dnscmd /zoneadd](#BKMK_22)|DNS 서버에서 새 영역을 만듭니다.|  
|[dnscmd /zonechangedirectorypartition](#BKMK_23)|영역 상주 하는 디렉터리 파티션을 변경 합니다.|  
|[dnscmd /zonedelete](#BKMK_24)|DNS 서버에서 영역을 삭제합니다.|  
|[dnscmd /zoneexport](#BKMK_25)|텍스트 파일에는 영역의 리소스 레코드를 씁니다.|  
|[dnscmd /zoneinfo](#BKMK_26)|영역 정보를 표시합니다.|  
|[dnscmd /zonepause](#BKMK_27)|영역 일시 중지합니다.|  
|[dnscmd /zoneprint](#BKMK_28)|영역에서 모든 레코드를 표시합니다.|  
|[dnscmd /zonerefresh](#BKMK_30)|마스터 영역에서 보조 영역을 고칩니다.|  
|[dnscmd /zonereload](#BKMK_31)|해당 데이터베이스에서 영역을 다시 로드합니다.|  
|[dnscmd /zoneresetmasters](#BKMK_32)|보조 영역에 영역 전송 정보를 제공 하는 마스터 서버를 변경 합니다.|  
|[dnscmd /zoneresetscavengeservers](#BKMK_33)|영역 청소할 하는 서버를 변경 합니다.|  
|[dnscmd /zoneresetsecondaries](#BKMK_34)|영역에 대 한 보조 정보를 다시 설정합니다.|  
|[dnscmd /zoneresettype](#BKMK_29)|영역 종류를 변경합니다.|  
|[dnscmd /zoneresume](#BKMK_35)|영역 다시 시작합니다.|  
|[dnscmd /zoneupdatefromds](#BKMK_36)|Active directory Domain Services (AD DS)에서 데이터를 사용 하 여 active directory 통합된 영역을 업데이트합니다.|  
|[dnscmd /zonewriteback](#BKMK_37)|영역 데이터를 파일에 저장 합니다.|  
### <a name="BKMK_1"></a>dnscmd /ageallrecords  
지정 된 영역 또는 노드는 DNS 서버에서 리소스 레코드에 타임 스탬프에 현재 시간을 설정합니다.  
#### <a name="syntax"></a>구문  
```  
dnscmd [<ServerName>] /ageallrecords <ZoneName>[<NodeName>] | [/tree]|[/f]  
```  
#### <a name="parameters"></a>매개 변수  
<ServerName>  
IP 주소나 정규화 된 도메인 이름 (FQDN)으로 호스트 이름으로 표시는 관리자는 계획을 관리 하는 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다.  
<ZoneName>  
영역의 FQDN을 지정합니다.  
<NodeName>  
영역에서 특정 노드 또는 하위 트리를 지정합니다. *NodeName* 에서 다음을 사용 하는 영역 노드 또는 하위 트리를 지정 합니다.  
-   @ 루트 영역 또는 FQDN  
-   노드 (끝에 마침표 (.)로 이름)의 FQDN  
-   영역 루트에 상대적인 이름에 대 한 단일 레이블  
/tree  
모든 자식 노드는 타임 스탬프를 받을 수도 지정 합니다.  
/f  
확인을 요청 하지 않고 명령을 실행 합니다.  
#### <a name="remarks"></a>설명  
-   **ageallrecords** DNS의 현재 버전과 이전 버전의 DNS는 에이징 및 청소 지원 되지 않았습니다 간의 이전 버전과 호환성을 위해 명령입니다. 현재 시간 타임 스탬프가 타임 스탬프를 갖지 않는 리소스 레코드를 추가 하 고 현재 시간 타임 스탬프가 없는 리소스 레코드에 설정 합니다.  
-   레코드에 타임 스탬프가 추가 하지 않으면 레코드 청소 발생 하지 않습니다. NS (이름 서버) 리소스 레코드를 (soa) 리소스 레코드의 시작 부분 및 인터넷 이름 서비스 WINS (Windows) 리소스 레코드 청소 프로세스에 포함 되지 않은 고 타임 스탬프가 기록 없는 경우에는 **ageallrecords** 명령 실행 합니다.  
-   이 명령은 DNS 서버 및 영역에 대 한 청소를 사용 하지 않으면 실패 합니다. 영역에 대 한 청소를 사용 하는 방법에 대 한 정보를 참조 하세요. 합니다 **에이징** 매개 변수 영역 수준 구문에 [구성](#BKMK_3) 명령입니다.  
-   DNS 리소스 레코드에 타임 스탬프가 추가 값을 사용 하면 Windows 2000, Windows XP 또는 Windows Server 2003 이외의 운영 체제에서 실행 되는 DNS 서버와 호환 되지 않습니다. 사용 하 여 추가 하는 타임 스탬프는 **ageallrecords** 명령을 취소할 수 없습니다.  
-   선택적 매개 변수를 지정 하는 경우이 명령은 지정 된 노드에서 모든 리소스 레코드를 반환 합니다. 선택적 매개 변수 중 하나에 대 한 값이 지정 하는 경우 **dnscmd** 값 또는 선택적 매개 변수 또는 매개 변수에서 지정 된 값을 해당 하는 리소스 레코드를 열거 합니다.  
#### <a name="example"></a>예제  
참조 [예제 1: 리소스 레코드에 타임 스탬프에 현재 시간을 설정](https://technet.microsoft.com/library/cc784399(v=ws.10).aspx)합니다.  
### <a name="BKMK_2"></a>dnscmd /clearcache  
지정된 된 DNS 서버에서 리소스 레코드의 DNS 캐시 메모리를 지웁니다.  
#### <a name="syntax"></a>구문  
```  
dnscmd [<ServerName>] /clearcache  
```  
#### <a name="parameters"></a>매개 변수  
<ServerName>  
IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다.  
#### <a name="sample-usage"></a>샘플 사용  
`dnscmd dnssvr1.contoso.com /clearcache`  
### <a name="BKMK_3"></a>dnscmd /config  
DNS 서버 및 개별 영역에 대 한 레지스트리 값을 변경합니다. 서버 수준 설정과 영역 수준 설정을 허용합니다.  
> [!CAUTION]  
> 편집 하지 마십시오 레지스트리 직접 대체 하지 않으면. 레지스트리 편집기의 성능이 저하, 하면 시스템이 손상 또는 Windows를 다시 설치 해야 할 수 있는 설정을 허용 표준 보호를 무시 합니다. 안전 하 게 제어판 또는 Microsoft Management Console (mmc)에서 프로그램을 사용 하 여 대부분의 레지스트리 설정을 변경할 수 있습니다. 레지스트리를 직접 편집 해야 하는 경우 먼저 백업 합니다. 자세한 내용은 레지스트리 편집기 도움말을 읽습니다.  
#### <a name="server-level-syntax"></a>서버 수준 구문  
```  
dnscmd [<ServerName>] /config <Parameter>  
```  
#### <a name="dnscmd-config"></a>dnscmd /config  
지정 된 서버의 구성을 수정합니다.  
#### <a name="parameters"></a>매개 변수  
<ServerName>  
로컬 컴퓨터 구문, IP 주소, FQDN 또는 호스트 이름으로 표시 하려고를 관리 하는 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다.  
<Parameter>  
설정을 지정 하 고, 필요에 따라 값입니다. 매개 변수 값에는이 구문을 사용합니다. *Parameter* [*Value*]  
다음 매개 변수 값이이 섹션의 나머지 부분에 설명 되어 있습니다.  
-   **/addressanswerlimit**  
-   **/bindsecondaries**  
-   **/bootmethod**  
-   **/defaultagingstate**  
-   **/defaultnorefreshinterval**  
-   **/defaultrefreshinterval**  
-   **/disableautoreversezones**  
-   **/disablensrecordsautocreation**  
-   **/dspollinginterval**  
-   **/dstombstoneinterval**  
-   **/ednscachetimeout**  
-   **/enablednsprobes**  
-   **/enablednssec**  
-   **/enableglobalnamessupport**  
-   **/enableglobalqueryblocklist**  
-   **/eventloglevel**  
-   **/forwarddelegations**  
-   **/forwardingtimeout**  
-   **/globalnamesqueryorder**  
-   **/globalqueryblocklist**  
-   **/isslave**  
-   **/localnetpriority**  
-   **/logfilemaxsize**  
-   **/logfilepath**  
-   **/logipfilterlist**  
-   **/loglevel**  
-   **/maxcachesize**  
-   **/maxcachettl**  
-   **/namecheckflag**  
-   **/notcp**  
-   **/norecursion**  
-   **/recursionretry**  
-   **/recursiontimeout**  
-   **/roundrobin**  
-   **/rpcprotocol**  
-   **/scavenginginterval**  
-   **/secureresponses**  
-   **/sendport**  
-   **/strictfileparsing**  
-   **/updateoptions**  
-   **/writeauthorityns**  
-   **/xfrconnecttimeout**  
**/addressanswerlimit [0|5-28]**  
DNS 서버가 쿼리에 대 한 응답으로 보낼 수 있는 호스트 레코드의 최대 수를 지정 합니다. 값 영 (0) 이거나 28 레코드를 통해 5의 범위에 있을 수 있습니다. 기본값은 영 (0).  
**/bindsecondaries[0|1]**  
최대 압축 효과 성과 얻을 수 있도록 영역 전송의 형식을 변경 합니다. 그러나이 형식은 버클리 인터넷 이름 도메인 (바인딩)의 이전 버전과 호환 되지 않습니다.  
**0**  
최대 압축을 사용합니다. 이 형식은 BIND 버전 4.9.4와 호환 되 고 이상만 해당 됩니다.  
**1**  
타사 DNS 서버에 메시지 별로 하나의 리소스 레코드를 보냅니다. 이 형식은 이전 버전 바인딩 4.9.4 호환 됩니다. 이 값은 기본 설정입니다.  
**/bootmethod[0|1|2|3]**  
DNS 서버를 구성 정보를 가져오는 소스를 결정 합니다.  
**0**  
구성 정보의 출처를 지웁니다.  
**1**  
기본적으로 %systemroot%\System32\DNS DNS 디렉터리에 있는 바인딩 파일에서 로드 합니다.  
**2**  
레지스트리에서 로드 합니다.  
**3**  
AD DS 및 레지스트리를 로드 합니다. 이 값은 기본 설정입니다.  
**/defaultagingstate[0|1]**  
새로 만든된 영역에서 기본적으로 DNS 청소 기능이 사용 되는지 여부를 결정 합니다.  
**0**  
청소 하는 사용 하지 않도록 설정 합니다. 이 값은 기본 설정입니다.  
**1**  
청소 수 있습니다.  
**/defaultnorefreshinterval[0x1-0xFFFFFFFF|0xA8]**  
동적으로 업데이트 된 레코드에 대 한 없는 새로 고침 허용 되는 기간을 설정 합니다. 서버에 영역이이 값을 자동으로 상속 합니다. 기본값을 변경 하려면의 범위에 값을 입력 **0x1 0xFFFFFFFF**합니다. 서버에서 기본값은 **0xA8**합니다.  
**/defaultrefreshinterval [0x1-0xFFFFFFFF|0xA8]**  
DNS 레코드에 대 한 동적 업데이트에 대해 허용 되는 기간을 설정 합니다. 서버에 영역이이 값을 자동으로 상속 합니다. 기본값을 변경 하려면의 범위에 값을 입력 **0x1 0xFFFFFFFF**합니다. 서버에서 기본값은 **0xA8**합니다.  
**/disableautoreversezones [0|1]**  
역방향 조회 영역을 자동 생성을 사용 하지 않도록 설정 하거나 사용 합니다. 역방향 조회 영역 IP (인터넷 프로토콜) 주소를 DNS 도메인 이름 확인을 제공합니다.  
**0**  
역방향 조회 영역을 자동으로 만들을 수 있습니다. 이 값은 기본 설정입니다.  
**1**  
역방향 조회 영역을 자동 생성을 사용 하지 않도록 설정 합니다.  
**/disablensrecordsautocreation {0|1}**  
여부 DNS 서버가 자동으로 NS (이름 서버) 리소스 레코드를 만듭니다 호스팅하는 영역에 대 한을 지정 합니다.  
**0**  
영역에 대 한 이름 서버 (NS) 리소스 레코드를 만들고 자동으로 DNS 서버가 호스트 합니다.  
**1**  
자동으로 만들지 않으므로 영역에 대 한 이름 서버 (NS) 리소스 레코드는 DNS 서버가 호스트 합니다.  
**/dspollinginterval 0-30**  
DNS 서버를 폴링합니다 AD DS 변경 내용 active directory에 영역을 통합 하는 빈도 지정 합니다.  
**/dstombstoneinterval [1-30]**  
AD DS에서 삭제 된 레코드를 유지 하는 시간 (초) 시간의 양입니다.  
**/ednscachetimeout [<seconds>]**  
확장 된 DNS (EDNS) 정보가 캐시 되는 시간 (초) 수를 지정 합니다. 최소값은 3600 하 고 최대값은 15,724,800 합니다. 기본값은 604, 800 초 (1 주)입니다.  
**/enableednsprobes {0|1}**  
사용 하거나 EDNS를 지원 하는지 확인 하기 위해 다른 서버를 검색 하는 서버를 사용 하지 않도록 설정 합니다.  
**0**  
EDNS 프로브에 대 한 활성 지원을 사용할 수 없습니다.  
**1**  
활성 EDNS 프로브 지원할을 수 있습니다.  
**/enablednssec {0|1}**  
사용 하거나 지원에 대 한 보안 확장 DNSSEC (DNS)를 사용 하지 않도록 설정 합니다.  
**0**  
DNSSEC를 사용 하지 않도록 설정 합니다.  
**1**  
DNSSEC를 수 있습니다.  
**/enableglobalnamessupport {0|1}**  
사용 하거나 GlobalNames 영역에 대 한 지원을 사용 하지 않도록 설정 합니다. GlobalNames 영역 포리스트에 단일 레이블 DNS 이름 확인을 지원합니다.  
**0**  
사용 하지 않도록 설정 GlobalNames 영역에 대 한 지원. 이 명령의 값을 설정 하면 **0**, DNS 서버 서비스가 단일 레이블 이름을 GlobalNames 영역에서 해결 되지 않습니다.  
**1**  
GlobalNames 영역에 대 한 수 있도록 지원합니다. 이 명령의 값을 설정 하면 **1**, DNS 서버 서비스는 단일 레이블 이름을 GlobalNames 영역에서 해결 합니다.  
**/enableglobalqueryblocklist {0|1}**  
사용 하거나 목록에서 이름에 대 한 이름 확인을 차단 하는 글로벌 쿼리 차단 목록에 대 한 지원을 사용 하지 않도록 설정 합니다. DNS 서버 서비스를 만들고 서비스를 처음 시작할 때 기본적으로 글로벌 쿼리 차단 목록을 사용 합니다. 현재 글로벌 쿼리 차단 목록을 보려면 사용 하 여는 **dnscmd /info /globalqueryblocklist** 명령입니다.  
**0**  
사용 하지 않도록 설정 글로벌 쿼리 차단 목록을 지원합니다. 이 명령의 값을 설정 하면 **0**, DNS 서버 서비스가 차단 목록에는 이름에 대 한 쿼리에 응답 합니다.  
**1**  
글로벌 쿼리 차단 목록을 지원 합니다. 이 명령의 값을 설정 하면 **1**, DNS 서버 서비스가 차단 목록에는 이름에 대 한 쿼리에 응답 하지 않습니다.  
**/eventloglevel [0 | 1 | 2 | 4]**  
이벤트는 이벤트 뷰어에서 DNS 서버 로그에 기록 됩니다 결정 합니다.  
**0**  
없는 이벤트를 기록 합니다.  
**1**  
오류만 기록 합니다.  
**2**  
오류 및 경고를 기록합니다.  
**4**  
오류, 경고 및 정보 이벤트를 기록합니다. 이 값은 기본 설정입니다.  
**/forwarddelegations [0 | 1]**  
DNS 서버 위임된 subzone에 대 한 쿼리를 처리 하는 방법을 결정 합니다. 이러한 쿼리는 DNS 서버에 대 한 하거나 참조 하는 쿼리에서 subzone 하 라는 전달자 목록에 보낼 수 있습니다. 설정의 항목 전달이 사용 하는 경우에 사용 됩니다.  
**0**  
자동으로 적절 한 subzone에 위임된 될을 참조 하는 쿼리를 보냅니다. 이 값은 기본 설정입니다.  
**1**  
기존 전달자에 위임 된 subzone를 참조 하는 쿼리를 전달 합니다.  
**/forwardingtimeout [<seconds>]**  
초 단위 시간 (0x1 0xFFFFFFFF) 전달자 다른 전달자를 시도 하기 전에 응답을 기다리는 DNS 서버를 결정 합니다. 기본값은 **0x5**, 5 초입니다.  
**/globalneamesqueryorder** {**0 | 1**}  
여부 DNS 서버 서비스는 먼저 검색 GlobalNames 영역 또는 로컬 영역에서 이름을 확인할 때 지정 합니다.  
**0**  
DNS 서버 서비스는 신뢰할 수 있는 영역을 쿼리 하기 전에 GlobalNames 영역을 쿼리하여 이름을 확인 하려고 합니다.  
**1**  
DNS 서버 서비스가 신뢰할 수 있는 GlobalNames 영역을 쿼리 하기 전에 영역을 쿼리하여 이름을 확인 하려고 합니다.  
**/globalqueryblocklist[[<name> [<name>]...]**  
현재 글로벌 쿼리 차단 목록을 지정 하는 이름의 목록을 바꿉니다. 모든 이름을 지정 하지 않으면이 명령은 차단 목록을 지웁니다. 기본적으로 글로벌 쿼리 차단 목록은 다음 항목을 포함 합니다.  
-   isatap  
-   wpad  
DNS 서버 서비스 경우 제거할 수 이러한 이름 중 하나 또는 모두를 처음 시작할 때 기존 영역에서 이러한 이름을 찾습니다.  
**/isslave [0|1]**  
전달 하는 쿼리 응답을 받지 때 DNS 서버가 응답 하는 방법을 결정 합니다.  
**0**  
DNS 서버 하위 항목이 아님을 지정 (라고도 *슬레이브*). 전달자 응답 하지 않을 경우에 DNS 서버 쿼리 자체를 확인 하려고 합니다. 이 값은 기본 설정입니다.  
**1**  
DNS 서버 하위 항목 임을 지정 합니다. 전달자 응답 하지 않을 경우 DNS 서버 검색을 종료 하 고 해결 프로그램에 오류 메시지를 보냅니다.  
**/localnetpriority [0|1]**  
DNS 서버에 동일한 이름의 여러 호스트 레코드 호스트 레코드가 반환 되는 순서를 결정 합니다.  
**0**  
DNS 데이터베이스에 나열 된 순서에 레코드를 반환 합니다.  
**1**  
반환 레코드를 유사한 ip 주소를 먼저 네트워크입니다. 이 값은 기본 설정입니다.  
**/logfilemaxsize [<size>]**  
(0xFFFFFFFF 0x10000) 바이트 Dns.log 파일의 최대 크기를 지정합니다. DNS는 파일이 최대 크기에 도달 하면 가장 오래 된 이벤트를 덮어씁니다. 기본 크기는 0x400000입니다, 4 메가바이트 (MB)입니다.  
**/logfilepath [<path+LogFileName>]**  
Dns.log 파일의 경로 지정합니다. 기본 경로 %systemroot%\System32\Dns\Dns.log 합니다. 형식을 사용 하 여 다른 경로 지정할 수 있습니다 *경로 + LogFileName*합니다.  
**/logipfilterlist <IPaddress> [,<IPaddress>...]**  
어떤 패킷이 디버그 로그 파일에 기록 됩니다 지정 합니다. 항목은 IP 주소의 목록입니다. 목록에서 IP 주소에서 이동 하는 패킷이 기록 됩니다.  
**/loglevel [<Eventtype>]**  
이벤트의 유형을 Dns.log 파일에 기록 되는지 결정 합니다. 각 이벤트 종류는 16 진수 숫자로 표현 됩니다. 로그에 하나 이상의 이벤트를 하려는 경우 16 진수 추가 사용 하 여 값을 추가 하려면 합계를 입력 합니다.  
**0x0**  
DNS 서버 로그를 만들지 않습니다. 이것이 기본 항목입니다.  
**0x10**  
쿼리를 기록합니다.  
**0x10**  
알림을 기록합니다.  
**0x20**  
업데이트를 기록합니다.  
**0xFE**  
Nonquery 트랜잭션을 기록합니다.  
**0x100**  
로그 트랜잭션을 질문입니다.  
**0x200**  
답변을 기록합니다.  
**0x1000**  
로그에는 패킷을 보냅니다.  
**0x2000**  
패킷을 수신 하는 로그입니다.  
**0x4000**  
사용자 데이터 그램 프로토콜 (UDP) 패킷을 기록합니다.  
**0x8000**  
패킷을 전송 제어 프로토콜 (TCP)을 기록합니다.  
**0xFFFF**  
모든 패킷이 기록합니다.  
**0x10000**  
Active directory 쓰기 트랜잭션을 기록합니다.  
**0x20000**  
Active directory 업데이트 트랜잭션을 기록합니다.  
**0x1000000**  
전체 패킷 로그 합니다.  
**0x80000000**  
로그 쓰기 트랜잭션입니다.  
**/maxcachesize**  
DNS 서버의 메모리 캐시의 최대 크기 (kb)를 지정합니다.  
**/maxcachettl [<seconds>]**  
초 단위 시간 (0x0 0xFFFFFFFF) 레코드를 캐시에 저장 된 것을 결정 합니다. 하는 경우는 **0x0** 설정을 사용 하는 경우 DNS 서버 레코드를 캐시 하지 않습니다. 기본 설정은 **0x15180** (86, 400 초 또는 1 일)입니다.  
**/maxnegativecachettl [<seconds>]**  
초 단위 시간 (0x1 0xFFFFFFFF) 쿼리에 부정 응답을 기록 하는 항목은 저장 DNS 캐시에 지정 합니다. 기본 설정은 **0x384** (900 초)입니다.  
**/namecheckflag [0 | 1 | 2 | 3].**  
DNS 이름을 확인할 때 사용 하는 문자 표준 지정 합니다.  
**0**  
인터넷 엔지니어링 작업을 준수 하는 ANSI 문자를 사용 하 여 강제로 주석 (Rfc)에 대 한 (IETF) 요청 합니다.  
**1**  
IETF Rfc을 반드시 준수 하지 않는 ANSI 문자를 사용 합니다.  
**2**  
사용 하 여 멀티 바이트 UCS 변환 형식 8 (u t F-8) 문자입니다. 이 값은 기본 설정입니다.  
**3**  
모든 문자를 사용합니다.  
**/norecursion [0|1]**  
DNS 서버 재귀적 이름 확인을 수행 하는지 여부를 결정 합니다.  
**0**  
쿼리에서 요청 된 경우 DNS 서버 재귀적 이름 확인을 수행 합니다. 이 값은 기본 설정입니다.  
**1**  
DNS 서버는 재귀적 이름 확인을 수행 하지 않습니다.  
**/notcp**  
이 매개 변수는 더 이상 현재 버전의 Windows Server 효과가 없습니다.  
**/recursionretry [<seconds>]**  
DNS 서버에서 원격 서버에 연결을 다시 시도 하기 전에 대기 하는 초 (0x1 0xFFFFFFFF)의 수를 결정 합니다. 기본 설정은 0x3 (3 초)입니다. 재귀 속도가 느린 광역 네트워크 (WAN) 링크를 통해 발생 하는 경우이 값을 늘려야 합니다.  
**/recursiontimeout [<seconds>]**  
DNS 서버에서 원격 서버 연결 시도 중단 하기 전에 대기 하는 초 (0x1 0xFFFFFFFF)의 수를 결정 합니다. 설정 범위에서 **0x1** 통해 **0xFFFFFFFF**합니다. 기본 설정은 **0xF** (15 초)입니다. 재귀 느린 WAN 링크를 통해 발생 하는 경우이 값을 늘려야 합니다.  
**/roundrobin [0|1]**  
서버에 동일한 이름의 여러 호스트 레코드 때 호스트 레코드가 반환 됩니다 순서를 결정 합니다.  
0  
DNS 서버는 라운드 로빈을 사용 하지 않습니다. 대신, 모든 쿼리에 첫 번째 레코드를 반환 합니다.  
**1**  
DNS 서버가 일치 하는 레코드 목록 맨 위에서 반환 레코드 사이에서 회전 합니다. 이 값은 기본 설정입니다.  
**/rpcprotocol [0x0|0x1|0x2|0x4|0xFFFFFFFF]**  
원격 프로시저 호출 (RPC)은 DNS 서버에서 연결을 사용 하는 프로토콜을 지정 합니다.  
**0x0**  
Dns RPC를 사용 하지 않도록 설정 합니다.  
**0x1**  
TCP/IP를 사용합니다.  
**0x2**  
명명 된 파이프를 사용 합니다.  
**0x4**  
로컬 프로시저 호출 (LPC)를 사용합니다.  
**0xFFFFFFFF**  
모든 프로토콜입니다. 이 값은 기본 설정입니다.  
**/scavenginginterval [<hours>]**  
DNS 서버에 대 한 청소 기능을 사용 하며 청소 주기 사이의 시간 (0x0 0xFFFFFFFF)의 수를 설정 하는지 여부를 결정 합니다. 기본 설정은 **0x0**, DNS 서버에 대 한 청소를 해제 합니다. 설정 보다 큰 **0x0** 서버에 대 한 청소 하 고 청소 주기 사이의 시간을 설정 합니다.  
**/secureresponses [0|1]**  
DNS 캐시에 저장 된 레코드를 필터링 하는지 여부를 결정 합니다.  
**0**  
쿼리 이름에 대 한 모든 응답 하는 캐시에 저장합니다. 이 값은 기본 설정입니다.  
**1**  
캐시에 동일한 DNS 하위에 속하는 레코드에만 저장 합니다.  
**/sendport [<port>]**  
DNS를 사용 하 여 다른 DNS 서버에 재귀 쿼리를 보내는 포트 번호 (0x0 0xFFFFFFFF)를 지정 합니다. 기본 설정은 **0x0**, 즉, 포트 번호 임의로 선택 합니다.  
**/serverlevelplugindll[<Dllpath>]**  
사용자 지정 플러그 인의 경로 지정합니다. 때 *Dllpath* 유효한 DNS 서버 플러그 인을 DNS 서버 이름 쿼리를 로컬로 모든 범위를 벗어나는 호스트 영역을 해결 하려면 플러그 인에서 함수 호출의 정규화 된 경로 이름을 지정 합니다. 쿼리 이름이 플러그인의 범위를 벗어난 경우 DNS 서버가 구성 된 대로 전달 또는 재귀를 사용 하 여 이름 확인을 수행 합니다. 하는 경우 *Dllpath* 지정 하지 않으면 사용자 지정 플러그 인을 이전에 구성한 경우 사용자 지정 플러그 인을 사용 하려면 DNS 서버를 중지 합니다.  
**/strictfileparsing [0|1]**  
영역을 로드 하는 동안 잘못 된 레코드를 발견 한 경우 DNS 서버의 동작을 결정 합니다.  
**0**  
DNS 서버는 서버에서 잘못 된 레코드를 발견 하는 경우에 영역을 로드할 계속 합니다. 이 오류는 DNS 로그에 기록 됩니다. 이 값은 기본 설정입니다.  
**1**  
DNS 서버가 영역을 로드를 중지 하 고 DNS 로그에 오류를 기록 합니다.  
**/updateoptions <RecordValue>**  
지정 된 유형의 레코드의 동적 업데이트를 금지합니다. 로그에서 허용 하지 않도록 둘 이상의 레코드 종류를 하려는 경우 16 진수 추가 사용 하 여 값을 추가 하려면 합계를 입력 합니다.  
**0x0**  
모든 레코드 종류를 제한 하지 않습니다.  
**0x1**  
시작 (soa) 리소스 레코드를 제외합니다.  
**0x2**  
이름 서버 (NS) 리소스 레코드를 제외합니다.  
**0x4**  
이름 서버 (NS) 리소스 레코드의 위임에서 제외 됩니다.  
**0x8**  
서버 호스트 레코드를 제외합니다.  
**0x100**  
보안 동적 업데이트 중 시작 (soa) 리소스 레코드를 제외합니다.  
**0x200**  
보안 동적 업데이트 하는 동안 루트 이름 서버 (NS) 리소스 레코드를 제외합니다.  
**0x30F**  
표준 동적 업데이트 하는 동안 이름 서버 (NS) 리소스 레코드 (soa) 리소스 레코드 및 서버 호스트 레코드의 시작 부분을 제외합니다. 보안 동적 업데이트 하는 동안 루트 이름 서버 (NS) 리소스 레코드와 시작 (soa) 리소스 레코드를 제외합니다. 위임 하 고, 서버 업데이트를 호스트 합니다.  
**0x400**  
보안 동적 업데이트 중 위임 이름 서버 (NS) 리소스 레코드를 제외합니다.  
**0x800**  
보안 동적 업데이트 하는 동안 서버 호스트 레코드를 제외합니다.  
**0x1000000**  
위임 서명자 (DS) 레코드를 제외합니다.  
**0x80000000**  
DNS 동적 업데이트를 사용 하지 않도록 설정 합니다.  
**/writeauthorityns [0|1]**  
DNS 서버는 응답의 기관 섹션에 이름 서버 (NS) 리소스 레코드를 기록 하는 시기를 결정 합니다.  
**0**  
조회만의 기관 섹션에 이름 서버 (NS) 리소스 레코드를 씁니다. 이 설정은 Rfc 2181, DNS 사양에 대 한 설명 이며 Rfc 1034, 도메인 이름은 개념 및 기능을 사용 하 여 준수합니다. 이 값은 기본 설정입니다.  
**1**  
모든 성공적인 신뢰할 수 있는 응답 기관 섹션에 이름 서버 (NS) 리소스 레코드를 씁니다.  
**/xfrconnecttimeout [<seconds>]**  
보조 서버에서 전송 응답에 대 한 주 DNS 서버를 대기 하는 시간 (0x0 0xFFFFFFFF)의 수를 결정 합니다. 기본값은 **0x1E** (30 초)입니다. 시간 제한 값이 만료 되 면 연결이 종료 됩니다.  
#### <a name="zone-level-syntax"></a>영역 수준 구문  
```  
dnscmd /config <Parameters>  
```  
#### <a name="dnscmd-config"></a>dnscmd /config  
지정된 된 영역의 구성을 수정합니다.  
#### <a name="parameters"></a>매개 변수  
**<Parameters>**  
영역 이름 및 값을 옵션으로는 설정을 지정 합니다. 매개 변수 값에는이 구문을 사용합니다. *ZoneName 매개 변수* [*값*]  
다음 매개 변수 값이이 섹션의 나머지 부분에 문서화 되어 있습니다.  
-   **/aging**  
-   **/allownsrecordsautocreation**  
-   **/allowupdate**  
-   **/forwarderslave**  
-   **/forwardertimeout**  
-   **/norefreshinterval**  
-   **/refreshinterval**  
-   **/securesecondaries**  
**/aging <ZoneName>**  
사용 하거나 특정 영역에 청소를 사용 하지 않도록 설정 합니다.  
**/allownsrecordsautocreation  <ZoneName> [<Value>]**  
DNS 서버 이름 서버 (NS) 리소스 레코드 autocreation 설정 보다 우선 합니다. 이 영역에 대 한 이전에 등록 된 이름 서버 (NS) 리소스 레코드의 영향을 받지 않습니다. 따라서를 수동으로 제거 해야 하지 않을 경우 해당 합니다.  
**/allowupdate <ZoneName>**  
지정된 된 영역 동적 업데이트를 허용 하는지 여부를 결정 합니다.  
**/forwarderslave <ZoneName>**  
DNS 서버 재정의 **/isslave** 설정 합니다.  
**/forwardertimeout <ZoneName>**  
초 단위 시간 전달자 다른 전달자를 시도 하기 전에 응답을 기다리는 DNS 영역 결정 합니다. 이 값은 서버 수준에서 설정 하는 값을 재정의 합니다.  
**/norefreshinterval <ZoneName>**  
이때 없는 새로 고침 동적으로 업데이트할 수는 지정 된 영역에서 DNS 레코드를 영역에 대 한 시간 간격을 설정 합니다.  
**/refreshinterval <ZoneName>**  
새로 고침 동적으로 업데이트할 수는 지정 된 영역에서 DNS 레코드를 영역에 대 한 시간 간격을 설정 합니다.  
**/securesecondaries <ZoneName>**  
이 영역에 대 한 마스터 서버에서 영역 업데이트를 받을 수 있는 보조 서버를 결정 합니다.  
#### <a name="remarks"></a>설명  
-   영역 이름 매개 변수 영역 수준에 대해서만 지정 되어야 합니다.  
### <a name="BKMK_4"></a>dnscmd /createbuiltindirectorypartitions  
DNS 응용 프로그램 디렉터리 파티션을 만듭니다. DNS가 설치 되는 서비스에 대 한 응용 프로그램 디렉터리 파티션은 포리스트 및 도메인 수준에서 생성 됩니다. 이 명령을 사용 하 여 삭제 되거나 생성 되지 않고 된 DNS 응용 프로그램 디렉터리 파티션을 만들 수 있습니다. 사용 하 여,이 명령은 도메인에 대 한 기본 제공 DNS 디렉터리 파티션을 만듭니다.  
#### <a name="syntax"></a>구문  
```  
dnscmd [<ServerName>] /createbuiltindirectorypartitions [/forest] [/alldomains]   
```  
#### <a name="parameters"></a>매개 변수  
**<ServerName>**  
IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다.  
**/forest**  
포리스트에 대 한 DNS 디렉터리 파티션을 만듭니다.  
**/alldomains**  
포리스트의 모든 도메인에 대 한 DNS 파티션을 만듭니다.  
### <a name="BKMK_5"></a>dnscmd /createdirectorypartition  
DNS 응용 프로그램 디렉터리 파티션을 만듭니다. DNS가 설치 되는 서비스에 대 한 응용 프로그램 디렉터리 파티션은 포리스트 및 도메인 수준에서 생성 됩니다. 이 작업에는 추가 DNS 응용 프로그램 디렉터리 파티션을 만듭니다.  
#### <a name="syntax"></a>구문  
```  
dnscmd [<ServerName>] /createdirectorypartition <PartitionFQDN>  
```  
#### <a name="parameters"></a>매개 변수  
**<ServerName>**  
IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다.  
**<PartitionFQDN>**  
생성 되는 DNS 응용 프로그램 디렉터리 파티션의 FQDN입니다.  
### <a name="BKMK_6"></a>dnscmd /deletedirectorypartition  
기존 DNS 응용 프로그램 디렉터리 파티션을 제거합니다.  
#### <a name="syntax"></a>구문  
```  
dnscmd [<ServerName>] /deletedirectorypartition <PartitionFQDN>  
```  
#### <a name="parameters"></a>매개 변수  
**<ServerName>**  
IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다.  
**<PartitionFQDN>**  
DNS 응용 프로그램 디렉터리 파티션 제거 될의 FQDN입니다.  
### <a name="BKMK_7"></a>dnscmd /directorypartitioninfo  
지정 된 DNS 응용 프로그램 디렉터리 파티션에 대 한 정보를 나열 합니다.  
#### <a name="syntax"></a>구문  
```  
dnscmd [<ServerName>] /directorypartitioninfo <PartitionFQDN> [/detail]   
```  
#### <a name="parameters"></a>매개 변수  
**<ServerName>**  
IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다.  
**<PartitionFQDN>**  
DNS 응용 프로그램 디렉터리 파티션에의 FQDN입니다.  
**/detail**  
응용 프로그램 디렉터리 파티션에 대 한 모든 정보를 나열 합니다.  
### <a name="BKMK_8"></a>dnscmd /enlistdirectorypartition  
지정 된 디렉터리 파티션의 복제 세트에 DNS 서버를 추가합니다.  
#### <a name="syntax"></a>구문  
```  
dnscmd [<ServerName>] /enlistdirectorypartition <PartitionFQDN>  
```  
#### <a name="parameters"></a>매개 변수  
**<ServerName>**  
IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다.  
**<PartitionFQDN>**  
DNS 응용 프로그램 디렉터리 파티션에의 FQDN입니다.  
### <a name="BKMK_9"></a>dnscmd /enumdirectorypartitions  
지정된 된 서버에 대 한 DNS 응용 프로그램 디렉터리 파티션을 나열합니다.  
#### <a name="syntax"></a>구문  
```  
dnscmd [<ServerName>] /enumdirectorypartitions [/custom]   
```  
#### <a name="parameters"></a>매개 변수  
**<ServerName>**  
IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다.  
**/custom**  
사용자가 만든 디렉터리 파티션으로 나열합니다.  
### <a name="BKMK_10"></a>dnscmd /enumrecords  
DNS 영역에 지정 된 노드의 리소스 레코드를 나열합니다.  
#### <a name="syntax"></a>구문  
```  
dnscmd [<ServerName>] /enumrecords <ZoneName> <NodeName> [/type <RRtype> <Rrdata>] [/authority] [/glue] [/additional] [/node | /child | /startchild<ChildName>] [/continue | /detail]   
```  
#### <a name="parameters"></a>매개 변수  
**<ServerName>**  
IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려고 하는 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다.  
**/enumrecords**  
지정된 된 된 영역에 리소스 레코드를 나열합니다.  
**<ZoneName>**  
리소스 레코드가 속해 있는 영역의 이름을 지정 합니다.  
**<NodeName>**  
리소스 레코드의 노드 이름을 지정합니다.  
**/type <RRtype> <Rrdata>**  
예상 되는 데이터의 형식과 나열 될 리소스 레코드 종류를 지정 합니다.  
**<RRtype>**  
나열 될 리소스 레코드의 유형을 지정 합니다.  
**<Rrdata>**  
필요한 레코드 데이터의 형식을 지정 합니다.  
**/authority**  
신뢰할 수 있는 데이터를 포함합니다.  
**/glue**  
붙이기 데이터가 포함 됩니다.  
**/additional**  
나열 된 리소스 레코드에 대 한 모든 추가 정보를 포함 합니다.  
**{/node | /child | /startchild <ChildName>}**  
필터링 하거나 리소스 레코드 디스플레이에 정보를 추가 합니다.  
**/node**  
지정 된 노드의 리소스 레코드를 나열합니다.  
**/child**  
지정된 된 하위 도메인의 리소스 레코드를 나열합니다.  
**/startchild <ChildName>**  
위에 있는 목록에서 지정한 자식 도메인을 시작합니다.  
**/continue | /detail**  
반환 된 데이터 표시 방법을 지정 합니다.  
**/continue**  
유형 및 데이터를 사용 하 여 리소스 레코드를 나열합니다.  
**/detail**  
리소스 레코드에 대 한 모든 정보를 나열합니다.  
#### <a name="sample-usage"></a>샘플 사용  
`dnscmd /enumrecords test.contoso.com test /additional`  
### <a name="BKMK_11"></a>dnscmd /enumzones  
지정된 된 DNS 서버에 존재 하는 영역을 나열 합니다.  
#### <a name="syntax"></a>구문  
```  
dnscmd [<ServerName>] /enumzones [/primary | /secondary | /forwarder | /stub | /cache | /auto-created] [/forward | /reverse | /ds | /file] [/domaindirectorypartition | /forestdirectorypartition | /customdirectorypartition | /legacydirectorypartition | /directorypartition <PartitionFQDN>]  
```  
#### <a name="parameters"></a>매개 변수  
**<ServerName>**  
IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다.  
**/primary | /secondary | /forwarder | /stub | /cache | /auto-created**  
표시할 영역의 종류를 필터링 합니다.  
**/primary**  
표준 기본 영역 또는 active directory 통합 영역 중 하나는 모든 영역을 나열 합니다.  
**/secondary**  
모든 표준 보조 영역을 나열합니다.  
**/forwarder**  
확인 되지 않은 다른 DNS 서버 쿼리를 전달 하는 영역을 나열 합니다.  
**/stub**  
모든 스텁 영역을 나열합니다.  
**/cache**  
캐시에 로드 되는 영역을 나열 합니다.  
**/auto-created**  
DNS 서버를 설치할 때 자동으로 생성 된 영역을 나열 합니다.  
**/ | 역방향 / | /ds | /file**  
영역을 표시 유형의 추가 필터를 지정 합니다.  
**/forward**  
정방향 조회 영역을 나열 합니다.  
**/reverse**  
역방향 조회 영역을 나열 합니다.  
**/ds**  
active directory 통합 영역을 나열합니다.  
**/file**  
파일에 의해 백업 되는 영역을 나열 합니다.  
**/domaindirectorypartition**  
도메인 디렉터리 파티션에 저장 된 영역을 나열 합니다.  
**/forestdirectorypartition**  
포리스트의 DNS 응용 프로그램 디렉터리 파티션에 저장 된 영역을 나열 합니다.  
**/customdirectorypartition**  
사용자 정의 응용 프로그램 디렉터리 파티션에 저장 된 모든 영역을 나열 합니다.  
**/legacydirectorypartition**  
도메인 디렉터리 파티션에 저장 된 모든 영역을 나열 합니다.  
**/directorypartition <PartitionFQDN>**  
지정 된 디렉터리 파티션에 저장 된 모든 영역을 나열 합니다.  
#### <a name="remarks"></a>설명  
-   **enumzones** 매개 변수 영역 목록에 대 한 필터로 작동 합니다. 필터가 지정 된 영역의 전체 목록이 반환 됩니다. 필터를 지정 하는 경우 해당 필터 조건을 충족 하는 영역만 영역의 반환된 목록에 포함 됩니다.  
#### <a name="example"></a>예제  
참조 [예제 2: DNS 서버에서 영역의 전체 목록을 표시](https://technet.microsoft.com/library/cc784399(v=ws.10).aspx) 또는 [예제 3: DNS 서버에서 자동 영역 목록을 표시](https://technet.microsoft.com/library/cc784399(v=ws.10).aspx)합니다.  
### <a name="BKMK_25a"></a>dnscmd /exportsettings  
DNS 서버 구성 세부 정보를 나열 하는 텍스트 파일을 만듭니다. 텍스트 파일 DnsSettings.txt 이라고 합니다. 프로그램은 서버의 %systemroot%\system32\dns 디렉터리에 있습니다.  
#### <a name="syntax"></a>구문  
```  
dnscmd [<ServerName>] /exportsettings   
```  
#### <a name="parameters"></a>매개 변수  
**<ServerName>**  
로컬 컴퓨터 구문, IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다.  
#### <a name="remarks"></a>설명  
-   파일에 정보를 사용할 수 있는 **dnscmd /exportsettings** 구성 문제를 해결 하거나 여러 서버를 동일 하 게 구성 되도록 만듭니다.  
### <a name="BKMK_12"></a>dnscmd /info  
지정 된 서버의 레지스트리 DNS 섹션에서 설정을 표시합니다. **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\DNS\Parameters**  
#### <a name="syntax"></a>구문  
```  
dnscmd [<ServerName>] /info [<Setting>]  
```  
#### <a name="parameters"></a>매개 변수  
**<ServerName>**  
IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다.  
**<Setting>**  
값으로 설정 하는 **정보** 명령 반환을 개별적으로 지정할 수 있습니다. 설정을 지정 하지 않으면 일반 설정에 대 한 보고서를 반환 됩니다.  
#### <a name="remarks"></a>설명  
-   이 명령은 DNS 서버 수준에 있는 레지스트리 설정을 표시 합니다. 영역 수준 레지스트리 설정을 표시 하려면 사용 된 [zoneinfo](#BKMK_26) 명령입니다. 이 명령으로 표시 될 수 있는 설정의 목록을 보려면 참조는 [구성](#BKMK_3) 설명 합니다.  
#### <a name="example"></a>예제  
참조 [예제 4: DNS 서버에서 IsSlave 설정을 표시](https://technet.microsoft.com/library/cc784399(v=ws.10).aspx) 또는 [예제 5: DNS 서버에서 Recursiontimeout 설정을 표시](https://technet.microsoft.com/library/cc784399(v=ws.10).aspx)합니다.  
### <a name="BKMK_29a"></a>dnscmd /ipvalidate  
작동 중인 DNS 서버 또는 DNS 서버 역할을 전달자, 루트 힌트 서버 또는 특정 영역에 대 한 마스터 서버 할 수 있는지 여부를 식별 하는 IP 주소 인지 테스트 합니다.  
#### <a name="syntax"></a>구문  
```  
dnscmd [<ServerName>] /ipvalidate <Context> [<ZoneName>] [[<IPaddress>]]  
```  
#### <a name="parameters"></a>매개 변수  
**<ServerName>**  
로컬 컴퓨터 구문, IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다.  
**<Context>**  
수행 하는 테스트의 유형을 지정 합니다. 다음 테스트를 지정할 수 있습니다.  
-   **/dnsservers** 지정 하는 주소와 컴퓨터 DNS 서버가 작동 하는지 테스트 합니다.  
-   **/forwarders** 를 지정 하는 주소 전달자 역할을 수행할 수 있는 DNS 서버를 식별 하는 테스트 합니다.  
-   **/roothints** 테스트를 지정 하는 주소를 루트 힌트 이름 서버로 작동할 수 있는 DNS 서버를 식별 합니다.  
-   **/zonemasters** 를 지정 하는 주소에 대 한 마스터 서버는 DNS 서버를 식별 하는 테스트 *ZoneName*합니다.  
**<ZoneName>**  
영역을 식별합니다. 이 매개 변수를 사용 하는 **/zonemasters** 매개 변수입니다.  
**<IPaddress>**  
이 명령은 테스트 하는 IP 주소를 지정 합니다.  
#### <a name="sample-usage"></a>샘플 사용  
<pre>dnscmd dnssvr1.contoso.com /ipvalidate /dnsservers 10.0.0.1 10.0.0.2  
dnscmd dnssvr1.contoso.com /ipvalidate /zonemasters corp.contoso.com 10.0.0.2</pre>  
### <a name="BKMK_13"></a>dnscmd /nodedelete  
지정된 된 호스트에 대 한 모든 레코드를 삭제합니다. # # # 구문을 ```  
dnscmd [<ServerName>] /nodedelete <ZoneName> <NodeName> [/tree] [/f] ```  
#### Parameters  
**<ServerName>**  
IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다.  
**<ZoneName>**  
영역 이름을 지정합니다.  
**<NodeName>**  
삭제할 노드의 호스트 이름을 지정 합니다.  
**/tree**  
모든 자식 레코드를 삭제합니다.  
**/f**  
확인을 요청 하지 않고 명령을 실행 합니다. # # # 예제에서는 참조 [예 6: 노드에서 레코드가 삭제](https://technet.microsoft.com/library/cc784399(v=ws.10).aspx)합니다.  
### <a name="BKMK_14"></a>dnscmd /recordadd  
DNS 서버에서 지정된 된 된 시간대에 레코드를 추가합니다. # # # 구문을 ```  
dnscmd [<ServerName>] /recordadd <ZoneName> <NodeName> <RRtype> <Rrdata> ```  
#### Parameters  
**<ServerName>**  
로컬 컴퓨터 구문, IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다.  
**<ZoneName>**  
레코드는 영역을 지정 합니다.  
**<NodeName>**  
영역에서 특정 노드를 지정합니다.  
**<RRtype>**  
추가할 레코드 종류를 지정 합니다.  
**<Rrdata>**  
예상 되는 데이터의 형식을 지정 합니다.  
> [!NOTE]  
레코드를 추가 하는 경우 올바른 데이터 형식 및 데이터 형식을 사용 해야 합니다. 리소스 레코드 종류 및 적절 한 데이터 형식 목록은 참조 하세요 [리소스 레코드 참조](https://technet.microsoft.com/library/cc758321(v=ws.10).aspx)합니다. # # # 샘플 사용
<pre>dnscmd dnssvr1.contoso.com /recordadd test A 10.0.0.5  
dnscmd /recordadd test.contoso.com test MX 10 mailserver.test.contoso.com</pre>  
### <a name="BKMK_15"></a>dnscmd /recorddelete  
지정된 된 된 시간대에서 리소스 레코드를 삭제합니다. # # # 구문을 ```  
dnscmd <ServerName> /recorddelete <ZoneName> <NodeName> <RRtype> <Rrdata>[/f] ```  
#### Parameters  
**<ServerName>**  
> IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다.  
**<ZoneName>**  
리소스 레코드는 영역을 지정 합니다.  
**<NodeName>**  
호스트의 이름을 지정합니다.  
**<RRtype>**  
삭제할 리소스 레코드 종류를 지정 합니다.  
**<Rrdata>**  
예상 되는 데이터의 형식을 지정 합니다.  
**/f**  
확인을 요청 하지 않고 명령을 실행:-노드는 둘 이상의 리소스 레코드를 가질 수 있으므로이 명령은 해야 삭제할 리소스 레코드 유형에 대 한 매우 구체적 이어야 합니다. -리소스 레코드 데이터의 형식을 지정 하지 않으면 데이터 형식을 지정 하 고 지정 된 노드는 특정 데이터 형식 가진 모든 레코드가 삭제 됩니다. # # # 샘플 사용 `dnscmd /recorddelete test.contoso.com test MX 10 mailserver.test.contoso.com`  
### <a name="BKMK_16"></a>dnscmd /resetforwarders  
DNS 서버 전달 하 DNS 쿼리에 로컬에서 확인할 수 없습니다. 해당 하는 경우 IP 주소를 다시 설정 하거나 선택 합니다. # # # 구문을 ```  
dnscmd [<ServerName>] /resetforwarders [<IPaddress> [,<IPaddress>]...] [/ timeout <timeOut>] [슬레이브 / | / noslave] ```  
#### Parameters  
**<ServerName>**  
IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다.  
**<IPaddress>**  
DNS 서버는 확인 되지 않은 쿼리를 전달 하는 IP 주소를 나열 합니다.  
**/timeout <timeOut>**  
DNS 서버 전달자에서 응답을 기다리는 시간 (초) 수를 설정 합니다. 기본적으로이 값은 5 초입니다.  
**/slave|/noslave**  
DNS 서버 전달자 쿼리를 해결 하지 못하는 경우 자체 반복 쿼리를 수행 하는지 여부를 결정 합니다.  
**/slave**  
DNS 서버를 전달자 쿼리를 해결 하지 못하는 경우 자체 반복 쿼리를 수행할 수 없습니다.  
**/noslave**  
DNS 서버가 전달자 쿼리를 해결 하지 못하는 경우 자체 반복 쿼리를 수행할 수 있습니다. 이 값은 기본 설정입니다. # # # 주의-기본적으로 DNS 서버 수행 반복 쿼리는 쿼리를 확인할 수 없는 경우. -를 사용 하 여 IP 주소를 설정 합니다.는 **resetforwarders** 명령을 사용 하면 DNS 서버를 지정 된 IP 주소에 있는 DNS 서버에 재귀 쿼리를 수행 합니다. 전달자는 쿼리를 해결 하지 않을 경우 DNS 서버 자체 반복 쿼리를 수행할 수 있습니다. -경우 합니다 **슬레이브/** 매개 변수는 사용, DNS 서버 자체 반복 쿼리를 수행 하지 않습니다. 즉, DNS 서버 목록에서 DNS 서버에만 확인할 수 없는 쿼리를 전달 하 고 전달자에서 해결 되지 않으면 반복 쿼리를 시도 하지 않습니다. 전달자 DNS 서버에 대 한 IP 주소를 설정 하는 더 효율적입니다. 사용할 수는 **resetforwarders** 의 해결 되지 않은 쿼리는 외부에 연결 하는 DNS 서버를 전달 하는 네트워크의 내부 서버에 대 한 도움말입니다. -DNS 서버를 두 번 해당 서버에 전달 하려고 하면 전달자의의 IP 주소를 두 번 나열 합니다. # # # 샘플 사용
<pre>dnscmd dnssvr1.contoso.com /resetforwarders 10.0.0.1 /timeout 7 /slave  
dnscmd dnssvr1.contoso.com /resetforwarders /noslave</pre>  
### <a name="BKMK_17"></a>dnscmd /resetlistenaddresses  
DNS 클라이언트 요청을 수신 하는 서버의 IP 주소를 지정 합니다. # # # 구문을 ```  
dnscmd [<ServerName>] /resetlistenaddresses [<listenaddress>] ```  
#### Parameters  
**<ServerName>**  
IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다.  
**<listenaddress>**  
DNS 클라이언트 요청을 수신 하는 DNS 서버의 IP 주소를 지정 합니다. 없는 수신 주소를 지정 하는 경우 모든 IP 주소가 서버에서 클라이언트 요청을 기다리고 있습니다. # # # 주의-기본적으로 모든 IP 주소는 DNS 서버에서 클라이언트 요청을 수신 DNS입니다. # # # 샘플 사용 `dnscmd dnssvr1.contoso.com /resetlistenaddresses 10.0.0.1`  
### <a name="BKMK_18"></a>dnscmd /startscavenging  
지정 된 DNS 서버에서 부실 리소스 레코드에 대 한 즉시 검색을 시도 하도록 DNS 서버를 알려 줍니다. # # # 구문을 ```  
dnscmd [<ServerName>] /startscavenging ```  
#### Parameter  
**<ServerName>**  
IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다. # # # 주의-이 명령을 성공적으로 완료 한 청소를 즉시 시작 합니다. -의 다음 전제 조건이 충족 하지 않는 한는 청소 성공적으로 완료 하는 청소를 시작 하는 명령을 표시 하지만 시작 하지 않습니다:-서버와 영역에 대 한 청소 사용 하도록 설정 합니다. -영역이 시작 됩니다. -리소스 레코드는 타임 스탬프입니다. -서버에 대 한 청소를 사용 하는 방법에 대 한 정보를 참조 하세요. 합니다 **scavenginginterval** 에서 서버 수준 구문에서 매개 변수를 [config](#BKMK_3) 섹션. -영역에 대 한 청소를 사용 하는 방법에 대 한 내용은 참조는 **에이징** 영역 수준 구문에서 매개 변수를 [구성](#BKMK_3) 섹션. -일시 중지 하는 영역을 시작 하는 방법에 대 한 내용은 참조는 [zoneresume](#BKMK_35) 섹션입니다. -타임 스탬프에 대 한 리소스 레코드를 확인 하는 방법에 대 한 내용은 참조는 [ageallrecords](#BKMK_1) 섹션입니다. -청소 실패 하면 경고 메시지가 나타납니다. # # # 샘플 사용 `dnscmd dnssvr1.contoso.com /startscavenging`  
### <a name="BKMK_19"></a>dnscmd /statistics  
표시 하거나 지정 된 DNS 서버에 대 한 데이터를 지웁니다. # # # 구문을 ```  
dnscmd [<ServerName>] /statistics [<StatID>] [/ 지우기] ```  
#### Parameters  
**<ServerName>**  
IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다.  
**<StatID>**  
통계 또는 표시 하는 통계의 조합을 지정 합니다. Id 번호는 통계를 식별 하는 데 사용 됩니다. 없는 통계 ID 번호를 지정 하면 모든 통계가 표시 됩니다.  
다음은 지정할 수 있는 숫자와 해당 통계를 표시 하는 목록입니다.  
**00000001**  
time  
**00000002**  
쿼리  
**00000004**  
query2  
**00000008**  
Recurse  
**00000010**  
마스터  
**00000020**  
보조  
**00000040**  
WINS  
**00000100**  
Update  
**00000200**  
SkwanSec  
**00000400**  
ds  
**00010000**  
메모리  
**00100000**  
PacketMem  
**00040000**  
Dbase  
**00080000**  
레코드  
**00200000**  
NbstatMem  
**/clear**  
지정한 통계 카운터를 0으로 다시 설정 합니다. # # # 주의-는 **통계** 명령은 시작 되거나 다시 시작 될 때 DNS 서버에서 시작 하는 카운터를 표시 합니다. # # # 예제를 보려면 [예 7: DNS 서버에 대 한 시간 통계가 표시](https://technet.microsoft.com/library/cc784399(v=ws.10).aspx) 또는 [예 8: DNS 서버에 대 한 NbstatMem 통계 표시](https://technet.microsoft.com/library/cc784399(v=ws.10).aspx)합니다.  
### <a name="BKMK_20"></a>dnscmd /unenlistdirectorypartition  
지정 된 디렉터리 파티션의 복제 세트에서 DNS 서버를 제거합니다. # # # 구문을 ```  
dnscmd [<ServerName>] /unenlistdirectorypartition <PartitionFQDN> ```  
#### Parameters  
**<ServerName>**  
IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다.  
**<PartitionFQDN>**  
DNS 응용 프로그램 디렉터리 파티션 제거 될의 FQDN입니다.  
### <a name="BKMK_21"></a>dnscmd /writebackfiles  
변경 내용에 대 한 DNS 서버 메모리를 확인 하 고 영구 저장소에 씁니다. # # # 구문을 ```  
dnscmd [<ServerName>] /writebackfiles [<ZoneName>] ```  
#### Parameters  
**<ServerName>**  
IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다.  
**<ZoneName>**  
업데이트할 영역의 이름을 지정 합니다. # # # 주의-는 **writebackfiles** 명령은 모든 커밋되지 않은 데이터 영역 또는 지정된 된 된 시간대를 업데이트 합니다. 내용이 메모리에서에 있는 영구 저장소에 아직 기록 되지 않은 경우 영역 비정상적입니다. 모든 영역을 확인 하는 서버 수준 작업입니다. 이 작업에 한 영역을 지정 하거나 사용할 수는 [zonewriteback](#BKMK_37) 작업 합니다. # # # 샘플 사용 `dnscmd dnssvr1.contoso.com /writebackfiles`  
### <a name="BKMK_22"></a>dnscmd /zoneadd  
DNS 서버에 영역을 추가 합니다. # # # 구문을 ```  
dnscmd [<ServerName>] /zoneadd <ZoneName> <Zonetype> [/dp <FQDN>| {/ 도메인 | / enterprise | 레거시 /}] ```  
#### Parameters  
**<ServerName>**  
IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다.  
**<ZoneName>**  
영역 이름을 지정합니다.  
**<Zonetype>**  
만들 영역 유형을 지정 합니다. 각 영역 형식에 다른 필수 매개 변수:  
**/dsprimary**  
active directory 통합된 영역을 만듭니다.  
* * / 기본 /file <FileName>**  
표준 기본 영역을 만들고 영역 정보를 저장 하는 파일의 이름을 지정 합니다.  
**/secondary <MasterIPaddress> [<MasterIPaddress>...]**  
표준 보조 영역을 만듭니다.  
**/stub <MasterIPaddress> [<MasterIPaddress>...] /file <FileName>**  
스텁 파일 지원 영역을 만듭니다.  
**/dsstub <MasterIPaddress> [<MasterIPaddress>...]**  
active directory 통합된 스텁 영역을 만듭니다.  
* * / 전달자 <MasterIPaddress> [<MasterIPaddress>]... / 파일 <FileName>**  
만든된 영역 전달 해결 되지 않은 다른 DNS 서버 쿼리를 지정 합니다.  
**/dsforwarder**  
만든된 active directory 통합된 영역에 확인 되지 않은 다른 DNS 서버 쿼리를 전달를 지정 합니다.  
**/dp <FQDN> {/domain | /enterprise | /legacy}**  
영역을 저장 하는 디렉터리 파티션을 지정 합니다.  
**<FQDN>**  
디렉터리 파티션의 FQDN을 지정합니다.  
**/domain**  
도메인 디렉터리 파티션에 영역을 저장합니다.  
**/enterprise**  
엔터프라이즈 디렉터리 파티션에서 영역을 저장합니다.  
**/legacy**  
레거시 디렉터리 파티션에서 영역을 저장합니다. # # # 주의-의 영역 형식 지정 **/forwarder** 하거나 **/dsforwarder** 조건부 전달을 수행 하는 영역을 만듭니다. # # # 샘플 사용
<pre>dnscmd dnssvr1.contoso.com /zoneadd test.contoso.com /dsprimary  
dnscmd dnssvr1.contoso.com /zoneadd secondtest.contoso.com /secondary 10.0.0.2</pre>  
### <a name="BKMK_23"></a>dnscmd /zonechangedirectorypartition  
지정된 된 된 영역 상주 하는 디렉터리 파티션을 변경 합니다. #### Syntax ```  
dnscmd [<ServerName>] /zonechangedirectorypartition <ZoneName>] {[<NewPartitionName>] | [<Zonetype>] } ```  
#### Parameters  
**<ServerName>**  
IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다.  
**<ZoneName>**  
영역 상주 하는 현재 디렉터리 파티션의 FQDN입니다.  
**<NewPartitionName>**  
영역으로 이동 됩니다 디렉터리 파티션의 FQDN입니다.  
**<Zonetype>**  
영역으로 이동 됩니다 디렉터리 파티션의 형식을 지정 합니다.  
**/domain**  
기본 제공 도메인 디렉터리 파티션에으로 영역을 이동 합니다.  
**/forest**  
기본 제공 포리스트 디렉터리 파티션에으로 영역을 이동 합니다.  
**/legacy**  
이전 active directory 도메인 컨트롤러에 대해 만들어진 디렉터리 파티션에 영역을 이동 합니다. 이 디렉터리 파티션을 기본 모드에 대 한 필요 하지 않습니다.  
### <a name="BKMK_24"></a>dnscmd /zonedelete  
지정된 된 된 시간대를 삭제합니다. # # # 구문을 ```  
dnscmd [<ServerName>] /zonedelete <ZoneName> [/dsdel] [/f] ```  
#### Parameters  
**<ServerName>**  
IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다.  
**<ZoneName>**  
삭제할 영역의 이름을 지정 합니다.  
**/dsdel**  
AD DS에서 영역을 삭제합니다.  
**/f**  
확인을 요청 하지 않고 명령을 실행 합니다. # # # 예제에서는 참조 [예제 9: DNS 서버에서 영역을 삭제](https://technet.microsoft.com/library/cc784399(v=ws.10).aspx)합니다.  
### <a name="BKMK_25"></a>dnscmd /zoneexport  
지정 된 영역의 리소스 레코드를 나열 하는 텍스트 파일을 만듭니다. #### Syntax `dnscmd [<ServerName>] /zoneexport <ZoneName> <ZoneExportFile>` #### Parameters **<ServerName>**  
로컬 컴퓨터 구문, IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다.  
**<ZoneName>**  
영역 이름을 지정합니다.  
**<ZoneExportFile>**  
만들려는 파일의 이름을 지정 합니다. # # # 주의-는 **zoneexport** 작업 문제 해결을 위해는 active directory 통합된 영역에 대 한 리소스 레코드의 파일을 만듭니다. 기본적으로이 명령은 파일 %systemroot%/System32/Dns 디렉터리는 기본적으로는 DNS 디렉터리에 배치 됩니다. # # # 예제에서는 참조 [예제 10: 영역 리소스 레코드 목록 파일로 내보내려면](https://technet.microsoft.com/library/cc784399(v=ws.10).aspx)합니다.  
### <a name="BKMK_26"></a>dnscmd /zoneinfo  
지정 된 영역의 레지스트리에의 섹션에서 설정을 표시: * * HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\DNS\Parameters\Zones\\<ZoneName>* * # # # 구문을 ```  
dnscmd [<ServerName>] /zoneinfo <ZoneName> [<Setting>] ```  
#### Parameters  
**<ServerName>**  
IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다.  
**<ZoneName>**  
영역 이름을 지정합니다.  
**<Setting>**  
설정 하는 개별적으로 지정할 수 있습니다 합니다 **zoneinfo** 명령이 반환 합니다. 설정을 지정 하지 않으면 모든 설정이 반환 됩니다. # # # 주의-는 **zoneinfo** 명령은 표시에 포함 된 DNS 영역 수준 레지스트리 설정 * * HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\DNS\Parameters\Zones\\<ZoneName>* * 합니다. -표시 하려면 서버 수준 레지스트리 설정을 사용 하십시오는 [정보](#BKMK_12) 명령입니다. -이 명령을 사용 하 여 표시할 수 있는 설정 목록을 참조 하십시오는 [config](#BKMK_3) 명령입니다. # # # 예제에서는 참조 [예제 11: 디스플레이 RefreshInterval 설정을 레지스트리에서](https://technet.microsoft.com/library/cc784399(v=ws.10).aspx) 또는 [예제 12: 디스플레이 에이징 설정을 레지스트리에서](https://technet.microsoft.com/library/cc784399(v=ws.10).aspx)합니다.  
### <a name="BKMK_27"></a>dnscmd /zonepause  
다음 쿼리 요청을 무시 하는 지정된 된 영역을 일시 중지 합니다. # # # 구문을 ```  
dnscmd [<ServerName>] /zonepause <ZoneName> ```  
#### Parameters  
**<ServerName>**  
IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다.  
**<ZoneName>**  
일시 중지 하려면 영역의 이름을 지정 합니다. # # # 주의-영역을 다시 시작, 일시 중지 된 후 사용할 수 있도록를 사용 하는 [zoneresume](#BKMK_35) 명령입니다. # # # 샘플 사용 `dnscmd dnssvr1.contoso.com /zonepause test.contoso.com`  
### <a name="BKMK_28"></a>dnscmd /zoneprint  
영역에 레코드를 나열합니다. # # # 구문을 ```  
dnscmd [<ServerName>] /zoneprint <ZoneName> ```  
#### Parameters  
**<ServerName>**  
로컬 컴퓨터 구문, IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다.  
**<ZoneName>**  
나열 될 영역을 식별 합니다.  
### <a name="BKMK_30"></a>dnscmd /zonerefresh  
마스터 영역에서 업데이트를 보조 DNS 영역을 강제로 수행 합니다. # # # 구문을 ```  
dnscmd <ServerName> /zonerefresh <ZoneName> ```  
#### Parameters  
**<ServerName>**  
IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다.  
**<ZoneName>**  
새로 고칠 영역의 이름을 지정 합니다. # # # 주의-는 **zonerefresh** 명령에는 마스터 서버 s 시작 (soa) 리소스 레코드의 버전 번호의 확인을 강제로 수행 합니다. 마스터 서버에 버전 번호는 보조 서버의 버전 번호 보다 높은 경우 보조 서버를 업데이트 하는 영역 전송이 시작 됩니다. 버전 번호가 동일한 경우 영역 전송이 수행 되지 발생 합니다. 기본적으로 15 분 마다 발생 하는 강제-확인 합니다. 기본값을 변경 하려면 사용 된 **dnscmd config refreshinterval** 명령입니다. # # # 샘플 사용 `dnscmd dnssvr1.contoso.com /zonerefresh test.contoso.com`  
### <a name="BKMK_31"></a>dnscmd /zonereload  
복사본에 정보 소스에서 영역입니다. # # # 구문을 ```  
dnscmd <ServerName> /zonereload <ZoneName> ```  
#### Parameters  
**<ServerName>**  
IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다.  
**<ZoneName>**  
영역 다시 로드 될 이름을 지정 합니다. # # # 주의-이면 영역 active directory 통합을 다시 로드 AD DS에서. -이면 영역 표준 파일 지원 영역을 다시 로드 하는 파일에서 합니다. # # # 샘플 사용 `dnscmd dnssvr1.contoso.com /zonereload test.contoso.com`  
### <a name="BKMK_32"></a>dnscmd /zoneresetmasters  
보조 영역에 영역 전송 정보를 제공 하 고 마스터 서버의 IP 주소를 다시 설정 합니다. # # # 구문을 ```  
dnscmd <ServerName> /zoneresetmasters <ZoneName> [/ 로컬] [<IPaddress> [<IPaddress>]...] ```  
#### Parameters  
**<ServerName>**  
IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다.  
**<ZoneName>**  
영역 다시 로드 될 이름을 지정 합니다.  
**/local**  
로컬 마스터 목록을 설정합니다. 이 매개 변수는 active directory 통합 영역에 사용 됩니다.  
**<IPaddress>**  
보조 영역 마스터 서버의 IP 주소. # # # 주의-이 값은 원래 보조 영역을 만들 때 설정 되었습니다. 사용 된 **zoneresetmasters** 보조 서버에서 명령입니다. 마스터 DNS 서버에 설정 된 경우에이 값 효과가 없습니다. # # # 샘플 사용
<pre>dnscmd dnssvr1.contoso.com /zoneresetmasters test.contoso.com 10.0.0.1  
dnscmd dnssvr1.contoso.com /zoneresetmasters test.contoso.com /local</pre>  
### <a name="BKMK_33"></a>dnscmd /zoneresetscavengeservers  
지정된 된 된 영역 청소할 하는 서버의 IP 주소를 변경 합니다. # # # 구문을 ```  
dnscmd [<ServerName>] /zoneresetscavengeservers <ZoneName> [<IPaddress> [<IPaddress>]...] ```  
#### Parameters  
**<ServerName>**  
로컬 컴퓨터 구문, IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다.  
**<ZoneName>**  
청소 하는 영역을 식별 합니다.  
**<IPaddress>**  
청소를 수행할 수 있는 서버의 IP 주소를 나열 합니다. 이 매개 변수를 생략 하면이 영역을 호스팅하는 모든 서버 청소할 것입니다. # # # 주의-기본적으로 영역을 호스트 하는 모든 서버에는 해당 영역 청소 수 있습니다. -영역 둘 이상의 DNS 서버에서 호스팅되면 있으면 영역 청소 하는 횟수를 줄이기 위해이 명령을 사용할 수 있습니다. -청소 하는 DNS 서버와이 명령으로 영향을 받는 영역에서 사용할 수 있어야 합니다. # # # 샘플 사용 `dnscmd dnssvr1.contoso.com /zoneresetscavengeservers test.contoso.com 10.0.0.1 10.0.0.2`  
### <a name="BKMK_34"></a>dnscmd /zoneresetsecondaries  
응답 하는 마스터 서버 영역 전송 물으면 보조 서버의 IP 주소 목록을 지정 합니다. # # # 구문을 ```  
dnscmd [<ServerName>] /zoneresetsecondaries <ZoneName> {/ noxfr | 보안 되지 않은 / | /securens | /securelist <SecurityIPaddresses>} {/ nonotify | 알림 / | 알림 <NotifyIPaddresses>} ```  
#### Parameters  
**<ServerName>**  
IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 하는 경우는 매개 변수가 생략 된, 로컬 서버를 사용 합니다.  
**<ZoneName>**  
해당 보조 서버에 있는 영역의 이름을 지정 다시 설정 합니다.  
**/noxfr | /nonsecure | /securens | /securelist <SecurityIPaddresses>**  
전체 또는 일부 업데이트를 요청 하는 보조 서버 가져오기 업데이트 여부를 지정 합니다.  
**/noxfr**  
없는 영역 전송 수를 지정 합니다.  
**/nonsecure**  
모든 영역 전송 요청에 권한이 부여 되어 있는지를 지정 합니다.  
**/securens**  
영역에 대 한 이름 서버 (NS) 리소스 레코드에 나열 된 서버 에서만 전송을 부여 되어 있음을 지정 합니다.  
**/securelist**  
영역 전송 서버의 목록에만 부여 되어 있는지를 지정 합니다. IP 주소 또는 주소 마스터 서버를 사용 하 여이 매개 변수를 따라야 합니다.  
**<SecurityIPaddresses>**  
마스터 서버에서 영역 전송의 받을 IP 주소를 나열 합니다. 이 매개 변수 에서만 사용 되는 **/securelist** 매개 변수입니다.  
**/nonotify | /notify | /notifylist <NotifyIPaddresses>**  
특정 보조 서버에만 변경 알림의 보냈음을 지정 합니다.  
**/nonotify**  
보조 서버로 변경 알림이 전송 되지 않습니다는 지정 합니다.  
**/notify**  
모든 보조 서버에 변경 알림의 보냈음을 지정 합니다.  
**/notifylist**  
서버 목록을 변경 알림이 전송 되는 것을 지정 합니다. 이 명령은 IP 주소 또는 주소 마스터 서버를 사용 하 여 따라야 합니다.  
**<NotifyIPaddresses>**  
IP 주소 또는 보조 서버 또는 서버 변경 알림이 전송 되는 주소를 지정 합니다. 에이 목록을 사용 하 여 **알림** 매개 변수입니다. # # # 주의-사용 된 **zoneresetsecondaries** 보조 서버에서 영역 전송 요청에 응답 하는 방법을 지정 하려면 마스터 서버에서 명령입니다. # # # 샘플 사용
<pre>dnscmd dnssvr1.contoso.com /zoneresetsecondaries test.contoso.com /noxfr /nonotify  
dnscmd dnssvr1.contoso.com /zoneresetsecondaries test.contoso.com /securelist 11.0.0.2</pre>  
### <a name="BKMK_29"></a>dnscmd /zoneresettype  
영역 종류를 변경합니다. # # # 구문을 ```  
dnscmd [<ServerName>] /zoneresettype <ZoneName> <Zonetype> [/ overwrite_mem | /overwrite_ds] ```  
#### Parameters  
**<ServerName>**  
로컬 컴퓨터 구문, IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다.  
**<ZoneName>**  
유형을 변경할 수는 영역을 식별 합니다.  
**<Zonetype>**  
만들 영역 유형을 지정 합니다. 각 형식에 다른 필수 매개 변수:  
**/dsprimary**  
active directory 통합된 영역을 만듭니다.  
* * / 기본 /file <FileName>**  
기본 표준 시간대를 만듭니다.  
**/secondary <MasterIPaddress> [,<MasterIPaddress>...]**  
표준 보조 영역을 만듭니다.  
**/stub <MasterIPaddress>[,<MasterIPaddress>...] /file <FileName>**  
스텁 파일 지원 영역을 만듭니다.  
**/dsstub <MasterIPaddress>[,<MasterIPaddress>...]**  
active directory 통합된 스텁 영역을 만듭니다.  
* * / 전달자 <MasterIPaddress[,<MasterIPaddress>]... / 파일<FileName>**  
만든된 영역 전달 해결 되지 않은 다른 DNS 서버 쿼리를 지정 합니다.  
**/dsforwarder**  
만든된 active directory 통합된 영역에 확인 되지 않은 다른 DNS 서버 쿼리를 전달를 지정 합니다.  
**/overwrite_mem | /overwrite_ds**  
기존 데이터 덮어쓰기 하는 방법을 지정 합니다.  
**/overwrite_mem**  
AD DS의 데이터에서 DNS 데이터를 덮어씁니다.  
**/overwrite_ds**  
AD DS에 기존 데이터를 덮어씁니다. # # # 주의-영역 설정으로 입력 **/dsforwarder** 조건부 전달을 수행 하는 영역을 만듭니다. # # # 샘플 사용
<pre>dnscmd dnssvr1.contoso.com /zoneresettype test.contoso.com /primary /file test.contoso.com.dns  
dnscmd dnssvr1.contoso.com /zoneresettype second.contoso.com /secondary 10.0.0.2</pre>  
### <a name="BKMK_35"></a>dnscmd /zoneresume  
이전에 일시 중지 된 지정된 된 된 시간대를 시작 합니다. # # # 구문을 ```  
dnscmd <ServerName> /zoneresume <ZoneName> ```  
#### Parameters  
**<ServerName>**  
IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다.  
**<ZoneName>**  
다시 시작 하려면 영역의 이름을 지정 합니다. # # #이 작업을 사용 하 여 역방향 주의-는 [zonepause](#BKMK_27) 작업 합니다. # # # 샘플 사용 `dnscmd dnssvr1.contoso.com /zoneresume test.contoso.com`  
### <a name="BKMK_36"></a>dnscmd /zoneupdatefromds  
AD DS에서 지정 된 active directory 통합된 영역을 업데이트합니다. # # # 구문을 ```  
dnscmd <ServerName> /zoneupdatefromds <ZoneName> ```  
#### Parameters  
**<ServerName>**  
IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다.  
**<ZoneName>**  
업데이트 하려면 영역의 이름을 지정 합니다. # # # 주의-active directory 통합된 영역이이 업데이트 기본적으로 5 분 마다 수행 합니다. 이 매개 변수를 변경 하려면 사용 된 **dnscmd config dspollinginterval** 명령입니다. # # # 샘플 사용 `dnscmd dnssvr1.contoso.com /zoneupdatefromds`  
### <a name="BKMK_37"></a>dnscmd /zonewriteback  
지정된 된 시간대에 관련 된 변경 내용에 대 한 DNS 서버 메모리를 확인 하 고 영구 저장소에 씁니다. # # # 구문을 ```  
dnscmd <ServerName> /zonewriteback <ZoneName> ```  
#### Parameters  
**<ServerName>**  
IP 주소, FQDN 또는 호스트 이름으로 표시를 관리 하려면 DNS 서버를 지정 합니다. 이 매개 변수를 생략 하면 로컬 서버에 사용 됩니다.  
**<ZoneName>**  
업데이트 하려면 영역의 이름을 지정 합니다. # # # 주의-영역 수준 작업입니다. 모든 영역에서 사용 하 여 DNS 서버를 업데이트할 수는 [writebackfiles](#BKMK_21) 작업 합니다. # # # 샘플 사용 `dnscmd dnssvr1.contoso.com /zonewriteback test.contoso.com`  
