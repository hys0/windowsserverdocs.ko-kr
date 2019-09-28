---
title: AD FS 2.0 페더레이션 서버를 Windows Server 2012 r 2의 AD FS로 마이그레이션 준비
description: AD FS 서버를 Windows Server 2012 r 2로 마이그레이션하도록 준비 하는 방법에 대 한 정보를 제공 합니다.
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/10/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 149e3d3fc4d4eee22fa9330475f0eed9d945f8b9
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359313"
---
# <a name="prepare-to-migrate-the-ad-fs-20-federation-server-to-ad-fs-on-windows-server-2012-r2"></a>AD FS 2.0 페더레이션 서버를 Windows Server 2012 r 2의 AD FS로 마이그레이션 준비

이 문서에서는 AD FS 2.0 또는 Windows Server 2012 페더레이션 서버 팜을 Windows Server 2012 R2 AD FS 팜으로 마이그레이션하는 방법에 대해 설명 합니다.  WID 또는 SQL Server를 기본 데이터베이스로 사용 하는 AD FS 팜에서 이러한 단계를 사용할 수 있습니다.  
  
-   [마이그레이션 프로세스 개요](prepare-migrate-ad-fs-server-r2.md#migration-process-outline)  
  
-   [Windows Server 2012 r 2의 새로운 AD FS 기능](prepare-migrate-ad-fs-server-r2.md#new-ad-fs-functionality-in-windows-server-2012-r2)  
  
-   [Windows Server 2012 r 2의 AD FS 요구 사항](prepare-migrate-ad-fs-server-r2.md#ad-fs-requirements-in-windows-server-2012-r2)  
  
-   [Windows PowerShell 제한 강화](prepare-migrate-ad-fs-server-r2.md#increasing-your-windows-powershell-limits)  
  
-   [기타 마이그레이션 작업 및 고려 사항](prepare-migrate-ad-fs-server-r2.md#other-migration-tasks-and-considerations)  
  
##  <a name="migration-process-outline"></a>마이그레이션 프로세스 개요

 AD FS 페더레이션 서버 팜을 Windows Server 2012 R2로 마이그레이션하려면 다음 작업을 완료해야 합니다.  
  
1.  기존 AD FS 팜에 다음 구성 데이터를 내보내고 기록 및 백업합니다. 이러한 작업을 완료하는 방법에 자세한 내용은 [AD FS 페더레이션 서버 마이그레이션](migrate-ad-fs-fed-server-r2.md)을 참조하십시오.  
  
다음 설정은 Windows Server 2012 R2 설치 CD의 \support\adfs 폴더에 있는 스크립트를 사용 하 여 마이그레이션합니다.  
  
-   클레임 공급자 트러스트(Active Directory 클레임 공급자 트러스트에 대한 사용자 지정 클레임 규칙 제외). 자세한 내용은 [AD FS 페더레이션 서버 마이그레이션](migrate-ad-fs-fed-server-r2.md)을 참조하십시오.  
  
-   신뢰 당사자 트러스트  
  
-   AD FS 내부적으로 생성된 자체 서명된 토큰 서명 및 토큰 암호 해독 인증서  
  
다음 사용자 지정 설정은 수동으로 마이그레이션해야 합니다.  
  
- 서비스 설정:  
  
  - 엔터프라이즈 또는 공용 인증 기관에서 발급한 기본 인증서가 아닌 토큰 서명 및 토큰 암호 해독 인증서  
  
  - AD FS에서 사용하는 SSL 서버 인증 인증서  
  
  - AD FS에서 사용하는 서비스 통신 인증서(기본적으로 SSL 인증서와 같음)  
  
    -   AutoCertificateRollover 또는 SSO 수명과 같은 페더레이션 서비스 속성에 대한 기본값이 아닌 값  
  
    -   기본 설정이 아닌 AD FS 끝점 설정 및 클레임 설명  
  
-   Active Directory 클레임 공급자 트러스트에 대한 사용자 지정 클레임 규칙  
  
    -   AD FS 로그인 페이지 사용자 지정  
  
자세한 내용은 [AD FS 페더레이션 서버 마이그레이션](migrate-ad-fs-fed-server-r2.md)을 참조하십시오.  
  
2. Windows Server 2012 R2 페더레이션 서버 팜을 만듭니다.  
  
3. 이 새 Windows Server 2012 R2 AD FS 팜으로 원래 구성 데이터를 가져옵니다.  
  
4. AD FS 로그인 페이지를 구성하고 사용자 지정합니다.  
  
##  <a name="new-ad-fs-functionality-in-windows-server-2012-r2"></a>Windows Server 2012 R2의 새로운 AD FS 기능  
 Windows Server 2012 r 2에서 다음과 같은 AD FS 기능 변경 내용은 Windows Server 2012에서 AD FS 2.0 또는 AD FS에서의 마이그레이션에 영향을 줍니다.  
  
**IIS 종속성**  
   - Windows Server 2012 R2의 AD FS는 자체 호스팅되므로 IIS를 설치할 필요가 없습니다. 이 변경 사항의 결과로서 다음 내용을 염두에 두어야 합니다.  
   -   AD FS 팜의 페더레이션 서버와 프록시 컴퓨터 모두에 대한 SSL 인증서 관리를 이제 Windows PowerShell을 통해 수행해야 합니다.  
  
**AD FS 로그인 페이지의 설정 및 사용자 지정에 대 한 변경 내용**  
-   Windows Server 2012 r 2의 AD FS에는 관리자와 사용자의 로그인 환경을 개선 하기 위한 몇 가지 변경 사항이 있습니다. 이전 버전의 AD FS에서 제공된 IIS 호스팅 웹 페이지가 이제 제거되었습니다. AD FS 로그인 웹 페이지의 모양과 느낌이 AD FS에서 자체 호스팅되며, 이제 사용자 환경에 맞게 사용자 지정할 수 있습니다. 변경 사항에는 다음이 포함됩니다.  
    -   회사 이름, 로고, 그림 및 로그인 설명에 대한 사용자 지정을 비롯한 AD FS 로그인 환경 사용자 지정  
    -   오류 메시지 사용자 지정  
    -   다음을 비롯한 AD FS 홈 영역 검색 환경 사용자 지정  
        -   특정 메일 접미사를 사용하도록 ID 공급자 구성  
        -   신뢰 당사자별 ID 공급자 목록 구성  
        -   인트라넷에 대한 홈 영역 검색 무시  
        -   사용자 지정 웹 테마 만들기  
  
AD FS 로그인 페이지의 모양과 느낌을 구성하는 방법에 대한 자세한 지침은 [Customizing the AD FS Sign-in Pages](../operations/AD-FS-Customization-in-Windows-Server-2016.md)을 참조하세요.  
  
기존 AD FS 팜에 Windows Server 2012 r 2로 마이그레이션하려는 웹 페이지 사용자 지정이 있는 경우 Windows Server 2012 r 2의 새로운 사용자 지정 기능을 사용 하 여 마이그레이션 프로세스의 일부로 다시 만들 수 있습니다.  
  
-   **기타 변경 내용**  
  
    -   Windows Server 2012 r 2의 AD FS는 WIF 4.5가 아니라 WIF (Windows Identity Foundation) 3.5을 기반으로 합니다. 따라서 WIF 4.5의 일부 특정 기능 (예: Kerberos 클레임 및 동적 액세스 제어)은 Windows Server 2012 r 2의 AD FS에서 지원 되지 않습니다.  
  
    -   Windows Server 2012 r 2의 DRS (Device Registration Service)는 포트 443에서 작동 합니다. 사용자 인증서 인증을 위한 ClientTLS는 포트 49443에서 작동 합니다.  
  
        -   포트 443을 가리키도록 특별히 하드 코드된 인증서 전송 모드 인증을 사용하는 브라우저가 아닌 활성 클라이언트의 경우, 포트 49443에서 사용자 인증서 인증을 계속 사용하려면 코드를 변경해야 합니다.  
  
        -   수동 응용 프로그램의 경우 AD FS에서 사용자 인증서 인증을 위한 올바른 포트로 리디렉션하기 때문에 별도의 변경 작업이 필요 없습니다.  
  
        -   클라이언트와 프록시 간의 방화벽 포트에서 사용자 인증서 인증을 위해 포트 49443 트래픽의 통과를 지원합니다.  
  
##  <a name="ad-fs-requirements-in-windows-server-2012-r2"></a>Windows Server 2012 R2의 AD FS 요구 사항  
 AD FS 팜을 Windows Server 2012 r 2로 마이그레이션하려면 다음 요구 사항을 충족 해야 합니다.  
  
 AD FS 작동 하려면 페더레이션 할 각 컴퓨터를 도메인에 가입 시켜야 합니다.  
  
 Windows Server 2012 r 2에서 실행 되는 AD FS 작동 하려면 Active Directory 도메인에서 다음 중 하나를 실행 해야 합니다.  
  
- Windows Server 2012 R2  
  
- Windows Server 2012  
  
- Windows Server 2008 R2  
  
- Windows Server 2008  
  
  AD FS에 대 한 서비스 계정으로 gMSA (그룹 관리 서비스 계정)를 사용 하려는 경우 Windows Server 2012 또는 Windows Server 2012 R2 운영 체제에서 실행 되는 환경에 도메인 컨트롤러가 하나 이상 있어야 합니다.  
  
  AD FS 배포의 일부로 AD Workplace Join에 대 한 DRS (Device Registration Service)를 배포 하려는 경우 AD DS 스키마를 Windows Server 2012 R2 수준으로 업데이트 해야 합니다. 스키마를 업데이트하는 방법에는 다음 세 가지가 있습니다.  
  
1.  기존 Active Directory 포리스트에서 Windows Server 2008 이상을 실행 하는 64 비트 서버에서 Windows Server 2012 R2 운영 체제 DVD의 \support\adprep 폴더에 있는 adprep/forestprep를 실행 합니다. 이 경우 추가 도메인 컨트롤러를 설치하거나 기존 도메인 컨트롤러를 업그레이드할 필요가 없습니다.  
  
adprep/forestprep를 실행하려면 스키마 마스터를 호스트하는 도메인의 Schema Admins 그룹, Enterprise Admins 그룹 및 Domain Admins 그룹의 구성원이어야 합니다.  
  
2. 기존 Active Directory 포리스트에서 Windows Server 2012 r 2를 실행 하는 도메인 컨트롤러를 설치 합니다. 이 경우에는 adprep /forestprep가 도메인 컨트롤러 설치의 일부로 자동으로 실행됩니다.  
  
도메인 컨트롤러 설치 중 adprep /forestprep를 실행하기 위해 추가 자격 증명을 지정해야 할 수도 있습니다.  
  
3. Windows Server 2012 r 2를 실행 하는 서버에 AD DS를 설치 하 여 새 Active Directory 포리스트를 만듭니다. 이 경우 DRS를 지원하는 데 필요한 모든 컨테이너 및 개체와 함께 스키마가 초기에 만들어지므로 adprep /forestprep를 실행할 필요가 없습니다.  
  
### <a name="sql-server-support-for-ad-fs-in-windows-server-2012-r2"></a>Windows Server 2012 R2의 AD FS에 대한 SQL Server 지원  
 AD FS 팜을 만들고 SQL Server를 사용하여 구성 데이터를 저장하려면 SQL Server 2008 이상(SQL Server 2012 포함)을 사용하면 됩니다.  
  
##  <a name="increasing-your-windows-powershell-limits"></a>Windows PowerShell 제한 증가  
 AD FS 팜에 1,000개가 넘는 클레임 공급자 트러스트와 신뢰 당사자 트러스트가 있는 경우 또는 AD FS 마이그레이션 내보내기/가져오기 도구를 실행하려고 할 때 다음 오류가 나타나는 경우 Windows PowerShell 제한을 늘려야 합니다.  
  
```  
'Exception of type 'System.OutOfMemoryException' was thrown. At E:\dev\ds\security\ADFSv2\Product\Migration\Export-FederationConfiguration.ps1:176 char:21 + $configData = Invoke-Command -ScriptBlock $GetConfig -Argume ...  
```  
  
 이 오류는 Windows PowerShell 세션 기본 메모리 제한은 너무 낮기 때문에 발생합니다. Windows PowerShell 2.0에서는 세션 기본 메모리가 150MB이고, Windows PowerShell 3.0에서는 세션 기본 메모리가 1024MB입니다. `Get-Item wsman:localhost\Shell\MaxMemoryPerShellMB`명령을 사용하여 Windows PowerShell 원격 세션 메모리 제한을 확인할 수 있습니다. 제한을 늘리려면 `Set-Item wsman:localhost\Shell\MaxMemoryPerShellMB 512` 명령을 실행합니다.  
  
## <a name="other-migration-tasks-and-considerations"></a>기타 마이그레이션 작업 및 고려 사항  
 AD FS 팜을 Windows Server 2012 R2로 마이그레이션하려면 다음 사항을 알아야 합니다.  
  
-   Windows Server 2012 R2 설치 CD의 \support\adfs 폴더에 있는 마이그레이션 스크립트를 사용 하려면 Windows로 마이그레이션할 때 레거시 AD FS 팜에서 사용한 것과 동일한 페더레이션 서버 팜 이름 및 서비스 계정 id 이름을 유지 해야 합니다. 서버 2012 R2.  
  
-   SQL Server AD FS 팜을 마이그레이션하려는 경우 마이그레이션 프로세스에 원래 구성 데이터를 가져와야 하는 새 SQL 데이터베이스 인스턴스를 만드는 과정이 포함되어 있음을 알아야 합니다.  
  
## <a name="next-steps"></a>다음 단계
 [Active Directory Federation Services 역할 서비스를 Windows Server 2012 r 2로 마이그레이션](migrate-ad-fs-service-role-to-windows-server-r2.md)   
 [AD FS 페더레이션 서버 마이그레이션](migrate-ad-fs-fed-server-r2.md)   
 [AD FS 페더레이션 서버 프록시 마이그레이션](migrate-fed-server-proxy-r2.md)   
 [Windows Server 2012 r 2로 AD FS 마이그레이션 확인](verify-ad-fs-migration.md)