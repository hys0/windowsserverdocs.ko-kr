---
title: 원격 액세스 서버의 OTP에 대 한 계획을 4 단계
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
ms.assetid: 4b97b2fd-767a-45c1-a64e-5b3edd0c8a47
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 470eebc82177a21985afb8d0bf143427a33d65fb
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59825444"
---
# <a name="step-4-plan-for-otp-on-the-remote-access-server"></a>원격 액세스 서버의 OTP에 대 한 계획을 4 단계

>적용 대상: Windows Server (반기 채널), Windows Server 2016

일회용 암호 (OTP) RADIUS 서버 및 인증서 설정에 대 한 계획 한 후에 원격 액세스 OTP 배포 계획의 마지막 단계는 원격 액세스 서버의 OTP 설정을 클라이언트에 대 한 계획 하는 것입니다.  
  
|태스크|설명|  
|----|--------|  
|[4.1 OTP 클라이언트 예외에 대 한 계획](#bkmk_4_1_Exemptions)|OTP를 사용 하 여 인증에 필요 하지 않은 사용자에 대 한 예외에 대 한 계획입니다.|  
|[4.2 Windows 7 클라이언트에 대 한 계획](#bkmk_4_2_Win7)|Windows 7 클라이언트 컴퓨터에는 연결 길잡이 DCA (DirectAccess) 2.0을 배포 하려고 합니다.|  
|[4.3 스마트 카드에 대 한 계획](#BKMK_smartcard)|추가 권한 부여에 대 한 스마트 카드의 사용을 계획 합니다.|  
  
## <a name="bkmk_4_1_Exemptions"></a>4.1 OTP 클라이언트 예외에 대 한 계획  
OTP 인증을 사용 하는 경우 기본적으로 모든 사용자에 게 필요한 사용자 이름 및 암호와 OTP 자격 증명의 조합을 사용 하 여 인증 합니다. 그러나 선택한 사용자가 OTP 없이 사용자 이름 및 암호만 사용 하 여 인증 하도록 허용할 수 있습니다. 이렇게 하려면 보안 그룹을 만들고에 OTP 인증에서 제외 하려는 사용자를 추가 합니다.  
  
> [!NOTE]  
> 때문에 단일 포리스트의 클라이언트 컴퓨터를 제외할 수 있습니다 클라이언트 예외에 대 한 하나의 보안 그룹을 선택할 수 있습니다.  
  
## <a name="bkmk_4_2_Win7"></a>4.2 Windows 7 클라이언트에 대 한 계획  
기본적으로 Windows 7 클라이언트 컴퓨터는 OTP를 사용 하 여 인증할 수 없습니다.  Windows 7 클라이언트 컴퓨터에서 DCA 2.0 Windows Server 2012 원격 액세스 배포에서 OTP를 사용 하 여 인증 해야 합니다. DCA 2.0에 대 한 자세한 내용은 참조 하십시오 [DirectAccess Connectivity Assistant 2.0](https://go.microsoft.com/fwlink/?LinkId=253699) Microsoft 다운로드 센터에서.  
  
## <a name="BKMK_smartcard"></a>4.3 스마트 카드에 대 한 계획  
OTP 인증을 사용 하는 경우 추가 권한 부여에 대 한 스마트 카드를 사용할 수 있도록 방법은 사용할 수 있습니다. 사용자의 스마트 카드 작동 하지 않습니다 하는 경우에 대 한 임시 액세스를 허용 하는 보안 그룹을 만듭니다.  
  
## <a name="BKMK_Links"></a>참고 항목  
  
-   [OTP 인증을 사용 하 여 DirectAccess를 구성 합니다.](https://technet.microsoft.com/windows-server-docs/networking/remote-access/ras/otp/deploy-ra-otp)  
  


