---
title: 'ksetup: mapuser'
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 84113e6e-89ff-488a-9cd0-f14bbf23b543
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6b80538999c364e9ed10ca0ed43387f603ac9ad3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71374984"
---
# <a name="ksetupmapuser"></a>ksetup: mapuser



Kerberos 보안 주체의 이름을 계정에 매핑합니다. 이 명령을 사용할 수 있는 방법을의 예 참조 [예제](#BKMK_Examples)합니다.

## <a name="syntax"></a>구문

```
ksetup /mapuser <Principal> <Account>
```

### <a name="parameters"></a>매개 변수

|  매개 변수   |                                                   설명                                                   |
|--------------|-----------------------------------------------------------------------------------------------------------------|
| \<Principal > |              모든 보안 주체의 정규화 된 도메인 이름입니다. 예를 들어 mike@corp.CONTOSO.COM입니다.              |
|  \<Account >  | 게스트, 도메인 사용자 또는 관리자와 같이이 컴퓨터에 존재 하는 계정 또는 보안 그룹 이름입니다. |

## <a name="remarks"></a>설명

도메인 게스트 등의 계정을 구체적으로 식별할 수 있습니다. 또는 와일드 카드 문자 (*)를 사용 하 여 모든 계정을 포함할 수 있습니다.

계정 이름을 생략 하면 지정 된 보안 주체에 대 한 매핑이 삭제 됩니다.

유효한 Kerberos 티켓이 있는 경우 컴퓨터는 지정 된 영역의 보안 주체를 인증 합니다.

매개 변수 또는 인수 없이 **ksetup** 를 사용 하 여 현재 매핑된 설정 및 기본 영역을 확인 합니다.

외부 키 배포 센터 (KDC) 및 영역 구성이 변경 될 때마다 설정이 변경 된 컴퓨터를 다시 시작 해야 합니다.

## <a name="BKMK_Examples"></a>예와

Kerberos 영역 CONTOSO 내에서이 컴퓨터의 게스트 계정에 Mike Danseglio의 계정을 매핑하고,이 컴퓨터에 인증 하지 않고도 기본 제공 게스트 계정의 구성원에 대 한 모든 권한을 부여 합니다.
```
ksetup /mapuser mike@corp.CONTOSO.COM guest
```
CONTOSO의 자격 증명을 사용 하 여이 컴퓨터에 대 한 인증을 방지 하기 위해이 컴퓨터의 게스트 계정에 대 한 Mike Danseglio의 계정 매핑을 제거 합니다.
```
ksetup /mapuser mike@corp.CONTOSO.COM 
```
CONTOSO Kerberos 영역 내의 Mike Danseglio의 계정을이 컴퓨터의 모든 기존 계정에 매핑합니다. (이 컴퓨터에서 표준 사용자 및 게스트 계정만 활성 상태인 경우에는 Mike의 권한이 설정 됩니다.)
```
ksetup /mapuser mike@corp.CONTOSO.COM *
```
CONTOSO Kerberos 영역 내의 모든 계정을이 컴퓨터에 있는 동일한 이름의 기존 계정에 모두 매핑:
```
ksetup /mapuser * *
```

#### <a name="additional-references"></a>추가 참조

-   [명령줄 구문 키](command-line-syntax-key.md)
-   [Ksetup](ksetup.md)