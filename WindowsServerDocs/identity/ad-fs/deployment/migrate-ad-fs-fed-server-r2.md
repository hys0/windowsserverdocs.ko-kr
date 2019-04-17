---
title: "ADFS 2.0 federation server를 마이그레이션해야"
description: "Windows Server 2012 r 2에는 ADFS 서버에 정보를 제공 합니다."
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/10/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: bef24f79cfa92dfeca1846501f14ebf6d8231f0d
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="migrate-the-ad-fs-20-federation-server-to-ad-fs-on-windows-server-2012-r2"></a>Windows Server 2012 r 2 ADFS ADFS 2.0 federation 서버 마이그레이션을

단일 노드 ADFS 농장, 군 농장 또는 Windows Server 2012 r 2에 SQL Server 팜에 속하는 ADFS federation 서버 마이그레이션할 다음과 같은 작업을 수행 해야 합니다.  
  
1.  [내보내고 ADFS 구성 데이터를 백업](migrate-ad-fs-fed-server-r2.md#export-and-backup-the-ad-fs-configuration-data)  
  
2.  [Windows Server 2012 r 2 federation 서버 팜 만들기](migrate-ad-fs-fed-server-r2.md#create-a-windows-server-2012-r2-federation-server-farm)  
  
3.  [Windows Server 2012 r 2 ADFS 농장 원래 구성 데이터 가져오기](migrate-ad-fs-fed-server-r2.md#import-the-original-configuration-data-into-the-windows-server-2012-r2-ad-fs-farm)  
  
##  <a name="export-and-backup-the-ad-fs-configuration-data"></a>내보내고 ADFS 구성 데이터를 백업  
 ADFS 구성 설정을 내보낼 다음 절차를 수행 합니다.  
  
###  <a name="to-export-service-settings"></a>서비스 설정이 내보내려면  
  
1.  .Pfx 파일로 다음 인증서와 개인 키에 액세스할 수 있는지 확인 하세요.  
  
    -   마이그레이션하려 federation 팜에서 사용 되는 ssl  
  
    -   (SSL 인증서에서 다른 경우) 서비스 통신 인증서 마이그레이션할 federation 팜으로 사용 되는  
  
    -   마이그레이션하려 federation 팜에서 사용 되는 모든 제 3 자 토큰 암호화/암호 해독 또는 토큰 서명 인증서  
  
SSL 인증서를 찾으려면 정보 IIS (인터넷 서비스) 관리를 엽니다 콘솔을 선택 **웹 사이트 기본** 왼쪽된 창에서 클릭 **바인딩을...** **작업** 창, 찾기 및 선택 https 구속력 클릭 **편집**을 차례로 클릭 하 고 **보기**합니다.  
  
Federation 서비스 및 개인 키.pfx 파일에 사용 하는 SSL 인증서를 내보내야 합니다. 자세한 내용은 참조 [내보내려면 서버 인증 인증서의 개인 키 부분](export-the-private-key-portion-of-a-server-authentication-certificate.md)합니다.  
  
> [!NOTE]
>  Windows Server 2012 r 2에서에 ADFS 실행의 일환으로 디바이스 등록 서비스 배포를 계획 하는 경우 새로운 SSL 인증서를 가져와야 합니다. 자세한 내용은 참조 [SSL 인증서 adfs 등록](enroll-an-ssl-certificate-for-ad-fs.md) 및 [federation 서버 등록 서비스 디바이스를 구성](configure-a-federation-server-with-device-registration-service.md)합니다.  
  
토큰 서명, 토큰 해독 및 사용 되는 서비스 통신 인증서를 보려면 파일에서 사용 중인 모든 인증서 목록이 만들려면 다음과 같은 Windows PowerShell 명령을 실행 합니다.  
  
``` powershell
Get-ADFSCertificate | Out-File “.\certificates.txt”  
 ```  
  
2.  ADFS federation 서비스 속성 federation 서비스, federation 서비스 표시 이름, 이름과 federation 서버 식별자와 같은 파일을를 내보냅니다.  
  
속성을 내보내려면 federation 서비스를 Windows PowerShell 열고 다음 명령을 실행 합니다. 

``` powershell
Get-ADFSProperties | Out-File “.\properties.txt”`.  
``` 

출력 파일에는 다음과 같은 구성 중요 한 값 포함 됩니다.  
 
|**Get ADFSProperties 들이 보고 federation 서비스 속성 이름**|**ADFS management console에서 federation 서비스 속성 이름**|
|-----|-----|  
|호스트|Federation 서비스 이름|  
|식별자|Federation 서비스 id|  
|표시 이름|Federation 서비스 표시 이름|  
  
3.  응용 프로그램 구성 파일을 백업 합니다. 다른 설정 중에서이 파일 정책 데이터베이스 연결 문자열을 포함 합니다.  
  
응용 프로그램 구성 파일을 백업 하려면 수동으로 복사 해야는 `%programfiles%\Active Directory Federation Services 2.0\Microsoft.IdentityServer.Servicehost.exe.config` 파일을 백업 하는 서버에 안전한 위치에 있습니다.  
  
> [!NOTE]
>  기록해 데이터베이스 연결 문자열이이 파일에서 바로 뒤 "policystore 연결 문자열 ="입니다. 연결 문자열 SQL Server 데이터베이스를 지정 하는 경우 값 federation 서버에 원래 ADFS 구성 복원 하는 경우 필요 합니다.  
>   
>  다음은 WID 연결 문자열의 예: `“Data Source=\\.\pipe\mssql$microsoft##ssee\sql\query;Initial Catalog=AdfsConfiguration;Integrated Security=True"`합니다. 다음은 SQL Server 연결 문자열의 예: `"Data Source=databasehostname;Integrated Security=True"`합니다.  
  
4.  ADFS federation 서비스 계정의 id 및이 계정의 암호를 기록 합니다.  
  
Id 값을 찾으려면 검사는 **사용자로 로그온** 열 **광고 FS 2.0 Windows 서비스** 에 **서비스** 콘솔 하 고 수동으로이 값을 기록 합니다.  
  
> [!NOTE]
>  독립 실행형 federation 서비스에 대 한 기본 제공 네트워크 서비스 계정을 사용 됩니다.  이 경우에 암호가 필요는 없습니다.  
  
5.  파일에 사용 가능한 ADFS 끝점 목록을 내보냅니다.  
  
이렇게 하려면 Windows PowerShell 열고 다음 명령을 실행 합니다. 

``` powershell
Get-ADFSEndpoint | Out-File “.\endpoints.txt”`.  
``` 

6.  모든 사용자 지정 클레임 설명을 파일 내보냅니다.  
  
이렇게 하려면 Windows PowerShell 열고 다음 명령을 실행 합니다. 

``` powershell
Get-ADFSClaimDescription | Out-File “.\claimtypes.txt”`.  
 ```

7.  사용자 지정 설정에는 토큰과 구성 useRelayStateForIdpInitiatedSignOn 등을 사용 하는 경우 참조용 토큰과 백업 사용자를 확인 합니다. 가상 경로 매핑됩니다 디렉터리에서 파일을 복사할 수 **"/ adfs/1!"** iis에서 합니다. 기본적으로에는 **%systemdrive%\inetpub\adfs\ls** 디렉터리 합니다.  
  
###  <a name="to-export-claims-provider-trusts-and-relying-party-trusts"></a>청구 공급자를 내보내려면 신뢰 하 고 당사자 신뢰  
  
1.  그러나 FS 내보내려면 AD 제공자 신뢰 주장 및 파티 신뢰를 사용 하지 않고 로그인 해야 관리자 권한으로 (도메인 관리자로 하지) 연합에 다음과 같은 Windows PowerShell 스크립트를 실행 하 고 서버에 있는 **미디어/server_support/adfs** Windows Server 2012 r 2 설치 CD 폴더: `export-federationconfiguration.ps1`합니다.  
  
> [!IMPORTANT]
>  내보내기 스크립트 다음 형식을 다음과 같습니다.  
>   
>  -   내보내기 FederationConfiguration.ps1-경로 < string\ > [-ComputerName < string\ >] [-자격 증명 < pscredential\ >] [-포스] [-CertificatePassword < securestring\ >]  
> -   내보내기 FederationConfiguration.ps1-경로 < string\ > [-ComputerName < string\ >] [-자격 증명 < pscredential\ >] [-포스] [-CertificatePassword < securestring\ >] [-< 문자열 > RelyingPartyTrustIdentifier] [-< 문자열 > ClaimsProviderTrustIdentifier]  
> -   내보내기 FederationConfiguration.ps1-경로 < string\ > [-ComputerName < string\ >] [-자격 증명 < pscredential\ >] [-포스] [-CertificatePassword < securestring\ >] [-< 문자열 > RelyingPartyTrustName] [-< 문자열 > ClaimsProviderTrustName]  
>   
>  **-RelyingPartyTrustIdentifier < 문자열 >** -cmdlet만 내보내기 해당 식별자 문자열 배열을에 지정 된 파티 신뢰를 사용 합니다. 기본값은 내보낼 신뢰 파티 신뢰 하는 중입니다. 스크립트 모든 내보냅니다 지정 RelyingPartyTrustIdentifier, ClaimsProviderTrustIdentifier, RelyingPartyTrustName, 및 ClaimsProviderTrustName 하지 않으면 당사자 신뢰 하 고 제공자 신뢰를 요구 합니다.  
>   
>  **-ClaimsProviderTrustIdentifier < 문자열 >** -cmdlet만 해당 식별자 문자열 배열을에 지정 된 청구 제공자 신뢰를 내보냅니다. 기본값은 내보낼 클레임 제공자 신뢰 하는 중입니다.  
>   
>  **-RelyingPartyTrustName < 문자열 >** -cmdlet만 내보내기 문자열 배열을에 지정 된 이름이 파티 신뢰를 사용 합니다. 기본값은 내보낼 신뢰 파티 신뢰 하는 중입니다.  
>   
>  **-ClaimsProviderTrustName < 문자열 >** -cmdlet만 문자열 배열을에 지정 된 이름이 클레임 제공자 신뢰를 내보냅니다. 기본값은 내보낼 클레임 제공자 신뢰 하는 중입니다.  
>   
>  **-경로 < string\ >** -경로 내보낸된 파일 포함 된 폴더를 합니다.  
>   
>  **-ComputerName < string\ >** -STS 서버 호스트 이름을 지정 합니다. 기본값은 로컬 컴퓨터 합니다. Windows Server 2012 r 2에서 ADFS ADFS 2.0 또는 Windows Server 2012에서 ADFS 마이그레이션하는, 경우 레거시 ADFS 서버 호스트 이름입니다.  
>   
>  **-> PSCredential\ < 자격 증명** -에이 작업을 수행할 수 있는 권한이 있는 사용자 계정에 지정 합니다. 기본값은 현재 사용자.  
>   
>  **-강제로** – 하지 사용자에 게 확인에 대 한 프롬프트를 지정 합니다.  
>   
>  **-CertificatePassword < SecureString\ >** -내보내기 개인 키 ADFS 인증서에 대 한 암호를 지정 합니다. 지정 하지 내보낼 개인 키로 ADFS 인증서가 필요한 경우 암호를 스크립트 표시 됩니다.  
>   
>  **입력**: 없음  
>   
>  **출력**: 문자열-이 cmdlet 내보내기 폴더 경로 반환 합니다. 가져오기 FederationConfiguration를 반환된 개체를 파이프 수 있습니다.  
  
###  <a name="to-back-up-custom-attribute-stores"></a>사용자 지정 된 특성 스토어를 백업 하려면  
  
1.  Windows Server 2012 r 2에서에 새 ADFS 팜에 유지 하려는 모든 사용자 지정 된 특성 스토어 수동으로 내보내야 합니다.  
  
> [!NOTE]
>  Windows Server 2012 r 2에 ADFS 또는 위에.NET Framework 4.0에 따라 특성 사용자 지정 상점 필요 합니다. 지침에 따라 [Microsoft.NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=30653) 설치 하 고 설치.Net Framework 4.5.  
  
Adfs에서 사용 중인 Windows PowerShell 다음 명령을 실행 하 여 사용자 지정 된 특성 스토어에 대 한 정보를 찾을 수 있습니다. 

``` powershell
Get-ADFSAttributeStore
```  

업그레이드 또는 사용자 지정 된 특성 스토어 마이그레이션할 단계 다릅니다.  
  
2.  또한 수동으로 하면 새 ADFS 농장 Windows Server 2012 r 2에서에 유지 하려면 사용자 지정 된 특성 저장소.dll 파일을 모두 내보내야 합니다. 업그레이드 또는.dll 파일의 특성을 사용자 지정 상점 마이그레이션할 단계 다릅니다.  
  
##  <a name="create-a-windows-server-2012-r2-federation-server-farm"></a>Windows Server 2012 r 2 federation 서버 팜 만들기  
  
1.  Windows Server 2012 r 2 운영 체제를 federation 서버로 한 후 ADFS 서버 역할을 추가 하는 컴퓨터에 설치 합니다. 자세한 내용은 참조 [ADFS 역할 서비스 설치](install-the-ad-fs-role-service.md)합니다. 새 federation 서비스 Active Directory Federation 서비스 구성 마법사 또는 Windows PowerShell 통해 구성 합니다. 자세한 내용은 참조 "새 federation 서버 농장의 첫 번째 federation 서버 구성"에서 [Federation 서버 구성](configure-a-federation-server.md)합니다.  

이 단계를 완료 하는 동안 다음이 지침을 따라야 합니다.  
  
-   Federation 서비스 구성 하기 위해 도메인 관리자 권한이 있어야 합니다.  
  
-   FS 2.0 또는 Windows Server 2012에서 ADFS 광고에 때 사용한 것과 동일한 federation 서비스 이름 (농장 이름)을 사용 해야 합니다. 이름이 같은 federation 서비스를 사용 하지 않으면를 백업 하는 인증서를 구성할 하려고 하는 Windows Server 2012 r 2 federation 서비스에 작동 하지 않습니다.  
  
-   WID 또는 SQL Server federation 서버 팜 인지를 지정 합니다. SQL 농장 경우 SQL Server 데이터베이스 위치와 인스턴스 이름을 지정 합니다.  
  
-   ADFS 마이그레이션 프로세스에 대 한 준비 과정의 일환으로 백업 SSL 서버 인증 인증서를 포함 하는 pfx 파일을 제공 해야 합니다.  
  
-   FS 2.0 또는 Windows Server 2012 농장의 ADFS 광고에 사용 된 서비스 계정 id 같은 지정 해야 합니다.  
  
2.  초기 노드 구성 되 면 추가 노드 새 그룹에 추가할 수 있습니다. 자세한 내용은 "federation 서버 기존 federation 서버 농장을 추가"에 표시 [Federation 서버 구성](configure-a-federation-server.md)합니다.  
  
##  <a name="import-the-original-configuration-data-into-the-windows-server-2012-r2-ad-fs-farm"></a>Windows Server 2012 r 2 ADFS 농장 원래 구성 데이터 가져오기  
 Windows Server 2012 r 2에서 실행 되는 ADFS federation 서버 팜 되었으므로 원래 ADFS 구성 데이터를 가져올 수 있습니다.  
  
1.  가져오기 및 기타 사용자 지정 ADFS 인증서를 구성, 비롯 한 외부 등록 한 토큰 서명 및 암호화-암호 해독/토큰 인증서 및 서비스 통신 인증서 SSL 인증서에서 다른 경우 됩니다.  
  
ADFS management console에서 선택 **인증서**합니다. 각 마이그레이션에 대 한 준비 하는 동안 certificates.txt 파일로 내보낸 값을 확인 하 여 서비스 통신문 전달, 해독 토큰 암호화 /, 및 토큰 서명 인증서를 확인 합니다.  
  
토큰 해독 또는 토큰 서명 인증서를 기본 자체 서명된 인증서의 외부 인증서를 변경 하려면 먼저 기본적으로 활성화 되어 있는 인증서 자동 롤오버 기능을 해제 해야 합니다. 이렇게 하려면 다음 Windows PowerShell 명령을 사용할 수 있습니다.  
  
``` powershell 
Set-ADFSProperties –AutoCertificateRollover $false  
```  
  
2.  사용자 지정 ADFS 서비스 설정을 사용 하 여 설정 AdfsProperties cmdlet AutoCertificateRollover 또는 SSO 수명 등을 구성 합니다.  
  
3.  그러나 ADFS 신뢰 파티 신뢰 하 고 클레임 제공자 신뢰를 가져오려면 로그인 해야 관리자 권한으로 (도메인 관리자로 하지) 연합에 다음과 같은 Windows PowerShell 스크립트를 실행 하 고 서버 폴더에 있는 \support\adfs Windows Server 2012 r 2 설치 CD의:  
  
``` powershell 
import-federationconfiguration.ps1  
```  
  
> [!IMPORTANT]
>  다음 형식을 스크립트 가져오기.  
>   
>  -  가져오기 FederationConfiguration.ps1-경로 < string\ > [-ComputerName < string\ >] [-자격 증명 < pscredential\ >] [-포스] [-LogPath < string\ >] [-CertificatePassword < securestring\ >]  
> -   가져오기 FederationConfiguration.ps1-경로 < string\ > [-ComputerName < string\ >] [-자격 증명 < pscredential\ >] [-포스] [-LogPath < string\ >] [-CertificatePassword < securestring\ >] [-< 문자열 > RelyingPartyTrustIdentifier] [-ClaimsProviderTrustIdentifier < 문자열 >  
> -   가져오기 FederationConfiguration.ps1-경로 < string\ > [-ComputerName < string\ >] [-자격 증명 < pscredential\ >] [-포스] [-LogPath < string\ >] [-CertificatePassword < securestring\ >] [-< 문자열 > RelyingPartyTrustName] [-< 문자열 > ClaimsProviderTrustName]  
>   
>  **-RelyingPartyTrustIdentifier < 문자열 >** -파티 신뢰를 식별자 문자열 배열을에 지정 된 의존 cmdlet만 가져오기. 기본 없음 신뢰 파티 신뢰 가져오는 것입니다. 스크립트를 모두 가져오려면는 지정 RelyingPartyTrustIdentifier, ClaimsProviderTrustIdentifier, RelyingPartyTrustName, 및 ClaimsProviderTrustName 하지 않으면 당사자 신뢰 하 고 제공자 신뢰를 요구 합니다.  
>   
>  **-ClaimsProviderTrustIdentifier < 문자열 >** -cmdlet만 해당 식별자 문자열 배열을에 지정 된 청구 제공자 신뢰를 가져옵니다. 기본 청구 제공자 신뢰 중 가져오는 것입니다.  
>   
>  **-RelyingPartyTrustName < 문자열 >** -문자열 배열을에 지정 된 이름이 파티 신뢰 의존 cmdlet만 가져오기. 기본 없음 신뢰 파티 신뢰 가져오는 것입니다.  
>   
>  **-ClaimsProviderTrustName < 문자열 >** -cmdlet 클레임 제공자 신뢰 문자열 배열을에 지정 된 이름이 가져옵니다. 기본 청구 제공자 신뢰 중 가져오는 것입니다.  
>   
>  **-경로 < string\ >** -경로 가져올 수 있도록 구성 파일이 들어 있는 폴더를 합니다.  
>   
>  **-LogPath < string\ >** -경로 가져오기를 로그 파일 들어 있는 폴더를 합니다. 이 폴더에서 "import.log" 이라는 로그 파일이 만들어집니다.  
>   
>  **-ComputerName < string\ >** -STS 서버의 호스트 이름을 지정 합니다. 기본값은 로컬 컴퓨터 합니다. Windows Server 2012 r 2에서 ADFS ADFS 2.0 또는 Windows Server 2012에서 ADFS 마이그레이션하는,이 매개 변수 호스트 레거시 ADFS 서버 설정 해야 합니다.  
>   
>  **-> PSCredential\ < 자격 증명**-에이 작업을 수행할 수 있는 권한이 있는 사용자 계정에 지정 합니다. 기본값은 현재 사용자.  
>   
>  **-강제로** – 하지 사용자에 게 확인에 대 한 프롬프트를 지정 합니다.  
>   
>  **-CertificatePassword < SecureString\ >** -ADFS 인증서 개인 키를 가져오는 대 한 암호를 지정 합니다. 지정 하지 가져올 개인 키로 ADFS 인증서가 필요한 경우 암호는 스크립트 표시 됩니다.  
>   
>  **입력:** 문자열-이 명령을 수행 입력으로 폴더 경로 가져오기. 이 명령 내보내기 FederationConfiguration 파이프 수 있습니다.  
>   
>  **출력:** 없음 합니다.  
  
신뢰 파티 신뢰 WSFedEndpoint 속성에서 뒤쪽의 공백을 오류 스크립트 가져오기 발생할 수 있습니다. 이 경우 파일을 가져오려면 사전에서 제거 공간 수동으로 합니다. 예를 들어, 이러한 항목 오류가 발생 합니다.  
  
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
>  을 사용 하는 모든 사용자 지정 클레임 ADFS 기본 규칙 이외의 개 규칙에 소스 시스템에서 Active Directory 클레임 공급자 신뢰 하는 경우 이러한는 하지 여 마이그레이션할 스크립트 합니다. Windows Server 2012 r 2는 새 기본값으로 하기 때문입니다. 새로운 Windows Server 2012 r 2 농장의 Active Directory 클레임 공급자 신뢰를 직접 추가 하 여 모든 사용자 지정 규칙 병합 해야 합니다.  
  
4.  모든 사용자 지정 ADFS 끝점 설정 구성 합니다. AD FS Management console에서 **끝점**합니다. 활성화 된 ADFS 끝점 ADFS 마이그레이션에 대 한 준비 하는 동안 내보낸 파일에는 활성화 된 ADFS 끝점 목록에 있는지 확인 합니다.  
  
     \-및-  
  
     모든 사용자 지정 클레임 설명을 구성 합니다. AD FS Management console에서 **클레임 설명을**합니다. ADFS 마이그레이션에 대 한 준비 하는 중 파일 내보낸 클레임 설명 사람 목록 ADFS 클레임 설명의 목록을 확인 합니다. 사용자 파일에 포함 되어 있지만 adfs에서 기본 목록에 포함 되지 않은 모든 사용자 지정 클레임 설명을 추가 합니다. 클레임 식별자 management console에서 파일에 ClaimType 매핑됩니다 note 합니다.  
  
5.  설치 및 구성 백업 된 모든 사용자 지정 상점 특성 합니다. 관리자로 서 사용자 지정 된 특성 스토어 이진 파일을 가리키도록 ADFS 구성 업데이트 하기 전에.NET Framework 4.0 이상 업그레이드는 있는지 확인 합니다.  
  
6.  레거시 web.config 파일 매개에 매핑하는 서비스 속성을 구성 합니다.  
  
    -   하는 경우 **useRelayStateForIdpInitiatedSignOn** 에 추가 되었고는 **web.config** FS 2.0 또는 ADFS Windows 서버 2012 농장의 광고에 파일을 Windows Server 2012 r 2 농장의 사용자 adfs에서 서비스는 구성 해야 합니다.  
  
        -   Windows Server 2012 r 2에서 ADFS 포함 한 **%systemroot%\ADFS\Microsoft.IdentityServer.Servicehost.exe.config** 파일. 요소와 같은 구문을으로 만들기는 **web.config** 파일 요소: `<useRelayStateForIdpInitiatedSignOn enabled="true" />`합니다. 이 요소의 일부로 포함 **< microsoft.identityserver.web >** 의 섹션은 **Microsoft.IdentityServer.Servicehost.exe.config** 파일.  
  
    -   하는 경우 **< 활성화 persistIdentityProviderInformation "참 & #124; false" lifetimeInDays = "90" enablewhrPersistence = = "참 & #124; false" / \ >** 에 추가 되었고는 **web.config** FS 2.0 또는 ADFS Windows 서버 2012 농장의 광고에 파일을 여 adfs 농장 Windows Server 2012 r 2에에서 다음과 같은 서비스 속성 구성 해야 합니다:  
  
        1.  Windows Server 2012 r 2에서 adfs, 다음 Windows PowerShell 명령을 실행: `Set-AdfsWebConfig –HRDCookieEnabled –HRDCookieLifetime`합니다.  
  
    -   하는 경우 **< singleSignOn 활성화 = "참 & #124; false" / \ >** 에 추가 되었고는 **web.config** 파일 ADFS 2.0에에서 또는 Windows 서버 2012 농장의 ADFS 하지 필요가 Windows Server 2012 r 2 농장의 사용자 adfs에서 추가 서비스 속성을 설정 합니다. 단일 로그인 화면에서 Windows Server 2012 r 2 농장 Adfs에 기본적으로 활성화 됩니다.  
  
    -   LocalAuthenticationTypes 설정에 추가 된 경우는 **web.config** FS 2.0 또는 ADFS Windows 서버 2012 농장의 광고에 파일을 Windows Server 2012 r 2 농장의 사용자 adfs에서 서비스는 구성 해야 합니다.  
  
        -   양식, 기본 변환 목록에 Windows Server 2012 r 2에 해당 하는 ADFS TlsClient federation 서비스 및 프록시 인증 형식을 지원 하기 위해 전 세계 인증 정책 설정에 통합, 있습니다. ADFS 관리 스냅인 아래에서에서 이러한 설정을 구성할 수 있습니다의 **인증 정책**합니다.  
  
 필요에 따라 원래 구성 데이터를 가져온 후 ADFS 로그인 페이지를 사용자 지정할 수 있습니다. 자세한 내용은 참조 [AD FS 로그인 페이지 사용자 지정](../operations/AD-FS-Customization-in-Windows-Server-2016.md)합니다.  
  
## <a name="next-steps"></a>다음 단계
 [Windows Server 2012 r 2 Active Directory Federation Services 역할 서비스 마이그레이션을](migrate-ad-fs-service-role-to-windows-server-r2.md)   
 [광고 FS Federation 서버 마이그레이션 준비](prepare-migrate-ad-fs-server-r2.md)   
 [AD FS Federation 서버 프록시 마이그레이션](migrate-fed-server-proxy-r2.md)   
 [Windows Server 2012 r 2에 AD FS 마이그레이션 확인](verify-ad-fs-migration.md)