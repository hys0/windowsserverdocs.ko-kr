---
title: Windows Server 2012 R2로 Active Directory Federation Services 역할 서비스 마이그레이션
description: Windows Server 2012 R2로 AD FS 서비스를 마이그레이션하기 위한 지침을 제공 합니다.
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/10/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 34eab7d5e0325a4ad8268a900738eea30b944ebb
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66444562"
---
# <a name="migrate-active-directory-federation-services-role-services-to-windows-server-2012-r2"></a>Windows Server 2012 R2로 Active Directory Federation Services 역할 서비스 마이그레이션
 이 문서는 Active Directory Federation Services (AD FS) Windows Server 2012 R2와 함께 설치 되는에 다음 역할 서비스를 마이그레이션하는 지침을 제공 합니다.  
  
-   Windows Server 2008 또는 Windows Server 2008 R2에 설치 된 AD FS 2.0 페더레이션 서버  
  
-   Windows Server 2012에 설치 된 AD FS 페더레이션 서버  
  
## <a name="supported-migration-scenarios"></a>지원되는 마이그레이션 시나리오  
 이 가이드의 마이그레이션 지침은 다음 작업으로 구성됩니다.  
  
- Windows Server 2008, Windows Server 2008 R2 또는 Windows Server 2012를 실행 하는 서버에서 AD FS 2.0 구성 데이터 내보내기  
  
- Windows Server 2012 R2로 Windows Server 2008, Windows Server 2008 R2 또는 Windows Server 2012에서이 서버의 운영 체제의 현재 위치 업그레이드를 수행 합니다. 
  
- 원래 AD FS 구성을 다시 만들고 나머지 AD FS를 복원 서비스는 이제 Windows Server 2012 R2와 함께 설치 된 AD FS 서버 역할을 실행 하는이 서버에서 설정 합니다.  
  
  여러 역할을 실행하는 서버를 마이그레이션하는 방법에 대한 지침은 이 가이드에 수록되어 있지 않습니다. 서버에서 여러 역할을 실행하는 경우 다른 역할 마이그레이션 가이드의 내용을 참조하여 해당 서버 환경에 적합한 사용자 지정 마이그레이션 프로세스를 계획하는 것이 좋습니다. 추가 역할에 대한 마이그레이션 가이드는 [Windows Server 마이그레이션 포털](https://go.microsoft.com/fwlink/?LinkId=247608)에서 확인할 수 있습니다.  
  
### <a name="supported-operating-systems"></a>지원되는 운영 체제  
 대상 서버 운영 체제:  
  
 Windows Server 2012 R2 (Server Core 및 전체 설치 옵션)  
  
 대상 서버 프로세서:  
  
 x64 기반  
  
|원본 서버 프로세서|원본 서버 운영 체제|  
|-----------------------------|------------------------------------|  
|x86 또는 x64 기반| Windows Server 2008, 전체 및 Server Core 설치 옵션|  
|x64 기반|Windows Server 2008 R2|  
|x64 기반|Windows Server 2008 R2의 server Core 설치 옵션|  
|x64 기반|Server Core 및 Windows Server 2012의 전체 설치 옵션|  
  
> [!NOTE]
> - 위 표에 나와 있는 운영 체제 버전은 지원되는 가장 이전 버전의 운영 체제와 서비스 팩의 조합입니다.  
>   -   Windows Server 운영 체제 Foundation, Standard, Enterprise 및 Datacenter 버전은 원본 또는 대상 서버로 지원 됩니다.  
>   -   실제 운영 체제와 가상 운영 체제 간 마이그레이션이 지원됩니다.  
  
### <a name="supported-ad-fs-role-services-and-features"></a>지원 되는 AD FS 역할 서비스 및 기능  
 다음 표에서 AD FS 역할 서비스 및이 가이드에 설명 되어 있는 해당 설정의 마이그레이션 시나리오를 설명 합니다.  
  
|보낸 사람|Windows Server 2012 R2를 사용 하 여 설치 된 AD FS에|  
|----------|----------------------------------------------------------------------------------------------|  
|Windows Server 2008 또는 Windows Server 2008 R2에 설치 된 AD FS 2.0 페더레이션 서버|동일 서버에서의 마이그레이션이 지원됩니다. 참조 항목:<br /><br /> [AD FS 페더레이션 서버 마이그레이션 준비](prepare-migrate-ad-fs-server-r2.md)<br /><br /> [AD FS 페더레이션 서버 마이그레이션](migrate-ad-fs-fed-server-r2.md)|  
|Windows Server 2012에 설치 된 AD FS 페더레이션 서버|동일 서버에서의 마이그레이션이 지원됩니다.  자세한 내용은 다음을 참조하세요.<br /><br /> [AD FS 페더레이션 서버 마이그레이션 준비](prepare-migrate-ad-fs-server-r2.md)<br /><br /> [AD FS 페더레이션 서버 마이그레이션](migrate-ad-fs-fed-server-r2.md)|  
  
## <a name="next-steps"></a>다음 단계
 [AD FS 페더레이션 서버 마이그레이션 준비](prepare-migrate-ad-fs-server-r2.md)   
 [AD FS 페더레이션 서버 마이그레이션](migrate-ad-fs-fed-server-r2.md)   
 [AD FS 페더레이션 서버 프록시 마이그레이션](migrate-fed-server-proxy-r2.md)   
 [Windows Server 2012 R2로 AD FS 마이그레이션 확인](verify-ad-fs-migration.md)