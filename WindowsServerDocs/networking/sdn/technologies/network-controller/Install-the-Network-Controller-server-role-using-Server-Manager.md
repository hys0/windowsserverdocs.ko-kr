---
title: 네트워크 컨트롤러 서버 역할 서버 관리자를 사용 하 여 설치
description: 이 항목의 Windows Server 2016 서버 관리자를 사용 하 여 네트워크 컨트롤러 서버 역할을 설치 하는 방법에 대해 설명 합니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 3a6e4352-ff62-4290-b8a4-5c83740070fc
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 15cb1ef3bad7038cc97784504807b44b4920def6
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="install-the-network-controller-server-role-using-server-manager"></a>네트워크 컨트롤러 서버 역할 서버 관리자를 사용 하 여 설치

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 항목 네트워크 컨트롤러 서버 역할 서버 관리자를 사용 하 여 설치 하는 방법에 대해 설명 합니다.

>[!IMPORTANT]
>네트워크 컨트롤러 서버 역할 실제 호스트에서를 배포 하지 않습니다. Hyper-v 가상 컴퓨터가에 네트워크 컨트롤러 서버 역할 설치 해야 하는 배포 하는 네트워크 컨트롤러, Hyper-v 호스트에 설치 되어 있는 \(VM\) 합니다. 네트워크 컨트롤러 Vm에서 세 가지 Hyper\ V 호스트에서를 설치한 후 Windows PowerShell 명령을 사용 하 여 네트워크 컨트롤러 호스트 추가 하 여 소프트웨어 네트워킹 정의 \(SDN\)에 대해 Hyper\ V 호스트를 설정 해야 **새로 NetworkControllerServer**합니다. 이렇게 하면 SDN 소프트웨어 부하 분산 기능을 사용할 수 있게 됩니다. 자세한 내용은 참조 [새로 NetworkControllerServer](https://technet.microsoft.com/itpro/powershell/windows/network-controller/new-networkcontrollerserver)합니다.
  
네트워크 컨트롤러를 설치한 후 네트워크 컨트롤러 추가 구성에 대 한 Windows PowerShell 명령을 사용 해야 합니다. 자세한 내용은 참조 [Windows PowerShell를 사용 하 여 네트워크 컨트롤러 배포](../../deploy/Deploy-Network-Controller-using-Windows-PowerShell.md)합니다.  
  
### <a name="to-install-network-controller"></a>네트워크 컨트롤러를 설치 하려면  
  
1.  서버 관리자 클릭 **관리**을 차례로 클릭 하 고 **역할 추가 및 기능**합니다. 기능 및 역할 추가 마법사가 열립니다. 클릭 **다음**합니다.  
  
2.  **설치 유형을 선택**기본 설정을 유지 하 고 클릭 **다음**합니다.  
  
3.  **대상 서버 선택**, 네트워크 컨트롤러, 설치를 클릭 한 다음 원하는 서버 선택 **다음**합니다.  
  
4.  **서버 역할 선택**에 **역할**, 클릭 **네트워크 컨트롤러**합니다.  
  
    ![네트워크 컨트롤러 서버 역할](../../../media/Install-the-Network-Controller-server-role-using-Server-Manager/netc_install_07.jpg)  
  
5.  **네트워크 컨트롤러에 필요한 기능을 추가** 대화 상자를 엽니다. 클릭 **기능을 추가**합니다.  
  
    ![네트워크 컨트롤러에 대 한 기능을 추가 합니다.](../../../media/Install-the-Network-Controller-server-role-using-Server-Manager/netc_install_06.jpg)  
  
6.  **서버 역할 선택**, 클릭 **다음**합니다.  
  
    ![클릭](../../../media/Install-the-Network-Controller-server-role-using-Server-Manager/netc_install_07.jpg)  
  
7.  **기능 선택**, 클릭 **다음**합니다.  
  
8.  **네트워크 컨트롤러** 클릭 **다음**합니다.  
  
9. **설치 선택을 확인**, 선택 내용을 검토 합니다. 네트워크 컨트롤러 설치 마법사가 실행 되 면 컴퓨터를 다시 시작 하면 해야 합니다. 이 인해 클릭 **필요한 경우 자동으로 목적지 서버를 다시 시작**합니다. **역할 추가 및 기능 마법사** 대화 상자를 엽니다. 클릭 **예**합니다.  
  
    ![역할 및 기능 마법사 추가](../../../media/Install-the-Network-Controller-server-role-using-Server-Manager/netc_install_11.jpg)  
  
10. **설치 선택을 확인**, 클릭 **설치**합니다.  
  
11. 네트워크 컨트롤러 서버 역할 대상 서버에 설치 하 고 서버를 다시 시작한 다음 합니다.  
  
12. 컴퓨터를 다시 시작한 후에 컴퓨터에 로그온 하 고 서버 관리자 확인 하 여 네트워크 컨트롤러 설치를 확인 합니다.  
  
    ![서버 관리자](../../../media/Install-the-Network-Controller-server-role-using-Server-Manager/nc_013.jpg)  
  
## <a name="see-also"></a>참조 하십시오  
[네트워크 컨트롤러](Network-Controller.md)  
  


