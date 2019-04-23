---
title: RADIUS 서버를 구성 하는 2 단계
description: 이 항목은 Windows Server 2016에서 OTP 인증을 사용 하 여 원격 액세스 배포 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0326818f-9144-496c-b946-f82be4eefbd3
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 219c333745d28bdedb9027c1dd46148ac80998f6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59840874"
---
# <a name="step-2-configure-the-radius-server"></a>RADIUS 서버를 구성 하는 2 단계

>적용 대상: Windows Server (반기 채널), Windows Server 2016

지원 하도록 원격 액세스 서버를 구성 하기 전에 DirectAccess OTP 사용 하 여 지원, RADIUS 서버를 구성 합니다.  
  
|태스크|설명|  
|----|--------|  
|[2.1. RADIUS 소프트웨어 배포 토큰 구성](#BKMK_1.1)|RADIUS 서버에서 소프트웨어 배포 토큰을 구성 합니다.|  
|[2.2. RADIUS 보안 정보 구성](#BKMK_1.2)|RADIUS 서버에서 사용할 공유 비밀 확인 하 고 포트를 구성 합니다.|  
|[2.3 OTP 검색에 대 한 사용자 계정 추가](#BKMK_Probe)|RADIUS 서버에서 OTP 검색에 대 한 새 사용자 계정을 만듭니다.|  
|[2.4 Active Directory와 동기화](#BKMK_Active)|RADIUS 서버에서 Active Directory 계정을 사용 하 여 동기화 된 사용자 계정을 만듭니다.|  
|[2.5 RADIUS 인증 에이전트를 구성 합니다.](#BKMK_AuthAgent)|RADIUS 인증 에이전트를 원격 액세스 서버를 구성 합니다.|  
  
## <a name="BKMK_1.1"></a>2.1 RADIUS 소프트웨어 배포 토큰 구성  
필요한 라이선스 및 OTP 사용 하 여 DirectAccess에서 사용할 소프트웨어 및/또는 하드웨어 배포 토큰을 사용 하 여 RADIUS 서버를 구성 되어야 합니다. 이 프로세스는 각 RADIUS 공급 업체 구현에 한정 됩니다.  
  
## <a name="BKMK_1.2"></a>2.2 RADIUS 보안 정보 구성  
RADIUS 서버 통신을 위해 UDP 포트를 사용 하 고 각 RADIUS 공급 업체에 들어오고 나가는 통신을 위해 자체 기본 UDP 포트. 원격 액세스 서버에서 작동 하도록 RADIUS 서버에 대 한 환경에서 모든 방화벽 필요에 따라 필요한 포트를 통해 DirectAccess 및 OTP 서버 간에 UDP 트래픽을 허용 하도록 구성 되어 있는지 확인 합니다.  
  
RADIUS 서버 인증을 위해 공유 암호를 사용합니다. 공유 암호에 대 한 강력한 암호를 사용 하 여 RADIUS 서버를 구성 하 고 OTP 사용 하 여 DirectAccess를 사용 하 여 DirectAccess 서버의 클라이언트 컴퓨터 구성 사용에 대 한를 구성할 때이 사용할 수 있는지 확인 합니다.  
  
## <a name="BKMK_Probe"></a>2.3 OTP 검색에 대 한 사용자 계정 추가  
RADIUS 서버에서 이라는 새 사용자 계정을 만듭니다 **사용자** 암호를 지정 **daprobepass입니다**합니다.  
  
## <a name="BKMK_Active"></a>2.4 Active Directory와 동기화  
RADIUS 서버에 사용 하는 DirectAccess OTP를 사용 하 여 Active Directory에서 사용자에 해당 하는 사용자 계정이 있어야 합니다.  
  
#### <a name="to-synchronize-the-radius-and-active-directory-users"></a>RADIUS 및 Active Directory 사용자를 동기화 하려면  
  
1.  OTP 사용자와 모든 DirectAccess에 대 한 Active Directory에서의 사용자 정보를 기록 합니다.  
  
2.  동일한 사용자를 만들려면 공급 업체 특정 절차를 따르십시오 **도메인 \ 사용자 이름** RADIUS 서버에서 기록 된 계정입니다.  
  
## <a name="BKMK_AuthAgent"></a>2.5 RADIUS 인증 에이전트를 구성 합니다.  
원격 액세스 서버는 DirectAccess OTP 구현에 대 한 RADIUS 인증 에이전트로 구성 되어야 합니다. RADIUS 인증 에이전트로 원격 액세스 서버를 구성 하는 RADIUS 공급 업체 지침을 따릅니다.  
  


