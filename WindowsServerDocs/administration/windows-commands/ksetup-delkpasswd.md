---
title: ksetup:delkpasswd
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2db0bfcd-bc08-48e3-9f30-65b6411839c6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a1c701707f736fe51a1f4af70a2571e63025f281
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438046"
---
# <a name="ksetupdelkpasswd"></a>ksetup:delkpasswd

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

영역에 대 한 Kerberos 암호 서버 (Kpasswd)를 제거합니다. 이 명령을 사용할 수 있는 방법을의 예 참조 [예제](#BKMK_Examples)합니다.
## <a name="syntax"></a>구문
```
ksetup /delkpasswd <RealmName> <KpasswdName>
```
### <a name="parameters"></a>매개 변수

|   매개 변수   |                                                                                                   설명                                                                                                   |
|---------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  <RealmName>  |                                영역 이름은 CORP. 같은 대문자는 DNS 이름으로 지정 됩니다. CONTOSO.COM, 기본적으로 나열 되 고 영역 또는 영역 = **ksetup** 실행 됩니다.                                |
| <KpasswdName> | Kerberos 암호 서버와 사용할 KDC 이름이 mitkdc.contoso.com 같은 대/소문자 정규화 된 도메인 이름으로 명시 됩니다. KDC 이름이 생략 된 경우 Kdc 찾을 DNS는 사용할 수 있습니다. |

## <a name="remarks"></a>설명
명령을 실행 **ksetup** KDC 이름을 확인할 수 있습니다. 하는 경우 **kpasswd =** 매핑을 구성한 경우 다음 출력에 나타나지 않습니다. 여러 매핑을 나열 됩니다 하는 경우 설정 합니다.
## <a name="BKMK_Examples"></a>예제
CORP. 영역 확인 CONTOSO.COM는 비 Windows KDC 서버 mitkdc.contoso.com 암호 서버로 사용합니다.
```
ksetup /delkpasswd CORP.CONTOSO.COM mitkdc.contoso.com
```
실행 명령이 의도 한 대로 작동을 확인 하려면 **ksetup** CORP. 영역을 확인 하려면 Windows 컴퓨터 CONTOSO.COM은 Kerberos 암호 서버 (KDC 이름)에 매핑되지 않았습니다.
## <a name="additional-references"></a>추가 참조
-   [ksetup](ksetup.md)
-   [ksetup:delkpasswd](ksetup-delkpasswd.md)
-   [명령줄 구문 키](command-line-syntax-key.md)
