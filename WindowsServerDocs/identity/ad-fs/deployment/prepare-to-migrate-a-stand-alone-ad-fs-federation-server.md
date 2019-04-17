---
title: "준비 마이그레이션해야 독립 실행형 ADFS federation 서버 하려면"
description: "Windows Server 2012 독립 실행형 ADFS 서버 마이그레이션을 준비 중에 대해 설명 합니다."
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 0c1fd2bc1026d9aee25c591cf5c91a1c59f66ee0
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
#  <a name="prepare-to-migrate-a-stand-alone-ad-fs-federation-server-or-a-single-node-ad-fs-farm"></a>독립 실행형 ADFS federation 서버 또는 단일 노드 ADFS 농장 마이그레이션을 준비합니다  
 
(동일한 서버 마이그레이션) 마이그레이션을 준비 하려면 독립 실행형 ADFS 2.0 federation 서버 또는 Windows Server 2012 단일 노드 ADFS 팜 내보내고이 서버에서 ADFS 구성 데이터를 백업 합니다.  
  
ADFS 구성 데이터를 내보내려면 다음 작업을 수행 합니다.  
  
-   [1 단계: 내보내기 서비스 설정](#step-1-export-service-settings)  
  
-   [2 단계: 제공자 신뢰 하는 내보내기 클레임](#step-2-export-claims-provider-trusts)  
  
-   [3 단계: 신뢰 파티 신뢰 내보내기](#step-3-export-relying-party-trusts)  
  
-   [4 단계: 특성 사용자 지정 상점 백업](#step-4-back-up-custom-attribute-stores)  
  
-   [웹 페이지 사용자 지정 백업 5 단계:](#step-5-back-up-webpage-customizations)  
  
## <a name="step-1-export-service-settings"></a>1 단계: 내보내기 서비스 설정  
 서비스 설정이 내보낼 다음 절차를 수행 합니다.  
  
### <a name="to-export-service-settings"></a>서비스 설정이 내보내려면  
  
1.  SSL 인증서 federation 서비스에서 사용 되는 인증서 주제 이름과 지문 값을 기록 합니다. SSL 인증서를 찾으려면 정보 IIS (인터넷 서비스) 관리를 엽니다 콘솔을 선택 **웹 사이트 기본** 왼쪽된 창에서 클릭 **바인딩을...** **작업** 창, 찾기 및 선택 https 구속력 클릭 **편집**을 차례로 클릭 하 고 **보기**합니다.  
  
> [!NOTE]
>  필요에 따라 federation 서비스 및 개인 키.pfx 파일에 사용 하는 SSL 인증서를 내보낼 수 있습니다. 자세한 내용은 참조 [내보내려면 서버 인증 인증서의 개인 키 부분](Export-the-Private-Key-Portion-of-a-Server-Authentication-Certificate.md)합니다.  
>   
>  이 인증서 개인 인증서 스토어 로컬 컴퓨터에에서 저장 되 고 운영 체제로 업그레이드에 유지 되므로 SSL 인증서 내보내는 선택 합니다.  
  
2.  ADFS 서비스 통신의 구성, 토큰 암호를 해독 및 토큰 서명 인증서를 기록 합니다.  사용 되는 모든 인증서를 보려면 Windows PowerShell 열고 ADFS cmdlet Windows PowerShell 세션에 추가 하려면 다음 명령을 실행: `PSH:>add-pssnapin “Microsoft.adfs.powershell”`합니다. 파일에서 사용 중인 모든 인증서 목록을 만들 수 다음 명령을 실행합니다 `PSH:>Get-ADFSCertificate | Out-File “.\certificates.txt”`  
  
> [!NOTE]
>  필요에 따라 토큰 서명, 토큰 암호화 또는 서비스 통신 인증서 및 생성 되지 않으면 내부적으로 모든 자체 서명된 인증서 뿐 아니라 키 내보낼 수 있습니다. Windows PowerShell를 사용 하 여 서버에 사용 중인 모든 인증서를 볼 수 있습니다. Windows PowerShell 열고 ADFS cmdlet Windows PowerShell 세션에 추가 하려면 다음 명령을 실행: `PSH:>add-pssnapin “Microsoft.adfs.powershell`합니다. 서버에서 사용 중인 모든 인증서를 보려면 다음 명령을 실행 `PSH:>Get-ADFSCertificate`합니다. 이 명령을 출력 각 인증서의 스토어 위치를 지정 하는 StoreLocation 및 StoreName 값을 포함 합니다. 에 대 한 지침을 사용할 수 있습니다 [내보내려면 서버 인증 인증서의 개인 키 부분](Export-the-Private-Key-Portion-of-a-Server-Authentication-Certificate.md) .pfx 파일을 각 인증서 및 개인 키를 내보내려면 합니다.  
>   
>  이러한 인증서 내보낼 때문에 선택적 모든 외부 인증서 운영 체제로 업그레이드 하는 동안 그대로 유지 됩니다.  
  
3.  AD 내보내기 FS 2.0 federation 서비스 속성을 federation 서비스 federation 서비스 이름, 이름과 federation 서버 식별자 파일을 표시합니다.  
  
Federation 서비스 속성을 내보내려면 Windows PowerShell 열고 ADFS cmdlet Windows PowerShell 세션에 추가 하려면 다음 명령을 실행: `PSH:>add-pssnapin “Microsoft.adfs.powershell”`합니다. Federation 서비스 속성 내보낼 다음 명령을 실행: `PSH:> Get-ADFSProperties | Out-File “.\properties.txt”`합니다.  
  
출력 파일에는 다음과 같은 구성 중요 한 값 포함 됩니다.  
  
    
|**Get ADFSProperties 들이 보고 federation 서비스 속성 이름**|**ADFS management console에서 federation 서비스 속성 이름**|
|------|------|
|호스트|Federation 서비스 이름|  
|식별자|Federation 서비스 id|  
|표시 이름|Federation 서비스 표시 이름|  
  
4.  응용 프로그램 구성 파일을 백업 합니다. 다른 설정 중에서이 파일 정책 데이터베이스 연결 문자열을 포함 합니다.  
  
응용 프로그램 구성 파일을 백업 하려면 수동으로 복사 해야는 `%programfiles%\Active Directory Federation Services 2.0\Microsoft.IdentityServer.Servicehost.exe.config` 파일을 백업 하는 서버에 안전한 위치에 있습니다.  
  
> [!NOTE]
>  기록해 데이터베이스 연결 문자열이이 파일에서 바로 뒤 "policystore 연결 문자열 ="). 연결 문자열 SQL Server 데이터베이스를 지정 하는 경우 값 federation 서버에 원래 ADFS 구성 복원 하는 경우 필요 합니다.  
>   
>  다음은 WID 연결 문자열의 예: `“Data Source=\\.\pipe\mssql$microsoft##ssee\sql\query;Initial Catalog=AdfsConfiguration;Integrated Security=True"`합니다. 다음은 SQL Server 연결 문자열의 예: `"Data Source=databasehostname;Integrated Security=True"`합니다.  
  
5.  ADFS 2.0 federation 서비스 계정의 id 및이 계정의 암호를 기록 합니다.  
  
Id 값을 찾으려면 검사는 **사용자로 로그온** 열 **광고 FS 2.0 Windows 서비스** 에 **서비스** 콘솔 하 고 수동으로이 값을 기록 합니다.  
  
> [!NOTE]
>  독립 실행형 federation 서비스에 대 한 기본 제공 네트워크 서비스 계정을 사용 됩니다.  이 경우에 암호가 필요는 없습니다.  
  
6.  파일에 사용 가능한 ADFS 끝점 목록을 내보냅니다.  
  
이렇게 하려면 Windows PowerShell 열고 ADFS cmdlet Windows PowerShell 세션에 추가 하려면 다음 명령을 실행: `PSH:>add-pssnapin “Microsoft.adfs.powershell”`합니다. 파일에 사용 가능한 ADFS 끝점 목록을 내보낼 다음 명령을 실행: `PSH:> Get-ADFSEndpoint | Out-File “.\endpoints.txt”`합니다.  
  
7.  모든 사용자 지정 클레임 설명을 파일 내보냅니다.  
  
이렇게 하려면 Windows PowerShell 열고 ADFS cmdlet Windows PowerShell 세션에 추가 하려면 다음 명령을 실행: `PSH:>add-pssnapin “Microsoft.adfs.powershell”`합니다. 모든 사용자 지정 클레임 설명을 파일 내보낼 다음 명령을 실행: `Get-ADFSClaimDescription | Out-File “.\claimtypes.txt”`합니다.  
  
##  <a name="step-2-export-claims-provider-trusts"></a>2 단계: 제공자 신뢰 하는 내보내기 클레임  
 클레임 제공자 신뢰를 내보내려면 다음 절차를 수행 합니다.  
  
### <a name="to-export-claims-provider-trusts"></a>클레임 제공자 신뢰를 내보내려면  
  
1.  모든 청구 제공자 신뢰를 내보내려면 Windows PowerShell 사용할 수 있습니다. Windows PowerShell 열고 ADFS cmdlet Windows PowerShell 세션에 추가 하려면 다음 명령을 실행: `PSH:>add-pssnapin “Microsoft.adfs.powershell”`합니다. 모든 청구 제공자 신뢰 내보낼 다음 명령을 실행: `PSH:>Get-ADFSClaimsProviderTrust | Out-File “.\cptrusts.txt”`합니다.  
  
## <a name="step-3-export-relying-party-trusts"></a>3 단계: 신뢰 파티 신뢰 내보내기  
 신뢰 파티 신뢰를 내보내려면 다음 절차를 수행 합니다.  
  
### <a name="to-export-relying-party-trusts"></a>신뢰 파티 신뢰를 내보내려면  
  
1.  모든 신뢰 파티 신뢰 내보내고 Windows PowerShell 열고 ADFS cmdlet Windows PowerShell 세션에 추가 하려면 다음 명령을 실행: `PSH:>add-pssnapin “Microsoft.adfs.powershell”`합니다. 모든 신뢰 파티 신뢰 내보낼 다음 명령을 실행:`PSH:>Get-ADFSRelyingPartyTrust | Out-File “.\rptrusts.txt”`합니다.  
  
## <a name="step-4-back-up-custom-attribute-stores"></a>4 단계: 특성 사용자 지정 상점 백업  
 Adfs에서 사용 중인 Windows PowerShell를 사용 하 여 사용자 지정 된 특성 스토어에 대 한 정보를 찾을 수 있습니다. Windows PowerShell 열고 ADFS cmdlet Windows PowerShell 세션에 추가 하려면 다음 명령을 실행: `PSH:>add-pssnapin “Microsoft.adfs.powershell”`합니다. 사용자 지정 된 특성 스토어에 대 한 정보를 찾으려면 다음 명령을 실행: `PSH:>Get-ADFSAttributeStore`합니다. 업그레이드 또는 사용자 지정 된 특성 스토어 마이그레이션할 단계 다릅니다.  
  
## <a name="step-5-back-up-webpage-customizations"></a>웹 페이지 사용자 지정 백업 5 단계:  
 모든 웹 페이지 사용자 지정을 백업 하려면 ADFS 웹 페이지를 복사 및 **web.config** 가상 경로 매핑됩니다 디렉터리의 파일 **"/ adfs/1!"** iis에서 합니다. 기본적으로에는 **%systemdrive%\inetpub\adfs\ls** 디렉터리 합니다.  

## <a name="next-steps"></a>다음 단계
 [광고 FS 2.0 Federation 서버 마이그레이션을 준비합니다](prepare-to-migrate-ad-fs-fed-server.md)   
 [광고 FS 2.0 Federation 서버 프록시 마이그레이션을 준비합니다](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [광고 FS 2.0 Federation Server를 마이그레이션해야](migrate-the-ad-fs-fed-server.md)   
 [광고 FS 2.0 Federation 서버 프록시 마이그레이션](migrate-the-ad-fs-2-fed-server-proxy.md)   
 [광고 FS 1.1 웹 에이전트 마이그레이션](migrate-the-ad-fs-web-agent.md)