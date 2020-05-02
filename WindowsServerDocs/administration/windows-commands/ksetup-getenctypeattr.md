---
title: 'ksetup: getenctypeattr'
description: '* * * *에 대 한 참조 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6c7ec002-355e-474d-bc27-27215049f1a8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f8363113d4fbb310d98b40d852b36a00f20320e6
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724629"
---
# <a name="ksetupgetenctypeattr"></a>ksetup: getenctypeattr



도메인에 대 한 암호화 유형 특성을 검색 합니다.

## <a name="syntax"></a>구문

```
ksetup /getenctypeattr <DomainName> 
```

#### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<DomainName>|연결을 설정 하려는 도메인 이름입니다. 정규화 된 도메인 이름 또는 corp.contoso.com 또는 contoso와 같은 간단한 형식의 이름을 사용 합니다.|

## <a name="remarks"></a>설명

Kerberos TGT (티켓 허용 티켓) 및 세션 키의 암호화 유형을 보려면 **klist** 명령을 실행 하 고 출력을 확인 합니다.

명령이 성공 하거나 실패 하면 성공적으로 완료 되거나 성공적으로 완료 되 면 상태 메시지가 표시 됩니다.

연결 하 고 사용 하려는 도메인을 설정 하려면 **ksetup/Domain \<DomainName>** 명령을 실행 합니다.

## <a name="examples"></a>예

도메인에 대 한 암호화 유형 특성을 확인 합니다.
```
ksetup /getenctypeattr mit.contoso.com
```

## <a name="additional-references"></a>추가 참조

-   [Klist](klist.md)
-   [Ksetup:domain](ksetup-domain.md)
-   [Ksetup:addenctypeattr](ksetup-addenctypeattr.md)
-   [Ksetup:setenctypeattr](ksetup-setenctypeattr.md)
-   [Ksetup:delenctypeattr](ksetup-delenctypeattr.md)
-   - [명령줄 구문 키](command-line-syntax-key.md)