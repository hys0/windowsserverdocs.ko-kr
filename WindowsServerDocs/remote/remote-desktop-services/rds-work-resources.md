---
title: Windows Server에서 PowerShell을 사용한 RDS 타이틀 "작업 리소스" 사용자 지정
description: Windows Server의 기본에서 작업 영역 이름을 변경 하는 방법에 대 한 설명을 제공 합니다.
ms.prod: windows-server-threshold
ms.technology: remote-desktop-services
ms.author: helohr
ms.date: 10/26/2017
ms.topic: article
author: Heidilohr
ms.openlocfilehash: 43837826a6cddc2c3c4c7c1af874334718a3a067
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59826714"
---
# <a name="customize-the-rds-title-work-resources-using-powershell-on-windows-server"></a>Windows Server에서 PowerShell을 사용한 RDS 타이틀 "작업 리소스" 사용자 지정

Windows Server를 사용 하 여 RD 웹 액세스 또는 새 원격 데스크톱 앱을 통해 Remoteapp 또는 데스크톱에 액세스를 알 수 있습니다 작업 영역이 기본적으로 "작업 리소스"를 제목은입니다.  PowerShell cmdlet을 사용 하 여 제목을 쉽게 변경할 수 있습니다.

제목을 변경 하려면 연결 브로커 서버에서 새 PowerShell 창을 열고 하 고 다음 명령 사용 하 여 RemoteDesktop 모듈을 가져옵니다.

```powershell
    Import-Module RemoteDesktop
```

그런 다음 명령을 사용 하 여 집합 RDWorkspace 작업 영역 이름을 변경 합니다.

```powershell
    Set-RDWorkspace [-Name] <string> [-ConnectionBroker <string>]  [<CommonParameters>]
```   

예를 들어 "Contoso Remoteapp"를 작업 영역 이름을 변경 하려면 다음 명령을 사용할 수 있습니다.

```powershell
    Set-RDWorkspace -Name "Contoso RemoteApps" -ConnectionBroker broker01.contoso.com
```

가용성 우선 모드에서 여러 연결 브로커를 실행 하는 경우 활성 broker에 대해 실행 해야 합니다. 이 명령을 사용할 수 있습니다.

```powershell
    Set-RDWorkspace -Name "Contoso RemoteApps" -ConnectionBroker (Get-RDConnectionBrokerHighAvailability).ActiveManagementServer
```

집합 RDWorkspace cmdlet에 대 한 자세한 내용은 참조는 [집합 RDSWorkspace](https://docs.microsoft.com/powershell/module/remotedesktop/set-rdworkspace?view=win10-ps) 참조 합니다.