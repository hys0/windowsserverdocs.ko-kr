---
title: "Windows Server 2012 r 2 ADFS 광고 FS 2.0 Federation 서버 마이그레이션하 준비"
description: "Windows Server 2012 r 2에 ADFS server를 마이그레이션해야 준비 중에 대해 설명 합니다."
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/10/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 4d0ff53b9118db1dd6ba5af94b3e627bf1597e0c
ms.sourcegitcommit: 03ce78a1624dbd7f4e6abf2ec1ef185b55de29a1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/12/2017
---
# <a name="prepare-to-migrate-the-ad-fs-20-federation-server-to-ad-fs-on-windows-server-2012-r2"></a>Windows Server 2012 r 2 ADFS 광고 FS 2.0 Federation 서버 마이그레이션하 준비

이 문서에서는 Windows Server 2012 r 2 ADFS 농장 ADFS 2.0 또는 Windows Server 2012 federation 서버 팜 마이그레이션을 하는 방법을 설명 합니다.  ADFS 농장 기본 데이터베이스와 WID 또는 SQL Server 중 하나를 사용 하는 단계를 사용할 수 있습니다.  
  
-   [마이그레이션 프로세스 개요](prepare-migrate-ad-fs-server-r2.md#migrate-process-outline)  
  
-   [Windows Server 2012 r 2의 새로운 ADFS 기능](prepare-migrate-ad-fs-server-r2.md#new-ad-fs-functionality-in-windows-server-2012-r2)  
  
-   [Windows Server 2012 r 2의 광고 FS 요구 사항](prepare-migrate-ad-fs-server-r2.md#ad-fs-requirements-in-windows-server-2012-r2)  
  
-   [Windows PowerShell 제한 증가](prepare-migrate-ad-fs-server-r2.md#increasing-your-windows-powershell-limits)  
  
-   [기타 마이그레이션 작업 및 고려 사항](prepare-migrate-ad-fs-server-r2.md#other-migration-tasks-and-considerations)  
  
##  <a name="migration-process-outline"></a>마이그레이션 프로세스 개요  
 Windows Server 2012 r 2에 federation ADFS 팜 마이그레이션을 완료 다음과 같은 작업을 완료 해야 합니다.  
  
1.  녹음을 내보내고, 하면 기존 ADFS 팜에 다음과 같은 구성 데이터를 백업 합니다. 이러한 작업을 완료 하는 방법에 대 한 자세한 내용은 참조 [AD FS Federation 서버 마이그레이션하](migrate-ad-fs-fed-server-r2.md)합니다.  
  
Windows Server 2012 r 2 설치 cd \support\adfs 폴더에 있는 스크립트는 다음과 같은 설정이 마이그레이션될:  
  
-   사용자 지정 클레임 규칙 Active Directory 클레임 공급자 신뢰를 제외 하 고 제공자 신뢰를 요구합니다. 자세한 내용은 참조 [AD FS Federation 서버 마이그레이션하](migrate-ad-fs-fed-server-r2.md)합니다.  
  
-   자 신뢰를 사용 합니다.  
  
-   ADFS 생성 내부적으로, 서명한 토큰 서명 및 토큰 해독 인증서 합니다.  
  
다음 사용자 지정 설정을 수동으로 마이그레이션해야 합니다.  
  
 -   서비스 설정이 있습니다.  
  
     -   토큰 서명 비 기본 및 엔터프라이즈 또는 공용 인증 기관에서 발급 한 암호를 해독 토큰 인증서 합니다.  
  
     -   SSL 서버 인증 인증서 ADFS 하 여 사용 합니다.  
  
     -   Adfs에 사용 된 서비스 통신 인증서 (기본적으로 이것이 SSL 인증서도 하 여 동일한 인증서 합니다.  
  
      -   기본이 아닌 값 AutoCertificateRollover 또는 SSO 수명 같은 federation 서비스 속성을입니다.  
  
      -   비 기본 ADFS 끝점 설정 및 청구 설명 합니다.  
  
-   사용자 지정 Active Directory 클레임 공급자 보안에 대 한 규칙 클레임 합니다.  
  
    -   광고 FS 로그인 페이지에서 사용자 지정  
  
자세한 내용은 참조 [AD FS Federation 서버 마이그레이션하](migrate-ad-fs-fed-server-r2.md)합니다.  
  
2.  Windows Server 2012 r 2 federation 서버 팜을 만듭니다.  
  
3.  원래 구성 데이터를이 새로운 Windows Server 2012 r 2 ADFS 농장을 가져옵니다.  
  
4.  구성 하 고 ADFS 로그인 페이지를 사용자 지정 합니다.  
  
##  <a name="new-ad-fs-functionality-in-windows-server-2012-r2"></a>Windows Server 2012 r 2의 새로운 ADFS 기능  
 다음과 같은 ADFS 기능 변경 Windows Server 2012 r 2 영향 마이그레이션 FS 2.0 또는 Windows Server 2012에서 ADFS AD에서:  
  
**IIS 종속성**  
   - Windows Server 2012 r 2에서 ADFS 자체 호스트 및 IIS 설치할 필요가 없습니다. 이 변경으로 인해 다음을 기록해 확인 하세요.  
   -   이제 SSL 인증서 관리 federation 서버와 ADFS 농장의 프록시 컴퓨터에 대 한 Windows PowerShell 통해 수행 해야 합니다.  
  
**ADFS 로그인 페이지의 설정 및 사용자 지정 변경**  
-   ADFS Windows Server 2012 r 2에서에 관리자와 사용자가 로그인 환경을 개선 하기 위한 몇 가지 변경 사항이 있습니다. Adfs의 이전 버전에 있었던 IIS 호스트 웹 페이지 이제 제거 됩니다. 웹 페이지에 로그인 Adfs의 모양과 느낌 Adfs에 호스팅된 자체 및 이제에 맞게 사용자 환경을 사용자 지정할 수 있습니다. 변경 내용을 다음과 같습니다.  
    -   ADFS 로그인 환경을, 회사 이름, 로고, 그림을 및 로그인 설명의 사용자 지정을 포함 하 여 사용자 지정 합니다.  
    -   오류 메시지를 사용자 지정 합니다.  
    -   Home 영역 검색 ADFS 경험을 사용자 지정 하는 다음과 같습니다.  
        -   특정 메일 접미사 사용 하 여 사용자의 신원을 공급자를 구성 합니다.  
        -   의존 당 id 공급자 목록 구성 자 합니다.  
        -   Home 영역 검색 인트라넷에 대 한 무시 합니다.  
        -   사용자 지정 웹 테마 만드는 중입니다.  
  
로그인 페이지 Adfs의 모양과 느낌 구성에 대 한 자세한 내용은 참조 [FS 로그인 페이지 광고를 사용자 지정](../operations/AD-FS-Customization-in-Windows-Server-2016.md)합니다.  
  
웹 페이지 사용자 지정 마이그레이션할 Windows Server 2012 r 2에는 기존 ADFS 농장 사용자의 경우 Windows Server 2012 r 2에 새로운 사용자 지정 기능을 사용 하 여 마이그레이션 프로세스의 일부로 다시 만들 수 있습니다.  
  
-   **기타 변경 내용**  
  
    -   Windows Server 2012 r 2에서 Adfs에 Windows 신원을 Foundation (군) 3.5, 군 4.5 하지 삼고 있습니다. 따라서 일부 특정 기능 군 4.5 (예: Kerberos 클레임 및 동적 액세스 제어) Windows Server 2012 r 2에서 Adfs에서 지원 되지 않습니다.  
  
    -   디바이스 등록 서비스 (DRS) Windows Server 2012 r 2에서 443; 포트에서 작동합니다. ClientTLS 사용자 인증 인증서에 대 한 포트 49443에서 작동합니다.  
  
        -   특히 있는 활성, 브라우저 비 클라이언트 전송 모드 인증 인증서를 사용 하 여에 대 한 포트 443 가리키도록 하드 코딩 코드 변경 필요 49443 포트에서 사용자 인증 인증서를 사용 하 여 계속 합니다.  
  
        -   수동 응용 프로그램에 대 한 아무런 변화가 필요 ADFS 사용자 인증 인증서에 대 한 올바른 포트 리디렉션합니다 하기 때문입니다.  
  
        -   방화벽 포트는 클라이언트와 프록시 포트 49443 교통 사용자 인증 인증서에 대 한 통과할 수를 설정 해야 합니다.  
  
##  <a name="ad-fs-requirements-in-windows-server-2012-r2"></a>Windows Server 2012 r 2의 광고 FS 요구 사항  
 Windows Server 2012 r 2 ADFS 농장 성공적으로 마이그레이션을 위해 다음과 같은 요구 사항을 충족 해야 합니다.  
  
 Adfs 기능을 연합 하려는 각 컴퓨터 도메인에 가입 수 있어야 합니다.  
  
 Windows Server 2012 r 2에 실행 하는 기능을 adfs, Active Directory 도메인 다음 중 하나를 실행 해야 합니다.  
  
-   Windows Server 2012 r 2  
  
-   Windows Server 2012  
  
-   Windows Server 2008 R2  
  
-   Windows Server 2008  
  
 Adfs의 서비스 계정으로 그룹 관리 서비스 계정 (gMSA)를 사용 하려는 경우 Windows Server 2012 R2 또는 Windows Server 2012 운영 체제에서 실행 되는 귀하의 환경에 하나 이상의 도메인 컨트롤러가 있어야 합니다.  
  
 ADFS 배포의 일환으로 디바이스 등록 서비스 (DRS) Workplace Join 광고에 대해 배포할 하려는 경우 AD DS 스키마 Windows Server 2012 r 2 수준으로 업데이트 해야 합니다. 스키마를 업데이트 하는 세 가지는 다음과 같습니다.  
  
1.  기존 Active Directory 숲 속의 adprep 실행 /forestprep Windows Server 2008 이상을 실행 하는 모든 64 비트 서버에 Windows Server 2012 r 2 운영 체제 DVD의 \support\adprep 폴더에서 합니다. 이 경우 없이 추가 도메인 컨트롤러를 설치 해야 하 고 기존 도메인 컨트롤러 없이 업그레이드 해야 합니다.  
  
Adprep/forestprep를 실행 하려면 관리자 스키마 그룹, Enterprise 관리자 그룹 및 도메인 관리자 그룹 스키마 마스터 호스트 하는 도메인의의 구성원 이어야 합니다.  
  
2.  기존 Active Directory 숲 속의 Windows Server 2012 r 2를 실행 하는 도메인 컨트롤러를 설치 합니다. 이 경우에 adprep /forestprep 도메인 컨트롤러 설치의 일부로 자동으로 실행 합니다.  
  
도메인 컨트롤러 설치 하는 동안 adprep 실행 하는 데 추가 자격 증명을 지정 해야 할 수도 있습니다 /forestprep 합니다.  
  
3.  Windows Server 2012 r 2를 실행 하는 서버에 AD DS 설치 하 여 새 Active Directory 숲을 만듭니다. 이 경우에 adprep /forestprep 스키마 모든 필요한 컨테이너 및 지원 DRS 개체를 처음 만들 수는 때문에 실행할 필요가 없습니다.  
  
### <a name="sql-server-support-for-ad-fs-in-windows-server-2012-r2"></a>ADFS Windows Server 2012 r 2에서에 대 한 지원이 SQL Server  
 ADFS 농장을 만들고 사용 SQL Server 구성 데이터를 저장 하려는 경우 SQL Server 2008 및 SQL Server 2012를 포함 하 여 최신 버전을 사용할 수 있습니다.  
  
##  <a name="increasing-your-windows-powershell-limits"></a>Windows PowerShell 제한 증가  
 개 이상의 1000 주장 제공자 신뢰 하는 경우 및 당사자 ADFS 팜 신뢰 또는 Windows PowerShell 제한 늘려야 ADFS 마이그레이션 가져오기 내보내기/도구를 실행 하는 동안 다음과 같은 오류를 표시 하는 경우:  
  
```  
'Exception of type 'System.OutOfMemoryException' was thrown. At E:\dev\ds\security\ADFSv2\Product\Migration\Export-FederationConfiguration.ps1:176 char:21 + $configData = Invoke-Command -ScriptBlock $GetConfig -Argume ...  
```  
  
 Windows PowerShell 세션 기본 메모리 제한 너무 낮습니다 때문에이 오류가 발생 합니다. Windows PowerShell 2.0 세션 기본 메모리는 150MB입니다. Windows PowerShell 3.0 세션 기본 메모리가 1024 MB 않습니다. 다음 명령을 사용 하 여 Windows PowerShell 원격 세션 메모리 제한 확인할 수 있습니다: `Get-Item wsman:localhost\Shell\MaxMemoryPerShellMB`합니다. 다음 명령을 실행 하 여 제한의 늘릴 수 있습니다: `Set-Item wsman:localhost\Shell\MaxMemoryPerShellMB 512`합니다.  
  
## <a name="other-migration-tasks-and-considerations"></a>기타 마이그레이션 작업 및 고려 사항  
 Windows Server 2012 r 2를 성공적으로 ADFS 농장 마이그레이션 하기 위해 다음 인식 하 고 있는지 확인 합니다.  
  
-   Windows Server 2012 r 2 설치 cd \support\adfs 폴더에 있는 마이그레이션 스크립트 같은 federation 서버 팜 이름 및 Windows Server 2012 r 2로 마이그레이션할 경우 사용자 레거시 ADFS 팜에 사용 되는 서비스 계정 id 이름을 유지 하는 필요 합니다.  
  
-   AD SQL Server FS 농장 마이그레이션할 경우 note 마이그레이션 프로세스 원래 구성 데이터 가져올 인증 된 새 SQL 데이터베이스 인스턴스 포함 됩니다.  
  
## <a name="next-steps"></a>다음 단계
 [Windows Server 2012 r 2 Active Directory Federation Services 역할 서비스 마이그레이션을](migrate-ad-fs-service-role-to-windows-server-r2.md)   
 [마이그레이션 광고 FS Federation 서버](migrate-ad-fs-fed-server-r2.md)   
 [AD FS Federation 서버 프록시 마이그레이션](migrate-fed-server-proxy-r2.md)   
 [Windows Server 2012 r 2에 AD FS 마이그레이션 확인](verify-ad-fs-migration.md)