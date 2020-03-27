---
title: 서버 관리자를 사용 하 여 네트워크 컨트롤러 서버 역할 설치
description: 이 항목에서는 Windows Server 2016에서 서버 관리자를 사용 하 여 네트워크 컨트롤러 서버 역할을 설치 하는 방법에 대 한 지침을 제공 합니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 3a6e4352-ff62-4290-b8a4-5c83740070fc
ms.author: lizross
author: eross-msft
ms.openlocfilehash: b8a3e1ede1cdec1ca5ee66be8d53d4420bec673b
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80317131"
---
# <a name="install-the-network-controller-server-role-using-server-manager"></a>서버 관리자를 사용 하 여 네트워크 컨트롤러 서버 역할 설치

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목에서는 서버 관리자를 사용 하 여 네트워크 컨트롤러 서버 역할을 설치 하는 방법에 지침을 제공 합니다.

>[!IMPORTANT]
>실제 호스트에 네트워크 컨트롤러 서버 역할을 배포 하지 마십시오. 네트워크 컨트롤러를 배포 하려면 hyper-v 호스트에 설치 된 VM\) \(Hyper-v 가상 컴퓨터에 네트워크 컨트롤러 서버 역할을 설치 해야 합니다. 3 개의 서로 다른\-Hyper-v 호스트에 Vm에 네트워크 컨트롤러를 설치한 후 Windows PowerShell 명령 **NetworkControllerServer**를 사용 하 여 네트워크 컨트롤러에 호스트를 추가 하 여 소프트웨어 정의 네트워킹 \(SDN\)에 대 한 하이퍼\-V 호스트를 사용 하도록 설정 해야 합니다. 이렇게 하면 SDN 소프트웨어 Load Balancer 기능을 사용할 수 있습니다. 자세한 내용은 [NetworkControllerServer](https://technet.microsoft.com/itpro/powershell/windows/network-controller/new-networkcontrollerserver)를 참조 하세요.
  
네트워크 컨트롤러를 설치한 후 추가 네트워크 컨트롤러 구성에 대 한 Windows PowerShell 명령을 사용 해야 합니다. 자세한 내용은 참조 [Windows PowerShell을 사용 하 여 네트워크 컨트롤러 배포](../../deploy/Deploy-Network-Controller-using-Windows-PowerShell.md)합니다.  
  
### <a name="to-install-network-controller"></a>네트워크 컨트롤러를 설치 하려면  
  
1.  서버 관리자에서 **관리**, **역할 및 기능 추가**를 차례로 클릭합니다. 역할 및 기능 추가 마법사가 열립니다. **다음**을 클릭합니다.  
  
2.  **설치 유형 선택**, 기본 설정을 유지 하 고 클릭 **다음**합니다.  
  
3.  **대상 서버 선택**, 를 클릭 하 고 네트워크 컨트롤러를 설치 하려는 서버를 선택 **다음**합니다.  
  
4.  **서버 역할 선택**,  **역할**, 클릭 **네트워크 컨트롤러**합니다.  
  
    ![네트워크 컨트롤러 서버 역할](../../../media/Install-the-Network-Controller-server-role-using-Server-Manager/netc_install_07.jpg)  
  
5.  **네트워크 컨트롤러에 필요한 기능 추가** 대화 상자가 열립니다. **기능 추가**를 클릭합니다.  
  
    ![네트워크 컨트롤러에 대 한 기능을 추가 합니다.](../../../media/Install-the-Network-Controller-server-role-using-Server-Manager/netc_install_06.jpg)  
  
6.  **서버 역할 선택**, 클릭 **다음**합니다.  
  
    ![다음을 클릭합니다.](../../../media/Install-the-Network-Controller-server-role-using-Server-Manager/netc_install_07.jpg)  
  
7.  **기능 선택**, 클릭 **다음**합니다.  
  
8.  **네트워크 컨트롤러** 클릭 **다음**합니다.  
  
9. **설치 선택 확인**, 선택 내용을 검토 합니다. 네트워크 컨트롤러 설치 마법사를 실행 하는 컴퓨터를 다시 시작 해야 필요 합니다. 이 때문에 클릭 **필요한 경우 자동으로 대상 서버를 다시 시작**합니다. **역할 및 추가 기능 마법사** 대화 상자가 열립니다. **예**를 클릭합니다.  
  
    ![역할 및 기능 추가 마법사](../../../media/Install-the-Network-Controller-server-role-using-Server-Manager/netc_install_11.jpg)  
  
10. **설치 선택 확인**에서 **설치**를 클릭합니다.  
  
11. 대상 서버의 네트워크 컨트롤러 서버 역할 설치 하 고 서버를 다시 시작한 다음 키를 누릅니다.  
  
12. 컴퓨터를 다시 시작한 후 컴퓨터에 로그온 하 고 서버 관리자를 확인 하 여 네트워크 컨트롤러 설치를 확인 합니다.  
  
    ![서버 관리자](../../../media/Install-the-Network-Controller-server-role-using-Server-Manager/nc_013.jpg)  
  
## <a name="see-also"></a>관련 항목  
[네트워크 컨트롤러](Network-Controller.md)  
  


