---
title: 2 단계 RADIUS 서버 배포 계획
description: 이 항목은 Windows Server 2016에서 OTP 인증을 사용 하 여 원격 액세스 배포 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2d6ad863-02a5-49b0-9aff-d189e78b2b80
ms.author: pashort
author: shortpatti
ms.openlocfilehash: f74a83c3962c7accd76fbf07307216742ada863d
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280825"
---
# <a name="step-2-plan-the-radius-server-deployment"></a>2 단계 RADIUS 서버 배포 계획

>적용 대상: Windows Server (반기 채널), Windows Server 2016

단일 원격 액세스 서버를 배포한 후 OTP (일회용 암호) 인증 서버를 계획 합니다.  
  
|태스크|설명|  
|----|--------|  
|2.1 RADIUS 서버 계획|OTP 인증 서버에 대 한 Windows Server 2016 및 Windows Server 2012 원격 액세스 (PAP)의 암호 인증 프로토콜을 지 원하는 모든 RADIUS 기반 OTP 서버를 지원 합니다.|  
  
## <a name="BKMK_1.1"></a>2.1 RADIUS 서버 계획  
OTP 인증을 위해 RADIUS 서버를 계획할 때 다음 note:  
  
-   OTP 배포의 대부분의 형식에 대 한 RADIUS 에이전트로 원격 액세스 서버를 구성 해야 합니다. 자세한 내용은 OTP 공급 업체 설명서를 참조 하십시오.  
  
-   모든 OTP 배포에 대 한 RADIUS 서버를 사용 하 여 Active Directory 사용자를 동기화 해야 합니다.  
  
-   RADIUS 서버는 도메인 구성원이 될 필요가 없습니다.  
  
-   RADIUS 서버를 배포 하면 공유 암호 및 RADIUS 트래픽에 대해 포트 번호를 구성 합니다. 이러한 세부 정보 기록 이러한는 원격 액세스 서버를 구성한 경우에 필요 합니다.  
  
에 있는 RSA SecurID 서버를 사용 하 여 OTP 인증을 설정 하는 예제 테스트 랩 가이드를 볼 수 있습니다 [테스트 랩 가이드: OTP 인증 및 RSA SecurID를 사용한 DirectAccess 시연](https://technet.microsoft.com/windows-server-docs/networking/remote-access/directaccess/tlg-otp-securid/test-lab-guide-demonstrate-directaccess-with-otp-authentication-and-rsa-securid)합니다.  
  
  
  


