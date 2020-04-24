---
title: Windows Admin Center 설치
description: 여러 사용자가 웹 브라우저를 사용하여 Windows Admin Center에 액세스할 수 있도록 Windows PC 또는 서버에 Windows Admin Center를 설치하는 방법입니다.
ms.technology: manage
ms.topic: article
author: jwwool
ms.author: jeffrew
ms.date: 07/17/2019
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: cab128a3da9fa58c598cebcdf188058631c33977
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2020
ms.locfileid: "75950004"
---
# <a name="install-windows-admin-center"></a>Windows Admin Center 설치

> 적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

이 항목에서는 여러 사용자가 웹 브라우저를 사용하여 Windows Admin Center에 액세스할 수 있도록 Windows PC 또는 서버에 Windows Admin Center를 설치하는 방법에 대해 설명합니다.

> [!Tip]
> Windows Admin Center를 처음 사용하시나요?
> [Windows Admin Center에 대해 자세히 알아보거나](../overview.md) [지금 다운로드](https://aka.ms/windowsadmincenter)하세요.

## <a name="determine-your-installation-type"></a>설치 유형 결정

[지원되는 운영 체제](https://docs.microsoft.com/windows-server/manage/windows-admin-center/plan/installation-options#installation-supported-operating-systems)가 포함된 [설치 옵션](../plan/installation-options.md)을 검토합니다. Azure의 VM에 Windows Admin Center를 설치하려면 [Azure에서 Windows Admin Center 배포](../azure/deploy-wac-in-azure.md)를 참조하세요.

## <a name="install-on-windows-10"></a>Windows 10에 설치

Windows 10에서 Windows Admin Center를 설치하면 기본적으로 6516 포트를 사용하지만 다른 포트를 지정하는 옵션이 있습니다. 바탕 화면 바로 가기를 만들고 Windows Admin Center에서 TrustedHosts를 관리하도록 할 수도 있습니다.

> [!NOTE]
> 작업 그룹 환경에서, 또는 도메인에서 로컬 관리자 자격 증명을 사용할 경우 TrustedHosts 수정이 필요합니다. 이 설정을 중단하고 싶으면 반드시 [TrustedHosts를 수동으로 구성](../support/troubleshooting.md#configure-trustedhosts)해야 합니다.

**시작** 메뉴에서 Windows Admin Center를 시작하면 기본 브라우저에서 열립니다.

처음으로 Windows Admin Center를 시작하면 데스크톱의 알림 영역에 아이콘이 표시됩니다. 이 아이콘을 마우스 오른쪽 단추로 클릭하고 **열기**를 선택하여 기본 브라우저에서 도구를 열거나 **종료**를 선택하여 백그라운드 프로세스를 종료합니다.

## <a name="install-on-windows-server-with-desktop-experience"></a>데스크톱 환경이 포함된 Windows Server에 설치

Windows Server에서 Windows Admin Center는 네트워크 서비스로 설치됩니다. 서비스가 수신 대기할 포트를 지정해야 하고 HTTPS에 대한 인증서가 필요합니다. 설치 관리자가 테스트용으로 자체 서명된 인증서를 생성하거나 사용자가 컴퓨터에 이미 설치된 인증서의 지문을 제공할 수 있습니다. 생성된 인증서를 사용하는 경우 이는 서버의 DNS 이름과 일치합니다. 자체 인증서를 사용하는 경우 인증서에 제공된 이름이 머신 이름과 일치하는지 확인합니다(와일드카드 인증서는 지원되지 않음). Windows Admin Center에서 TrustedHosts를 관리하도록 선택할 수도 있습니다.

> [!NOTE]
> 작업 그룹 환경에서, 또는 도메인에서 로컬 관리자 자격 증명을 사용할 경우 TrustedHosts 수정이 필요합니다. 이 설정을 중단하고 싶으면 반드시 [TrustedHosts를 수동으로 구성](../support/troubleshooting.md#configure-trustedhosts)해야 합니다.

설치가 완료되면 원격 컴퓨터에서 브라우저를 열고 설치 관리자의 마지막 단계에 표시된 URL로 이동합니다.

> [!WARNING]
> 자동 생성된 인증서는 설치 60일 후에 만료됩니다.

## <a name="install-on-server-core"></a>Server Core에 설치

Windows Server의 Server Core 설치가 있는 경우 명령 프롬프트(관리자 권한으로 실행)에서 Windows Admin Center를 설치할 수 있습니다. 각각 `SME_PORT` 및 `SSL_CERTIFICATE_OPTION` 인수를 사용하여 포트 및 SSL 인증서를 지정합니다. 기존 인증서를 사용하려는 경우 `SME_THUMBPRINT`를 사용하여 지문을 지정합니다.

> [!WARNING]
> Windows Admin Center를 설치하면 모든 원격 PowerShell 세션을 지원하는 WinRM 서비스가 다시 시작됩니다. 로컬 Cmd 또는 PowerShell에서 설치하는 것이 좋습니다. WinRM 서비스 재시작으로 인해 중단된 자동화 솔루션을 사용하여 설치하는 경우 설치 인수에 ```RESTART_WINRM=0``` 매개 변수를 추가할 수 있지만 Windows Admin Center가 작동하려면 WinRM을 다시 시작해야 합니다.

Windows Admin Center를 설치하고 자체 서명된 인증서를 자동으로 생성하려면 다음 명령을 실행합니다.

```   
msiexec /i <WindowsAdminCenterInstallerName>.msi /qn /L*v log.txt SME_PORT=<port> SSL_CERTIFICATE_OPTION=generate
```

기존 인증서를 사용하여 Windows Admin Center를 설치하려면 다음 명령을 실행합니다.

```
msiexec /i <WindowsAdminCenterInstallerName>.msi /qn /L*v log.txt SME_PORT=<port> SME_THUMBPRINT=<thumbprint> SSL_CERTIFICATE_OPTION=installed
```

> [!WARNING]
> PowerShell에서 ./ 상대 경로 표기법(예: `.\<WindowsAdminCenterInstallerName>.msi`)을 사용하여 `msiexec`를 호출하지 마세요. 해당 표기법은 지원되지 않으며 설치가 실패합니다. `.\` 접두사를 제거하거나 MSI에 대한 전체 경로를 지정합니다.

## <a name="upgrading-to-a-new-version-of-windows-admin-center"></a>새 버전의 Windows Admin Center로 업그레이드

Microsoft 업데이트를 사용하거나 수동 설치를 통해 미리 보기가 아닌 Windows Admin Center 버전을 업데이트할 수 있습니다.

새 버전의 Windows Admin Center로 업그레이드 시 설정이 유지됩니다. 공식적으로 Windows Admin Center의 Insider Preview 버전 업그레이드를 지원하지 않습니다. 새로 설치하는 것이 더 좋을 것으로 생각하지만 이를 차단하지는 않습니다.

## <a name="updating-the-certificate-used-by-windows-admin-center"></a>Windows Admin Center에서 사용하는 인증서 업데이트

Windows Admin Center를 서비스로 배포하는 경우 HTTPS에 대한 인증서를 제공해야 합니다. 나중에 이 인증서를 업데이트하려면 설치 관리자를 다시 실행하고 ```change```를 선택합니다.
