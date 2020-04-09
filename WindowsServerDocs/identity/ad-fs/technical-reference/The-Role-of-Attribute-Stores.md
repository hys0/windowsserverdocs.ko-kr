---
ms.assetid: 4ddb927d-d65e-491d-840a-16049c083d13
title: 특성 저장소의 역할
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 595f0b3b11172df9bf95d3bb8aab90368bb0e77f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80860196"
---
# <a name="the-role-of-attribute-stores"></a>특성 저장소의 역할
Active Directory Federation Services는 "특성 저장소" 라는 용어를 사용 하 여 조직에서 사용자 계정 및 관련 특성 값을 저장 하는 데 사용 하는 디렉터리 또는 데이터베이스를 참조 합니다. Id 공급자 조직에 구성 된 후 AD FS는 저장소에서 이러한 특성 값을 검색 하 고 해당 정보에 따라 클레임을 만듭니다. 그러면 페더레이션 사용자 \(계정이 id 공급자 조직에 저장 된 사용자\) 응용 프로그램이 나 서비스에 대 한 액세스를 시도할 때마다 적절 한 권한 부여 결정을 내릴 수 있습니다.  
  
클레임이 생성되는 방법에 대한 자세한 내용은 [The Role of Claims](The-Role-of-Claims.md)을 참조하세요.  
  
## <a name="how-attribute-stores-fit-in-with-your-ad-fs-deployment-goals"></a>특성 저장소가 AD FS 배포 목표를 맞추는 방법  
사용자 특성 저장소의 위치 및 사용자가 인증 하는 위치에 따라 사용자 id를 지원 하기 위해 AD FS를 설계 하는 방법이 결정 됩니다. 특성 저장소가 있는 위치 및 사용자가 인트라넷 또는 인터넷\)의 응용 프로그램 \(액세스 하는 위치에 따라 다음 배포 목표 중 하나를 사용할 수 있습니다.  
  
-   사용자에 게 [클레임 인식 응용 프로그램 및 서비스에 대 한 액세스 권한을 Active Directory 제공](https://technet.microsoft.com/library/dd807071.aspx)합니다 .이 목표에서 조직의 사용자는 회사 인트라넷의 Active Directory에 로그온 할 때 사용자 응용 프로그램 또는 서비스 또는 파트너의 응용 프로그램 또는 서비스\) \(AD FS 보안 응용 프로그램 또는 서비스에 액세스할 수 있습니다.  
  
-   [Active Directory 사용자에 게 다른 조직의 응용 프로그램 및 서비스에 대 한 액세스를 제공](https://technet.microsoft.com/library/dd807123.aspx)합니다 .이 목표에서 조직의 사용자는 회사 인트라넷의 특성 저장소에 로그온 하 고 인터넷에서 원격으로 로그온 할 때 사용자의 응용 프로그램이 나 서비스 또는 파트너의 응용 프로그램 또는\) 서비스 \(AD FS 보안 응용 프로그램 또는 서비스에 액세스할 수 있습니다.  
  
-   [다른 조직의 사용자에 게 클레임 인식 응용 프로그램 및 서비스에 대 한 액세스 권한 부여](https://technet.microsoft.com/library/dd807099.aspx)-이 목표에서 해당 조직의 회사 인트라넷의 특성 저장소에 있는 다른 조직의 사용자 계정은 조직의 AD FS 보안 응용 프로그램에 액세스 해야 합니다. 이 목표는 조직의 경계 네트워크의 특성 저장소에 있는 소비자\-기반 사용자 계정이 조직의 AD FS 보안 응용 프로그램에 대 한 액세스를 제공 해야 하는 경우에도 작동 합니다.  
  
특성 저장소 배치 및 조직의 기타 요구 사항에 따라 이러한 여러 배포 목표를 조합 하 여 AD FS 배포의 설계를 완료할 수 있습니다.  
  
## <a name="attribute-stores-that-are-supported-by-ad-fs"></a>AD FS에서 지원되는 특성 저장소  
AD FS는 관리자\-정의 된 특성 값을 추출 하 고 해당 값으로 클레임을 채우는 데 사용할 수 있는 광범위 한 디렉터리 및 데이터베이스 저장소를 지원 합니다. AD FS은 특성 저장소로 다음 디렉터리 또는 데이터베이스를 지원 합니다.  
  
-   Windows server 2003의 Active Directory windows server 2008에서\) \(AD DS windows Server 2012 및 2012 R2 및 Windows Server 2016의 AD DS를 Active Directory Domain Services 합니다. 
  
-   Microsoft SQL Server 2005, SQL Server 2008, SQL Server 2012, SQL Server 2014 및 SQL Server 2016의 모든 버전  
  
-   사용자 지정 특성 저장소  
  

