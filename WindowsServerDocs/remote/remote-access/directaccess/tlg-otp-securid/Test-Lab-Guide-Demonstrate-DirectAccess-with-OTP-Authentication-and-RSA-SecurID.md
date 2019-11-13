---
title: 테스트 랩 가이드-OTP 인증 및 RSA SecurID를 사용한 DirectAccess 시연
description: 이 항목은 테스트 랩 가이드-OTP 인증을 사용 하는 DirectAccess 시연 및 Windows Server 2016에 대 한 RSA SecurID의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 10c7a49c-5671-4bec-b562-13fdd67f4629
ms.author: pashort
author: shortpatti
ms.openlocfilehash: f226c4c4b8a7517458ede95b4e237b567e0c49df
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404667"
---
# <a name="test-lab-guide-demonstrate-directaccess-with-otp-authentication-and-rsa-securid"></a>테스트 랩 가이드: OTP 인증 및 RSA SecurID를 사용한 DirectAccess 시연

>적용 대상: Windows Server(반기 채널), Windows Server 2016

원격 액세스는 원격 사용자가 라우팅과 함께 DirectAccess 또는 Vpn (가상 사설망)을 사용 하 여 내부 네트워크 리소스에 안전 하 게 액세스할 수 있도록 하는 Windows Server 2016, Windows Server 2012 R2 및 Windows Server 2012 운영 체제의 서버 역할입니다. 및 원격 액세스 서비스 (RRAS)를 사용 합니다. 이 가이드에는 [테스트 랩 가이드: IPv4 및 i p v 6을 사용 하 여 DirectAccess 단일 서버 설치 시연](https://go.microsoft.com/fwlink/p/?LinkId=237004) 을 확장 하 여 원격 액세스 OTP (일회용 암호) 구성을 시연 하는 단계별 지침이 포함 되어 있습니다.  
  
> [!WARNING]  
> 이 테스트 랩 가이드의 디자인에는 도메인 컨트롤러 및 Windows Server 2012 R2 또는 Windows Server 2012를 실행 하는 CA (인증 기관)와 같은 인프라 서버가 포함 되어 있습니다. 이 테스트 랩 가이드를 사용 하 여 다른 운영 체제를 실행 하는 인프라 서버를 구성 하는 것은 테스트 되지 않았으며 다른 운영 체제를 구성 하기 위한 지침은이 가이드에 포함 되어 있지 않습니다.  
  
## <a name="about-this-guide"></a>이 가이드 정보  
Windows server 2016, Windows server 2012 R2 및 Windows Server 2012의 원격 액세스는 OTP를 사용 하 여 클라이언트 인증에 대 한 지원을 추가 합니다. 이 테스트 랩의 목적을 위해 RSA SecurID는 원격 액세스를 사용 하는 OTP 기능을 시연 하는 데만 사용 됩니다. 다른 RADIUS 기반 OTP 솔루션도 지원 되지만이 테스트 랩의 범위를 벗어납니다. 이 가이드에는 서버 6개와 클라이언트 컴퓨터 2대를 사용하여 원격 액세스를 구성 및 시연하는 지침이 나와 있습니다. OTP 테스트 랩에서 완료 된 원격 액세스는 인트라넷, 인터넷 및 홈 네트워크를 시뮬레이션 하 고 다양 한 인터넷 연결 시나리오의 원격 액세스 기능을 보여 줍니다.  
  
> [!IMPORTANT]  
> 이 랩을 통해 컴퓨터의 개수를 최소한으로 사용하는 개념을 파악할 수 있습니다. 이 가이드에 나와 있는 세부 구성은 테스트 랩 전용이므로, 프로덕션 환경에서 사용해서는 안 됩니다.  
  


