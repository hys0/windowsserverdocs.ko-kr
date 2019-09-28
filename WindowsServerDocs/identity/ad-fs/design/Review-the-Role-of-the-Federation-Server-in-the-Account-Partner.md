---
ms.assetid: d0ba3c0d-869f-4e24-89d7-499da7576f22
title: 계정 파트너에서 페더레이션 서버의 역할 검토
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: ead8868f38faa570a0e524630e23d99e276a7c79
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407920"
---
# <a name="review-the-role-of-the-federation-server-in-the-account-partner"></a>계정 파트너에서 페더레이션 서버의 역할 검토

Active Directory Federation Services \(AD FS @ no__t-1의 페더레이션 서버는 보안 토큰 발급자로 작동 합니다. 페더레이션 서버는 로컬 특성 저장소에 있는 계정 값에 따라 클레임을 생성 하 고 사용자가 웹 @ no__t-0browser @ no__t 기반 응용 @no__t 프로그램에 원활 하 게 액세스할 수 있도록 (single sign @ no__t를 사용 하 여) 리소스 파트너 조직에서 호스트 되는 \(SSO @ no__t @ no__t-6  
  
> [!NOTE]  
> 사용자가 웹 브라우저를 사용 하 여 페더레이션된 응용 프로그램에 액세스 하는 경우 페더레이션 서버는 사용자에 게 자동으로 쿠키를 발급 하 여 해당 웹 @ no__t-0browser @ no__t 기반 응용 프로그램에 대 한 로그온 상태를 유지 합니다. 이러한 쿠키는 사용자에 대한 클레임을 포함합니다. 쿠키를 사용 하면 사용자가 리소스 파트너의 다른 웹 @ no__t-0browser @ no__t-1based 응용 프로그램을 방문할 때마다 자격 증명을 입력할 필요가 없도록 SSO 기능을 사용할 수 있습니다.  
  
웹 SSO 디자인에서 인터넷 사용자가 응용 프로그램에 액세스할 수 있도록 하려는 경계 네트워크가 있는 조직은 경계 네트워크에 페더레이션 서버 프록시를 설치 해야 합니다. 페더레이션된 웹 SSO 디자인에서는 계정 파트너 조직의 회사 네트워크에 하나 이상의 페더레이션 서버가 설치 되어 있어야 하 고 리소스 파트너 조직의 회사 네트워크에 하나 이상의 페더레이션 서버가 설치 되어 있어야 합니다.  
  
> [!NOTE]  
> 계정 파트너 조직에서 페더레이션 서버 컴퓨터를 설정 하려면 먼저 페더레이션 서버를 사용 하 여 해당 포리스트의 사용자를 인증 하는 Active Directory 포리스트의 도메인에 컴퓨터를 가입 해야 합니다. 자세한 내용은 [ 검사 목록을 참조 하세요. 페더레이션 서버 설정 @ no__t-0.  
  
## <a name="see-also"></a>관련 항목
[Windows Server 2012의 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012.md)
