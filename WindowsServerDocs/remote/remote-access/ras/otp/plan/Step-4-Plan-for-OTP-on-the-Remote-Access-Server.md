---
title: 4 단계 원격 액세스 서버에서 OTP 계획
description: 이 항목은 Windows Server 2016에서 OTP 인증을 사용 하 여 원격 액세스 배포 가이드의 일부입니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: 4b97b2fd-767a-45c1-a64e-5b3edd0c8a47
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 789fd72e2f3fc1693bf4803f33dcc1e7f1b3acc3
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855776"
---
# <a name="step-4-plan-for-otp-on-the-remote-access-server"></a>4 단계 원격 액세스 서버에서 OTP 계획

>적용 대상: Windows Server(반기 채널), Windows Server 2016

OTP (일회용 암호) RADIUS 서버 및 인증서 설정을 계획 한 후 원격 액세스 OTP 배포 계획의 마지막 단계는 원격 액세스 서버에서 클라이언트 OTP 설정을 계획 하는 것입니다.  
  
|작업|설명|  
|----|--------|  
|[4.1 OTP 클라이언트 예외 계획](#bkmk_4_1_Exemptions)|OTP를 사용 하 여 인증 하지 않아도 되는 사용자에 대 한 예외를 계획 합니다.|  
|[4.2 Windows 7 클라이언트에 대 한 계획](#bkmk_4_2_Win7)|Windows 7 클라이언트 컴퓨터에는 DCA (DirectAccess 연결 길잡이) 2.0을 배포 하도록 계획 합니다.|  
|[4.3 스마트 카드 계획](#BKMK_smartcard)|추가 권한 부여에 대 한 스마트 카드 사용을 계획 합니다.|  
  
## <a name="41-plan-for-otp-client-exemptions"></a><a name="bkmk_4_1_Exemptions"></a>4.1 OTP 클라이언트 예외 계획  
OTP 인증을 사용 하도록 설정한 경우 기본적으로 모든 사용자는 사용자 이름 및 암호와 OTP 자격 증명의 조합을 사용 하 여 인증 해야 합니다. 그러나 선택한 사용자가 OTP 없이 사용자 이름 및 암호만 사용 하 여 인증 하도록 허용할 수 있습니다. 이렇게 하려면 보안 그룹을 만들고 OTP 인증에서 제외 하려는 모든 사용자를 추가 합니다.  
  
> [!NOTE]  
> 클라이언트 예외에 대해 보안 그룹을 하나만 선택할 수 있기 때문에 단일 포리스트의 클라이언트 컴퓨터만 제외 될 수 있습니다.  
  
## <a name="42-plan-for-windows-7-clients"></a><a name="bkmk_4_2_Win7"></a>4.2 Windows 7 클라이언트에 대 한 계획  
기본적으로 Windows 7 클라이언트 컴퓨터는 OTP를 사용 하 여 인증할 수 없습니다.  Windows 7 클라이언트 컴퓨터에는 Windows Server 2012 원격 액세스 배포에서 OTP를 사용 하 여 인증 하려면 DCA 2.0이 필요 합니다. DCA 2.0에 대 한 자세한 내용은 Microsoft 다운로드 센터에서 [DirectAccess 연결 길잡이 2.0](https://go.microsoft.com/fwlink/?LinkId=253699) 를 참조 하세요.  
  
## <a name="43-plan-for-smart-cards"></a><a name="BKMK_smartcard"></a>4.3 스마트 카드 계획  
OTP 인증을 사용 하는 경우 추가 권한 부여에 대 한 스마트 카드를 사용 하도록 설정 하는 옵션을 사용할 수 있습니다. 사용자의 스마트 카드가 작동 하지 않는 경우 임시 액세스를 허용 하는 보안 그룹을 만듭니다.  
  
## <a name="see-also"></a><a name="BKMK_Links"></a>참고 항목  
  
-   [OTP 인증을 사용 하 여 DirectAccess 구성](https://technet.microsoft.com/windows-server-docs/networking/remote-access/ras/otp/deploy-ra-otp)  
  


