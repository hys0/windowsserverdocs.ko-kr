---
title: Windows Server 2016에서 제거되었거나 사용되지 않는 기능
description: 기능 및 Windows Server 2016에서 현재 릴리스의 제품에서 제거 되었거나 또는 (사용 되지 않음) 하는 후속 릴리스에서 제거 하도록 계획 되어 있는 특성의 목록입니다. 상용 환경에서 운영 체제를 업데이트하는 IT 전문가가 참조하시면 유용합니다.
ms.prod: windows-server-threshold
ms.technology: server-general
ms.topic: article
ms.date: 05/21/2019
ms.assetid: 5d10c5f9-ebac-49a0-b808-c0b1702e0437
author: jasongerend
ms.author: jgerend
manager: dougkim
ms.localizationpriority: medium
ms.openlocfilehash: 83855cf7e4fa86a932298dd15735dc5bf7277dfb
ms.sourcegitcommit: c8cc0b25ba336a2aafaabc92b19fe8faa56be32b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/21/2019
ms.locfileid: "65976601"
---
# <a name="features-removed-or-deprecated-in--windows-server-2016"></a>Windows Server 2016에서 제거되었거나 사용되지 않는 기능

>적용 대상: Windows Server 2016

아래에는 현재 릴리스에서 제거되었거나 다음 릴리스에서 제거될 예정인 Windows Server 2016의 기능, 즉 더 이상 사용되지 않는 기능의 목록이 나와 있습니다. 상용 환경에서 운영 체제를 업데이트하는 IT 전문가가 참조하시면 유용합니다. 후속 릴리스의 변경 사항에 따라 달라질 수 있으며 일부 사용되지 않는 기능이 생략되었을 수 있습니다. 특정 기능 또는 해당 기능을 대신하는 기능에 대한 자세한 내용은 해당 기능에 대한 설명서를 참조하세요.

항목 제거 되었거나 최신 버전에서 지원 되지 않는 대 한 정보를 참조 하세요 [기능 제거 또는 교체를 시작 하는 Windows Server 2019에 대해 계획 된](../get-started-19/removed-features-19.md)합니다.

## <a name="features-removed-from-windows-server-2016"></a>Windows Server 2016에서 제거된 기능

아래 기능은 이번 Windows Server 2016 릴리스에서 제거되었습니다. 제거된 기능에 종속된 응용 프로그램, 코드, 사용법은 다른 방법을 취하지 않는 한 이번 릴리스에서 실행되지 않습니다.  

> [!NOTE]  
> Windows Server 2012 R2 또는 Windows Server 2012 이전의 서버 릴리스에서 Windows Server 2016으로 전환하는 경우 [Windows Server 2012 R2에서 제거되었거나 더 이상 사용되지 않는 기능](https://technet.microsoft.com/library/dn303411.aspx) 및 [Windows Server 2012에서 제거되었거나 더 이상 사용되지 않는 기능](https://technet.microsoft.com/library/hh831568.aspx)도 검토해야 합니다.  


### <a name="file-server"></a>파일 서버  
Microsoft Management Console용 공유 및 저장소 관리 스냅인이 제거되었습니다. 대신 다음 중 하나를 수행합니다.  

-   관리하려는 컴퓨터에서 Windows Server 2016 이전 운영 체제를 실행 중인 경우 원격 데스크톱에 연결하여 로컬 버전의 공유 및 저장소 관리 스냅인을 사용합니다.  

-   Windows 8.1 이하를 실행하는 컴퓨터에서 RSAT의 공유 및 저장소 관리 스냅인을 사용하여 관리하려는 컴퓨터를 확인합니다.  

-   클라이언트 컴퓨터에서 Hyper-V를 사용하여 RSAT에 공유 및 저장소 관리 스냅인이 있는 Windows 7, Windows 8 또는 Windows 8.1 실행 가상 컴퓨터를 실행합니다.  

### <a name="journaldll"></a>Journal.dll  
Journal.dll은 Windows Server 2016에서 제거되었습니다. 대체 기능은 없습니다.  

### <a name="security-configuration-wizard"></a>보안 구성 마법사  
보안 구성 마법사가 제거되었습니다. 대신, 기본적으로 기능 보안이 유지됩니다. 특정 보안 설정을 제어해야 하는 경우 그룹 정책 또는 [Microsoft Security Compliance Manager](https://technet.microsoft.com/solutionaccelerators/cc835245.aspx)중 하나를 사용할 수 있습니다.  

### <a name="sqm"></a>SQM  
사용자 환경 개선 프로그램 참여를 관리하는 옵트인 구성 요소가 제거되었습니다. 

### <a name="windows-update"></a>Windows 업데이트
**wuauclt.exe /detectnow** 명령은 제거되어 더 이상 지원되지 않습니다. 업데이트 검색을 시작하려면 다음 중 하나를 수행합니다.

- 다음과 같은 PowerShell 명령을 실행합니다.
    ````powershell
    $AutoUpdates = New-Object -ComObject "Microsoft.Update.AutoUpdate"`
    $AutoUpdates.DetectNow()` 
    ````

- 아니면 다음의 VBScript를 사용합니다.
    ````vb
    Set automaticUpdates = CreateObject("Microsoft.Update.AutoUpdate")
    automaticUpdates.DetectNow()
    ````

## <a name="features-deprecated-starting-with-windows-server-2016"></a>Windows Server 2016부터 사용되지 않는 기능 
다음 기능은 이번 릴리스부터 사용되지 않습니다. 결국 제품에서 완전히 제거될 예정이지만 일단 이 버전에서는 계속 제공됩니다. 그러나 경우에 따라 일부 기능이 제거될 수 있습니다. 이러한 기능에 종속된 응용 프로그램, 코드, 사용법을 계속 사용하기 위한 다른 방법을 생각해야 합니다.  

### <a name="configuration-tools"></a>구성 도구  

-   **Scregedit.exe** 사용 되지 않습니다. Scregedit.exe에 의존하는 스크립트가 있는 경우 Reg.exe 또는 Windows PowerShell 방법을 사용하도록 조정합니다.  

-   **Sconfig.exe** 사용 되지 않습니다. 대신 Windows PowerShell을 사용합니다.  

### <a name="netcfg-custom-apis"></a>NetCfg 사용자 지정 API  
NetCfg 사용자 지정 API를 사용한 PrintProvider, NetClient 및 ISDN 설치가 더 이상 사용되지 않습니다.  

### <a name="remote-management"></a>원격 관리  
WinRM.vbs가 더 이상 사용되지 않습니다. 대신 Windows PowerShell WinRM 공급자의 기능을 사용합니다.  

### <a name="smb"></a>SMB  
SMB 2+ over NetBT가 더 이상 사용되지 않습니다. 대신 SMB over TCP 또는 RDMA를 구현합니다. 
