---
title: 높은 가용성과 함께 Windows Admin Center를 배포
description: 고가용성 (Project Honolulu)를 사용 하 여 Windows Admin Center를 배포
ms.technology: manage
ms.topic: article
author: jwwool
ms.author: jeffrew
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: a0062230dd3d9e9c52aa317f87e06b0e84507dc4
ms.sourcegitcommit: 802a7bd537cab22893abb7e6657c4be90346ef88
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "9025035"
---
# 높은 가용성과 함께 Windows Admin Center를 배포

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

Windows Admin Center 게이트웨이 서비스에 대 한 고가용성을 제공 하기 위해 장애 조치 클러스터에 Windows Admin Center를 배포할 수 있습니다. 제공 된 솔루션이 Windows Admin Center의 한 인스턴스만 활성화 되는 활성 수동 솔루션이입니다. 클러스터 노드 중 하나에 실패 하는 경우 Windows Admin Center 정상적으로 장애 조치 다른 노드로 환경에서 서버를 원활 하 게 관리 계속 수 있습니다. 

[다른 Windows Admin Center 배포 옵션에 알아봅니다.](../plan/installation-options.md)

## 필수 조건

- Windows Server 2016 또는 2019에 두 개 이상의 노드의 장애 조치 클러스터 합니다. [장애 조치 클러스터 배포에 대해 자세히 알아봅니다](../../../failover-clustering/failover-clustering-overview.md).
- 클러스터 공유 볼륨 (CSV) 클러스터의 모든 노드에서 액세스할 수 있는 영구 데이터를 저장 하는 Windows Admin Center에 대 한 됩니다. 10GB에 CSV에 대 한 충분 한 수 있습니다.
- [Windows Admin Center HA 스크립트 zip 파일](https://aka.ms/WACHAScript)에서 고가용성 배포 스크립트입니다. 로컬 컴퓨터에 스크립트가 포함 된.zip 파일을 다운로드 한 다음 복사 스크립트 필요에 따라 아래 지침에 따라 합니다.
- 좋지만 선택 사항: 서명 된 인증서.pfx & 암호. 클러스터 노드에서 인증서를 이미 설치한 필요가 없습니다-스크립트는는 않습니다. 하나를 지정 하지 않으면, 설치 스크립트 60 일이 지나면 만료 되는 자체 서명 된 인증서를 생성 합니다.

## 장애 조치 클러스터에 Windows Admin Center 설치

1. 복사의 ```Install-WindowsAdminCenterHA.ps1``` 스크립트를 클러스터의 노드로 합니다. 다운로드 하거나 Windows Admin Center.msi 같은 노드에 복사 합니다.
2. RDP 및 실행을 통해 노드에 연결 하는 ```Install-WindowsAdminCenterHA.ps1``` 스크립트는 다음 매개 변수를 사용 하 여 해당 노드에서:
    - `-clusterStorage`: Windows Admin Center 데이터를 저장 하는 클러스터 공유 볼륨의 로컬 경로입니다.
    - `-clientAccessPoint`: Windows Admin Center에 액세스 하는 데 사용할 수 있는 이름을 선택 합니다. 예를 들어, 매개 변수를 사용 하 여 스크립트를 실행 하는 경우 `-clientAccessPoint contosoWindowsAdminCenter`를 방문 하 여 Windows Admin Center 서비스에 액세스 합니다 `https://contosoWindowsAdminCenter.<domain>.com`
    - `-staticAddress`: 선택 사항입니다. 클러스터 일반 서비스에 대 한 하나 이상의 정적 주소입니다. 
    - `-msiPath`: Windows Admin Center.msi 파일에 대 한 경로입니다.
    - `-certPath`: 선택 사항입니다. 인증서는.pfx 파일의 경로입니다.
    - `-certPassword`: 선택 사항입니다. 에 제공 된 인증서.pfx에 대 한 SecureString 암호 `-certPath`
    - `-generateSslCert`: 선택 사항입니다. 서명 된 인증서를 제공 하기 위해 않으려는 경우에 자체 서명 된 인증서를 생성 하려면이 매개 변수 플래그를 포함 됩니다. 참고 자체 서명 된 인증서 60 일 내에 만료 됩니다.
    - `-portNumber`: 선택 사항입니다. 포트를 지정 하지 않으면 게이트웨이 서비스는 포트 443 (HTTPS)에서 배포 됩니다. 사용 하려면이 매개 변수에서 다른 포트를 지정 합니다. Note (443 외에도 모든) 사용자 지정 포트를 사용 하는 경우 됩니다 액세스할 수 있는지 Windows Admin Center https://\<clientAccessPoint\>:\<port\>로 이동 합니다.

> [!NOTE]
> ```Install-WindowsAdminCenterHA.ps1``` 지원 스크립트 ```-WhatIf ``` 및 ```-Verbose``` 매개 변수

### 예

#### 서명 된 인증서를 사용 하 여 설치 합니다.

```powershell
$certPassword = Read-Host -AsSecureString
.\Install-WindowsAdminCenterHA.ps1 -clusterStorage "C:\ClusterStorage\Volume1" -clientAccessPoint "contoso-ha-gateway" -msiPath ".\WindowsAdminCenter.msi" -certPath "cert.pfx" -certPassword $certPassword -Verbose
```

#### 자체 서명 된 인증서를 사용 하 여 설치 합니다.

```powershell
.\Install-WindowsAdminCenterHA.ps1 -clusterStorage "C:\ClusterStorage\Volume1" -clientAccessPoint "contoso-ha-gateway" -msiPath ".\WindowsAdminCenter.msi" -generateSslCert -Verbose
```

## 기존 고가용성 설치를 업데이트

사용 ```Install-WindowsAdminCenterHA.ps1``` 연결 데이터 손실 없이 HA 배포, 업데이트 하는 스크립트입니다.

### Windows Admin Center의 새 버전으로 업데이트

새 버전의 Windows Admin Center를 놓을 때 실행 하기만 하면 됩니다 합니다 ```Install-WindowsAdminCenterHA.ps1``` 유일한으로 다시 스크립트는 ```msiPath``` 매개 변수:

```powershell
.\Install-WindowsAdminCenterHA.ps1 -msiPath '.\WindowsAdminCenter.msi' -Verbose
```

### Windows Admin Center에서 사용 되는 인증서 업데이트

새 인증서의.pfx 파일을 제공 하 여 언제 든 지 Windows Admin Center의 HA 배포에 사용 된 인증서를 업데이트할 수 및 및 암호입니다.

```powershell
$certPassword = Read-Host -AsSecureString
.\Install-WindowsAdminCenterHA.ps1 -certPath "cert.pfx" -certPassword $certPassword -Verbose
```

새.msi 파일로 Windows Admin Center 플랫폼을 업데이트 하는 동시에 인증서도 업데이트할 수 있습니다.

```powershell
$certPassword = Read-Host -AsSecureString
.\Install-WindowsAdminCenterHA.ps1 -msiPath ".\WindowsAdminCenter.msi" -certPath "cert.pfx" -certPassword $certPassword -Verbose
``` 

## 제거

장애 조치 클러스터에서 Windows Admin Center HA 배포를 제거 하려면 통과 ```-Uninstall``` 매개 변수를는 ```Install-WindowsAdminCenterHA.ps1``` 스크립트입니다.

```powershell
.\Install-WindowsAdminCenterHA.ps1 -Uninstall -Verbose
```

## 문제 해결

CSV (예를 들어 C:\ClusterStorage\Volume1\temp)의 임시 폴더에 저장 됩니다.