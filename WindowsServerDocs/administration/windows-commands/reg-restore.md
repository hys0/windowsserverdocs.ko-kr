---
title: reg 복원
description: '* * * *에 대 한 참조 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a51f1c0c-969b-4b76-930a-c8bb14dea26e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4d490f99f032b38c8bbbe9352b8571b4a85202e1
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722516"
---
# <a name="reg-restore"></a>reg 복원



쓰기 저장 된 하위 키와 항목 레지스트리를 백업합니다.



## <a name="syntax"></a>구문

```
Reg restore <KeyName> <FileName>
```

### <a name="parameters"></a>매개 변수

|매개 변수|Description|
|---------|-----------|
|\<KeyName>|복원 해야 하는 하위 키의 전체 경로 지정 합니다. 복원 작업이 로컬 컴퓨터 에서만 작동합니다. 키 이름에는 유효한 루트 키를 포함 해야 합니다. 유효한 루트 키가: HKLM, HKCU, HKCR, HKU, 및 HKCC 합니다.|
|\<파일 이름>|콘텐츠를 레지스트리에 쓸 수 있는 파일의 경로 이름을 지정 합니다. 으로이 파일을 사전에 생성 되어야 합니다는 **reg 저장** .hiv 확장을 사용 하 여 작업 합니다.|
|/?|에 대 한 도움말을 표시 **reg 복원** 명령 프롬프트입니다.|

## <a name="remarks"></a>설명

-   레지스트리 항목을 편집 하기 전에 저장 된 부모 하위 키의 **reg 저장** 작업 합니다. 편집에 실패 하면 복원으로 원래 하위 키의 **reg 복원** 작업 합니다.
-   다음 표에 대 한 반환 값은 **reg 복원** 작업 합니다.

|값|설명|
|-----|-----------|
|0|Success|
|1|실패|

## <a name="examples"></a>예

HKLM\Software\Microsoft\ResKit 키로 NTRKBkUp.hiv 라는 파일을 복원 하는 키의 기존 내용을 덮어씁니다 다음을 입력 합니다.
```
REG RESTORE HKLM\Software\Microsoft\ResKit NTRKBkUp.hiv
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)