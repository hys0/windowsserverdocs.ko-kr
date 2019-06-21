---
title: 고가용성을 사용 하 여 Windows Admin Center 배포
description: 고가용성 (프로젝트 브라 티)를 사용 하 여 Windows Admin Center 배포
ms.technology: manage
ms.topic: article
author: jwwool
ms.author: jeffrew
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: ad8e2a8eade1ea9d3faaba8f387b1f489854e589
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280627"
---
# <a name="deploy-windows-admin-center-with-high-availability"></a>고가용성을 사용 하 여 Windows Admin Center 배포

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

Windows Admin Center 게이트웨이 서비스에 대 한 고가용성을 제공 하려면 장애 조치 클러스터에서 Windows Admin Center 배포할 수 있습니다. 제공 하는 솔루션은 Windows Admin Center 인스턴스가 하나만 활성화 되어 있는 활성-수동 솔루션 합니다. 클러스터의 노드 중 하나가 실패 하면 Windows Admin Center 정상적으로 장애 조치를 다른 노드로 환경의 서버를 원활 하 게 관리를 계속할 수 있도록 합니다. 

[다른 Windows Admin Center 배포 옵션에 알아봅니다.](../plan/installation-options.md)

## <a name="prerequisites"></a>사전 요구 사항

- Windows Server 2016 또는 2019에 2 개 이상의 노드 장애 조치 클러스터입니다. [장애 조치 클러스터를 배포 하는 방법에 대 한 자세한](../../../failover-clustering/failover-clustering-overview.md)합니다.
- 클러스터 공유 볼륨 (CSV) 클러스터의 모든 노드에 액세스할 수 있는 영구 데이터를 저장 하려면 Windows Admin Center 대 한 합니다. CSV에 대 한 10GB 됩니다.
- 고가용성 배포 스크립트 [Windows Admin Center HA 스크립트 zip 파일](https://aka.ms/WACHAScript)합니다. 로컬 컴퓨터에 스크립트가 포함 된.zip 파일을 다운로드 하 고 스크립트 복사 하 고 필요에 따라 아래 지침에 따라 키를 누릅니다.
- 권장 되지만 선택 사항임: 서명 된 인증서.pfx 및 암호입니다. 클러스터 노드에서 인증서를 이미 설치 하지 않아도 됩니다.-스크립트는이 수 있습니다. 하나를 제공 하지 않으면 설치 스크립트는 60 일 후 만료 되는 자체 서명 된 인증서를 생성 합니다.

## <a name="install-windows-admin-center-on-a-failover-cluster"></a>장애 조치 클러스터 설치 Windows Admin Center

1. 복사를 ```Install-WindowsAdminCenterHA.ps1``` 클러스터의 노드에 스크립트입니다. 다운로드 하거나 Windows Admin Center.msi는 동일한 노드에 복사 합니다.
2. RDP 및 실행을 통해 노드에 연결 된 ```Install-WindowsAdminCenterHA.ps1``` 다음 매개 변수를 사용 하 여 해당 노드에서 스크립트:
    - `-clusterStorage`: Windows Admin Center 데이터를 저장 하는 클러스터 공유 볼륨의 로컬 경로입니다.
    - `-clientAccessPoint`: Windows Admin Center 액세스 하는 데 사용할 수 있는 이름을 선택 합니다. 예를 들어, 매개 변수를 사용 하 여 스크립트를 실행 하는 경우 `-clientAccessPoint contosoWindowsAdminCenter`를 방문 하 여 Windows Admin Center 서비스 액세스 `https://contosoWindowsAdminCenter.<domain>.com`
    - `-staticAddress`: (선택 사항) 클러스터 일반 서비스에 대 한 정적 주소를 하나 이상. 
    - `-msiPath`: Windows Admin Center.msi 파일에 대 한 경로입니다.
    - `-certPath`: (선택 사항) 인증서.pfx 파일에 대 한 경로입니다.
    - `-certPassword`: (선택 사항) 에 제공 된 인증서.pfx에 대 한 SecureString 암호 `-certPath`
    - `-generateSslCert`: (선택 사항) 서명 된 인증서를 제공 하지 않으려는 경우 자체 서명 된 인증서를 생성 하려면이 매개 변수 플래그를 포함 합니다. 자체 서명 된 인증서를 60 일 후 만료 됩니다를 참고 합니다.
    - `-portNumber`: (선택 사항) 포트를 지정 하지 않으면, 게이트웨이 서비스는 포트 443(https)에 배포 됩니다. 사용할 다른 포트는이 매개 변수에 지정 합니다. 사용자 지정 포트 (아무 것도 외에도 443)를 사용 하는 경우 액세스 하는 Windows Admin Center https://로 이동 하 여 참고\<clientAccessPoint\>:\<포트\>합니다.

> [!NOTE]
> 합니다 ```Install-WindowsAdminCenterHA.ps1``` 지원 스크립트 ```-WhatIf ``` 고 ```-Verbose``` 매개 변수

### <a name="examples"></a>예

#### <a name="install-with-a-signed-certificate"></a>서명 된 인증서를 사용 하 여 설치 합니다.

```powershell
$certPassword = Read-Host -AsSecureString
.\Install-WindowsAdminCenterHA.ps1 -clusterStorage "C:\ClusterStorage\Volume1" -clientAccessPoint "contoso-ha-gateway" -msiPath ".\WindowsAdminCenter.msi" -certPath "cert.pfx" -certPassword $certPassword -Verbose
```

#### <a name="install-with-a-self-signed-certificate"></a>자체 서명 된 인증서를 사용 하 여 설치 합니다.

```powershell
.\Install-WindowsAdminCenterHA.ps1 -clusterStorage "C:\ClusterStorage\Volume1" -clientAccessPoint "contoso-ha-gateway" -msiPath ".\WindowsAdminCenter.msi" -generateSslCert -Verbose
```

## <a name="update-an-existing-high-availability-installation"></a>기존 고가용성 설치 업데이트

사용한 것과 동일한 ```Install-WindowsAdminCenterHA.ps1``` 연결 데이터 손실 없이 HA 배포를 업데이트 하는 스크립트입니다.

### <a name="update-to-a-new-version-of-windows-admin-center"></a>Windows Admin Center 새 버전으로 업데이트

Windows Admin Center 새 버전이 출시 되 면 실행 하기만 하면 됩니다 합니다 ```Install-WindowsAdminCenterHA.ps1``` 다시만 포함 하는 스크립트는 ```msiPath``` 매개 변수:

```powershell
.\Install-WindowsAdminCenterHA.ps1 -msiPath '.\WindowsAdminCenter.msi' -Verbose
```

### <a name="update-the-certificate-used-by-windows-admin-center"></a>Windows Admin Center 사용 하는 인증서 업데이트

새 인증서의.pfx 파일 및 암호를 제공 하 여 언제 든 지 Windows Admin Center HA 배포에서 사용 된 인증서를 업데이트할 수 있습니다.

```powershell
$certPassword = Read-Host -AsSecureString
.\Install-WindowsAdminCenterHA.ps1 -certPath "cert.pfx" -certPassword $certPassword -Verbose
```

또한 새.msi 파일을 사용 하 여 Windows Admin Center 플랫폼을 업데이트 하는 동시에 인증서를 업데이트할 수 있습니다.

```powershell
$certPassword = Read-Host -AsSecureString
.\Install-WindowsAdminCenterHA.ps1 -msiPath ".\WindowsAdminCenter.msi" -certPath "cert.pfx" -certPassword $certPassword -Verbose
``` 

## <a name="uninstall"></a>Uninstall

Windows Admin Center HA 배포에서 장애 조치 클러스터를 제거 하려면 전달 된 ```-Uninstall``` 매개 변수를는 ```Install-WindowsAdminCenterHA.ps1``` 스크립트입니다.

```powershell
.\Install-WindowsAdminCenterHA.ps1 -Uninstall -Verbose
```

## <a name="troubleshooting"></a>문제 해결

로그 (예를 들어 C:\ClusterStorage\Volume1\temp) CSV의 임시 폴더에 저장 됩니다.