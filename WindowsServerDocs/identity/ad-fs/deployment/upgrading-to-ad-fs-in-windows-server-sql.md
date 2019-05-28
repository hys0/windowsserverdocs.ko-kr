---
title: SQL Server 사용 하 여 Windows Server 2016에서에서 AD FS로 업그레이드
description: ''
author: billmath
manager: mtillman
ms.date: 04/11/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 70f279bf-aea1-4f4f-9ab3-e9157233e267
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 8ada2ae5c9fcdb77f35200581848041f222ed7f3
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66191957"
---
# <a name="upgrading-to-ad-fs-in-windows-server-2016-with-sql-server"></a>SQL Server 사용 하 여 Windows Server 2016에서에서 AD FS로 업그레이드



## <a name="moving-from-a-windows-server-2012-r2-ad-fs-farm-to-a-windows-server-2016-ad-fs-farm"></a>Windows Server 2016 AD FS 팜을 Windows Server 2012 R2 AD FS 팜에서 이동  
다음 문서에서는 AD FS 데이터베이스에 대 한 SQL Server를 사용 하는 경우 AD FS Windows Server 2012 R2 팜에 Windows Server 2016에서 AD FS로 업그레이드 하는 방법을 설명 합니다.  

### <a name="upgrading-ad-fs-to-windows-server-2016-fbl"></a>AD FS Windows Server 2016 FBL로 업그레이드  
새 Windows Server 2016 용 AD FS의 기능은 팜 동작 수준 (FBL)입니다.   이 기능을 팜 다양 하 고 AD FS 팜에 사용할 수 있는 기능을 결정 합니다.   Windows Server 2012 R2 AD FS 팜에서 FBL 기본적으로 Windows Server 2012 R2 FBL를 합니다.  

Windows Server 2016 AD FS 서버를 Windows Server 2012 R2 팜에 추가할 수 있습니다 및 Windows Server 2012 R2로 동일한 FBL에서 작동 합니다.  이 방식으로 작동 하는 Windows Server 2016 AD FS 서버에 있는 경우 "혼합" 될 팜에 라고 합니다.  그러나는 FBL Windows Server 2016으로 발생할 때까지 새 Windows Server 2016 기능을 활용할 수 없습니다.  혼합 팜과:  

-   관리자는 새로운 Windows Server 2012 R2 팜에 페더레이션 서버를 Windows Server 2016 추가할 수 있습니다.  결과적으로, 팜의 "mixed mode" 이며 Windows Server 2012 R2 팜 동작 수준 작동 합니다.  팜 전체에서 일관 된 동작을 보장 하려면 새 Windows Server 2016 기능을 구성 하거나이 모드에서 사용할 수 수 없습니다.  

-   관리자가 모든 Windows Server 2012 R2 페더레이션 서버에서 혼합된 모드 팜 제거한 후 주 노드 역할에 승격 된 새 Windows Serve 2016 페더레이션 서버 중 하나를 WID 팜의 경우 Win에서 FBL 발생 시킬 수 있습니다. dows Server 2012 R2를 Windows Server 2016 합니다.  결과적으로, 새 AD FS Windows Server 2016 기능 후 구성 및 사용할 수 있습니다.  

-   결과적으로 AD FS Windows Server 2012 R2 조직에 Windows Server 2016으로 업그레이드 하는 완전히 새로운 팜을 배포 하지 않아도 됩니다 혼합 된 팜 기능 데이터 내보내기 및 가져오기 구성 합니다.  대신이 온라인 상태인 동안 기존 팜에 Windows Server 2016 노드를 추가할 수 있으며만 비교적 간단한 가동 중지 시간이 발생 FBL raise에 관련 된 있습니다.  

팜 혼합된 모드에서 AD FS 팜에 아님을 새 기능이 나 Windows Server 2016에서 AD FS에 도입 된 기능 수에 유의 합니다.  즉, 새 기능을 사용해 하려는 조직에는 FBL 발생할 때까지이 수행할 수 없습니다.  따라서 조직에는 FBL rasing 하기 전에 새 기능을 테스트할 찾고이 위해 별도 팜을 배포 하는 것이 해야 합니다.  

나머지는 Windows Server 2012 R2 환경에 Windows Server 2016 페더레이션 서버를 추가 하 고 다음 Windows Server 2016으로 FBL 발생 하는 단계를 설명 됩니다.  이러한 단계는 아래 아키텍처 다이어그램에 설명 된 테스트 환경에서 수행 되었습니다.  

> [!NOTE]  
> Windows Server 2016 FBL에서 AD FS를 이동할 수 있습니다, 전에 Windows 2012 R2 노드를 모두 제거 해야 합니다.  Windows Server 2012 R2 운영 체제를 Windows Server 2016으로 업그레이드만 없으며 2016 노드 될 것 없습니다.  제거 하 고 새 2016 노드를 교체 해야 합니다.  

다음 아키텍처 다이어그램의 유효성을 검사 하 고 다음 단계를 기록 하는 데 사용 된 설치를 보여 줍니다.

![Architecture](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/arch.png)


#### <a name="join-the-windows-2016-ad-fs-server-to-the-ad-fs-farm"></a>Windows 2016 AD FS 서버를 AD FS 팜에 조인

1.  Windows Server 2016에서 서버 관리자 Active Directory Federation Services 역할 설치를 사용 하 여  

2.  AD FS 구성 마법사를 사용 하는 새 Windows Server 2016 서버를 기존 AD FS 팜에 가입 시킵니다.  에 **환영** 화면 클릭 **다음**합니다.
 ![팜 조인](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/configure1.png)  
3.  에 **Active Directory Domain Services에 연결** 화면, s**관리자 계정 지정** 클릭 하 여 페더레이션 서비스 구성을 수행할 권한이 있는 **다음**.
4.  에 **팜 지정** 화면, SQL server 및 인스턴스의 이름을 입력 하 고 클릭 **다음**합니다.
![팜 조인](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/configure3.png)
5.  에 **SSL 인증서 지정** 화면에서 인증서를 지정 하 고 클릭 **다음**합니다.
![팜 조인](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/configure4.png)
6.  에 **서비스 계정 지정** 화면에서 서비스 계정을 지정 하 고 클릭 **다음**합니다.
7.  에 **옵션을 검토** 화면에서 옵션을 검토 하 고 클릭 **다음**합니다.
8.  에 **필수 조건 검사** 화면에서 모든 필수 구성 요소 검사 통과 및 클릭 **구성**합니다.
9.  에 **결과** 화면에서 해당 서버가 제대로 구성 되었는지 확인 하 고 클릭 **닫기**합니다.


#### <a name="remove-the-windows-server-2012-r2-ad-fs-server"></a>Windows Server 2012 R2 AD FS 서버를 제거 합니다.

>[!NOTE]
>AdfsSyncProperties 집합을 사용 하 여 기본 AD FS 서버를 설정할 필요가 없습니다-데이터베이스와 SQL을 사용 하는 경우 역할입니다.  이 구성에서 기본으로 간주 됩니다 모든 노드의 때문입니다.

1.  Windows Server 2012 R2 AD FS 서버에서 서버 관리자 사용 **역할 및 기능 제거** 아래에서 **관리**합니다.
![서버 제거](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/remove1.png)
2.  **시작하기 전** 화면에서 **다음**을 클릭합니다.
3.  에 **서버 선택** 화면에서 클릭 **다음**합니다.
4.  에 **서버 역할** 화면에서 옆에 확인 제거 **Active Directory Federation Services** 클릭 **다음**합니다.
![서버 제거](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/remove2.png)
5.  에 **기능** 화면에서 클릭 **다음**합니다.
6.  에 **확인** 화면에서 클릭 **제거**합니다.
7.  이 완료 되 면 서버를 다시 시작 합니다.

#### <a name="raise-the-farm-behavior-level-fbl"></a>팜 동작 수준을 (FBL)를 발생 시킵니다.
이 단계 전에 forestprep 및 domainprep Active Directory 환경에서 실행 하 고 Active Directory에 Windows Server 2016 스키마를 지정 해야 합니다.  이 문서는 Windows 2016 도메인 컨트롤러를 사용 하 여 시작 하 고 AD가 설치 될 때 실행 하는 것 때문에 이러한 실행 필요가 없습니다.

>[!NOTE]
>아래 프로세스를 시작 하기 전에 설정을에서 Windows 업데이트를 실행 하 여 Windows Server 2016를 최신 상태로 유지 합니다.  업데이트가 더 이상 필요하지 않을 때까지 이 프로세스를 계속합니다.

1. 이제 Windows Server 2016 서버에서 PowerShell을 열고 다음을 실행 합니다. **$cred = Get-credential** 하 고 enter 키를 누릅니다.
2. SQL Server에 대 한 관리자 권한이 있는 자격 증명을 입력 합니다.
3. 이제 PowerShell에서 다음을 입력 합니다. **Invoke-AdfsFarmBehaviorLevelRaise -Credential $cred**
2. 메시지가 표시 되 면 입력 **Y**합니다.  수준 올리기 시작 됩니다.  이 작업이 완료 되는 FBL 제기해 했습니다.  
![업데이트 완료](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/finish1.png)
3. 이제 AD FS 관리 하려는 경우 Windows Server 2016에서 AD FS에 대 한 추가 된 새 노드가 표시 됩니다.  
4. 마찬가지로, PowerShell cmdlt을 사용할 수 있습니다.  Get-AdfsFarmInformation 현재 FBL 보여 줍니다.  
![업데이트 완료](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/finish2.png)

#### <a name="upgrade-the-configuration-version-of-existing-wap-servers"></a>기존 WAP 서버의 구성 버전 업그레이드
1. 각 웹 응용 프로그램 프록시에 다시 나타나는 창에서 다음 PowerShell 명령을 실행 하 여 WAP 구성:  
    ```powershell
    $trustcred = Get-Credential -Message "Enter Domain Administrator credentials"
    Install-WebApplicationProxy -CertificateThumbprint {SSLCert} -fsname fsname -FederationServiceTrustCredential $trustcred  
    ```
2. 클러스터에서 이전 서버를 제거 하 고 WAP 서버만 최신 서버 버전에서 실행 된 다음 Powershell commandlet을 실행 하 여 위의 다시 구성 하는 유지 합니다.
    ```powershell
    Set-WebApplicationProxyConfiguration -ConnectedServersName WAPServerName1, WAPServerName2
    ```
3. Get-WebApplicationProxyConfiguration commmandlet를 실행 하 여 WAP 구성을 확인 합니다. 이전 명령에서 실행 하는 서버를 ConnectedServersName에 반영 됩니다.
    ```powershell
    Get-WebApplicationProxyConfiguration
    ```
4. ConfigurationVersion WAP 서버를 업그레이드 하려면 다음 Powershell 명령을 실행 합니다.
    ```powershell
    Set-WebApplicationProxyConfiguration -UpgradeConfigurationVersion
    ```
5. ConfigurationVersion Get WebApplicationProxyConfiguration Powershell 명령을 사용 하 여 업그레이드를 확인 합니다.
    
