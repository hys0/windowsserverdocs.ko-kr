---
title: "Windows Server Essentials 경험 배포 하 여 호스팅된 서버"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a455c6b4-b29f-4f76-8c6b-1578b6537717
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: c299d2b5f3d6b48693c473754a5205a7d26b5d6a
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="deploy-windows-server-essentials-experience-as-a-hosted-server"></a>Windows Server Essentials 경험 배포 하 여 호스팅된 서버

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

이 문서는 자신의 랩에서 설치 (이라고 Windows Server Essentials 문서의 나머지 부분에서는) Windows Server Essentials 경험 역할 Microsoft Windows Server 16 배포 및 서비스를 고객에 게 Windows Server Essentials 경험을 제공 하 게 호스팅 업체와 관련 된 정보가 포함 됩니다. 이 문서는 다음 섹션에 포함 됩니다.  
  

-   [Windows Server Essentials 경험 개요](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_WSEEOverview)  
  
-   [Windows Server Essentials 환경 호스트의 이점](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Benefits)  
  
-   [지원 되는 배포 옵션](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_SupportedDeployment)  
  
-   [지원 되는 네트워크 토폴로지에서](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_SupportedToplogy)  
  
-   [Windows Server Essentials 경험 역할 이미지를 사용자 지정](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_CustomizeImage)  
  
-   [Windows Server Essentials 경험 배포 자동화](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_AutomateDeployment)  
  
-   [Windows Server Essentials 환경에서 Windows Small Business Server 데이터 마이그레이션](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Migrate)  
  
-   [Windows PowerShell를 사용 하 여 일반적인 작업을 수행 합니다.](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_PowerShell)  
  
-   [Windows Server Essentials의 메일 통합](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_EmailIntegration)  
  
-   [모니터링 하 고 기본 도구를 사용 하 여 관리](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Monitoring)  
  
-   [테스트 시나리오](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Scenarios)  
  
-   [지원 정보](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Support)  

-   [Windows Server Essentials 경험 개요](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_WSEEOverview)  
  
-   [Windows Server Essentials 환경 호스트의 이점](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Benefits)  
  
-   [지원 되는 배포 옵션](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_SupportedDeployment)  
  
-   [지원 되는 네트워크 토폴로지에서](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_SupportedToplogy)  
  
-   [Windows Server Essentials 경험 역할 이미지를 사용자 지정](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_CustomizeImage)  
  
-   [Windows Server Essentials 경험 배포 자동화](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_AutomateDeployment)  
  
-   [Windows Server Essentials 환경에서 Windows Small Business Server 데이터 마이그레이션](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Migrate)  
  
-   [Windows PowerShell를 사용 하 여 일반적인 작업을 수행 합니다.](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_PowerShell)  
  
-   [Windows Server Essentials의 메일 통합](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_EmailIntegration)  
  
-   [모니터링 하 고 기본 도구를 사용 하 여 관리](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Monitoring)  
  
-   [테스트 시나리오](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Scenarios)  
  
-   [지원 정보](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Support)  

  
##  <a name="BKMK_WSEEOverview"></a>Windows Server Essentials 경험 개요  
 Windows Server Essentials 경험 Windows Server 2012 r 2 표준 및 Windows Server 2012 R2 Datacenter에서 사용할 수 있는 서버 역할입니다. Windows Server Essentials 경험 역할 Windows Server 2012 r 2를 실행 하는 서버에 설치 되어, 고객 잠금 및 제한 없이 Windows Server Essentials에서 사용할 수 있는 모든 기능을 활용을 걸릴 수 있습니다. Windows Server Essentials 경험에 대해 알아보고 중소기업 다음과 같은 간 온-프레미스 솔루션을 사용할 수 있습니다.  
  
-   **데이터 저장 한 보호** 고객 저장할 수 있습니다 "중앙된 위치에™의 데이터 클라이언트 및 서버 데이터 보호 서버 및의 네트워크 안에 클라이언트 컴퓨터 (미만 75)에 백업 합니다.  
  
-   **사용자 관리** 사용자 및 그룹 간단한 서버 대시보드를 통해 관리할 수 있습니다. 또한, Microsoft Azure Active Directory (Azure AD)와 통합 액세스할 수 있도록 쉽게 데이터 (예를 들어, Office 365, Exchange Online 및 SharePoint Online) Microsoft online services에 대 한 사용자에 대 한 도메인 자격 증명을 사용 하 여 합니다.  
  
-   **통합 서비스** 온라인 서비스 (Office 365, SharePoint Online 및 Microsoft Azure Backup) 등 Microsoft 서버를 통합할 수 있습니다. 서비스 또는 제 3 자 공급자에서 제공 되는 서비스와 서버를 통합할 수 있습니다.  
  
-   **위치에 액세스할** 고객 서버, 네트워크 컴퓨터 및 데이터에 액세스할 수에서 어디에서 나은 인터넷에 연결 되어 있는 거의 모든 디바이스를 사용 하 여 합니다. 원격 Web Access 액세스 응용 프로그램 및 능률적인을 쉽게 터치 할 브라우저 환경의와 데이터를 사용 하도록 설정 합니다. 서버에 사용할 앱을 통해 Windows Phone 또는 Microsoft 스토어 앱의 데이터에 액세스할 수 있습니다.  
  
-   **스트리밍 미디어** 종료 고객 사용 하도록 설정한 Windows Server Essentials 환경을 사용 하는 서버에서 미디어 패키지를 설치한 경우 음악, 동영상 및 사진을 공유 폴더에 저장 다음 네트워크에 연결 된 컴퓨터 또는 웹에 대 한 원격 액세스에서 이러한 미디어 파일에 액세스할 수 있습니다.  
  
-   **상태를 모니터링** 네트워크 상태를 모니터링 하 고 사용자 지정 된 건강 보고서를 얻을 수 있습니다.  
  
##  <a name="BKMK_Benefits"></a>Windows Server Essentials 환경 호스트의 이점  
  Windows Server Essentials 경험 Windows Server의 역할 이므로 기존 배포 및 Windows Server를 배포 및 Windows Server Essentials 경험 역할을 구성에서 관리 프레임 워크 다시 사용할 수 있습니다. Windows Server Essentials 경험 역할 호스트 다음 이점을 제공 합니다.  
  
-   **배포 효율성을 높였습니다** 및 Windows Server Essentials 경험 역할을 설정 하면 일부 가장 일반적으로 사용 되는 역할 기능이 켜져 있고 작 및 midsized 비즈니스에 대 한 유용한으로 구성 되어 있습니다. Windows Server Essentials 기능을 사용자 지정 하거나 온-프레미스 기능 중 일부를 숨길 수 있습니다. Windows Azure 팩을 사용 하는 경우 Windows Server 2012 r 2에 Windows Server Essentials 경험에 대 한 갤러리 템플릿을 다운로드할 수 있습니다.  
  
-   **간소화 된 대시보드** Windows Server Essentials 대시보드에 서버 폴더, 관리 서버 저장소, 백업 및 복원, 사용자 또는 그룹 계정, 디바이스, 원격 액세스 메일 등의 일반적인 작업을 간소화. 중소기업 midsized 비즈니스 고객 기술 지원에 대 한 기술 지원 서비스를 호출 하는 대신 매일 관리 작업을 수행할 수 있습니다.  
  
-   **확장성** Windows Server Essentials 대시보드 및 Windows Server Essentials 커넥터 소프트웨어는 확장할 수 있습니다. 브랜드 직접 추가 하 고 고객이 서버 및 서비스에 대 한 모든 하나의 진입점 않아도 통합, 서비스 수 있습니다.  
  
-   **모니터** System Center 모니터링 팩의 새로운 버전을 모니터링 하 고 Windows Server Essentials 실행 하는 여러 서버 관리에 사용할 수 있습니다. 관리 팩을 다운로드 하려면 참조 [시스템 센터 관리 팩에 대 한 Windows Server Essentials](https://www.microsoft.com/download/details.aspx?id=40809)합니다.  
  
##  <a name="BKMK_SupportedDeployment"></a>지원 되는 배포 옵션  
  Windows Server Essentials 환경 새로운 Active Directory 환경;에 도메인 컨트롤러도 배포할 수 있습니다. 또는 기존 Active Directory 환경 도메인 구성원에 배포할 수 있습니다.  
  
 Windows Server 2012 r 2 표준 또는 Windows Server 2012 R2 Datacenter 먼저 배포 하 고 다음 Windows Server Essentials 경험 역할을 설치 하는 것이 좋습니다. 이 배포 방법을 잠금 및 제한 없이 Windows Server Essentials 버전의 모든 기능 얻을 수 있습니다.  
  

 Windows Server 2012 r 2는 Windows Server Essentials 경험 역할 설치에 대 한 자세한 내용은 참조 [설치 및 구성 Windows Server Essentials](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md)합니다.  


  
##  <a name="BKMK_SupportedToplogy"></a>지원 되는 네트워크 토폴로지에서  
 Windows Server Essentials 경험 로밍 클라이언트에서를 사용 하려면 VPN은 사용 해야 합니다. 로밍 하는 클라이언트에서 서버에 대 한 원격 액세스를 사용 하도록 설정할 포트 443 열고 서버 포트 80 해야 합니다.  
  
 두 개의 일반적인 서버 쪽 네트워킹 토롤로지, 있으며 VPN 및 원격 Web Access 구성할 수 있습니다 방법을 다음과 같습니다.  
  
-   **1 토폴로지** (이의 기본 설정, 것과 같은 서브넷 서버 및 VPN IP 범위 장소):  
  
    -   네트워크 주소 번역 (NAT) 디바이스에서 별도 가상 네트워크에서 서버를 설정 합니다.  
  
    -   DHCP 가상 네트워크의 서비스를 사용 하거나 서버에 대해 고정 IP 주소를 지정 합니다.  
  
    -   로컬 네트워크의 서버의 주소를 라우터의 공개 IP 포트 443 전달 합니다.  
  
    -   포트 443 통과 VPN 연결을 허용 합니다.  
  
    -   서버 주소와 같은 서브넷 범위 내에 VPN IPv4 주소 풀을 설정 합니다.  
  
    -   두 번째 서버 내 같은 서브넷 하지만 VPN 주소 풀에서 고정 IP 주소를 지정 합니다.  
  
-   **2 토폴로지**:  
  
    -   서버 개인 IP 주소를 지정 합니다.  
  
    -   포트 443 서버에 연결할 공개 포트 443 IP 주소를 허용 합니다.  
  
    -   포트 443 통과 VPN 연결을 허용 합니다.  
  
    -   다른 범위 VPN IPv4 주소 풀 및 서버 주소를 지정 합니다.  
  
 토폴로지 2 다른 서버 같은 도메인에 추가할 수 없으므로 두 번째 서버 시나리오 지원 되지 않습니다.  
  
 초기 구성 이후 마법사를 구성할 수 있습니다 또는 우리의 Windows PowerShell 스크립트를 사용 하 여 자리를 비운 사이 배포 하는 동안 VPN을 사용할 수 있습니다.  
  
 Windows PowerShell를 사용 하 여 VPN을 사용 하려면 Windows Server Essentials 실행 하는 서버에서 관리자 권한으로 다음 명령을 실행 하 고 필요한 모든 정보를 제공 합니다.  
  
```  
##  
## To configure external domain and SSL certificate (if not yet done in unattended Initial Configuration).  
##  
  
$myExternalDomainName = 'remote.contoso.com';   ## corresponds to A or AAAA DNS record(s) that can be resolved on Internet and routed to the server  
$mySslCertificateFile = 'C:\ssl.pfx';   ## full path to SSL certificate file  
$mySslCertificatePassword = ConvertTo-SecureString  œAsPlainText  œForce '******';   ## password for private key of the SSL certificate  
$skipCertificateVerification = $true;   ## whether or not, skip verification for the SSL certificate  
  
Set-WssDomainNameConfiguration  œDomainName $myExternalDomainName  œCertificatePath $mySslCertificateFile  œCertificateFilePassword $mySslCertificatePassword  œNoCertificateVerification  
##  
## To install VPN with static IPv4 pool (and allow all existing users to establish VPN).  
##  
  
Install-WssVpnServer -IPv4AddressRange ('192.168.0.160','192.168.0.240') -ApplyToExistingUsers;  
  
```  
  
> [!NOTE]
>  고객은 서버 소유 전에 VPN 연결을 제공할 수 없는 경우 고객이 원격 데스크톱 프로토콜 서버에 연결 하 고 구성에 사용할 수 있도록 서버 포트 3389 인터넷에 연결할 수 있는 인지 확인 합니다.  
  
##  <a name="BKMK_CustomizeImage"></a>Windows Server Essentials 경험 역할 이미지를 사용자 지정  
 Windows Server Essentials 경험 역할 구성 하기 전에 이미지를 사용자 지정할 수 있습니다. 표준 Windows Server Sysprep 프로세스에 대 한 자세한 내용은 [Windows Assessment and Deployment Kit](https://msdn.microsoft.com/library/hh825420.aspx)합니다. Sysprep 사용 하 여 이미지를 준비한 다음 사용 하거나 새 배포 Install.wim에 reseal 수 있습니다.  
  
 가상 컴퓨터 관리자를 사용 하는 경우 서식 실행 중인 인스턴스를 사용 하 여 만들 수 있습니다. 이 프로세스 Sysprep를 사용 하 여 인스턴스를 준비 하 고 컴퓨터를 종료 합니다. 라이브러리에 있는 템플릿의 저장 한 후 개별적으로에서 사용할 수 있습니다.  
  
 Windows Server Essentials 경험 역할을 설치한 후 Windows Server Essentials의 기능을 사용자 지정할 수 있습니다. 가장 중요 한 사용자 지정 중 하나는 **IsHosted** 레지스트리 키: **를 Server\Deployment\IsHosted**합니다.  
  
 0x1이 키가 설정, 동작 온-프레미스 기능 중 일부를 변경 됩니다. 이러한 기능 변경 내용은 다음과 같습니다.  
  
-   **클라이언트 백업** 클라이언트 백업 꺼집니다 클라이언트를 새로 참여 컴퓨터 기본적으로 설정 합니다.  
  
-   **클라이언트 복원 서비스** 클라이언트 복원 서비스가 수 없게 되 고 UI 대시보드에서 표시 되지 것입니다.  
  
-   **파일 히스토리** 서버에서 파일 히스토리 설정 새로 만든된 사용자 계정에 대 한 자동으로 관리 되지 것입니다.  
  
-   **서버 백업** 서버 백업 서비스 수 없게 되 고 서버 백업 UI 대시보드에서 표시 되지 것입니다.  
  
-   **저장소 공간** 만들거나 저장소 공간 관리 하기 위한의 UI 대시보드에서 표시 되지 것입니다.  
  
-   **어디서 나 액세스** 설정 어디서 나 액세스 마법사가 실행 하는 경우 VPN와 라우터 구성은 기본적으로 건너뜁니다.  
  
 나열 된 각 기능의 동작을 제어 하려는 경우 해당 레지스트리 키 각각의 설정할 수 있습니다. 레지스트리 키를 설정 하는 방법에 대 한 정보를 참조는 [사용자 지정 하 고 Windows Server 2012 r 2에 Windows Server Essentials 배포](https://technet.microsoft.com/library/dn293241.aspx)  
  
##  <a name="BKMK_AutomateDeployment"></a>Windows Server Essentials 경험 배포 자동화  
 배포 자동화, 하려면 먼저 운영 체제를 배포 하 고 Windows Server Essentials 경험 역할을 설치 해야 합니다.  
  
-   지침에 따라 자동으로 배포할 Windows Server 2012 r 2 표준 또는 Windows Server 2012 R2 Datacenter [Windows Assessment and Deployment Kit](https://msdn.microsoft.com/library/hh825420.aspx)합니다.  
  
-   Windows Server Essentials 경험 역할 Windows PowerShell를 사용 하 여 설치 하는 방법을 알아보려면 [설치 및 구성 Windows Server Essentials](https://technet.microsoft.com/library/dn281793.aspx)합니다.  
  
> [!NOTE]
>  호스트 가상 컴퓨터 및 Windows Server Essentials 환경의 표준 시간대 설정을 동일한 지 확인 합니다. 그렇지 않은 경우 몇 가지 오류가 발생할 수 있습니다. 여기에: 서버 초기 구성에 실패할 수 관련된 작업을 인증서, Windows Server Essentials 경험 역할을 설치한 후 디바이스 정보 올바르게 업데이트 되지 것입니다 몇 시간 동안 인증서 작동 하지 않을 수 있습니다.  
  
 사용 하 여 Windows PowerShell cmdlet 배포 후 **Get WssConfigurationStatus** 초기 구성 성공 했는지 확인 합니다. 반환 된 상태에서 다음 중 하나 여야: **Notstarted**, **FinishedWithWarning**, **실행**, **마침**, **실패**, 또는 **PendingReboot**합니다.  
  
 초기 구성 하는 동안 서버를 다시 시작 됩니다. 이 자동으로 다시 시작 되지 않도록 하려는 경우 다음 명령을 레지스트리 키 초기 구성 시작 하기 전에 추가할 사용할 수 있습니다.  
  
```  
New-ItemProperty "HKLM:\Software\Microsoft\Windows Server\Setup"Ã‚Â  -Name "WaitForReboot" -Value 1 -PropertyType "DWord" -Force -Confirm:$false  
  
```  
  
 초기 구성 시작을 사용할 수 있습니다 **Get WssConfigurationStatus** 초기 구성 상태를 확인 하려면 상태가 되 면 및 **PendingReboot**, 서버를 다시 시작할 수 있습니다.  
  
##  <a name="BKMK_Migrate"></a>Windows Server Essentials 환경에서 Windows Small Business Server 데이터 마이그레이션  
 Windows Server Essentials 실행 서버로 작은 Business Server 2011 Windows, Windows Small Business Server 2008, Windows Small Business Server 2003, 또는 Windows Server Essentials 실행 하는 서버에서 데이터 마이그레이션할 수 있습니다. 리뷰는 [Windows Server essentials 마이그레이션](../migrate/Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md) 마이그레이션 온-프레미스 2migrations에 대 한 지침을 호스팅 귀하의 환경에 따라 필요한 사용자 지정 합니다.  
  
> [!NOTE]
>  원본 서버와 대상 서버 같은 서브넷에 저장 하는 것이 좋습니다. 없는 경우 있는지 확인 해야 하는 다음과 같습니다.  
>   
>  -   원본 서버 대상 서버 액세스할 수 있는 서로 "™ s 내부 DNS 이름입니다.  
> -   필요한 모든 포트 열려 있습니다.  
  
 마이그레이션 후 잠금 하 고 한계를 제거 하 여 라이선스 업그레이드할 수 있습니다. 자세한 내용은 참조 [Windows Server Essentials에서 Windows Server 2012 표준으로 전환은](https://technet.microsoft.com/library/jj247582.aspx)합니다.  
  
##  <a name="BKMK_PowerShell"></a>Windows PowerShell를 사용 하 여 일반적인 작업을 수행 합니다.  
 이 섹션 몇 가지 일반적인 Windows PowerShell를 사용 하 여 수행할 수 있는 작업에 설명 합니다.  
  
### <a name="enable-remote-web-access"></a>원격 웹 액세스  
 **구문**:  
  
 Enable-WssRemoteWebAccess [-SkipRouter] [-DenyAccessByDefault] [-ApplyToExistingUsers]  
  
 **예제**:  
  
 $Enable-WssRemoteWebAccess œDenyAccessByDefault œApplyToExistingUsers  
  
 이 명령을 자동으로 구성 라우터 원격 웹 액세스를 활성화 되 고 모든 사용자에 게 기존의 기본 액세스 권한을 변경 합니다.  
  
### <a name="add-user"></a>사용자 추가  
 **구문**:  
  
 Add-WssUser [-이름] < string\ > [-암호] < securestring\ > [-AccessLevel < string\ > {사용자 및 #124; 관리자}] [-< string\ > 이름] [-성 < string\ >] [-AllowRemoteAccess] [-AllowVpnAccess] [< CommonParameters\ >]  
  
 **예제**:  
  
 $password = ConvertTo-SecureString "Passw0rd!" -asplaintext œforce$ 추가 WssUser-이름 User2Test-암호 $password Accesslevel 관리자-이름 사용자 2 성 테스트  
  
 이 명령을 User2Test 암호 Passw0rd 붙은 관리자가 추가 됩니다!.  
  
### <a name="add-server-folder"></a>서버 폴더 추가  
 **구문**:  
  
 Add-WssFolder [-이름] < string\ > [-경로] < string\ > [[-설명] < string\ >] [-KeepPermissions] [< CommonParameters\ >]  
  
 **예제**:  
  
 $추가 WssFolder-이름을 "MyTestFolder"-"C:\ServerFolders\MyTestFolder" 경로  
  
 이 명령을 MyTestFolder 지정된 위치에 라는 서버 폴더를 추가 합니다.  
  
##  <a name="BKMK_EmailIntegration"></a>Windows Server Essentials의 메일 통합  
 Exchange Server 호스트 또는 Windows Server Essentials 경험 Office 365와 통합 될 수 있습니다. 여 호스팅된 메일을 사용 하 여 고객 추가 기능에 Windows Server Essentials 경험 여 호스팅된 메일 솔루션 부합 개발 해야 합니다. 자세한 내용은 참조 [Windows Server Essentials SDK](https://msdn.microsoft.com/library/gg513877.aspx)합니다.  
  
##  <a name="BKMK_Monitoring"></a>모니터링 하 고 기본 도구를 사용 하 여 관리  
 이 섹션에는 기본 Windows Server 2012 r 2를 모니터링 하 고 서버 관리에 사용할 수 있는 도구 설명 합니다.  
  
### <a name="group-policy"></a>그룹 정책  
  Windows Server Essentials 경험 Windows Server 2012 r 2에 기본적으로 지원 그룹 정책을 활용 하 고 폴더 리디렉션 및 보안 설정을 구성 하려면 사용자 인터페이스를 제공 합니다.  
  
> [!NOTE]
>  여 호스팅된 환경에 대 한 사용자 프로필을 폴더 리디렉션을 사용 하는 경우 데이터 크기가 큰 때 로그인 하는 최종 사용자에 대 한 시간을 늘릴 수 있습니다.  
  
### <a name="system-center-monitoring-pack"></a>System Center 모니터링 팩  
 소규모 기업 조직에 건강 알림 시스템 많은 하는 Windows Server Essentials 실행 하는 서버 관리 하는 데 도움이 되는 최선을 다하고 Windows Server Essentials 경험 모니터에 대 한 system Center 모니터링 팩 합니다. 자세한 내용은 참조 [시스템 센터 관리 팩에 대 한 Windows Server Essentials](https://www.microsoft.com/download/details.aspx?id=40809)합니다.  
  
### <a name="backup-and-restore"></a>백업 및 복원  
  Windows Server 2012 r 2와 Windows Server Essentials 경험 서버와 클라이언트 네트워크의 컴퓨터에에서 백업할 수 있습니다.  
  
#### <a name="server-backup"></a>서버 백업  
 Windows Server Essentials 서버를 백업 하는 두 가지 지원: 온-프레미스 백업 및 끄기 온-프레미스 백업 합니다. 직접 서버 백업 솔루션 배포 하려면 다음이 옵션을 지정할 수 있습니다.  
  
-   **온-프레미스 백업** 별도 디스크를 정기적으로 차단 수준을 증분 백업을 수행할 수 있습니다. 호스팅,으로 가상 하드 디스크를 Windows Server Essentials 실행 가상 컴퓨터에 연결 하 고 서버에 백업 하는이 가상 하드 디스크를 구성 합니다 수 합니다. 가상 하드 디스크는 다른 Windows Server Essentials 실행 가상 컴퓨터 실제 디스크에 있어야 합니다.  
  
    > [!NOTE]
    >  가상 컴퓨터에 대 한 백업 다른 해결 방법 있고 사용자에 게 기본 Windows Server Essentials 서버 백업 기능 원하지 않는 경우에 기능을 해제 하 고 관련된 사용자 인터페이스 대시보드에서 제거할 수 있습니다. 자세한 내용은 참조는 [서버 백업 사용자 지정](https://technet.microsoft.com/library/dn293413.aspx) 섹션의 [사용자 지정 하 고 Windows Server Essentials Windows Server 2012 r 2에 배포](https://technet.microsoft.com/library/dn293241.aspx)합니다.  
  
-   **끄기 온-프레미스 백업** 서버 데이터 클라우드 기반 서비스를 정기적으로 백업 수 있습니다. 다운로드 하 고 있는 Microsoft Azure Backup 통합 모듈에 대 한 Windows Server Essentials Microsoft에서 제공 되는 Azure 백업 활용할 수 있도록 설치할 수 있습니다.  
  
     자세한 내용은 참조와 Windows Server Essentials 섹션에 통합 Windows Azure 백업 [서버 관리 백업](../manage/Manage-Server-Backup-in-Windows-Server-Essentials.md)합니다.  
  
     사용자 또는 사용자가 원하는 다른 클라우드 서비스는 다음과 같은 고려해 야 합니다.  
  
    -   대신 하는 기본 Azure 백업 선호 클라우드 서비스에 연결 하도록 대시보드의 사용자 인터페이스를 업데이트 합니다.  
  
    -   (선택 사항) 대시보드 구성 하 고 관리 클라우드 기반 백업 서비스에 대 한 추가 기능을 개발 합니다.  
  
#### <a name="client-computer-backup"></a>클라이언트 컴퓨터 백업  
 Windows Server Essentials 경험에서는 두 가지 유형의 클라이언트 데이터 백업: 전체 클라이언트 백업 및 파일 히스토리 합니다.  
  
> [!NOTE]
>  클라이언트를 백업 데이터를 통해 VPN 클라이언트는 서버 전송할 수 하기 때문에 성능이 저하 될 수 있습니다.  
  
##### <a name="full-client-backup"></a>전체 클라이언트 백업  
 전체 클라이언트 백업 Windows Server Essentials 네트워크에 연결 된 모든 클라이언트 디바이스용 기본적으로 켜져 있습니다. 완전히 클라이언트에 대 한 시스템 정보 및 데이터를 백업 하 고 데이터 중복 제거를 지원 합니다. 백업 하는 데이터는 Windows Server Essentials 실행 하는 서버에 저장 됩니다. 이 통해 실패 하는 클라이언트 이전 백업 지점에서 데이터를 검색 합니다.  
  
 전체 클라이언트 컴퓨터 백업에 대 한 몇 가지 사항을 다음과 같습니다.  
  
-   **성능** 초기 클라이언트 백업 업로드 하는 데이터의 양이 시간이 오래 걸릴 수 있습니다.  
  
-   **안정성** 인터넷 연결이 클라이언트 쪽 안정적 경우가 있습니다. 클라이언트 백업은 자동으로 다시 시작 되도록 설계 및 클라이언트 백업 데이터베이스 40 g B 데이터를 백업 때마다 검사점 만들어집니다. 이 값 신뢰할 수 있는 인터넷 연결을 원하는 경우에 더 적은 수 변경할 수 있습니다.  
  
    -   검사점 업무를 사용 하도록 설정 하려면: 서버 레지스트리 키 설정 **HKLM\Software\Microsoft\Windows Server\Backup\GetCheckPointJobs** 1.  
  
    -   검사점 임계값을 변경 하려면: 클라이언트에서 변경 **HKLM\Software\Microsoft\Windows Server\Backup\CheckPointThreshold** 40 g B의 기본값에서입니다.  
  
-   **앙상한 금속 복원 클라이언트** 클라이언트 앙상한 금속 복원은 Windows 사전 설치 환경 VPN 연결을 지원 하지 않으므로 지원 되지 않습니다. 단계를 수행 하 여 작업 클라이언트 복원 서비스 숨기기 해야 [사용자 지정 하 고 Windows Server Essentials Windows Server 2012 r 2에 배포](https://technet.microsoft.com/library/dn293241.aspx)합니다.  
  
##### <a name="file-history"></a>파일 히스토리  
 네트워크 공유를 프로필 데이터 (라이브러리, 바탕 화면, 연락처, 즐겨찾기) 백업 파일 히스토리는.1 Windows 8 및 Windows 8 기능. 중앙.1 Windows 8 또는 Windows 8을 실행 중인 Windows Server Essentials 네트워크에 연결 된 모든 컴퓨터의 파일 히스토리 설정을 관리할 수 있습니다. 백업 하는 데이터는 Windows Server Essentials 실행 하는 서버에 저장 됩니다. 단계를 수행 하 여 작업 클라이언트 복원 서비스 숨기기 해야 [사용자 지정 하 고 Windows Server 2012 r 2에 Windows Server Essentials 배포](https://technet.microsoft.com/library/dn293241.aspx)  
  
### <a name="storage-management"></a>저장소 관리  
 저장소 공간 집계 서로 다른 하드 드라이브의 실제 메모리 용량, 동적으로 하드 드라이브, 추가 하 고 데이터 볼륨의 복원 력이 지정된 수준으로 만들 수 있습니다. 호스트 켜거나 가상 컴퓨터에서 수행할 수 있습니다. Windows Server Essentials 실행 가상 컴퓨터에서이 기능을 숨기기 하려는 경우 지침에 따라 [사용자 지정 하 고 Windows Server Essentials Windows Server 2012 r 2에 배포](https://technet.microsoft.com/library/dn293241.aspx)합니다.  
  
##  <a name="BKMK_Scenarios"></a>테스트 시나리오  
 호스팅 관점에서 다음과 같은 경우 테스트 하는 것이 좋습니다.  
  

-   [서버 배포](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_ServerDeploy)  
  
-   [서버 구성](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_ServerConfig2)  
  
-   [서버 관리](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_ServerManage)  
  
-   [클라이언트 환경](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_ClientXP)  

  
###  <a name="BKMK_ServerDeploy"></a>서버 배포  
 다음과 같은 서버 배포 시나리오를 테스트할 수 있습니다.  
  
-   Windows Server 2012 R2 도메인 컨트롤러에서 사용자 환경으로 실행 하는 서버 배포 및 Windows Server Essentials 경험 역할을 설치 합니다.  
  
-   사용자 환경에서 Windows Server 2012 r 2를 실행 하는 서버에 배포,이 서버 기존 도메인에 가입 하 고 Windows Server Essentials 경험 역할을 설치 합니다.  
  
-   필요에 따라 Windows Server Essentials 이미지를 사용자 지정 합니다.  
  
-   Windows Server Essentials 배포 된 Windows PowerShell 및 자리를 비운 사이 파일 자동화 합니다.  
  
-   Windows Server Essentials 실행 호스팅된 서버에 Small Business Server Windows를 실행 하는 온-프레미스 서버 마이그레이션해야 합니다.  
  
###  <a name="BKMK_ServerConfig2"></a>서버 구성  
 다음 서버 구성 시나리오를 테스트할 수 있습니다.  
  
-   어디서 나 액세스 (가상 사설망, 원격 Web Access 및 DirectAccess)을 구성 합니다.  
  
-   저장소 및 서버 폴더를 구성 합니다.  
  
-   BranchCache 켭니다.  
  
-   해당 하는 경우 서버 백업, Online Backup-, 클라이언트 백업 구성 하 고 파일을 기록 합니다.  
  
-   해당 하는 경우 구성 하 고 저장소 공간을 관리 합니다.  
  
-   해당 하는 경우 메일 솔루션 통합 (Office 365 및 Exchange Server 호스팅된)을 구성 합니다.  
  
-   해당 하는 경우 통합 다른 Microsoft 온라인 서비스를 구성 합니다.  
  
-   해당 하는 경우 미디어 서버를 구성 합니다.  
  
###  <a name="BKMK_ServerManage"></a>서버 관리  
 다음과 같은 서버 관리 시나리오를 테스트할 수 있습니다.  
  
-   사용자 및 그룹 관리 합니다.  
  
-   구성 하 고 메일 알림 알림을 받게 됩니다.  
  
-   오류 또는 경고 메시지가 있는지 확인 하려면 모범 사례 분석기 실행 합니다.  
  
-   System Center Operations Manager 팩을 구성 합니다.  
  
-   운영 체제에 손상이 발생 했을 때 서버 복구를 구성 합니다.  
  
###  <a name="BKMK_ClientXP"></a>클라이언트 환경  
 최종 사용자는 다음과 같은 시나리오를 테스트할 수 있습니다.  
  
-   (PC 또는 Mac 운영 체제) 인터넷을 통해 클라이언트를 배포 합니다.  
  
-   클라이언트의 실행 패드를 사용 하 여 공유 폴더에 액세스할 수 있습니다.  
  
-   액세스 서버 자산 웹에 대 한 원격 액세스 다양 한 장치 (PC, 휴대폰 및 태블릿)의 합니다.  
  
-   Windows Phone에 대 한 서버 앱 내에 액세스 합니다.  
  
-   해당 하는 경우 액세스 파일 히스토리, 클라이언트 백업 및 복원 및 폴더 리디렉션을 합니다.  
  
-   해당 하는 경우 메일 통합 경험을 확인 합니다.  
  
##  <a name="BKMK_Support"></a>지원 정보  
 Windows Server Essentials 소프트웨어 개발 키트 (SDK) Windows Server Essentials Assessment 및 배포 Kit (ADK)를 다운로드할 수 있습니다.  
  
-   [Windows Server Essentials 소프트웨어 개발 키트](https://msdn.microsoft.com/library/gg513877.aspx)SDK  
  
-   [사용자 지정 및 Windows Server 2012 r 2에서는 Windows Server Essentials 배포](https://technet.microsoft.com/library/dn293241.aspx)  
  
## <a name="see-also"></a>참조 하십시오  
  
-   [Windows Server Essentials의 새로운 기능](../get-started/what-s-new.md)  

-   [Windows Server Essentials 설치](Install-Windows-Server-Essentials.md)  

-   [Windows Server Essentials 시작](../get-started/get-started.md)
