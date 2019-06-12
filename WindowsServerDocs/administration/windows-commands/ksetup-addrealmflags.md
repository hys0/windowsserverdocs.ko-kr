---
title: ksetup:addrealmflags
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 80ca1e16-8871-494b-b9be-6bc9d63de860
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f097fc8268976cf038523de0d5fa33c1dd3c6901
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438033"
---
# <a name="ksetupaddrealmflags"></a>ksetup:addrealmflags



지정 된 영역에 추가 영역 플래그를 추가합니다. 이 명령을 사용할 수 있는 방법을의 예 참조 [예제](#BKMK_Examples)합니다.

## <a name="syntax"></a>구문

```
ksetup /addrealmflags <RealmName> [sendaddress] [tcpsupported] [delegate] [ncsupported] [rc4]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|영역 이름|영역 이름은 CORP. 같은 대문자는 DNS 이름으로 명시 CONTOSO.COM입니다.|

## <a name="remarks"></a>설명

영역 플래그를 Windows Server 운영 체제를 기반으로 하는 Kerberos 영역의 추가 기능을 지정 합니다. Windows Server 2003, Windows Server 2008 또는 Windows Server 2008 R2를 실행 중인 컴퓨터는 Kerberos 관리할 서버를 Windows Server 운영 체제를 실행 하는 도메인을 사용 하는 대신 인증을 사용할 수 있으며 이러한 시스템에 참여를 Kerberos 영역입니다. 이 항목의 영역 기능을 설정합니다. 다음 표에서 각를 설명 합니다.

|값|영역 플래그|설명|
|-----|----------|-----------|
|0xF를 지정합니다.|All|영역 플래그를 모두 설정 됩니다.|
|0x00|없음|영역 플래그가 설정 되지 않음, 및 없는 추가 기능을 사용할 수 있습니다.|
|0x01|SendAddress|IP 주소 ticket-granting ticket 내에 포함 됩니다.|
|0x02|TcpSupported|(TCP (Transmission Control Protocol) 및 사용자 데이터 그램 프로토콜 (UDP) 둘 다이 영역에서 지원 됩니다.|
|0x04|대리자|모든 사용자가이 영역입니다 위임용으로 트러스트 합니다.|
|0x08|NcSupported|이 영역에서는 DNS 및 영역 이름 지정 표준이 허용 하는 이름을 정규화를 지원 합니다.|
|0x80|RC4|이 영역 TLS 사용에 대 한 수 있는 상호 영역 트러스트를 사용 하도록 설정 하려면 RC4 암호화를 지원 합니다.|

영역 플래그 레지스트리의 아래에 저장 됩니다 **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\Kerberos\Domains\\** <em>영역 이름을</em>입니다. 이 항목은 기본적으로 레지스트리에 없습니다. 사용할 수는 [ksetup: addrealmflags](ksetup-addrealmflags.md) 레지스트리를 채우는 데 명령입니다.

어떤 영역 플래그는 설정 및 사용 가능한 표시 ksetup 또는 ksetup /dumpstate의 출력을 확인 하 여 합니다.

## <a name="BKMK_Examples"></a>예제

CONTOSO 영역에 대 한 사용 가능한 영역 플래그를 나열 합니다.
```
Ksetup /listrealmflags
```
CONTOSO 영역에 두 개의 플래그를 설정 합니다.
```
ksetup /setrealmflags CONTOSO ncsupported delegate
```
현재 집합에 없는 자세한 플래그를 추가 합니다.
```
ksetup /addrealmflags CONTOSO SendAddress
```
실행 하는 **ksetup** 출력을 표시 하 고 찾고 여 영역 플래그가 설정 되어 있는지 확인 하기 위해 명령을 **영역 플래그 =** 합니다.

#### <a name="additional-references"></a>추가 참조

-   [Ksetup:listrealmflags](ksetup-listrealmflags.md)
-   [Ksetup:setrealmflags](ksetup-setrealmflags.md)
-   [Ksetup:delrealmflags](ksetup-delrealmflags.md)
-   [명령줄 구문 키](command-line-syntax-key.md)