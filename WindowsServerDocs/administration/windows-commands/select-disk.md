---
title: select disk
description: '\* * * *에 대 한 Windows 명령 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a0da614b-09d9-433b-b4eb-9127f84431cb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 441e680f0a705255f6eba8c4a16db4a623e50b6b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80834816"
---
# <a name="select-disk"></a>select disk

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

지정 된 디스크를 선택 하 고 포커스를 이동 합니다.  
  
  
  
## <a name="syntax"></a>구문  
  
```  
select disk={ <n> | <disk path> | system | next }  
```  
  
> [!NOTE]  
> **<disk path>** , **시스템**및 **다음** 매개 변수는 windows 7 및 windows Server 2008 r 2 에서만 사용할 수 있습니다.  
  
### <a name="parameters"></a>매개 변수  
  
|  매개 변수  |                                                                                                                                                                                                            설명                                                                                                                                                                                                            |
|-------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     <n>     | 포커스를 받을 디스크의 번호를 지정 합니다. 사용 하 여 컴퓨터에 모든 디스크에 대 한 숫자를 볼 수는 **목록 디스크** DiskPart 명령을 합니다. **참고:** 시스템 여러 디스크를 구성할 때 사용 하지 않는 **디스크 선택\=0** 시스템 디스크를 지정 합니다. 컴퓨터를 다시 부팅 하 고 동일한 디스크 구성으로 서로 다른 컴퓨터에서 다른 디스크 번호를 가질 수 있습니다 디스크 번호를 다시 할당할 수 있습니다. |
| <disk path> |                                                                                                                 포커스를 받을 디스크의 위치를 지정 합니다 (예: **PCIROOT\(0\)\#PCI\(0F02\)\#atA\(C00T00L00\)** ). 디스크의 위치 경로 보려면 선택 하 고 입력 한 다음 **세부 디스크**합니다.                                                                                                                  |
|   시스템    |                                 BIOS 컴퓨터에 포커스를 받을 해당 디스크 0을 지정 합니다. EFI 컴퓨터의 경우 EFI 시스템 파티션을 포함 하는 디스크에 \(ESP\) 사용 되는 현재 부팅 포커스를 받을 있습니다. EFI 컴퓨터에서 ESP가 없거나, ESP가 두 개 이상 있거나, Windows PE\)Windows 사전 설치 환경 \(컴퓨터가 부팅 되는 경우 명령이 실패 합니다.                                  |
|    next     |                                                                                                                                     디스크를 선택 하면이 명령은 디스크 목록에 있는 모든 디스크를 반복 합니다. 이 명령을 실행 하는 경우 다음 디스크 목록에 포커스를 받게 됩니다.                                                                                                                                      |
  
## <a name="examples"></a><a name=BKMK_examples></a>예와  
1 디스크에 포커스를 이동, 다음을 입력 합니다.  
  
```  
select disk=1  
```  
  
해당 위치 경로 사용 하 여 디스크를 선택 하려면 다음을 입력 합니다.  
  
```  
select disk=PCIROOT(0)#PCI(0100)#atA(C00T00L01)  
```  
  
시스템 디스크에 포커스를 이동, 다음을 입력 합니다.  
  
```  
select disk=system  
```  
  
포커스를 이동 다음 디스크를 컴퓨터에를 입력 합니다.  
  
```  
select disk=next  
```  
  
## <a name="additional-references"></a>추가 참조  
- [명령줄 구문 키](command-line-syntax-key.md)  
  

  

