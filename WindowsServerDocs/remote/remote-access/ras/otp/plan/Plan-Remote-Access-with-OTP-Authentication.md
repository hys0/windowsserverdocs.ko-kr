---
title: OTP 인증을 통한 원격 액세스 계획
description: 이 항목은 Windows Server 2016에서 OTP 인증을 사용 하 여 원격 액세스 배포 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 762bc463-eead-46ac-8b90-32355743c27c
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 328e092dff23495203ee21fccbace1f7f36918d2
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280821"
---
# <a name="plan-remote-access-with-otp-authentication"></a>OTP 인증을 통한 원격 액세스 계획

>적용 대상: Windows Server (반기 채널), Windows Server 2016

 Windows Server 2016 및 Windows Server 2012 DirectAccess 및 라우팅 및 원격 액세스 서비스 (RRAS) VPN 단일 원격 액세스 역할로 결합합니다. 이 개요에서는 단일 Windows Server 2016 또는 Windows Server 2012 원격 액세스 멀티 사이트 배포를 배포 하는 데 필요한 구성 단계를 소개 합니다.  
  
  
-  1단계: [고급 설정 사용 하 여 단일 DirectAccess 서버 배포](https://technet.microsoft.com/windows-server-docs/networking/remote-access/directaccess/single-server-advanced/deploy-a-single-directaccess-server-with-advanced-settings)합니다. 이 단계는 단일 서버를 배포 하는 데 필요한 인프라에 대 한 계획이 포함 됩니다. 네트워크 및 서버 설정, 인증서 요구 사항, DNS 설정, 네트워크 위치 서버 배포, DirectAccess 관리 서버, Active Directory 설정 및 그룹 정책 개체 (Gpo)에 대 한 계획이 포함 됩니다.  
  
-   [2단계: RADIUS 서버 배포 계획](Step-2-Plan-the-RADIUS-Server-Deployment.md)  
  
-   [3단계: OTP 인증서 배포 계획](Step-3-Plan-OTP-Certificate-Deployment.md)  
  
-   [4단계: 원격 액세스 서버의 OTP에 대 한 계획](Step-4-Plan-for-OTP-on-the-Remote-Access-Server.md)  
  
이러한 계획 단계를 완료 한 후 [OTP 인증을 사용 하 여 원격 액세스 구성](https://technet.microsoft.com/windows-server-docs/networking/remote-access/ras/otp/configure/configure-ra-with-otp-authentication)합니다. 랩 환경에서 개념 증명으로 멀티 사이트 배포를 구성 하는 방법에 대 한 정보를 참조 하세요. [테스트 랩 가이드: OTP 인증 및 RSA SecurID를 사용한 DirectAccess 시연](https://technet.microsoft.com/windows-server-docs/networking/remote-access/directaccess/tlg-otp-securid/test-lab-guide-demonstrate-directaccess-with-otp-authentication-and-rsa-securid)합니다.  
  


