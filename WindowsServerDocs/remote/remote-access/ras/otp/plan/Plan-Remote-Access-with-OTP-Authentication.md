---
title: OTP 인증을 통한 원격 액세스 계획
description: 이 항목은 Windows Server 2016에서 OTP 인증을 사용 하 여 원격 액세스 배포 가이드의 일부입니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: 762bc463-eead-46ac-8b90-32355743c27c
ms.author: lizross
author: eross-msft
ms.openlocfilehash: ddcfa2898f4b90bf724a547bb16244cfad4ab3ff
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858196"
---
# <a name="plan-remote-access-with-otp-authentication"></a>OTP 인증을 통한 원격 액세스 계획

>적용 대상: Windows Server(반기 채널), Windows Server 2016

 Windows Server 2016 및 Windows Server 2012에서는 DirectAccess 및 RRAS (라우팅 및 원격 액세스 서비스) VPN을 단일 원격 액세스 역할로 결합 합니다. 이 개요에서는 단일 Windows Server 2016 또는 Windows Server 2012 원격 액세스 멀티 사이트 배포를 배포 하기 위해 필요한 구성 단계를 소개 합니다.  
  
  
-  1 단계: [고급 설정을 사용 하 여 단일 DirectAccess 서버를 배포](https://technet.microsoft.com/windows-server-docs/networking/remote-access/directaccess/single-server-advanced/deploy-a-single-directaccess-server-with-advanced-settings)합니다. 이 단계에는 단일 서버를 배포 하는 데 필요한 인프라에 대 한 계획이 포함 됩니다. 여기에는 네트워크 및 서버 설정, 인증서 요구 사항, DNS 설정, 네트워크 위치 서버 배포, DirectAccess 관리 서버, Active Directory 설정 및 Gpo (그룹 정책 개체)에 대 한 계획이 포함 됩니다.  
  
-   [2 단계: RADIUS 서버 배포 계획](Step-2-Plan-the-RADIUS-Server-Deployment.md)  
  
-   [3 단계: OTP 인증서 배포 계획](Step-3-Plan-OTP-Certificate-Deployment.md)  
  
-   [4 단계: 원격 액세스 서버에서 OTP 계획](Step-4-Plan-for-OTP-on-the-Remote-Access-Server.md)  
  
이러한 계획 단계를 완료 한 후 [OTP 인증을 사용 하 여 원격 액세스 구성](https://technet.microsoft.com/windows-server-docs/networking/remote-access/ras/otp/configure/configure-ra-with-otp-authentication)을 참조 하세요. 랩 환경의 개념 증명으로 멀티 사이트 배포를 구성 하는 방법에 대 한 자세한 내용은 [테스트 랩 가이드: OTP 인증 및 RSA SecurID를 사용한 DirectAccess 시연](https://technet.microsoft.com/windows-server-docs/networking/remote-access/directaccess/tlg-otp-securid/test-lab-guide-demonstrate-directaccess-with-otp-authentication-and-rsa-securid)을 참조 하세요.  
  


