---
title: Windows Server Essentials에서 BranchCache 관리
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f6e05aec-d07c-4e0b-94ab-f20279e9ffd1
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 13d1d439eb9eeb60de9779d783e36405aee3ddfc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59828804"
---
# <a name="manage-branchcache-in-windows-server-essentials"></a>Windows Server Essentials에서 BranchCache 관리

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

BranchCache 도움이 될 수 있습니다, 인터넷 사용을 최적화 하 고, 네트워크 응용 프로그램의 성능을 개선 하 고, Windows Server Essentials 서버가 있는 원격 사무실에 가까워지거나 광역 네트워크 (WAN)에서 트래픽을 줄일 클라이언트 컴퓨터 로컬 서버 사용 하 여 클라우드 기반 리소스를 SharePoint Online 라이브러리와 같은 연결 합니다.  
  
 사용 하도록 설정 하는 BranchCache를 사용 하 여 클라이언트 컴퓨터에서 원격 Windows Server Essentials 서버에 콘텐츠를 콘텐츠를 요청 하는 경우 로컬 사무실에 캐시 됩니다. 그 후에는 동일한 사무실의 다른 컴퓨터가 WAN을 통해 서버에서 콘텐츠를 다시 다운로드하는 대신 로컬에서 콘텐츠를 가져올 수 있습니다. 이 경우 네트워크 응용 프로그램의 성능이 향상되고 WAN을 통한 대역폭 사용량이 감소됩니다.  
  
 Windows Server Essentials 서버에 로컬 또는 원격 인지, BranchCache 서버 공유 폴더 및 웹 콘텐츠 서버 (예: SharePoint Online 라이브러리)에서 호스트 되는 응답 시간을 개선할 수 있습니다.  
  
 BranchCache에 필요한 새로운 하드웨어 또는 네트워크 토폴로지 변경이 없으므로 이 기능을 통해 간단하게 대역폭 사용량을 최적화하고 WAN을 통해 액세스되는 서비스 및 리소스에 대한 응답 시간을 향상시킬 수 있습니다.  
  
## <a name="branchcache-scenarios"></a>BranchCache 시나리오  
 원격 서버와 함께 BranchCache를 사용하기 위한 세 가지 기본 시나리오가 있습니다.  
  
-   Windows Server Essentials 서버에 Microsoft Azure에서 호스트 됩니다.  
  
-   Windows Server Essentials 서버에는 타사 서비스 공급자의 데이터 센터에서 호스팅됩니다.  
  
-   Windows Server Essentials 서버에 다른 사무실 다른 물리적 위치에 있는 경우  
  
## <a name="distributed-cache-mode"></a>분산 캐시 모드  
 Windows Server Essentials에서 BranchCache에서 구현 됩니다 *분산된 캐시 모드*, BranchCache에서 사용할 수 있는 두 가지 캐시 모드 중 하나입니다. 분산 캐시 모드에서는 지점의 콘텐츠 캐시가 클라이언트 컴퓨터 간에 분산됩니다. 필요한 추가 하드웨어 또는 토폴로지 변경이 없기 때문에 이 모드는 원격 서버를 사용하거나 로컬 서버를 사용하여 SharePoint Online과 같은 클라우드 기반 서비스에 액세스하는 소규모 사무실에 적합합니다. Windows Server Essentials에서 BranchCache을 켜면 분산된 캐시 모드가 구현 됩니다.  
  
> [!NOTE]
>  둘 이상의 서브넷이 있거나 네트워크로 연결된 응용 프로그램을 사용하는 많은 직원이 있는 대규모 지점에서는 *호스트 캐시 모드*로 BranchCache를 구현하는 것이 좋습니다. 호스트 캐시 모드에서는 콘텐츠 캐시가 지점에 호스트된 하나 이상의 캐시 서버에 저장됩니다.
  
## <a name="requirements"></a>요구 사항  
 Windows Server Essentials에서 BranchCache를 사용 하려면 서버 및 클라이언트 컴퓨터는 다음 요구 사항을 충족 해야 합니다.  
  
-   서버는 Windows Server Essentials Experience 역할을 사용 하 여 Windows Server Essentials 운영 체제를 Windows Server 2012 R2 Standard 또는 Windows Server 2012 R2 Datacenter 운영 체제 실행 되어야 합니다.  
  
     Windows Server 2012 R2 Standard 또는 Windows Server 2012 R2 Datacenter 서버에서 BranchCache는 Windows Server Essentials Experience 역할을 추가할 때 추가 됩니다. BranchCache를 켜려면 도메인 관리자 자격 증명을 사용 하 여 Windows Server Essentials 대시보드에 로그인 해야 합니다.  
  
-   클라이언트 컴퓨터는 Windows 7 Enterprise, Windows 7 Ultimate, Windows 8 Enterprise 또는 Windows 8.1 Enterprise 운영 체제 실행 되어야 합니다.  
  
-   분산 캐시 모드에서는 모든 클라이언트 컴퓨터가 동일한 서브넷에 있어야 합니다.  
  
    > [!NOTE]
    >  도메인에 가입시키지 않고 클라이언트 컴퓨터를 Windows Server Essentials 서버에 연결한 경우 해당 컴퓨터는 기본적으로 캐싱에서 제외됩니다. 도메인에 가입되지 않은 클라이언트 컴퓨터를 캐싱에 포함하려면 클라이언트 컴퓨터에서 [Enable-BCDistributed](https://technet.microsoft.com/library/hh848398.aspx) Windows PowerShell cmdlet을 실행합니다. 자세한 내용은 [Windows PowerShell의 BranchCache Cmdlet](https://technet.microsoft.com/library/hh848392.aspx)을 참조하세요.  
 
  
## <a name="turn-branchcache-on"></a>BranchCache 켜기  
 분산된 캐시 모드로 BranchCache를 켜려면, 단순히 Windows Server Essentials 대시보드에서 단추를 클릭 합니다. 캐싱이 즉시 시작되고 투명하게 수행됩니다.  
  
#### <a name="to-turn-on-branchcache-in-windows-server-essentials"></a>Windows Server Essentials에서 BranchCache를 켜려면  
  
1.  관리자 계정으로 Windows Server Essentials 서버에 로그인 합니다.  
  
2.  Windows Server Essentials 대시보드를 클릭 **설정을**합니다.  
  
     설정 마법사가 열립니다.  
  
3.  **BranchCache**를 클릭합니다.  
  
4.  **BranchCache 설정** 페이지에서 **켜기**를 클릭합니다.  
  
## <a name="use-windows-powershell-to-turn-branchcache-on-or-off"></a>Windows PowerShell을 사용하여 BranchCache 켜기/끄기  
 Windows PowerShell을 사용하여 BranchCache의 상태(사용 또는 사용 안 함)를 확인하고 BranchCache를 켜거나 끌 수 있습니다.  
  
#### <a name="to-turn-branchcache-on-or-off-using-windows-powershell"></a>Windows PowerShell을 사용하여 BranchCache를 켜거나 끄려면  
  
1.  서버에서 관리자 권한으로 Windows PowerShell을 엽니다. **시작l** 페이지에서 **Windows PowerShell**을 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행**을 클릭한 다음 **예**를 클릭합니다.  
  
2.  명령 프롬프트에 다음 cmdlet 중 하나를 입력합니다.  
  
    -   BranchCache의 상태(사용 또는 사용 안 함)를 확인하려면 다음을 입력합니다.  
  
        ```powershell  
        Get-WSSBranchCacheStatus  
        ```  
  
    -   BranchCache를 켜려면 다음을 입력합니다.  
  
        ```powershell  
        Enable-WSSBranchCache  
        ```  
  
    -   BranchCache를 끄려면 다음을 입력합니다.  
  
        ```powershell  
        Disable-WSSBranchCache  
        ```  
  
## <a name="see-also"></a>참조  
    
-   [BranchCache 개요](https://technet.microsoft.com/library/hh831696.aspx)  
  
-   [Windows Server Essentials 관리](Manage-Windows-Server-Essentials.md)
