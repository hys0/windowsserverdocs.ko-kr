---
title: Hyper-v 호스트 원격 관리
description: Hyper-v 호스트와 Hyper-v 관리자 간의 버전 호환성과 도메인 간 및 독립 실행형을 비롯 한 다양 한 환경에서 원격 호스트에 연결 하는 방법을 설명 합니다.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.topic: article
ms.assetid: 2d34e98c-6134-479b-8000-3eb360b8b8a3
author: kbdazure
ms.author: kathydav
ms.date: 12/06/2016
ms.openlocfilehash: bbd96e35cbab94f3e10a4f62f785db7724308a0f
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85471108"
---
# <a name="remotely-manage-hyper-v-hosts-with-hyper-v-manager"></a>Hyper-V 관리자를 사용하여 원격으로 Hyper-V 호스트 관리

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows 10, Windows 8.1

이 문서에서는 Hyper-v 호스트와 Hyper-v 관리자 버전의 지원 되는 조합을 나열 하 고 원격 및 로컬 Hyper-v 호스트에 연결 하 여 관리할 수 있도록 하는 방법을 설명 합니다.

Hyper-v 관리자를 사용 하면 몇 가지 Hyper-v 호스트 (원격 및 로컬)를 관리할 수 있습니다. Hyper-v 관리 도구를 설치할 때 설치 됩니다 .이 도구는 전체 Hyper-v 설치 또는 도구 전용 설치를 통해 수행할 수 있습니다. 도구 전용 설치를 사용 하는 경우 Hyper-v를 호스팅하기 위한 하드웨어 요구 사항을 충족 하지 않는 컴퓨터의 도구를 사용할 수 있습니다. Hyper-v 호스트의 하드웨어에 대 한 자세한 내용은 [시스템 요구 사항](../System-requirements-for-Hyper-V-on-Windows.md)을 참조 하세요.

Hyper-v 관리자가 설치 되지 않은 경우 아래 [지침](#install-hyper-v-manager) 을 참조 하세요.

## <a name="supported-combinations-of-hyper-v-manager-and-hyper-v-host-versions"></a>Hyper-v 관리자 및 Hyper-v 호스트 버전의 지원 되는 조합

테이블에 표시 된 것 처럼 호스트의 Hyper-v 버전과 다른 버전의 Hyper-v 관리자를 사용할 수 있는 경우도 있습니다. 이 작업을 수행 하는 경우 Hyper-v 관리자는 관리 중인 호스트의 Hyper-v 버전에 사용할 수 있는 기능을 제공 합니다. 예를 들어 windows server 2012 r 2에서 hyper-v 관리자의 버전을 사용 하 여 Windows Server 2012에서 Hyper-v를 실행 하는 호스트를 원격으로 관리 하는 경우 해당 Hyper-v 호스트에서 Windows Server 2012 r 2에 제공 되는 기능을 사용할 수 없습니다.

다음 표에서는 특정 버전의 Hyper-v 관리자에서 관리할 수 있는 Hyper-v 호스트의 버전을 보여 줍니다. 지원 되는 운영 체제 버전만 나열 됩니다. 특정 운영 체제 버전의 지원 상태에 대 한 자세한 내용을 보려면 [Microsoft 수명 주기 정책](https://support.microsoft.com/lifecycle) 페이지에서 **product 수명 주기 검색** 단추를 사용 합니다. 일반적으로 이전 버전의 Hyper-v 관리자는 동일한 버전 또는 호환 되는 Windows Server 버전을 실행 하는 Hyper-v 호스트만 관리할 수 있습니다.

|Hyper-v 관리자 버전 | Hyper-v 호스트 버전|
|---|---|
|Windows 2016, Windows 10|-Windows Server 2016-모든 버전 및 설치 옵션 (Nano 서버 포함) 및 해당 하는 버전의 Hyper-v 서버 <br>-Windows Server 2012 R2-모든 버전 및 설치 옵션 및 해당 하는 버전의 Hyper-v 서버 <br>-Windows Server 2012-모든 버전 및 설치 옵션 및 해당 하는 버전의 Hyper-v 서버 <br> - Windows 10 <br> - Windows 8.1  |
| Windows Server 2012 R2, Windows 8.1 | -Windows Server 2012 R2-모든 버전 및 설치 옵션 및 해당 하는 버전의 Hyper-v 서버 <br>-Windows Server 2012-모든 버전 및 설치 옵션 및 해당 하는 버전의 Hyper-v 서버 <br>- Windows 8.1
| Windows Server 2012 | -Windows Server 2012-모든 버전 및 설치 옵션 및 해당 하는 버전의 Hyper-v 서버
| Windows Server 2008 R2 서비스 팩 1, Windows 7 서비스 팩 1 | -Windows Server 2008 R2-모든 버전 및 설치 옵션 및 해당 하는 버전의 Hyper-v 서버
| Windows Server 2008, Windows Vista 서비스 팩 2 | -Windows Server 2008-모든 버전 및 설치 옵션 및 해당 하는 버전의 Hyper-v 서버

>[!NOTE]
>2016 년 1 월 12 일에 Windows 8에 대 한 서비스 팩 지원이 종료 되었습니다. 자세한 내용은 [WINDOWS 8.1 FAQ](https://support.microsoft.com/help/18581)를 참조 하십시오.

## <a name="connect-to-a-hyper-v-host"></a>Hyper-v 호스트에 연결

Hyper-v 관리자에서 hyper-v 호스트에 연결 하려면 왼쪽 창에서 **Hyper-v 관리자** 를 마우스 오른쪽 단추로 클릭 한 다음 **서버에 연결**을 클릭 합니다.

## <a name="manage-hyper-v-on-a-local-computer"></a>로컬 컴퓨터의 Hyper-v 관리

Hyper-v 관리자는 로컬 컴퓨터를 포함 하 여 컴퓨터를 추가할 때까지 Hyper-v를 호스트 하는 컴퓨터를 나열 하지 않습니다. 다음을 수행합니다.

1. 왼쪽 창에서 **Hyper-v 관리자**를 마우스 오른쪽 단추로 클릭 합니다.
2. **서버에 연결을**클릭 합니다.
3. **컴퓨터 선택**에서 **로컬 컴퓨터** 를 클릭 한 다음 **확인**을 클릭 합니다.

연결할 수 없는 경우:

* Hyper-v 도구만 설치 되어 있을 수 있습니다. Hyper-v 플랫폼이 설치 되어 있는지 확인 하려면 가상 컴퓨터 관리 서비스를 찾습니다. /(서비스 데스크톱 앱 열기: **시작**, **검색 시작** 상자를 차례로 클릭 하 고 **Services.msc**를 입력 한 다음 **enter**키를 누릅니다. 가상 컴퓨터 관리 서비스가 나열 되지 않은 경우 hyper-v [설치](../get-started/Install-the-Hyper-V-role-on-Windows-Server.md)의 지침에 따라 hyper-v 플랫폼을 설치 합니다.
* 하드웨어가 요구 사항을 충족 하는지 확인 합니다. [시스템 요구 사항](../System-requirements-for-Hyper-V-on-Windows.md)을 참조 하세요.
* 사용자 계정이 Administrators 그룹이 나 Hyper-v Administrators 그룹에 속해 있는지 확인 합니다.

## <a name="manage-hyper-v-hosts-remotely"></a>원격으로 Hyper-v 호스트 관리

원격 Hyper-v 호스트를 관리 하려면 로컬 컴퓨터와 원격 호스트에서 원격 관리를 사용 하도록 설정 합니다.

Windows server에서 서버 관리자 \> **로컬 서버** \> **원격 관리** 를 열고 **이 컴퓨터에 원격 연결 허용**을 클릭 합니다.

또는 두 운영 체제에서 관리자 권한으로 Windows PowerShell을 열고 다음을 실행 합니다.

```
Enable-PSRemoting
```

### <a name="connect-to-hosts-in-the-same-domain"></a>동일한 도메인의 호스트에 연결

Windows 8.1 및 이전 버전의 경우 원격 관리는 호스트가 동일한 도메인에 있고 로컬 사용자 계정도 원격 호스트에 있는 경우에만 작동 합니다.

Hyper-v 관리자에 원격 Hyper-v 호스트를 추가 하려면 **컴퓨터 선택** 대화 상자에서 **다른 컴퓨터** 를 선택 하 고 원격 호스트의 호스트 이름, NetBIOS 이름 또는 fqdn (정규화 된 도메인 이름)을 입력 합니다 \( \) .

Windows Server 2016 및 Windows 10의 hyper-v 관리자는 다음 섹션에 설명 된 것 처럼 이전 버전 보다 더 많은 유형의 원격 연결을 제공 합니다.

### <a name="connect-to-a-windows-2016-or-windows-10-remote-host-as-a-different-user"></a>다른 사용자로 Windows 2016 또는 Windows 10 원격 호스트에 연결

이를 통해 hyper-v 호스트에서 hyper-v 관리자 그룹 또는 Administrators 그룹의 구성원 인 사용자로 로컬 컴퓨터에서 실행 되 고 있지 않은 경우 Hyper-v 호스트에 연결할 수 있습니다. 다음을 수행합니다.

1. 왼쪽 창에서 **Hyper-v 관리자**를 마우스 오른쪽 단추로 클릭 합니다.
1. **서버에 연결을**클릭 합니다.
1. **컴퓨터 선택** 대화 상자에서 **다른 사용자로 연결을** 선택 합니다.
1. **사용자 설정**을 선택 합니다.

>[!NOTE]
> 이는 Windows Server 2016 또는 Windows 10 **원격** 호스트에만 적용 됩니다.

### <a name="connect-to-a-windows-2016-or-windows-10-remote-host-using-ip-address"></a>IP 주소를 사용 하 여 Windows 2016 또는 Windows 10 원격 호스트에 연결

다음을 수행합니다.

1. 왼쪽 창에서 **Hyper-v 관리자**를 마우스 오른쪽 단추로 클릭 합니다.
1. **서버에 연결을**클릭 합니다.
1. **다른 컴퓨터** 텍스트 필드에 IP 주소를 입력 합니다.

>[!NOTE]
> 이는 Windows Server 2016 또는 Windows 10 **원격** 호스트에만 적용 됩니다.

### <a name="connect-to-a-windows-2016-or-windows-10-remote-host-outside-your-domain-or-with-no-domain"></a>도메인 외부 또는 도메인 외부의 Windows 2016 또는 Windows 10 원격 호스트에 연결

다음을 수행합니다.

1. 관리할 Hyper-v 호스트에서 관리자 권한으로 Windows PowerShell 세션을 엽니다.

1. 개인 네트워크 영역에 대해 필요한 방화벽 규칙을 만듭니다.

   ```
   Enable-PSRemoting
   ```

2. 공용 영역에 대 한 원격 액세스를 허용 하려면 CredSSP 및 WinRM에 대 한 방화벽 규칙을 사용 하도록 설정 합니다.

   ```
   Enable-WSManCredSSP -Role server
   ```

    자세한 내용은 [enable-psremoting](https://technet.microsoft.com/library/hh849694.aspx) 및 [enable-wsmancredssp](https://technet.microsoft.com/library/hh849872.aspx)를 참조 하세요.

그런 다음 Hyper-v 호스트를 관리 하는 데 사용할 컴퓨터를 구성 합니다.

1. 관리자 권한으로 Windows PowerShell 세션을 엽니다.
1. 다음 명령을 실행합니다.

     ```
     Set-Item WSMan:\localhost\Client\TrustedHosts -Value "fqdn-of-hyper-v-host"
     ```
     ```
     Enable-WSManCredSSP -Role client -DelegateComputer "fqdn-of-hyper-v-host"
     ```
1. 다음 그룹 정책을 구성 해야 할 수도 있습니다.
    * **컴퓨터 구성** \> **관리 템플릿** \> **시스템** \> **자격 증명 위임** \> **NTLM 전용 서버 인증을 사용 하 여 새 자격 증명 위임 허용**
    * **사용** 을 클릭 하 고 *wsman/hyper-v-호스트*를 추가 합니다.
1. **Hyper-v 관리자**를 엽니다.
1. 왼쪽 창에서 **Hyper-v 관리자**를 마우스 오른쪽 단추로 클릭 합니다.
1. **서버에 연결을**클릭 합니다.

>[!NOTE]
> 이는 Windows Server 2016 또는 Windows 10 **원격** 호스트에만 적용 됩니다.

Cmdlet에 대 한 자세한 내용은 [enable-wsmancredssp 및 Enable-](https://technet.microsoft.com/library/hh849872.aspx)를 [참조 하세요.](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.management/set-item)

## <a name="install-hyper-v-manager"></a>Hyper-v 관리자 설치

UI 도구를 사용 하려면 Hyper-v 관리자를 실행 하는 컴퓨터의 운영 체제에 적합 한 도구를 선택 합니다.

Windows Server에서 \> **Manage** \> **역할 및 기능 추가**서버 관리자 관리를 엽니다. **기능** 페이지로 이동 하 여 **원격 서버 관리 도구** \> **역할 관리 도구** \> **hyper-v 관리 도구**를 확장 합니다.

Windows에서 hyper-v 관리자는 [hyper-v가 포함 된 모든 Windows 운영 체제](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_compatibility)에서 사용할 수 있습니다.

1. Windows 바탕 화면에서 시작 단추를 클릭 하 고 **프로그램 및 기능**을 입력 하기 시작 합니다.
1. 검색 결과에서 **프로그램 및 기능**을 클릭 합니다.
1. 왼쪽 창에서 **Windows 기능 사용/사용 안 함**을 클릭 합니다.
1. Hyper-v 폴더를 확장 하 고 **Hyper-v 관리 도구를 클릭**합니다.
1. Hyper-v 관리자를 설치 하려면 **Hyper-v 관리 도구**를 클릭 합니다. Hyper-v 모듈을 설치 하려는 경우 해당 옵션을 클릭 합니다.

Windows PowerShell을 사용 하려면 관리자 권한으로 다음 명령을 실행 합니다.

```
add-windowsfeature rsat-hyper-v-tools
```

## <a name="additional-references"></a>추가 참조

[Hyper-V 설치](../get-started/Install-the-Hyper-V-role-on-Windows-Server.md)

