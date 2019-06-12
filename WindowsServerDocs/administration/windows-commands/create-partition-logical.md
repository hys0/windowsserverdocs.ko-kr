---
title: 파티션 논리 만들기
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1f59b79a-d690-4d0e-ad38-40df5a0ce38e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d3af60aed6c8305e410c6ebfba3cf2e006034ad7
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66434157"
---
# <a name="create-partition-logical"></a>파티션 논리 만들기

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

기존 확장 파티션의 논리 파티션을 만듭니다. 마스터 부트 레코드에만이 명령을 사용할 수 있습니다 \(MBR\) 디스크.  
  
  
  
## <a name="syntax"></a>구문  
  
```  
create partition logical [size=<n>] [offset=<n>] [align=<n>] [noerr]  
```  
  
## <a name="parameters"></a>매개 변수  
  
|  매개 변수  |                                                                                                                                                                                                                       설명                                                                                                                                                                                                                        |
|-------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  size\=<n>  |                                                                                                              (메가바이트 단위)는 논리 파티션에의 크기를 지정 \(MB\), 확장 된 파티션을 보다 작은 해야 합니다. 크기를 지정 하는 경우 파티션을 확장 파티션의 가능한 공간이 없을 때까지 계속 합니다.                                                                                                               |
| offset\=<n> | (킬로바이트)에서 오프셋을 지정 \(KB\), 파티션을 만들 때에 있습니다. 오프셋 반올림을 완전히 사용 되는 모든 실린더 크기를 채웁니다. 오프셋이, 파티션은 저장 하는 데 충분히 큰 첫 번째 디스크에에서 배치 됩니다. 파티션에 지정 된 수 만큼 바이트에서 길이가 **크기\=<n>** 합니다. 논리 파티션에 대 한 크기를 지정 하면 확장된 파티션의 보다 작아야 합니다. |
| align\=<n>  |                                                                                     모든 볼륨 또는 파티션 범위에 있는 가장 가까운 맞춤 경계선을 맞춥니다. 일반적으로 하드웨어 RAID 논리 단위 번호와 사용 \(LUN\) 성능을 향상 시키기 위해 배열입니다.  <n> (킬로바이트)입니다 \(KB\) 가장 가까운 맞춤 경계선을 디스크의 시작 부분에서.                                                                                      |
|    noerr    |                                                                                                                           만 스크립팅 합니다. 오류가 발생 하면 오류가 발생 하지 않은 경우에 따라 명령을 처리 하도록 DiskPart 계속 합니다. 이 매개 변수를 크기는 오류 코드를 수행 합니다.                                                                                                                           |
  
## <a name="remarks"></a>설명  
  
-   경우는 **크기** 하 고 **오프셋** 매개 변수가 지정 되지 않은, 논리 파티션 확장 파티션에서 사용할 수 있는 가장 큰 디스크 범위에 생성 됩니다.  
  
-   파티션이 만들어지면 포커스는 자동으로 새 논리 파티션으로 이동 합니다.  
  
-   이 작업을 수행 하려면 기본 MBR 디스크를 선택 해야 합니다. 사용 된 **디스크 선택** 디스크를 선택 하 고 포커스를 이동 하는 명령입니다.  
  
## <a name="BKMK_examples"></a>예제  
선택된 된 디스크의 확장 파티션의 크기를 메가바이트 1000 논리적 파티션을 만들려면 다음을 입력 합니다.  
  
```  
create partition logical size=1000  
```  
  
#### <a name="additional-references"></a>추가 참조  
[명령줄 구문 키](command-line-syntax-key.md)  
  

  

