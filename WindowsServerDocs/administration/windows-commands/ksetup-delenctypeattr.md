---
title: 'ksetup: delenctypeattr'
description: '\* * * *에 대 한 Windows 명령 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4fc25ef3-e271-4229-a712-72c507df55aa
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c650b973ac34e28394d5b6ec38142a058ad76338
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80841766"
---
# <a name="ksetupdelenctypeattr"></a>ksetup: delenctypeattr



도메인에 대 한 암호화 유형 특성을 제거 합니다. 이 명령을 사용할 수 있는 방법을의 예 참조 [예제](#BKMK_Examples)합니다.

## <a name="syntax"></a>구문

```
ksetup /delenctypeattr <DomainName> 
```

#### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<DomainName >|연결을 설정 하려는 도메인 이름입니다. 정규화 된 도메인 이름 또는 corp.contoso.com 또는 contoso와 같은 간단한 형식의 이름을 사용 합니다.|

## <a name="remarks"></a>주의

Kerberos TGT (티켓 허용 티켓) 및 세션 키의 암호화 유형을 보려면 **klist** 명령을 실행 하 고 출력을 확인 합니다.

성공 또는 실패 완료 시 상태 메시지가 표시 됩니다.

연결 하 고 사용 하려는 도메인을 설정 하려면 **ksetup/domain \<DomainName >** 명령을 실행 합니다.

## <a name="examples"></a><a name=BKMK_Examples></a>예와

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