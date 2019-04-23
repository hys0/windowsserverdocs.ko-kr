---
title: 'Secedit: 유효성 검사'
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9fb06354-f55a-4ca4-9fbc-9a872eb9b9cf
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cca64f6b2904ed11f6b45e316c8e4da0093c373e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59877914"
---
# <a name="seceditvalidate"></a>Secedit: 유효성 검사



보안 템플릿 (.inf 파일)에 저장 된 보안 설정의 유효성을 검사 합니다. 이 명령을 사용할 수 있는 방법을의 예 참조 [예제](#BKMK_Examples)합니다.

## <a name="syntax"></a>구문

```
Secedit /validate <configuration file name>  

```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|구성 파일 이름|필수 사항입니다.</br>유효성을 검사할 보안 서식 파일에 대 한 경로 파일 이름을 지정 합니다.|

## <a name="remarks"></a>설명

보안 템플릿 유효성을 검사 하는 경우 도움이 됩니다 하나 손상 되거나 부적절 하 게 설정 합니다.

잘못 된 보안 템플릿을 적용 되지 않습니다.

로그 파일이 업데이트 되지 않습니다.

Windows Server 2008에서 `Secedit /refreshpolicy` 바뀌었습니다 `gpupdate`합니다. 보안 설정을 새로 고치는 방법에 대 한 자세한 내용은 [Gpupdate](gpupdate.md)합니다.

## <a name="BKMK_Examples"></a>예제

보안 템플릿 롤백을 수행 된 후 하는지 확인 하려면 rollback inf 파일, secRBKcontoso.inf, 유효 합니다.
```
Secedit /validate secRBKcontoso.inf
```

#### <a name="additional-references"></a>추가 참조

-   [Secedit:generaterollback](secedit-generaterollback.md)
-   [secedit](secedit.md)
-   [명령줄 구문 키](command-line-syntax-key.md)