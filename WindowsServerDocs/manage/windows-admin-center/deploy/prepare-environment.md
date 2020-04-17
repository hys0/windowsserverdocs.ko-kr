---
title: Windows Admin Center에 대한 환경 준비
description: Windows Admin Center에 대한 환경 준비(Project Honolulu)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 06/07/2019
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 7a4dacd611741942e874e831fd9598aeda5e97b3
ms.sourcegitcommit: 20d07170c7f3094c2fb4455f54b13ec4b102f2d7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/13/2020
ms.locfileid: "81269280"
---
# <a name="prepare-your-environment-for-windows-admin-center"></a>Windows Admin Center에 대한 환경 준비

> 적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

Windows Admin Center를 사용하여 관리할 준비가 되기 전에 추가 준비를 해야 하는 일부 Server 버전이 있습니다.

- [Windows Server 2012 및 2012 R2](#prepare-windows-server-2012-and-2012-r2)
- [Microsoft Hyper-V Server 2016](#prepare-microsoft-hyper-v-server-2016)
- [Microsoft Hyper-V Server 2012 R2](#prepare-microsoft-hyper-v-server-2012-r2)

Windows Admin Center를 사용하여 관리하기 전에 [대상 서버에 대한 포트 구성](#port-configuration-on-the-target-server)을 수정해야 할 수도 있는 몇 가지 시나리오도 있습니다.

## <a name="prepare-windows-server-2012-and-2012-r2"></a>Windows Server 2012 및 2012 R2 준비

### <a name="install-wmf-version-51-or-higher"></a>WMF 버전 5.1 이상 설치

Windows Admin Center에는 기본적으로 Windows Server 2012 및 2012 R2에 포함되지 않은 PowerShell 기능이 필요합니다. Windows Admin Center로 Windows Server 2012 또는 2012 R2를 관리하려면 해당 서버에서 WMF 5.1 이상 버전을 설치해야 합니다.

WMF가 설치되어 있는지, 그리고 버전이 5.1 이상인지 확인하려면 PowerShell에 `$PSVersiontable`을 입력합니다.

설치되어있지 않은 경우 [WMF 5.1을 다운로드하여 설치](https://docs.microsoft.com/powershell/wmf/setup/install-configure)할 수 있습니다.

## <a name="prepare-microsoft-hyper-v-server-2016"></a>Microsoft Hyper-V Server 2016 준비

Windows Admin Center로 Microsoft Hyper-V Server 2016을 관리하려면 이를 수행하기 전에 활성화해야 하는 몇 가지 서버 역할이 있습니다.

### <a name="to-manage-microsoft-hyper-v-server-2016-with-windows-admin-center"></a>Microsoft Hyper-V Server 2016을 Windows Admin Center로 관리하려면:

1. 원격 관리를 사용하도록 설정합니다.
2. 파일 서버 역할을 사용하도록 설정합니다.
3. PowerShell용 Hyper-V 모듈을 사용하도록 설정합니다.

### <a name="step-1-enable-remote-management"></a>**1단계:** 원격 관리를 사용하도록 설정

Hyper-V Server에서 원격 관리를 사용하도록 설정하려면:

1. Hyper-V Server에 로그인합니다.
2. 원격 관리를 구성하려면 **서버 구성**(SCONFIG) 도구에서 **4**를 입력합니다.
3. 원격 관리를 사용하도록 설정하려면 **1**을 입력합니다.
4. 주 메뉴로 돌아가려면 **4**를 입력합니다.

### <a name="step-2-enable-file-server-role"></a>**2단계:** 파일 서버 역할을 사용하도록 설정

기본 파일 공유 및 원격 관리에 대해 파일 서버 역할을 사용하도록 설정하려면:

1. **도구** 메뉴에서 **역할 및 기능**을 클릭합니다.
2. **역할 및 기능**에서 **파일 및 스토리지 서비스**를 찾아 **파일 및 iSCSI 서비스** 및 **파일 서버**를 확인합니다.

![선택한 파일 및 iSCSI 서비스 역할을 보여 주는 역할 및 기능의 스크린샷](../media/prepare-environment/c6c30b812d96afcc1edcdb6f52f0e13c.png)

### <a name="step-3-enable-hyper-v-module-for-powershell"></a>**3단계:** PowerShell용 Hyper-V 모듈을 사용하도록 설정

PowerShell 기능용 Hyper-V 모듈을 사용하도록 설정하려면:

1. **도구** 메뉴에서 **역할 및 기능**을 클릭합니다.
2. **역할 및 기능**에서 **원격 서버 관리 도구**를 찾아 **역할 관리 도구** 및 **PowerShell용 Hyper-V 모듈**을 확인합니다.

![선택된 Hyper-V 역할을 보여 주는 역할 및 기능의 스크린샷](../media/prepare-environment/7ab0999602b7083733525bd0c1ba2747.png)

Microsoft Hyper-V Server 2016은 이제 Windows Admin Center로 관리할 수 있는 준비가 되었습니다.

## <a name="prepare-microsoft-hyper-v-server-2012-r2"></a>Microsoft Hyper-V Server 2012 R2 준비

Windows Admin Center로 Microsoft Hyper-V Server 2012 R2를 관리하려면 이를 수행하기 전에 활성화해야 하는 몇 가지 서버 역할이 있습니다.  또한 WMF 5.1 이상 버전을 설치해야 합니다.

### <a name="to-manage-microsoft-hyper-v-server-2012-r2-with-windows-admin-center"></a>Microsoft Hyper-V Server 2012 R2를 Windows Admin Center로 관리하려면:

1. WMF(Windows Management Framework) 5.1 이상 버전 설치
2. 원격 관리를 사용하도록 설정
3. 파일 서버 역할을 사용하도록 설정
4. PowerShell용 Hyper-V 모듈을 사용하도록 설정

### <a name="step-1-install-windows-management-framework-51"></a>1단계: Windows Management Framework 5.1 설치

Windows Admin Center에는 기본적으로 Microsoft Hyper-V Server 2012 R2에 포함되지 않은 PowerShell 기능이 필요합니다. Windows Admin Center로 Microsoft Hyper-V Server 2012 R2를 관리하려면 WMF 버전 5.1 이상을 설치해야 합니다.

WMF가 설치되어 있는지, 그리고 버전이 5.1 이상인지 확인하려면 PowerShell에 `$PSVersiontable`을 입력합니다. 

설치가 되어 있지 않는 경우에 [WMF 5.1을 다운로드](https://docs.microsoft.com/powershell/wmf/setup/install-configure)할 수 있습니다.

### <a name="step-2-enable-remote-management"></a>2단계: 원격 관리를 사용하도록 설정

Hyper-V Server 원격 관리를 사용하도록 설정하려면:

1. Hyper-V Server에 로그인합니다.
2. 원격 관리를 구성하려면 **서버 구성**(SCONFIG) 도구에서 **4**를 입력합니다.
3. 원격 관리를 사용하도록 설정하려면 **1**을 입력합니다.
4. 주 메뉴로 돌아가려면 **4**를 입력합니다.

### <a name="step-3-enable-file-server-role"></a>3단계: 파일 서버 역할을 사용하도록 설정

기본 파일 공유 및 원격 관리에 대해 파일 서버 역할을 사용하도록 설정하려면:

1. **도구** 메뉴에서 **역할 및 기능**을 클릭합니다.
2. **역할 및 기능**에서 **파일 및 스토리지 서비스**를 찾아 **파일 및 iSCSI 서비스** 및 **파일 서버**를 확인합니다.

![선택한 파일 및 iSCSI 서비스 역할을 보여 주는 역할 및 기능의 스크린샷](../media/prepare-environment/c6c30b812d96afcc1edcdb6f52f0e13c.png)

### <a name="step-4-enable-hyper-v-module-for-powershell"></a>4단계: PowerShell용 Hyper-V 모듈을 사용하도록 설정

PowerShell 기능용 Hyper-V 모듈을 사용하도록 설정하려면:

1. **도구** 메뉴에서 **역할 및 기능**을 클릭합니다.
2. **역할 및 기능**에서 **원격 서버 관리 도구**를 찾아 **역할 관리 도구** 및 **PowerShell용 Hyper-V 모듈**을 확인합니다.

![선택된 Hyper-V 원격 서버 관리 도구를 보여 주는 역할 및 기능의 스크린샷](../media/prepare-environment/7ab0999602b7083733525bd0c1ba2747.png)

Microsoft Hyper-V Server 2012 R2은 이제 Windows Admin Center로 관리할 수 있는 준비가 되었습니다.

## <a name="port-configuration-on-the-target-server"></a>대상 서버의 포트 구성

Windows Admin Center는 원격 서버에서 인증서를 가져오는 경우와 같은 일부 파일 복사 작업에 SMB 파일 공유 프로토콜을 사용합니다. 이러한 파일 복사 작업이 성공하려면 원격 서버의 방화벽이 포트 445에서 인바운드 연결을 허용해야 합니다.  Windows Admin Center의 방화벽 도구를 사용하여 '파일 서버 원격 관리(SMB-In)'에 대한 들어오는 규칙이 이 포트에 대한 액세스를 허용하도록 설정되었는지 확인할 수 있습니다.

> [!Tip]
> Windows Admin Center를 설치할 준비가 되셨습니까? [지금 다운로드](https://docs.microsoft.com/windows-server/manage/windows-admin-center/understand/windows-admin-center#download-now)
