---
title: 고가용성을 사용 하 여 Windows 관리 센터 배포
description: 고가용성을 사용 하 여 Windows 관리 센터 배포 (Project Honolulu)
ms.technology: manage
ms.topic: article
author: jwwool
ms.author: jeffrew
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 6ae7bd9ed7aee5835ac1f53b9e10879ad8824f52
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406949"
---
# <a name="deploy-windows-admin-center-with-high-availability"></a>고가용성을 사용 하 여 Windows 관리 센터 배포

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

Windows 관리 센터 게이트웨이 서비스에 대해 고가용성을 제공 하기 위해 장애 조치 (failover) 클러스터에 Windows 관리 센터를 배포할 수 있습니다. 제공 된 솔루션은 Windows 관리 센터의 인스턴스가 하나만 활성화 된 활성-수동 솔루션입니다. 클러스터의 노드 중 하나가 실패 하면 Windows 관리 센터는 다른 노드로 정상적으로 장애 조치 하 여 환경에서 서버를 원활 하 게 관리할 수 있도록 합니다. 

[다른 Windows 관리 센터 배포 옵션에 대해 알아봅니다.](../plan/installation-options.md)

## <a name="prerequisites"></a>사전 요구 사항

- Windows Server 2016 또는 2019에서 2 개 이상의 노드로 이루어진 장애 조치 (failover) 클러스터 [장애 조치 (Failover) 클러스터 배포에 대해 자세히 알아보세요](../../../failover-clustering/failover-clustering-overview.md).
- Windows 관리 센터의 CSV (클러스터 공유 볼륨)는 클러스터의 모든 노드에서 액세스할 수 있는 영구 데이터를 저장 합니다. 10 GB는 CSV에 충분 합니다.
- [Windows 관리 센터 HA 스크립트 zip 파일](https://aka.ms/WACHAScript)의 고가용성 배포 스크립트입니다. 스크립트가 포함 된 .zip 파일을 로컬 컴퓨터에 다운로드 한 다음 아래 지침에 따라 필요에 따라 스크립트를 복사 합니다.
- 권장 되지만 선택 사항: 서명 된 인증서 .pfx & 암호입니다. 클러스터 노드에 인증서를 아직 설치 하지 않아도 됩니다. 스크립트에서이 작업을 수행 합니다. 제공 하지 않는 경우 설치 스크립트는 60 일 후에 만료 되는 자체 서명 된 인증서를 생성 합니다.

## <a name="install-windows-admin-center-on-a-failover-cluster"></a>장애 조치 (failover) 클러스터에 Windows 관리 센터 설치

1. @No__t-0 스크립트를 클러스터의 노드에 복사 합니다. Windows 관리 센터 .msi를 동일한 노드에 다운로드 하거나 복사 합니다.
2. RDP를 통해 노드에 연결 하 고 다음 매개 변수를 사용 하 여 해당 노드에서 ```Install-WindowsAdminCenterHA.ps1``` 스크립트를 실행 합니다.
    - `-clusterStorage`: Windows 관리 센터 데이터를 저장할 클러스터 공유 볼륨의 로컬 경로입니다.
    - `-clientAccessPoint`: Windows 관리 센터에 액세스 하는 데 사용할 이름을 선택 합니다. 예를 들어 `-clientAccessPoint contosoWindowsAdminCenter` 매개 변수를 사용 하 여 스크립트를 실행 하는 경우 `https://contosoWindowsAdminCenter.<domain>.com`을 방문 하 여 Windows 관리 센터 서비스에 액세스 합니다.
    - `-staticAddress`: (선택 사항) 클러스터 일반 서비스에 대 한 하나 이상의 정적 주소입니다. 
    - `-msiPath`: Windows 관리 센터 .msi 파일의 경로입니다.
    - `-certPath`: (선택 사항) 인증서 .pfx 파일의 경로입니다.
    - `-certPassword`: (선택 사항) @No__t에서 제공 하는 인증서 .pfx의 SecureString 암호입니다.-0
    - `-generateSslCert`: (선택 사항) 서명 된 인증서를 제공 하지 않으려면이 매개 변수 플래그를 포함 하 여 자체 서명 된 인증서를 생성 합니다. 자체 서명 된 인증서는 60 일 후에 만료 됩니다.
    - `-portNumber`: (선택 사항) 포트를 지정 하지 않으면 게이트웨이 서비스는 포트 443 (HTTPS)에 배포 됩니다. 다른 포트를 사용 하려면이 매개 변수에를 지정 합니다. 사용자 지정 포트 (443 외)를 사용 하는 경우 https://\<clientAccessPoint @ no__t-1: \<port @ no__t-3으로 이동 하 여 Windows 관리 센터에 액세스 합니다.

> [!NOTE]
> @No__t-0 스크립트는 ```-WhatIf ``` 및 ```-Verbose``` 매개 변수를 지원 합니다.

### <a name="examples"></a>예

#### <a name="install-with-a-signed-certificate"></a>서명 된 인증서를 사용 하 여 설치:

```powershell
$certPassword = Read-Host -AsSecureString
.\Install-WindowsAdminCenterHA.ps1 -clusterStorage "C:\ClusterStorage\Volume1" -clientAccessPoint "contoso-ha-gateway" -msiPath ".\WindowsAdminCenter.msi" -certPath "cert.pfx" -certPassword $certPassword -Verbose
```

#### <a name="install-with-a-self-signed-certificate"></a>자체 서명 된 인증서를 사용 하 여 설치:

```powershell
.\Install-WindowsAdminCenterHA.ps1 -clusterStorage "C:\ClusterStorage\Volume1" -clientAccessPoint "contoso-ha-gateway" -msiPath ".\WindowsAdminCenter.msi" -generateSslCert -Verbose
```

## <a name="update-an-existing-high-availability-installation"></a>기존 고가용성 설치 업데이트

연결 데이터를 잃지 않고 동일한 ```Install-WindowsAdminCenterHA.ps1``` 스크립트를 사용 하 여 HA 배포를 업데이트 합니다.

### <a name="update-to-a-new-version-of-windows-admin-center"></a>Windows 관리 센터의 새 버전으로 업데이트

Windows 관리 센터의 새 버전이 릴리스되면 ```msiPath``` 매개 변수만 사용 하 여 ```Install-WindowsAdminCenterHA.ps1``` 스크립트를 다시 실행 하면 됩니다.

```powershell
.\Install-WindowsAdminCenterHA.ps1 -msiPath '.\WindowsAdminCenter.msi' -Verbose
```

### <a name="update-the-certificate-used-by-windows-admin-center"></a>Windows 관리 센터에서 사용 하는 인증서 업데이트

언제 든 지 새 인증서의 .pfx 파일 및 암호를 제공 하 여 Windows 관리 센터의 HA 배포에서 사용 하는 인증서를 업데이트할 수 있습니다.

```powershell
$certPassword = Read-Host -AsSecureString
.\Install-WindowsAdminCenterHA.ps1 -certPath "cert.pfx" -certPassword $certPassword -Verbose
```

새 .msi 파일을 사용 하 여 Windows 관리 센터 플랫폼을 업데이트 하는 동시에 인증서를 업데이트할 수도 있습니다.

```powershell
$certPassword = Read-Host -AsSecureString
.\Install-WindowsAdminCenterHA.ps1 -msiPath ".\WindowsAdminCenter.msi" -certPath "cert.pfx" -certPassword $certPassword -Verbose
``` 

## <a name="uninstall"></a>Uninstall

장애 조치 (failover) 클러스터에서 Windows 관리 센터의 HA 배포를 제거 하려면 ```-Uninstall``` 매개 변수를 ```Install-WindowsAdminCenterHA.ps1``` 스크립트에 전달 합니다.

```powershell
.\Install-WindowsAdminCenterHA.ps1 -Uninstall -Verbose
```

## <a name="troubleshooting"></a>문제 해결

로그는 CSV의 temp 폴더 (예: C:\ClusterStorage\Volume1\temp)에 저장 됩니다.