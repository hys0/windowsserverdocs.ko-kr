---
title: ksetup:mapuser
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 2828f92b20cafcb571c81c8ceae28c741fbe025a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59872864"
---
# <a name="ksetupmapuser"></a>ksetup:mapuser



Kerberos 주체 이름의 계정에 매핑합니다. 이 명령을 사용할 수 있는 방법을의 예 참조 [예제](#BKMK_Examples)합니다.

## <a name="syntax"></a>구문

```
ksetup /mapuser <Principal> <Account>
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<계정 >|모든 보안 주체;의 정규화 된 도메인 이름 예를 들어 mike@corp.CONTOSO.COM합니다.|
|\<계정 >|모든 계정 또는 보안 그룹 이름 같은 게스트, 도메인 사용자 또는 관리자가이 컴퓨터에 존재 하는입니다.|

## <a name="remarks"></a>설명

계정을 식별할 수 있습니다 특히, 도메인 게스트 등. 또는 모든 계정을 포함 하도록 와일드 카드 문자 (*)를 사용할 수 있습니다.

계정 이름을 생략 하면 지정된 된 보안 주체에 대 한 매핑이 삭제 됩니다.

만 컴퓨터는 유효한 Kerberos 티켓을 제공 하는 경우 지정된 된 영역의 보안 주체를 인증 해야 합니다.

사용 하 여 **ksetup** 모든 매개 변수 또는 인수를 설정 및 기본 영역이 현재 매핑되는지 확인 합니다.

외부 키 배포 센터 (KDC) 및 영역 구성으로 변경 될 때마다 여기서 설정이 변경 된 컴퓨터를 다시 시작이 필요 합니다.

## <a name="BKMK_Examples"></a>예제

문의 사항이 있으면이 컴퓨터에 인증할 필요가 없는 기본 제공 Guest 계정 멤버의 모든 권한을 부여 하는이 컴퓨터에 대 한 게스트 계정에 CONTOSO Kerberos 영역 내에서 Mike Danseglio 계정을 매핑하십시오.
```
ksetup /mapuser mike@corp.CONTOSO.COM guest
```
문의 사항이 있으면 CONTOSO에서 자신의 자격 증명을 사용 하 여이 컴퓨터에 인증 되지 않도록 하려면이 컴퓨터의 게스트 계정에 Mike Danseglio 계정 매핑을 제거 합니다.
```
ksetup /mapuser mike@corp.CONTOSO.COM 
```
Mike Danseglio 계정을 CONTOSO Kerberos 영역 내에서이 컴퓨터의 모든 기존 계정에 매핑하십시오. (표준 사용자 및 게스트 계정에는이 컴퓨터에서 활성 상태인 경우 Mike의 권한은 설정할 것):
```
ksetup /mapuser mike@corp.CONTOSO.COM *
```
이 컴퓨터에 동일한 이름의 모든 기존 계정에서 CONTOSO Kerberos 영역 내에서 모든 계정을 매핑하십시오.
```
ksetup /mapuser * *
```

#### <a name="additional-references"></a>추가 참조

-   [명령줄 구문 키](command-line-syntax-key.md)
-   [Ksetup](ksetup.md)