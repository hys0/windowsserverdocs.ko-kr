---
title: 일반적인 문제 해결
description: 이 가이드의 일부인이 항목에서는 여러 원격 액세스 서버 배포 Windows Server 2016에서 멀티 사이트 배포에서 합니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 354ae5e3-bae1-44f9-afd7-7eaba70f2346
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 87614ac3b83eaacefb4ac5f9fddef238ed500953
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67282549"
---
# <a name="troubleshooting-general-issues"></a>일반적인 문제 해결

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 항목에서는 원격 액세스와 관련 된 일반적인 문제에 대 한 문제 해결 정보를 포함 합니다.  
  
## <a name="gpo-retrieval-error"></a>GPO 검색 오류  
**수신 된 오류**합니다. DirectAccess 서버 GPO 설정은 검색할 수 없습니다. GPO에 대 한 편집 권한이 있는지 확인 합니다.  
  
이 오류를 받은 후 원격 액세스 관리 콘솔을 응답 하지 않습니다.  
  
**가능한 원인**  
  
DirectAccess 배포에서 진입점 중 하나의 GPO에 액세스할 수 없습니다 하 고 결과적으로 구성을 로드 하지 못했습니다.  
  
**해결 방법**  
  
배포의 각 진입점에 해당 도메인 컨트롤러에서 해당 GPO 있는지 확인 하 고 로그온된 한 사용자 읽기 및 쓰기 원격 액세스 배포에서 구성 하는 모든 Gpo에 대 한 권한이 있는지를 확인 합니다.  
  
대 안으로 원격 액세스 관리 콘솔을 사용 하는 대신 구성 cmdlet을 사용 예를 들어,를 사용 하 여 `Get-RemoteAccess` 고 `Get-DAEntryPoint`입니다.  
  
> [!NOTE]  
> 이 시나리오에는 현재 진입점의 서버 GPO를 사용할 수 없는 경우 발생 하지 않습니다.  
  
사용할 수는 `Get-DAEntryPointDC` 서버 Gpo를 저장 하는 모든 도메인 컨트롤러를 나열 하는 cmdlet 및 `Get-DAMultiSite` 와 함께에서 `Get-RemoteAccess` 배포의 서버 Gpo의 전체 목록을 검색 하려면. 예를 들어 다음과 같은 가치를 제공해야 합니다.  
  
```  
$ServerGpos = Get-DAEntryPointDC | ForEach-Object {   
   @{   
       GpoName = (Get-RemoteAccess -EntryPoint $_.EntryPointName).ServerGpoName;   
        DC = $_.DomainControllerName }   
}  
$ServerGpos | ForEach-Object { $GpoName = $_['GpoName'] ; $DC = $_['DC'] ; Write-Host "Server GPO '$GpoName' on DC '$DC'" }  
```  
  
## <a name="windows-7-to-windows-8-or-10-client-upgrade"></a>Windows 8로 Windows 7 또는 10 클라이언트 업그레이드  
**증상**합니다. Windows 7 클라이언트 멀티 사이트 배포에서 Windows 10 또는 Windows 8로 업그레이드 한 후에 DirectAccess 연결 네트워크 목록에 표시 되지 않습니다.  
  
**가능한 원인**  
  
멀티 사이트 배포에서 Windows 7 Gpo는 Windows 8 네트워크 연결 길잡이 구성을 포함 되지 않습니다.  
  
 Windows 7 클라이언트는 Windows 7 클라이언트 Gpo에서에서 별도 수동 구성 해야 하는 게 DirectAccess 연결 상태를 모니터링 하려면 DirectAccess 연결 길잡이 사용 해야 합니다. Windows 7 클라이언트를 Windows 10 또는 Windows 8 업그레이드 되는 네트워크 연결 길잡이가 작동 하지 않습니다 경우 Windows 7 클라이언트 GPO가 여전히 적용 됩니다.  
  
**해결 방법**  
  
DirectAccess 연결 길잡이 설정을 Windows 7 Gpo에 구성 된 경우에 다음 PowerShell cmdlet을 사용 하 여 Windows 7 Gpo를 수정 하 여 클라이언트 컴퓨터를 업그레이드 하기 전에이 문제를 해결할 수 있습니다.  
  
```  
Set-GPRegistryValue -Name <Windows7GpoName> -Domain <DomainName> -Key "HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\NetworkConnectivityAssistant" -ValueName "TemporaryValue" -Type Dword -Value 1  
Remove-GPRegistryValue -Name <Windows7GpoName> -Domain <DomainName> -Key "HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\NetworkConnectivityAssistant"  
```  
  
이미 업그레이드 된 클라이언트는 DCA 구성 되지 않은, 경우 Windows 10 또는 Windows 8 보안 그룹에 클라이언트 컴퓨터를 이동 합니다.  
  
## <a name="general-cmdlet-errors"></a>일반 cmdlet 오류  
  
-   **문제 1**  
  
    **수신 된 오류**합니다. 도메인 컨트롤러 < 도메인 > _ < 서버 _ 이름 또는 진입점 >에 연결할 수 없습니다.  
  
    **가능한 원인**  
  
    멀티 사이트 배포에서 구성 일관성을 유지하려면 각 GPO를 한 도메인 컨트롤러로 관리하는 것이 중요합니다. 진입점의 서버 GPO를 관리 하는 도메인 컨트롤러를 사용할 수 없는 경우 원격 액세스 구성 설정의 내용을 읽거나 수정 될 수 없습니다.  
  
    **해결 방법**  
  
    에 설명 된 "서버 Gpo를 관리 하는 도메인 컨트롤러를 변경 하려면" 절차에 따라 [2.4. Gpo 구성](assetId:///b1960686-a81e-4f48-83f1-cc4ea484df43#ConfigGPOs)합니다.  
  
-   **문제점 2**  
  
    **수신 된 오류**합니다. < 도메인 _ 이름 > 도메인에서 주 도메인 컨트롤러에 연결할 수 없습니다.  
  
    **가능한 원인**  
  
    멀티 사이트 배포에서 구성 일관성을 유지하려면 각 GPO를 한 도메인 컨트롤러로 관리하는 것이 중요합니다. 클라이언트 GPO는 기본 도메인 컨트롤러에서 관리됩니다. 기본 도메인 컨트롤러가 없다면 원격 액세스 구성 설정을 읽거나 수정할 수 없습니다.  
  
    **해결 방법**  
  
    에 설명 된 "PDC 에뮬레이터 역할을 전송 하려면" 절차에 따라 [2.4. Gpo 구성](assetId:///b1960686-a81e-4f48-83f1-cc4ea484df43#ConfigGPOs)합니다.  
  


