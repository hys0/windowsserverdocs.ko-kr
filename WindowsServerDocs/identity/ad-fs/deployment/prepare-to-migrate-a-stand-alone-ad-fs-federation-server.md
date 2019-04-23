---
title: 독립 실행형 AD FS 페더레이션 서버 마이그레이션 준비
description: 독립 실행형 AD FS 서버를 Windows Server 2012로 마이그레이션할 준비 하기에 정보를 제공 합니다.
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 0c1fd2bc1026d9aee25c591cf5c91a1c59f66ee0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59834494"
---
#  <a name="prepare-to-migrate-a-stand-alone-ad-fs-federation-server-or-a-single-node-ad-fs-farm"></a>독립 실행형 AD FS 페더레이션 서버 또는 단일 노드 AD FS 팜 마이그레이션 준비  
 
마이그레이션 (동일 서버 마이그레이션) 하기 위해 준비 하려면 독립 실행형 AD FS 2.0 페더레이션 서버 또는 단일 노드 AD FS 팜을 Windows Server 2012 내보내고이 서버에서 AD FS 구성 데이터를 백업 합니다.  
  
AD FS 구성 데이터를 내보내려면 다음 작업을 수행합니다.  
  
-   [1단계:  서비스 설정 내보내기](#step-1-export-service-settings)  
  
-   [2단계:  클레임 공급자 트러스트 내보내기](#step-2-export-claims-provider-trusts)  
  
-   [3 단계:  신뢰 당사자 트러스트 내보내기](#step-3-export-relying-party-trusts)  
  
-   [4 단계:  사용자 지정 특성 저장소 백업](#step-4-back-up-custom-attribute-stores)  
  
-   [5단계:  웹 페이지 사용자 지정 백업](#step-5-back-up-webpage-customizations)  
  
## <a name="step-1-export-service-settings"></a>1단계: 서비스 설정 내보내기  
 서비스 설정을 내보내려면 다음 절차를 수행합니다.  
  
### <a name="to-export-service-settings"></a>서비스 설정을 내보내려면  
  
1.  페더레이션 서비스에서 사용하는 SSL 인증서의 인증서 주체 이름 및 지문 값을 기록합니다. SSL 인증서를 찾으려면 IIS(인터넷 정보 서비스) 관리 콘솔을 열고 왼쪽 창에서 **기본 웹 사이트** 를 선택합니다. 그런 다음 **동작** 에 **작업** 찾기 및 선택 https 바인딩, 창 클릭 **편집**를 클릭 하 고 **보기**합니다.  
  
> [!NOTE]
>  필요한 경우 페더레이션 서비스에서 사용되는 SSL 인증서와 해당 개인 키를 .pfx 파일로 내보낼 수도 있습니다. 자세한 내용은 [서버 인증 인증서의 개인 키 부분 내보내기](Export-the-Private-Key-Portion-of-a-Server-Authentication-Certificate.md)를 참조하세요.  
>   
>  SSL 인증서 내보내기는 선택 사항입니다. 이 인증서는 로컬 컴퓨터 개인 인증서 저장소에 저장되고 운영 체제 업그레이드 중에 유지되기 때문입니다.  
  
2.  AD FS 서비스 통신, 토큰 암호 해독 및 토큰 서명 인증서의 구성을 기록합니다.  사용되는 모든 인증서를 보려면 Windows PowerShell을 열고 `PSH:>add-pssnapin “Microsoft.adfs.powershell”`명령을 실행하여 Windows PowerShell 세션에 AD FS cmdlet을 추가합니다. 그런 다음 `PSH:>Get-ADFSCertificate | Out-File “.\certificates.txt”` 명령을 실행하여 파일에서 사용 중인 모든 인증서 목록을 만듭니다.  
  
> [!NOTE]
>  필요한 경우 자체 서명된 모든 인증서 외에 내부적으로 생성되지 않은 토큰 서명, 토큰 암호화 또는 서비스 통신 인증서 및 키도 내보낼 수 있습니다. Windows PowerShell을 사용하여 서버에서 사용 중인 모든 인증서를 볼 수 있습니다. Windows PowerShell을 열고 `PSH:>add-pssnapin “Microsoft.adfs.powershell`명령을 실행하여 Windows PowerShell 세션에 AD FS cmdlet을 추가합니다. 그런 다음 `PSH:>Get-ADFSCertificate` 명령을 실행하여 서버에서 사용 중인 모든 인증서를 확인합니다. 이 명령의 출력은 각 인증서의 저장소 위치를 지정하는 StoreLocation 및 StoreName 값을 포함합니다. 그런 다음 [서버 인증 인증서의 개인 키 부분 내보내기](Export-the-Private-Key-Portion-of-a-Server-Authentication-Certificate.md)의 지침을 사용하여 각 인증서와 해당 개인 키를.pfx 파일로 내보낼 수 있습니다.  
>   
>  외부 인증서 내보내기는 선택 사항입니다. 모든 외부 인증서는 운영 체제 업그레이드 중에 유지되기 때문입니다.  
  
3.  페더레이션 서비스 이름, 페더레이션 서비스 표시 이름 및 페더레이션 서버 식별자와 같은 AD FS 2.0 페더레이션 서비스 속성을 파일로 내보냅니다.  
  
페더레이션 서비스 속성을 내보내려면 Windows PowerShell을 열고 `PSH:>add-pssnapin “Microsoft.adfs.powershell”`명령을 실행하여 Windows PowerShell 세션에 AD FS cmdlet을 추가합니다. 그런 다음 `PSH:> Get-ADFSProperties | Out-File “.\properties.txt”` 명령을 실행하여 페더레이션 서비스 속성을 내보냅니다.  
  
출력 파일에 다음과 같은 중요한 구성 값이 포함됩니다.  
  
    
|**Get-adfsproperties에서 보고 한 대로 페더레이션 서비스 속성 이름**|**AD FS 관리 콘솔의 페더레이션 서비스 속성 이름**|
|------|------|
|HostName|페더레이션 서비스 이름|  
|Identifier|페더레이션 서비스 식별자|  
|DisplayName|페더레이션 서비스 표시 이름|  
  
4.  응용 프로그램 구성 파일을 백업합니다. 여러 설정 중 이 파일에는 특히 정책 데이터베이스 연결 문자열이 포함됩니다.  
  
응용 프로그램 구성 파일을 백업하려면 `%programfiles%\Active Directory Federation Services 2.0\Microsoft.IdentityServer.Servicehost.exe.config` 파일을 백업 서버의 안전한 위치에 수동으로 복사해야 합니다.  
  
> [!NOTE]
>  이 파일의 "policystore connectionstring=" 바로 뒤에 있는 데이터베이스 연결 문자열을 적어 두세요. 연결 문자열에 SQL Server 데이터베이스가 지정된 경우 페더레이션 서버에서 원래 AD FS 구성을 복원할 때 이 값이 필요합니다.  
>   
>  예를 들어 WID 연결 문자열은 `“Data Source=\\.\pipe\mssql$microsoft##ssee\sql\query;Initial Catalog=AdfsConfiguration;Integrated Security=True"`이고, SQL Server 연결 문자열은 `"Data Source=databasehostname;Integrated Security=True"`입니다.  
  
5.  AD FS 2.0 페더레이션 서비스 계정의 ID와 이 계정의 암호를 기록합니다.  
  
ID 값을 찾으려면 **Services(서비스)** 콘솔에서 **AD FS 2.0 Windows Service(AD FS 2.0 Windows 서비스)** 의 **Log On As(다음 사용자로 로그온)** 열을 확인하여 이 값을 수동으로 기록합니다.  
  
> [!NOTE]
>  독립 실행형 페더레이션 서비스의 경우 기본 제공 네트워크 서비스 계정이 사용됩니다.  이 경우에는 암호를 사용할 필요가 없습니다.  
  
6.  사용하도록 설정된 AD FS 끝점 목록을 파일로 내보냅니다.  
  
이렇게 하려면 Windows PowerShell을 열고 `PSH:>add-pssnapin “Microsoft.adfs.powershell”`명령을 실행하여 Windows PowerShell 세션에 AD FS cmdlet을 추가합니다. 그런 다음 `PSH:> Get-ADFSEndpoint | Out-File “.\endpoints.txt”`명령을 실행하여 사용하도록 설정된 AD FS 끝점 목록을 파일로 내보냅니다.  
  
7.  모든 사용자 지정 클레임 설명을 파일로 내보냅니다.  
  
이렇게 하려면 Windows PowerShell을 열고 `PSH:>add-pssnapin “Microsoft.adfs.powershell”`명령을 실행하여 Windows PowerShell 세션에 AD FS cmdlet을 추가합니다. 그런 다음 `Get-ADFSClaimDescription | Out-File “.\claimtypes.txt”` 명령을 실행하여 사용자 지정 클레임 설명을 파일로 내보냅니다.  
  
##  <a name="step-2-export-claims-provider-trusts"></a>2단계: 클레임 공급자 트러스트 내보내기  
 클레임 공급자 트러스트를 내보내려면 다음 절차를 수행합니다.  
  
### <a name="to-export-claims-provider-trusts"></a>클레임 공급자 트러스트를 내보내려면  
  
1.  Windows PowerShell을 사용하여 모든 클레임 공급자 트러스트를 내보낼 수 있습니다. Windows PowerShell을 열고 `PSH:>add-pssnapin “Microsoft.adfs.powershell”`명령을 실행하여 Windows PowerShell 세션에 AD FS cmdlet을 추가합니다. 그런 다음 `PSH:>Get-ADFSClaimsProviderTrust | Out-File “.\cptrusts.txt”`명령을 실행하여 모든 클레임 공급자 트러스트를 내보냅니다.  
  
## <a name="step-3-export-relying-party-trusts"></a>3단계: 신뢰 당사자 트러스트 내보내기  
 신뢰 당사자 트러스트를 내보내려면 다음 절차를 수행합니다.  
  
### <a name="to-export-relying-party-trusts"></a>신뢰 당사자 트러스트를 내보내려면  
  
1.  모든 신뢰 당사자 트러스트를 내보내려면 Windows PowerShell을 열고 `PSH:>add-pssnapin “Microsoft.adfs.powershell”`명령을 실행하여 Windows PowerShell 세션에 AD FS cmdlet을 추가합니다. 그런 다음`PSH:>Get-ADFSRelyingPartyTrust | Out-File “.\rptrusts.txt”`명령을 실행하여 모든 신뢰 당사자 트러스트를 내보냅니다.  
  
## <a name="step-4-back-up-custom-attribute-stores"></a>4단계: 사용자 지정 특성 저장소 백업  
 Windows PowerShell을 사용하여 AD FS에서 사용 중인 사용자 지정 특성 저장소에 대한 정보를 확인할 수 있습니다. Windows PowerShell을 열고 `PSH:>add-pssnapin “Microsoft.adfs.powershell”`명령을 실행하여 Windows PowerShell 세션에 AD FS cmdlet을 추가합니다. 그런 다음 `PSH:>Get-ADFSAttributeStore`명령을 실행하여 사용자 지정 특성 저장소에 대한 정보를 찾습니다. 사용자 지정 특성 저장소를 업그레이드하거나 마이그레이션하는 단계는 다양합니다.  
  
## <a name="step-5-back-up-webpage-customizations"></a>5단계: 웹 페이지 사용자 지정 백업  
 웹 페이지 사용자 지정 항목을 백업하려면 IIS의 가상 경로 **“/adfs/ls”** 에 매핑된 디렉터리에서 **web.config** 파일과 AD FS 웹 페이지를 복사합니다. 기본적으로 **%systemdrive%\inetpub\adfs\ls** 디렉터리에 있습니다.  

## <a name="next-steps"></a>다음 단계
 [AD FS 2.0 페더레이션 서버 마이그레이션 준비](prepare-to-migrate-ad-fs-fed-server.md)   
 [AD FS 2.0 페더레이션 서버 프록시 마이그레이션 준비](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [AD FS 2.0 페더레이션 서버 마이그레이션](migrate-the-ad-fs-fed-server.md)   
 [AD FS 2.0 페더레이션 서버 프록시 마이그레이션](migrate-the-ad-fs-2-fed-server-proxy.md)   
 [AD FS 1.1 웹 에이전트 마이그레이션](migrate-the-ad-fs-web-agent.md)