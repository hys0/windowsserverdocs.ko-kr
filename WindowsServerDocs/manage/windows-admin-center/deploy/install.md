---
title: Windows Admin Center 설치
description: Windows Admin Center 설치
ms.technology: manage
ms.topic: article
author: jwwool
ms.author: jeffrew
ms.date: 03/07/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 94ac1281ca94a49ae54ce28d86dd4d95ff1d5574
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59866924"
---
# <a name="install-windows-admin-center"></a>Windows Admin Center 설치

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

> [!Tip]
> Windows Admin Center를 처음 사용하시나요?
> [Windows Admin Center에 대해 자세히 알아보거나](../understand/windows-admin-center.md)[지금 다운로드](https://aka.ms/windowsadmincenter)하세요.

## <a name="determine-your-installation-type"></a>설치 유형을 확인합니다

검토 합니다 [설치 옵션](..\plan\installation-options.md) 포함 하는 합니다 [지원 되는 운영 체제](..\plan\installation-options.md#supported-operating-systems-installation)합니다.

## <a name="install-on-windows-10"></a>Windows 10에 설치

Windows 10에서 Windows Admin Center를 설치하면 기본적으로 6516 포트를 사용하지만 다른 포트를 지정하는 옵션이 있습니다. 바탕 화면 바로 가기를 만들고 Windows Admin Center에서 TrustedHosts를 관리하도록 할 수도 있습니다.

> [!NOTE]
> 작업 그룹 환경에서, 또는 도메인에서 로컬 관리자 자격 증명을 사용할 경우 TrustedHosts 수정이 필요합니다. 이 설정을 중단하고 싶으면 반드시 [TrustedHosts를 수동으로 구성](../use/troubleshooting.md#configure-trustedhosts)해야 합니다.

**시작** 메뉴에서 Windows Admin Center를 시작하면 기본 브라우저에서 열립니다.

처음으로 Windows Admin Center를 시작하면 데스크톱의 알림 영역에 아이콘이 표시됩니다. 이 아이콘을 마우스 오른쪽 단추로 클릭하고 **열기**를 선택하여 기본 브라우저에서 도구를 열거나 **종료**를 클릭하여 백그라운드 프로세스를 종료합니다.

## <a name="install-on-windows-server-with-desktop-experience"></a>데스크톱 환경 포함 Windows Server에 설치

Windows Server에서 Windows Admin Center는 네트워크 서비스로 설치됩니다. 서비스가 수신 대기할 포트를 지정해야 하고 HTTPS에 대한 인증서가 필요합니다. 설치 프로그램이 테스트용으로 자체 서명된 인증서를 생성하거나 사용자가 컴퓨터에 이미 설치된 인증서의 지문을 제공할 수 있습니다. 생성된 인증서를 사용하는 경우 이는 서버의 DNS 이름과 일치합니다. 사용자 고유의 인증서를 사용 하는 경우 인증서에 지정 된 이름과 일치 해야 컴퓨터 이름 (와일드 카드 인증서는 지원 되지 않습니다). Windows Admin Center TrustedHosts를 관리할 수 있도록 하려면 선택도 나와 있습니다.

> [!NOTE]
> 작업 그룹 환경에서, 또는 도메인에서 로컬 관리자 자격 증명을 사용할 경우 TrustedHosts 수정이 필요합니다. 이 설정을 중단하고 싶으면 반드시 [TrustedHosts를 수동으로 구성](../use/troubleshooting.md#configure-trustedhosts)해야 합니다.

설치가 완료 되 면 원격 컴퓨터에서 브라우저를 열고 설치 관리자의 마지막 단계에 제공 된 URL로 이동 합니다.

> [!WARNING]
> 자동 생성된 인증서는 설치 60일 후에 만료됩니다.

## <a name="install-on-server-core"></a>Server Core에 설치

Windows Server의 Server Core 설치가 있는 경우 명령 프롬프트(관리자 권한으로 실행)에서 Windows Admin Center를 설치할 수 있습니다. 각각 `SME_PORT` 및 `SSL_CERTIFICATE_OPTION` 인수를 사용하여 포트 및 SSL 인증서를 지정합니다. 기존 인증서를 사용하려는 경우 `SME_THUMBPRINT`를 사용하여 지문을 지정합니다.

> [!WARNING]
> Windows Admin Center 설치 하면 모든 원격 PowerShells 세션 서버를 WinRM 서비스를 다시 시작 됩니다. 로컬 Cmd 또는 PowerShell을 설치 하는 것이 좋습니다. WinRM 서비스가 다시 시작을 대상인 자동화 솔루션을 사용 하 여 설치 하는 경우 매개 변수를 추가할 수 있습니다 ```RESTART_WINRM=0``` 설치에 인수가 있지만 WinRM 다시 시작 해야 Windows Admin Center 대 한 함수입니다.

Windows Admin Center를 설치하고 자체 서명된 인증서를 자동으로 생성하려면 다음 명령을 실행합니다.

```   
msiexec /i <WindowsAdminCenterInstallerName>.msi /qn /L*v log.txt SME_PORT=<port> SSL_CERTIFICATE_OPTION=generate
```

기존 인증서를 사용하여 Windows Admin Center를 설치하려면 다음 명령을 실행합니다.

```
msiexec /i <WindowsAdminCenterInstallerName>.msi /qn /L*v log.txt SME_PORT=<port> SME_THUMBPRINT=<thumbprint> SSL_CERTIFICATE_OPTION=installed
```

> [!WARNING]
> PowerShell에서 ./ 상대 경로 표기법(예: `.\<WindowsAdminCenterInstallerName>.msi`)을 사용하여 `msiexec`를 호출하지 마십시오. 해당 표기법은 지원되지 않으며 설치가 실패합니다. `.\` 접두사를 제거하거나 MSI에 대한 전체 경로를 지정합니다.

## <a name="updating-windows-admin-center"></a>Windows Admin Center 업데이트

Windows Admin Center 새 버전으로 업그레이드할 때 사용자 설정이 유지 됩니다. 업그레이드 Insider Preview 버전의 Windows Admin Center 공식적으로 지원 되지 않습니다--새로 설치 하는 것이 좋습니다 생각 하지만 차단 되지 않도록 합니다.