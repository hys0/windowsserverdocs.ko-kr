---
title: Windows Server에서 PowerShell을 사용하여 "작업 리소스" RDS 제목 사용자 지정
description: 작업 영역 이름을 Windows Server의 기본 이름에서 다르게 변경하는 방법을 설명합니다.
ms.prod: windows-server-threshold
ms.technology: remote-desktop-services
ms.author: helohr
ms.date: 10/26/2017
ms.topic: article
author: Heidilohr
ms.openlocfilehash: 43837826a6cddc2c3c4c7c1af874334718a3a067
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2019
ms.locfileid: "63743342"
---
# <a name="customize-the-rds-title-work-resources-using-powershell-on-windows-server"></a>Windows Server에서 PowerShell을 사용하여 "작업 리소스" RDS 제목 사용자 지정

Windows Server를 사용하여 RD WebAccess 또는 새 원격 데스크톱 앱을 통해 RemoteApp 또는 데스크톱에 액세스할 경우 기본적으로 작업 영역 제목이 "Work Resources"로 표시됩니다.  PowerShell cmdlet을 사용하여 이 제목을 쉽게 변경할 수 있습니다.

제목을 변경하려면 연결 브로커 서버에서 새 PowerShell 창을 열고 다음 명령을 사용하여 RemoteDesktop 모듈을 가져옵니다.

```powershell
    Import-Module RemoteDesktop
```

그런 다음, Set-RDWorkspace 명령을 사용하여 작업 영역 이름을 변경합니다.

```powershell
    Set-RDWorkspace [-Name] <string> [-ConnectionBroker <string>]  [<CommonParameters>]
```   

예를 들어, 다음 명령을 사용하여 작업 영역 이름을 "Contoso RemoteAapps"로 변경할 수 있습니다.

```powershell
    Set-RDWorkspace -Name "Contoso RemoteApps" -ConnectionBroker broker01.contoso.com
```

고가용성 모드에서 여러 연결 브로커를 실행하는 경우 활성 브로커에 대해 이 명령을 실행해야 합니다. 다음 명령을 사용할 수 있습니다.

```powershell
    Set-RDWorkspace -Name "Contoso RemoteApps" -ConnectionBroker (Get-RDConnectionBrokerHighAvailability).ActiveManagementServer
```

Set-RDWorkspace cmdlet에 대한 자세한 내용은 [Set-RDSWorkspace](https://docs.microsoft.com/powershell/module/remotedesktop/set-rdworkspace?view=win10-ps) 참조를 참조하세요.