---
title: reg 추가
description: '\* * * *에 대 한 Windows 명령 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d9ad143e-dc10-4e2e-a229-408393c40079
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: df59477c980169699dac897e36836e5226b6a0fa
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80836596"
---
# <a name="reg-add"></a>reg 추가


새 하위 키 또는 항목을 레지스트리에 추가합니다.

## <a name="syntax"></a>구문

```
reg add <KeyName> [{/v ValueName | /ve}] [/t DataType] [/s Separator] [/d Data] [/f]
```
이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

### <a name="parameters"></a>매개 변수

|      매개 변수      |                                                                                                                                                                                                                                                                   설명                                                                                                                                                                                                                                                                   |
|---------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| \<KeyName<em>></em> | 하위 키 또는 추가할 항목의 전체 경로 지정 합니다. 원격 컴퓨터를 지정 하려면 컴퓨터 이름을 *KeyName*의 일부로 \\\<ComputerName\) > \\형식으로 포함 합니다. ComputerName을 \\\\생략 하면 작업이 로컬 컴퓨터를 기본값으로 설정 됩니다. *KeyName* 유효한 루트 키를 포함 해야 합니다. 로컬 컴퓨터에 대 한 유효한 루트 키: HKLM, HKCU, HKCR, HKU, 및 HKCC 합니다. 원격 컴퓨터를 지정 하는 경우 올바른 루트 키가: HKLM 및 HKU 합니다. 레지스트리 키 이름에 공백이 포함 되어 있으면 키 이름을 따옴표로 묶으십시오. |
|   /v \<ValueName >   |                                                                                                                                                                                                                                지정된 된 하위 키 아래에 추가 될 레지스트리 항목의 이름을 지정 합니다.                                                                                                                                                                                                                                 |
|         /s 모든 하위         |                                                                                                                                                                                                                                레지스트리에 추가 된 레지스트리 항목이 null 값을 갖도록 지정 합니다.                                                                                                                                                                                                                                |
|     /t \<형식 >      |                                                                                                                                          레지스트리 항목에 대 한 형식을 지정합니다. *형식* 다음 중 하나 여야 합니다.</br>REG_SZ</br>REG_MULTI_SZ</br>REG_DWORD_BIG_ENDIAN</br>REG_DWORD</br>REG_BINARY</br>REG_DWORD_LITTLE_ENDIAN</br>REG_LINK</br>REG_FULL_RESOURCE_DESCRIPTOR</br>REG_EXPAND_SZ                                                                                                                                          |
|   /s \<구분 기호 >   |                                                                                                                                                              REG_MULTI_SZ 데이터 형식이 지정 되 고 하나 이상의 항목을 나열 해야 하는 경우 데이터의 여러 인스턴스를 구분 하는 데 사용할 문자를 지정 합니다. 지정 하지 않으면 기본 구분 기호는 **\0**합니다.                                                                                                                                                              |
|     /d \<데이터 >      |                                                                                                                                                                                                                                                 새 레지스트리 항목에 대 한 데이터를 지정합니다.                                                                                                                                                                                                                                                  |
|         /f          |                                                                                                                                                                                                                                           확인 메시지 없이 레지스트리 항목을 추가 합니다.                                                                                                                                                                                                                                           |
|         /?          |                                                                                                                                                                                                                                              에 대 한 도움말을 표시 **reg 추가** 명령 프롬프트입니다.                                                                                                                                                                                                                                               |

## <a name="remarks"></a>주의

-   이 작업을 하위 트리를 추가할 수 없습니다. 이 버전의 **reg** 하위 키를 추가 하는 경우 확인을 위해 묻지 않습니다.
-   다음 표에 대 한 반환 값은 **reg 추가** 작업 합니다.

| 값 | 설명 |
|-------|-------------|
|   0   |   성공   |
|   1   |   실패   |

-   REG_EXPAND_SZ 키 형식에 대해/d 매개 변수 내의 **%** 와 함께 캐럿 기호 ( **^** )를 사용 합니다.

## <a name="examples"></a><a name=BKMK_examples></a>예와

원격 컴퓨터 ABC에서 HKLM\Software\MyCo 키를 추가 하려면 다음을 입력 합니다.
```
REG ADD \\ABC\HKLM\Software\MyCo
```
명명 된 값을 가진 HKLM\Software\MyCo 레지스트리 항목을 추가 하려면 **데이터** 의 REG_BINARY와의 데이터 입력 **fe340ead**, 유형:
```
REG ADD HKLM\Software\MyCo /v Data /t REG_BINARY /d fe340ead
```
값 이름을 가진 HKLM\Software\MyCo 다중값된 레지스트리 항목을 추가 하려면 **MRU** 의 REG_MULTI_SZ와의 데이터 입력 **fax\0mail\0\0**, 유형:
```
REG ADD HKLM\Software\MyCo /v MRU /t REG_MULTI_SZ /d fax\0mail\0\0
```
값 이름을 가진 HKLM\Software\MyCo에 확장 된 레지스트리 항목을 추가 하려면 **경로** 의 REG_EXPAND_SZ와의 데이터 입력 **%systemroot%** , 유형:
```
REG ADD HKLM\Software\MyCo /v Path /t REG_EXPAND_SZ /d ^%systemroot^%
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
