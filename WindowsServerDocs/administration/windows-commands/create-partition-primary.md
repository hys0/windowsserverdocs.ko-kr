---
title: 파티션 기본 만들기
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6d652d8e-3935-4a91-8ced-b17c0e7937be
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bbbb4b89540b7264fe907f79ca003117429da08e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59881714"
---
# <a name="create-partition-primary"></a>파티션 기본 만들기

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

포커스가 있는 기본 디스크에 주 파티션을 만듭니다.  
  
> [!CAUTION]  
  
  
  
## <a name="syntax"></a>구문  
  
```  
create partition primary [size=<n>] [offset=<n>] [id={ <byte> | <guid> }] [align=<n>] [noerr]  
```  
  
## <a name="parameters"></a>매개 변수  
  
|매개 변수|설명|  
|-------|--------|  
|size\=<n>|파티션의 크기 (메가바이트)에서 지정 \(MB\)합니다. 크기를 지정 하는 경우 파티션이 될 때까지 할당 되지 않은 현재 지역에서 공간을 계속 합니다.|  
|offset\=<n>|(킬로바이트)의 오프셋 \(KB\), 파티션을 만들 때에 있습니다. 없는 오프셋을 지정 하는 경우 파티션을 저장 하는 데 충분히 큰 가장 큰 디스크 범위의 시작 부분에 시작 됩니다.|  
|align\=<n>|모든 파티션 범위에 있는 가장 가까운 맞춤 경계선을 맞춥니다. 일반적으로 하드웨어 RAID 논리 단위 번호와 사용 \(LUN\) 성능을 향상 시키기 위해 배열입니다. <n> (킬로바이트)입니다 \(KB\) 가장 가까운 맞춤 경계선을 디스크의 시작 부분에서.|  
|id\={ <byte> & #124; <guid> }|파티션 형식을 지정합니다. 이 매개 변수는 원래 장비 제조업체를 위한 \(OEM\) 만 사용 합니다. 이 매개 변수는 모든 파티션 형식 바이트 또는 GUID를 지정할 수 있습니다. 16 진수 형식 또는 GUID 바이트 인지 확인을 제외 하 고 유효성에 대 한 파티션 유형을 확인 하지 않습니다. **주의:** 이 매개 변수를 사용 하 여 파티션 만들기 실패 하거나 시작 하지 못할 컴퓨터를 발생할 수 있습니다. OEM 또는 gpt 디스크를 사용 하 여 발생 하는 IT 전문가가 아니라면이 매개 변수를 사용 하 여 gpt 디스크에 파티션을 만들지 마십시오. 대신 항상을 **efi 파티션을 만들** EFI 시스템 파티션에 만드는 명령을 합니다 **파티션 msr 만드는** Microsoft 예약 파티션을 만드는 명령 및 **만들기 기본 파티션** 명령 \(없이 **id\={0} 바이트&#124;guid}** 매개 변수\) gpt 디스크에 주 파티션을 만들려면 합니다.<br /><br />**마스터 부트 레코드 디스크**<br /><br />마스터 부트 레코드에 대 한 \(MBR\) 디스크, 파티션 종류 바이트를 파티션에 대 한 16 진수 형식으로 지정 합니다. MBR 디스크에 대해이 매개 변수를 지정 하지 않으면,이 명령은 파일 시스템을 설치 되어 있는지를 지정 하는 형식의 0x06, 파티션을 만듭니다. 예를 들면 다음과 같습니다.<br /><br />데이터 파티션을 LDM: 0x42<br />-복구 파티션을: 0x27<br />-인식된 OEM 파티션: 0x12, 0x84, 0xDE, 0xFE, 0xA0<br /><br />**GUID 파티션 테이블 디스크**<br /><br />GUID 파티션 테이블에 대 한 \(gpt\) 디스크에서 만들려는 파티션에 대 한 파티션 유형 GUID를 지정할 수 있습니다. 인식 된 Guid는 다음과 같습니다.<br /><br />-EFI 시스템 파티션을: c12a7328\-f81f\-11 d 2\-ba4b\-00a0c93ec93b<br />-Microsoft Reserved 파티션: e3c9e316\-0b5c\-4db8\-817 d\-f92df00215ae<br />-기본 데이터 파티션을: ebd0a0a2\-b9e5\-4433\-87 c 0\-68b6b72699c7<br />동적 디스크에 메타 데이터 파티션을 LDM: 5808c8aa\-7e8f\-42e0\-85d2\-e1e90434cfb3<br />동적 디스크에 데이터 파티션을 LDM: af9b60a0\-1431\-4f62\-bc68\-3311714a69ad<br />-복구 파티션을: de94bba4\-06 d 1\-4d 40\-a16a\-bfd50179d6ac<br /><br />이 매개 변수는 gpt 디스크에 대 한 지정 하지 않으면이 명령은 기본 데이터 파티션을 만듭니다.|  
|noerr|만 스크립팅 합니다. 오류가 발생 하면 오류가 발생 하지 않은 경우에 따라 명령을 처리 하도록 DiskPart 계속 합니다. 디스크 크기는 오류 코드를 수행 합니다.|  
  
## <a name="remarks"></a>설명  
  
-   파티션을 만든 후 포커스는 자동으로 새 파티션으로 이동 합니다.  
  
-   파티션의는 드라이브 문자를 받지 않습니다. 사용 해야는 **할당** 파티션에 드라이브 문자를 할당 하려면 DiskPart 명령을 합니다.  
  
-   이 작업을 수행 하려면 기본 디스크를 선택 해야 합니다. 사용 된 **디스크 선택** 기본 디스크를 선택 하 고 포커스를 이동 하는 명령입니다.  
  
## <a name="BKMK_examples"></a>예제  
1000 메가바이트 주 파티션 크기에서를 만들려면 다음을 입력 합니다.  
  
```  
create partition primary size=1000  
```  
  
#### <a name="additional-references"></a>추가 참조  
[명령줄 구문 키](command-line-syntax-key.md)  
  

  

