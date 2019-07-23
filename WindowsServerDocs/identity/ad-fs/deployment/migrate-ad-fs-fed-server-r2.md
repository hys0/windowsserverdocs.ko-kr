---
title: AD FS 2.0 페더레이션 서버 마이그레이션
description: AD FS 서버를 Windows Server 2012 R2로 마이그레이션하는 방법을 설명 합니다.
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/10/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 46d0b643d786443093e0dfeafe4cddde3278ff76
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66444627"
---
# <a name="migrate-the-ad-fs-20-federation-server-to-ad-fs-on-windows-server-2012-r2"></a>Windows Server 2012 R2에서 AD FS를 AD FS 2.0 페더레이션 서버 마이그레이션

단일 노드 AD FS 팜, WIF 팜 또는 Windows Server 2012 R2는 SQL 서버 팜에 속한 AD FS 페더레이션 서버를 마이그레이션하려면 다음 작업을 수행 해야 합니다.  
  
1.  [내보내기 및 AD FS 구성 데이터를 백업 합니다.](migrate-ad-fs-fed-server-r2.md#export-and-backup-the-ad-fs-configuration-data)  
  
2.  [Windows Server 2012 R2 페더레이션 서버 팜 만들기](migrate-ad-fs-fed-server-r2.md#create-a-windows-server-2012-r2-federation-server-farm)  
  
3.  [Windows Server 2012 R2 AD FS 팜에 원래 구성 데이터 가져오기](migrate-ad-fs-fed-server-r2.md#import-the-original-configuration-data-into-the-windows-server-2012-r2-ad-fs-farm)  
  
##  <a name="export-and-backup-the-ad-fs-configuration-data"></a>AD FS 구성 데이터 내보내기 및 백업  
 AD FS 구성 설정을 내보내려면 다음 절차를 수행합니다.  
  
###  <a name="to-export-service-settings"></a>서비스 설정을 내보내려면  
  
1.  .pfx 파일에서 다음 인증서와 해당 프라이빗 키에 액세스할 수 있는지 확인합니다.  
  
    -   마이그레이션할 페더레이션 서버 팜에서 사용되는 SSL 인증서  
  
    -   마이그레이션할 페더레이션 서버 팜에서 사용되는 서비스 통신 인증서(SSL 인증서와 다른 경우)  
  
    -   마이그레이션할 페더레이션 서버 팜에서 사용되는 모든 타사 토큰 서명 또는 토큰 암호화/암호 해독 인증서  
  
SSL 인증서를 찾으려면 IIS(인터넷 정보 서비스) 관리 콘솔을 열고 왼쪽 창에서 **기본 웹 사이트** 를 선택합니다. 그런 다음 **동작** 에 **작업** 찾기 및 선택 https 바인딩, 창 클릭 **편집**를 클릭 하 고 **보기**합니다.  
  
페더레이션 서비스에서 사용되는 SSL 인증서와 해당 프라이빗 키를 .pfx 파일로 내보내야 합니다. 자세한 내용은 [서버 인증 인증서의 프라이빗 키 부분 내보내기](export-the-private-key-portion-of-a-server-authentication-certificate.md)를 참조하세요.  
  
> [!NOTE]
>  Windows Server 2012 R2에서 AD FS를 실행 하는 일부로 장치 등록 서비스를 배포 하려는 경우에 새 SSL 인증서를 가져와야 합니다. 자세한 내용은 [AD FS에 대 한 SSL 인증서를 등록](enroll-an-ssl-certificate-for-ad-fs.md) 하 고 [Device Registration Service를 사용 하 여 페더레이션 서버 구성](configure-a-federation-server-with-device-registration-service.md)합니다.  
  
토큰 서명, 토큰 암호 해독 및 사용되는 서비스 통신 인증서를 보려면 다음 Windows PowerShell 명령을 실행하여 사용 중인 모든 인증서 목록을 파일로 만듭니다.  
  
``` powershell
Get-ADFSCertificate | Out-File “.\certificates.txt”  
 ```  
  
2. 페더레이션 서비스 이름, 페더레이션 서비스 표시 이름 및 페더레이션 서버 식별자와 같은 AD FS 페더레이션 서비스 속성을 파일로 내보냅니다.  
  
페더레이션 서비스 속성을 내보내려면 Windows PowerShell을 열고 다음 명령을 실행합니다. 

``` powershell
Get-ADFSProperties | Out-File “.\properties.txt”`.  
``` 

출력 파일에 다음과 같은 중요한 구성 값이 포함됩니다.  
 
|**Get-adfsproperties에서 보고 한 대로 페더레이션 서비스 속성 이름**|**AD FS 관리 콘솔의 페더레이션 서비스 속성 이름**|
|-----|-----|  
|HostName|페더레이션 서비스 이름|  
|Identifier|페더레이션 서비스 식별자|  
|DisplayName|페더레이션 서비스 표시 이름|  
  
3. 응용 프로그램 구성 파일을 백업합니다. 여러 설정 중 이 파일에는 특히 정책 데이터베이스 연결 문자열이 포함됩니다.  
  
응용 프로그램 구성 파일을 백업하려면 `%programfiles%\Active Directory Federation Services 2.0\Microsoft.IdentityServer.Servicehost.exe.config` 파일을 백업 서버의 안전한 위치에 수동으로 복사해야 합니다.  
  
> [!NOTE]
>  이 파일의 "policystore connectionstring=" 바로 뒤에 있는 데이터베이스 연결 문자열을 적어 둡니다. 연결 문자열에 SQL Server 데이터베이스가 지정된 경우 페더레이션 서버에서 원래 AD FS 구성을 복원할 때 이 값이 필요합니다.  
>   
>  예를 들어 WID 연결 문자열은 `“Data Source=\\.\pipe\mssql$microsoft##ssee\sql\query;Initial Catalog=AdfsConfiguration;Integrated Security=True"`이고, SQL Server 연결 문자열은 `"Data Source=databasehostname;Integrated Security=True"`입니다.  
  
4. AD FS 페더레이션 서비스 계정의 ID와 이 계정의 암호를 기록합니다.  
  
ID 값을 찾으려면 **Services(서비스)** 콘솔에서 **AD FS 2.0 Windows Service(AD FS 2.0 Windows 서비스)** 의 **Log On As(다음 사용자로 로그온)** 열을 확인하여 이 값을 수동으로 기록합니다.  
  
> [!NOTE]
>  독립 실행형 페더레이션 서비스의 경우 기본 제공 네트워크 서비스 계정이 사용됩니다.  이 경우에는 암호를 사용할 필요가 없습니다.  
  
5. 사용하도록 설정된 AD FS 끝점 목록을 파일로 내보냅니다.  
  
이렇게 하려면 Windows PowerShell을 열고 

``` powershell
Get-ADFSEndpoint | Out-File “.\endpoints.txt”`.  
``` 

6. 모든 사용자 지정 클레임 설명을 파일로 내보냅니다.  
  
이렇게 하려면 Windows PowerShell을 열고 

``` powershell
Get-ADFSClaimDescription | Out-File “.\claimtypes.txt”`.  
 ```

7. useRelayStateForIdpInitiatedSignOn과 같은 사용자 지정 설정을 web.config 파일에 구성한 경우 참조를 위해 web.config 파일을 백업해야 합니다. IIS의 가상 경로 **"/ adf/ls"** 에 매핑된 디렉터리에서 파일을 복사할 수 있습니다. 기본적으로 **%systemdrive%\inetpub\adfs\ls** 디렉터리에 있습니다.  
  
###  <a name="to-export-claims-provider-trusts-and-relying-party-trusts"></a>클레임 공급자 트러스트와 신뢰 당사자 트러스트를 내보내려면  
  
1.  내보내기 AD FS 클레임 공급자 트러스트와 신뢰 당사자 트러스트에 로그인 해야 관리자 권한으로 (단, 도메인 관리자 하지)에 있는 페더레이션 서버와 다음 Windows PowerShell 스크립트를 실행 합니다 **미디어 / server_support/adfs** Windows Server 2012 R2 설치 CD의 폴더: `export-federationconfiguration.ps1`합니다.  
  
> [!IMPORTANT]
>  내보내기 스크립트에는 다음 매개 변수가 사용됩니다.  
> 
> - 내보내기 FederationConfiguration.ps1-Path < 문자열\> [-ComputerName < 문자열\>] [-자격 증명 < pscredential\>] [-Force] [-CertificatePassword < securestring\>]  
>   -   내보내기 FederationConfiguration.ps1-Path < 문자열\> [-ComputerName < 문자열\>] [-자격 증명 < pscredential\>] [-Force] [-CertificatePassword < securestring\>] [- RelyingPartyTrustIdentifier < 문자열 >] [-ClaimsProviderTrustIdentifier < 문자열 >]  
>   -   내보내기 FederationConfiguration.ps1-Path < 문자열\> [-ComputerName < 문자열\>] [-자격 증명 < pscredential\>] [-Force] [-CertificatePassword < securestring\>] [- RelyingPartyTrustName < 문자열 >] [-ClaimsProviderTrustName < 문자열 >]  
> 
>   **-RelyingPartyTrustIdentifier <string[]>** - 이 cmdlet은 식별자가 문자열 배열에 지정된 신뢰 당사자 트러스트만 내보냅니다. 기본값은 신뢰 당사자 트러스트를 내보내지 않는 것입니다. RelyingPartyTrustIdentifier, ClaimsProviderTrustIdentifier, RelyingPartyTrustName 및 ClaimsProviderTrustName 중에 지정된 항목이 없는 경우 이 스크립트는 모든 신뢰 당사자 트러스트와 클레임 공급자 트러스트를 내보냅니다.  
> 
>   **-ClaimsProviderTrustIdentifier <string[]>** - 이 cmdlet은 식별자가 문자열 배열에 지정된 클레임 공급자 트러스트만 내보냅니다. 기본값은 클레임 공급자 트러스트를 내보내지 않는 것입니다.  
> 
>   **-RelyingPartyTrustName <string[]>** - 이 cmdlet은 이름이 문자열 배열에 지정된 신뢰 당사자 트러스트만 내보냅니다. 기본값은 신뢰 당사자 트러스트를 내보내지 않는 것입니다.  
> 
>   **-ClaimsProviderTrustName <string[]>** - 이 cmdlet은 이름이 문자열 배열에 지정된 클레임 공급자 트러스트만 내보냅니다. 기본값은 클레임 공급자 트러스트를 내보내지 않는 것입니다.  
> 
>   **-Path < 문자열\>**  -내보낸된 파일을 포함할 폴더의 경로를 합니다.  
> 
>   **-ComputerName < 문자열\>**  -STS 서버 호스트 이름을 지정 합니다. 기본값은 로컬 컴퓨터입니다. Windows Server 2012의 AD FS 2.0 또는 AD FS를 Windows Server 2012 R2의 AD FS로 마이그레이션하는 경우 기존 AD FS 서버의 호스트 이름으로 설정됩니다.  
> 
>   **-Credential < PSCredential\>**  -이 작업을 수행할 수 있는 권한을 가진 사용자 계정을 지정 합니다. 기본값은 현재 사용자입니다.  
> 
>   **-Force** – 사용자 확인 메시지를 표시하지 않도록 지정합니다.  
> 
>   **-CertificatePassword < SecureString\>**  -AD FS 인증서의 개인 키를 내보내기 위한 암호를 지정 합니다. 이 매개 변수를 지정하지 않으면 프라이빗 키가 있는 AD FS 인증서를 내보내야 하는 경우 암호를 묻는 메시지가 표시됩니다.  
> 
>   **입력**: 없음  
> 
>   **Outputs**: 문자열 - 이 cmdlet은 내보내기 폴더 경로를 반환합니다. 반환된 개체를 Import-FederationConfiguration에 파이프할 수 있습니다.  
  
###  <a name="to-back-up-custom-attribute-stores"></a>사용자 지정 특성 저장소를 백업하려면  
  
1.  Windows Server 2012 R2에서 새 AD FS 팜에서 유지할 하려는 모든 사용자 지정 특성 저장소를 수동으로 내보내야 합니다.  
  
> [!NOTE]
>  Windows Server 2012 R2에서 AD FS에는.NET Framework 4.0 이상을 기반으로 하는 사용자 지정 특성 저장소에 필요 합니다. [Microsoft .NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=30653) 의 지침에 따라 .Net Framework 4.5를 설치하고 설정합니다.  
  
AD FS에서 사용 중인 사용자 지정 특성 저장소에 대한 정보를 확인하려면 다음 Windows PowerShell 명령을 실행하면 됩니다. 

``` powershell
Get-ADFSAttributeStore
```  

사용자 지정 특성 저장소를 업그레이드하거나 마이그레이션하는 단계는 다양합니다.  
  
2. Windows Server 2012 R2에서 새 AD FS 팜에서 유지할 사용자 지정 특성 저장소의 모든.dll 파일을 수동으로 내보내야 합니다. 사용자 지정 특성 저장소의 .dll 파일을 업그레이드하거나 마이그레이션하는 단계는 다양합니다.  
  
##  <a name="create-a-windows-server-2012-r2-federation-server-farm"></a>Windows Server 2012 R2 페더레이션 서버 팜 만들기  
  
1.  페더레이션 서버로 작동 한 후 AD FS 서버 역할을 추가 하려는 컴퓨터에 Windows Server 2012 R2 운영 체제를 설치 합니다. 자세한 내용은 [Install the AD FS Role Service](install-the-ad-fs-role-service.md)를 참조하세요. 그런 다음 Active Directory Federation Service 구성 마법사 또는 Windows PowerShell을 통해 새 페더레이션 서비스를 구성합니다. 자세한 내용은 [페더레이션 서버 구성](configure-a-federation-server.md)에서 "새 페더레이션 서버 팜의 첫 번째 페더레이션 서버 구성"을 참조하십시오.  

이 단계를 완료하는 동안 다음 지침을 따라야 합니다.  
  
-   페더레이션 서비스를 구성하려면 도메인 관리자 권한이 있어야 합니다.  
  
-   Windows Server 2012의 AD FS 2.0 또는 AD FS에서 사용한 것과 동일한 페더레이션 서비스 이름(팜 이름)을 사용해야 합니다. 동일한 페더레이션 서비스 이름을 사용 하지 않으면 백업한 인증서를 구성 하려고 하는 Windows Server 2012 R2 페더레이션 서비스에서 작동 하지 않습니다.  
  
-   WID 페더레이션 서버 팜인지 또는 SQL Server 페더레이션 서버 팜인지 지정합니다. SQL 팜인 경우 SQL Server 데이터베이스 위치 및 인스턴스 이름을 지정합니다.  
  
-   AD FS 마이그레이션 프로세스의 일부로 백업한 SSL 서버 인증 인증서가 포함된 pfx 파일을 제공해야 합니다.  
  
-   Windows Server 2012 팜의 AD FS 2.0 또는 AD FS에서 사용한 것과 동일한 서비스 계정 ID를 지정해야 합니다.  
  
2. 초기 노드를 구성한 후에는 새 팜에 추가 노드를 추가할 수 있습니다. 자세한 내용은 [페더레이션 서버 구성](configure-a-federation-server.md)에서 "기존 페더레이션 서버 팜에 페더레이션 서버 추가"를 참조하십시오.  
  
##  <a name="import-the-original-configuration-data-into-the-windows-server-2012-r2-ad-fs-farm"></a>Windows Server 2012 R2 AD FS 팜으로 원래 구성 데이터 가져오기  
 Windows Server 2012 R2에서 실행 되는 AD FS 페더레이션 서버 팜을 설정 했으므로 원래 AD FS 구성 데이터를 가져올 수 있습니다.  
  
1.  외부에서 등록한 토큰 서명 및 토큰 암호 해독/암호화 인증서와 서비스 통신 인증서(SSL 인증서와 다른 경우)를 비롯한 다른 사용자 지정 AD FS 인증서를 가져와서 구성합니다.  
  
ADFS 관리 콘솔에서 **Certificates(인증서)** 를 선택합니다. 마이그레이션을 준비하는 동안 certificates.txt 파일로 내보낸 값과 대조하여 서비스 통신, 토큰 암호화/암호 해독 및 토큰 서명 인증서를 각각 확인합니다.  
  
토큰 암호 해독 또는 토큰 서명 인증서를 기본 자체 서명된 인증서에서 외부 인증서로 변경하려면 먼저 기본적으로 사용되는 자동 인증서 롤오버 기능을 사용하지 않도록 설정해야 합니다. 이렇게 하려면 다음 Windows PowerShell 명령을 사용하면 됩니다.  
  
``` powershell 
Set-ADFSProperties –AutoCertificateRollover $false  
```  
  
2. Set-AdfsProperties cmdlet을 사용하여 AutoCertificateRollover 또는 SSO 수명과 같은 사용자 지정 AD FS 서비스 설정을 구성합니다.  
  
3. AD FS 신뢰 당사자 트러스트와 클레임 공급자 트러스트를 가져오려면 있습니다 로그인 해야 관리자 권한으로 (단, 도메인 관리자 하지) 페더레이션 다음 Windows PowerShell 스크립트를 실행 하 고 서버 \support\adfs 폴더에 Windows Server 2012 R2 설치 CD 합니다.  
  
``` powershell 
import-federationconfiguration.ps1  
```  
  
> [!IMPORTANT]
>  가져오기 스크립트에는 다음 매개 변수가 사용됩니다.  
> 
> - Import-FederationConfiguration.ps1 -Path <string\> [-ComputerName <string\>] [-Credential <pscredential\>] [-Force] [-LogPath <string\>] [-CertificatePassword <securestring\>]  
>   -   가져오기 FederationConfiguration.ps1-Path < 문자열\> [-ComputerName < 문자열\>] [-자격 증명 < pscredential\>] [-Force] [-LogPath < 문자열\>] [-CertificatePassword < securestring \>] [-RelyingPartyTrustIdentifier < 문자열 >] [-ClaimsProviderTrustIdentifier < 문자열 >  
>   -   가져오기 FederationConfiguration.ps1-Path < 문자열\> [-ComputerName < 문자열\>] [-자격 증명 < pscredential\>] [-Force] [-LogPath < 문자열\>] [-CertificatePassword < securestring \>] [-RelyingPartyTrustName < 문자열 >] [-ClaimsProviderTrustName < 문자열 >]  
> 
>   **-RelyingPartyTrustIdentifier <string[]>** - 이 cmdlet은 식별자가 문자열 배열에 지정된 신뢰 당사자 트러스트만 가져옵니다. 기본값은 신뢰 당사자 트러스트를 가져오지 않는 것입니다. RelyingPartyTrustIdentifier, ClaimsProviderTrustIdentifier, RelyingPartyTrustName 및 ClaimsProviderTrustName 중에 지정된 항목이 없는 경우 이 스크립트는 모든 신뢰 당사자 트러스트와 클레임 공급자 트러스트를 가져옵니다.  
> 
>   **-ClaimsProviderTrustIdentifier <string[]>** - 이 cmdlet은 식별자가 문자열 배열에 지정된 클레임 공급자 트러스트만 가져옵니다. 기본값은 클레임 공급자 트러스트를 가져오지 않는 것입니다.  
> 
>   **-RelyingPartyTrustName <string[]>** - 이 cmdlet은 이름이 문자열 배열에 지정된 신뢰 당사자 트러스트만 가져옵니다. 기본값은 신뢰 당사자 트러스트를 가져오지 않는 것입니다.  
> 
>   **-ClaimsProviderTrustName <string[]>** - 이 cmdlet은 이름이 문자열 배열에 지정된 클레임 공급자 트러스트만 가져옵니다. 기본값은 클레임 공급자 트러스트를 가져오지 않는 것입니다.  
> 
>   **-Path < 문자열\>**  -가져올 구성 파일이 포함 된 폴더의 경로를 합니다.  
> 
>   **-LogPath < 문자열\>**  -가져오기 로그 파일을 포함할 폴더의 경로를 합니다. "Import.log"라는 로그 파일이 이 폴더에 만들어집니다.  
> 
>   **-ComputerName < 문자열\>**  -STS 서버의 호스트 이름을 지정 합니다. 기본값은 로컬 컴퓨터입니다. Windows Server 2012의 AD FS 2.0 또는 AD FS를 Windows Server 2012 R2의 AD FS로 마이그레이션하는 경우 이 매개 변수는 기존 AD FS 서버의 호스트 이름으로 설정됩니다.  
> 
>   **-Credential < PSCredential\>** -이 작업을 수행할 수 있는 권한을 가진 사용자 계정을 지정 합니다. 기본값은 현재 사용자입니다.  
> 
>   **-Force** – 사용자 확인 메시지를 표시하지 않도록 지정합니다.  
> 
>   **-CertificatePassword < SecureString\>**  -AD FS 인증서의 개인 키를 가져오기 위한 암호를 지정 합니다. 이 매개 변수를 지정하지 않으면 프라이빗 키가 있는 AD FS 인증서를 가져와야 하는 경우 암호를 묻는 메시지가 표시됩니다.  
> 
>   **Inputs:** 문자열 - 이 명령은 가져오기 폴더 경로를 입력으로 사용합니다. Export-FederationConfiguration을 이 명령에 파이프할 수 있습니다.  
> 
>   **Outputs:** 없음  
  
신뢰 당사자 트러스트의 WSFedEndpoint 속성에 후행 공백이 있으면 가져오기 스크립트 오류가 발생할 수 있습니다. 이 경우 가져오기 전에 파일에서 공백을 수동으로 제거하세요. 예를 들어 다음 항목은 오류를 일으킵니다.  
  
    ```  
    <URI N="WSFedEndpoint">https://127.0.0.1:444 /</URI>  
    ```  
  
    ```  
    <URI N="WSFedEndpoint">https://myapp.cloudapp.net:83 /</URI>  
    ```  
  
     They must be edited to:  
  
    ```  
    <URI N="WSFedEndpoint">https://127.0.0.1:444/</URI>  
    ```  
  
    ```  
    <URI N="WSFedEndpoint">https://myapp.cloudapp.net:83/</URI>  
    ```  
> [!IMPORTANT]
>  원본 시스템의 Active Directory 클레임 공급자 트러스트에 사용자 지정 클레임 규칙(AD FS 기본 규칙 이외의 규칙)이 있는 경우 이러한 규칙은 스크립트를 통해 마이그레이션되지 않습니다. Windows Server 2012 R2에는 새로운 기본값이 있기 때문입니다. 모든 사용자 규칙은 새로운 Windows Server 2012 R2 팜에서 Active Directory 클레임 공급자 트러스트에 수동으로 추가 하 여 병합 해야 합니다.  
  
4. 모든 사용자 지정 AD FS 끝점 설정을 구성합니다. AD FS 관리 콘솔에서 **Endpoints(끝점)** 를 선택합니다. AD FS 마이그레이션을 준비하는 동안 파일로 내보낸 사용 가능한 AD FS 끝점 목록과 사용하도록 설정된 AD FS 끝점을 대조합니다.  
  
    \- And -  
  
    모든 사용자 지정 클레임 설명을 구성합니다. AD FS 관리 콘솔에서 **Claim Descriptions(클레임 설명)** 를 선택합니다. AD FS 마이그레이션을 준비하는 동안 파일로 내보낸 클레임 설명 목록과 AD FS 클레임 설명 목록을 대조합니다. 파일에 포함되어 있지만 AD FS의 기본 목록에 포함되어 있지 않은 모든 사용자 지정 클레임 설명을 추가합니다. 관리 콘솔의 클레임 식별자는 파일의 ClaimType에 매핑됩니다.  
  
5. 백업한 모든 사용자 지정 특성 저장소를 설치하고 구성합니다. 관리자는 사용자 지정 특성 저장소 이진 파일을 가리키도록 AD FS 구성을 업데이트하기 전에 모든 사용자 지정 특성 저장소 이진 파일이 .NET Framework 4.0 이상으로 업그레이드되었는지 확인해야 합니다.  
  
6. 기존 web.config 파일 매개 변수에 매핑된 서비스 속성을 구성합니다.  
  
   -   하는 경우 **userelaystateforidpinitiatedsignon과** 에 추가 된 합니다 **web.config** 파일 AD FS 2.0 또는 Windows Server 2012 팜의 AD FS에서에서 AD fs에서 다음 서비스 속성을 구성 해야 합니다 Windows Server 2012 R2 팜:  
  
       -   Windows Server 2012 R2에서 AD FS 포함 된 **%systemroot%\ADFS\Microsoft.IdentityServer.Servicehost.exe.config** 파일입니다. 와 동일한 구문으로 요소를 만들 합니다 **web.config** file 요소: `<useRelayStateForIdpInitiatedSignOn enabled="true" />`합니다. 일부로이 요소를 포함 **< microsoft.identityserver.web >** 섹션을 **Microsoft.IdentityServer.Servicehost.exe.config** 파일입니다.  
  
   -   하는 경우 **< persistIdentityProviderInformation 사용 = "true&#124;false" lifetimeInDays "90" enablewhrPersistence = = "true&#124;false" /\>**  에 추가 된 합니다 **web.config** 파일을 AD FS 2.0 또는 Windows Server 2012 팜의 AD FS Windows Server 2012 R2 팜의 AD FS에서 다음 서비스 속성을 구성 해야 합니다.  
  
       1.  Windows Server 2012 R2에서 AD FS에서 다음 Windows PowerShell 명령을 실행 합니다: `Set-AdfsWebConfig –HRDCookieEnabled –HRDCookieLifetime`합니다.  
  
   -   경우 **< 사용 하도록 설정 하는 singleSignOn = "true&#124;false" /\>**  에 추가 된 합니다 **web.config** AD FS 2.0에서에서 파일 또는 Windows Server 2012 팜의 AD FS를 필요가 없습니다 추가 서비스를 설정 하려면 Windows Server 2012 R2 팜의 AD FS의 속성입니다. Single sign on Windows Server 2012 R2 팜의 AD FS에서 기본적으로 사용 됩니다.  
  
   -   LocalAuthenticationTypes 설정이 추가 된 경우는 **web.config** 파일 AD FS 2.0 또는 Windows Server 2012 팜의 AD FS에서에서 Windows Server 2012 R2 팜의 AD FS에서 다음 서비스 속성을 구성 해야 합니다.  
  
       -   통합 된 Forms, TlsClient, Basic Transform 목록에 Windows Server 2012 R2에 해당 하는 AD FS에 페더레이션 서비스 및 프록시 인증 유형을 둘 다를 지 원하는 전역 인증 정책 설정이 이러한 설정은 AD FS 관리 스냅인의 **Authentication Policies(인증 정책)** 에서 구성할 수 있습니다.  
  
   원래 구성 데이터를 가져온 후에는 필요에 따라 AD FS 로그인 페이지를 사용자 지정할 수 있습니다. 자세한 내용은 [Customizing the AD FS Sign-in Pages](../operations/AD-FS-Customization-in-Windows-Server-2016.md)를 참조하세요.  
  
## <a name="next-steps"></a>다음 단계
 [Windows Server 2012 R2로 Active Directory Federation Services 역할 서비스 마이그레이션](migrate-ad-fs-service-role-to-windows-server-r2.md)   
 [AD FS 페더레이션 서버 마이그레이션 준비](prepare-migrate-ad-fs-server-r2.md)   
 [AD FS 페더레이션 서버 프록시 마이그레이션](migrate-fed-server-proxy-r2.md)   
 [Windows Server 2012 R2로 AD FS 마이그레이션 확인](verify-ad-fs-migration.md)