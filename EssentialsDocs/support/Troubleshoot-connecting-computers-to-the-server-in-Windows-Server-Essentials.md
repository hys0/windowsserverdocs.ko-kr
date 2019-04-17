---
title: "Windows Server Essentials의 서버로 컴퓨터를 연결 문제 해결"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e45b3d89-c057-4c70-a627-86fb06dd22aa
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 9b0d11be08840ecedabab6fd4e96f5d453ea4857
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="troubleshoot-connecting-computers-to-the-server-in-windows-server-essentials"></a>Windows Server Essentials의 서버로 컴퓨터를 연결 문제 해결

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다. 
  
 이 항목에서는 컴퓨터를 Windows Server Essentials 또는 Windows Server Essentials 실행 하는 서버에 연결할 때 발생할 수 있는 문제에 대 한 문제 해결 지침입니다.  
  
> [!NOTE]
>  Windows Server Essentials 및 Windows Server Essentials 커뮤니티에서 가장 최근 문제 해결 정보에 대 한 것이 좋습니다 방문 하 여 [Windows Server Essentials 포럼](https://social.technet.microsoft.com/Forums/windowsserver/home?forum=winserveressentials)합니다. Windows Server Essentials 포럼에 대 한 도움말을 검색 하거나 질문 하기에 좋은 장소입니다.  
  
 이 항목에서는 다음과 같은 문제에 대 한 솔루션을 제공합니다.  
  

-   문제 1: [1 문제](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BMRK_Package)  
  
-   문제 2: [발급 2](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssue2)  
  
-   문제 3: [3 문제](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssue2a)  
  
-   문제 4: [4 문제](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssueNetFramework)  
  
-   문제 5: [5 문제](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_Time)  
  
-   문제 6: [6 문제](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ServiceStopped)  
  
-   7 문제: [7 문제](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssueReconnect)  
  
-   문제 8: [8을 실행](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_JoinWin7)  
  
-   문제 9: [9 문제](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssueAutologon)  
  
-   10 문제: [10 문제](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssueOldLogs)  
  
-   문제 11: [11 실행](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_UpgradeClientOS)  

-   문제 1: [1 문제](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BMRK_Package)  
  
-   문제 2: [발급 2](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssue2)  
  
-   문제 3: [3 문제](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssue2a)  
  
-   문제 4: [4 문제](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssueNetFramework)  
  
-   문제 5: [5 문제](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_Time)  
  
-   문제 6: [6 문제](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ServiceStopped)  
  
-   7 문제: [7 문제](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssueReconnect)  
  
-   문제 8: [8을 실행](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_JoinWin7)  
  
-   문제 9: [9 문제](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssueAutologon)  
  
-   10 문제: [10 문제](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssueOldLogs)  
  
-   문제 11: [11 실행](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_UpgradeClientOS)  

  
##  <a name="BMRK_Package"></a>1 문제  
 **문제**  
  
 설치가 완료 하지 못했습니다 패키지를 받습니다. Windows Server Essentials 커넥터를 다시 설치 해 보세요. 문제가 계속 되 면 컴퓨터를 서버에 연결할 때 사용자의 네트워크 관리자에 오류가 문의  
  
 **설명**  
  
 이 문제는 컴퓨터 보류 중인 다른 Windows 업데이트 또는 응용 프로그램 설치 하 고 커넥터 설치를 취소은 Windows Server Essentials 실행 하는 서버에 연결 하는 경우 발생할 수 있습니다.  
  
 **해결 방법**  
  
 다른 모든 업데이트 또는 응용 프로그램 설치를 완료 합니다. 메시지가 표시 되 면 컴퓨터를 다시 시작 합니다.  
  
##  <a name="BKMK_ConnectorIssue2"></a>문제 2  
 **문제**  
  
 컴퓨터를 Windows Server Essentials 가입 수 없습니다  
  
 **설명**  
  
 컴퓨터 이름에 ASCII 아닌 문자가 포함 된 컴퓨터 Windows Server Essentials 가입 수 없습니다. "오류가 발생 했습니다." 오류 메시지가 나타납니다 컴퓨터 이름을 ASCII 문자를 포함 하는 경우  
  
 **해결 방법**  
  
 ASCII 문자를 포함 하는 이름으로 클라이언트 컴퓨터 바꾸고 Windows Server Essentials에 컴퓨터를 다시 추가 해 보세요.  
  
##  <a name="BKMK_ConnectorIssue2a"></a>3 문제  
 **문제**  
  
 저는 소프트웨어 설치 되는 커넥터 취소 오류가 발생 컴퓨터 서버에 연결할 때  
  
 **설명**  
  
 컴퓨터의 서버에 연결할 수 시스템 계정 Windows Server Essentials 대시보드에서 표시 되는 서버 폴더에서 전체 권한이 있어야 합니다. "커넥터 소프트웨어 설치 취소" 오류가 발생 하는 데 필요한 권한을 부여 되지 않은 경우 메시지가 표시 됩니다.  
  
 **해결 방법**  
  
 시스템 계정 부여 **모든 권한** 각 서버 폴더에 대 한 권한을 합니다.  
  
#### <a name="to-grant-the-system-account-full-control-permissions-on-a-server-folder"></a>시스템 계정 모든 권한 서버 폴더에 대 한 권한을 부여 하려면  
  
1.  Windows Server Essentials 대시보드를 엽니다.  
  
2.  클릭 **저장소**을 차례로 클릭 하 고 **서버 폴더**합니다.  
  
3.  서버 폴더를 마우스 오른쪽 단추로 클릭 한 다음 클릭 **폴더를 열고**합니다. (표시 되지 않는 경우는 **폴더를 열고** 옵션을 필요가 없습니다 폴더에 사용 권한을 설정할 수 있습니다.)  
  
4.  Windows 탐색기의 맨 네트워크 오솔길 서버에서 공유 폴더를 표시 하는 서버 공유를 클릭 합니다. 예를 들어 경로 **네트워크 > Server01 > 파일 히스토리를 백업**, 클릭 **Server01**합니다.  
  
5.  서버 폴더를 마우스 오른쪽 단추로 클릭 한 다음 클릭 **속성**합니다.  
  
6.  클릭 하 고 **보안** 탭 합니다.  
  
7.  하는 경우 **모든 권한** 는 클릭 시스템 계정에 사용할 수 없습니다 **편집**을 차례로 클릭 하 고 **시스템**합니다. 아래에서 **시스템에 대 한 권한**는 **허용** 옆에 있는 확인란 **모든 권한**합니다.  
  
8.  클릭 **확인** 두 번 업데이트 하는 권한을 닫습니다 **속성**합니다.  
  
##  <a name="BKMK_ConnectorIssueNetFramework"></a>4 문제  
 **문제**  
  
 응용이 프로그램을 실행 To 보는, 다음 버전의.NET Framework 중 하나를 설치 해야: V4.5.50709 "컴퓨터 서버에 연결 하는 동안 오류가 발생 했습니다.  
  
 **설명**  
  
 컴퓨터를 Windows Server Essentials 또는 Windows Server Essentials 실행 하는 서버에 연결할 때 마법사.NET Framework 버전 4.5.50709 컴퓨터에 설치를 시도 합니다. 하지만 이전 버전의.NET Framework 4.5 버전 있으면 출시 된 업데이트를 설치할 수 없습니다 하 고이 오류 메시지와 함께 실패 하는 연결 시도: 실행이 응용 프로그램을 설치 해야 다음 버전의.NET Framework 중 하나: V4.5.50709 합니다. 적절 한 버전의.NET Framework 받기에 대 한 지침은 할당 게시자에 게 문의 합니다.  
  
 **해결 방법**  
  
 .NET Framework 4.5 된 컴퓨터에서 제거 하 고 서버에 컴퓨터를 연결 합니다.  
  
#### <a name="to-uninstall-net-framework-45"></a>.NET Framework 4.5 제거 하려면  
  
1.  에 **시작** 열기 클라이언트 컴퓨터의 페이지 **제어판**합니다.  
  
2.  제어판의에서 **프로그램**, 클릭 **프로그램을 제거**합니다.  
  
3.  마우스 오른쪽 단추로 클릭 **Microsoft.NET Framework 4.5**을 차례로 클릭 하 고 **제거**합니다.  
  
4.  .NET Framework 4.5 성공적으로 제거한 후 컴퓨터의 서버에 연결 합니다. .NET Framework 4.5 올바른 릴리스 커넥터 소프트웨어와 함께 설치 되어 있습니다.  
  
##  <a name="BKMK_Time"></a>5 문제  
 **문제**  
  
 보는 서버를 사용할 수 없습니다. 이 문제를 해결 하려면 네트워크 관리자에 담당자에 게 문의 합니다. 컴퓨터 서버에 연결 하는 동안 오류가 발생 했습니다.  
  
 **설명**  
  
 이 날짜 및 시간 연결 된 컴퓨터에서 날짜와 시간이 서버에 동기화 되지 않는 경우 발생할 수 있습니다.  Windows Server Essentials 및 Windows Server Essentials 날짜 및 시간 Windows Server Essentials 또는 Windows Server Essentials 네트워크에서 실행 중인 컴퓨터의 동기화 하도록 시간 동기화 서비스를 사용 합니다. 동기화 된 시간은 기본 인증 프로토콜 서버 시간 인증 과정의 일환으로 사용 하기 때문에 중요 합니다. 예를 들어, 경우 적합 한 날짜 및 시간, Windows Server Essentials 시계 클라이언트 컴퓨터에 동기화 되지 않았습니다 또는 Windows Server Essentials 인증 잘못 될 수 있습니다 로그온 요청 침입 시도으로 해석 하 고 사용자에 대 한 액세스 거부 합니다.  
  
 이 서버 s 무료 메모리 5% 미만인 경우 발생할 수 있습니다.  
  
 Windows 필수 패키지 서버에 VPN 연결에 이미 있으며 도메인 주소를 사용 하 여는 커넥터 소프트웨어 끄기-프레미스 구성 하려고 하면 경우일 수 있습니다.  
  
 **해결 방법**  
  
1.  날짜 및 시간 클라이언트 컴퓨터에서 서버와 동기화 합니다. 다음 컴퓨터 서버에 연결 합니다.  
  
2.  서버 쪽에 있는 일부 응용 프로그램을 닫은 후 서버에 컴퓨터를 연결 합니다.  
  
3.  VPN 연결을 닫은 후 컴퓨터의 서버에 연결 합니다.  
  
#### <a name="to-change-the-date-and-time-on-the-client-computer"></a>날짜 및 시간 클라이언트 컴퓨터에서 변경 하려면  
  
1.  클라이언트 컴퓨터의 시작 페이지를 열고 **제어판**합니다.  
  
2.  제어판에서 클릭 **시계, 언어 및 지역**을 차례로 클릭 하 고 **날짜 및 시간**합니다.  
  
3.  클릭 **날짜 및 시간 변경**적합 한 날짜 및 시간, 날짜 및 시간을 설정 하 고 클릭 한 다음 **확인**합니다.  
  
4.  클릭 **확인**, 한 다음 제어판을 닫습니다.  
  
5.  컴퓨터에 연결 하는 클라이언트는 서버 다시 시도 합니다. 자세한 내용은 서버에 연결 컴퓨터를 참조 하십시오.  
  
 그래도 연결할 수 없는 경우 클라이언트 컴퓨터 서버, 날짜 및 시간 서버에 맞는지 확인 합니다. 날짜 및 시간 올바르지 않은 경우 변경 합니다.  
  
#### <a name="to-change-the-date-and-time-on-the-server"></a>서버에서 시간 및 날짜 변경 하려면  
  
1.  Windows Server Essentials 또는 Windows Server Essentials 설치 및 구성을 설정 하는 암호를 사용 하 여 서버에 로그온 합니다.  
  
    > [!NOTE]
    >  서버를 원격으로 관리 하는 경우 원격 데스크톱 연결을 사용 하 여 서버에 로그온 해야 합니다.  
  
2.  에 **시작** 페이지를 열고 **제어판**합니다.  
  
3.  제어판에서 클릭 **시계, 언어 및 지역**을 차례로 클릭 하 고 **날짜 및 시간**합니다.  
  
4.  클릭 **날짜 및 시간 변경**적합 한 날짜 및 시간, 날짜 및 시간을 설정 하 고 클릭 한 다음 **확인**합니다.  
  
5.  클릭 **확인**, 한 다음 제어판을 닫습니다.  
  
6.  클라이언트 컴퓨터의 컴퓨터에 연결 하는 클라이언트는 서버 다시 시도 합니다. 자세한 내용은 서버에 연결 컴퓨터를 참조 하십시오.  
  
##  <a name="BKMK_ServiceStopped"></a>6 문제  
 **문제**  
  
 An 보는 오류가 발생 했습니다. 이 문제를 해결 하려면 네트워크 관리자에 담당자에 게 문의 합니다. 컴퓨터 서버에 연결 하는 동안 오류가 발생 했습니다.  
  
 **설명**  
  
 이 오류 메시지가 WSS 인증서 웹 서비스 실행 되지 않을 수 있습니다.  
  
 **해결 방법**  
  
 WSS 인증서 웹 서비스를 시작 합니다.  
  
#### <a name="to-start-the-wss-certificate-web-service"></a>WSS 인증서 웹 서비스를 시작 하려면  
  
1.  서버에서 **시작** 페이지를 열고 **관리 도구**합니다.  
  
     **관리 도구**를 마우스 오른쪽 단추로 클릭 **서비스 IIS (인터넷 정보) 관리자**을 차례로 클릭 하 고 **열기**합니다.  
  
2.  탐색 창에서 클릭 **WSS 인증서 웹 서비스**합니다.  
  
3.  에 **작업** 창 클릭 **시작**합니다.  
  
##  <a name="BKMK_ConnectorIssueReconnect"></a>7 문제  
 **문제**  
  
 이 이름은 컴퓨터 이미 서버에 연결 하 여 경고 시도가 실패 한 연결 후 컴퓨터를 서버에 연결할 때 나타나는  
  
 **설명**  
  
 다시 연결 하려고 하면 다음 경고 이전 컴퓨터 서버에 연결 하려고 취소 또는 중단 된 경우 발생할 수 있습니다:이 이름의 컴퓨터 이미 서버에 연결 합니다. 이 오류는 인증서가 서버에 처음 연결 하려고 할 때 발급 때문에 발생 합니다.  
  
 **해결 방법** 인 경우 동일한 이름의 다른 컴퓨터는 서버에 이미 연결 되어 있는지 클릭 **다음**를 완료 하는 지침을 따릅니다는 **내 컴퓨터는 서버에 연결할** 마법사 합니다.  
  
##  <a name="BKMK_JoinWin7"></a>8 문제  
 **문제**  
  
 커넥터 소프트웨어를 실행 하기 위한 웹 페이지가 열립니다 하지만 클라이언트 컴퓨터 서버에 연결할 수 없는 서버에 Windows 7 Home 실행 하는 클라이언트 컴퓨터에 연결 하려고 하면  
  
 **설명**  
  
 라우터가 네트워크에는 활성화 멀티 캐스트, 서버와 Windows 7 Home Basic 또는 Windows 7 Home Premium 실행 하는 클라이언트 컴퓨터 간 통신 제대로 작동 하지 않습니다.  
  
 **해결 방법**  
  
 라우터를 사용 하지 않도록 설정 합니다. 일부 라우터에서 립-2 분 라우팅 프로토콜을 사용 하지 않도록 설정 하는 할 수 있습니다. 자세한 내용은 라우터 제조업체에서 제공 되는 설명서를 참조 하세요.  
  
##  <a name="BKMK_ConnectorIssueAutologon"></a>9 문제  
 **문제**  
  
 자동 로그온 I 컴퓨터 서버에 연결 된 후에 작동 중지 됨  
  
 **설명**  
  
 Windows Server Essentials에 컴퓨터를 연결 하면 자동 로그온 사용자 계정에 대 한 설정 되어, 커넥터 소프트웨어는 컴퓨터에 설치 되어 설정을 덮어씁니다.  
  
 **해결 방법** 컴퓨터 서버에 연결할 때이 문제를 해결 하려면 사용자 계정에 대 한 사용 암호를 확인 합니다. 커넥터 소프트웨어를 설치한 후 구성 해당 계정을 사용 하 여 자동 로그온 합니다.  
  
> [!NOTE]
>  Windows Server Essentials 도메인 계정 암호 정책 기본 요구 사항을 충족 하는 암호가 필요 합니다.  
  
##  <a name="BKMK_ConnectorIssueOldLogs"></a>10 문제  
 **문제**  
  
 기존 로그를 제거 하지 않습니다 커넥터 소프트웨어의 시험판 버전이 제거  
  
 **설명**  
  
 (Beta 또는 RC) 시험판 Windows Server Essentials의 릴리스 버전으로 업데이트 한 후에 서버에 연결 된 각 컴퓨터에서 커넥터 소프트웨어를 제거 하 고 다시 커넥터 소프트웨어의 릴리스 버전을 설치 하려면 컴퓨터를 연결 해야 합니다.  
  
 그러나 네트워크 컴퓨터에서 커넥터 소프트웨어를 제거 하면, 해당 컴퓨터에 %ProgramData%\Microsoft\Windows Server\Logs\ 폴더의 기존 로그 파일 삭제 되지 않습니다. 로그 폴더를 삭제 하면 Windows Server Essentials의 릴리스 버전에 컴퓨터를 연결 하는 경우 로그 파일을 손상 될 수 있습니다.  
  
 **해결 방법** 로그 파일 손상이 방지 하려면 직접 폴더를 삭제 로그 클라이언트 컴퓨터 업데이트 서버에 연결 하기 전에 합니다.  
  
#### <a name="to-reconnect-a-computer-after-a-server-update-without-corrupting-the-log-files"></a>파일 서버 로그 손상 없이 업데이트 한 후 컴퓨터를 다시 연결 하려면  
  
1.  컴퓨터에서 커넥터 소프트웨어를 제거 합니다.  
  
2.  %ProgramData%\Microsoft\Windows Server\ 폴더에서 로그 폴더를 삭제 합니다.  
  
3.  서버에 컴퓨터를 다시 연결 합니다. 하는 새 로그 폴더 및 파일 로그 만들기 커넥터 소프트웨어의 릴리스 버전을 설치 합니다.  
  
##  <a name="BKMK_UpgradeClientOS"></a>11 문제  
 **문제**  
  
 업그레이드 하는 클라이언트 컴퓨터에서 운영 체제 하려는 경우  
  
 **설명**  
  
 커넥터 소프트웨어를 설치 하는 동안 클라이언트 모든 커넥터 필수 조건을 충족 확인 하는 클라이언트 운영 체제에 대해 많은 검사가 수행 됩니다. 클라이언트 운영 체제를 커넥터 소프트웨어를 설치한 후 업그레이드 하면, 수 일부 필수 있으며 클라이언트 커넥터 실패할 수 있습니다.  
  
 **해결 방법**  
  
 클라이언트 운영 체제 다른 버전으로 업그레이드 하기 전에 (예를 들어, Windows XP를 Windows Vista 또는 Windows Vista의 Windows 7로)로 업그레이드 커넥터 소프트웨어를 제거 해야 합니다. 사용 하 여 **프로그램 추가 / 제거** 제어판의 합니다. 클라이언트 운영 체제 업그레이드가 완료 되 면 http://< 열어 클라이언트 커넥터 다시를 설치할 수 있습니다. *서버*> 연결 하려면 웹 브라우저에서 / 어디 <*서버*> 서버 Windows Server Essentials의 이름입니다.  
  
 이미 클라이언트 커넥터 소프트웨어가 설치 된 업그레이드를 사용 하 여 **프로그램 추가/제거** 또는 **프로그램 및 기능** 커넥터 소프트웨어를 제거 합니다. 커넥터 소프트웨어를 다시 설치 합니다.  
  
## <a name="see-also"></a>참조 하십시오  
  
-   [Windows Server Essentials 관리](../manage/Manage-Windows-Server-Essentials.md)  
  
-   [Windows 2012 Server Essentials ConnectComputer (TechNet Wiki)의 문제 해결](https://social.technet.microsoft.com/wiki/contents/articles/14370.windows-2012-server-essentials-connectcomputer-troubleshooting.aspx)
