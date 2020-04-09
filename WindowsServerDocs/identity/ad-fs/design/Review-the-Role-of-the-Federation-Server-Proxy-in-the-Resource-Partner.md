---
ms.assetid: 14aa112d-ae31-4181-97e4-92623b5c9270
title: 리소스 파트너에서 페더레이션 서버 프록시의 역할 검토
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 6f49677df16cb1b44d08449a3983ae29fed3cb27
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858546"
---
# <a name="review-the-role-of-the-federation-server-proxy-in-the-resource-partner"></a>리소스 파트너에서 페더레이션 서버 프록시의 역할 검토

리소스 파트너 조직의 요구를 충족 하도록 서버를 구성 하는 방법에 따라 AD FS\) \(Active Directory Federation Services의 페더레이션 서버 프록시는 다음 역할 중 하나 이상으로 작동할 수 있습니다.  
  
-   **계정 파트너 검색**: 인터넷 클라이언트 컴퓨터는 인증할 계정 파트너를 식별해야 합니다. 클라이언트는 리소스 파트너의 페더레이션 서버 프록시에 저장 된 계정 파트너 검색 웹 양식 \(discoverclientrealm.aspx\)를 사용 하 여 계정 파트너를 찾습니다. 둘 이상의 계정 파트너가의 AD FS 관리\-스냅인에서 구성 된 경우 계정 파트너 검색 웹 양식에 액세스 하는 인터넷 클라이언트 컴퓨터에 표시 되는 모든 사용 가능한 계정 파트너와 함께 드롭\-다운 메뉴가 클라이언트에 표시 됩니다. discoverclientrealm.aspx 파일을 사용자 지정하여 계정 파트너 검색 웹 양식이 클라이언트 컴퓨터에 표시되는 방식을 변경할 수 있습니다.  
  
-   **보안 토큰 리디렉션**: 계정 파트너의 페더레이션 서버 프록시는 리소스 파트너에 게 보안 토큰을 보냅니다. 리소스 페더레이션 서버 프록시는 이러한 토큰을 수락 하 고 리소스 파트너의 페더레이션 서버에 전달 합니다. 그런 다음 리소스 페더레이션 서버는 특정 리소스 웹 서버에 바인딩된 보안 토큰을 발급 합니다. 그러면 리소스 페더레이션 서버 프록시가 토큰을 클라이언트로 리디렉션합니다.  
  
요약 하자면, 리소스 페더레이션 서버 프록시는 클라이언트를 인증할 수 있는 페더레이션 서버에 클라이언트 컴퓨터를 리디렉션하여 페더레이션된 로그온 프로세스를 용이 하 게 합니다. 리소스 페더레이션 서버 프록시는 또한 리소스 페더레이션 서버에 대 한 클라이언트 보안 토큰의 프록시 역할을 합니다.  
  
> [!NOTE]  
> 하드웨어 양과 필요한 인증서 수를 줄이는 데 필요한 경우 페더레이션 서버 프록시는 웹 서버와 동일한 컴퓨터에 있을 수 있습니다.  
  
## <a name="see-also"></a>참고 항목
[Windows Server 2012의 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012.md)

