---
title: Windows Admin Center에 대한 환경 준비
description: Windows Admin Center에 대한 환경 준비(Project Honolulu)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/19/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 598eeae64925d24ec6d97b59da9cae1e2d10585d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59864974"
---
# <a name="prepare-your-environment-for-windows-admin-center"></a>Windows Admin Center에 대한 환경 준비

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

Windows Admin Center를 사용하여 관리할 준비가 되기 전에 추가 준비를 해야 하는 일부 Server 버전이 있습니다.

- [Windows Server 2012 and 2012 R2](#prepare-windows-server-2012-and-2012-r2)
- [Windows Server 2008 R2](#prepare-windows-server-2008-r2)
- [Microsoft Hyper-V Server 2016](#prepare-microsoft-hyper-v-server-2016)
- [Microsoft Hyper-V Server 2012 R2](#prepare-microsoft-hyper-v-server-2012-r2)

## <a name="prepare-windows-server-2012-and-2012-r2"></a>Windows Server 2012 및 2012 R2 준비

### <a name="install-wmf-version-51-or-higher"></a>WMF 버전 5.1 이상 설치

Windows Admin Center에는 기본적으로 Windows Server 2012 및 2012 R2에 포함되지 않은 PowerShell 기능이 필요합니다. Windows Admin Center로 Windows Server 2012 또는 2012 R2를 관리하려면 해당 서버에서 WMF 5.1 이상 버전을 설치해야 합니다.

WMF가 설치되어 있는지, 그리고 버전이 5.1 이상인지 확인하려면 PowerShell에 `$PSVersiontable`을 입력합니다.

설치되어있지 않은 경우 [WMF 5.1을 다운로드하여 설치할](https://docs.microsoft.com/powershell/wmf/5.1/install-configure)수 있습니다.

## <a name="prepare-windows-server-2008-r2"></a>Windows Server 2008 R2 준비

### <a name="install-wmf-version-51-or-higher"></a>WMF 버전 5.1 이상 설치

Windows Admin Center에는 기본적으로 Windows Server 2008 R2에 포함되지 않은 PowerShell 기능이 필요합니다. Windows Admin Center로 Windows Server 2008 R2를 관리하려면 해당 서버에서 WMF 5.1 이상 버전을 설치해야 합니다. 

했는지 [.NET Framework 4.5.2 이상](https://docs.microsoft.com/dotnet/framework/install/on-windows-7) 컴퓨터에 이미 설치 되어 있습니다.

WMF가 설치되어 있는지, 그리고 버전이 5.1 이상인지 확인하려면 PowerShell에 `$PSVersiontable`을 입력합니다.

설치되어있지 않은 경우 [WMF 5.1을 다운로드하여 설치할](https://docs.microsoft.com/powershell/wmf/5.1/install-configure)수 있습니다.

PowerShell 원격 연결을 사용하도록 설정하려면 PowerShell 콘솔에서 `Enable-PSRemoting –force`를 실행합니다. 

### <a name="enable-remote-desktop"></a>원격 데스크톱을 사용하도록 설정

Windows Admin Center 내에서 원격 데스크톱을 사용하려면 Windows Server 2008 R2 서버에서 원격 데스크톱을 사용하도록 설정해야 합니다.

**서버 관리자**에서 **원격 데스크톱 구성**으로 이동합니다. "모든 버전의 원격 데스크톱을 실행 중인 컴퓨터에서 연결 허용"을 위해 원격 데스크톱을 사용하도록 설정합니다.

## <a name="prepare-microsoft-hyper-v-server-2016"></a>Microsoft Hyper-V Server 2016 준비

Windows Admin Center로 Microsoft Hyper-V Server 2016을 관리하려면 이를 수행하기 전에 활성화해야 하는 몇 가지 서버 역할이 있습니다.

### <a name="to-manage-microsoft-hyper-v-server-2016-with-windows-admin-center"></a>Microsoft Hyper-V Server 2016을 Windows Admin Center로 관리하는 방법:

1. 원격 관리를 사용하도록 설정합니다.
2. 파일 서버 역할을 사용하도록 설정합니다.
3. PowerShell용 Hyper-V 모듈을 사용하도록 설정합니다.

### <a name="step-1-enable-remote-management"></a>**1 단계:** 원격 관리를 사용하도록 설정

Hyper-V Server에서 원격 관리를 활성화하는 방법:

1. Hyper-V Server에 로그인합니다.
2. 원격 관리를 구성하려면 **서버 구성**(SCONFIG) 도구에서 **4**를 입력합니다.
3. 원격 관리를 사용하도록 설정하려면 **1**을 입력합니다.
4. 주 메뉴로 돌아가려면 **4**를 입력합니다.

### <a name="step-2-enable-file-server-role"></a>**2 단계:** 파일 서버 역할을 사용하도록 설정

기본 파일 공유 및 원격 관리에 대해 파일 서버 역할을 사용하도록 설정하려면:

1. **도구** 메뉴에서 **역할 및 기능**을 클릭합니다.
2. **역할 및 기능**에서 **파일 및 저장소 서비스**를 찾아 **파일 및 iSCSI 서비스** 및 **파일 서버**를 확인합니다.

![](../media/prepare-environment/c6c30b812d96afcc1edcdb6f52f0e13c.png)

### <a name="step-3-enable-hyper-v-module-for-powershell"></a>**3 단계:** PowerShell용 Hyper-V 모듈을 사용하도록 설정

PowerShell 기능용 Hyper-V 모듈을 사용하도록 설정하는 방법:

1. **도구** 메뉴에서 **역할 및 기능**을 클릭합니다.
2. **역할 및 기능**에서 **원격 서버 관리 도구**를 찾아 **역할 관리 도구** 및 **PowerShell용 Hyper-V 모듈**을 확인합니다.

![](../media/prepare-environment/7ab0999602b7083733525bd0c1ba2747.png)

Microsoft Hyper-V Server 2016은 이제 Windows Admin Center로 관리할 수 있는 준비가 되었습니다.

## <a name="prepare-microsoft-hyper-v-server-2012-r2"></a>Microsoft Hyper-V Server 2012 R2 준비

Windows Admin Center로 Microsoft Hyper-V Server 2012 R2를 관리하려면 이를 수행하기 전에 활성화해야 하는 몇 가지 서버 역할이 있습니다.  또한 WMF 5.1 이상 버전을 설치해야 합니다.

### <a name="to-manage-microsoft-hyper-v-server-2012-r2-with-windows-admin-center"></a>Microsoft Hyper-V Server 2012 R2를 Windows Admin Center로 관리하는 방법:

1. WMF(Windows Management Framework) 5.1 이상 버전 설치
2. 원격 관리를 사용하도록 설정
3. 파일 서버 역할을 사용하도록 설정
4. PowerShell용 Hyper-V 모듈을 사용하도록 설정

### <a name="step-1-install-windows-management-framework-51"></a>**1 단계:** Windows Management Framework 5.1 설치

Windows Admin Center에는 기본적으로 Microsoft Hyper-V Server 2012 R2에 포함되지 않은 PowerShell 기능이 필요합니다. Windows Admin Center로 Microsoft Hyper-V Server 2012 R2를 관리하려면 WMF 버전 5.1 이상을 설치해야 합니다.

WMF가 설치되어 있는지, 그리고 버전이 5.1 이상인지 확인하려면 PowerShell에 `$PSVersiontable`을 입력합니다. 

설치가 되어 있지 않는 경우에 [WMF 5.1을 다운로드](https://docs.microsoft.com/powershell/wmf/5.1/install-configure)할 수 있습니다.

### <a name="step-2-enable-remote-management"></a>**2 단계:** 원격 관리를 사용하도록 설정 

Hyper-V Server 원격 관리를 활성화하는 방법:

1. Hyper-V Server에 로그인합니다.
2. 원격 관리를 구성하려면 **서버 구성**(SCONFIG) 도구에서 **4**를 입력합니다.
3. 원격 관리를 사용하도록 설정하려면 **1**을 입력합니다.
4. 주 메뉴로 돌아가려면 **4**를 입력합니다.

### <a name="step-3-enable-file-server-role"></a>3단계: 파일 서버 역할을 사용하도록 설정

기본 파일 공유 및 원격 관리에 대해 파일 서버 역할을 사용하도록 설정하려면:

1. **도구** 메뉴에서 **역할 및 기능**을 클릭합니다.
2. **역할 및 기능**에서 **파일 및 저장소 서비스**를 찾아 **파일 및 iSCSI 서비스** 및 **파일 서버**를 확인합니다.

![](../media/prepare-environment/c6c30b812d96afcc1edcdb6f52f0e13c.png)

### <a name="step-4-enable-hyper-v-module-for-powershell"></a>4단계: PowerShell용 Hyper-V 모듈을 사용하도록 설정 ##

PowerShell 기능용 Hyper-V 모듈을 사용하도록 설정하는 방법:

1. **도구** 메뉴에서 **역할 및 기능**을 클릭합니다.
2. **역할 및 기능**에서 **원격 서버 관리 도구**를 찾아 **역할 관리 도구** 및 **PowerShell용 Hyper-V 모듈**을 확인합니다.

![](../media/prepare-environment/7ab0999602b7083733525bd0c1ba2747.png)

Microsoft Hyper-V Server 2012 R2은 이제 Windows Admin Center로 관리할 수 있는 준비가 되었습니다.

> [!Tip]
> Windows Admin Center를 설치할 준비가 되셨습니까? [지금 다운로드](https://docs.microsoft.com/windows-server/manage/windows-admin-center/understand/windows-admin-center#download-now)