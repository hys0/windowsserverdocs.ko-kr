---
title: ksetup
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4e046f8a-811b-48dc-9a69-18d8e097f353
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0194cf81d069d7a5c1223f0a514d593e4870d397
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59868844"
---
# <a name="ksetup"></a>ksetup



설정 및 Kerberos 프로토콜 및 Windows 도메인도 없는 Kerberos 영역 지원 하기 위해 키 배포 센터 (KDC)를 유지 관리에 관련 된 작업을 수행 합니다. 이 명령을 사용할 수 있는 방법을 예제를 보려면 각 관련된 하위 항목의 예 섹션을 참조 합니다.

## <a name="syntax"></a>구문

```
ksetup 
[/setrealm <DNSDomainName>] 
[/mapuser <Principal> <Account>] 
[/addkdc <RealmName> <KDCName>] 
[/delkdc <RealmName> <KDCName>]
[/addkpasswd <RealmName> <KDCPasswordName>] 
[/delkpasswd <RealmName> <KDCPasswordName>]
[/server <ServerName>] 
[/setcomputerpassword <Password>]
[/removerealm <RealmName>]  
[/domain <DomainName>] 
[/changepassword <OldPassword> <NewPassword>] 
[/listrealmflags] 
[/setrealmflags <RealmName> [sendaddress] [tcpsupported] [delegate] [ncsupported] [rc4]] 
[/addrealmflags <RealmName> [sendaddress] [tcpsupported] [delegate] [ncsupported] [rc4]] 
[/delrealmflags [sendaddress] [tcpsupported] [delegate] [ncsupported] [rc4]] 
[/dumpstate]
[/addhosttorealmmap] <HostName> <RealmName>]  
[/delhosttorealmmap] <HostName> <RealmName>]  
[/setenctypeattr] <DomainName> {DES-CBC-CRC | DES-CBC-MD5 | RC4-HMAC-MD5 | AES128-CTS-HMAC-SHA1-96 | AES256-CTS-HMAC-SHA1-96}
[/getenctypeattr] <DomainName>
[/addenctypeattr] <DomainName> {DES-CBC-CRC | DES-CBC-MD5 | RC4-HMAC-MD5 | AES128-CTS-HMAC-SHA1-96 | AES256-CTS-HMAC-SHA1-96}
[/delenctypeattr] <DomainName>

```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|[Ksetup:setrealm](ksetup-setrealm.md)|이 컴퓨터의 Kerberos 영역 구성원을 만듭니다.|
|[Ksetup:mapuser](ksetup-mapuser.md)|Kerberos 사용자를 계정에 매핑합니다.|
|[Ksetup:addkdc](ksetup-addkdc.md)|지정 된 영역에 대 한 KDC 항목을 정의합니다.|
|[Ksetup:delkdc](ksetup-delkdc.md)|영역에 대 한 KDC 항목을 삭제합니다.|
|[Ksetup:addkpasswd](ksetup-addkpasswd.md)|영역에 대 한 Kpasswd 서버 주소를 추가합니다.|
|[Ksetup:delkpasswd](ksetup-delkpasswd.md)|영역에 대 한 Kpasswd 서버 주소를 삭제합니다.|
|[Ksetup:server](ksetup-server.md)|변경 내용을 적용 하는 Windows 컴퓨터의 이름을 지정할 수 있습니다.|
|[Ksetup:setcomputerpassword](ksetup-setcomputerpassword.md)|컴퓨터의 도메인 계정 (또는 호스트 보안 주체)에 대 한 암호를 설정합니다.|
|[Ksetup:removerealm](ksetup-removerealm.md)|레지스트리에서 지정한 영역에 대 한 모든 정보를 삭제합니다.|
|[Ksetup:domain](ksetup-domain.md)|도메인을 지정할 수 있습니다 (경우 \<도메인 이름 >를 사용 하 여 설정 되지 않은 **/domain**).|
|[Ksetup:changepassword](ksetup-changepassword.md)|로그온된 한 사용자의 암호를 변경 하는 Kpasswd를 사용할 수 있습니다.|
|[Ksetup:listrealmflags](ksetup-listrealmflags.md)|사용할 수 있는 목록 영역에 플래그를 지정 하는 **ksetup** 감지할 수 있습니다.|
|[Ksetup:setrealmflags](ksetup-setrealmflags.md)|특정 영역에 대 한 영역 플래그를 설정합니다.|
|[Ksetup:addrealmflags](ksetup-addrealmflags.md)|영역에 추가 영역 플래그를 추가합니다.|
|[Ksetup:delrealmflags](ksetup-delrealmflags.md)|영역에서 영역 플래그를 삭제합니다.|
|[Ksetup:dumpstate](ksetup-dumpstate.md)|지정한 컴퓨터에서 Kerberos 구성을 분석 합니다. 레지스트리에서 영역 매핑 호스트를 추가합니다.|
|[Ksetup:addhosttorealmmap](ksetup-addhosttorealmmap.md)|Kerberos 영역에 호스트를 매핑하려면 레지스트리 값을 추가 합니다.|
|[Ksetup:delhosttorealmmap](ksetup-delhosttorealmmap.md)|호스트 컴퓨터 Kerberos 영역에 매핑된 레지스트리 값을 삭제 합니다.|
|[Ksetup:setenctypeattr](ksetup-setenctypeattr.md)|하나 이상의 암호화 종류는 도메인에 대 한 신뢰 특성을 설정합니다.|
|[Ksetup:getenctypeattr](ksetup-getenctypeattr.md)|도메인에 대 한 암호화 형식 신뢰 특성을 가져옵니다.|
|[Ksetup:addenctypeattr](ksetup-addenctypeattr.md)|도메인에 대 한 암호화 형식 신뢰 특성에는 암호화 종류를 추가합니다.|
|[Ksetup:delenctypeattr](ksetup-delenctypeattr.md)|도메인에 대 한 암호화 형식 신뢰 특성을 삭제합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

**Ksetup** Kerberos 영역을 찾기 위한 컴퓨터 설정을 변경 하는 데 사용 됩니다. Microsoft Kerberos 기반 구현에서이 정보는 일반적으로 Krb5.conf 파일에 유지 됩니다. Windows Server 운영 체제의 레지스트리에 저장 됩니다. 이 설정을 수정 하려면이 도구를 사용할 수 있습니다. 이러한 설정은가 도메인 컨트롤러를 찾을 영역 간 트러스트 관계에 대 한 Kerberos 영역 Kerberos 영역을 찾으려고 워크스테이션이 사용 됩니다.

**Ksetup** Kerberos 보안 지원 공급자 (SSP) 컴퓨터가 Windows Server 2003, Windows Server 2008 또는 Windows Server 2008 R2 실행 되 고는 Windows의 구성원이 아닙니다 경우 Kerberos 영역에 대 한 KDC를 찾기 위해 사용 하는 레지스트리 키를 초기화 합니다. 도메인입니다. 구성 후 운영 체제에 로그온 할 수는 Windows를 실행 하는 클라이언트 컴퓨터의 사용자는 Kerberos 영역에 차지 합니다.

Kerberos 버전 5 프로토콜은 Windows XP Professional, Windows Vista 및 Windows 7을 실행 하는 컴퓨터에 네트워크 인증에 대 한 기본값입니다. Kerberos SSP에는 분야와 사용자의 도메인 이름에 대 한 레지스트리를 검색 하 고 DNS 서버를 쿼리하여 이름을 IP 주소로 확인 합니다. Kerberos 프로토콜 영역 이름만 사용 하 여 Kdc를 찾는 데 DNS를 사용할 수 있지만 그러려면 특별히 구성 해야 합니다.

#### <a name="additional-references"></a>추가 참조

-   [명령줄 구문 키](command-line-syntax-key.md)