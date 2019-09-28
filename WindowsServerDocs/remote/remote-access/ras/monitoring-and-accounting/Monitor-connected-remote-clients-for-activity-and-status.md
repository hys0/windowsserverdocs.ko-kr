---
title: 연결된 원격 클라이언트에서 활동 및 상태 모니터링
description: 이 항목은 Windows Server 2016의 원격 액세스 모니터링 및 계정에 대 한 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: beb94475-b21f-46a9-ac51-bf2bb28ca94e
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 03d87fb086a9f2797af8399be3d833b11bed79a5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71367263"
---
# <a name="monitor-connected-remote-clients-for-activity-and-status"></a>연결된 원격 클라이언트에서 활동 및 상태 모니터링

>적용 대상: Windows Server(반기 채널), Windows Server 2016

**참고:** Windows Server 2012에서는 DirectAccess 및 원격 액세스 서비스 (RAS)를 단일 원격 액세스 역할로 결합 합니다.  
  
원격 액세스 서버에서 원격 클라이언트의 작업 및 상태를 모니터링 하는 관리 콘솔을 사용할 수 있습니다.  
  
> [!NOTE]  
> 이 항목에 설명 된 작업을 완료 하려면 Domain Admins 그룹의 구성원 또는 각 컴퓨터에서 Administrators 그룹의 구성원으로 로그인 해야 합니다. Administrators 그룹의 구성원 인 계정으로 로그인 하는 동안에 작업을 완료할 수 없는 경우에 Domain Admins 그룹의 구성원 인 계정으로 로그인 하는 동안 작업을 수행해 봅니다.  
  
#### <a name="to-monitor-remote-client-activity-and-status"></a>원격 클라이언트의 작업 및 상태를 모니터링 하려면  
  
1.  **서버 관리자**, 클릭 **도구**, 를 클릭 하 고 **원격 액세스 관리**합니다.  
  
2.  클릭 **보고** 탐색할 **원격 액세스 보고** 에 **원격 액세스 관리 콘솔**합니다.  
  
3.  클릭 **원격 클라이언트 상태** 원격 클라이언트 활동 및 상태 사용자 인터페이스를 탐색 하는 **원격 액세스 관리 콘솔**합니다.  
  
4.  원격 액세스 서버에 연결 되 고 자세한 사용자의 목록을 표시에 대 한 통계입니다. 클라이언트에 해당 하는 목록에서 첫 번째 행을 클릭 합니다. 행을 선택 하면 원격 사용자 활동은 미리 보기 창에 표시 됩니다.  
  
![Windows PowerShell](../../../media/Monitor-connected-remote-clients-for-activity-and-status/PowerShellLogoSmall.gif)***<em>windows powershell 해당 명령</em>***  
  
다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.  
  
```  
PS> Get-RemoteAccessConnectionStatistics  
```  
  
사용자 통계는 다음 표에 필드를 사용 하 여 선택한 조건에 따라 필터링 할 수 있습니다.  
  
|필드 이름|값|  
|-------|-----|  
|Username|원격 사용자의 사용자 이름 또는 별칭입니다. 예: contoso 사용자 그룹을 선택 하는 와일드 카드 문자를 사용할 수 있습니다\\* 또는 \*\administrator 합니다.|  
|Hostname|원격 사용자의 컴퓨터 계정 이름입니다. 또한 IPv4 또는 IPv6 주소 지정할 수 있습니다.|  
|type|DirectAccess 또는 VPN입니다. DirectAccess를 선택 하는 경우 DirectAccess를 사용 하 여 연결 된 모든 원격 사용자가 나열 됩니다. VPN을 선택 하면 VPN을 사용 하 여 연결 된 모든 원격 사용자가 나열 됩니다.|  
|ISP 주소|원격 사용자의 IPv4 또는 IPv6 주소입니다.|  
|IPv4 주소|원격 사용자는 회사 네트워크에 연결 하는 터널의 내부 IPv4 주소입니다.|  
|IPv6 주소|원격 사용자를 회사 네트워크에 연결하는 터널의 내부 IPv6 주소입니다.|  
|프로토콜/터널|원격 클라이언트에 의해 사용 되는 전환 기술입니다. 이 Teredo, 6to4 또는 IP-HTTPS DirectAccess 사용자에 대 한 아니며 PPTP, L2TP, SSTP 또는 IKEv2 VPN 사용자에 대 한 합니다.|  
|액세스한 리소스|특정 회사 리소스나 끝점에 액세스하고 있는 모든 사용자입니다. 이 필드에 해당 하는 값이 서버의 호스트 이름/i P 주소입니다.|  
|서버|클라이언트가 연결될 원격 액세스 서버입니다. 이 필드는 클러스터 및 멀티 사이트 배포에만 해당됩니다.|  
  
  
  


