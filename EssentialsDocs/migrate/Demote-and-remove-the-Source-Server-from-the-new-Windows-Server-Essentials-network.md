---
title: "내리기 하 고 원본 서버 새로운 Windows Server Essentials 네트워크 1에서 제거"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d9f18b29-8e03-439e-bdf0-1dac5e4f70c5
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 1545189732194ad5c0aba401f834b0102799e016
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="demote-and-remove-the-source-server-from-the-new-windows-server-essentials-network1"></a>내리기 하 고 원본 서버 새로운 Windows Server Essentials 네트워크 1에서 제거

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

Windows Server Essentials를 설치를 완료 한 후 마이그레이션 마법사의 작업을 완료 하면 다음과 같은 작업을 수행 해야 합니다.  
  

1.  [Exchange Server 2003 제거](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_UninstallExchangeServer2003)합니다.  
  
2.  [연결 끊기 소스 서버에 직접 연결 된 프린터는](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_PhysicallyDisconnect)합니다.  
  
3.  [원본 서버 내리기](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_DemoteTheSourceServer)합니다.  
  
4.  [원본 서버에서 라우터에서 DHCP 서버 역할 이동](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_MoveTheDHCPRole)합니다.  
  
5.  [제거 하 고 원본 서버 재활용](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_RemoveTheSourceServer)합니다.  

1.  [Exchange Server 2003 제거](../migrate/Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_UninstallExchangeServer2003)합니다.  
  
2.  [연결 끊기 소스 서버에 직접 연결 된 프린터는](../migrate/Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_PhysicallyDisconnect)합니다.  
  
3.  [원본 서버 내리기](../migrate/Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_DemoteTheSourceServer)합니다.  
  
4.  [원본 서버에서 라우터에서 DHCP 서버 역할 이동](../migrate/Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_MoveTheDHCPRole)합니다.  
  
5.  [제거 하 고 원본 서버 재활용](../migrate/Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_RemoveTheSourceServer)합니다.  

  
###  <a name="BKMK_UninstallExchangeServer2003"></a>Exchange Server 2003 제거  
  
> [!IMPORTANT]
>  대상 서버에 및 Exchange Server 2003 원본 서버에서 제거 하기 전에 사서함 이동한 후 사용자 계정이 추가한 사서함 원본 서버에 추가 됩니다. 의도 된입니다. 이 기간 동안 추가 하는 모든 사용자 계정에 대해 대상 서버로 사서함 이동 해야 합니다. Exchange Server 2003 제거 하기 전에 Windows Server Essentials 마이그레이션에 대 한 지침 Exchange Server 이동 사서함 및 설정에를 반복 합니다.  
  
 Exchange Server 2003 내리기 하기 전에 원본 서버에서 제거 해야 합니다. Active Directory Domain Services (AD DS)를 Exchange Server 원본 서버에 대 한 언급을 모두 제거합니다. Exchange Server 2003 제거 하 여 Windows Small Business Server 2003 미디어 있어야 합니다.  
  
##### <a name="to-uninstall-exchange-server-2003-from-the-source-server"></a>Exchange Server 2003 원본 서버에서 제거 하려면  
  
1.  관리자 권한으로 로그온 소스 서버에  
  
2.  클릭 **시작**, 클릭 **제어판**을 차례로 클릭 하 고 **프로그램 추가 / 제거**합니다.  
  
3.  프로그램 목록에서 선택 **Windows Small Business Server 2003**을 차례로 클릭 하 고 **제거/변경**합니다.  
  
4.  설치 마법사에서 클릭 **다음** 될 때까지 **구성 요소 선택** 페이지가 나타납니다.  
  
5.  구성 요소 선택 페이지 확장 **Exchange Server**를 선택한 다음 **제거**합니다.  
  
    > [!NOTE]

    >  Exchange Server 없는 사서함 또는 서버에 공용 폴더는 있는지 확인 합니다. 클릭할 때 오류 메시지가 나타납니다 데이터가 유지 되 면 **제거**합니다. 이 문제를 방지 하 않도록 항목의 절차 모두 완료 했으면 [SBS 2003 이동 설정과 대상 서버에 데이터를](Move-Windows-SBS-2003-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md)합니다.  

    >  Exchange Server 없는 사서함 또는 서버에 공용 폴더는 있는지 확인 합니다. 클릭할 때 오류 메시지가 나타납니다 데이터가 유지 되 면 **제거**합니다. 이 문제를 방지 하 않도록 항목의 절차 모두 완료 했으면 [SBS 2003 이동 설정과 대상 서버에 데이터를](../migrate/Move-Windows-SBS-2003-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md)합니다.  

  
6.  클릭 **다음**합니다.  
  
7.  메시지가 표시 되 면 Windows 작은 Business Server 2003 CD # 3를 넣고 화면의 지시에 따릅니다.  
  
###  <a name="BKMK_PhysicallyDisconnect"></a>원본 서버에 직접 연결 된 프린터에 연결 끊기  
 원본 서버, 내릴 전에 실제로 원본 서버에 직접 연결 되어 있고 원본 서버를 통해 공유 되는 프린터를 분리 합니다. 원본 서버에 직접 연결 된 프린터에 대 한 Active Directory 개체 없는 유지 하는 확인 합니다. 프린터 다음 수 직접 대상 서버에 연결 되어 있고 Windows Server Essentials의 공유 합니다.  
  
###  <a name="BKMK_DemoteTheSourceServer"></a>원본 서버 내리기  
 AD DS 도메인 컨트롤러 역할 소스 서버의 도메인 구성원 서버 역할을 내릴 하기 전에 다음 절차에 설명 된 대로 그룹 정책 설정을 모든 클라이언트 컴퓨터에 적용 되는지 확인 합니다.  
  
> [!IMPORTANT]
>  원본 서버와 대상 서버 동안 그룹 정책 업데이트 되는 클라이언트 컴퓨터에는 네트워크에 연결 합니다.  
  
##### <a name="to-force-a-group-policy-update-on-a-client-computer"></a>그룹 정책 업데이트는 클라이언트 컴퓨터에서 강제로  
  
1.  클라이언트 컴퓨터에서 관리자 권한으로 로그온 합니다.  
  
2.  관리자 권한으로 명령 프롬프트 창을 엽니다.  
  
3.  명령 프롬프트에 입력 **gpupdate /force**, ENTER 키를 누릅니다.  
  
4.  프로세스를 완료 하려면 다시 로그인 및 로그 오프 해야 할 수 있습니다. 클릭 **예** 하 여 확인 합니다.  
  
##### <a name="to-demote-the-source-server"></a>원본 서버를  
  
1.  원본 서버에서 **시작**, 클릭 **실행**, 입력 **dcpromo**을 차례로 클릭 하 고 **확인**합니다.  
  
2.  클릭 **다음** 두 번 합니다.  
  
    > [!NOTE]
    >  선택 하지 않으면 **이 서버가 도메인에 있는 마지막 도메인 컨트롤러**합니다.  
  
3.  서버에서 새 관리자 계정에 대 한 암호를 입력 한 다음 **다음**합니다.  
  
4.  에 **요약** 대화 상자에서 AD DS은 컴퓨터에서 제거 될 및 서버는 도메인의 회원 수 있는지 알려줍니다. 클릭 **다음**합니다.  
  
5.  클릭 **완료**합니다. 원본 서버를 다시 시작 해야 합니다.  
  
6.  원본 서버를 다시 시작한 후에 네트워크에서 분리 하기 전에 원본 서버 작업 그룹의 회원으로 추가 합니다.  
  
 원본 서버 작업 그룹의 회원 들을 추가 하 고 네트워크에서 연결이 후 AD DS 대상 서버에서 제거 해야 합니다.  
  
##### <a name="to-remove-the-source-server-from-active-directory"></a>원본 서버 Active Directory를 제거 하려면  
  
1.  대상 서버에서 엽니다 **Active Directory 사용자 및 컴퓨터**합니다.  
  
2.  에 **Active Directory 사용자 및 컴퓨터** 탐색 창 도메인 이름 확장 한 다음 확장 **컴퓨터**합니다.  
  
3.  원본 서버 이름 여전히 서버의 목록에 있으면 클릭 마우스 오른쪽 단추로 클릭 **삭제**을 차례로 클릭 하 고 **예**합니다.  
  
4.  원본 서버 되어 있지 않은지 확인 하 고 종가, 나열 된 **Active Directory 사용자 및 컴퓨터**합니다.  
  
###  <a name="BKMK_MoveTheDHCPRole"></a>원본 서버에서 라우터에서 DHCP 서버 역할 이동  
  
> [!NOTE]

>  마이그레이션 프로세스를 시작 하기 전에이 작업이 이미 수행 하는 경우 계속 섹션 [제거 하 고 원본 서버 재활용](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_RemoveTheSourceServer)합니다.  

>  마이그레이션 프로세스를 시작 하기 전에이 작업이 이미 수행 하는 경우 계속 섹션 [제거 하 고 원본 서버 재활용](../migrate/Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_RemoveTheSourceServer)합니다.  

  
 원본 서버 DHCP 역할을 실행 중인 경우 라우터에서 DHCP 역할 이동 하려면 다음 단계를 수행 합니다.  
  
##### <a name="to-move-the-dhcp-role-from-the-source-server-to-the-router"></a>원본 서버에서 라우터에서 DHCP 역할 이동 하려면  
  
1.  원본 서버, DHCP 서비스를 다음과 같이 끄려면:  
  
    1.  원본 서버의 클릭 **시작**, 클릭 **관리 도구**을 차례로 클릭 하 고 **서비스**합니다.  
  
    2.  현재 실행 중인 서비스 목록에서 마우스 오른쪽 단추로 클릭는 **Windows Server**을 차례로 클릭 하 고 **속성**합니다.  
  
    3.  에 대 한 **시작 유형**선택 **사용 안 함**합니다.  
  
    4.  서비스를 중지 합니다.  
  
2.  라우터에서 DHCP 역할을 켜려면  
  
    1.  라우터에서 DHCP 역할을 켜려면 라우터 설명서에서 지침을 따릅니다.  
  
    2.  IP 주소 서버 원본에서 발급 한 그대로 유지 되도록 DHCP 범위 원본 서버의 동일 하 게 라우터에서 DHCP 범위 구성 하려면 라우터 설명서에서 지침을 따릅니다.  
  
    > [!IMPORTANT]
    >  대상 서버에 대 한 라우터에에서 고정 IP 또는 DHCP 예약을 설정 하지 않은 경우 DHCP 범위 원본 서버와 동일 하지는 불가능 라우터 대상 서버에 대 한 새로운 IP 주소를 발표할 예정입니다. 이 경우 초기화 포트 전달 전달 대상 서버 새 IP 주소를 라우터의 규칙 합니다.  
  
###  <a name="BKMK_RemoveTheSourceServer"></a>원본 서버 재활용 및 제거  
 원본 서버 끄고 네트워크에서 연결이 합니다. 필요한 모든 데이터 마이그레이션 대상 서버에 되었는지 확인 하기 최소한 한 주에 대 한 소스 서버 포맷 하지 않는 것이 좋습니다. 모든 데이터는 마이그레이션 되었는지 확인 한 후 다시 설치할 수 있습니다이 서버 네트워크에서 다른 작업에 대 한 보조 서버로 필요 합니다.  
  
> [!NOTE]
>  내리기 하 고 원본 서버 제거 대상 서버 다시 시작 합니다.  
  
 원본 서버, 내리기 후 정상 상태로 것은 아닙니다. 원본 서버 재활용 하려는 경우 가장 간단한 방법은 포맷 서버 운영 체제를 설치 하 고 다음 추가 서버도 사용 하도록 설정입니다.
