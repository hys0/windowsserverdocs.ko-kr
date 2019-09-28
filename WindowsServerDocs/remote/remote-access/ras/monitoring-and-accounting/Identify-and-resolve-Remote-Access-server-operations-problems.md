---
title: 원격 액세스 서버 작업 문제 식별 및 해결
description: 이 항목은 Windows Server 2016의 원격 액세스 모니터링 및 계정에 대 한 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7ce84c9f-fd1f-4463-8fc7-d2f33344a2c9
ms.author: pashort
author: shortpatti
ms.openlocfilehash: db10f784f383938edb29b18d7e8febf869378abc
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404564"
---
# <a name="identify-and-resolve-remote-access-server-operations-problems"></a>원격 액세스 서버 작업 문제 식별 및 해결

>적용 대상: Windows Server(반기 채널), Windows Server 2016

**참고:** Windows Server 2012에는 DirectAccess와 RRAS(Routing and Remote Access Service)가 단일 원격 액세스 역할로 통합되어 있습니다.  
  
다음 절차를 사용 하 여 원격 액세스 서버 작업 문제, 해당 근본 원인 및 문제를 해결 하는 데 필요한 해상도 식별 하는 것이 있습니다.  
  
> [!NOTE]  
> 이 항목에 설명 된 작업을 완료 하려면 Domain Admins 그룹의 구성원 또는 각 컴퓨터에서 Administrators 그룹의 구성원으로 로그인 해야 합니다. Administrators 그룹의 구성원 인 계정으로 로그인 하는 동안에 작업을 완료할 수 없는 경우에 Domain Admins 그룹의 구성원 인 계정으로 로그인 하는 동안 작업을 수행해 봅니다.  
  
이 항목에는 다음 작업을 수행 하는 방법에 대 한 정보가 포함 됩니다.  
  
- 작업 문제를 시뮬레이션 합니다.  
  
- 작업 문제를 식별 하 고 수정 작업을 수행  
  
- IP 도우미 서비스를 복원 합니다.  
  
### <a name="BKMK_Simulate"></a>작업 문제 시뮬레이트  
  
> [!CAUTION]  
> 구성 때문에 원격 액세스 서버는 제대로 및 not이 문제가 발생을 작업 문제를 시뮬레이션 하는 다음 절차를 사용할 수 있습니다. 서버에 현재 프로덕션 환경에서 클라이언트를 서비스 하 고, 경우 지금 이러한 작업을 수행 하지 않을 수 있습니다. 대신, 나중에 원격 액세스 서버에서 문제가 발생할 수 있는 문제를 해결 하는 방법을 이해 하는 단계를 읽을 수 있습니다.  
  
IP 도우미 서비스 (IPHlpSvc) 호스트 IPv6 전환 기술 (예: IP-HTTPS 6to4 또는 Teredo) 이며 제대로 작동 하려면 DirectAccess 서버에 필요 합니다. 원격 액세스 서버에서 시뮬레이션 된 작업 문제를 보여 주기 위해 (IPHlpSvc) 네트워크 서비스를 중지 해야 합니다.  
  
##### <a name="to-stop-the-ip-helper-service"></a>IP 도우미 서비스를 중지 하려면  
  
1.  에 **시작** 화면 원격 액세스 서버를 클릭 하 여 **관리 도구**, 를 두 번 클릭 하 고 **서비스**.  
  
2.  목록에서 **서비스**, 아래로 스크롤하여 마우스 오른쪽 단추로 클릭 **IP 도우미**, 를 클릭 하 고 **중지**합니다.  
  
### <a name="BKMK_Identify"></a>작업 문제를 확인 하 고 정정 작업 수행  
IP 도우미 서비스를 해제 하면 원격 액세스 서버에서 심각한 오류가 발생 합니다. 모니터링 대시보드는 서버 작업 상태 및 문제에 대 한 세부 정보에 표시 됩니다.  
  
##### <a name="to-identify-the-details-and-take-corrective-action"></a>세부 정보를 식별 하 고 수정 작업을 수행 하려면  
  
1.  **서버 관리자**, 클릭 **도구**, 를 클릭 하 고 **원격 액세스 관리**합니다.  
  
2.  **대시보드**를 클릭하여 **원격 액세스 관리 콘솔**의 **원격 액세스 대시보드**로 이동합니다.  
  
3.  왼쪽된 창에서 원격 액세스 서버가 선택 되어 있는지 확인 하 고 가운데 창에서 클릭 **작동 상태**합니다.  
  
4.  작업 상태를 나타내는 녹색 또는 빨간색 아이콘으로 구성 요소 목록이 표시 됩니다. 클릭 된 **IP-HTTPS** 목록의 행입니다. 행을 선택 하는 경우에 작업에 대 한 세부 정보에 표시 됩니다는 **세부 정보** 다음과 같이 창:  
  
    **오류**  
  
    (IPHlpSvc) IP 도우미 서비스가 중지 되었습니다. DirectAccess 예상과 다르게 동작할 수 있습니다. IP 도우미 서비스의 연결, IPv6 전환 기술 플랫폼과 IP-HTTPS를 사용 하 여 터널 연결을 제공 합니다.  
  
    **컨트롤이**  
  
    1.  IP 도우미 서비스가 중지 되었습니다.  
  
    2.  IP 도우미 서비스가 응답 하지 않습니다.  
  
    **해결 방법**  
  
    1.  서비스가 실행 되 고 있는지를 확인 하려면 다음을 입력 **Get-service iphlpsc** Windows PowerShell 프롬프트입니다.  
  
    2.  서비스를 사용 하려면 입력 **Start-service iphlpsvc** 관리자 권한 Windows PowerShell 프롬프트에서.  
  
    3.  서비스를 다시 시작 하려면 입력 **서비스 다시 시작 iphlpsvc** 관리자 권한 Windows PowerShell 프롬프트에서.  
  
### <a name="BKMK_Restart"></a>IP 도우미 서비스 복원  
원격 액세스 서버에 IP 도우미 서비스를 복원 하려면 위의 하거나 서비스를 다시 시작 하려면 해결 단계를 수행 하거나 IP 도우미 서비스 오류를 시뮬레이션 하는 데 사용 하는 프로시저를 되돌리려면 다음 절차를 사용할 수 있습니다.  
  
##### <a name="to-restart-the-ip-helper-service-on-the-remote-access-server"></a>원격 액세스 서버에 IP 도우미 서비스를 다시 시작  
  
1.  에 **시작** 화면에서 **관리 도구**, 를 두 번 클릭 하 고 **서비스**합니다.  
  
2.  목록에서 **서비스**, 아래로 스크롤하여 마우스 오른쪽 단추로 클릭 **IP 도우미**, 를 클릭 하 고 **시작**합니다.  
  
![Windows PowerShell](../../../media/Identify-and-resolve-Remote-Access-server-operations-problems/PowerShellLogoSmall.gif)***<em>windows powershell 해당 명령</em>***  
  
다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.  
  
```  
PS> Get-RemoteAccessHealth | Where-Object {$_.Component -eq "IP-HTTPS"} | Format-List -Property *  
```  
  


