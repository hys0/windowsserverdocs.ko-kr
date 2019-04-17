---
ms.assetid: 3ecb6e87-17f1-4d38-97d2-9c4d52b7cf39
title: "Federation 서버 프록시 용량에 대 한 계획"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 2e57f34b173c10e9e753c7f3b8dcd88d7bf6742c
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="planning-for-federation-server-proxy-capacity"></a>Federation 서버 프록시 용량에 대 한 계획

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

용량 federation 서버 프록시에 대 한 계획을 평가할 수 있습니다.  
  
-   각 federation 서버 프록시에 대 한 적절 한 하드웨어 요구 합니다.  
  
-   Federation 서버 및 각 조직에 federation 서버 프록시 수 있습니다.  
  
Federation 서버 프록시 보호 federation 서버 회사 네트워크에서 보안 토큰 연합된 사용자에 게 이동합니다. Federation 서버 프록시 배포의 목적은 외부 사용자 federation 서버에 연결할 수 있도록 합니다. 실제로 ADFS 구성 데이터베이스의에서 데이터에 쓰거나 토큰 서명 합니다. 따라서 federation 서버 프록시 위한 하드웨어 요구 사항은 일반적으로 하드웨어 요구 사항을 federation 서버에 대 한 보다 낮은 큽니다.  
  
모든 federation 프록시 서버에 요청 federation 서버 또는 federation 서버 팜 요청 결과, 하기 때문에 용량 federation 서버 및 federation 서버 프록시에 대 한 계획을 동시에 수행 되어야 합니다.  
  
피크 sign\ 기능에 대 한 federation 서버 프록시 초당 예측 필요 federation 서버 프록시 통해 로그인는 연결 된 사용자의 사용 패턴을 이해 합니다. 많은 배포에서 인터넷에 연결 된 사용자에 게 federation 서버 프록시 사용 하 여 로그인 있습니다. 피크 sign\ 기능 초당 Adfs에 의해 보호 됩니다 기존 웹 응용 프로그램에서이 연결 된 사용자의 사용 패턴을 보면 예상할 수 있습니다.  
  
> [!NOTE]  
> 프로덕션 배포에 대 한 각 federation 서버 농장 인스턴스 배포한 두 federation 서버 프록시 최소를 것이 좋습니다.  
  
## <a name="estimate-the-number-of-federation-server-proxies-required-for-your-organization"></a>조직에 필요한 federation 서버 프록시 횟수 예측  
수를 예상할 수 있는 전에 총 federation 서버 조직에 배포할 수를 확인 해야 먼저 ADFS federation 서버 프록시 컴퓨터 필요 합니다. 이 작업을 수행 하는 방법에 대 한 자세한 내용은 참조 [Federation 서버 용량에 대 한 계획](Planning-for-Federation-Server-Capacity.md)합니다.  
  
결정 했으면 federation 서버의 수에 곱하기 요청 외부 사용자 로부터 하 게 될 것이 수가 들어오는 연결 된 인증 배율 서버 \ (회사 network\ 외 있음). 이 계산 값 예상된 federation 서버 프록시 외부 사용자를 위한 수신 인증 요청을 처리할 수를 제공 합니다.  
  
예를 들어 권장된 federation 서버 수가 3 고 외부 사용자 로부터 하 게 인증 요청의 총의 연결 된 인증 총 60% 약 된다는 것으로 예상 계산와 같습니다. 1.8 \ (3 배. 60\) 라운드 수 있는 최대 2.  따라서이 경우 해야 로드 외부 사용자 인증에 대 한 요청이 세 federation 서버에 맞게 두 federation 서버 프록시 컴퓨터를 배포 합니다.  
  
테스트 수행 ADFS 제품 팀에서에서 동일한 농장에 대 한 federation 서버에서 발견 된 있는 cpu 크게 미만 각 federation 서버 프록시에서 전체 cpu가 되었습니다.  테스트 중 하나는 것은 완전히 가득 한 federation 서버 CPU 나타내는 된 동안 사용률이 20% 동일한 해당 그룹에 대 한 프록시 서비스를 제공 하는 federation 서버 프록시에 대 한 CPU 발견 되었습니다. 따라서 테스트를 사용 하는 하드웨어 specifications 유사한 설명한 대로 앞이 섹션에는 federation 서버 프록시 CPU의 로드 약 3 federation 서버에 대해 처리량을 처리할 수 합리적으로 표시 됩니다.  
  
그러나 오류 허용 목적으로 배포할 각 federation 서버 농장에 대 한 두 federation 서버 프록시 최소를 좋습니다.  
  
## <a name="see-also"></a>참조 하십시오
[Windows Server 2012의에서 지침에 따라 AD FS 디자인](AD-FS-Design-Guide-in-Windows-Server-2012.md)
