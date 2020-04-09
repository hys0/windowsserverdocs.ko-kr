---
title: 'ksetup: addkpasswd'
description: '\* * * *에 대 한 Windows 명령 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d3196995-1b38-48ff-ba08-911cfab77317
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 73abfff54ecfcd31ebbd7469c12228fff850fbf1
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80841826"
---
# <a name="ksetupaddkpasswd"></a>ksetup: addkpasswd



영역에 대 한 Kerberos 암호 (Kpasswd) 서버 주소를 추가합니다. 이 명령을 사용할 수 있는 방법을의 예 참조 [예제](#BKMK_Examples)합니다.

## <a name="syntax"></a>구문

```
ksetup /addkpasswd <RealmName> [<KpasswdName>]
```

#### <a name="parameters"></a>매개 변수

워크스테이션 됩니다 인증 하는 수를 지 원하는 Kerberos Kerberos 영역 암호 프로토콜을 변경 하는 경우에 Kerberos 암호 서버를 사용 하 여 Windows 운영 체제를 실행 하는 클라이언트 컴퓨터를 구성할 수 있습니다. 이 설정은 영역 쪽에서 구성 됩니다.

|매개 변수|설명|
|---------|-----------|
|\<RealmName >|영역 이름은 CORP. 같은 대문자는 DNS 이름으로 명시 CONTOSO.COM, 기본적으로 나열 하 고 영역 또는 영역 = **ksetup** 실행 됩니다.|
|\<KpasswdName >|Kerberos 암호 서버도 사용할 수 있는 KDC 이름이 mitkdc.microsoft.com 같은 대/소문자 정규화 된 도메인 이름으로 명시 됩니다. KDC 이름이 생략 된 경우 Kdc 찾을 DNS는 사용할 수 있습니다.|

## <a name="remarks"></a>주의

워크스테이션 됩니다 인증 하는 수를 지 원하는 Kerberos Kerberos 영역 암호 프로토콜을 변경 하는 경우에 Kerberos 암호 서버를 사용 하 여 Windows 운영 체제를 실행 하는 클라이언트 컴퓨터를 구성할 수 있습니다.

명령을 실행 **ksetup** KDC 이름을 확인할 수 있습니다. 경우 **kpasswd =** 나타나지 않고 출력에서 매핑을 구성 하지 않았습니다.

한 번에 하나씩 추가 KDC 이름에 추가할 수 있습니다.

## <a name="examples"></a><a name=BKMK_Examples></a>예와

영역, CORP. 구성 CONTOSO.COM mitkdc.contoso.com, 비 Windows KDC 서버 암호 서버로 사용 하도록 합니다.
```
ksetup /addkpasswd CORP.CONTOSO.COM mitkdc.contoso.com
```
이 인해 인증 사이 영역에 대 한 모든 암호를 제어 하는 비 Windows Kerberos 암호 서버.

## <a name="additional-references"></a>추가 참조

-   [Ksetup](ksetup.md)
-   [Ksetup:delkpasswd](ksetup-delkpasswd.md)
-   - [명령줄 구문 키](command-line-syntax-key.md)