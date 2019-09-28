---
title: nfsadmin
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7375b2cf-c6b8-45b5-abf6-6c10e462defd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2658cf610e4328d382b9224f4230d68a022d1cc3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71373225"
---
# <a name="nfsadmin"></a>nfsadmin

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

사용할 수 있습니다 **nfsadmin** NFS 용 서버와 NFS 용 클라이언트 서버를 관리 합니다.  
  
## <a name="syntax"></a>구문  
**nfsadmin server** `[`*computerName*`] [` @ no__t-4u *UserName*`[` @ no__t-7p *Password*`]]` 0l  
  
**nfsadmin server** `[`*computerName*`] [` @ no__t-4u *UserName* `[` @ no__t-7p *Password*`]]` 0r 1*client* 3 all @ no__t-14  
  
**nfsadmin server** `[`*computerName*`] [` @ no__t-4u *UserName* `[` @ no__t-7p *Password*`]] {`start 0 stop @ no__t-11  
  
**nfsadmin server** `[`*computerName*`] [` @ no__t-4u *UserName* `[` @ no__t-7p *Password*`]]` config *Option*1  
  
**nfsadmin server** `[`*computerName*`] [` @ no__t-4u *UserName* `[` @ no__t-7p *Password*`]]` creategroup *Name*  
  
**nfsadmin server** `[`*computerName*`] [` @ no__t-4u *UserName* `[` @ no__t-7p *Password*`]]` listgroups  
  
**nfsadmin server** `[`*computerName*`] [` @ no__t-4u *UserName* `[` @ no__t-7p *Password*`]]` 주로 *Name*  
  
**nfsadmin server** `[`*computerName*`] [` @ no__t-4u *UserName* `[` @ no__t-7p *Password*`]]` renamegroup *OldName NewName*  
  
**nfsadmin server** `[`*computerName*`] [` @ no__t-4u *UserName* `[` @ no__t-7p *Password*`]]` addmembers *Name Host*1  
  
**nfsadmin server** `[`*computerName*`] [` @ no__t-4u *UserName* `[` @ no__t-7p *Password*`]]` listmembers  
  
**nfsadmin server** `[`*computerName*`] [` @ no__t-4u *UserName* `[` @ no__t-7p *Password*`]]` deletemembers *Group Host*1  
  
**nfsadmin client** `[`*computerName*`] [` @ no__t-4u *UserName* `[` @ no__t-7p *Password*`]] {`start 0 stop @ no__t-11  
  
**nfsadmin client** `[`*computerName*`] [` @ no__t-4u *UserName* `[` @ no__t-7p *Password*`]]` config *Option*1  
  
## <a name="description"></a>설명  
**nfsadmin** 명령\-명령줄 유틸리티는 NFS 또는 NFS 용 클라이언트에 대 한 네트워크 파일 시스템에 대 한 Microsoft 서비스를 실행 하는 로컬 또는 원격 컴퓨터에서 서버를 관리 \(NFS\)합니다. 필요한 권한이 없는 계정으로 로그온 하는 경우에 사용자 이름 및 수행 하는 계정의 암호를 지정할 수 있습니다. 수행한 동작 **nfsadmin** 제공한 명령 인수에 따라 달라 집니다.  
  
서비스 뿐 아니라\-특정 명령 인수 및 옵션을 **nfsadmin** 다음 허용 합니다.  
  
*컴퓨터*  
관리 하려는 원격 컴퓨터를 지정 합니다. Windows 인터넷 이름 서비스를 사용 하 여 컴퓨터를 지정할 수 있습니다 \(WINS\) 이름 또는 도메인 이름 시스템 \(DNS\) 이름 또는 인터넷 프로토콜을 통해 \(IP\) 주소입니다.  
  
**\-u** *사용자 이름*  
자격 증명에 사용 하려는 사용자의 사용자 이름을 지정 합니다. 양식에서 사용자 이름에 도메인 이름을 추가 하려면 할 수 있습니다 <em>도메인</em> **\\** <em>사용자 이름</em>  
  
**\- p** *암호*  
사용 하 여 지정 된 사용자의 암호를 지정 된 **\-u** 옵션입니다. 지정 하는 경우는 **\-u** 옵션은 있 생략 된 **\-p** 옵션을 사용자의 암호를 묻는 메시지가 나타납니다.  
  
#### <a name="administering-server-for-nfs"></a>NFS 용 서버 관리  
사용 된 **nfsadmin server** NFS 용 서버를 관리 하는 명령입니다. 특정 작업 하는 **nfsadmin server** 는 명령 옵션 또는 인수에 지정 된 수에 따라 달라 집니다.  
  
**\-l**  
클라이언트에서 보유 한 모든 잠금을 나열 합니다.  
  
**\-r** {*client* | **all**}  
지정한 잠금을 해제 한 *클라이언트* 또는 **모든** 모든 클라이언트에 의해 지정 됩니다.  
  
**start**  
NFS 용 서버 서비스를 시작 합니다.  
  
**stop**  
NFS 용 서버를 중지합니다.  
  
**config**  
NFS 용 서버에 대 한 일반 설정을 지정합니다. 하나 이상의 다음 옵션을 제공 해야는 **config** 인수:  
  
**mapsvr\=** <em>서버</em>  
집합 *서버* NFS 용 서버에 대 한 사용자 이름 매핑 서버입니다. 이 옵션을 이전 버전과 호환성에 대 한 지원 계속 있지만 사용 해야는 **sfuadmin** 유틸리티 대신 합니다.  
  
**auditlocation\=** {**eventlog** | **파일** | **모두** | **none**}  
이벤트는 감사 여부 및 이벤트를 기록할지를 지정 합니다. 다음 인수 중 하나가 필요 합니다.  
  
**eventlog**  
이벤트 뷰어 응용 프로그램 로그만 감사 된 이벤트를 기록할지를 지정 합니다.  
  
**file**  
로 지정 된 파일에 감사 된 이벤트를 기록할지 지정 **config fname**합니다.  
  
**양방향**  
지정 된 파일이 비롯 하 여 이벤트 뷰어 응용 프로그램 로그에 감사 된 이벤트를 기록할지 지정 **config fname**합니다.  
  
**none**  
이벤트를 감사 되지 않습니다 지정 합니다.  
  
**fname\=** <em>파일</em>  
지정 된 파일을 설정 *파일* 감사 파일입니다. 기본값은 %sfudir%\\로그\\nfssvr.log  
  
**fsize\=** \=*크기*  
집합 *크기* 메가바이트 감사 파일의 최대 크기입니다. 기본 최대 크기는 7 MB입니다.  
  
**audit @ no__t-1**\[ **\+** | **\-** \]**탑재** \=0**2**3**5**6**읽기** 8 @no__t-**20** **1 @no__ t-23**4**쓰기** 6**8**9**1**2**create** 4**6**7**9**0**delete** 2 **@no__ t-44**5**7**8**잠금** 0**2**3**5**6**all**  
이벤트가 기록 되도록 지정 합니다. 이벤트 로그를 시작 하려면 더하기 기호를 입력 \( **\+** \) ; 이벤트 로깅을 중지 하려면 이벤트 이름 앞에 빼기 기호를 입력 \( **\-** \) 이벤트 이름 앞입니다. 부호를 생략 하면 더하기 기호 가정 합니다. 사용 하지 않는 **모든** 다른 이벤트 이름입니다.  
  
**lockperiod\=** <em>초</em>  
NFS 용 서버는 NFS 용 서버 서비스를 다시 시작한 후 NFS 용 서버에 대 한 연결 손실 되 고 다음 연결이 다시 설정 된 후 또는 잠금을 회수할 때까지 대기할 시간 (초)의 수를 지정 합니다.  
  
Portmapprotocol\={TCP | UDP | TCP\+UDP  
Portmap의 지원 되는 전송 프로토콜을 지정 합니다. 기본 설정은 **TCP\+UDP**합니다.  
  
mountprotocol\={TCP | UDP | TCP\+UDP}  
전송을 지정 프로토콜 지원 탑재 합니다. 기본 설정은 **TCP\+UDP**합니다.  
  
nfsprotocol\={TCP | UDP | TCP\+UDP}  
전송 프로토콜을 통해 네트워크 파일 시스템 지정 \(NFS\) 지원 합니다. 기본 설정은 **TCP\+UDP**  
  
nlmprotocol\={TCP | UDP | TCP\+UDP}  
네트워크 잠금 관리자는 전송 프로토콜을 통해 지정 \(NLM\) 지원 합니다. 기본 설정은 **TCP\+UDP**합니다.  
  
nsmprotocol\={TCP | UDP | TCP\+UDP}  
네트워크 상태 관리자는 전송 프로토콜을 통해 지정 \(NSM\) 지원 합니다. 기본 설정은 **TCP\+UDP**합니다.  
  
**enableV3\=** {**예** | **없는**}  
NFS 버전 3 프로토콜은 지원 되는지 여부를 지정 합니다. 기본 설정은 **예**합니다.  
  
**renewauth\=** {**예** | **없는**}  
클라이언트 연결에 지정 된 기간 후을 다시 인증 하는 데 필요한 않을 것인지 여부를 지정 **config renewauthinterval**합니다. 기본 설정은 **없는**합니다.  
  
**renewauthinterval\=** <em>초</em>  
클라이언트가 경우 다시 인증 해야 하기 전까지 걸리는 시간 (초)의 수를 지정 **구성 renewauth** 로 설정 된 **예**합니다. 기본값은 600 초입니다.  
  
**dircache\=** <em>크기</em>  
디렉터리 캐시의 킬로바이트 단위에서 크기를 지정합니다. 로 지정 된 숫자 *크기* 4와 128 사이의 4의 배수 여야 합니다. 기본 디렉터리\-캐시 크기는 128KB입니다.  
  
**translationfile**\= @ no__t-2file @ no__t-3  
Windows에서 이동 하는 경우 대체 파일의 이름에는 문자에 대 한 매핑 정보를 포함 하는 파일을 지정\-unix 기반\-파일 시스템을 기반으로 합니다. 경우 *파일* 를 지정 하지 않으면 파일 이름 문자 변환을 사용할 수 없습니다. 하는 경우의 값 **translationfile** 은 변경, 다시 시작 해야 변경 내용이 적용에 대 한 서버입니다.  
  
**dotfileshidden**\={**예** | **없는**}  
마침표로 시작 하는 이름을 사용 하 여 만든 파일을 \( @no__t.-1은 Windows 파일 시스템에서 숨김 상태로 표시 되 고 그에 따라 NFS 클라이언트에서 숨겨집니다. 기본 설정은 **없는**합니다.  
  
**casesensitivelookups\=** {**예** | **없는**}  
디렉터리 조회 대/소문자 구분 여부를 지정 \(문자 사례의 정확한 일치 요구\)합니다.  
  
Windows 커널 대/소문자를 사용 하지 않도록 설정 해야\-경우를 지원 하기는 NFS 용 서버에 대 한 순서에서를 구분 하지 않도록\-중요 한 파일 이름입니다. Windows 커널 케이스를 비활성화할 수\-다음 레지스트리 키를 0 선택 취소 하 여를 구분 하지 않도록 합니다.  
  
HKLM\\시스템\\CurrentControlSet\\컨트롤\\세션 관리자\\커널  
  
DWOrd obcaseinsensitive   
  
> [!IMPORTANT]  
> 이 섹션은 Windows Server 2008 R2, Windows Server 2008 및 Windows Server 2003에만 적용 됩니다. 이 섹션은 Windows Server 2012 R2 또는 Windows Server 2012에 적용 되지 않습니다.  
  
**ntfscase\=** {**낮은** | **위** | **유지**}  
NTFS 파일 시스템에 있는 파일의 이름에 문자를 소문자, 대문자 또는 디렉터리에 저장 된 폼에서에서 반환될지 여부를 지정 합니다. 기본 설정은 **유지**합니다. 이 설정을 변경할 수 없습니다 **casesensitivelookups** 로 설정 된 **예**합니다.  
  
**creategroup** *이름*  
새 클라이언트 그룹을 만들어 지정 된 *이름을*제공 합니다.  
  
**listgroups**  
모든 클라이언트 그룹의 이름을 표시합니다.  
  
**주로** *이름*  
*이름*으로 지정 된 클라이언트 그룹을 제거 합니다.  
  
**renamegroup** *OldName NewName*  
*OldName* 에 지정 된 클라이언트 그룹의 이름을 *NewName* 으로 변경 합니다.  
  
**addmembers** *Name Host*\[ ... \]  
*이름*으로 지정 된 클라이언트 그룹에 *호스트* 를 추가 합니다.  
  
**listmembers** *이름*  
*이름*으로 지정 된 클라이언트 그룹의 호스트 컴퓨터를 나열 합니다.  
  
**deletemembers** *그룹 호스트*\[ ... \]  
*그룹*으로 지정 된 클라이언트 그룹에서 *호스트로* 지정 된 클라이언트를 제거 합니다.  
  
명령 옵션 또는 인수를 지정 하지 않으면 **nfsadmin SERVER** NFS 구성 설정에 대 한 현재 서버를 표시 합니다.  
  
#### <a name="administering-client-for-nfs"></a>NFS 용 클라이언트를 관리합니다.  
사용 된 **nfsadmin 클라이언트** NFS 용 클라이언트를 관리 하는 명령입니다. 특정 작업 하는 **nfsadmin 클라이언트** 하나 지정 하는 명령 인수에 따라 달라 집니다.  
  
**start**  
NFS 용 클라이언트 서비스를 시작 합니다.  
  
**stop**  
NFS 용 클라이언트 서비스를 중지합니다.  
  
**config**  
NFS 용 클라이언트에 대 한 일반 설정을 지정합니다. 하나 이상의 다음 옵션을 제공 해야는 **config** 인수:  
  
**fileaccess\=** <em>모드</em>  
-   네트워크 파일 시스템에서 만든 파일에 대 한 기본 사용 권한 모드를 지정 \(NFS\) 서버입니다. *모드* 인수는 세 자리 숫자로 0에서 7로 구성 됩니다. \(포괄\) 사용자, 그룹 및 부여 된 기본 사용 권한을 나타내는 \(각각\)합니다. 숫자는 다음과 같이 UNIX @ no__t-0style 사용 권한으로 변환 됩니다. 0 @ no__t-0none, 1 @ no__t-1x, 2 @ no__t-2w, 3 @ no__t-3wx, 4 @ no__t-4r, 5 @ no__t-5rx, 6 @ no__t-6rw 및 7 @ no__t-7rwx. 예를 들어 **fileaccess\=750** 제공 소유자에 게 rwx 권한, 그룹에 rx 권한 및 다른 사용자에 게 액세스 권한이 없습니다.  
  
**mapsvr\=** <em>서버</em>  
집합 *서버* NFS 용 클라이언트에 대 한 사용자 이름 매핑 서버입니다. 이 옵션을 이전 버전과 호환성에 대 한 지원 계속 있지만 사용 해야는 **sfuadmin** 유틸리티 대신 합니다.  
  
**mtype\=** {**하드** | **소프트**}  
기본 탑재 유형을 지정합니다. 하드 탑재에 대 한 NFS 용 클라이언트 계속 성공할 때까지 실패 한 RPC를 다시 시도 합니다. 소프트 탑재를 위해 NFS 용 클라이언트 수를 반환 실패 한 호출을 다시 시도한 후 호출 응용 프로그램에 지정 된 횟수는 **다시 시도** 옵션입니다.  
  
**다시 시도\=** <em>번호</em>  
소프트 탑재에 대 한 연결 시도 횟수를 지정 합니다. 이 값은 1에서 10 (포함) 여야 합니다. 기본값은 1입니다.  
  
**제한 시간\=** <em>초</em>  
연결 시 대기 시간 (초)의 수를 지정 \(원격 프로시저 호출\)합니다. 이 값은 0.8, 0.9, 또는 1에서 60도 (포함) 사이의 정수 여야 합니다. 기본값은 0.8입니다.  
  
**프로토콜 @ no__t-1 {TCP | UDP | TCP @ no__t-2UDP}**  
클라이언트에서 지 원하는 전송 프로토콜을 지정 합니다. 기본 설정은 **TCP\+UDP**  
  
**rsize\=** <em>크기</em>  
(킬로바이트) 읽기 버퍼의 크기를 지정 합니다. 이 값은 0.5, 1, 2, 4, 8, 16, 32 또는 수 있습니다. 기본값은 32입니다.  
  
**wsize\=** <em>크기</em>  
(킬로바이트) 쓰기 버퍼의 크기를 지정 합니다. 이 값은 0.5, 1, 2, 4, 8, 16, 32 또는 수 있습니다. 기본값은 32입니다.  
  
**perf @ no__t-1default**  
다음 성능 설정을 기본값으로 복원합니다.  
  
-   **mtype**  
  
-   **retry**  
  
-   **timeout**  
  
-   **rsize**  
  
-   **wsize**  
  
**fileaccess\=** <em>모드</em>  
네트워크 파일 시스템에서 만든 파일에 대 한 기본 사용 권한 모드를 지정 \(NFS\) 서버입니다. *모드* 인수는 세 자리 숫자로 0에서 7로 구성 됩니다. \(포괄\) 사용자, 그룹 및 부여 된 기본 사용 권한을 나타내는 \(각각\)합니다. 숫자는 다음과 같이 UNIX @ no__t-0style 사용 권한으로 변환 됩니다. 0 @ no__t-0none, 1 @ no__t-1x, 2 @ no__t-2w, 3 @ no__t-3wx, 4 @ no__t-4r, 5 @ no__t-5rx, 6 @ no__t-6rw 및 7 @ no__t-7rwx. 예를 들어 **fileaccess\=750** 제공 소유자에 게 rwx 권한, 그룹에 rx 권한 및 다른 사용자에 게 액세스 권한이 없습니다.  
  
명령 옵션 또는 인수를 지정 하지 않으면 **nfsadmin CLIENT** NFS 구성 설정에 대 한 현재 클라이언트를 표시 합니다.  
  

