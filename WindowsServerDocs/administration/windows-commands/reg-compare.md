---
title: reg 비교
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 83bb010af4bfbf38ce41001d6a6001d5a3996090
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66441924"
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
|   \<KeyName1>   |                                                               비교할 첫 번째 하위 키의 전체 경로 지정 합니다. 원격 컴퓨터를 지정 하려면 컴퓨터 이름을 포함 합니다 (형식에서 \\ \\ComputerName\) 의 일부로 합니다 *KeyName*합니다. 생략 \\ \\ComputerName\ 하면 로컬 컴퓨터에 기본 작업이 있습니다. *KeyName* 유효한 루트 키를 포함 해야 합니다. 로컬 컴퓨터에 대 한 유효한 루트 키 다음과 같습니다. HKLM, HKCU, HKCR, HKU, and HKCC. 원격 컴퓨터를 지정 하는 경우 유효한 루트 키 다음과 같습니다. HKLM 및 HKU 합니다.                                                                |
|   \<KeyName2>   | 비교할 두 번째 하위 키의 전체 경로 지정 합니다. 원격 컴퓨터를 지정 하려면 컴퓨터 이름을 포함 합니다 (형식에서 \\ \\ComputerName\) 의 일부로 합니다 *KeyName*합니다. 생략 \\ \\ComputerName\ 하면 로컬 컴퓨터에 기본 작업이 있습니다. 에 컴퓨터 이름만 지정 *KeyName2* 에 지정 된 하위 키에 대 한 경로 사용 하 여 작업을 발생 시킨 *KeyName1*합니다. *KeyName* 유효한 루트 키를 포함 해야 합니다. 로컬 컴퓨터에 대 한 유효한 루트 키 다음과 같습니다. HKLM, HKCU, HKCR, HKU, and HKCC. 원격 컴퓨터를 지정 하는 경우 유효한 루트 키 다음과 같습니다. HKLM 및 HKU 합니다. |
| /v \<ValueName> |                                                                                                                                                                                                                                                                     하위 키 아래 비교할 값 이름을 지정 합니다.                                                                                                                                                                                                                                                                      |
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

|값|Description|
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

## <a name="BKMK_examples"></a>예제

키 아래의 모든 값을 비교할 **MyApp** 키 아래의 모든 값을 사용 하 여 **SaveMyApp**, 유형:

REG COMPARE HKLM\Software\MyCo\MyApp HKLM\Software\MyCo\SaveMyApp

키 버전에 대 한 값을 비교 하려면 **MyCo** 키 아래에서 버전에 대 한 값 **MyCo1**, 유형:

REG COMPARE HKLM\Software\MyCo HKLM\Software\MyCo1 /v Version

모든 하위 키와 모든 하위 키와 로컬 컴퓨터에서 HKLM\Software\MyCo 아래의 값을 사용 하 여 육십갑자 이라는 컴퓨터에서 HKLM\Software\MyCo 아래의 값을 비교 하려면 다음을 입력 합니다.

REG COMPARE \\\\ZODIAC\HKLM\Software\MyCo \\\\. /s

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)