---
ms.assetid: 95e82190-68c5-4e40-87b1-f1bd816ef4e9
title: "서비스 통신 인증서"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 32e60f2c2d9e4fced04061ace44882b792e1a3bc
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="service-communications-certificates"></a>서비스 통신 인증서

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Federation server 서비스 통신 인증서의 사용 WCF 메시지 보안을 사용 하는 시나리오에 대해 필요 합니다.  
  
## <a name="service-communication-certificate-requirements"></a>서비스 통신 인증서 요구 사항  
서비스 통신 인증서 ADFS 작업할 다음 요구 사항을 충족 해야 합니다.  
  
-   서비스 통신 인증서 서버 인증 향상 키 사용 \(EKU\) 확장을 포함 해야 합니다.  
  
-   인증서 해지 목록을 \(CRLs\) 루트 인증서에 서비스 통신 인증서의 모든 인증서 체인의에 액세스할 수 있어야 합니다. 캘리포니아 루트 federation 서버 프록시 및 해당 federation 서버를 신뢰할 수 있는 웹 서버도 신뢰할 수 있어야 합니다.  
  
-   서비스 통신 인증서에 사용 되는 주체 이름을 Federation 서비스 속성에서 Federation 서비스 이름을 일치 해야 합니다.  
  
## <a name="deployment-considerations-for-service-communication-certificates"></a>배포 서비스 통신 인증서 사항  
동일한 인증서를 사용 하는 모든 federation 서버 서비스 통신 인증서를 구성 합니다. 웹 Single\-Sign\-On 연방 \(SSO\) 디자인을 배포 하는 경우 서비스 통신 인증서 공개 캘리포니아에서 발급 되어야 하는 것이 좋습니다. 요청 하 고 IIS 관리자 snap\ 기능을 통해 이러한 인증서를 설치할 수 있습니다.  
  
서비스 통신 인증서를 테스트 랩 환경에서 federation 서버에 성공적으로, self\ 서명 사용할 수 있습니다. 하지만, 생산 환경에서 공개 캘리포니아 서비스 통신 인증서를 얻는 것이 좋습니다. 사용 self\ 서명 서비스 통신 인증서가 아닌 라이브 배포 해야 하는 이유는 다음과 같습니다.  
  
-   A self\ 서명 인증서 SSL에 추가 해야 각 리소스 파트너 조직에서 federation 서버의 루트 신뢰할 수 있는 저장소. 이 그대로 않는 하지을 사용 하면는 공격자 리소스 federation 서버를 self\ 서명 인증서를 신뢰 하는 컴퓨터의 공격 높이 및 인증서 서명자 신뢰할 수 없는 경우 보안 문제를 일으킬 수 있습니다.  
  
-   잘못 된 사용자 경험을 만듭니다. 클라이언트 다음 메시지를 표시 하는 연결 된 리소스에 액세스 하려고 할 때 보안 경고 메시지를 받게 됩니다. "의 보안 인증서 신뢰할 하도록 선택 하지 않은 회사에서 발급 되었습니다." 예상 되는 동작 self\ 서명 인증서를 신뢰할 수 없기 때문입니다.  
  
    > [!NOTE]  
    > 필요한 경우에 수동으로 아래로 self\ 서명 인증서를 신뢰할 수 있는 루트 스토어 ADFS 사이트에 액세스 하려고 각 클라이언트 컴퓨터에서 그룹 정책을 사용 하 여이 문제를 해결할 수 있습니다.  
  
-   CAs 추가 기능을 제공 certificate\ 기반, 개인 키 보관, 갱신 해지 등 self\ 서명 인증서가 제공 되지 않는 합니다.  
  

