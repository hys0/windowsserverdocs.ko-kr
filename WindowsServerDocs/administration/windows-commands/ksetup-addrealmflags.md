---
title: 'ksetup: addrealmflags'
description: '* * * *에 대 한 참조 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 80ca1e16-8871-494b-b9be-6bc9d63de860
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 26f06e23f40216fe31403280d8946c56825967d6
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724713"
---
# <a name="ksetupaddrealmflags"></a>ksetup: addrealmflags



지정 된 영역에 영역 플래그를 추가 합니다.

## <a name="syntax"></a>구문

```
ksetup /addrealmflags <RealmName> [sendaddress] [tcpsupported] [delegate] [ncsupported] [rc4]
```

#### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|영역 이름|영역 이름은 CORP. 같은 대문자는 DNS 이름으로 명시 CONTOSO.COM입니다.|

## <a name="remarks"></a>설명

영역 플래그는 Windows Server 운영 체제를 기반으로 하지 않는 Kerberos 영역의 추가 기능을 지정 합니다. Windows server 2003, Windows Server 2008 또는 Windows Server 2008 r 2를 실행 하는 컴퓨터는 Kerberos 서버를 사용 하 여 Windows Server 운영 체제를 실행 하는 도메인을 사용 하는 대신 Kerberos 서버를 사용 하 여 인증을 관리할 수 있으며, 이러한 시스템은 Kerberos 영역에 참여 합니다. 이 항목은 영역의 기능을 설정 합니다. 다음 표에서는 각에 대해 설명 합니다.

|값|영역 플래그|설명|
|-----|----------|-----------|
|0xF를 지정합니다.|모두|모든 영역 플래그를 설정 합니다.|
|0x00|None|영역 플래그는 설정 되지 않으며 추가 기능을 사용할 수 없습니다.|
|0x01|SendAddress|IP 주소는 티켓 부여 티켓에 포함 됩니다.|
|0x02|TcpSupported|이 영역에서는 TCP (전송 제어 프로토콜)와 UDP (사용자 데이터 그램 프로토콜)가 모두 지원 됩니다.|
|0x04|대리자(delegate)|이 영역에 있는 모든 사용자는 위임용으로 트러스트 됩니다.|
|0x08|NcSupported|이 영역은 DNS 및 영역 명명 표준을 허용 하는 이름 정규화를 지원 합니다.|
|0x80|RC4|이 영역 TLS 사용에 대 한 수 있는 상호 영역 트러스트를 사용 하도록 설정 하려면 RC4 암호화를 지원 합니다.|

영역 플래그는 **HKEY_LOCAL_MACHINE \system\currentcontrolset\control\lsa\kerberos\domains\\**의 레지스트리에 저장<em>됩니다.</em> 이 항목은 기본적으로 레지스트리에 없습니다. [Ksetup: addrealmflags](ksetup-addrealmflags.md) 명령을 사용 하 여 레지스트리를 채울 수 있습니다.

Ksetup 또는 ksetup/dumpstate.의 출력을 확인 하 여 사용할 수 있는 영역 플래그와 설정 된 영역 플래그를 확인할 수 있습니다.

## <a name="examples"></a>예

CONTOSO 영역에 사용할 수 있는 영역 플래그를 나열 합니다.
```
Ksetup /listrealmflags
```
CONTOSO 영역에 두 개의 플래그를 설정 합니다.
```
ksetup /setrealmflags CONTOSO ncsupported delegate
```
현재 집합에 없는 플래그를 하나 더 추가 합니다.
```
ksetup /addrealmflags CONTOSO SendAddress
```
실행 하는 **ksetup** 출력을 표시 하 고 찾고 여 영역 플래그가 설정 되어 있는지 확인 하기 위해 명령을 **영역 플래그 =** 합니다.

## <a name="additional-references"></a>추가 참조

-   [Ksetup:listrealmflags](ksetup-listrealmflags.md)
-   [Ksetup:setrealmflags](ksetup-setrealmflags.md)
-   [Ksetup:delrealmflags](ksetup-delrealmflags.md)
-   - [명령줄 구문 키](command-line-syntax-key.md)