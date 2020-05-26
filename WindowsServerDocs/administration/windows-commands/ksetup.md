---
title: ksetup
description: Ksetup 명령에 대 한 참조 항목으로, kerberos 프로토콜을 설정 및 유지 관리 하는 작업과 관련 된 작업을 수행 하 고 Kerberos 영역을 지원 하기 위해 KDC (키 배포 센터)를 수행 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4e046f8a-811b-48dc-9a69-18d8e097f353
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 82b1627a8ddbc9e51ac32825c5a42c3df9effbf7
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83817353"
---
# <a name="ksetup"></a>ksetup

Kerberos 프로토콜을 설정 하 고 유지 관리 하는 작업과 관련 된 작업을 수행 하 고 Kerberos 영역을 지원 하기 위한 키 배포 센터 (KDC) 구체적으로이 명령은 다음 작업에 사용 됩니다.

- Kerberos 영역을 찾기 위한 컴퓨터 설정을 변경 합니다. Microsoft가 아닌 Kerberos 기반 구현에서이 정보는 일반적으로 Krb5.conf 파일에 보관 됩니다. Windows Server 운영 체제에서는 레지스트리에 보관 됩니다. 이 설정을 수정 하려면이 도구를 사용할 수 있습니다. 이러한 설정은가 도메인 컨트롤러를 찾을 영역 간 트러스트 관계에 대 한 Kerberos 영역 Kerberos 영역을 찾으려고 워크스테이션이 사용 됩니다.

- 컴퓨터가 Windows 도메인의 구성원이 아닌 경우 Kerberos SSP (보안 지원 공급자)가 Kerberos 영역에 대 한 KDC를 찾기 위해 사용 하는 레지스트리 키를 초기화 합니다. 구성 후 Windows 운영 체제를 실행 하는 클라이언트 컴퓨터의 사용자는 Kerberos 영역에 있는 계정에 로그온 할 수 있습니다.

- 레지스트리에서 사용자 영역의 도메인 이름을 검색 한 다음 DNS 서버를 쿼리하여 이름을 IP 주소로 확인 합니다. Kerberos 프로토콜 영역 이름만 사용 하 여 Kdc를 찾는 데 DNS를 사용할 수 있지만 그러려면 특별히 구성 해야 합니다.

## <a name="syntax"></a>구문

```
ksetup
[/setrealm <DNSdomainname>]
[/mapuser <principal> <account>]
[/addkdc <realmname> <KDCname>]
[/delkdc <realmname> <KDCname>]
[/addkpasswd <realmname> <KDCPasswordName>]
[/delkpasswd <realmname> <KDCPasswordName>]
[/server <servername>]
[/setcomputerpassword <password>]
[/removerealm <realmname>]
[/domain <domainname>]
[/changepassword <oldpassword> <newpassword>]
[/listrealmflags]
[/setrealmflags <realmname> [sendaddress] [tcpsupported] [delegate] [ncsupported] [rc4]]
[/addrealmflags <realmname> [sendaddress] [tcpsupported] [delegate] [ncsupported] [rc4]]
[/delrealmflags [sendaddress] [tcpsupported] [delegate] [ncsupported] [rc4]]
[/dumpstate]
[/addhosttorealmmap] <hostname> <realmname>]
[/delhosttorealmmap] <hostname> <realmname>]
[/setenctypeattr] <domainname> {DES-CBC-CRC | DES-CBC-MD5 | RC4-HMAC-MD5 | AES128-CTS-HMAC-SHA1-96 | AES256-CTS-HMAC-SHA1-96}
[/getenctypeattr] <domainname>
[/addenctypeattr] <domainname> {DES-CBC-CRC | DES-CBC-MD5 | RC4-HMAC-MD5 | AES128-CTS-HMAC-SHA1-96 | AES256-CTS-HMAC-SHA1-96}
[/delenctypeattr] <domainname>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| [ksetup setrealm](ksetup-setrealm.md) | 이 컴퓨터의 Kerberos 영역 구성원을 만듭니다. |
| [ksetup addkdc](ksetup-addkdc.md) | 지정 된 영역에 대 한 KDC 항목을 정의합니다. |
| [ksetup delkdc](ksetup-delkdc.md) | 영역에 대 한 KDC 항목을 삭제합니다. |
| [ksetup addkpasswd](ksetup-addkpasswd.md) | 영역에 대 한 kpasswd 서버 주소를 추가 합니다. |
| [ksetup delkpasswd](ksetup-delkpasswd.md) | 영역에 대 한 kpasswd 서버 주소를 삭제 합니다. |
| [ksetup 서버](ksetup-server.md) | 변경 내용을 적용 하는 Windows 컴퓨터의 이름을 지정할 수 있습니다. |
| [ksetup setcomputerpassword](ksetup-setcomputerpassword.md) | 컴퓨터의 도메인 계정 (또는 호스트 보안 주체)에 대 한 암호를 설정합니다. |
| [ksetup removerealm](ksetup-removerealm.md) | 레지스트리에서 지정한 영역에 대 한 모든 정보를 삭제합니다. |
| [ksetup 도메인](ksetup-domain.md) | 도메인을 지정할 수 있습니다 (가 `<domainname>` 이미 **/domain** 매개 변수로 설정 되지 않은 경우). |
| [ksetup changepassword](ksetup-changepassword.md) | Kpasswd를 사용 하 여 로그온 한 사용자의 암호를 변경할 수 있습니다. |
| [ksetup listrealmflags](ksetup-listrealmflags.md) | 사용할 수 있는 목록 영역에 플래그를 지정 하는 **ksetup** 감지할 수 있습니다. |
| [ksetup setrealmflags](ksetup-setrealmflags.md) | 특정 영역에 대 한 영역 플래그를 설정합니다. |
| [ksetup addrealmflags](ksetup-addrealmflags.md) | 영역에 추가 영역 플래그를 추가합니다. |
| [ksetup delrealmflags](ksetup-delrealmflags.md) | 영역에서 영역 플래그를 삭제합니다. |
| [ksetup](ksetup-dumpstate.md) | 지정한 컴퓨터에서 Kerberos 구성을 분석 합니다. 레지스트리에서 영역 매핑 호스트를 추가합니다. |
| [ksetup addhosttorealmmap](ksetup-addhosttorealmmap.md) | Kerberos 영역에 호스트를 매핑하려면 레지스트리 값을 추가 합니다. |
| [ksetup delhosttorealmmap](ksetup-delhosttorealmmap.md) | 호스트 컴퓨터 Kerberos 영역에 매핑된 레지스트리 값을 삭제 합니다. |
| [ksetup setenctypeattr](ksetup-setenctypeattr.md) | 하나 이상의 암호화 종류는 도메인에 대 한 신뢰 특성을 설정합니다. |
| [ksetup getenctypeattr](ksetup-getenctypeattr.md) | 도메인에 대 한 암호화 형식 신뢰 특성을 가져옵니다. |
| [ksetup addenctypeattr](ksetup-addenctypeattr.md) | 도메인에 대 한 암호화 형식 신뢰 특성에는 암호화 종류를 추가합니다. |
| [ksetup delenctypeattr](ksetup-delenctypeattr.md) | 도메인에 대 한 암호화 형식 신뢰 특성을 삭제합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)