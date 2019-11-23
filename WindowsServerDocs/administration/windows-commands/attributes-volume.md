---
title: 특성 볼륨
description: '**특성 볼륨** 에 대 한 Windows 명령 항목-볼륨의 특성을 표시, 설정 또는 지웁니다.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e40e8284-3d57-4de8-a46c-e4ade34a0d53
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 225a10307123763d1a024fcc08fbae536fd0b5df
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382576"
---
# <a name="attributes-volume"></a>특성 볼륨

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

표시 설정 하거나 볼륨의 특성을 지웁니다.  
  
  
  
## <a name="syntax"></a>구문  
  
```  
attributes volume [{set | clear}] [{hidden | readonly | nodefaultdriveletter | shadowcopy}] [noerr]  
```  
  
## <a name="parameters"></a>매개 변수  
  
|매개 변수|설명|  
|-------|--------|  
|집합|포커스가 있는 볼륨의 지정된 된 특성을 설정합니다.|  
|clear|포커스가 있는 볼륨의 지정된 된 특성을 지웁니다.|  
|읽기 전용|볼륨이 읽기 지정\-만 합니다.|  
|숨김|볼륨 숨겨지는지를 지정 합니다.|  
|nodefaultdriveletter|볼륨 기본적으로 드라이브 문자를 할당 하지 않는 것을 지정 합니다.|  
|섀도 복사본|볼륨 섀도 복사본 볼륨 임을 지정 합니다.|  
|noerr|스크립팅 전용입니다. 오류가 발생 하면 오류가 발생 하지 않은 경우에 따라 명령을 처리 하도록 DiskPart 계속 합니다. 이 매개 변수를 크기는 오류 코드를 수행 합니다.|  
  
## <a name="remarks"></a>설명  
  
-   마스터 부트 레코드에서 \(MBR\) 디스크는 **숨겨진**, **readonly**, 및 **nodefaultdriveletter** 매개 변수는 디스크에 있는 모든 볼륨에 적용 합니다.  
  
-   기본 GUID 파티션 테이블 \(gpt\) 디스크 및 동적 MBR 및 gpt 디스크에서 **hidden**, **readonly**및 **nodefaultdriveletter** 매개 변수는 선택한 볼륨에만 적용 됩니다.  
  
-   볼륨을 선택 해야는 **볼륨 특성** 명령을 성공적으로 합니다. 사용 하 여는 **볼륨 선택** 볼륨을 선택 하 고 포커스를 이동 하는 명령입니다.  
  
## <a name="BKMK_examples"></a>예와  
선택된 된 볼륨의 현재 속성을 표시 하려면 다음을 입력 합니다.  
  
```  
attributes volume  
```  
  
선택한 볼륨 숨겨져 있고 읽기로 설정 하려면\-만 입력 합니다.  
  
```  
attributes volume set hidden readonly  
```  
  
숨겨진 및 읽기를 제거 하려면\-특성만 선택된 된 볼륨을 입력 합니다.  
  
```  
attributes volume clear hidden readonly  
```  
  
#### <a name="additional-references"></a>추가 참조  
[명령줄 구문 키](command-line-syntax-key.md)  
  

  

