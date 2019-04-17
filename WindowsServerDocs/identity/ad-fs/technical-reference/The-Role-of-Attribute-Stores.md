---
ms.assetid: 4ddb927d-d65e-491d-840a-16049c083d13
title: "역할의 특성 스토어"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 730411ed7efbb9cf0db3d7e94a486cec4c363849
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
 >적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

# <a name="the-role-of-attribute-stores"></a>역할의 특성 스토어
Active Directory Federation Services "특성 스토어" 라는 용어를 사용 하 여 디렉터리 또는 조직에서 저장 해당 사용자 계정 및 관련된 특성 값 데이터베이스를 참조할 수 있습니다. ADFS 관련 된 스토어에서 검색 및 웹 응용 프로그램 또는 서비스가 신뢰 파티 조직에서 호스트 하는 연결 된 사용자 될 때마다 적절 한 인증 결정 만들 수 있도록 해당 정보에 따라 클레임 만듭니다 신원 공급자 조직에서 구성 후 \ (사용자 계정이 신원 공급자 organization\에 저장 되어) 응용 프로그램이 나 서비스에 액세스 하려고 합니다.  
  
클레임은 생성 하는 방법에 대 한 자세한 내용은 참조 [The 역할 클레임](The-Role-of-Claims.md)합니다.  
  
## <a name="how-attribute-stores-fit-in-with-your-ad-fs-deployment-goals"></a>ADFS 배포 목표는 맞지 특성 저장 되는 방식  
사용자 특성 저장소 위치와 위치를 사용자가 인증 ADFS 사용자 id를 지원 하도록 디자인 하는 방법을 결정 합니다. 사용자가 응용 프로그램에 액세스 하 고 특성 스토어가에 따라 \ (인트라넷 또는 Internet\)에서 다음 배포 목표 중 하나를 사용할 수 있습니다.  
  
-   [나만의 Active Directory 사용자 액세스 클레임 인식 나만의 응용 프로그램 및 서비스를 제공](https://technet.microsoft.com/library/dd807071.aspx)-이 목표 조직에서 사용자가 액세스할 광고 FS-보안 응용 프로그램 또는 서비스가 \ (고유한 응용 프로그램 또는 서비스가 또는 파트너의 응용 프로그램 또는 service\) 때 사용자가 로그인 Active Directory에 회사 인트라넷 합니다.  
  
-   [응용 프로그램 및 기타 조직 서비스에 사용자 Active Directory 사용자 액세스를 제공](https://technet.microsoft.com/library/dd807123.aspx)-이 목표 조직에서 사용자가 액세스할 광고 FS-보안 응용 프로그램 또는 서비스가 \ (고유한 응용 프로그램 또는 서비스가 또는 파트너의 응용 프로그램 또는 service\) 때의 로그온 한 사용자의 회사 인트라넷 하 고 인터넷에서 원격으로 로그온 할 때 특성 스토어로 합니다.  
  
-   [조직 가기에서 다른 사용자가 나만의 클레임 인식 응용 프로그램과 서비스를 제공](https://technet.microsoft.com/library/dd807099.aspx)-이 목표 회사 인트라넷 해당 조직에 특성 스토어에 있는 다른 조직에서 사용자 계정을 FS-보안 응용 프로그램 조직에서 광고에 액세스 해야 합니다. 이 목표 주변 조직의 네트워크의 특성 스토어에 있는 consumer\ 기반 사용자 계정에 액세스할 수 있는 FS-보안 응용 프로그램 조직에서 광고를 제공 해야 하는 경우에 작동 합니다.  
  
특성 스토어 배치 및 회사의 기타 요구 사항에 따라 이러한 ADFS 배포 디자인을 완료 하려면 배포 목표 중 몇 가지 결합할 수 있습니다.  
  
## <a name="attribute-stores-that-are-supported-by-ad-fs"></a>스토어 Adfs에서 지원 되는 특성  
ADFS 다양 한 범위의 디렉터리를 지원 하 고 데이터베이스에 저장 administrator\ 정의 특성 값 압축을 풀고 이러한 값으로 클레임 채우기에 사용할 수 있습니다. ADFS 특성 스토어도 다음 디렉터리 또는 데이터베이스를 지원합니다.  
  
-   Windows Server 2003, Active Directory Domain Services의 active Directory \ (AD DS \), Windows Server 2008, Windows Server 2012 및 2012 R2 및 Windows Server 2016 AD DS 합니다. 
  
-   2005 Microsoft SQL Server, SQL Server 2008, 2012 SQL Server, SQL Server 2014 년 및 SQL Server 2016의 모든 버전  
  
-   사용자 지정 된 특성 스토어  
  

