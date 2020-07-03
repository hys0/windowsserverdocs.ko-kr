---
title: 'secedit: 유효성 검사'
description: '* * * *에 대 한 참조 문서'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9fb06354-f55a-4ca4-9fbc-9a872eb9b9cf
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7f2da0792768a6b6d6113842614bc6f93c258822
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85935975"
---
# <a name="seceditvalidate"></a>secedit: 유효성 검사



보안 템플릿 (.inf 파일)에 저장 된 보안 설정의 유효성을 검사 합니다.

## <a name="syntax"></a>구문

```
Secedit /validate <configuration file name>

```

#### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|구성 파일 이름|필수 요소.</br>유효성을 검사할 보안 서식 파일에 대 한 경로 파일 이름을 지정 합니다.|

## <a name="remarks"></a>설명

보안 템플릿 유효성을 검사 하는 경우 도움이 됩니다 하나 손상 되거나 부적절 하 게 설정 합니다.

잘못 된 보안 템플릿을 적용 되지 않습니다.

로그 파일이 업데이트 되지 않습니다.

Windows Server 2008에서 `Secedit /refreshpolicy` 바뀌었습니다 `gpupdate`합니다. 보안 설정을 새로 고치는 방법에 대 한 자세한 내용은 [Gpupdate](gpupdate.md)합니다.

## <a name="examples"></a>예

보안 템플릿 롤백을 수행 된 후 하는지 확인 하려면 rollback inf 파일, secRBKcontoso.inf, 유효 합니다.
```
Secedit /validate secRBKcontoso.inf
```

## <a name="additional-references"></a>추가 참조

-   [Secedit:generaterollback](secedit-generaterollback.md)
-   [Secedit](secedit.md)
- [명령줄 구문 키](command-line-syntax-key.md)