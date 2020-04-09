---
title: bootcfg
description: Boot.ini 파일 설정을 구성, 쿼리 또는 변경 하는 bootcfg에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3deb354c-5717-4066-bc79-b9323d559e44
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a977b857242c030515a09a67eb0d284ade7a0beb
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80848386"
---
# <a name="bootcfg"></a>bootcfg

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Boot.ini 파일 설정을 구성, 쿼리 또는 변경합니다.

## <a name="syntax"></a>구문

```  
bootcfg <parameter> [arguments...]  
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|  
|-------|--------|  
|[bootcfg addsw](bootcfg-addsw.md)|지정 된 운영 체제 항목에 대 한 운영 체제 로드 옵션을 추가 합니다.|  
|[bootcfg copy](bootcfg-copy.md)|명령줄 옵션을 추가할 수 있는 있는 기존 부팅 항목의 복사본을 만듭니다.|  
|[bootcfg dbg1394](bootcfg-dbg1394.md)|지정된 된 운영 체제 항목에 대 한 1394 포트 디버깅을 구성 합니다.|  
|[bootcfg debug](bootcfg-debug.md)|지정 된 운영 체제 항목에 대 한 디버그 설정을 추가 하거나 변경 합니다.|  
|[bootcfg default](bootcfg-default.md)|기본적으로 지정 하려면 운영 체제 항목을 지정 합니다.|  
|[bootcfg delete](bootcfg-delete.md)|Boot.ini 파일의 **[운영 체제]** 섹션에서 운영 체제 항목을 삭제 합니다.|  
|[bootcfg ems](bootcfg-ems.md)|사용자를 추가 하 여 원격 컴퓨터에 응급 관리 서비스 콘솔의 리디렉션에 대 한 설정을 변경할 수 있습니다.|  
|[bootcfg query](bootcfg-query.md)|쿼리하고 [부팅 로더]을 표시 하 고 **[운영 체제]** Boot.ini에서 항목입니다.|  
|[bootcfg raw](bootcfg-raw.md)|Boot.ini 파일의 **[운영 체제]** 섹션에서 운영 체제 항목에 문자열로 지정 된 운영 체제 로드 옵션을 추가 합니다.|  
|[bootcfg rmsw](bootcfg-rmsw.md)|지정 된 운영 체제 항목에 대 한 운영 체제 로드 옵션을 제거 합니다.|  
|[bootcfg timeout](bootcfg-timeout.md)|운영 체제의 시간 제한 값을 변경 합니다.|  
