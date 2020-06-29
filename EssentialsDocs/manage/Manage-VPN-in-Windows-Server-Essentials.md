---
title: Windows Server Essentials에서 VPN 관리
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: cc2b264a-b9a8-4114-9f7b-8604f77096e5
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: ac6969522344165583bd21ac882fa7b4f6695145
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85470478"
---
# <a name="manage-vpn-in-windows-server-essentials"></a>Windows Server Essentials에서 VPN 관리

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

 VPN(가상 사설망) 연결을 사용하면 재택 근무자나 이동 중인 사용자가 인터넷과 같은 공용 네트워크에서 제공하는 인프라를 사용하여 개인 네트워크의 서버에 액세스할 수 있습니다. VPN을 사용하여 서버 리소스에 액세스하려면 다음을 완료해야 합니다.

-   [서버에서 원격 액세스에 VPN 사용](Manage-VPN-in-Windows-Server-Essentials.md#BKMK_1)

-   [네트워크 사용자에 대한 VPN 사용 권한 설정](Manage-VPN-in-Windows-Server-Essentials.md#BKMK_2)

-   [서버에 클라이언트 컴퓨터 연결](Manage-VPN-in-Windows-Server-Essentials.md#BKMK_Connect)

-   [VPN을 사용하여 Windows Server Essentials에 연결](Manage-VPN-in-Windows-Server-Essentials.md#BKMK_3)

##  <a name="enable-vpn-for-remote-access-on-the-server"></a><a name="BKMK_1"></a>서버에서 원격 액세스에 VPN 사용
 원격 액세스를 사용할 수 있도록 Windows Server Essentials에서 VPN을 구성하려면 다음 절차를 완료합니다.

#### <a name="to-enable-vpn-in-windows-server-essentials"></a>Windows Server Essentials에서 VPN을 사용하도록 설정하려면

1.  대시보드를 엽니다.

2.  **설정**을 클릭한 다음 **원격 액세스** 탭을 클릭합니다.

3.  **구성**을 클릭합니다. 원격 액세스 설정 마법사가 나타납니다.

4.  **사용할 원격 액세스 기능 선택** 페이지에서 **가상 사설망** 확인란을 선택합니다.

5.  지시에 따라 마법사를 완료합니다.

##  <a name="set-vpn-permissions-for-network-users"></a><a name="BKMK_2"></a>네트워크 사용자에 대 한 VPN 권한 설정
 VPN을 사용하여 Windows Server Essentials에 연결하고 서버에 저장된 모든 리소스에 액세스할 수 있습니다. 이 기능은 특히 VPN 연결을 통해 호스트된 Windows Server Essentials 서버에 연결하는 데 사용할 수 있는 네트워크 계정으로 설정되는 클라이언트 컴퓨터가 있는 경우 유용합니다. 호스트된 Windows Server Essentials 서버에서 새로 만든 모든 사용자 계정은 처음에 VPN을 사용하여 클라이언트 컴퓨터에 로그온해야 합니다.

#### <a name="to-set-vpn-permissions-for-network-users"></a>네트워크 사용자에 대한 VPN 사용 권한을 설정하려면

1.  대시보드를 엽니다.

2.  탐색 모음에서 **사용자**를 클릭합니다.

3.  사용자 계정 목록에서 데스크톱에 원격으로 액세스할 수 있는 사용 권한을 부여할 사용자 계정을 선택합니다.

4.  **사용자 계정 \> 작업<** 창에서 **속성**을 클릭 합니다.

5.  **<사용자 계정 \> 속성**에서 **원격 액세스** 탭을 클릭 합니다.

6.  **원격 액세스** 탭에서 사용자가 vpn을 사용 하 여 서버에 연결할 수 있게 하려면 **Vpn (가상 사설망) 허용** 확인란을 선택 합니다.

7.  **적용**, **확인**을 차례로 클릭합니다.

##  <a name="connect-client-computers-to-the-server"></a><a name="BKMK_Connect"></a>서버에 클라이언트 컴퓨터 연결
 Windows Server Essentials를 실행하는 서버에서 원격 액세스에 VPN을 사용하도록 설정하고 나면 VPN 연결을 사용하여 서버에 연결하고 서버에 저장된 모든 리소스에 액세스할 수 있습니다. 그러나 먼저 컴퓨터를 서버에 연결해야 합니다. 서버에 컴퓨터 연결 마법사를 사용하여 서버에 컴퓨터를 연결하면 클라이언트 컴퓨터에서 VPN 네트워크 연결이 자동으로 생성되며 재택 근무 또는 이동 중에 이 연결을 사용하여 서버 리소스에 액세스할 수 있습니다. 서버에 컴퓨터를 연결 하는 방법에 대 한 단계별 지침은 [서버에 컴퓨터 연결](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_9)을 참조 하세요.

##  <a name="use-vpn-to-connect-to-windows-server-essentials"></a><a name="BKMK_3"></a>VPN을 사용 하 여 Windows Server Essentials에 연결
 VPN 연결을 통해 Windows Server Essentials를 실행하는 호스트된 서버에 연결하는 데 사용할 수 있는 네트워크 계정으로 설정되는 클라이언트 컴퓨터가 있으면 호스트된 서버에서 새로 생성된 모든 사용자 계정은 클라이언트 컴퓨터에 처음 로그온할 때 VPN을 사용해야 합니다. 서버에 연결된 클라이언트 컴퓨터에서 다음 절차를 완료하세요.

#### <a name="to-use-vpn-to-remotely-access-server-resources"></a>VPN을 사용하여 서버 리소스에 원격으로 액세스하려면

1.  클라이언트 컴퓨터에서 Ctrl+Alt+Delete를 누릅니다.

2.  로그온 화면에서 **사용자 전환**을 클릭합니다.

3.  화면 오른쪽 아래에 있는 네트워크 로그온 아이콘을 클릭합니다.

4.  네트워크 사용자 이름 및 암호를 사용하여 Windows Server Essentials 네트워크에 로그온합니다.

## <a name="additional-references"></a>추가 참조

-   [원격으로 작업](../use/Work-Remotely-in-Windows-Server-Essentials.md)

-   [원격 액세스 관리](Manage-Anywhere-Access-in-Windows-Server-Essentials.md)

-   [Windows Server Essentials 관리](Manage-Windows-Server-Essentials.md)
