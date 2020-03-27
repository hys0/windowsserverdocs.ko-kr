---
title: 일반적인 문제 해결
description: 이 항목은 Windows Server 2016에서 멀티 사이트 배포에서 여러 원격 액세스 서버 배포 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 354ae5e3-bae1-44f9-afd7-7eaba70f2346
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 513bcae13d4a8f3ab935d2bda77745baa1788fa9
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80313791"
---
# <a name="troubleshooting-general-issues"></a>일반적인 문제 해결

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목에는 원격 액세스와 관련 된 일반적인 문제에 대 한 문제 해결 정보가 포함 되어 있습니다.  
  
## <a name="gpo-retrieval-error"></a>GPO 검색 오류  
**오류가 수신**되었습니다. DirectAccess 서버 GPO 설정을 검색할 수 없습니다. GPO에 대 한 편집 권한이 있는지 확인 합니다.  
  
이 오류를 받은 후 원격 액세스 관리 콘솔이 응답 하지 않습니다.  
  
**원인**  
  
DirectAccess에서 배포의 진입점 중 하나에 대 한 GPO에 액세스할 수 없으므로 구성이 로드 되지 않습니다.  
  
**해결 방법**  
  
배포의 각 진입점에 해당 하는 GPO가 해당 도메인 컨트롤러에 있는지 확인 하 고 로그온 한 사용자에 게 원격 액세스 배포에 구성 된 모든 Gpo에 대 한 읽기 및 쓰기 권한이 있는지 확인 합니다.  
  
문제를 해결 하려면 원격 액세스 관리 콘솔을 사용 하는 대신 구성 cmdlet을 사용 합니다. 예를 들어 `Get-RemoteAccess` 및 `Get-DAEntryPoint`를 사용 합니다.  
  
> [!NOTE]  
> 이 시나리오는 현재 진입점의 서버 GPO를 사용할 수 없는 경우에는 발생 하지 않습니다.  
  
`Get-DAEntryPointDC` cmdlet을 사용 하 여 서버 Gpo 및 `Get-DAMultiSite`를 `Get-RemoteAccess`와 함께 저장 하는 모든 도메인 컨트롤러를 나열 하 여 배포에서 전체 서버 Gpo 목록을 검색할 수 있습니다. 예를 들면 다음과 같습니다.  
  
```  
$ServerGpos = Get-DAEntryPointDC | ForEach-Object {   
   @{   
       GpoName = (Get-RemoteAccess -EntryPoint $_.EntryPointName).ServerGpoName;   
        DC = $_.DomainControllerName }   
}  
$ServerGpos | ForEach-Object { $GpoName = $_['GpoName'] ; $DC = $_['DC'] ; Write-Host "Server GPO '$GpoName' on DC '$DC'" }  
```  
  
## <a name="windows-7-to-windows-8-or-10-client-upgrade"></a>Windows 7에서 Windows 8 또는 10 클라이언트 업그레이드  
**증상**. Windows 7 클라이언트를 멀티 사이트 배포에서 Windows 10 또는 Windows 8로 업그레이드 한 후에는 네트워크 목록에 DirectAccess 연결이 표시 되지 않습니다.  
  
**원인**  
  
멀티 사이트 배포의 Windows 7 Gpo에는 Windows 8 네트워크 연결 길잡이 구성이 포함 되어 있지 않습니다.  
  
 Windows 7 클라이언트는 DirectAccess 연결 길잡이를 사용 하 여 Windows 7 클라이언트 Gpo에서 별도의 수동 구성이 필요한 DirectAccess 연결 상태를 모니터링 해야 합니다. Windows 7 클라이언트를 windows 10 또는 Windows 8로 업그레이드 하는 경우 Windows 7 클라이언트 GPO가 계속 적용 되는 경우 네트워크 연결 도우미가 작동 하지 않습니다.  
  
**해결 방법**  
  
Windows 7 Gpo에서 DirectAccess 연결 길잡이 설정이 구성 된 경우 다음 PowerShell cmdlet을 사용 하 여 Windows 7 Gpo를 수정 하 여 클라이언트 컴퓨터를 업그레이드 하기 전에이 문제를 해결할 수 있습니다.  
  
```  
Set-GPRegistryValue -Name <Windows7GpoName> -Domain <DomainName> -Key "HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\NetworkConnectivityAssistant" -ValueName "TemporaryValue" -Type Dword -Value 1  
Remove-GPRegistryValue -Name <Windows7GpoName> -Domain <DomainName> -Key "HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\NetworkConnectivityAssistant"  
```  
  
클라이언트를 이미 업그레이드 했거나 DCA가 구성 되지 않은 경우 클라이언트 컴퓨터를 Windows 10 또는 Windows 8 보안 그룹으로 이동 합니다.  
  
## <a name="general-cmdlet-errors"></a>일반 cmdlet 오류  
  
-   **문제 1**  
  
    **오류가 수신**되었습니다. < Server_name 또는 entry_point_name >에 대해 도메인 컨트롤러 < domain_controller >에 연결할 수 없습니다.  
  
    **원인**  
  
    멀티 사이트 배포에서 구성 일관성을 유지하려면 각 GPO를 한 도메인 컨트롤러로 관리하는 것이 중요합니다. 진입점의 서버 GPO를 관리 하는 도메인 컨트롤러를 사용할 수 없는 경우 원격 액세스 구성 설정을 읽거나 수정할 수 없습니다.  
  
    **해결 방법**  
  
    2\.4에 설명 된 "서버 Gpo를 관리 하는 도메인 컨트롤러를 변경 하려면" 절차를 따르세요 [. Gpo를 구성](assetId:///b1960686-a81e-4f48-83f1-cc4ea484df43#ConfigGPOs)합니다.  
  
-   **문제 2**  
  
    **오류가 수신**되었습니다. 도메인 < domain_name >의 주 도메인 컨트롤러에 연결할 수 없습니다.  
  
    **원인**  
  
    멀티 사이트 배포에서 구성 일관성을 유지하려면 각 GPO를 한 도메인 컨트롤러로 관리하는 것이 중요합니다. 클라이언트 GPO는 기본 도메인 컨트롤러에서 관리됩니다. 기본 도메인 컨트롤러가 없다면 원격 액세스 구성 설정을 읽거나 수정할 수 없습니다.  
  
    **해결 방법**  
  
    2\.4에 설명 된 "PDC 에뮬레이터 역할을 전송 하려면" 절차를 따르세요 [. Gpo를 구성](assetId:///b1960686-a81e-4f48-83f1-cc4ea484df43#ConfigGPOs)합니다.  
  


