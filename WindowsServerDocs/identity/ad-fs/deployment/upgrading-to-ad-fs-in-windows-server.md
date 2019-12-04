---
ms.assetid: 7671e0c9-faf0-40de-808a-62f54645f891
title: Windows Server 2016의 AD FS로 업그레이드
description: ''
author: billmath
manager: femila
ms.date: 04/09/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 428e35524fbcfe5177b544e1c6cc6fa32ec32056
ms.sourcegitcommit: 4a03f263952c993dfdf339dd3491c73719854aba
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2019
ms.locfileid: "74791373"
---
# <a name="upgrading-to-ad-fs-in-windows-server-2016-using-a-wid-database"></a>WID 데이터베이스를 사용하여 Windows Server 2016에서 AD FS로 업그레이드


> [!NOTE]
> 완료를 위해 계획 된 시간 프레임을 사용 하 여 업그레이드를 시작 합니다. 확장 된 시간 동안 AD FS를 혼합 모드 상태로 유지 하지 않는 것이 좋습니다 .이 경우 혼합 모드 상태에서 AD FS 벗어나면 팜에 문제가 발생할 수 있습니다.

## <a name="upgrading-a-windows-server-2012-r2-or-2016-ad-fs-farm-to-windows-server-2019"></a>Windows Server 2012 R2 또는 2016 AD FS 팜을 Windows Server 2019로 업그레이드
다음 문서에서는 WID 데이터베이스를 사용 하는 경우 AD FS 팜을 Windows Server 2019에서 AD FS로 업그레이드 하는 방법을 설명 합니다.

### <a name="ad-fs-farm-behavior-levels-fbl"></a>AD FS 팜 동작 수준 (FBL)
Windows Server 2016에 대 한 AD FS에서 팜 동작 수준 (FBL)이 도입 되었습니다. 이는 AD FS 팜이 사용할 수 있는 기능을 결정 하는 팜 전체 설정입니다.

다음 표에는 Windows Server 버전에 따라 FBL 값이 나열 되어 있습니다.

| Windows Server 버전  | FBL | AD FS 구성 데이터베이스 이름 |
| ------------- | ------------- | ------------- |
| 2012 R2  | 1  | AdfsConfiguration |
| 2016  | 3  | AdfsConfigurationV3 |
| 2019  | 추가를 클릭합니다.  | AdfsConfigurationV4 |

> [!NOTE]
> FBL를 업그레이드 하면 새 AD FS 구성 데이터베이스가 만들어집니다.  각 Windows Server AD FS version 및 FBL 값에 대 한 구성 데이터베이스의 이름은 위의 표를 참조 하세요.

### <a name="new-vs-upgraded-farms"></a>새 팜 및 업그레이드 된 팜
기본적으로 새 AD FS 팜의 FBL는 설치 된 첫 번째 팜 노드의 Windows Server 버전에 대 한 값과 일치 합니다.

이후 버전의 AD FS 서버를 AD FS 2012 R2 또는 2016 팜에 조인할 수 있으며, 팜이 기존 노드와 동일한 FBL에서 작동 합니다. 가장 낮은 버전의 FBL 값에 있는 동일한 팜에서 여러 Windows Server 버전을 운영 하는 경우 팜이 "mixed" 라고 합니다. 그러나 FBL이 발생 하기 전에는 이후 버전의 기능을 활용할 수 없습니다. 혼합 팜 사용:

- 관리자는 새 Windows Server 2019 페더레이션 서버를 기존 Windows Server 2012 R2 또는 2016 팜에 추가할 수 있습니다. 결과적으로 팜은 "혼합 모드" 이며 원래 팜과 동일한 팜 동작 수준에서 작동 합니다. 팜 전체에서 일관 된 동작을 보장 하기 위해 최신 Windows Server AD FS 버전의 기능을 구성 하거나 사용할 수 없습니다.

- FBL를 발생 시키려면 관리자는 팜에서 이전 Windows Server 버전의 AD FS 노드를 제거 해야 합니다.  WID 팜의 경우에는 새 Windows Server 2019 페더레이션 서버 중 하나가 팜의 주 노드 역할로 승격 되어야 한다는 점에 유의 해야 합니다.

- 팜의 모든 페더레이션 서버가 동일한 Windows Server 버전에 있으면 FBL 발생할 수 있습니다.  따라서 새로운 AD FS Windows Server 2019 기능을 구성 하 고 사용할 수 있습니다.

혼합 팜 모드에서는 AD FS 팜이 Windows Server 2019의 AD FS에 도입 된 새로운 기능 또는 기능을 사용할 수 없습니다. 즉, 새 기능을 사용해 보려는 조직은 FBL 발생할 때까지이 작업을 수행할 수 없습니다. 따라서 조직에서 FBL를 발생 시키기 전에 새 기능을 테스트 하려는 경우 별도의 팜을 배포 하 여이 작업을 수행 해야 합니다.

이 문서의 나머지 부분에서는 windows server 2019 페더레이션 서버를 windows server 2016 또는 2012 R2 환경에 추가 하 고 FBL를 Windows Server 2019로 올리는 단계를 제공 합니다. 이러한 단계는 아래 아키텍처 다이어그램에 설명 된 테스트 환경에서 수행 되었습니다.

> [!NOTE]
> Windows Server 2019 FBL에서 AD FS로 이동 하려면 먼저 Windows Server 2016 또는 2012 R2 노드를 모두 제거 해야 합니다. Windows Server 2016 또는 2012 R2 OS를 Windows Server 2019로 업그레이드 하 여 2019 노드가 될 수는 없습니다. 이를 제거 하 고 새 2019 노드로 바꾸어야 합니다.

##### <a name="to-upgrade-your-ad-fs-farm-to-windows-server-2019-farm-behavior-level"></a>AD FS 팜을 Windows Server 2019 팜 동작 수준으로 업그레이드 하려면

1. 서버 관리자를 사용 하 여 Windows Server 2019에 Active Directory Federation Services 역할을 설치 합니다.

2. AD FS 구성 마법사를 사용 하 여 새 Windows Server 2019 서버를 기존 AD FS 팜에 가입 시킵니다.

![업그레이드](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_1.png)

3. Windows Server 2019 페더레이션 서버에서 AD FS 관리를 엽니다. 이 페더레이션 서버는 주 서버가 아니므로 관리 기능을 사용할 수 없습니다.

![업그레이드](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_3.png)

4. Windows Server 2019 서버에서 관리자 권한 PowerShell 명령 창을 열고 다음 cmdlet을 실행 합니다.

```PowerShell
Set-AdfsSyncProperties -Role PrimaryComputer
```

![업그레이드](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_4.png)

5. 이전에 기본으로 구성 된 AD FS 서버에서 관리자 권한 PowerShell 명령 창을 열고 다음 cmdlet을 실행 합니다.

```PowerShell
Set-AdfsSyncProperties -Role SecondaryComputer -PrimaryComputerName {FQDN}
```

![업그레이드](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_5.png)

6. 이제 Windows Server 2016 페더레이션 서버에서 AD FS 관리를 엽니다. 이제 주 역할이이 서버로 전송 되었으므로 모든 관리 기능이 표시 됩니다.

![업그레이드](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_6.png)

7. AD FS 2012 R2 팜을 2016 또는 2019로 업그레이드 하는 경우 팜 업그레이드를 수행 하려면 AD 스키마가 수준 85 이상 이어야 합니다.  Windows Server 2016 설치 미디어를 사용 하 여 스키마를 업그레이드 하려면 명령 프롬프트를 열고 support\adprep 디렉터리로 이동 합니다. 다음을 실행 합니다. `adprep /forestprep`

![업그레이드](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_7.png)

완료 되 면 실행 `adprep/domainprep`

> [!NOTE]
> 다음 단계를 실행 하기 전에 설정에서 Windows 업데이트를 실행 하 여 Windows Server가 최신 상태 인지 확인 합니다. 업데이트가 더 이상 필요하지 않을 때까지 이 프로세스를 계속합니다.

![업그레이드](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_8.png)

8. 이제 Windows Server 2016 서버에서 PowerShell을 열고 다음 cmdlet을 실행 합니다.

> [!NOTE]
> 다음 단계를 실행 하기 전에 팜에서 모든 2012 R2 서버를 제거 해야 합니다.

```PowerShell
Invoke-AdfsFarmBehaviorLevelRaise
```

![업그레이드](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_9.png)

9. 메시지가 표시 되 면 Y를 입력 합니다. 그러면 수준이 시작 됩니다. 이 작업이 완료 되 면 FBL 성공적으로 발생 합니다.

![업그레이드](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_10.png)

10. 이제 AD FS 관리로 이동 하면 이후 AD FS 버전에 대 한 새로운 기능이 추가 된 것을 확인할 수 있습니다.

![업그레이드](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_12.png)

11. 마찬가지로 `Get-AdfsFarmInformation` PowerShell cmdlet을 사용 하 여 현재 FBL을 표시할 수 있습니다.

![업그레이드](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_13.png)

12. WAP 서버를 최신 수준으로 업그레이드 하려면 각 웹 응용 프로그램 프록시에서 관리자 권한 창에서 다음 PowerShell cmdlet을 실행 하 여 WAP를 다시 구성 합니다.

```PowerShell
$trustcred = Get-Credential -Message "Enter Domain Administrator credentials"
Install-WebApplicationProxy -CertificateThumbprint {SSLCert} -fsname fsname -FederationServiceTrustCredential $trustcred
```

클러스터에서 이전 서버를 제거 하 고 다음 Powershell cmdlet을 실행 하 여 위에서 다시 구성한 최신 서버 버전을 실행 하는 WAP 서버만 유지 합니다.

```PowerShell
Set-WebApplicationProxyConfiguration -ConnectedServersName WAPServerName1, WAPServerName2
```

Set-webapplicationproxyconfiguration cmdlet을 실행 하 여 WAP 구성을 확인 합니다. ConnectedServersName는 이전 명령의 서버 실행을 반영 합니다.

```PowerShell
Get-WebApplicationProxyConfiguration
```
ConfigurationVersion의 WAP 서버를 업그레이드 하려면 다음 Powershell 명령을 실행 합니다.

```PowerShell
Set-WebApplicationProxyConfiguration -UpgradeConfigurationVersion
```

그러면 WAP 서버 업그레이드를 완료 합니다.
