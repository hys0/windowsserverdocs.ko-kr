---
ms.assetid: 7671e0c9-faf0-40de-808a-62f54645f891
title: Windows Server 2016의 AD FS로 업그레이드
description: ''
author: billmath
manager: femila
ms.date: 04/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: c8e72f1075b984506f9f992cd45cf853b50bddeb
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66191925"
---
# <a name="upgrading-to-ad-fs-in-windows-server-2016-using-a-wid-database"></a>WID 데이터베이스를 사용하여 Windows Server 2016에서 AD FS로 업그레이드



## <a name="upgrading-a-windows-server-2012-r2-or-2016-ad-fs-farm-to-windows-server-2019"></a>Windows Server 2012 R2 또는 2016 AD FS 팜을 Windows Server 2019로 업그레이드
다음 문서에서는 WID 데이터베이스를 사용 하는 경우 AD fs Windows Server 2019에 AD FS 팜을 업그레이드 하는 방법을 설명 합니다.  

### <a name="ad-fs-farm-behavior-levels-fbl"></a>AD FS 팜 동작 수준 (FBL)  
Windows Server 2016 용 AD FS에서 팜 동작 수준 (FBL) 도입 되었습니다. 기능 AD FS 팜을 사용 하 여 수를 결정 하는 팜 전체 설정입니다.

다음 표에서 Windows Server 버전에서 FBL 값을 나열합니다.
| Windows Server 버전  | FBL | AD FS 구성 데이터베이스 이름 |
| ------------- | ------------- | ------------- |
| 2012 R2  | 1  | AdfsConfiguration |
| 2016  | 3  | AdfsConfigurationV3 |
| 2019  | 4  | AdfsConfigurationV4 |

> [!NOTE]  
> 업그레이드는 FBL 새 AD FS 구성 데이터베이스를 만듭니다.  각 Windows Server AD FS 버전 및 FBL 값에 대 한 구성 데이터베이스의 이름에 대 한 위의 표를 참조 하세요.

### <a name="new-vs-upgraded-farms"></a>새 vs Upgraded 팜
기본적으로 새 AD FS 팜의 FBL 설치 된 첫 번째 팜 노드의 Windows Server 버전에 대 한 값을 찾습니다.  

이상 버전의 AD FS 서버는 AD FS 2012 R2 또는 2016 팜에 조인할 수 있습니다 하 고 팜의 기존 노드를 동일한 FBL에서 작동 합니다. FBL 값 가장 낮은 버전을 동일한 팜에에서 작동 하는 여러 Windows Server 버전에 있는 경우 "혼합" 될 팜에 라고 합니다. 그러나는 FBL 발생할 때까지 이후 버전의 기능을 활용할 수 없게 됩니다. 혼합 팜과:  

-   관리자는 기존 Windows Server 2012 R2 또는 2016 팜에 새 Windows Server 2019 페더레이션 서버를 추가할 수 있습니다. 결과적으로, 팜의 "mixed mode" 이며 원래 팜과 동일한 팜 동작 수준에서 작동 합니다. 팜 전체에서 일관 된 동작을 보장 하려면 최신 Windows Server AD FS 버전의 기능을 구성 하거나 사용할 수 수 없습니다.  

- FBL 발생할 수 있습니다, 전에 관리자는 팜에서 이전 Windows Server 버전의 AD FS 노드를 제거 해야 합니다.  WID 팜의 경우 팜에서 주 노드 역할에 새 Windows Server 2019 페더레이션 서버 tp 중 하나에서는이 승격 합니다.

-   팜의 모든 페더레이션 서버는 동일한 Windows Server 버전에서 되 면는 FBL 발생할 수 있습니다.  결과적으로, 새 AD FS Windows Server 2019 기능 후 구성 및 사용할 수 있습니다.

팜 혼합된 모드에서 AD FS 팜에 아님을 새 기능이 나 Windows Server 2019에서 AD FS에 도입 된 기능 수에 유의 합니다. 즉, 새 기능을 사용해 하려는 조직에는 FBL 발생할 때까지이 수행할 수 없습니다. 따라서 조직에는 FBL rasing 하기 전에 새 기능을 테스트할 찾고이 위해 별도 팜을 배포 하는 것이 해야 합니다.  

나머지는 문서는 Windows Server 2016 또는 2012 R2 환경에 Windows Server 2019 페더레이션 서버를 추가 하 고 Windows Server 2019에 FBL 발생 시키는 다음 단계를 제공 됩니다. 이러한 단계는 아래 아키텍처 다이어그램에 설명 된 테스트 환경에서 수행 되었습니다.  

> [!NOTE]  
> Windows Server 2019 FBL에서 AD FS를 이동할 수 있습니다, 전에 Windows Server 2016의 모든 또는 2012 R2 노드를 제거 해야 합니다. Windows Server 2016 또는 2012 R2 운영 체제를 Windows Server 2019 업그레이드만 없으며 2019 노드 될 것 없습니다. 제거 하 고 새 2019 노드를 교체 해야 합니다.



##### <a name="to-upgrade-your-ad-fs-farm-to-windows-server-2019-farm-behavior-level"></a>Windows Server 2019 팜 동작 수준에 AD FS 팜을 업그레이드 하려면  

1.  Windows Server 2019 Active Directory Federation Services 역할 설치 서버 관리자 사용

2.  AD FS 구성 마법사를 사용 하는 새 Windows Server 2019 서버를 기존 AD FS 팜에 가입 시킵니다.  

    ![업그레이드](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_1.png)  

3.  Windows Server 2019 페더레이션 서버의 AD FS 관리를 엽니다. 이 페더레이션 서버는 주 서버에 없기 때문에 관리 기능을 사용할 수는 참고 합니다.  

    ![업그레이드](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_3.png)  

4.  Windows Server 2019 서버에서 관리자 권한 PowerShell 명령 창을 열고 다음 cmdlt을 실행 합니다. `Set-AdfsSyncProperties -Role PrimaryComputer`

    ![업그레이드](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_4.png)  

5.  기본으로 이전에 구성 된 AD FS 서버에서 관리자 권한 PowerShell 명령 창을 열고 다음 cmdlt을 실행 합니다. `Set-AdfsSyncProperties -Role SecondaryComputer -PrimaryComputerName {FQDN} `

    ![업그레이드](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_5.png)  

6.  이제 Windows Server 2016 페더레이션 서버의 AD FS 관리를 엽니다. 주 역할에서이 서버에 전송 된 때문에 표시 하는 관리 기능을 모두 이제는 note 합니다.  

    ![업그레이드](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_6.png)  

7.  팜 업그레이드가 필요한 AD 스키마를 2019 2016에 AD FS 2012 R2 팜에 업그레이드 하는 경우 85를 최소 수준입니다.  스키마, Windows Server 2016 사용 하 여 설치 미디어를 업그레이드 하려면 명령 프롬프트를 열고 support\adprep 디렉터리로 이동 합니다. 다음을 실행 합니다.  `adprep /forestprep`

    ![업그레이드](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_7.png)  

    작업이 완료 된 후 실행 `adprep/domainprep`
    >[!NOTE]
    >다음 단계를 실행 하기 전에 설정을에서 Windows 업데이트를 실행 하 여 Windows Server를 최신 상태로 유지 합니다. 업데이트가 더 이상 필요하지 않을 때까지 이 프로세스를 계속합니다.
    >

    ![업그레이드](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_8.png)  

8. 이제 Windows Server 2016 서버에서 PowerShell을 열고 다음 cmdlt을 실행 합니다.
    >[!NOTE]
    > 다음 단계를 실행 하기 전에 모든 2012 R2 서버 팜에서 제거 해야 합니다.

    `Invoke-AdfsFarmBehaviorLevelRaise`  

    ![업그레이드](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_9.png)  

9. 대화 상자가 나타나면 Y를 입력 합니다. 수준 올리기 시작 됩니다. 이 작업이 완료 되는 FBL 제기해 했습니다.  

    ![업그레이드](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_10.png)  

10. 이제 AD FS 관리로 이동 하면 표시 됩니다 이상 AD FS 버전에 대 한 새 기능이 추가 되었습니다.

    ![업그레이드](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_12.png)  

11. 마찬가지로, PowerShell cmdlt을 사용할 수 있습니다: `Get-AdfsFarmInformation` 현재 FBL 보여 줍니다.  

    ![업그레이드](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_13.png)  

12. 각 웹 응용 프로그램 프록시에 최신 수준으로 WAP 서버를 업그레이드 하려면 관리자 권한 창에서 다음 PowerShell 명령을 실행 하 여 WAP 다시 구성:  
    ```powershell
    $trustcred = Get-Credential -Message "Enter Domain Administrator credentials"
    Install-WebApplicationProxy -CertificateThumbprint {SSLCert} -fsname fsname -FederationServiceTrustCredential $trustcred  
    ```
    클러스터에서 이전 서버를 제거 하 고 WAP 서버만 최신 서버 버전에서 실행 된 다음 Powershell commandlet을 실행 하 여 위의 다시 구성 하는 유지 합니다.
    ```powershell
    Set-WebApplicationProxyConfiguration -ConnectedServersName WAPServerName1, WAPServerName2
    ```
    Get-WebApplicationProxyConfiguration commmandlet를 실행 하 여 WAP 구성을 확인 합니다. 이전 명령에서 실행 하는 서버를 ConnectedServersName에 반영 됩니다.
    ```powershell
    Get-WebApplicationProxyConfiguration
    ```
    ConfigurationVersion WAP 서버를 업그레이드 하려면 다음 Powershell 명령을 실행 합니다.
    ```powershell
    Set-WebApplicationProxyConfiguration -UpgradeConfigurationVersion
    ```
    이 WAP 서버 업그레이드를 완료 합니다.
