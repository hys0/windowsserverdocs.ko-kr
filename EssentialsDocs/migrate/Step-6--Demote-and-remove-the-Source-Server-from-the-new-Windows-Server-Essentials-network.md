---
title: "6 단계: 내리기 하 고 원본 서버 새로운 Windows Server Essentials 네트워크에서 제거"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
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
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="step-6-demote-and-remove-the-source-server-from-the-new-windows-server-essentials-network"></a>6 단계: 내리기 하 고 원본 서버 새로운 Windows Server Essentials 네트워크에서 제거

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

Windows Server Essentials를 설치를 완료 하 고 마이그레이션을 완료 한 후 다음과 같은 작업을 수행 해야 합니다.  
  
1.  [제거 Active Directory 인증서 서비스](Step-6--Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_ADCS)  
  
2.  [원본 서버에 직접 연결 된 프린터에 연결 끊기](Step-6--Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_PhysicallyDisconnect)  
  
3.  [원본 서버 내리기](Step-6--Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_DemoteTheSourceServer)  
  
4.  [원본 서버 재활용 및 제거](Step-6--Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_RemoveTheSourceServer)  
  
##  <a name="BKMK_ADCS"></a>제거 Active Directory 인증서 서비스  
 절차는 여러 Active Directory 인증서 서비스 (AD CS) 역할 서비스 단일 서버에 설치 되어 있는 경우 약간 다릅니다. 다음 절차 AD CS 역할 서비스를 제거 하 고 다른 AD CS 역할 서비스를 사용할 수 있습니다.  
  
 이 절차를 완료 하려면 설치한 인증 기관 (캐나다) 사용자와 동일한 사용 권한으로 로그온 해야 합니다. 엔터프라이즈 캘리포니아를 제거 하는 엔터프라이즈 관리자 또는 해당 구성원이이 절차를 수행 하는 데 필요한 최소입니다.  
  
#### <a name="to-remove-ad-cs"></a>AD CS 제거 하려면  
  
1.  원본 서버 도메인 관리자 권한으로 로그온 합니다.  
  
2.  클릭 **시작**, 클릭 **관리 도구**을 차례로 클릭 하 고 **서버 관리자**합니다.  
  
3.  클릭 **계속** 에 **사용자 계정 컨트롤** 대화 상자가 합니다.  
  
4.  에 **역할 요약** 섹션에서 클릭 **역할 제거**합니다.  
  
5.  제거 역할 마법사에서 클릭 **다음**합니다.  
  
6.  지우기는 **Active Directory 인증서 서비스** 확인란을 선택한 다음 클릭 **다음**합니다.  
  
7.  에 **제거 옵션 확인** 페이지에서 정보를 검토 한 다음 클릭 **제거**합니다.  
  
    > [!NOTE]
    >  정보 IIS (인터넷 서비스)를 실행 하는 경우 계속 하기 전에 서비스를 중지 하 라는 메시지가 표시 됩니다. 클릭 **확인**합니다.  
  
    > [!NOTE]
    >  먼저, 제거 해야 할 수 있습니다 **인증 기관 웹 등록**설치 된 경우, 합니다.  
  
8.  제거 역할 마법사를 완료 서버 제거가 프로세스를 완료 하려면 다시 시작 합니다.  
  
    > [!IMPORTANT]
    >  이렇게 하 라는 메시지가 표시 되지 않을 경우에 서버를 다시 시작 합니다.  
  
##  <a name="BKMK_PhysicallyDisconnect"></a>원본 서버에 직접 연결 된 프린터에 연결 끊기  
 원본 서버, 내릴 전에 실제로 원본 서버에 직접 연결 되어 있고 원본 서버를 통해 공유 되는 프린터를 분리 합니다. 원본 서버에 직접 연결 된 프린터에 대 한 Active Directory 개체 없는 유지 하는 확인 합니다. 프린터 다음 수 직접 대상 서버에 연결 되어 있고 Windows Server Essentials의 공유 합니다.  
  
##  <a name="BKMK_DemoteTheSourceServer"></a>원본 서버 내리기  
 AD DS 도메인 컨트롤러 역할 소스 서버의 도메인 구성원 서버 역할을 내릴 하기 전에 다음 절차에 설명 된 대로 그룹 정책 설정을 모든 클라이언트 컴퓨터에 적용 되는지 확인 합니다.  
  
> [!IMPORTANT]
>  원본 서버와 대상 서버 동안 그룹 정책 업데이트 되는 클라이언트 컴퓨터에는 네트워크에 연결 합니다.  
  
#### <a name="to-force-a-group-policy-update-on-a-client-computer"></a>그룹 정책 업데이트는 클라이언트 컴퓨터에서 강제로  
  
1.  클라이언트 컴퓨터에서 관리자 권한으로 로그인 합니다.  
  
2.  관리자 권한으로 명령 프롬프트 창을 엽니다.  
  
3.  명령 프롬프트에 입력 **gpupdate /force**, ENTER 키를 누릅니다.  
  
4.  프로세스를 완료 하려면 다시 로그인 및 로그 오프 해야 할 수 있습니다. 클릭 **예** 하 여 확인 합니다.  
  
 이전 버전 또는 Windows Server Essentials의 마이그레이션할 경우 서버 내리기 참조 [Active Directory Domain Services 제거](https://technet.microsoft.com/library/hh472163.aspx)합니다. 원본 서버 작업 그룹의 회원 들을 추가 하 고 네트워크에서 연결이 후 AD DS 대상 서버에서 제거 해야 합니다.  
  
 Windows Server Essentials에서 마이그레이션하는 서버 관리자를 사용 하 여 되므로 다음 절차를 사용 하 여 원본 서버에 도메인 컨트롤러 내리기 Active Directory Domain Services 역할을 제거 하려면:  
  
#### <a name="to-remove-the-source-server-from-active-directory"></a>원본 서버 Active Directory를 제거 하려면  
  
1.  대상 서버에서 엽니다 **Active Directory 사용자 및 컴퓨터**합니다.  
  
2.  에 **Active Directory 사용자 및 컴퓨터** 탐색 창 도메인 이름 확장 한 다음 확장 **컴퓨터**합니다.  
  
3.  원본 서버 여전히 서버 목록에 있는 경우 원본 서버 이름을 마우스 오른쪽 단추로 클릭 **삭제**을 차례로 클릭 하 고 **예**합니다.  
  
4.  원본 서버 되어 있지 않은지 확인 하 고 종가, 나열 된 **Active Directory 사용자 및 컴퓨터**합니다.  
  
##  <a name="BKMK_RemoveTheSourceServer"></a>원본 서버 재활용 및 제거  
 원본 서버 끄고 네트워크에서 연결이 합니다. 필요한 모든 데이터 마이그레이션 대상 서버에 되었는지 확인 하기 최소한 한 주에 대 한 소스 서버 포맷 하지 않는 것이 좋습니다. 모든 데이터는 마이그레이션 되었는지 확인 한 후 다시 설치할 수 있습니다이 서버 네트워크에서 다른 작업에 대 한 보조 서버로 필요 합니다.  
  
> [!NOTE]
>  내리기 하 고 원본 서버 제거 대상 서버 다시 시작 합니다.  
  
 원본 서버, 내리기 후 정상 상태로 것은 아닙니다. 원본 서버 재활용 하려는 경우 가장 간단한 방법은 포맷 서버 운영 체제를 설치 하 고 다음 추가 서버도 사용 하도록 설정입니다.  
  
## <a name="next-steps"></a>다음 단계  
 내리는 하 고 원본 서버 새로운 Windows Server Essentials 네트워크 제거 했습니다. 지금 이동 [7 단계: Windows Server Essentials 마이그레이션에 대 한 후 마이그레이션 작업을 수행](Step-7--Perform-post-migration-tasks-for-the-Windows-Server-Essentials-migration.md)합니다.  
  

모든 단계를 참조 [Windows Server essentials 마이그레이션](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md)합니다.

