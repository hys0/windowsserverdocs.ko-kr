---
title: "Windows Server 2012 r 2 Active Directory Federation Services 역할 서비스 마이그레이션을"
description: "Windows Server 2012 r 2에는 ADFS 서비스 마이그레이션에 대 한 지침을 제공 합니다."
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/10/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 478729a7b6560beba5f04a1a15ad035561ad31f0
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="migrate-active-directory-federation-services-role-services-to-windows-server-2012-r2"></a>Windows Server 2012 r 2 Active Directory Federation Services 역할 서비스 마이그레이션을
 이 문서는 다음과 같은 역할 서비스 Active Directory Federation Services (ADFS) Windows Server 2012 r 2를 설치 하는 하 게 마이그레이션하는 지침을 제공 합니다.  
  
-   Windows Server 2008 또는 Windows Server 2008 R2에 설치 된 광고 FS 2.0 federation 서버  
  
-   Windows Server 2012에 설치 된 광고 FS federation 서버  
  
## <a name="supported-migration-scenarios"></a>지원 되는 마이그레이션 시나리오  
 이 가이드 마이그레이션 지침 다음 작업 중으로 구성 됩니다.  
  
-   Windows Server 2008, Windows Server 2008 R2 또는 Windows Server 2012에서 실행 하는 서버에서 ADFS 2.0 구성 데이터 내보내기  
  
-   Windows Server 2012 r 2에 Windows Server 2008, Windows Server 2008 R2 또는 Windows Server 2012에서이 서버 운영 체제의 제자리에 업그레이드를 수행 합니다. 
  
-   다시 원래 ADFS 구성 하 고 남은 ADFS 복원 설정에서이 서버, Windows Server 2012 r 2를 설치 하는 ADFS 서버 역할 실행 되는 서비스입니다.  
  
 이 가이드 지침 마이그레이션 여러 역할을 실행 하는 서버에 포함 되지 않습니다. 서버 여러 역할을 실행 중인 경우 다른 역할 마이그레이션 가이드에 제공 된 정보에 따라 서버 환경에 특정 사용자 지정 마이그레이션 프로세스를 디자인 하는 것이 좋습니다. 사용할 수 있는 추가 역할 마이그레이션 가이드는 [Windows Server 마이그레이션 포털](https://go.microsoft.com/fwlink/?LinkId=247608)합니다.  
  
### <a name="supported-operating-systems"></a>지원 되는 운영 체제  
 서버 운영 체제 대상:  
  
 Windows Server 2012 R2 (Server Core 및 전체 설치 옵션)  
  
 서버 프로세서 대상:  
  
 x64 기반  
  
|원본 서버 프로세서|원본 서버 운영 체제|  
|-----------------------------|------------------------------------|  
|x86-또는 x64-기반| Windows Server 2008, 전체 및 서버 Core 설치 옵션|  
|x64 기반|Windows Server 2008 R2|  
|x64 기반|Windows Server 2008 r 2의 서버 Core 설치 옵션|  
|x64 기반|서버 Core 및 Windows Server 2012 전체 설치 옵션|  
  
> [!NOTE]
>  -   위의 표에 나열 된 운영 체제의 버전은 지원 되는 서비스 팩 및 운영 체제의 오래 된 조합입니다.  
> -   Windows Server 운영 체제의 Foundation, 표준, Enterprise 및 Datacenter edition 소스 또는 대상 서버도 지원 됩니다.  
> -   마이그레이션 사이의 물리적 운영 체제 및 가상 운영 체제 지원 됩니다.  
  
### <a name="supported-ad-fs-role-services-and-features"></a>지원 되는 ADFS 역할 서비스 및 기능  
 다음 표에서 ADFS 역할 서비스 및 해당 설정을이 가이드에 설명 된 마이그레이션 시나리오에 설명 합니다.  
  
|보낸 사람|ADFS Windows Server 2012 r 2를 설치 하려면|  
|----------|----------------------------------------------------------------------------------------------|  
|Windows Server 2008 또는 Windows Server 2008 R2에 설치 된 광고 FS 2.0 federation 서버|마이그레이션 같은 서버에서 지원 됩니다. 자세한 내용은 참조 하십시오.<br /><br /> [광고 FS Federation 서버 마이그레이션 준비](prepare-migrate-ad-fs-server-r2.md)<br /><br /> [마이그레이션 광고 FS Federation 서버](migrate-ad-fs-fed-server-r2.md)|  
|Windows Server 2012에 설치 된 광고 FS federation 서버|마이그레이션 같은 서버에서 지원 됩니다.  자세한 내용은 참조 하십시오.<br /><br /> [광고 FS Federation 서버 마이그레이션 준비](prepare-migrate-ad-fs-server-r2.md)<br /><br /> [마이그레이션 광고 FS Federation 서버](migrate-ad-fs-fed-server-r2.md)|  
  
## <a name="next-steps"></a>다음 단계
 [광고 FS Federation 서버 마이그레이션 준비](prepare-migrate-ad-fs-server-r2.md)   
 [마이그레이션 광고 FS Federation 서버](migrate-ad-fs-fed-server-r2.md)   
 [AD FS Federation 서버 프록시 마이그레이션](migrate-fed-server-proxy-r2.md)   
 [Windows Server 2012 r 2에 AD FS 마이그레이션 확인](verify-ad-fs-migration.md)