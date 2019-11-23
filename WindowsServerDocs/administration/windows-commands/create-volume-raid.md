---
title: 볼륨 raid 만들기
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9f257950-9240-4d5f-9537-8ad653d48ebf
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5a3c13cb5b78ae3e771b461a35a7130a48e7ec01
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71378857"
---
# <a name="create-volume-raid"></a>볼륨 raid 만들기

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

3 개 이상의 지정 된 동적 디스크를 사용 하 여 RAID\-5 볼륨을 만듭니다.  
  
> [!IMPORTANT]  
> 이 DiskPart 명령을 Windows Vista의 모든 버전에서 사용할 수 없는 경우  
  
  
  
## <a name="syntax"></a>구문  
  
```  
create volume raid [size=<n>] disk=<n>,<n>,<n>[,<n>,...] [align=<n>] [noerr]  
```  
  
## <a name="parameters"></a>매개 변수  
  
|           매개 변수           |                                                                                                                                                                                                                                              설명                                                                                                                                                                                                                                              |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|           크기\=<n>           | 메가바이트 단위로 디스크 공간의 크기 \(MB\), 각 디스크에 볼륨이 차지할입니다. 크기를 지정할 경우 가장 큰 가능한 RAID\-5 볼륨이 만들어집니다. RAID에 대 한 크기를 결정 하는 가장 작은 사용 가능한 인접 한 여유 공간이 디스크\-5 볼륨과 동일한 공간의 각 디스크에서 할당 됩니다. 실제 RAID에 사용할 수 있는 디스크 공간의 양을\-5 볼륨 보다 작으면 결합 된 디스크 공간의 필요 하기 때문에 일부 디스크 공간이 패리티에 있습니다. |
| disk\=<n>,<n>,<n>\[<n>,...\] |                                                                                                                                               동적 디스크는 RAID를 만드는 데 기반이\-5 볼륨입니다. RAID를 만들기 위해 세 개 이상의 동적 디스크가 필요\-5 볼륨입니다. **\=<n>크기** 에 해당 하는 공간의 크기는 각 디스크에 할당 됩니다.                                                                                                                                                |
|          \=<n> 맞춤           |                                                                                                                   모든 볼륨 범위에 있는 가장 가까운 맞춤 경계선을 맞춥니다. 일반적으로 하드웨어 RAID 논리 단위 번호와 사용 \(LUN\) 성능을 향상 시키기 위해 배열입니다. *n* 는 킬로바이트의 수는 \(KB\) 가장 가까운 맞춤 경계선을 디스크의 시작 부분에서.                                                                                                                   |
|             noerr             |                                                                                                                                                 스크립팅 전용입니다. 오류가 발생 하면 오류가 발생 하지 않은 경우에 따라 명령을 처리 하도록 DiskPart 계속 합니다. 이 매개 변수를 크기는 오류 코드를 수행 합니다.                                                                                                                                                  |
  
## <a name="remarks"></a>설명  
  
-   볼륨을 만든 후 포커스는 자동으로 새 볼륨으로 이동 합니다.  
  
## <a name="BKMK_examples"></a>예와  
RAID를 만드는\-1000 메가바이트 1, 2 및 3, 유형 디스크를 사용 하 여 크기의 5 개 볼륨:  
  
```  
create volume raid size=1000 disk=1,2,3  
```  
  
#### <a name="additional-references"></a>추가 참조  
[명령줄 구문 키](command-line-syntax-key.md)  
  

  

