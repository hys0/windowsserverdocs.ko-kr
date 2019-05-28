---
ms.assetid: 9eab8c43-a0f2-4d19-a5a4-e1399f0d5f25
title: 리소스 파트너의 페더레이션 응용 프로그램 전략 결정
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 15a6c095648795badfae6f68f1ba2f9270219db8
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66191457"
---
# <a name="determine-your-federated-application-strategy-in-the-resource-partner"></a>리소스 파트너의 페더레이션 응용 프로그램 전략 결정

새 Active Directory Federation Services를 디자인 하는 중요 한 부분은 \(AD FS\) 리소스 파트너 조직에서 인프라에 참여 하는 데 사용할 수 있는 응용 프로그램과 서비스의 전체 집합과 결정 하는 것은 페더레이션 및 해당 리소스의 수신인이 될 계정 파트너는 합니다. 페더레이션 응용 프로그램 및 서비스 전략을 디자인하기 전에 다음 질문을 고려합니다.  
  
-   사용 하도록 설정 되며 ASP.NET 응용 프로그램 또는 Windows Communication Foundation을 배포 \(WCF\) 페더레이션에 대 한 서비스?  
  
-   회사 네트워크의 사용자가 Windows 통합 인증을 통해 페더레이션 응용 프로그램 또는 서비스에 액세스해야 하나요?  
  
-   경계 네트워크의 사용자가 페더레이션 응용 프로그램 또는 서비스를 사용하나요? 사용한다면 Windows 통합 인증이 필요하나요?  
  
-   모든 Windows Server 운영 체제 및 인터넷 정보 서비스를 실행 하는 페더레이션된 응용 프로그램을 호스트 하는 웹 서버가 \(IIS\)?  
  
-   페더레이션 응용 프로그램 또는 서비스에서 리소스를 제공하는 대상은 누구인가요?  
  
이러한 질문에 답변 견고한 AD FS 디자인 계획 하는 데 도움이 됩니다. 또한 효율적인 비용과 리소스로 페더레이션 응용 프로그램 및 서비스 전략을 세울 수 있습니다. 소속한 조직에 가장 적합한 페더레이션 응용 프로그램 및 서비스의 전략을 디자인하는 방법에 대한 자세한 내용은 이 가이드의 다음 항목을 참조하세요.  
  
-   [Active Directory 사용자에게 클레임 인식 애플리케이션 및 서비스에 대한 액세스 제공](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md)  
  
-   [Active Directory 사용자에게 다른 조직의 애플리케이션 및 서비스에 대한 액세스 제공](Provide-Your-Active-Directory-Users-Access-to-the-Applications-and-Services-of-Other-Organizations.md)  
  
-   [다른 조직의 사용자에게 클레임 인식 애플리케이션 및 서비스에 대한 액세스 제공](Provide-Users-in-Another-Organization-Access-to-Your-Claims-Aware-Applications-and-Services.md)  
  
클레임을 만드는 방법에 대 한 자세한 내용은\-인식 ASP.NET 응용 프로그램 또는 WCF 서비스를 참조 하세요 [Windows Identity Foundation SDK](https://go.microsoft.com/fwlink/?LinkId=122266)합니다.  
  
## <a name="see-also"></a>관련 항목
[Windows Server 2012의 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012.md)

