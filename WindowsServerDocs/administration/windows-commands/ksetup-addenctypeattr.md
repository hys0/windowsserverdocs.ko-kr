---
title: ksetup:addenctypeattr
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 32cc87d7-b9e1-4d14-9eb7-3b439c55aa3a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 711da6a81269fc838ca091765ddbcac63c3fe6e4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886394"
---
# <a name="ksetupaddenctypeattr"></a>ksetup:addenctypeattr



암호화 유형 특성을 도메인에 대 한 가능한 형식 목록에 추가합니다. 이 명령을 사용할 수 있는 방법을의 예 참조 [예제](#BKMK_Examples)합니다.

## <a name="syntax"></a>구문

```
ksetup /addenctypeattr <DomainName> {DES-CBC-CRC | DES-CBC-MD5 | RC4-HMAC-MD5 | AES128-CTS-HMAC-SHA1-96 | AES256-CTS-HMAC-SHA1-96}
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<DomainName>|연결을 설정 하려는 도메인 이름입니다. 정규화 된 도메인 이름 또는 간단한 형태의 corp.contoso.com 또는 contoso와 같은 이름 사용 합니다.|
|암호화 유형|다음 지원 되는 암호화 유형 중 하나 여야 합니다.</br>-   DES-CBC-CRC</br>-   DES-CBC-MD5</br>-   RC4-HMAC-MD5</br>-   AES128-CTS-HMAC-SHA1-96</br>-   AES256-CTS-HMAC-SHA1-96|

## <a name="remarks"></a>설명

Kerberos 티켓 부여 티켓 (TGT) 및 세션 키의 암호화 유형을 보려면를 실행 합니다 **klist** 명령 및 출력을 확인 합니다.

설정 하거나 공백을 사용 하 여 명령에서 암호화 유형을 구분 하 여 여러 암호화 종류를 추가할 수 있습니다. 그러나만 하면 한 도메인에 대 한 번입니다.

명령이 성공 또는 실패 하는 경우 상태 메시지가 표시 됩니다.

연결 하 고 사용 하려는 도메인을 설정 하려면 다음을 실행 합니다 **ksetup /domain \<DomainName >** 명령입니다.

## <a name="BKMK_Examples"></a>예제

이 컴퓨터에 설정 된 현재 암호화 종류를 결정 합니다.
```
klist
```
Corp.contoso.com에 도메인을 설정 합니다.
```
ksetup /domain corp.contoso.com
```
암호화 유형 AES-256-CTS-HMAC-SHA1-96 도메인 corp.contoso.com에 대 한 가능한 형식 목록에 추가 합니다.
```
ksetup /addenctypeattr corp.contoso.com AES-256-CTS-HMAC-SHA1-96
```
Corp.contoso.com 도메인 내에 대 한 AES-256-CTS-HMAC-SHA1-96을 암호화 유형 특성을 설정 합니다.
```
ksetup /setenctypeattr corp.contoso.com AES-256-CTS-HMAC-SHA1-96
```
암호화 유형 특성을 도메인에 대 한 의도 한 대로 설정 된 있는지 확인 합니다.
```
ksetup /getenctypeattr corp.contoso.com
```

#### <a name="additional-references"></a>추가 참조

-   [Klist](klist.md)
-   [Ksetup:domain](ksetup-domain.md)
-   [Ksetup:setenctypeattr](ksetup-setenctypeattr.md)
-   [Ksetup:getenctypeattr](ksetup-getenctypeattr.md)
-   [Ksetup:delenctypeattr](ksetup-delenctypeattr.md)
-   [명령줄 구문 키](command-line-syntax-key.md)