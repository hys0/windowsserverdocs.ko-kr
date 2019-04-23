---
title: '6단계: 새 Windows Server Essentials 네트워크에서 원본 서버 수준 내리기 및 제거'
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 86244c66-2c5e-488d-adb8-112e1ca3e2e1
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 24a1f2da2333c7e6854e9efd9d996391d0fcb3b9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59872364"
---
# <a name="step-6-demote-and-remove-the-source-server-from-the-new-windows-server-essentials-network"></a>6단계: 새 Windows Server Essentials 네트워크에서 원본 서버 수준 내리기 및 제거

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Windows Server Essentials 설치를 마친 후 마이그레이션을 완료 하는 다음 작업을 수행 해야 합니다.  
  
1.  [Active Directory 인증서 서비스를 제거 합니다.](Step-6--Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_ADCS)  
  
2.  [원본 서버에 직접 연결 된 프린터 연결 끊기](Step-6--Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_PhysicallyDisconnect)  
  
3.  [원본 서버의 수준을 내리기](Step-6--Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_DemoteTheSourceServer)  
  
4.  [제거 하 고 원본 서버의 용도 다시 설정](Step-6--Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_RemoveTheSourceServer)  
  
##  <a name="BKMK_ADCS"></a> Active Directory 인증서 서비스를 제거 합니다.  
 단일 서버에 여러 AD CS(Active Directory 인증서 서비스) 역할 서비스가 설치되어 있으면 절차가 약간 다릅니다. 다음 절차를 사용하여 AD CS 역할 서비스를 제거하고 다른 AD CS 역할 서비스를 유지할 수 있습니다.  
  
 이 절차를 완료하려면 CA(인증 기관)를 설치한 사용자와 동일한 권한으로 로그온해야 합니다. 엔터프라이즈 CA를 제거할 경우 Enterprise Admins의 구성원 또는 동등한 항목은 최소한 이 절차를 완료해야 합니다.  
  
#### <a name="to-remove-ad-cs"></a>AD CS를 제거하려면  
  
1.  도메인 관리자로 원본 서버에 로그온 합니다.  
  
2.  **시작**, **관리 도구**, **서버 관리자**를 차례로 클릭합니다.  
  
3.  **사용자 계정 컨트롤** 대화 상자에서 **계속** 을 클릭합니다.  
  
4.  **역할 요약** 섹션에서 **역할 제거**를 클릭합니다.  
  
5.  역할 제거 마법사에서 **다음**을 클릭합니다.  
  
6.  **Active Directory 인증서 서비스** 확인란을 선택 취소하고 **다음**을 클릭합니다.  
  
7.  **제거 옵션 확인** 페이지에서 정보를 검토하고 **제거**를 클릭합니다.  
  
    > [!NOTE]
    >  IIS(인터넷 정보 서비스)를 실행 중이면 계속 진행하기 전에 서비스를 중지하라는 메시지가 표시됩니다. **확인**을 클릭합니다.  
  
    > [!NOTE]
    >  먼저, **인증 기관 웹 등록**이 설치되어 있는 경우 이를 제거해야 할 수 있습니다.  
  
8.  역할 제거 마법사가 완료되면 서버를 다시 시작하여 제거 프로세스를 완료합니다.  
  
    > [!IMPORTANT]
    >  이에 대한 메시지가 표시되지 않더라도 서버를 다시 시작합니다.  
  
##  <a name="BKMK_PhysicallyDisconnect"></a> 원본 서버에 직접 연결 된 프린터 연결 끊기  
 원본 서버에서 수준을 내리기 전에 원본 서버에 직접 연결되거나 원본 서버를 통해 공유되는 모든 프린터의 연결을 실제로 끊습니다. 원본 서버에 직접 연결된 프린터에 대한 Active Directory 개체가 남아 있는지 확인합니다. 프린터 수 다음 직접 대상 서버에 연결 되며 Windows Server Essentials에서 공유 합니다.  
  
##  <a name="BKMK_DemoteTheSourceServer"></a> 원본 서버의 수준을 내리기  
 AD DS 도메인 컨트롤러 역할에서 도메인 구성원 서버 역할로 원본 서버의 수준을 내리기 전에 다음 절차에 설명된 대로 그룹 정책 설정이 모든 클라이언트 컴퓨터에 적용되는지 확인합니다.  
  
> [!IMPORTANT]
>  클라이언트 컴퓨터에서 그룹 정책 변경 내용을 업데이트하는 동안 원본 서버와 대상 서버가 네트워크에 연결되어야 합니다.  
  
#### <a name="to-force-a-group-policy-update-on-a-client-computer"></a>클라이언트 컴퓨터에서 그룹 정책 업데이트를 강제로 적용하려면  
  
1.  관리자로 클라이언트 컴퓨터에 로그인합니다.  
  
2.  관리자 권한으로 명령 프롬프트를 엽니다.  
  
3.  명령 프롬프트에 **gpupdate /force**를 입력하고 Enter 키를 누릅니다.  
  
4.  프로세스를 완료하려면 로그오프한 후 다시 로그온해야 합니다. **예** 를 클릭하여 확인합니다.  
  
 Windows Server Essentials 또는 이전 버전에서로 마이그레이션하는 경우 서버 수준 내리기 참조 [Active Directory Domain Services 제거](https://technet.microsoft.com/library/hh472163.aspx)합니다. 원본 서버를 작업 그룹의 구성원으로 추가하고 네트워크에서 연결을 끊고 나서 대상 서버의 AD DS에서 원본 서버를 제거해야 합니다.  
  
 Windows Server Essentials에서로 마이그레이션하는 경우 함으로써 다음 절차를 사용 하 여 원본 서버에서 도메인 컨트롤러의 수준을 내립니다 Active Directory Domain Services 역할을 제거 하려면 서버 관리자를 사용 합니다.  
  
#### <a name="to-remove-the-source-server-from-active-directory"></a>Active Directory에서 원본 서버를 제거하려면  
  
1.  대상 서버에서 **Active Directory 사용자 및 컴퓨터**를 엽니다.  
  
2.  **Active Directory 사용자 및 컴퓨터** 탐색 창에서 도메인 이름을 확장하고 **컴퓨터**를 확장합니다.  
  
3.  원본 서버가 서버 목록에 여전히 있는 경우 원본 서버 이름을 마우스 오른쪽 단추로 클릭하고 **삭제**를 클릭한 후 **예**를 클릭합니다.  
  
4.  원본 서버가 목록에 없는지 확인하고 **Active Directory 사용자 및 컴퓨터**를 닫습니다.  
  
##  <a name="BKMK_RemoveTheSourceServer"></a> 제거 하 고 원본 서버의 용도 다시 설정  
 원본 서버를 끄고 네트워크에서 연결을 끊습니다. 필요한 모든 데이터가 대상 서버로 마이그레이션되도록 최소한 한 주 동안 원본 서버를 다시 포맷하지 않는 것이 좋습니다. 모든 데이터가 마이그레이션되었는지 확인하고 나서 필요하면 다른 작업에 대한 보조 서버로 이 서버를 네트워크에 다시 설치할 수 있습니다.  
  
> [!NOTE]
>  원본 서버의 수준을 내리고 원본 서버를 제거하고 나서 대상 서버를 다시 시작합니다.  
  
 원본 서버의 수준을 내리고 나면 서버는 정상 상태가 아닙니다. 원본 서버의 용도를 변경하려는 경우 가장 간단한 방법은 원본 서버를 다시 포맷하고 서버 운영 체제를 설치한 다음 추가 서버로 사용하도록 설정하는 것입니다.  
  
## <a name="next-steps"></a>다음 단계  
 강등 하 고 새 Windows Server Essentials 네트워크에서 원본 서버를 제거 했습니다. 이제 [7 단계: Windows Server Essentials 마이그레이션을 위한 마이그레이션 후 작업 수행](Step-7--Perform-post-migration-tasks-for-the-Windows-Server-Essentials-migration.md)합니다.  
  

모든 단계를 보려면 [Windows Server Essentials로 마이그레이션](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md)합니다.

