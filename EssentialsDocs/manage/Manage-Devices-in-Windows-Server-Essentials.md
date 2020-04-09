---
title: Windows Server Essentials에서 장치 관리
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: f5fe1088-ebe7-4799-a47d-075b0048dea1
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: f05d156447cddf9afbbe20fddc4b590459a37ae7
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80852816"
---
# <a name="manage-devices-in-windows-server-essentials"></a>Windows Server Essentials에서 장치 관리

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials
 
 다음 섹션에서는 서버의 디바이스 관리 기능에 대해 설명하고 네트워크에서 디바이스를 설정 및 사용하는 방법을 설명합니다.  
  
-   [대시보드를 사용 하 여 장치 관리](Manage-Devices-in-Windows-Server-Essentials.md#BKMK_1)  
  
-   [사용자 계정에 특정 네트워크 컴퓨터에 로그온 할 수 있는 권한 할당](Manage-Devices-in-Windows-Server-Essentials.md#BKMK_2)  
  
-   [서버에서 컴퓨터 제거](Manage-Devices-in-Windows-Server-Essentials.md#BKMK_3)  
  
-   [폴더 리디렉션 및 보안에 대 한 그룹 정책 설정 구성](Manage-Devices-in-Windows-Server-Essentials.md#BKMK_5)  
  
-   [원격 데스크톱 세션을 사용 하 여 네트워크 컴퓨터에 연결](Manage-Devices-in-Windows-Server-Essentials.md#BKMK_7)  
  
-   [컴퓨터 속성 보기](Manage-Devices-in-Windows-Server-Essentials.md#BKMK_8)  
  
##  <a name="manage-devices-by-using-the-dashboard"></a><a name="BKMK_1"></a>대시보드를 사용 하 여 장치 관리  
 Windows Server Essentials에서는 Windows Server Essentials 대시보드를 사용하여 일반적인 관리 작업을 수행할 수 있습니다. 대시보드의 **장치** 페이지에서는 다음을 제공합니다.  
  
-   다음을 표시하는 네트워크 컴퓨터 목록:  
  
    -   컴퓨터 이름  
  
    -   컴퓨터 상태, **온라인** 또는 **오프라인**  
  
    -   컴퓨터 설명  
  
    -   컴퓨터의 백업 상태  
  
    -   컴퓨터의 업데이트 상태  
  
    -   컴퓨터의 보안 상태  
  
    -   컴퓨터의 경고 상태  
  
    -   컴퓨터에 대한 그룹 정책 정보  
  
-   선택한 컴퓨터에 대한 추가 정보가 있는 세부 정보 창  
  
-   컴퓨터 속성 및 경고 보기, 컴퓨터 백업 설정, 백업에서 파일 및 폴더 복원과 같은 일련의 디바이스 관리 작업이 포함된 작업 창  
  
#### <a name="to-view-the-status-of-network-computers"></a>네트워크 컴퓨터의 상태를 보려면  
  
1. Windows Server Essentials 대시보드를 엽니다.  
  
2. 탐색 모음에서 **장치**를 클릭합니다.  
  
3. 목록 창에서 네트워크에 있는 모든 컴퓨터의 상태를 확인합니다.  
  
   다음 표에서는 Windows Server Essentials 대시보드에서 사용할 수 있는 다양한 컴퓨터 및 백업 작업에 대해 설명합니다. 일부 작업은 컴퓨터 관련 작업이고 목록에서 컴퓨터를 선택할 때만 표시됩니다.  
  
### <a name="computer-tasks-in-the-dashboard"></a>대시보드의 컴퓨터 작업  
  
|작업 이름|설명|  
|---------------|-----------------|  
|컴퓨터 속성 보기|선택한 컴퓨터에 대한 일반적인 정보를 표시하고 컴퓨터 백업에 대한 세부 정보를 볼 수 있습니다.|  
|이 컴퓨터에 대한 백업 설정|백업 설정 마법사를 실행합니다.|  
|컴퓨터에 대한 백업 사용자 지정|선택한 컴퓨터에 대한 백업 설정을 변경할 수 있는 백업 속성을 엽니다.|  
|컴퓨터에 대한 백업 시작|선택한 컴퓨터에 대한 백업을 시작합니다.|  
|컴퓨터에 대한 백업 중지|선택한 컴퓨터에 대한 백업을 중지합니다.|  
|컴퓨터에 대한 파일 또는 폴더 복원|특정 파일, 폴더 또는 드라이브를 복원할 수 있는 파일 및 폴더 복원 마법사를 실행합니다.|  
|컴퓨터에 대한 경고 보기|중요 및 기타 정보 경고를 표시하고 가능한 경우 수정 작업을 수행할 수 있습니다.|  
|컴퓨터에 대한 원격 데스크톱|선택한 컴퓨터에 대한 원격 데스크톱 연결을 엽니다.|  
|컴퓨터 제거|Windows Server Essentials 대시보드에서 컴퓨터를 분리하는 컴퓨터 제거 마법사를 실행합니다.|  
|컴퓨터 백업 및 파일 기록 설정 사용자 지정|클라이언트 컴퓨터에 대한 백업 일정 및 파일 히스토리 설정을 변경할 수 있는 백업 설정 페이지를 엽니다.|  
|서버에 컴퓨터를 연결하는 방법|컴퓨터를 네트워크에 연결하려고 수행하는 단계에 대해 설명하는 도움말 항목을 엽니다.|  
|그룹 정책 구현|도메인에 가입된 Windows 8 및 Windows 7 컴퓨터에 정책 설정을 적용합니다.|  
  
##  <a name="assign-user-accounts-permission-to-log-on-to-specific-network-computers"></a><a name="BKMK_2"></a>사용자 계정에 특정 네트워크 컴퓨터에 로그온 할 수 있는 권한 할당  
 사용자가 원격 위치에서 Windows Server Essentials 네트워크에 액세스할 때 특정 네트워크 컴퓨터에만 로그온할 수 있도록 사용자 계정에 사용 권한을 할당할 수 있습니다.  
  
#### <a name="to-change-the-computer-access-for-a-user-account"></a>사용자 계정에 대한 컴퓨터 액세스 권한을 변경하려면  
  
1.  Windows Server Essentials 대시보드를 엽니다.  
  
2.  탐색 모음에서 **사용자**를 클릭합니다.  
  
3.  사용자 계정 목록에서 변경하려는 사용자 계정을 선택합니다.  
  
4.  **< 사용자 계정\> 작업** 창에서 **계정 속성 보기**를 클릭 합니다. 사용자 계정에 대한 **속성** 페이지가 나타납니다.  
  
5.  **컴퓨터 액세스** 탭에서 사용자가 원격으로 액세스할 수 있는 컴퓨터를 선택하고 **확인**을 클릭합니다.  
  
##  <a name="remove-a-computer-from-the-server"></a><a name="BKMK_3"></a>서버에서 컴퓨터 제거  
 대시보드를 사용하여 Windows Server Essentials를 실행 중인 서버에서 컴퓨터를 제거하면 컴퓨터가 더 이상 서버에서 관리되지 않습니다. 따라서 서버에서는 컴퓨터 백업 만들기를 중지하거나 컴퓨터가 네트워크에서 제거되고 난 후의 상태를 모니터링합니다.  
  
> [!NOTE]
>  서버에서 컴퓨터를 제거해도 네트워크에서 컴퓨터의 연결이 끊어지지 않습니다. 컴퓨터에서는 서버에 연결되기 전과 같은 방식으로 네트워크의 리소스에 계속 액세스할 수 있습니다. 컴퓨터에서 서버 리소스에 액세스하지 못하게 하고 서버에서 컴퓨터 연결을 끊으려면 도메인에서 컴퓨터를 제거해야 합니다. 또한 서버에서 컴퓨터를 제거해도 제거 중인 컴퓨터에서 Connector 소프트웨어 또는 실행 패드가 자동으로 제거되지 않습니다. 컴퓨터에서 Connector 소프트웨어를 수동으로 제거해야 합니다. 자세한 내용은 [Get Connected](../use/Get-Connected-in-Windows-Server-Essentials.md)에서 Connector 소프트웨어 제거 섹션을 참조 하세요.  
  
#### <a name="to-remove-a-computer-from-the-network-by-using-the-dashboard"></a>대시보드를 사용하여 네트워크에서 컴퓨터를 제거하려면  
  
1.  Windows Server Essentials 대시보드를 엽니다.  
  
2.  탐색 모음에서 **장치** 탭을 클릭합니다.  
  
3.  컴퓨터 목록에서, 네트워크에서 제거할 컴퓨터를 마우스 오른쪽 단추로 클릭하고 **컴퓨터 제거**를 클릭합니다.  
  
##  <a name="configure-group-policy-settings-for-folder-redirection-and-security"></a><a name="BKMK_5"></a>폴더 리디렉션 및 보안에 대 한 그룹 정책 설정 구성  
 Windows Server Essentials 대시보드를 사용하여 그룹 정책을 구성하고 Windows Server Essentials 네트워크의 컴퓨터에 배포할 수 있습니다. Windows Server Essentials의 그룹 정책에는 Windows 업데이트, Windows Defender 및 네트워크 방화벽에 영향을 미치는 폴더 리디렉션 및 보안에 대한 설정이 포함됩니다.  
  
#### <a name="to-configure-group-policy-in-windows-server-essentials"></a>Windows Server Essentials에서 그룹 정책을 구성하려면  
  
1.  Windows Server Essentials 대시보드를 엽니다.  
  
2.  탐색 모음에서 **장치**를 클릭합니다.  
  
3.  Windows Server Essentials의 경우: 전역 **사용자 작업** 창에서 **그룹 정책 구현**을 클릭 합니다.  
  
     Windows Server Essentials의 경우: 전역 **장치 작업** 창에서 **그룹 정책 구현**을 클릭 합니다.  
  
4.  그룹 정책 구현 마법사가 열립니다.  
  
5.  마법사의 **폴더 리디렉션 그룹 정책 사용** 페이지에서 리디렉션할 사용자 폴더를 선택할 수 있습니다.  
  
6.  마법사의 **보안 정책 설정 사용** 페이지에서 **Windows 업데이트**, **Windows Defender** 및 **네트워크 방화벽**에 대한 그룹 정책 설정을 사용하도록 설정할 수 있습니다.  
  
7.  **마침**을 클릭하여 그룹 정책 설정을 구현합니다.  
  
##  <a name="connect-to-a-network-computer-by-using-a-remote-desktop-session"></a><a name="BKMK_7"></a>원격 데스크톱 세션을 사용 하 여 네트워크 컴퓨터에 연결  
 사무실을 비울 때 Windows Server Essentials 네트워크 컴퓨터에 원격으로 액세스 하려면 웹 브라우저를 사용 하 여 조직의 원격 웹 액세스 웹 사이트에 로그온 하 고 컴퓨터 탭에서 컴퓨터 이름을 클릭 **합니다.**  
  
 **상태** 열에는 네트워크의 컴퓨터에 연결할 수 있는지가 표시되고 다음 값이 포함될 수 있습니다.  
  
-   **사용 가능**  
  
     컴퓨터가 켜져 있고 원격 연결에 사용할 수 있습니다. 이 상태가 표시되더라도 타사 방화벽이 연결을 차단하면 이 컴퓨터에 연결하지 못할 수 있습니다.  
  
-   **오프 라인 또는 절전 모드**  
  
     컴퓨터가 꺼져 있거나 절전 모드 또는 최대 절전 모드에 있습니다. 컴퓨터가 오프라인이거나 절전 모드이면 컴퓨터를 사용할 수 있을 때 알 수 있도록 상태가 실시간으로 업데이트됩니다.  
  
-   **지원 되지 않는 운영 체제**  
  
     컴퓨터의 운영 체제에서 원격 데스크톱을 지원하지 않습니다. 변경 사항이 있으면 서버에서 이 상태가 업데이트되는 데 최대 6시간이 걸릴 수 있습니다.  
  
-   **연결 사용 안 함**  
  
     컴퓨터 연결이 방화벽으로 차단되거나 원격 데스크톱이 컴퓨터 또는 그룹 정책에서 사용 안 함으로 설정되었습니다. 변경 사항이 있으면 서버에서 이 상태가 업데이트되는 데 최대 6시간이 걸릴 수 있습니다.  
  
##  <a name="view-computer-properties"></a><a name="BKMK_8"></a>컴퓨터 속성 보기  
 Windows Server Essentials 대시보드의 **장치** 섹션에는 네트워크 컴퓨터 목록이 표시됩니다. 목록에서는 각 컴퓨터에 대한 추가 정보도 제공합니다.  
  
#### <a name="to-view-a-list-of-computers"></a>컴퓨터 목록을 보려면  
  
1.  Windows Server Essentials 대시보드를 엽니다.  
  
2.  기본 탐색 모음에서 **장치**를 클릭합니다.  
  
3.  대시보드에는 현재 컴퓨터 목록이 표시됩니다.  
  
#### <a name="to-view-or-change-properties-for-a-computer"></a>컴퓨터에 대한 속성을 보거나 변경하려면  
  
1.  컴퓨터 목록에서 속성을 보거나 변경할 계정을 선택합니다.  
  
2.  **< Computername\> 작업** 창에서 **컴퓨터 속성 보기**를 클릭 합니다. 컴퓨터에 대한 **속성** 페이지가 나타납니다.  
  
3.  탭을 클릭하여 해당 컴퓨터에 대한 속성을 표시합니다.  
  
4.  컴퓨터 속성의 모든 변경 사항을 저장하려면 **적용**을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
  
-   [원격 웹 액세스 관리](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md)  
  
-   [원격 웹 액세스 사용](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md)  
  
-   [대시보드를 사용 하 여 사용자 계정 관리](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage8)  
  
-   [Windows Server Essentials 관리](Manage-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials 사용](../use/Use-Windows-Server-Essentials.md)
