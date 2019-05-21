---
title: ipxroute
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3a30304f-655e-43d2-a4ac-7568abf8975c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d995204eea0af776a2084a82411fa95542d1d77a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889094"
---
# <a name="ipxroute"></a>ipxroute

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

표시 하 고 IPX 프로토콜에 의해 사용 되는 라우팅 테이블에 대 한 정보를 수정 합니다. 매개 변수 없이 사용  **ipxroute** 알 수 없는, 브로드캐스트 및 멀티 캐스트 주소로 보내진 패킷에 대 한 기본 설정을 표시 합니다.   
## <a name="syntax"></a>구문  
```  
ipxroute servers [/type=X]  
ipxroute ripout <Network>  
ipxroute resolve {guid | name} {GUID | <AdapterName>}  
ipxroute board= N [def] [gbr] [mbr] [remove=xxxxxxxxxxxx]  
ipxroute config  
```  
### <a name="parameters"></a>매개 변수  
|매개 변수|설명|  
|-------|--------|  
|서버 [/ 유형 = X]|지정 된 서버 유형에 대 한 서비스 액세스 지점 (SAP) 테이블을 표시합니다.  **X** 정수 여야 합니다. 예를 들어 **/유형 = 4** 모든 파일 서버를 표시 합니다. 지정 하지 않으면 **/유형**, **ipxroute 서버** 모든 종류의 서버, 서버 이름으로 나열 표시 됩니다.|  
|ripout 네트워크|검색 하는 경우 *네트워크* IPX 스택의 경로 테이블을 참조 하 고 필요한 경우 rip 요청을 보내는 하 여 연결할 수는 있습니다.  *네트워크* IPX 네트워크 세그먼트 수입니다.|  
|해결 {GUID&#124; 이름} {GUID&#124; AdapterName}|GUID의 이름을 식별 이름으로 하거나 이름을 해당 GUID로 확인 됩니다.|  
|보드 = *N*|쿼리 또는 매개 변수를 설정 하려는 네트워크 어댑터를 지정 합니다.|  
|def|모든 경로 브로드캐스트 패킷을 전송합니다. 원본 라우팅 테이블에 없는 고유한 미디어 액세스 카드 (MAC) 주소에 패킷이 전송 되는 경우 **ipxroute** 기본적으로 브로드캐스트하는 단일 경로 패킷을 보냅니다.|  
|gbr|모든 경로 브로드캐스트 패킷을 전송합니다. 패킷을 브로드캐스트 주소 (FFFFFFFFFFFF)에 전송 되는 경우 **ipxroute** 기본적으로 브로드캐스트하는 단일 경로 패킷을 보냅니다.|  
|mbr|모든 경로 브로드캐스트 패킷을 전송합니다. 패킷이 멀티 캐스트 주소 (C000xxxxxxxx)로 전송 되는 경우 **ipxroute** 기본적으로 브로드캐스트하는 단일 경로 패킷을 보냅니다.|  
|제거 = *됩니다.*|원본 라우팅 테이블에서 지정 된 노드의 주소를 제거합니다.|  
|구성|모든 바인딩은 IPX가 구성에 대 한 정보를 표시 합니다.|  
|/?|명령 프롬프트에 도움말을 표시합니다.|  
## <a name="BKMK_Examples"></a>예제  
워크스테이션에 연결 된 네트워크 세그먼트, 워크스테이션 노드 주소 및 사용 되는 유형을 프레임을 표시 하려면 다음을 입력 합니다.  
```  
ipxroute config  
```  
## <a name="additional-references"></a>추가 참조  
-   [명령줄 구문 키](command-line-syntax-key.md)  
