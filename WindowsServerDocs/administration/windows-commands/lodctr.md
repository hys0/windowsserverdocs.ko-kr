---
title: lodctr
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5a849abd-6b31-4833-bc8a-306c05eca29a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b67c11b24013adb911309ab2ea9bdbfdfc3408da
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66437896"
---
# <a name="lodctr"></a>lodctr

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

등록 성능 카운터 이름 및 레지스트리 설정을 파일에 저장 하 고, 신뢰할 수 있는 서비스를 지정할 수 있습니다.
## <a name="syntax"></a>구문
```
lodctr <filename> [/s:<filename>] [/r:<filename>] [/t:<servicename>]
```
### <a name="parameters"></a>매개 변수

|    매개 변수     |                                                                                                                                         설명                                                                                                                                          |
|------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    <filename>    |                                                                                          성능 카운터 이름 설정 및 초기화 파일 파일 이름에에서 제공 된 설명 텍스트를 등록 합니다.                                                                                          |
|  /s:<filename>   |                                                                                                       저장 성능 카운터 레지스트리 설정 및 설명 텍스트 파일에 <filename>합니다.                                                                                                       |
|        /r        |                                현재 레지스트리 설정과 관련 된 캐시 된 성능 파일에서 카운터 레지스트리 설정 및 설명 텍스트를 복원 합니다.<br /><br />이 옵션은 Windows Server 2003 운영 체제 에서만 사용할 수 있습니다.                                |
|  /r:<filename>   | 복원 작업 성능 카운터 레지스트리 설정 및 설명 텍스트 파일에서 <filename>합니다. **경고:** 사용 하는 경우는 **lodctr /r** 명령을 모든 성능 카운터 레지스트리 설정을 덮어쓰게 되며 지정 된 파일에 정의 된 구성을 사용 하 여 대체 하 여 텍스트를 설명 합니다. |
| /t:<servicename> |                                                                                                                       해당 서비스를 나타내는 <servicename> 신뢰할 수 있습니다.                                                                                                                       |
|        /?        |                                                                                                                             명령 프롬프트에 도움말을 표시합니다.                                                                                                                             |

## <a name="remarks"></a>설명
텍스트가 주위에 따옴표를 사용 하 여 사용자가 제공 하는 정보에 공백이 포함 되 면 (예를 들어 "<filename>").
## <a name="BKMK_Examples"></a>예제
현재 성능 레지스트리 설정을 저장 하 고 파일에 대 한 설명 텍스트에 대처 하려면 **성능 backup1.txt**:
```
lodctr /s:"perf backup1.txt"
```
## <a name="additional-references"></a>추가 참조
-   [명령줄 구문 키](command-line-syntax-key.md)

