---
title: "Windows Server Essentials의 BranchCache 관리"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
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
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="manage-branchcache-in-windows-server-essentials"></a>Windows Server Essentials의 BranchCache 관리

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

BranchCache는 인터넷 사용을 최적화, 네트워크에 연결 된 응용 프로그램의 성능을 향상 하 고 교통 고 전체의 영역 (네트워크)에 때 저하 Windows Server Essentials 서버 위치한 원격 사무실에서 또는 클라이언트 컴퓨터 로컬 서버에 연결 되어 있을 때 SharePoint Online 라이브러리 등 클라우드 기반 리소스를 사용할 수 있습니다.  
  
 BranchCache 활성화를 사용 하는 클라이언트 컴퓨터 콘텐츠 원격 Windows Server Essentials 서버에서 콘텐츠를 요청 하는 경우 현지 사무실에 캐시 된 합니다. 그 후 같은 사무실에 있는 다른 컴퓨터 wan 다시 서버에서 콘텐츠를 다운로드 하는 대신 로컬 콘텐츠를 받을 수 있습니다. 네트워크에 연결 된 응용 프로그램 성능이 향상 하 고 wan 대역폭 사용량을 줄일 수 있습니다.  
  
 Windows Server Essentials 서버 로컬 또는 원격 인지 BranchCache 서버 공유 폴더 및 웹 콘텐츠를 호스트 (예: SharePoint Online 라이브러리) 서버에 응답 시간을 개선할 수 있습니다.  
  
 새 하드웨어 또는 네트워크 토폴로지 변경 BranchCache 필요 하지 않으므로,이 기능은 대역폭 사용을 최적화 하 고 서비스 및 wan 액세스 리소스에 대 한 응답 시간을 개선 하는 간단한 방법을 제공 합니다.  
  
## <a name="branchcache-scenarios"></a>BranchCache 시나리오  
 원격 서버 BranchCache 사용 되는 세 가지 기본 시나리오는 다음과 같습니다.  
  
-   Microsoft Azure에서 Windows Server Essentials 서버 호스트 됩니다.  
  
-   Windows Server Essentials 서버 제 3 자 서비스 제공자의 데이터 센터에 호스트 합니다.  
  
-   Windows Server Essentials 서버 실제 다른 위치에서 다른 office입니다.  
  
## <a name="distributed-cache-mode"></a>분산된 캐시 모드  
 Windows Server Essentials BranchCache를 구현 *분산된 캐시 모드*, 중 한 캐시 모드 BranchCache에서 사용할 수 있습니다. 분산된 캐시 모드에서는 콘텐츠 캐시 지점에 컴퓨터 분산 됩니다. 토폴로지 변경 없거나 추가 하드웨어가 필요 하므로 소규모 사무실 원격 서버를 사용 하거나 SharePoint Online 등 클라우드 기반 서비스에 액세스할 수 로컬 서버를 사용 하는 데이 모드가 작동 합니다. Windows Server Essentials의 BranchCache을 활성화 하면 캐시 분산된 모드 구현 됩니다.  
  
> [!NOTE]
>  네트워크에 연결 된 응용 프로그램을 사용 하 여 직원 많은 또는 여러 개 서브넷와 큰 지점에서는에 BranchCache 구현 하는 것이 좋습니다 수 *캐시 모드 호스트*합니다. 호스트 캐시 모드로 콘텐츠 캐시 지점에서 하나 이상의 호스트 캐시 서버에 저장 됩니다.
  
## <a name="requirements"></a>요구 사항  
 Windows Server Essentials의 BranchCache를 사용 하 여 서버와 클라이언트 컴퓨터 다음 요구 사항을 충족 해야 합니다.  
  
-   서버는 Windows Server Essentials 경험 역할와 Windows Server Essentials 운영 체제 Windows Server 2012 r 2 표준 또는 Windows Server 2012 R2 Datacenter 운영 체제 실행 되어야 합니다.  
  
     Windows Server 2012 r 2 표준 또는 Windows Server 2012 R2 Datacenter server에서 Windows Server Essentials 경험 역할을 추가 하면 BranchCache 추가 됩니다. BranchCache를 켜려면 Windows Server Essentials 대시보드 도메인 관리자 자격 증명으로 로그인 해야 합니다.  
  
-   Windows 7 Enterprise, Windows 7 Ultimate, Windows 8 Enterprise, 또는 Windows 8.1 Enterprise 운영 체제 클라이언트 컴퓨터 실행 해야 합니다.  
  
-   분산된 캐시 모드 모든 클라이언트 컴퓨터 같은 서브넷 켜져 있어야 합니다.  
  
    > [!NOTE]
    >  도메인에 가입 하지 않고 컴퓨터 Windows Server Essentials 서버에 연결 하는 컴퓨터에서 기본적으로 캐싱 제외 됩니다. 도메인에 가입 하지는 하는 클라이언트 컴퓨터 캐싱에 포함할을 실행 하는 [활성화 BCDistributed](https://technet.microsoft.com/library/hh848398.aspx) 클라이언트 컴퓨터에서 Windows PowerShell cmdlet 합니다. 자세한 내용은 참조 [에서 Windows PowerShell Cmdlet BranchCache](https://technet.microsoft.com/library/hh848392.aspx)합니다.  
 
  
## <a name="turn-branchcache-on"></a>BranchCache 켜기  
 BranchCache 분산된 캐시 모드에서를 켜려면 하기만 하면 Windows Server Essentials 대시보드에서 단추를 클릭 합니다. 캐시 바로 시작 되 고 투명 하 게 수행 됩니다.  
  
#### <a name="to-turn-on-branchcache-in-windows-server-essentials"></a>Windows Server Essentials의 BranchCache을 켜려면  
  
1.  관리자 계정 사용 하 여 Windows Server Essentials 서버에 로그인 합니다.  
  
2.  Windows Server Essentials 대시보드에서 클릭 **설정**합니다.  
  
     설정이 열립니다.  
  
3.  클릭 **BranchCache**합니다.  
  
4.  에 **BranchCache 설정** 페이지, 클릭 **켜기**합니다.  
  
## <a name="use-windows-powershell-to-turn-branchcache-on-or-off"></a>Windows PowerShell를 사용 하 여 BranchCache 켜기 또는 끄기  
 Windows PowerShell BranchCache (사용 또는 사용 안 함)의 상태를 확인 하 고 BranchCache 켜기 또는 끄기 사용할 수 있습니다.  
  
#### <a name="to-turn-branchcache-on-or-off-using-windows-powershell"></a>켜거나 BranchCache Windows PowerShell 사용 하려면  
  
1.  서버에서 Windows PowerShell을 관리자 권한으로 엽니다. 에 **시작** 페이지에서 마우스 오른쪽 단추로 클릭 **Windows PowerShell**, 클릭 **관리자 권한으로 실행**을 차례로 클릭 하 고 **예**합니다.  
  
2.  명령 프롬프트에서 다음 cmdlet 중 하나를 입력 합니다.  
  
    -   (사용 또는 사용 안 함) BranchCache의 상태를 확인 하려면 다음을 입력 합니다.  
  
        ```powershell  
        Get-WSSBranchCacheStatus  
        ```  
  
    -   BranchCache를 켜려면 입력 합니다.  
  
        ```powershell  
        Enable-WSSBranchCache  
        ```  
  
    -   BranchCache을 끄려면 다음을 입력 합니다.  
  
        ```powershell  
        Disable-WSSBranchCache  
        ```  
  
## <a name="see-also"></a>참조 하십시오  
    
-   [BranchCache 개요](https://technet.microsoft.com/library/hh831696.aspx)  
  
-   [Windows Server Essentials 관리](Manage-Windows-Server-Essentials.md)
