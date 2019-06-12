---
title: clean
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9bbe6fd3-e07e-487b-9035-910957a1d326
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cd5eb2ec1bde4523eb6f0f919e09b9711b2654fb
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66434322"
---
# <a name="clean"></a>clean

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Clean Diskpart 명령을 모든 파티션 또는 볼륨 포커스가 있는 디스크에서 서식이 제거 합니다.
## <a name="syntax"></a>구문
```
clean [all]
```
## <a name="parameters"></a>매개 변수

| 매개 변수 |                                                        설명                                                        |
|-----------|---------------------------------------------------------------------------------------------------------------------------|
|    모든    | 각 섹터 디스크에서 디스크에 포함 된 모든 데이터를 완전히 삭제를 0으로 설정 되어 있는지를 지정 합니다. |

## <a name="remarks"></a>설명
- 마스터 부트 레코드 (MBR) 디스크에 MBR 파티션 정보와 숨겨진된 섹터 정보와 덮어쓰여집니다.
- GUID 파티션 테이블 (gpt) 디스크에 파티션 정보를 보호 하는 MBR을 포함 하 여 gpt은 덮어씁니다. 숨겨진된 섹터 정보가 없는 합니다.
- 이 작업을 수행 하려면 디스크를 선택 해야 합니다. 사용 된 **디스크 선택** 디스크를 선택 하 고 포커스를 이동 하는 명령입니다.
  ## <a name="BKMK_examples"></a>예제
  선택된 된 디스크에서 모든 서식을 제거 하려면 다음을 입력 합니다.
  ```
  clean
  ```

[Clear-Disk](https://technet.microsoft.com/library/hh848661.aspx)
