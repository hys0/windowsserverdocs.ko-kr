---
title: 새 Windows Server Essentials에서 원본 서버 수준 내리기 및 제거
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: d9f18b29-8e03-439e-bdf0-1dac5e4f70c5
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 50d5265b4059629082b4c7ef74b0186b5d4277e7
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80852606"
---
# <a name="demote-and-remove-the-source-server-from-the-new-windows-server-essentials-network1"></a>새 Windows Server Essentials에서 원본 서버 수준 내리기 및 제거

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Windows Server Essentials 설치를 완료 하 고 마이그레이션 마법사의 작업을 완료 한 후에는 다음 작업을 수행 해야 합니다.  
  

1.  [Exchange Server 2003를 제거](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_UninstallExchangeServer2003)합니다.  
  
2.  [원본 서버에 직접 연결된 프린터 연결 끊기](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_PhysicallyDisconnect).  
  
3.  [원본 서버 수준 내리기](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_DemoteTheSourceServer).  
  
4.  [원본 서버에서 라우터로 DHCP 서버 역할을 이동](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_MoveTheDHCPRole)합니다.  
  
5.  [원본 서버 제거 및 용도 변경](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_RemoveTheSourceServer).  

1.  [Exchange Server 2003를 제거](../migrate/Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_UninstallExchangeServer2003)합니다.  
  
2.  [원본 서버에 직접 연결된 프린터 연결 끊기](../migrate/Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_PhysicallyDisconnect).  
  
3.  [원본 서버 수준 내리기](../migrate/Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_DemoteTheSourceServer).  
  
4.  [원본 서버에서 라우터로 DHCP 서버 역할을 이동](../migrate/Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_MoveTheDHCPRole)합니다.  
  
5.  [원본 서버 제거 및 용도 변경](../migrate/Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_RemoveTheSourceServer).  

  
###  <a name="uninstall-exchange-server-2003"></a><a name="BKMK_UninstallExchangeServer2003"></a>Exchange Server 2003 제거  
  
> [!IMPORTANT]
>  사서함을 대상 서버로 이동 하 고 원본 서버에서 Exchange Server 2003을 제거 하기 전에 사용자 계정을 추가 하면 해당 사서함이 원본 서버에 추가 됩니다. 이것은 정상적인 현상입니다. 이 시간 동안 추가된 모든 사용자 계정에 대해 사서함을 대상 서버로 이동해야 합니다. Exchange Server 2003을 제거 하기 전에 Windows Server Essentials 마이그레이션에 대 한 Exchange Server 사서함 및 설정 이동의 지침을 반복 합니다.  
  
 수준을 내리기 전에 원본 서버에서 Exchange Server 2003을 제거 해야 합니다. 그러면 Active Directory Domain Services (AD DS)에서 원본 서버의 Exchange Server에 대 한 모든 참조가 제거 됩니다. Exchange Server 2003를 제거 하려면 Windows Small Business Server 2003 미디어가 있어야 합니다.  
  
##### <a name="to-uninstall-exchange-server-2003-from-the-source-server"></a>원본 서버에서 Exchange Server 2003를 제거 하려면  
  
1. 관리자로 원본 서버에 로그온합니다.  
  
2. **시작**, **제어판**, **프로그램 추가/제거**를 차례로 클릭합니다.  
  
3. 프로그램 목록에서 **Windows Small Business Server 2003**을 선택한 다음 **변경/제거**를 클릭 합니다.  
  
4. 설치 마법사에서 **구성 요소 선택** 페이지가 나타날 때까지 **다음**을 클릭합니다.  
  
5. 구성 요소 선택 페이지에서 **Exchange Server**를 확장하고 **제거**를 선택합니다.  
  
   > [!NOTE]
   > 
   >  Exchange Server에서는 서버에 사서함 또는 공용 폴더가 없는지 확인합니다. 데이터가 남아 있으면 **제거**를 클릭할 때 오류 메시지가 나타납니다. 이 문제를 방지 하려면 항목의 모든 절차를 완료 했는지 확인 하세요. [SBS 2003 설정 및 데이터를 대상 서버로 이동](Move-Windows-SBS-2003-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md)합니다.  
   > 
   >  Exchange Server에서는 서버에 사서함 또는 공용 폴더가 없는지 확인합니다. 데이터가 남아 있으면 **제거**를 클릭할 때 오류 메시지가 나타납니다. 이 문제를 방지 하려면 항목의 모든 절차를 완료 했는지 확인 하세요. [SBS 2003 설정 및 데이터를 대상 서버로 이동](../migrate/Move-Windows-SBS-2003-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md)합니다.  

  
6. **다음**을 클릭합니다.  
  
7. 메시지가 표시 되 면 Windows Small Business Server 2003 CD # 3을 삽입 하 고 화면의 지침을 따릅니다.  
  
###  <a name="disconnect-printers-that-are-directly-connected-to-the-source-server"></a><a name="BKMK_PhysicallyDisconnect"></a>원본 서버에 직접 연결 된 프린터 연결 끊기  
 원본 서버에서 수준을 내리기 전에 원본 서버에 직접 연결되거나 원본 서버를 통해 공유되는 모든 프린터의 연결을 실제로 끊습니다. 원본 서버에 직접 연결된 프린터에 대한 Active Directory 개체가 남아 있는지 확인합니다. 그런 다음 프린터를 대상 서버에 직접 연결 하 고 Windows Server Essentials에서 공유할 수 있습니다.  
  
###  <a name="demote-the-source-server"></a><a name="BKMK_DemoteTheSourceServer"></a>원본 서버 수준 내리기  
 AD DS 도메인 컨트롤러 역할에서 도메인 구성원 서버 역할로 원본 서버의 수준을 내리기 전에 다음 절차에 설명된 대로 그룹 정책 설정이 모든 클라이언트 컴퓨터에 적용되는지 확인합니다.  
  
> [!IMPORTANT]
>  클라이언트 컴퓨터에서 그룹 정책 변경 내용을 업데이트하는 동안 원본 서버와 대상 서버가 네트워크에 연결되어야 합니다.  
  
##### <a name="to-force-a-group-policy-update-on-a-client-computer"></a>클라이언트 컴퓨터에서 그룹 정책 업데이트를 강제로 적용하려면  
  
1.  관리자로 클라이언트 컴퓨터에 로그온합니다.  
  
2.  관리자 권한으로 명령 프롬프트를 엽니다.  
  
3.  명령 프롬프트에 **gpupdate /force**를 입력하고 Enter 키를 누릅니다.  
  
4.  프로세스를 완료하려면 로그오프한 후 다시 로그온해야 합니다. **예**를 클릭하여 확인합니다.  
  
##### <a name="to-demote-the-source-server"></a>원본 서버 수준을 내리려면  
  
1. 원본 서버에서 **시작**, **실행**을 차례로 클릭하고 **dcpromo**를 입력하고 나서 **확인**을 클릭합니다.  
  
2. **다음**을 두 번 클릭합니다.  
  
   > [!NOTE]
   >  **이 서버가 도메인의 마지막 도메인 컨트롤러입니다.** 를 선택하지 않습니다.  
  
3. 서버에서 새 관리자 계정의 암호를 입력하고 **다음**을 클릭합니다.  
  
4. **요약** 대화 상자에 AD DS 컴퓨터에서 제거 되 고 서버가 도메인의 구성원이 될 것 이라는 알림이 표시 됩니다. **다음**을 클릭합니다.  
  
5. **마침**을 클릭합니다. 원본 서버가 다시 시작됩니다.  
  
6. 원본 서버가 다시 시작되고 나면 네트워크에서 연결을 끊기 전에 원본 서버를 작업 그룹의 구성원으로 추가합니다.  
  
   원본 서버를 작업 그룹의 구성원으로 추가하고 네트워크에서 연결을 끊고 나서 대상 서버의 AD DS에서 원본 서버를 제거해야 합니다.  
  
##### <a name="to-remove-the-source-server-from-active-directory"></a>Active Directory에서 원본 서버를 제거하려면  
  
1.  대상 서버에서 **Active Directory 사용자 및 컴퓨터**를 엽니다.  
  
2.  **Active Directory 사용자 및 컴퓨터** 탐색 창에서 도메인 이름을 확장하고 **컴퓨터**를 확장합니다.  
  
3.  원본 서버 이름이 서버 목록에 있으면 원본 서버 이름을 마우스 오른쪽 단추로 클릭하고 **삭제**, **예**를 차례로 클릭합니다.  
  
4.  원본 서버가 목록에 없는지 확인하고 **Active Directory 사용자 및 컴퓨터**를 닫습니다.  
  
###  <a name="move-the-dhcp-server-role-from-the-source-server-to-the-router"></a><a name="BKMK_MoveTheDHCPRole"></a>원본 서버에서 라우터로 DHCP 서버 역할 이동  
  
> [!NOTE]
> 
>  마이그레이션 프로세스를 시작하기 전에 이미 이 작업을 수행했으면 [원본 서버 제거 및 용도 변경](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_RemoveTheSourceServer) 섹션을 계속 진행합니다.  
> 
>  마이그레이션 프로세스를 시작하기 전에 이미 이 작업을 수행했으면 [원본 서버 제거 및 용도 변경](../migrate/Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_RemoveTheSourceServer) 섹션을 계속 진행합니다.  

  
 원본 서버에서 DHCP 역할을 실행하고 있으면 다음 단계를 수행하여 DHCP 역할을 라우터로 이동합니다.  
  
##### <a name="to-move-the-dhcp-role-from-the-source-server-to-the-router"></a>원본 서버에서 라우터로 DHCP 역할을 이동하려면  
  
1.  다음과 같이 원본 서버에서 DHCP 서비스를 끕니다.  
  
    1.  원본 서버에서 **시작**, **관리 도구**, **서비스**를 차례로 클릭합니다.  
  
    2.  현재 실행 중인 서비스 목록에서 **Windows Server**를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.  
  
    3.  **시작 유형**으로 **사용 안 함**을 선택합니다.  
  
    4.  서비스를 중지합니다.  
  
2.  라우터에서 DHCP 역할을 켭니다.  
  
    1.  라우터 설명서의 지침에 따라 라우터에서 DHCP 역할을 켭니다.  
  
    2.  원본 서버에서 발급된 IP 주소를 동일하게 유지하려면 라우터 설명서의 지침에 따라 라우터의 DHCP 범위를 원본 서버의 DHCP 범위와 동일하게 구성합니다.  
  
    > [!IMPORTANT]
    >  대상 서버에 대한 라우터에서 고정 IP 또는 DHCP 예약을 설정하지 않았고 DHCP 범위가 원본 서버와 다르면 라우터에서 대상 서버에 대한 새 IP 주소를 발급할 수 있습니다. 이 문제가 발생하면 라우터의 대상 서버의 새 IP 주소를 전달하도록 포트 전달 규칙을 다시 설정합니다.  
  
###  <a name="remove-and-repurpose-the-source-server"></a><a name="BKMK_RemoveTheSourceServer"></a>원본 서버 제거 및 용도 변경  
 원본 서버를 끄고 네트워크에서 연결을 끊습니다. 필요한 모든 데이터가 대상 서버로 마이그레이션되도록 최소한 한 주 동안 원본 서버를 다시 포맷하지 않는 것이 좋습니다. 모든 데이터가 마이그레이션되었는지 확인하고 나서 필요하면 다른 작업에 대한 보조 서버로 이 서버를 네트워크에 다시 설치할 수 있습니다.  
  
> [!NOTE]
>  원본 서버의 수준을 내리고 원본 서버를 제거하고 나서 대상 서버를 다시 시작합니다.  
  
 원본 서버의 수준을 내리고 나면 서버는 정상 상태가 아닙니다. 원본 서버의 용도를 변경하려는 경우 가장 간단한 방법은 원본 서버를 다시 포맷하고 서버 운영 체제를 설치한 다음 추가 서버로 사용하도록 설정하는 것입니다.
