---
title: 'ksetup: delenctypeattr'
description: '* * * *에 대 한 참조 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4fc25ef3-e271-4229-a712-72c507df55aa
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2908cc0a095a6985c11f7885766926b7f0354ab0
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724700"
---
# <a name="ksetupdelenctypeattr"></a>ksetup: delenctypeattr



도메인에 대 한 암호화 유형 특성을 제거 합니다.

## <a name="syntax"></a>구문

```
ksetup /delenctypeattr <DomainName> 
```

#### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<DomainName>|연결을 설정 하려는 도메인 이름입니다. 정규화 된 도메인 이름 또는 corp.contoso.com 또는 contoso와 같은 간단한 형식의 이름을 사용 합니다.|

## <a name="remarks"></a>설명

Kerberos TGT (티켓 허용 티켓) 및 세션 키의 암호화 유형을 보려면 **klist** 명령을 실행 하 고 출력을 확인 합니다.

성공 또는 실패 완료 시 상태 메시지가 표시 됩니다.

연결 하 고 사용 하려는 도메인을 설정 하려면 **ksetup/Domain \<DomainName>** 명령을 실행 합니다.

## <a name="examples"></a>예

이 컴퓨터에 설정 된 현재 암호화 종류를 확인 합니다.
```
klist
```
도메인을 mit.contoso.com로 설정 합니다.
```
ksetup /domain mit.contoso.com
```
도메인에 대 한 암호화 유형 특성을 확인 합니다.
```
ksetup /getenctypeattr mit.contoso.com
```
도메인 mit.contoso.com에 대 한 암호화 유형 설정 특성을 제거 합니다.
```
ksetup /delenctypeattr mit.contoso.com
```

## <a name="additional-references"></a>추가 참조

-   [Klist](klist.md)
-   [Ksetup:domain](ksetup-domain.md)
-   [Ksetup:addenctypeattr](ksetup-addenctypeattr.md)
-   [Ksetup:setenctypeattr](ksetup-setenctypeattr.md)
-   [Ksetup:delenctypeattr](ksetup-delenctypeattr.md)
-   - [명령줄 구문 키](command-line-syntax-key.md)