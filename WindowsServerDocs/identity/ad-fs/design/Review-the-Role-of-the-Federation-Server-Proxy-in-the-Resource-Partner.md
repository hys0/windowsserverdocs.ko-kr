---
ms.assetid: 14aa112d-ae31-4181-97e4-92623b5c9270
title: 리소스 파트너에서 페더레이션 서버 프록시의 역할 검토
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 377baa8f282f3886284a53b686944fe145b1b15e
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66190891"
---
# <a name="review-the-role-of-the-federation-server-proxy-in-the-resource-partner"></a>리소스 파트너에서 페더레이션 서버 프록시의 역할 검토

Active Directory Federation Services에서 페더레이션 서버 프록시 \(AD FS\) 리소스 파트너 조직의 요구를 충족 하도록 서버를 구성 하는 방법에 따라 다음 역할 중 하나 이상으로 작동할 수 있습니다.  
  
-   **계정 파트너 검색**: 인터넷 클라이언트 컴퓨터는 인증할 계정 파트너를 식별해야 합니다. 클라이언트 계정 파트너 사용 하 여 검색 하는 계정 파트너 검색 웹 양식 \(discoverclientrealm.aspx\)에 리소스 파트너에 페더레이션 서버 프록시에 저장 됩니다. 둘 이상의 계정 파트너 구성 된 경우 AD FS 관리 스냅인\-드롭다운에서는\-드롭다운 메뉴는 계정 파트너에 액세스 하는 인터넷 클라이언트 컴퓨터에 표시 되는 모든 사용 가능한 계정 파트너를 사용 하 여 클라이언트에 표시 Web form 검색 합니다. discoverclientrealm.aspx 파일을 사용자 지정하여 계정 파트너 검색 웹 양식이 클라이언트 컴퓨터에 표시되는 방식을 변경할 수 있습니다.  
  
-   **보안 토큰 리디렉션**: 계정 파트너에서 페더레이션 서버 프록시 리소스 파트너에 게 보안 토큰을 보냅니다. 리소스 페더레이션 서버 프록시 이러한 토큰을 수락 하 고 리소스 파트너 페더레이션 서버에 전달 합니다. 리소스 페더레이션 서버에는 특정 리소스 웹 서버에 바인딩된 보안 토큰을 발급 합니다. 리소스 페더레이션 서버 프록시는 해당 클라이언트에 토큰을 리디렉션합니다.  
  
요약 하면, 리소스 페더레이션 서버 프록시 클라이언트를 인증할 수 있는 페더레이션 서버에 클라이언트 컴퓨터를 리디렉션하여 페더레이션된 로그온 프로세스를 지원 합니다. 리소스 페더레이션 서버 프록시를 클라이언트 보안 토큰 리소스 페더레이션 서버 프록시로 작동합니다.  
  
> [!NOTE]  
> 하드웨어의 규모와 필요한 인증서의 수를 줄이는 데 필요한 경우 페더레이션 서버 프록시 웹 서버와 동일한 컴퓨터에 위치할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목
[Windows Server 2012의 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012.md)

