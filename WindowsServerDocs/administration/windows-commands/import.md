---
title: diskshadow 가져오기
description: 로드 된 메타 데이터 파일에서 시스템으로 전송 가능한 섀도 복사본을 가져오는 가져오기 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7bd78d76-0560-4d47-944c-fe960be2c10b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ab1c3c6d324cec939a2529191cbc8ce40165b807
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85924448"
---
# <a name="import-diskshadow"></a>가져오기 (diskshadow)

시스템에 로드 된 메타 데이터 파일에서 전송 가능한 섀도 복사본을 가져옵니다.

> 중요 한 이 명령을 사용 하려면 먼저 [메타 데이터 로드 명령을](load-metadata.md) 사용 하 여 DiskShadow 메타 데이터 파일을 로드 해야 합니다.

## <a name="syntax"></a>구문

```
import
```

#### <a name="remarks"></a>설명

- 전송 가능한 섀도 복사본은 시스템에 즉시 저장 되지 않습니다. 세부 정보는 DiskShadow에서 자동으로 요청 하 고 작업 디렉터리에.cab 메타 데이터 파일에 저장 된 백업 구성 요소 문서 XML 파일을에 저장 됩니다. [Set metadata 명령을](set-metadata.md) 사용 하 여이 XML 파일의 경로와 이름을 변경 합니다.

## <a name="examples"></a>예

다음은의 사용을 보여 주는 샘플 DiskShadow 스크립트는 **가져올** 명령:

```
#Sample DiskShadow script demonstrating IMPORT
SET CONTEXT PERSISTENT
SET CONTEXT TRANSPORTABLE
SET METADATA transHWshadow_p.cab
#P: is the volume supported by the Hardware Shadow Copy provider
ADD VOLUME P:
CREATE
END BACKUP
#The (transportable) shadow copy is not in the system yet.
#You can reset or exit now if you wish.

LOAD METADATA transHWshadow_p.cab
IMPORT
#The shadow copy will now be loaded into the system.
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [diskshadow 명령](diskshadow.md)