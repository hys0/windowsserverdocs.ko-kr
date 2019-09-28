---
title: netcfg
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e2daaab7-12db-4e36-b70c-db8906d084f7 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8f8368aaff16592a55cc9def84d593cf323f28ee
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71373294"
---
# <a name="netcfg"></a>netcfg

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Windows 사전 설치 환경 (WinPE) 워크스테이션을 배포 하는 데 사용 되는 Windows의 경량 버전을 설치 합니다.   
## <a name="syntax"></a>구문  
```  
netcfg [/v] [/e] [/winpe] [/l ] /c /i  
```  
### <a name="parameters"></a>매개 변수  
|매개 변수|설명|  
|-------|--------|  
|/v|자세한 (세부) 모드에서 실행|  
|/e|설치 중 서비스 환경 변수를 사용 및 제거|  
|/winpe|Windows 사전 설치 환경에 대 한 TCP/IP, NetBIOS 및 Microsoft 클라이언트를 설치합니다.|  
|/l|INF의 위치를 제공합니다.|  
|/c|설치, 구성 요소 클래스를 제공 합니다. 프로토콜, 서비스 또는 클라이언트|  
|/i|구성 요소 ID를 제공합니다.|  
|/s|구성 요소를 표시 유형을 제공합니다<br /><br />\ta 어댑터, n = = net 구성 요소|  
|/?|명령 프롬프트에 도움말을 표시합니다.|  
## <a name="BKMK_Examples"></a>예와  
프로토콜을 설치 하려면 *예제* c:\oemdir\example.inf를 사용 하 여:  
```  
netcfg /l c:\oemdir\example.inf /c p /i example  
```  
설치 하는 *MS_Server* 서비스:  
```  
netcfg /c s /i MS_Server  
```  
Windows 사전 설치 환경에 대 한 TCP/IP, NetBIOS 및 Microsoft 클라이언트를 설치 하려면  
```  
netcfg /v /winpe  
```  
경우 구성 요소를 표시 하려면 *MS_IPX* 가 설치 되어 있습니다.  
```  
netcfg /q MS_IPX  
```  
구성 요소를 제거 하려면 *MS_IPX*:  
```  
netcfg /u MS_IPX  
```  
모두 표시 하려면 net 구성 요소를 설치 합니다.  
```  
netcfg /s n  
```  
포함 하는 경로 바인딩 쇼에 *MS_TCPIP*:  
```  
netcfg /b ms_tcpip  
```  
## <a name="additional-references"></a>추가 참조  
-   [명령줄 구문 키](command-line-syntax-key.md)  
