---
title: 원격 Hyper-v 호스트 관리
description: Hyper-v 호스트 및 Hyper-v 관리자 및 도메인 간 및 독립 실행형을 비롯 한 다양 한 환경에서 원격 호스트에 연결 하는 방법 간에 버전 호환성을 설명 합니다.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2d34e98c-6134-479b-8000-3eb360b8b8a3
author: KBDAzure
ms.author: kathydav
ms.date: 12/06/2016
ms.openlocfilehash: df66f308ee7999f97fe7e57a8b52256f2561faa2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59870234"
---
# <a name="remotely-manage-hyper-v-hosts-with-hyper-v-manager"></a>Hyper-v 관리자를 사용 하 여 Hyper-v 호스트를 원격으로 관리

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows 10, Windows 8.1

이 문서는 Hyper-v 호스트 및 Hyper-v Manager 버전의 지원 되는 조합을 나열 하 고 관리할 수 있도록 원격 및 로컬 Hyper-v 호스트에 연결 하는 방법에 설명 합니다. 

Hyper-v 관리자를 사용 하면 소수의 원격 및 로컬 Hyper-v 호스트를 관리할 수 있습니다. 수행할 수 있는 Hyper-v 관리 도구를 설치할 때 설치 된 전체 통해 Hyper-v 설치 또는 도구만 설치 합니다. 도구 전용 설치 방법을 수행 Hyper-v 호스트의 하드웨어 요구 사항을 충족 하지 않는 컴퓨터에서 도구를 사용할 수 있습니다. Hyper-v 호스트에 대 한 하드웨어에 대 한 자세한 내용은 참조 하세요 [시스템 요구 사항](..\System-requirements-for-Hyper-V-on-Windows.md)합니다.

Hyper-v 관리자 설치 되지 않은 경우 참조를 [지침](#install-hyper-v-manager) 아래.

## <a name="supported-combinations-of-hyper-v-manager-and-hyper-v-host-versions"></a>Hyper-v 관리자 및 Hyper-v 호스트 버전의 지원 되는 조합

일부 경우 테이블에 표시 된 대로 Hyper-v 버전과 다른 버전의 Hyper-v 관리자 호스트에서 사용할 수 있습니다. 이 작업을 수행 하는 경우 Hyper-v 관리자를 관리 하는 호스트에서 Hyper-v의 버전에 대 한 사용 가능한 기능을 제공 합니다. 예를 들어, Windows Server 2012의 Hyper-v를 실행 하는 호스트를 관리할 수 있는 Windows Server 2012 R2에서 Hyper-v 관리자의 버전을 사용 하는 경우 해당 Hyper-v 호스트에서 Windows Server 2012 R2에서 사용할 수 있는 기능을 사용 하는 일을 할 수 없습니다.

다음 표에서 버전의 Hyper-v 호스트-Hyper-v 관리자의 특정 버전에서 관리할 수 있습니다. 버전이 나열 되어 운영 체제 에서만 지원 됩니다. 특정 운영 체제 버전의 지원 상태에 대 한 세부 정보를 사용 합니다 **검색 제품 수명 주기** 단추를 [Microsoft 수명 주기 정책](https://support.microsoft.com/lifecycle) 페이지. 일반적으로 이전 버전의 Hyper-v 관리자의 같은 버전이 나 비교 가능한 Windows Server 버전을 실행 하는 Hyper-v 호스트에만 관리할 수 있습니다.

|Hyper-v 관리자 버전 | Hyper-v 호스트 버전|
|---|---|
|Windows 2016, Windows 10|Windows Server 2016-모든 버전 및 설치 옵션, Nano 서버 및 해당 버전의 Hyper-v Server <br>Windows Server 2012 R2-모든 버전 및 설치 옵션 및 해당 버전의 Hyper-v Server <br>Windows Server 2012-모든 버전 및 설치 옵션 및 해당 버전의 Hyper-v Server <br> - Windows 10 <br> - Windows 8.1  |
| Windows Server 2012 R2, Windows 8.1 | Windows Server 2012 R2-모든 버전 및 설치 옵션 및 해당 버전의 Hyper-v Server <br>Windows Server 2012-모든 버전 및 설치 옵션 및 해당 버전의 Hyper-v Server <br>- Windows 8.1
| Windows Server 2012 | Windows Server 2012-모든 버전 및 설치 옵션 및 해당 버전의 Hyper-v Server
| Windows Server 2008 R2 서비스 팩 1, Windows 7 서비스 팩 1 | Windows Server 2008 R2-모든 버전 및 설치 옵션 및 해당 버전의 Hyper-v Server
| Windows Server 2008, Windows Vista 서비스 팩 2 | Windows Server 2008-모든 버전 및 설치 옵션 및 해당 버전의 Hyper-v Server

>[!NOTE]
>서비스 팩 지원 Windows 8 용 2016 년 1 월 12 일에 종료 됩니다. 자세한 내용은 참조는 [Windows 8.1 FAQ](https://support.microsoft.com/help/18581)합니다.

## <a name="connect-to-a-hyper-v-host"></a>Hyper-v 호스트에 연결

Hyper-v 관리자에서 Hyper-v 호스트에 연결을 마우스 오른쪽 단추로 클릭 **Hyper-v 관리자** 클릭 한 다음 확인 하 고 왼쪽된 창에서 **서버에 연결**합니다.

## <a name="manage-hyper-v-on-a-local-computer"></a>로컬 컴퓨터에서 Hyper-v 관리

Hyper-v 관리자는 로컬 컴퓨터를 포함 하 여 컴퓨터를 추가 하기 전에 Hyper-v를 호스트 하는 모든 컴퓨터 표시 되지 않습니다. 가상 하드 디스크 파일에 대한 중요 정보를 제공하려면

1. 왼쪽된 창에서 마우스 오른쪽 단추로 클릭 **Hyper-v 관리자**합니다.
2. 클릭 **서버에 연결할**합니다.
3. **컴퓨터 선택**, 클릭 **로컬 컴퓨터** 을 클릭 한 다음 **확인**합니다.

연결할 수 없으면:

* Hyper-v 도구만 설치 된 것 같습니다. Hyper-v 플랫폼이 설치 되어 있는지를 확인 하려면 가상 컴퓨터 관리 서비스를 찾아봅니다. \(서비스 데스크톱 응용 프로그램을 엽니다: 클릭 **시작**를 클릭 합니다 **검색 시작** 상자에 입력 **services.msc**, 누릅니다 **Enter**합니다. 가상 머신 관리 서비스가 나열 되지 않은 경우의 지침에 따라 Hyper-v 플랫폼을 설치 [Hyper-v 설치](..\get-started\Install-the-Hyper-V-role-on-Windows-Server.md)합니다.\)
* 하드웨어 요구 사항을 충족 하는지 확인 합니다. 참조 [시스템 요구 사항](..\System-requirements-for-Hyper-V-on-Windows.md)합니다.
* 사용자 계정이 Administrators 그룹 또는 Hyper-v Administrators 그룹에 속해 있는지 확인 합니다.

## <a name="manage-hyper-v-hosts-remotely"></a>원격 Hyper-v 호스트 관리  

원격 Hyper-v 호스트를 관리 하려면 로컬 컴퓨터와 원격 호스트에서 원격 관리를 사용 하도록 설정 합니다.

Windows Server에서 서버 관리자를 엽니다 \> **로컬 서버** \> **Remote management** 클릭 하 고 **가이컴퓨터에원격연결허용**. 

또는 운영 체제 중 하나에서 Windows PowerShell 관리자 권한으로 열고 실행 합니다. 

```
Enable-PSRemoting
```

### <a name="connect-to-hosts-in-the-same-domain"></a>동일한 도메인의 호스트에 연결

Windows 8.1 및 이전 버전에서 원격 관리 호스트가 동일한 도메인에 로컬 사용자 계정이 원격 호스트에서 또한 경우에 작동 합니다.

원격 Hyper-v 호스트-Hyper-v 관리자를 추가 하려면 **다른 컴퓨터** 에 **컴퓨터 선택** 대화 상자 및 원격 호스트의 호스트 이름, NetBIOS 이름 또는 정규화 된 도메인 이름 입력\(FQDN\)합니다.

Windows Server 2016 및 Windows 10에서 Hyper-v 관리자는 다음 섹션에 설명 된 이전 버전 보다 더 다양 한 유형의 원격 연결을 제공 합니다.  

### <a name="connect-to-a-windows-2016-or-windows-10-remote-host-as-a-different-user"></a>다른 사용자로 Windows 2016 또는 Windows 10 원격 호스트에 연결

이렇게 하면 Hyper-v Administrators 그룹 또는 Hyper-v 호스트에서 Administrators 그룹의 구성원 인 사용자로 로컬 컴퓨터에서 실행 되지 하는 경우 Hyper-v 호스트에 연결할 수 있습니다. 가상 하드 디스크 파일에 대한 중요 정보를 제공하려면

1. 왼쪽된 창에서 마우스 오른쪽 단추로 클릭 **Hyper-v 관리자**합니다.
1. 클릭 **서버에 연결할**합니다.
1. 선택 **다른 사용자로 연결** 에 **컴퓨터 선택** 대화 상자.
1. 선택 **사용자 설정**합니다.

>[!NOTE]
> Windows Server 2016 또는 Windows 10 에서만 작동 이렇게 **원격** 호스트 합니다.

### <a name="connect-to-a-windows-2016-or-windows-10-remote-host-using-ip-address"></a>IP 주소를 사용 하 여 Windows 2016 또는 Windows 10 원격 호스트에 연결

가상 하드 디스크 파일에 대한 중요 정보를 제공하려면

1. 왼쪽된 창에서 마우스 오른쪽 단추로 클릭 **Hyper-v 관리자**합니다.
1. 클릭 **서버에 연결할**합니다.
1. IP 주소를 입력 합니다 **다른 컴퓨터** 텍스트 필드입니다.

>[!NOTE]
> Windows Server 2016 또는 Windows 10 에서만 작동 이렇게 **원격** 호스트 합니다.

### <a name="connect-to-a-windows-2016-or-windows-10-remote-host-outside-your-domain-or-with-no-domain"></a>Windows 2016 또는 Windows 10 원격 호스트에 없는 도메인 또는 도메인에 외부 연결

가상 하드 디스크 파일에 대한 중요 정보를 제공하려면

1. 관리할 Hyper-v 호스트에서 관리자 권한으로 Windows PowerShell 세션을 엽니다.

1. 개인 네트워크 영역에 대 한 필요한 방화벽 규칙을 만듭니다.   
   
   ```
   Enable-PSRemoting
   ```

2. 공용 영역에 대 한 원격 액세스를 허용 하려면 CredSSP 및 WinRM에 대 한 방화벽 규칙을 사용 합니다.
  
   ```
   Enable-WSManCredSSP -Role server
   ```

    자세한 내용은 참조 하세요 [Enable-psremoting](https://technet.microsoft.com/library/hh849694.aspx) 하 고 [Enable-wsmancredssp](https://technet.microsoft.com/library/hh849872.aspx)합니다.

다음으로 구성 컴퓨터에서 Hyper-v 호스트를 관리 하는 데 사용 됩니다.

1. 관리자 권한으로 Windows PowerShell 세션을 엽니다.
1. 이러한 명령을 실행 합니다.

     ```
     Set-Item WSMan:\localhost\Client\TrustedHosts -Value "fqdn-of-hyper-v-host"
     ```
     ```
     Enable-WSManCredSSP -Role client -DelegateComputer "fqdn-of-hyper-v-host"
     ```
1. 다음 그룹 정책을 구성 해야 할 수 있습니다. 
    * **컴퓨터 구성** \> **관리 템플릿** \> **System** \> **자격 증명을 위임** \> **NTLM 전용일 서버 인증을 사용 하 여 새 자격 증명 위임 허용**
    * 클릭 **을 사용 하도록 설정** 추가한 *wsman/fqdn-의-하이퍼-v-호스트*합니다.
1. 열기 **Hyper-v 관리자**합니다.
1. 왼쪽된 창에서 마우스 오른쪽 단추로 클릭 **Hyper-v 관리자**합니다.
1. 클릭 **서버에 연결할**합니다.

>[!NOTE]
> Windows Server 2016 또는 Windows 10 에서만 작동 이렇게 **원격** 호스트 합니다.

Cmdlet 세부 정보를 참조 하세요 [Set-item](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.management/set-item) 하 고 [Enable-wsmancredssp](https://technet.microsoft.com/library/hh849872.aspx)합니다.

## <a name="install-hyper-v-manager"></a>Hyper-v 관리자를 설치 합니다.

UI 도구를 사용 하려면 Hyper-v 관리자를 실행 하는 컴퓨터의 운영 체제에 대 한 적절 한 것을 선택 합니다.

Windows Server에서 서버 관리자를 엽니다 \> **관리** \> **역할 및 기능 추가**합니다. 으로 이동 합니다 **기능** 페이지 및 확장 **원격 서버 관리 도구** \> **역할 관리 도구** \>  **Hyper-v 관리 도구**합니다. 

Windows, Hyper-v 관리자는에서 사용할 수 있습니다 [Hyper-v를 포함 하는 모든 Windows 운영 체제](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_compatibility)합니다.

1. Windows 바탕 화면에서 시작 단추를 클릭 하 고 입력 하기 시작 **프로그램 및 기능**합니다. 
1. 검색 결과에서 클릭 **프로그램 및 기능**합니다.
1. 왼쪽된 창에서 클릭 **설정할 Windows 기능 사용 /** 합니다.
1. Hyper-v가 폴더를 확장 하 고 **Hyper-v 관리 도구**합니다.
1. Hyper-v 관리자를 설치 하려면 클릭 **Hyper-v 관리 도구**합니다. 또한 Hyper-v 모듈을 설치 하려는 경우 해당 옵션을 클릭 합니다.

Windows PowerShell을 사용 하려면 다음 명령을 관리자 권한으로 실행 합니다.

```
add-windowsfeature rsat-hyper-v-tools
```

## <a name="see-also"></a>참조  
 
[Hyper-V 설치](..\get-started\Install-the-Hyper-V-role-on-Windows-Server.md) 

