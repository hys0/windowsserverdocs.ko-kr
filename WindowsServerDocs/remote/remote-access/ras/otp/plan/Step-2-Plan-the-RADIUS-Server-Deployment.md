---
title: 2 단계 RADIUS 서버 배포 계획
description: 이 항목은 Windows Server 2016에서 OTP 인증을 사용 하 여 원격 액세스 배포 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2d6ad863-02a5-49b0-9aff-d189e78b2b80
ms.author: pashort
author: shortpatti
ms.openlocfilehash: a991b312a0938a3809acd2b94c00aa678f5b41da
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404393"
---
# <a name="step-2-plan-the-radius-server-deployment"></a>2 단계 RADIUS 서버 배포 계획

>적용 대상: Windows Server(반기 채널), Windows Server 2016

단일 원격 액세스 서버를 배포한 후 OTP (일회용 암호) 인증 서버를 계획 합니다.  
  
|태스크|설명|  
|----|--------|  
|2.1 RADIUS 서버 계획|OTP 인증 서버의 경우 Windows Server 2016 및 Windows Server 2012의 원격 액세스에서 PAP (암호 인증 프로토콜)를 지 원하는 모든 RADIUS 사용 OTP 서버를 지원 합니다.|  
  
## <a name="BKMK_1.1"></a>2.1 RADIUS 서버 계획  
OTP 인증용 RADIUS 서버를 계획할 때에는 다음 사항에 유의 하세요.  
  
-   대부분의 OTP 배포 유형에 대해서는 원격 액세스 서버를 RADIUS 에이전트로 구성 해야 합니다. 자세한 내용은 OTP 공급 업체 설명서를 참조 하세요.  
  
-   모든 OTP 배포의 경우 Active Directory 사용자를 RADIUS 서버와 동기화 해야 합니다.  
  
-   RADIUS 서버는 도메인 멤버일 필요가 없습니다.  
  
-   RADIUS 서버를 배포할 때 RADIUS 트래픽에 대 한 공유 암호 및 포트 번호를 구성 합니다. 이러한 세부 정보를 기록해 둡니다. 원격 액세스 서버를 구성할 때 필요 합니다.  
  
[테스트 랩 가이드: otp 인증 및 Rsa securid를 사용한 DirectAccess 시연](https://technet.microsoft.com/windows-server-docs/networking/remote-access/directaccess/tlg-otp-securid/test-lab-guide-demonstrate-directaccess-with-otp-authentication-and-rsa-securid)에서 RSA securid 서버를 사용 하 여 otp 인증을 설정 하는 테스트 랩 가이드 예제를 볼 수 있습니다.  
  
  
  


