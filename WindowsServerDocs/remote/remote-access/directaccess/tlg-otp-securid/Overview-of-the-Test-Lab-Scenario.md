---
title: 테스트 랩 시나리오 개요
description: 이 항목은 일부 테스트 랩 가이드-OTP 인증 및 Windows Server 2016 RSA SecurID를 사용한 DirectAccess 시연
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ce584811-b209-48fe-ab2b-4c399bd0bd79
ms.author: pashort
author: shortpatti
ms.openlocfilehash: ebf19d75928e2a19732f2c6c4acaebbf8b34f25f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59871164"
---
# <a name="overview-of-the-test-lab-scenario"></a>테스트 랩 시나리오 개요

>적용 대상: Windows Server (반기 채널), Windows Server 2016

원격 액세스는 Windows Server 2016에서 서버 역할로, 원격 사용자가 안전 하 게 내부를 액세스할 수 있는 운영 체제를 Windows Server 2012 R2 및 Windows Server 2012 DirectAccess를 사용 하 여 리소스를 네트워크 또는 가상 사설망 (Vpn)으로 라우팅 및 원격 액세스 서비스 (RRAS)입니다. 이 가이드에는 확장에 대 한 단계별 지침이 포함 되어 있습니다.는 [테스트 랩 가이드: IPv4 및 IPv6을 사용 하 여 DirectAccess 단일 서버 설치 시연](https://go.microsoft.com/fwlink/p/?LinkId=237004) 원격 액세스 OTP (일회용 암호) 구성을 보여 줍니다.  
  
> [!WARNING]  
> 이 테스트 랩 가이드의 디자인에는 도메인 컨트롤러와 Windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012를 실행 하는 인증 기관 (CA) 등의 인프라 서버를 포함 합니다. 이 테스트 랩 가이드를 사용 하 여 다른 운영 체제를 실행 하는 인프라 서버를 구성 하는 테스트 되지 않았습니다 하 고 다른 운영 체제를 구성 하기 위한 지침은이 가이드에 포함 되지 않습니다.  
  
## <a name="about-this-guide"></a>이 가이드 정보  
Windows Server 2016, Windows Server 2012 R2 및 Windows Server 2012의 원격 액세스에는 OTP 사용 하 여 클라이언트 인증에 대 한 지원이 추가 되었습니다. 이 테스트 랩의 목적에 대 한 원격 액세스를 사용 하 여 OTP 기능을 보여 주기 위해 RSA SecurID만 사용 됩니다. 다른 RADIUS 기반 OTP 솔루션도 지원 되지만이 테스트 랩에서는 다루지 않습니다. 이 가이드에는 서버 6개와 클라이언트 컴퓨터 2대를 사용하여 원격 액세스를 구성 및 시연하는 지침이 나와 있습니다. OTP 테스트 랩 사용 하 여 완료 된 원격 액세스는 인트라넷, 인터넷 및 홈 네트워크, 시뮬레이션 및 다양 한 인터넷 연결 시나리오에서 원격 액세스 기능을 보여 줍니다.  
  
> [!IMPORTANT]  
> 이 랩을 통해 컴퓨터의 개수를 최소한으로 사용하는 개념을 파악할 수 있습니다. 이 가이드에 나와 있는 세부 구성은 테스트 랩 전용이므로, 프로덕션 환경에서 사용해서는 안 됩니다.  
  


