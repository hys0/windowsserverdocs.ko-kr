---
title: unlodctr
description: Unlodctr에 대 한 Windows 명령 항목-시스템 레지스트리에서 서비스 또는 장치 드라이버에 대 한 성능 카운터 이름 및 설명 텍스트를 제거 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fc8aa6f0-c1d9-47ea-937a-28152148e774
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fe7fc3c9eafefd59a5daab625e3af06b6addd292
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80832260"
---
# <a name="unlodctr"></a>unlodctr

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

시스템 레지스트리에서 서비스 또는 장치 드라이버에 대 한 **성능 카운터** 이름 및 **설명** 텍스트를 제거 합니다.   

## <a name="syntax"></a>구문  
```  
Unlodctr <DriverName>   
```  
#### <a name="parameters"></a>매개 변수  
|매개 변수|설명|  
|-------|--------|  
|\<DriverName >|Windows Server 2003 레지스트리에서 드라이버 또는 서비스 <DriverName>에 대 한 성능 카운터 이름 설정 및 설명 텍스트를 제거 합니다.|  
|/?|명령 프롬프트에 도움말을 표시합니다.|  

## <a name="remarks"></a>주의  
> [!WARNING]  
> 레지스트리를 잘못 편집하면 시스템이 크게 손상될 수 있습니다. 따라서 레지스트리를 변경하기 전에 컴퓨터의 중요한 데이터를 백업해 두어야 합니다.  

텍스트가 주위에 따옴표를 사용 하 여 사용자가 제공 하는 정보에 공백이 포함 되 면 (예를 들어 <DriverName>).  

## <a name="examples"></a><a name=BKMK_Examples></a>예와  
SMTP (Simple Mail Transfer Protocol) 서비스에 대 한 현재 성능 레지스트리 설정 및 카운터 설명 텍스트를 제거 하려면 다음을 수행 합니다.  
```  
unlodctr SMTPSVC  
```  
## <a name="additional-references"></a>추가 참조  
-   - [명령줄 구문 키](command-line-syntax-key.md)  
  
