---
title: 'ksetup: setenctypeattr'
description: '\* * * *에 대 한 Windows 명령 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 88fb913e-6b57-48d9-8c16-a035ab2977ac
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 78450202b33f76ab7b0a374fe4559f0a25e709b5
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80841346"
---
# <a name="ksetupsetenctypeattr"></a>ksetup: setenctypeattr



도메인에 대 한 암호화 유형 특성을 설정합니다. 이 명령을 사용할 수 있는 방법을의 예 참조 [예제](#BKMK_Examples)합니다.

## <a name="syntax"></a>구문

```
ksetup /setenctypeattr <Domain name> {DES-CBC-CRC | DES-CBC-MD5 | RC4-HMAC-MD5 | AES128-CTS-HMAC-SHA1-96 | AES256-CTS-HMAC-SHA1-96}
```

#### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<DomainName >|연결을 설정 하려는 도메인 이름입니다. 정규화 된 도메인 이름 또는 corp.contoso.com 또는 contoso와 같은 간단한 형식의 이름을 사용 합니다.|
|암호화 유형|다음 지원 되는 암호화 유형 중 하나 여야 합니다.</br>-DES-CBC-CRC</br>-DES-CBC-MD5</br>-RC4-HMAC-MD5</br>-AES128--HMAC-SHA1-96</br>-AES256--HMAC-SHA1-96|

## <a name="remarks"></a>주의

Kerberos TGT (티켓 허용 티켓) 및 세션 키의 암호화 유형을 보려면 **klist** 명령을 실행 하 고 출력을 확인 합니다.

명령의 암호화 유형을 공백으로 구분 하 여 여러 암호화 유형을 설정 하거나 추가할 수 있습니다. 그러나 한 번에 하나의 도메인에 대해서만이 작업을 수행할 수 있습니다.

명령이 성공 하거나 실패 하면 상태 메시지가 표시 됩니다.

연결 하 고 사용 하려는 도메인을 설정 하려면 **ksetup/domain \<DomainName >** 명령을 실행 합니다.

## <a name="examples"></a><a name=BKMK_Examples></a>예와

이 컴퓨터에 설정 된 현재 암호화 종류를 확인 합니다.
```
klist
```
Corp.contoso.com에 도메인을 설정 합니다.
```
ksetup /domain corp.contoso.com
```
Corp.contoso.com 도메인 내에 대 한 AES-256-CTS-HMAC-SHA1-96을 암호화 유형 특성을 설정 합니다.
```
ksetup /setenctypeattr corp.contoso.com AES-256-CTS-HMAC-SHA1-96
```
암호화 유형 특성이 도메인에 대해 의도 한 대로 설정 되었는지 확인 합니다.
```
ksetup /getenctypeattr corp.contoso.com
```

## <a name="additional-references"></a>추가 참조

-   [Klist](klist.md)
-   [Ksetup:domain](ksetup-domain.md)
-   [Ksetup:addenctypeattr](ksetup-addenctypeattr.md)
-   [Ksetup:getenctypeattr](ksetup-getenctypeattr.md)
-   [Ksetup:delenctypeattr](ksetup-delenctypeattr.md)
-   - [명령줄 구문 키](command-line-syntax-key.md)