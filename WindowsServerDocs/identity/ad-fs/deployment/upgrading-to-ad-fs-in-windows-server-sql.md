---
title: SQL Server를 사용 하 여 Windows Server 2016의 AD FS로 업그레이드
description: ''
author: billmath
manager: mtillman
ms.date: 04/11/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: 70f279bf-aea1-4f4f-9ab3-e9157233e267
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: dd843724faf1c7a8101def84091484a5e7f7900f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408236"
---
# <a name="upgrading-to-ad-fs-in-windows-server-2016-with-sql-server"></a>SQL Server를 사용 하 여 Windows Server 2016의 AD FS로 업그레이드


> [!NOTE]  
> 완료를 위해 계획 된 시간 프레임을 사용 하 여 업그레이드를 시작 합니다. 확장 된 시간 동안 AD FS를 혼합 모드 상태로 유지 하지 않는 것이 좋습니다 .이 경우 혼합 모드 상태에서 AD FS 벗어나면 팜에 문제가 발생할 수 있습니다.


## <a name="moving-from-a-windows-server-2012-r2-ad-fs-farm-to-a-windows-server-2016-ad-fs-farm"></a>Windows Server 2012 R2 AD FS 팜에서 Windows Server 2016 AD FS 팜으로 이동  
다음 문서에서는 AD FS 데이터베이스용 SQL Server를 사용 하는 경우 windows server 2016에서 AD FS Windows Server 2012 R2 팜을 AD FS로 업그레이드 하는 방법을 설명 합니다.  

### <a name="upgrading-ad-fs-to-windows-server-2016-fbl"></a>AD FS Windows Server 2016로 업그레이드 FBL  
Windows Server 2016에 대 한 AD FS의 새로운 기능은 팜 동작 수준 기능 (FBL)입니다.   이 기능은 팜 전체 이며 AD FS 팜에서 사용할 수 있는 기능을 결정 합니다.   기본적으로 Windows Server 2012 R2 AD FS 팜의 FBL는 Windows Server 2012 R2 FBL에 있습니다.  

Windows server 2016 AD FS 서버는 windows server 2012 R2 팜에 추가할 수 있으며 Windows server 2012 r 2와 동일한 FBL에서 작동 합니다.  이러한 방식으로 Windows Server 2016 AD FS 서버를 작동 하는 경우 팜이 "mixed" 라고 합니다.  그러나 Windows Server 2016로 FBL 될 때까지 새로운 Windows Server 2016 기능을 활용할 수 없습니다.  혼합 팜 사용:  

-   관리자는 새로운 Windows Server 2016 페더레이션 서버를 기존 Windows Server 2012 R2 팜에 추가할 수 있습니다.  결과적으로 팜은 "혼합 모드" 이며 Windows Server 2012 R2 팜 동작 수준을 운영 합니다.  팜 전체에서 일관성 있는 동작을 보장 하기 위해이 모드에서는 새로운 Windows Server 2016 기능을 구성 하거나 사용할 수 없습니다.  

-   모든 Windows Server 2012 R2 페더레이션 서버가 혼합 모드 팜에서 제거 되 고 WID 팜의 경우 새 Windows 서비스 2016 페더레이션 서버 중 하나가 주 노드의 역할로 승격 된 후 관리자가 FBL를 발생 시킬 수 있습니다. dows Server 2012 R2에서 Windows Server 2016로  따라서 새로운 AD FS Windows Server 2016 기능을 구성 하 고 사용할 수 있습니다.  

-   혼합 팜 기능의 결과로 Windows Server 2016로 업그레이드 하려고 하는 Windows Server 2012 R2 조직 AD FS 완전히 새로운 팜을 배포 하 고, 구성 데이터를 내보내고 가져올 필요가 없습니다.  대신, Windows Server 2016 노드는 온라인 상태에서 기존 팜에 추가 하 고 FBL에 관련 된 상대적으로 짧은 가동 중지 시간을 발생 시킬 수 있습니다.  

혼합 팜 모드에서는 AD FS 팜이 Windows Server 2016의 AD FS에 도입 된 새로운 기능 또는 기능을 사용할 수 없습니다.  즉, 새 기능을 사용해 보려는 조직은 FBL 발생할 때까지이 작업을 수행할 수 없습니다.  따라서 조직에서 FBL를 rasing 하기 전에 새 기능을 테스트 하려는 경우 별도의 팜을 배포 하 여이 작업을 수행 해야 합니다.  

이 문서의 나머지 부분에서는 windows server 2016 페더레이션 서버를 windows server 2012 R2 환경에 추가 하 고 FBL를 Windows Server 2016로 올리는 단계를 제공 합니다.  이러한 단계는 아래 아키텍처 다이어그램에 설명 된 테스트 환경에서 수행 되었습니다.  

> [!NOTE]  
> Windows Server 2016 FBL에서 AD FS로 이동 하려면 먼저 모든 Windows 2012 R2 노드를 제거 해야 합니다.  Windows Server 2012 R2 OS를 Windows Server 2016로 업그레이드 하 고 2016 노드가 되도록 할 수는 없습니다.  이를 제거 하 고 새 2016 노드로 바꾸어야 합니다.  

다음 아키텍처 다이어그램에는 아래 단계를 확인 하 고 기록 하는 데 사용 된 설정이 표시 됩니다.

![아키텍처](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/arch.png)


#### <a name="join-the-windows-2016-ad-fs-server-to-the-ad-fs-farm"></a>Windows 2016 AD FS 서버를 AD FS 팜에 가입 시킵니다.

1.  서버 관리자 사용 하 여 Windows Server 2016에 Active Directory Federation Services 역할 설치  

2.  AD FS 구성 마법사를 사용 하 여 새 Windows Server 2016 서버를 기존 AD FS 팜에 가입 시킵니다.  **시작** 화면에서 **다음**을 클릭 합니다.
 ![팜 참가](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/configure1.png)  
3.  **Active Directory Domain Services에 연결** 화면에서 페더레이션 서비스 구성을 수행할 수 있는 권한이 있는**관리자 계정을 p)** **다음**을 클릭 합니다.
4.  **팜 지정** 화면에서 SQL server 및 인스턴스 이름을 입력 하 고 **다음**을 클릭 합니다.
![팜 참가](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/configure3.png)
5.  **SSL 인증서 지정** 화면에서 인증서를 지정 하 고 **다음**을 클릭 합니다.
![팜 참가](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/configure4.png)
6.  **서비스 계정 지정** 화면에서 서비스 계정을 지정 하 고 **다음**을 클릭 합니다.
7.  **검토 옵션** 화면에서 옵션을 검토 하 고 **다음**을 클릭 합니다.
8.  필수 구성 요소 **확인** 화면에서 모든 필수 구성 요소 검사를 통과 했는지 확인 하 고 **구성**을 클릭 합니다.
9.  **결과** 화면에서 서버가 성공적으로 구성 되었는지 확인 하 고 **닫기**를 클릭 합니다.


#### <a name="remove-the-windows-server-2012-r2-ad-fs-server"></a>Windows Server 2012 R2 AD FS 서버를 제거 합니다.

>[!NOTE]
>SQL을 데이터베이스로 사용할 때 AdfsSyncProperties-Role을 사용 하 여 기본 AD FS 서버를 설정할 필요가 없습니다.  이 구성에서는 모든 노드가 주 복제본으로 간주 되기 때문입니다.

1.  서버 관리자의 Windows Server 2012 R2 AD FS 서버에서 **관리**아래의 **역할 및 기능 제거** 를 사용 합니다.
서버](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/remove1.png) ![제거
2.  **시작하기 전** 화면에서 **다음**을 클릭합니다.
3.  **서버 선택** 화면에서 **다음**을 클릭 합니다.
4.  **서버 역할** 화면에서 **Active Directory Federation Services** 옆의 확인란을 제거 하 고 **다음**을 클릭 합니다.
서버](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/remove2.png) ![제거
5.  **기능** 화면에서 **다음**을 클릭 합니다.
6.  **확인** 화면에서 **제거**를 클릭 합니다.
7.  이 작업이 완료 되 면 서버를 다시 시작 합니다.

#### <a name="raise-the-farm-behavior-level-fbl"></a>팜 동작 수준 (FBL)을 발생 시킵니다.
이 단계 전에는 forestprep 및 domainprep이 Active Directory 환경에서 실행 되었으며 Active Directory에 Windows Server 2016 스키마가 있는지 확인 해야 합니다.  이 문서는 Windows 2016 도메인 컨트롤러에서 시작 되었으며 AD가 설치 될 때 실행 되기 때문에 실행이 필요 하지 않았습니다.

>[!NOTE]
>아래 프로세스를 시작 하기 전에 설정에서 Windows 업데이트를 실행 하 여 Windows Server 2016이 최신 상태 인지 확인 합니다.  업데이트가 더 이상 필요하지 않을 때까지 이 프로세스를 계속합니다.

1. 이제 Windows Server 2016 서버에서 PowerShell을 열고 다음을 실행 합니다. **$cred = Get 자격 증명** 을 입력 하 고 enter 키를 누릅니다.
2. SQL Server에 대 한 관리자 권한이 있는 자격 증명을 입력 합니다.
3. 이제 PowerShell에서 다음을 입력 합니다. **AdfsFarmBehaviorLevelRaise-Credential $cred**
2. 메시지가 표시 되 면 **Y**를 입력 합니다.  그러면 수준이 시작 됩니다.  이 작업이 완료 되 면 FBL 성공적으로 발생 합니다.  
업데이트를 완료 ![](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/finish1.png)
3. 이제 AD FS 관리로 이동 하면 Windows Server 2016에 AD FS에 추가 된 새 노드가 표시 됩니다.  
4. 마찬가지로 PowerShell cmdlt: AdfsFarmInformation를 사용 하 여 현재 FBL를 표시할 수 있습니다.  
![업데이트 완료](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/finish2.png)

#### <a name="upgrade-the-configuration-version-of-existing-wap-servers"></a>기존 WAP 서버의 구성 버전 업그레이드
1. 각 웹 응용 프로그램 프록시에서 관리자 권한 창에서 다음 PowerShell 명령을 실행 하 여 WAP를 다시 구성 합니다.  
    ```powershell
    $trustcred = Get-Credential -Message "Enter Domain Administrator credentials"
    Install-WebApplicationProxy -CertificateThumbprint {SSLCert} -fsname fsname -FederationServiceTrustCredential $trustcred  
    ```
2. 클러스터에서 이전 서버를 제거 하 고 다음 Powershell을 실행 하 여 위에서 다시 구성한 최신 서버 버전을 실행 하는 WAP 서버만 유지 합니다.
    ```powershell
    Set-WebApplicationProxyConfiguration -ConnectedServersName WAPServerName1, WAPServerName2
    ```
3. Set-webapplicationproxyconfiguration commmandlet를 실행 하 여 WAP 구성을 확인 합니다. ConnectedServersName는 이전 명령의 서버 실행을 반영 합니다.
    ```powershell
    Get-WebApplicationProxyConfiguration
    ```
4. ConfigurationVersion의 WAP 서버를 업그레이드 하려면 다음 Powershell 명령을 실행 합니다.
    ```powershell
    Set-WebApplicationProxyConfiguration -UpgradeConfigurationVersion
    ```
5. ConfigurationVersion이 Set-webapplicationproxyconfiguration Powershell 명령을 사용 하 여 업그레이드 되었는지 확인 합니다.
