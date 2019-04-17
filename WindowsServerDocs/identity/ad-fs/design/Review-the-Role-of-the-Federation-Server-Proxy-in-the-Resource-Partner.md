---
ms.assetid: 14aa112d-ae31-4181-97e4-92623b5c9270
title: "리소스 파트너에 Federation 서버 프록시 역할을 검토"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 31e285e863e4316a8e0a65f9b68c27442290927d
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="review-the-role-of-the-federation-server-proxy-in-the-resource-partner"></a>리소스 파트너에 Federation 서버 프록시 역할을 검토

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Active Directory Federation Services \(AD FS\)는 federation 서버 프록시 리소스 파트너 회사의 요구 사항에 맞게 서버를 구성 하는 방법에 따라 다음과 같은 역할을 중 하나 이상을에서 작동할 수 있습니다.  
  
-   **계정 파트너 검색**: 계정을 파트너는 인증 하는 인터넷 가지의 식별 해야 합니다. 클라이언트 계정 파트너를 계정을 파트너 검색 웹 양식 \(discoverclientrealm.aspx\), 리소스 파트너 해당 federation 서버 프록시에 저장 되는 사용 하 여 찾습니다. 둘 이상의 계정을 파트너 snap\ 기능에 drop\ 다운 메뉴 클라이언트 웹 양식을 계정은 파트너 검색에 액세스 하는 인터넷 클라이언트 컴퓨터에 표시 되는 모든 계정 사용할 수 있는 파트너와 함께 나타납니다 AD FS 관리 구성 됩니다. 컴퓨터에 discoverclientrealm.aspx 파일을 사용자 지정 하 여 웹 양식을 계정은 파트너 검색은 표시 하는 방법을 변경할 수 있습니다.  
  
-   **보안 토큰 리디렉션을**: 계정 파트너의 federation 서버 프록시 보안 토큰 리소스 파트너에 게 보냅니다. 리소스 federation 서버 프록시 이러한 토큰을 받는 및 리소스 파트너에 federation 서버에 전달 합니다. 다음 리소스 federation 서버 보안 토큰 특정 리소스 웹 서버에 연결 하는 문제를 합니다. 다음 리소스 federation 서버 프록시 클라이언트 토큰을 리디렉션합니다.  
  
요약 리소스 federation 서버 프록시 쉽게 클라이언트 컴퓨터 클라이언트 인증할 수 있는 federation 서버에 리디렉션하여 연합된 로그온을 수 있습니다. 또한 리소스 federation 서버 프록시 역할을 클라이언트 보안 토큰 연합 서버 리소스에 대 한 프록시 합니다.  
  
> [!NOTE]  
> 하드웨어의 양과 필요한 인증서의 수를 줄이는 데 도움이 필요한 경우 federation 서버 프록시 웹 서버와 동일한 컴퓨터에 있을 수 있습니다.  
  
## <a name="see-also"></a>참조 하십시오
[Windows Server 2012의에서 지침에 따라 AD FS 디자인](AD-FS-Design-Guide-in-Windows-Server-2012.md)

