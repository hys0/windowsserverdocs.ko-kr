---
title: "Windows Server Essentials에서 VPN 관리"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cc2b264a-b9a8-4114-9f7b-8604f77096e5
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 08a08a13d696371420bdfdf89f54320c787636b0
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="manage-vpn-in-windows-server-essentials"></a>Windows Server Essentials에서 VPN 관리

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다. 
  
 (VPN) 가상 개인 네트워크 연결 집에서 또는 이동 중에 작업 수 있도록 인터넷 등 공용 네트워크에서 제공 하는 인프라를 사용 하 여 사설망 서버에 액세스 합니다. 서버 리소스에 액세스 하기 위해 VPN을 사용 하려면 다음을 완료 해야 합니다.  
  
-   [서버에 대 한 원격 액세스를 위해 VPN을 사용 하도록 설정](Manage-VPN-in-Windows-Server-Essentials.md#BKMK_1)  
  
-   [네트워크 사용자에 대 한 사용 권한을 VPN 설정](Manage-VPN-in-Windows-Server-Essentials.md#BKMK_2)  
  
-   [컴퓨터 클라이언트는 서버에 연결](Manage-VPN-in-Windows-Server-Essentials.md#BKMK_Connect)  
  
-   [VPN을 사용 하 여 Windows Server Essentials에 연결 하려면](Manage-VPN-in-Windows-Server-Essentials.md#BKMK_3)  
  
##  <a name="BKMK_1"></a>서버에 대 한 원격 액세스를 위해 VPN을 사용 하도록 설정  
 원격 액세스할 수 있도록 하려면 Windows Server Essentials의 VPN 구성 하려면 다음 단계를 수행 합니다.  
  
#### <a name="to-enable-vpn-in-windows-server-essentials"></a>Windows Server Essentials에서 VPN을 사용 하도록 설정 하려면  
  
1.  대시보드를 엽니다.  
  
2.  클릭 **설정**을 차례로 클릭 하 고 있는 **원하는 위치에 액세스** 탭 합니다.  
  
3.  클릭 **구성**합니다. 설정 어디서 나 액세스 마법사 나타납니다.  
  
4.  에 **선택 어디서 나 액세스 기능을 사용 하도록 설정** 페이지를 선택 하 고는 **가상 개인 네트워크** 확인란을 선택 합니다.  
  
5.  마법사를 완료 하 고 지침을 따릅니다.  
  
##  <a name="BKMK_2"></a>네트워크 사용자에 대 한 사용 권한을 VPN 설정  
 Windows Server Essentials에 연결 하는 서버에 저장 된 모든 리소스에 액세스 VPN을 사용할 수 있습니다. VPN 연결을 통해 호스팅된 Windows Server Essentials 서버에 연결 하는 데 사용 될 수 있는 네트워크 계정을 설정 하는 클라이언트 컴퓨터 하는 경우 특히 유용 합니다. 모든 새로 만든된 사용자 계정 여 호스팅된 Windows Server Essentials 서버에 처음으로 대 한 클라이언트 컴퓨터에 로그온 할 VPN을 사용 해야 합니다.  
  
#### <a name="to-set-vpn-permissions-for-network-users"></a>네트워크 사용자에 대 한 사용 권한을 VPN 설정 하려면  
  
1.  대시보드를 엽니다.  
  
2.  탐색 모음에서 클릭 **사용자**합니다.  
  
3.  사용자 계정의 목록에서 사용자 계정에 대 원격 데스크톱에 액세스할 권한을 부여 하려는 선택 합니다.  
  
4.  에 **< 사용자 Account\ > 작업** 창 클릭 **속성**합니다.  
  
5.  에 **< 사용자 Account\ > 속성**를 클릭는 **액세스 어디서 나** 탭 합니다.  
  
6.  에 **어디서 나 액세스** VPN을 사용 하 여 서버에 연결할 수 있도록 탭을 선택는 **허용 개인 VPN (가상)** 확인란을 선택 합니다.  
  
7.  클릭 **적용**을 차례로 클릭 하 고 **확인**합니다.  
  
##  <a name="BKMK_Connect"></a>컴퓨터 클라이언트는 서버에 연결  
 VPN을 원격 액세스를 위해 Windows Server Essentials 실행 하는 서버에 사용할 수 있으면에 연결 하 고 서버에 저장 된 모든 리소스에 액세스 VPN 연결을 사용할 수 있습니다. 하지만 먼저 컴퓨터 서버에 연결 해야 합니다. 서버 마법사 연결 내 컴퓨터를 사용 하 여 컴퓨터를 서버에 연결할 때 VPN 네트워크 연결 클라이언트 컴퓨터에 자동으로 생성 됩니다와 집에서 또는 이동 중에 작동 하는 동안 서버 리소스에 액세스 하는 데 사용 될 수 있습니다. 컴퓨터에 연결 하는 서버에 대 한 단계별 지침을 참조 하세요. [서버에 컴퓨터를 연결](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_9)합니다.  
  
##  <a name="BKMK_3"></a>VPN을 사용 하 여 Windows Server Essentials에 연결 하려면  
 모든 새로 만든된 사용자 계정 VPN 연결을 통해 Windows Server Essentials 실행 호스팅된 서버에 연결 하는 데 사용 될 수 있는 네트워크 계정을 설정 하는 클라이언트 컴퓨터 있는 경우 여 호스팅된 서버 처음에 대 한 클라이언트 컴퓨터에 로그온 할 VPN을 사용 해야 합니다. 서버에 연결 하는 클라이언트 컴퓨터에서 다음 단계를 수행 합니다.  
  
#### <a name="to-use-vpn-to-remotely-access-server-resources"></a>VPN를 사용 하 여 원격 서버 리소스에 액세스 하려면  
  
1.  키를 눌러 Ctrl + Alt + Delete 클라이언트 컴퓨터에서 합니다.  
  
2.  클릭 **사용자 전환** 로그인 화면에서 합니다.  
  
3.  화면의 오른쪽 아래 모서리에서 네트워크 로그온 아이콘을 클릭 합니다.  
  
4.  Windows Server Essentials 네트워크 네트워크 사용자 이름 및 암호를 사용 하 여 로그온 합니다.  
  
## <a name="see-also"></a>참조 하십시오  
  
-   [원격 작업](../use/Work-Remotely-in-Windows-Server-Essentials.md)  
  
-   [액세스를 어디서 나 관리](Manage-Anywhere-Access-in-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials 관리](Manage-Windows-Server-Essentials.md)
