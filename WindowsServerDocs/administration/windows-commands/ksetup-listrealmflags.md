---
title: 'ksetup: listrealmflags'
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aa96e4da-6b98-4c05-bccf-73cbf33258c2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8f103875dc10dfbf7b0c604a8e2060fe58ee7a92
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71374974"
---
# <a name="ksetuplistrealmflags"></a>ksetup: listrealmflags



**Ksetup**에서 보고할 수 있는 사용 가능한 영역 플래그를 나열 합니다. 이 명령을 사용할 수 있는 방법을의 예 참조 [예제](#BKMK_Examples)합니다.

## <a name="syntax"></a>구문

```
ksetup /listrealmflags
```

### <a name="parameters"></a>매개 변수

없음

## <a name="remarks"></a>설명

영역 플래그는 비 Windows 기반 Kerberos 영역에 대 한 추가 기능을 지정 합니다. Windows server 2003, Windows Server 2008 또는 Windows Server 2008 r 2를 실행 하는 컴퓨터는 windows Server 운영 체제를 실행 하는 도메인을 사용 하는 대신 Windows 기반이 아닌 Kerberos 서버를 사용 하 여 인증을 관리할 수 있습니다. 이러한 시스템은 Windows 도메인 대신 Kerberos 영역에 참여 합니다. 이 항목은 영역의 기능을 설정 합니다. 다음 표에서는 각에 대해 설명 합니다.

|값|영역 플래그|설명|
|-----|----------|-----------|
|0xF를 지정합니다.|모두|모든 영역 플래그를 설정 합니다.|
|0x00|없음|영역 플래그는 설정 되지 않으며 추가 기능을 사용할 수 없습니다.|
|0x01|SendAddress|IP 주소는 티켓 부여 티켓에 포함 됩니다.|
|0x02|TcpSupported|이 영역에서는 TCP (전송 제어 프로토콜) 및 UDP (사용자 데이터 그램 프로토콜)가 지원 됩니다.|
|0x04|대리자|이 영역에 있는 모든 사용자는 위임용으로 트러스트 됩니다.|
|0x08|NcSupported|이 영역은 DNS 및 영역 명명 표준을 허용 하는 이름 정규화를 지원 합니다.|
|0x80|RC4|이 영역 TLS 사용에 대 한 수 있는 상호 영역 트러스트를 사용 하도록 설정 하려면 RC4 암호화를 지원 합니다.|

영역 플래그는 **HKEY_LOCAL_MACHINE \system\currentcontrolset\control\lsa\kerberos\domains\\** 의 레지스트리에 저장 <em>됩니다.</em> 이 항목은 기본적으로 레지스트리에 없습니다. 사용할 수는 [Ksetup:addrealmflags](ksetup-addrealmflags.md) 레지스트리를 채우는 데는 명령입니다.

## <a name="BKMK_Examples"></a>예와

이 컴퓨터에 알려진 영역 플래그를 나열 합니다.
```
ksetup /listrealmflags
```
명령줄에서 다음 명령 중 하나를 입력 하 여 **Ksetup** 에서 알지 못하는 사용 가능한 영역 플래그를 설정 합니다.
```
ksetup /setrealmflags CORP.CONTOSO.COM sendaddress tcpsupported delete ncsupported
```
```
ksetup /setrealmflags CORP.CONTOSO.COM 0xF
```

#### <a name="additional-references"></a>추가 참조

-   [Ksetup:setrealmflags](ksetup-setrealmflags.md)
-   [Ksetup:addrealmflags](ksetup-addrealmflags.md)
-   [Ksetup:delrealmflags](ksetup-delrealmflags.md)
-   [Ksetup](ksetup.md)
-   [명령줄 구문 키](command-line-syntax-key.md)