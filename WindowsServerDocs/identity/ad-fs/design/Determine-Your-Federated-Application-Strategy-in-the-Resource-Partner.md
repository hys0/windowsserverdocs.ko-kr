---
ms.assetid: 9eab8c43-a0f2-4d19-a5a4-e1399f0d5f25
title: 리소스 파트너의 페더레이션 응용 프로그램 전략 결정
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 0cc7a9202813cd3f8d45a72305d13ad197f5b04d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359157"
---
# <a name="determine-your-federated-application-strategy-in-the-resource-partner"></a>리소스 파트너의 페더레이션 응용 프로그램 전략 결정

리소스 파트너 조직에서 새로운 Active Directory Federation Services \(AD FS\) 인프라를 디자인 하는 중요 한 부분은 페더레이션에 참여 하는 데 사용 되는 응용 프로그램 및 서비스의 전체 집합 및 해당 리소스의 수신자가 될 계정 파트너를 결정 하는 것입니다. 페더레이션 응용 프로그램 및 서비스 전략을 디자인하기 전에 다음 질문을 고려합니다.  
  
-   페더레이션을 위해 ASP.NET 응용 프로그램 또는 WCF\) 서비스 \(Windows Communication Foundation을 사용 하도록 설정 하 고 배포할 예정 인가요?  
  
-   회사 네트워크의 사용자가 Windows 통합 인증을 통해 페더레이션 응용 프로그램 또는 서비스에 액세스해야 하나요?  
  
-   경계 네트워크의 사용자가 페더레이션 응용 프로그램 또는 서비스를 사용하나요? 사용한다면 Windows 통합 인증이 필요하나요?  
  
-   페더레이션 응용 프로그램을 호스트 하는 모든 웹 서버가 Windows Server 운영 체제를 실행 하 고 인터넷 정보 서비스 \(IIS\)있나요?  
  
-   페더레이션 응용 프로그램 또는 서비스에서 리소스를 제공하는 대상은 누구인가요?  
  
이러한 질문에 대답 하면 견고한 AD FS 디자인을 계획 하는 데 도움이 됩니다. 또한 효율적인 비용과 리소스로 페더레이션 응용 프로그램 및 서비스 전략을 세울 수 있습니다. 소속한 조직에 가장 적합한 페더레이션 응용 프로그램 및 서비스의 전략을 디자인하는 방법에 대한 자세한 내용은 이 가이드의 다음 항목을 참조하세요.  
  
-   [Active Directory 사용자에게 클레임 인식 애플리케이션 및 서비스에 대한 액세스 제공](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md)  
  
-   [Active Directory 사용자에게 다른 조직의 애플리케이션 및 서비스에 대한 액세스 제공](Provide-Your-Active-Directory-Users-Access-to-the-Applications-and-Services-of-Other-Organizations.md)  
  
-   [다른 조직의 사용자에게 클레임 인식 애플리케이션 및 서비스에 대한 액세스 제공](Provide-Users-in-Another-Organization-Access-to-Your-Claims-Aware-Applications-and-Services.md)  
  
클레임\-인식 ASP.NET 응용 프로그램 또는 WCF 서비스를 만드는 방법에 대 한 자세한 내용은 [Windows Identity FOUNDATION SDK](https://go.microsoft.com/fwlink/?LinkId=122266)를 참조 하세요.  
  
## <a name="see-also"></a>참고 항목
[Windows Server 2012의 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012.md)

