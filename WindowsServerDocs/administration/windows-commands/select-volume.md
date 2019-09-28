---
title: select volume
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5d70d776-80ad-4f20-8288-a7997fb1df28
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cc981131c8de2dc4534e390645ef45c39a7b02ab
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71371057"
---
# <a name="select-volume"></a>select volume

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

지정 된 볼륨을 선택 하 고 포커스를 이동 합니다. 이 명령은 현재 선택된 된 디스크에 포커스를가지고 있는 볼륨을 표시 하려면 데도 사용할 수 있습니다.  
  
  
  
## <a name="syntax"></a>구문  
  
```  
select volume={<n>|<d>}  
```  
  
## <a name="parameters"></a>매개 변수  
  
| 매개 변수 |                                                                               설명                                                                                |
|-----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    <n>    | 포커스를 받을 때 변환할 볼륨의 수입니다. 사용 하 여 현재 선택 된 디스크에 모든 볼륨에 대 한 숫자를 볼 수는 **볼륨 목록** DiskPart 명령을 합니다. |
|    <d>    |                                                 포커스를 받을 때 변환할 볼륨의 드라이브 문자 또는 탑재 지점 경로입니다.                                                 |
  
## <a name="remarks"></a>설명  
  
-   볼륨이 지정 되지 않은 경우이 명령은 현재 선택 된 디스크에 포커스가 있는 볼륨을 표시 합니다.  
  
-   기본 디스크에 볼륨을 선택 하면 또한 포커스를 해당 파티션에 합니다.  
  
-   해당 하는 파티션이 있는 볼륨을 선택 하면 파티션이 자동으로 선택 됩니다.  
  
-   파티션이 해당 볼륨으로 선택 된 경우 볼륨이 자동으로 선택 됩니다.  
  
## <a name="BKMK_examples"></a>예와  
포커스를 볼륨 2 입력 합니다.  
  
```  
select volume=2  
```  
  
C 드라이브에 포커스를 이동, 다음을 입력 합니다.  
  
```  
select volume=c  
```  
  
포커스를 이동 "mountpath" 라는 폴더에 탑재 된 볼륨에을 입력 합니다.  
  
```  
select volume=c:\mountpath  
```  
  
현재 선택된 된 디스크에 포커스를가지고 있는 볼륨을 표시 하려면 다음을 입력 합니다.  
  
```  
select volume  
```  
  
#### <a name="additional-references"></a>추가 참조  
[명령줄 구문 키](command-line-syntax-key.md)  
  

  

