---
ms.assetid: 9eab8c43-a0f2-4d19-a5a4-e1399f0d5f25
title: "연결 된 응용 프로그램이 전략 리소스 파트너에 결정"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: aca47658cc5a20f63dbd59a26ebe135dd04def92
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="determine-your-federated-application-strategy-in-the-resource-partner"></a>연결 된 응용 프로그램이 전략 리소스 파트너에 결정

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

중요 한 일부 리소스 파트너 조직에서 새 Active Directory Federation Services \(AD FS\) 인프라 디자인 하면 전체 응용 프로그램 및 서비스 집합을 연합에 참여 하는 데 사용 될는 하 고는 계정 파트너 리소스 받는 됩니다 결정 하는 것입니다. 연결 된 응용 프로그램 및 전략 서비스를 디자인 하기 전에 다음과 같은 질문을 고려 합니다.  
  
-   사용 하면 되며 ASP.NET 응용 프로그램 또는 federation에 대 한 Windows Communication Foundation \(WCF\) 서비스 배포 있나요?  
  
-   회사 네트워크에 사용자가 연결 된 응용 프로그램이 나 통합 인증 Windows를 통해 서비스에 대 한 액세스가 필요 합니다.  
  
-   연결 된 응용 프로그램이 나 서비스 주변 네트워크에 사용자가 사용할 수 있나요? 그렇다면은 Windows 통합 인증 필요할 수 있나요?  
  
-   Windows Server 운영 체제 및 인터넷 정보 서비스 \(IIS\) 실행 되는 호스트 연결 된 응용 프로그램의 웹 서버 모든 되나요?  
  
-   누가 연결 된 응용 프로그램이 나 서비스 제공에 대 한 리소스 하나요?  
  
이러한 질문에 대답 단색 ADFS 디자인을 계획 하는 데 도움이 됩니다. 또한 연결 된 응용 프로그램 및는 비용 효과적인 서비스 전략 리소스 효율적으로 만들 지원 합니다. 연결 된 응용 프로그램을 가장 적합 한 및 조직에 대 한 서비스 전략 디자인에 대 한 자세한 내용은 다음 항목이이 가이드에서는 참조 하십시오.  
  
-   [인식 클레임 응용 프로그램 및 서비스에 사용자 Active Directory 사용자가 액세스할 수 있도록](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md)  
  
-   [응용 프로그램 및 서비스에서는 다른 조직의 Active Directory 사용자 액세스를 제공](Provide-Your-Active-Directory-Users-Access-to-the-Applications-and-Services-of-Other-Organizations.md)  
  
-   [조직에 대 한 또 다른 액세스에 사용자가 인식 클레임 응용 프로그램 및 서비스에 제공](Provide-Users-in-Another-Organization-Access-to-Your-Claims-Aware-Applications-and-Services.md)  
  
Claims\ 인식 ASP.NET 응용 프로그램이 나 WCF 서비스를 만드는 방법에 대 한 자세한 내용은 참조 [Windows 신원을 Foundation SDK](https://go.microsoft.com/fwlink/?LinkId=122266)합니다.  
  
## <a name="see-also"></a>참조 하십시오
[Windows Server 2012의에서 지침에 따라 AD FS 디자인](AD-FS-Design-Guide-in-Windows-Server-2012.md)

