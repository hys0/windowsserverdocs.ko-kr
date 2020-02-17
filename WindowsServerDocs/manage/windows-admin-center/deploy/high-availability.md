---
title: 고가용성을 사용하여 Windows Admin Center 배포
description: 고가용성을 사용하여 Windows Admin Center 배포(Project Honolulu)
ms.technology: manage
ms.topic: article
author: jwwool
ms.author: jeffrew
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 6ae7bd9ed7aee5835ac1f53b9e10879ad8824f52
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406949"
---
# <a name="deploy-windows-admin-center-with-high-availability"></a>고가용성을 사용하여 Windows Admin Center 배포

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

Windows Admin Center 게이트웨이 서비스에 대해 고가용성을 제공하기 위해 장애 조치(failover) 클러스터에 Windows Admin Center를 배포할 수 있습니다. 제공된 솔루션은 Windows Admin Center의 인스턴스가 하나만 활성화된 활성-수동 솔루션입니다. 클러스터의 노드 중 하나가 실패하면 Windows Admin Center는 다른 노드로 정상적으로 장애 조치하여 환경에서 서버를 원활하게 관리할 수 있도록 합니다. 

[다른 Windows Admin Center 배포 옵션에 대해 알아봅니다.](../plan/installation-options.md)

## <a name="prerequisites"></a>필수 구성 요소

- Windows Server 2016 또는 2019에서 2개 이상의 노드로 이루어진 장애 조치(failover) 클러스터 [장애 조치(Failover) 클러스터 배포에 대한 자세한 정보](../../../failover-clustering/failover-clustering-overview.md)
- Windows Admin Center의 CSV(클러스터 공유 볼륨)는 클러스터의 모든 노드에서 액세스할 수 있는 영구 데이터를 저장합니다. 10GB는 CSV에 충분합니다.
- [Windows Admin Center HA 스크립트 zip 파일](https://aka.ms/WACHAScript)의 고가용성 배포 스크립트입니다. 스크립트가 포함된 .zip 파일을 로컬 머신에 다운로드한 다음, 아래 지침에 따라 필요에 따라 스크립트를 복사합니다.
- 권장되지만 선택 사항: 서명된 인증서 .pfx 및 암호 클러스터 노드에 인증서를 아직 설치하지 않아도 됩니다. 스크립트에서 이 작업을 수행합니다. 제공하지 않는 경우 설치 스크립트는 60일 후에 만료되는 자체 서명된 인증서를 생성합니다.

## <a name="install-windows-admin-center-on-a-failover-cluster"></a>장애 조치(failover) 클러스터에 Windows Admin Center 설치

1. ```Install-WindowsAdminCenterHA.ps1``` 스크립트를 클러스터의 노드에 복사합니다. Windows Admin Center .msi를 동일한 노드에 다운로드하거나 복사합니다.
2. RDP를 통해 노드에 연결하고 다음 매개 변수를 사용하여 해당 노드에서 ```Install-WindowsAdminCenterHA.ps1``` 스크립트를 실행합니다.
    - `-clusterStorage`: Windows Admin Center 데이터를 저장할 클러스터 공유 볼륨의 로컬 경로입니다.
    - `-clientAccessPoint`: Windows Admin Center에 액세스하는 데 사용할 이름을 선택합니다. 예를 들어 `-clientAccessPoint contosoWindowsAdminCenter` 매개 변수를 사용하여 스크립트를 실행하는 경우 `https://contosoWindowsAdminCenter.<domain>.com`을 방문하여 Windows Admin Center 서비스에 액세스합니다.
    - `-staticAddress`: 선택 사항입니다. 클러스터 일반 서비스에 대한 하나 이상의 정적 주소입니다. 
    - `-msiPath`: Windows Admin Center .msi 파일의 경로입니다.
    - `-certPath`: 선택 사항입니다. 인증서 .pfx 파일의 경로입니다.
    - `-certPassword`: 선택 사항입니다. `-certPath`에서 제공하는 인증서 .pfx에 대한 SecureString 암호입니다.
    - `-generateSslCert`: 선택 사항입니다. 서명된 인증서를 제공하지 않으려면 이 매개 변수 플래그를 포함하여 자체 서명된 인증서를 생성합니다. 자체 서명된 인증서는 60일 후에 만료됩니다.
    - `-portNumber`: 선택 사항입니다. 포트를 지정하지 않으면 게이트웨이 서비스는 포트 443(HTTPS)에 배포됩니다. 다른 포트를 사용하려면 이 매개 변수에서 지정합니다. 사용자 지정 포트(443 외)를 사용하는 경우 https://\<clientAccessPoint\>:\<포트\>로 이동하여 Windows Admin Center에 액세스합니다.

> [!NOTE]
> ```Install-WindowsAdminCenterHA.ps1``` 스크립트는 ```-WhatIf ``` 및 ```-Verbose``` 매개 변수를 지원합니다.

### <a name="examples"></a>예

#### <a name="install-with-a-signed-certificate"></a>서명된 인증서를 사용하여 설치:

```powershell
$certPassword = Read-Host -AsSecureString
.\Install-WindowsAdminCenterHA.ps1 -clusterStorage "C:\ClusterStorage\Volume1" -clientAccessPoint "contoso-ha-gateway" -msiPath ".\WindowsAdminCenter.msi" -certPath "cert.pfx" -certPassword $certPassword -Verbose
```

#### <a name="install-with-a-self-signed-certificate"></a>자체 서명된 인증서를 사용하여 설치:

```powershell
.\Install-WindowsAdminCenterHA.ps1 -clusterStorage "C:\ClusterStorage\Volume1" -clientAccessPoint "contoso-ha-gateway" -msiPath ".\WindowsAdminCenter.msi" -generateSslCert -Verbose
```

## <a name="update-an-existing-high-availability-installation"></a>기존 고가용성 설치 업데이트

연결 데이터를 잃지 않고 동일한 ```Install-WindowsAdminCenterHA.ps1``` 스크립트를 사용하여 HA 배포를 업데이트합니다.

### <a name="update-to-a-new-version-of-windows-admin-center"></a>새 버전의 Windows Admin Center로 업데이트

Windows Admin Center의 새 버전이 릴리스되면 ```msiPath``` 매개 변수만 사용하여 ```Install-WindowsAdminCenterHA.ps1``` 스크립트를 다시 실행하면 됩니다.

```powershell
.\Install-WindowsAdminCenterHA.ps1 -msiPath '.\WindowsAdminCenter.msi' -Verbose
```

### <a name="update-the-certificate-used-by-windows-admin-center"></a>Windows Admin Center에서 사용하는 인증서 업데이트

언제든지 새 인증서의 .pfx 파일 및 암호를 제공하여 Windows Admin Center의 HA 배포에서 사용하는 인증서를 업데이트할 수 있습니다.

```powershell
$certPassword = Read-Host -AsSecureString
.\Install-WindowsAdminCenterHA.ps1 -certPath "cert.pfx" -certPassword $certPassword -Verbose
```

새 .msi 파일을 사용하여 Windows Admin Center 플랫폼을 업데이트하는 동시에 인증서를 업데이트할 수도 있습니다.

```powershell
$certPassword = Read-Host -AsSecureString
.\Install-WindowsAdminCenterHA.ps1 -msiPath ".\WindowsAdminCenter.msi" -certPath "cert.pfx" -certPassword $certPassword -Verbose
``` 

## <a name="uninstall"></a>제거

장애 조치(failover) 클러스터에서 Windows Admin Center의 HA 배포를 제거하려면 ```-Uninstall``` 매개 변수를 ```Install-WindowsAdminCenterHA.ps1``` 스크립트에 전달합니다.

```powershell
.\Install-WindowsAdminCenterHA.ps1 -Uninstall -Verbose
```

## <a name="troubleshooting"></a>문제 해결

로그는 CSV의 임시 폴더(예: C:\ClusterStorage\Volume1\temp)에 저장됩니다.