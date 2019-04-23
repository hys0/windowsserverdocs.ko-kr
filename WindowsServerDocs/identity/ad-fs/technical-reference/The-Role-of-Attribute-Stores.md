---
ms.assetid: 4ddb927d-d65e-491d-840a-16049c083d13
title: 특성 저장소의 역할
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 730411ed7efbb9cf0db3d7e94a486cec4c363849
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59860414"
---
 >적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

# <a name="the-role-of-attribute-stores"></a>특성 저장소의 역할
Active Directory Federation Services 사용 "특성 저장소" 라는 용어는 조직이 해당 사용자 계정 및 관련된 특성 값을 저장 하기 위해 사용 하는 디렉터리 또는 데이터베이스를 가리키도록 합니다. AD FS id 공급자 조직에 구성 된 후 저장소에서 이러한 특성 값을 검색 하 고 웹 응용 프로그램 또는 신뢰 당사자 조직에서 호스트 되는 서비스 수 있도록 적절 한 정보에 따라 클레임을 만듭니다. 때마다 페더레이션된 사용자 권한 부여 결정 \(계정이 id 공급자 조직에 저장 된 사용자\) 응용 프로그램 또는 서비스에 액세스 하려고 합니다.  
  
클레임이 생성되는 방법에 대한 자세한 내용은 [The Role of Claims](The-Role-of-Claims.md)을 참조하세요.  
  
## <a name="how-attribute-stores-fit-in-with-your-ad-fs-deployment-goals"></a>특성 저장소가 AD FS 배포 목표를 맞추는 방법  
사용자 특성 저장소의 위치 및 사용자를 인증 하는 위치에 사용자 id를 지원 하도록 AD FS를 디자인 하는 방법을 결정 합니다. 특성 저장소의 위치 및 사용자가 응용 프로그램을 액세스 하는 위치에 따라 \(인트라넷에서 또는 인터넷에서\), 다음과 같은 배포 목표 중 하나를 사용할 수 있습니다.  
  
-   [사용자 Active Directory 사용자가 액세스 클레임 인식 응용 프로그램 및 서비스 제공](https://technet.microsoft.com/library/dd807071.aspx)—이 목표에서 조직의 사용자가 AD FS 보안 응용 프로그램 또는 서비스에 액세스 \(사용자 고유의 응용 프로그램 또는 서비스 또는 파트너의 응용 프로그램 또는 서비스\) 사용자 기록 되는 경우 Active Directory에 회사 인트라넷에 있습니다.  
  
-   [응용 프로그램 및 서비스의 다른 조직 Your Active Directory 사용자가 액세스를 제공](https://technet.microsoft.com/library/dd807123.aspx)—이 목표에서 조직의 사용자가 AD FS 보안 응용 프로그램 또는 서비스에 액세스 \(사용자 고유의 응용 프로그램 또는 서비스 또는 파트너의 응용 프로그램 또는 서비스\) 특성 저장소에서 회사 인트라넷 및 인터넷에서 원격으로 로그온 할 때에 사용자가 로그온 때.  
  
-   [다른 조직 액세스에서 사용자에 게 클레임 인식 응용 프로그램 및 서비스 제공](https://technet.microsoft.com/library/dd807099.aspx)—이 목표에서 해당 조직의 회사 인트라넷의 특성 저장소에 있는 다른 조직의 사용자 계정에 액세스 해야는 AD FS- 조직에서 응용 프로그램을 보호 합니다. 이 목표 역시 때 소비자\-조직의 경계 네트워크의 특성 저장소에 따라 사용자 계정 액세스를 사용 하 여 AD FS 보안 응용 프로그램에서 조직에 제공 해야 합니다.  
  
특성 저장소 배치 및 조직의 기타 요구 사항에 따라 다양 한 AD FS 배포의 설계를 완료 하려면 이러한 배포 목표를 결합할 수 있습니다.  
  
## <a name="attribute-stores-that-are-supported-by-ad-fs"></a>AD FS에서 지원되는 특성 저장소  
AD FS는 광범위 한 디렉터리를 지원 하 고 데이터베이스 관리자를 추출 하기 위한 사용할 수 있는 저장\-특성 값을 정의 하 고 해당 값으로 클레임을 채우기입니다. AD FS는 특성 저장소로 다음 디렉터리 또는 데이터베이스를 지원합니다.  
  
-   Windows Server 2003 Active Directory Domain Services에서에서 active Directory \(AD DS\) Windows Server 2012 및 2012 R2에서 Windows Server 2008 AD DS 및 Windows Server 2016에서. 
  
-   Microsoft SQL Server 2005, SQL Server 2008, SQL Server 2012, SQL Server 2014 및 SQL Server 2016의 모든 버전  
  
-   사용자 지정 특성 저장소  
  

