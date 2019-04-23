---
title: ksetup:getenctypeattr
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6c7ec002-355e-474d-bc27-27215049f1a8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 302f94616f98eb350332b08ad37a58305a0a0be1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59841994"
---
# <a name="ksetupgetenctypeattr"></a>ksetup:getenctypeattr



도메인에 대 한 암호화 유형 특성을 검색합니다. 이 명령을 사용할 수 있는 방법을의 예 참조 [예제](#BKMK_Examples)합니다.

## <a name="syntax"></a>구문

```
ksetup /getenctypeattr <DomainName> 
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<DomainName>|연결을 설정 하려는 도메인 이름입니다. 정규화 된 도메인 이름 또는 간단한 형태의 corp.contoso.com 또는 contoso와 같은 이름 사용 합니다.|

## <a name="remarks"></a>설명

Kerberos 티켓 부여 티켓 (TGT) 및 세션 키의 암호화 유형을 보려면를 실행 합니다 **klist** 명령 및 출력을 확인 합니다.

명령이 성공 또는 실패 하는 경우 성공 또는 실패 한 완료 시 상태 메시지가 표시 됩니다.

연결 하 고 사용 하려는 도메인을 설정 하려면 다음을 실행 합니다 **ksetup /domain \<DomainName >** 명령입니다.

## <a name="BKMK_Examples"></a>예제

도메인에 대 한 암호화 유형 특성을 확인 합니다.
```
ksetup /getenctypeattr mit.contoso.com
```

#### <a name="additional-references"></a>추가 참조

-   [Klist](klist.md)
-   [Ksetup:domain](ksetup-domain.md)
-   [Ksetup:addenctypeattr](ksetup-addenctypeattr.md)
-   [Ksetup:setenctypeattr](ksetup-setenctypeattr.md)
-   [Ksetup:delenctypeattr](ksetup-delenctypeattr.md)
-   [명령줄 구문 키](command-line-syntax-key.md)