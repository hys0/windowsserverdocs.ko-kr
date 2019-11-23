---
title: reg 비교
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 177dc6a3-034e-4846-a394-330d03c14e0b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bfccc1f64b0113967a52e3ac0516d800cfea3532
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71384721"
---
# <a name="reg-compare"></a>reg 비교



비교 하 여 레지스트리 하위 키 또는 항목을 지정 합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
reg compare <KeyName1> <KeyName2> [{/v ValueName | /ve}] [{/oa | /od | /os | on}] [/s]
```

## <a name="parameters"></a>매개 변수

|    매개 변수    |                                                                                                                                                                                                                                                                                          설명                                                                                                                                                                                                                                                                                           |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   \<KeyName1 >   |                                                               비교할 첫 번째 하위 키의 전체 경로 지정 합니다. 원격 컴퓨터를 지정 하려면 컴퓨터 이름을 *KeyName*의 일부로 \\\\ComputerName\) 형식으로 포함 합니다. ComputerName을 \\\\생략 하면 작업이 로컬 컴퓨터를 기본값으로 설정 됩니다. *KeyName* 유효한 루트 키를 포함 해야 합니다. 로컬 컴퓨터에 대 한 유효한 루트 키: HKLM, HKCU, HKCR, HKU, 및 HKCC 합니다. 원격 컴퓨터를 지정 하는 경우 올바른 루트 키가: HKLM 및 HKU 합니다.                                                                |
|   \<KeyName2 >   | 비교할 두 번째 하위 키의 전체 경로 지정 합니다. 원격 컴퓨터를 지정 하려면 컴퓨터 이름을 *KeyName*의 일부로 \\\\ComputerName\) 형식으로 포함 합니다. ComputerName을 \\\\생략 하면 작업이 로컬 컴퓨터를 기본값으로 설정 됩니다. 에 컴퓨터 이름만 지정 *KeyName2* 에 지정 된 하위 키에 대 한 경로 사용 하 여 작업을 발생 시킨 *KeyName1*합니다. *KeyName* 유효한 루트 키를 포함 해야 합니다. 로컬 컴퓨터에 대 한 유효한 루트 키: HKLM, HKCU, HKCR, HKU, 및 HKCC 합니다. 원격 컴퓨터를 지정 하는 경우 올바른 루트 키가: HKLM 및 HKU 합니다. |
| /v \<ValueName > |                                                                                                                                                                                                                                                                     하위 키 아래 비교할 값 이름을 지정 합니다.                                                                                                                                                                                                                                                                      |
|       /s 모든 하위       |                                                                                                                                                                                                                                                         Null 값 이름이 있는 항목만 비교 되어야 함을 지정 합니다.                                                                                                                                                                                                                                                         |
|      [{/oa      |                                                                                                                                                                                                                                                                                              /od                                                                                                                                                                                                                                                                                               |
|       /oa       |                                                                                                                                                                                                                                             모든 차이 일치 하는 항목 표시 되도록 지정 합니다. 기본적으로 변경 된 사항만 나열 됩니다.                                                                                                                                                                                                                                             |
|       /od       |                                                                                                                                                                                                                                                          차이만 표시 되도록 지정 합니다. 이는 기본 동작입니다.                                                                                                                                                                                                                                                          |
|       /os       |                                                                                                                                                                                                                                                    일치만 표시 되도록 지정 합니다. 기본적으로 변경 된 사항만 나열 됩니다.                                                                                                                                                                                                                                                     |
|       /on       |                                                                                                                                                                                                                                                       아무 것도 표시 되도록 지정 합니다. 기본적으로 변경 된 사항만 나열 됩니다.                                                                                                                                                                                                                                                        |
|       /s        |                                                                                                                                                                                                                                                                         모든 하위 키와 항목 재귀적으로 비교합니다.                                                                                                                                                                                                                                                                          |
|       /?        |                                                                                                                                                                                                                                                                    에 대 한 도움말을 표시 **reg 비교** 명령 프롬프트입니다.                                                                                                                                                                                                                                                                    |

## <a name="remarks"></a>설명

다음 표에서 반환 값에 대 한 **reg 비교**합니다.

|값|설명|
|-----|-----------|
|0|비교는 성공 하 고 결과 동일 합니다.|
|1|비교에 실패 했습니다.|
|2|비교 성공적이 고 차이 찾았습니다.|

다음 표에서 결과에 표시 된 기호를 나열 합니다.

|Symbol|설명|
|------|-----------|
|=|*KeyName1* 데이터 같으면 *KeyName2* 데이터입니다.|
|<|*KeyName1* 데이터는 보다 작은 *KeyName2* 데이터입니다.|
|>|*KeyName1* 데이터 보다 크면 *KeyName2* 데이터입니다.|

## <a name="BKMK_examples"></a>예와

**MyApp** 키 아래의 모든 값을 **Savemyapp**키의 모든 값과 비교 하려면 다음을 입력 합니다.

REG COMPARE HKLM\Software\MyCo\MyApp HKLM\Software\MyCo\SaveMyApp

**MyCo** 키 아래에 있는 버전의 값과 키 **MyCo1**의 버전 값을 비교 하려면 다음을 입력 합니다.

REG COMPARE HKLM\Software\MyCo HKLM\Software\MyCo1/v Version

HKLM\Software\MyCo 아래의 모든 하위 키와 값을 로컬 컴퓨터의 HKLM\Software\MyCo에 있는 모든 하위 키 및 값으로 지정 하 여 해당 컴퓨터의 하위 키 및 값을 비교 하려면 다음을 입력 합니다.

REG COMPARE \\\\ZODIAC\HKLM\Software\MyCo \\\\. /s

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)