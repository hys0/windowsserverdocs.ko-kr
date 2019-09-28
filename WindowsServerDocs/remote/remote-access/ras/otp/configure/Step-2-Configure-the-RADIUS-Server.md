---
title: 2 단계 RADIUS 서버 구성
description: 이 항목은 Windows Server 2016에서 OTP 인증을 사용 하 여 원격 액세스 배포 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0326818f-9144-496c-b946-f82be4eefbd3
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 00ea76d6995f875e509a3bc9ef0bab3d2689c52b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71367024"
---
# <a name="step-2-configure-the-radius-server"></a>2 단계 RADIUS 서버 구성

>적용 대상: Windows Server(반기 채널), Windows Server 2016

OTP 지원으로 DirectAccess를 지원 하도록 원격 액세스 서버를 구성 하기 전에 RADIUS 서버를 구성 합니다.  
  
|태스크|설명|  
|----|--------|  
|[2.1. RADIUS 소프트웨어 배포 토큰 구성 @ no__t-0|RADIUS 서버에서 소프트웨어 배포 토큰을 구성 합니다.|  
|[2.2. RADIUS 보안 정보 구성 @ no__t-0|RADIUS 서버에서 사용할 포트 및 공유 암호를 구성 합니다.|  
|[2.3 OTP 검색을 위한 사용자 계정 추가](#BKMK_Probe)|RADIUS 서버에서 OTP 검색을 위한 새 사용자 계정을 만듭니다.|  
|[2.4 Active Directory와 동기화](#BKMK_Active)|RADIUS 서버에서 Active Directory 계정과 동기화 된 사용자 계정 만들기를 시작 합니다.|  
|[2.5 RADIUS 인증 에이전트 구성](#BKMK_AuthAgent)|RADIUS 인증 에이전트로 원격 액세스 서버를 구성 합니다.|  
  
## <a name="BKMK_1.1"></a>2.1 RADIUS 소프트웨어 배포 토큰 구성  
RADIUS 서버는 OTP를 사용 하 여 DirectAccess에서 사용 되는 필수 라이선스 및 소프트웨어 및/또는 하드웨어 배포 토큰으로 구성 해야 합니다. 이 프로세스는 각 RADIUS 공급 업체 구현과 관련이 있습니다.  
  
## <a name="BKMK_1.2"></a>2.2 RADIUS 보안 정보 구성  
RADIUS 서버는 통신을 위해 UDP 포트를 사용 하며 각 RADIUS 공급 업체에는 들어오고 나가는 통신을 위한 자체 기본 UDP 포트가 있습니다. RADIUS 서버에서 원격 액세스 서버를 사용 하려면 필요한 포트를 통해 DirectAccess와 OTP 서버 간에 UDP 트래픽을 허용 하도록 환경의 모든 방화벽이 구성 되어 있는지 확인 합니다.  
  
RADIUS 서버는 인증을 위해 공유 암호를 사용 합니다. 공유 암호에 대 한 강력한 암호를 사용 하 여 RADIUS 서버를 구성 합니다 .이는 OTP를 사용 하 여 DirectAccess에서 사용할 DirectAccess 서버의 클라이언트 컴퓨터 구성을 구성할 때 사용 됩니다.  
  
## <a name="BKMK_Probe"></a>2.3 OTP 검색을 위한 사용자 계정 추가  
RADIUS 서버에서 **DAProbeUser** 라는 새 사용자 계정을 만들고 암호를 **DAProbePass**로 지정 합니다.  
  
## <a name="BKMK_Active"></a>2.4 Active Directory와 동기화  
RADIUS 서버에는 OTP와 함께 DirectAccess를 사용 하는 Active Directory 사용자에 해당 하는 사용자 계정이 있어야 합니다.  
  
#### <a name="to-synchronize-the-radius-and-active-directory-users"></a>RADIUS 및 Active Directory 사용자를 동기화 하려면  
  
1.  OTP 사용자를 사용 하 여 모든 DirectAccess에 대해 Active Directory에서 사용자 정보를 기록 합니다.  
  
2.  공급 업체의 특정 절차를 사용 하 여 기록 된 RADIUS 서버에 동일한 사용자 **도메인 \** 사용자 계정을 만듭니다.  
  
## <a name="BKMK_AuthAgent"></a>2.5 RADIUS 인증 에이전트 구성  
원격 액세스 서버는 OTP 구현이 포함 된 DirectAccess에 대 한 RADIUS 인증 에이전트로 구성 되어야 합니다. Radius 공급 업체 지침에 따라 원격 액세스 서버를 RADIUS 인증 에이전트로 구성 합니다.  
  


