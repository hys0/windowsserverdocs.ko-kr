---
title: "Windows Server 2012 Active Directory Federation Services 역할 서비스 마이그레이션을"
description: "Windows Server 2012 ADFS 서비스 마이그레이션에 대 한 지침을 제공 합니다."
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 2b44ed504c2b3dc8a8ac0ca9648f1db9e362e075
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="migrate-active-directory-federation-services-role-services-to-windows-server-2012"></a>Windows Server 2012 Active Directory Federation Services 역할 서비스 마이그레이션을

다음 Active Directory Federation Services (ADFS) Windows Server 2012에서 다음과 같은 역할 서비스 마이그레이션에 지침을 제공 합니다.  
  
-   광고 FS 1.1 Windows 토큰 따라 에이전트와 광고 FS 1.1 클레임 인식 에이전트가 Windows Server 2008 또는 Windows Server 2008 R2 설치  
  
-   광고 FS 2.0 federation 서버 및 Windows Server 2008 또는 Windows Server 2008 R2에 설치 된 ADFS 2.0 federation 서버 프록시    
  
## <a name="supported-migration-scenarios"></a>지원 되는 마이그레이션 시나리오  
 마이그레이션 지침은 다음과 같은 작업이 포함 되어 있습니다.  
  
-   Windows Server 2008 R2 또는 Windows Server 2008를 실행 하는 서버에서 ADFS 2.0 구성 데이터 내보내기  
  
-   Windows Server 2012를 Windows Server 2008 또는 Windows Server 2008 R2이 서버 운영 체제의 제자리에 업그레이드를 수행 합니다.
  
-   다시 원래 ADFS 구성 하 고 남은 ADFS 복원 설정에서이 서버, Windows Server 2012를 설치 하는 ADFS 서버 역할 실행 되는 서비스입니다.  
  
 이 가이드 지침 마이그레이션 여러 역할을 실행 하는 서버에 포함 되지 않습니다. 서버 여러 역할을 실행 중인 경우 다른 역할 마이그레이션 가이드에 제공 된 정보에 따라 서버 환경에 특정 사용자 지정 마이그레이션 프로세스를 디자인 하는 것이 좋습니다. 사용할 수 있는 추가 역할 마이그레이션 가이드는 [Windows Server 마이그레이션 포털](https://go.microsoft.com/fwlink/?LinkId=247608)합니다.  
  
## <a name="supported-operating-systems"></a>지원 되는 운영 체제  
 **서버 운영 체제 대상:**  
  

-  (Server Core 및 전체 설치 옵션) Windows Server 2008 R2 또는 Windows Server 2012  
  
 **서버 프로세서 대상:**  
  

-  x64 기반  
  
|원본 서버 프로세서|원본 서버 운영 체제|  
|-----|-----|  
|x86-또는 x64-기반|Windows Server 2003 서비스 팩 2|  
|x86-또는 x64-기반|Windows Server 2003 R2|  
|x86-또는 x64-기반|Windows Server 2008, 전체 및 서버 Core 설치 옵션|  
|x64 기반|Windows Server 2008 R2|  
|x64 기반|Windows Server 2008 r 2의 서버 Core 설치 옵션|  
|x64 기반|서버 Core 및 Windows Server 2012 전체 설치 옵션|  
  
> [!NOTE]
>  -   위의 표에 나열 된 운영 체제의 버전은 지원 되는 서비스 팩 및 운영 체제의 오래 된 조합입니다.  
> -   Windows Server 운영 체제의 Foundation, 표준, Enterprise 및 Datacenter edition 소스 또는 대상 서버도 지원 됩니다.  
> -   마이그레이션 사이의 물리적 운영 체제 및 가상 운영 체제 지원 됩니다.  
  
### <a name="supported-ad-fs-role-services-and-features"></a>지원 되는 ADFS 역할 서비스 및 기능  
 다음 표에서 ADFS 역할 서비스 및 해당 설정을이 가이드에 설명 된 마이그레이션 시나리오에 설명 합니다.  
  
|보낸 사람|ADFS Windows Server 2012를 설치 하려면|  
|----------|-----|  
|Windows Server 2003 R2과 함께 설치 광고 FS 1.0 federation 서버|마이그레이션이 없습니다.|  
|광고 FS 1.0 federation 서버 프록시 Windows Server 2003 R2과 함께 설치|마이그레이션이 없습니다.|  
|AD FS 1.0 Windows 토큰 따라 에이전트와 Windows Server 2003 R2 함께 설치|마이그레이션이 없습니다.|  
|Windows Server 2003 R2과 함께 설치 FS 1.0 인식 클레임 에이전트를 AD)|마이그레이션이 없습니다.|  
|Windows Server 2008 또는 Windows Server 2008 r 2와 함께 설치 된 광고 FS 1.1 federation 서버|마이그레이션이 없습니다.|  
|광고 FS 1.1 federation 서버 프록시 Windows Server 2008 또는 Windows Server 2008 r 2를 사용 하 여 설치|마이그레이션이 없습니다.|  
|광고 FS 1.1 Windows 토큰 따라 에이전트 Windows Server 2008 또는 Windows Server 2008 r 2를 사용 하 여 설치|마이그레이션 같은 서버에서 지원 되지만 마이그레이션된 AD FS Windows 토큰 따라 에이전트와 Windows Server 2008 또는 Windows Server 2008 r 2를 설치 하는 ADFS 1.1 federation 서비스 있는 경우에 작동 합니다. 자세한 내용은 참조 하십시오.<br /><br /> [광고 FS 1.1 웹 에이전트 마이그레이션](migrate-the-ad-fs-web-agent.md)<br /><br /> [Adfs와 상호 작용 1.x](Interoperating-with-AD-FS-1.x.md)|  
|Windows Server 2008 또는 Windows Server 2008 R2과 함께 설치 FS 1.1 인식 클레임 에이전트를 AD)|마이그레이션 같은 서버에서 지원 됩니다. 다음으로 마이그레이션된 ADFS 1.1 클레임 인식 웹 에이전트 작동 합니다.<br /><br /> Windows Server 2008 또는 Windows Server 2008 r 2와 함께 설치 된 광고 FS 1.1 federation 서비스<br /><br /> Windows Server 2008 또는 Windows Server 2008 R2에 설치 된 ADFS 2.0 federation 서비스<br /><br /> Windows Server 2012와 함께 설치 된 ADFS federation 서비스<br /><br /> 자세한 내용은 참조 하십시오.<br /><br /> [광고 FS 1.1 웹 에이전트 마이그레이션](migrate-the-ad-fs-web-agent.md)<br /><br /> [Adfs와 상호 작용 1.x](Interoperating-with-AD-FS-1.x.md)|  
|Windows Server 2008 또는 Windows Server 2008 R2에 설치 된 광고 FS 2.0 federation 서버|마이그레이션 같은 서버에서 지원 됩니다. 자세한 내용은 참조 하십시오.<br /><br /> [광고 FS 2.0 Federation 서버 마이그레이션을 준비합니다](prepare-to-migrate-ad-fs-fed-server.md)<br /><br /> [광고 FS 2.0 Federation Server를 마이그레이션해야](migrate-the-ad-fs-fed-server.md)|  
|Windows Server 2008 또는 Windows Server 2008 R2에 설치 된 광고 FS 2.0 federation 서버 프록시|마이그레이션 같은 서버에서 지원 됩니다.  자세한 내용은 참조 하십시오.<br /><br /> [광고 FS 2.0 Federation 서버 프록시 마이그레이션을 준비합니다](prepare-to-migrate-ad-fs-fed-proxy.md)<br /><br /> [광고 FS 2.0 Federation 서버 프록시 마이그레이션](migrate-the-ad-fs-2-fed-server-proxy.md)|  
  
## <a name="see-also"></a>참조 하십시오  
 [광고 FS 2.0 Federation 서버 마이그레이션을 준비합니다](prepare-to-migrate-ad-fs-fed-server.md)   
 [광고 FS 2.0 Federation 서버 프록시 마이그레이션을 준비합니다](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [광고 FS 2.0 Federation Server를 마이그레이션해야](migrate-the-ad-fs-fed-server.md)   
 [광고 FS 2.0 Federation 서버 프록시 마이그레이션](migrate-the-ad-fs-2-fed-server-proxy.md)   
 [광고 FS 1.1 웹 에이전트 마이그레이션](migrate-the-ad-fs-web-agent.md)