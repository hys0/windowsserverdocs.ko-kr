---
title: "Windows Server Essentials의 디바이스 관리"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f5fe1088-ebe7-4799-a47d-075b0048dea1
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 288d62a3fe4d9073ba2c0e3fdff385d8317f20d4
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="manage-devices-in-windows-server-essentials"></a>Windows Server Essentials의 디바이스 관리

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.
 
 다음 섹션 서버 장치 관리 기능에 설명 하 고을 설정 하 고 네트워크에서 디바이스를 사용 하는 방법을 설명 합니다.  
  
-   [대시보드를 사용 하 여 디바이스 관리](Manage-Devices-in-Windows-Server-Essentials.md#BKMK_1)  
  
-   [특정 네트워크 컴퓨터에 로그온 할 수 있는 사용자 계정에 할당](Manage-Devices-in-Windows-Server-Essentials.md#BKMK_2)  
  
-   [컴퓨터 서버에서 제거](Manage-Devices-in-Windows-Server-Essentials.md#BKMK_3)  
  
-   [폴더 리디렉션 및 보안에 대 한 그룹 정책 설정을 구성합니다](Manage-Devices-in-Windows-Server-Essentials.md#BKMK_5)  
  
-   [원격 데스크톱 세션을 사용 하 여 네트워크 컴퓨터에 연결](Manage-Devices-in-Windows-Server-Essentials.md#BKMK_7)  
  
-   [컴퓨터 속성 보기](Manage-Devices-in-Windows-Server-Essentials.md#BKMK_8)  
  
##  <a name="BKMK_1"></a>대시보드를 사용 하 여 디바이스 관리  
 Windows Server Essentials을 사용 하면 Windows Server Essentials 대시보드 사용 하 여 일반적인 관리 작업을 수행할 수 있습니다. **디바이스** 대시보드의 페이지에서 다음을 제공 합니다.  
  
-   표시 된 네트워크 컴퓨터의 목록 다음과 같습니다.  
  
    -   컴퓨터 이름  
  
    -   컴퓨터의 상태 중 **온라인** 또는 **오프 라인**  
  
    -   컴퓨터 설명  
  
    -   백업에서 컴퓨터의 상태  
  
    -   컴퓨터의 업데이트 상태  
  
    -   컴퓨터의 보안 상태  
  
    -   컴퓨터의 알림 상태  
  
    -   컴퓨터에 대 한 그룹 정책 정보  
  
-   세부 정보 창으로 선택 된 컴퓨터에 대 한 자세한 내용은  
  
-   컴퓨터 속성 및 경고 보기, 컴퓨터 백업 설정 백업에서 파일 및 폴더 복원을 등 디바이스 관리 작업 집합을 포함 하는 작업 창  
  
#### <a name="to-view-the-status-of-network-computers"></a>네트워크 컴퓨터의 상태를 확인 하려면  
  
1.  Windows Server Essentials 대시보드를 엽니다.  
  
2.  탐색 모음에서 클릭 **디바이스**합니다.  
  
3.  목록 창에서 네트워크의 모든 컴퓨터의 상태를 확인 합니다.  
  
 다음 표에 다양 한 컴퓨터 및 Windows Server Essentials 대시보드에서 사용할 수 있는 작업을 백업 합니다. 컴퓨터 관련 된 일부의 작업 하 고만 표시 된 목록에서 컴퓨터를 선택할 때.  
  
### <a name="computer-tasks-in-the-dashboard"></a>대시보드에 컴퓨터 작업  
  
|작업 이름|설명|  
|---------------|-----------------|  
|컴퓨터 속성 보기|선택한 컴퓨터에 대 한 일반 정보를 표시 하 고 컴퓨터 백업에 대 한 세부 정보를 볼 수 있습니다.|  
|이 컴퓨터에 대 한 백업 설정|설정 백업 마법사가 실행 됩니다.|  
|백업에서 컴퓨터에 대 한 사용자 지정|변경할 수 있습니다 선택된 된 컴퓨터에 대 한 백업 설정 백업 속성을 엽니다.|  
|컴퓨터에 대 한 백업을 시작합니다|선택한 컴퓨터에 대 한 백업을 시작합니다.|  
|컴퓨터에 대 한 백업 중지|선택한 컴퓨터에 대 한 백업을 중지합니다.|  
|파일 또는 폴더가 컴퓨터 복원|복원 파일 및 폴더 마법사 특정 파일, 폴더 또는 드라이브를 복원할 수 있도록 자동으로 실행 합니다.|  
|컴퓨터에 대 한 알림도 보기|중요 한 및 기타 정보 알림 표시 하 고 사용 가능한 경우 조치를 취할 수 있습니다.|  
|컴퓨터에 원격 데스크톱|선택한 컴퓨터에 원격 데스크톱 연결을 엽니다.|  
|컴퓨터에서 제거|Windows Server Essentials 대시보드에서 컴퓨터를 분리 하 컴퓨터 마법사를 제거를 실행 합니다.|  
|컴퓨터 백업 및 파일 히스토리 설정 사용자 지정|백업 설정 페이지에서를 변경할 수 있습니다 백업 일정 및 클라이언트에 대 한 파일 히스토리 설정으로 컴퓨터를 엽니다.|  
|컴퓨터 서버에 연결 하려면 어떻게 해야 하나요?|네트워크에는 컴퓨터에 참여 하기 위해 수행 하는 단계에 설명 도움말 항목을 엽니다.|  
|그룹 정책 구현|Windows 8 및 Windows 7 컴퓨터가 도메인에 가입 하는 정책 설정 적용 됩니다.|  
  
##  <a name="BKMK_2"></a>특정 네트워크 컴퓨터에 로그온 할 수 있는 사용자 계정에 할당  
 사용자에 게 로그온 할 수 있도록 특정 네트워크 컴퓨터에 Windows Server Essentials 네트워크 원격 위치에서에 액세스할 때 사용자 계정에 사용 권한을 지정할 수 있습니다.  
  
#### <a name="to-change-the-computer-access-for-a-user-account"></a>사용자 계정의 경우 컴퓨터 액세스를 변경 하려면  
  
1.  Windows Server Essentials 대시보드를 엽니다.  
  
2.  탐색 모음에서 클릭 **사용자**합니다.  
  
3.  사용자 계정의 목록에서 변경 하려면 사용자 계정을 선택 합니다.  
  
4.  에 **< 사용자 Account\ > 작업** 창 클릭 **계정 속성 보기**합니다. **속성** 페이지가 표시 되 면 사용자 계정의 합니다.  
  
5.  에 **컴퓨터 액세스** 탭을 선택이 사용자 원격으로 액세스할 수 있고 클릭 한 다음 컴퓨터 **확인**합니다.  
  
##  <a name="BKMK_3"></a>컴퓨터 서버에서 제거  
 컴퓨터를 Windows Server Essentials 대시보드를 사용 하 여 실행 하는 서버에서 제거 하면 더 이상 서버에서 관리 합니다. 결과적으로, 서버 컴퓨터 백업을 만드는 중지 하거나 네트워크에서 제거 그 후의 상태를 모니터링 합니다.  
  
> [!NOTE]
>  서버에서 컴퓨터의 제거 네트워크에서 컴퓨터를 끊지 않습니다. 컴퓨터에서 서버에 연결 하기 전에 수와 같은 방식으로 리소스에 액세스할 수 있습니다. 컴퓨터 서버 리소스에 액세스 하지 못하도록 및을 유선 도크를 분리 서버에서 컴퓨터에서 도메인 제거 해야 합니다. 또한 제거 서버에서 컴퓨터의 제거 되지 않습니다 자동으로 커넥터 소프트웨어 또는 실행 패드 제거 되는 컴퓨터에서. 컴퓨터에서 커넥터 소프트웨어를 수동으로 제거 해야 합니다. 자세한 내용은 섹션 참조에 커넥터 소프트웨어를 제거 [연결](../use/Get-Connected-in-Windows-Server-Essentials.md)합니다.  
  
#### <a name="to-remove-a-computer-from-the-network-by-using-the-dashboard"></a>네트워크에서 대시보드를 사용 하 여 컴퓨터를 제거 하려면  
  
1.  Windows Server Essentials 대시보드를 엽니다.  
  
2.  탐색 모음에서 클릭는 **디바이스** 탭 합니다.  
  
3.  컴퓨터의 목록에서 마우스 오른쪽 단추로 클릭 하는 네트워크에서 제거 하 고 클릭 한 다음 원하는 컴퓨터 **컴퓨터 제거**합니다.  
  
##  <a name="BKMK_5"></a>폴더 리디렉션 및 보안에 대 한 그룹 정책 설정을 구성합니다  
 그룹 정책을 구성 하 고 Windows Server Essentials 대시보드를 사용 하 여 Windows Server Essentials 네트워크의 컴퓨터에 배포할 수 있습니다. Windows Server Essentials의 그룹 정책을 영향을 미치는 Windows 업데이트에서 Windows Defender와 네트워크 방화벽 폴더 리디렉션 및 보안에 대 한 설정이 포함 됩니다.  
  
#### <a name="to-configure-group-policy-in-windows-server-essentials"></a>Windows Server Essentials에서 그룹 정책을 구성 하려면  
  
1.  Windows Server Essentials 대시보드를 엽니다.  
  
2.  탐색 모음에서 클릭 **디바이스**합니다.  
  
3.  Windows Server essentials: 전역에서 **사용자가 작업** 창 클릭 **구현 그룹 정책**합니다.  
  
     Windows Server essentials: 전역에서 **디바이스 작업** 창 클릭 **구현 그룹 정책**합니다.  
  
4.  구현 그룹 정책 마법사가 열립니다.  
  
5.  에 **폴더 리디렉션을 그룹 정책을 사용 하도록 설정** 페이지 마법사의 리디렉션합니다를 원하는 사용자 폴더를 선택할 수 있습니다.  
  
6.  에 **보안 정책 설정 사용** 페이지 마법사, 그룹 정책 설정에 대 한 사용 하도록 선택할 수 있습니다 **Windows 업데이트**, **Windows Defender**, 및 **네트워크 방화벽**합니다.  
  
7.  클릭 **완료** 그룹 정책 설정 구현할 수 있습니다.  
  
##  <a name="BKMK_7"></a>원격 데스크톱 세션을 사용 하 여 네트워크 컴퓨터에 연결  
 원격으로 액세스 하려면 Windows Server Essentials 네트워크 컴퓨터 사무실 밖에 있을 때 사용 웹 브라우저를 조직의 웹에 대 한 원격 액세스 웹 사이트에 로그온 할는 **컴퓨터** 탭에서 컴퓨터의 이름을 클릭 합니다.  
  
 **상태** 열 표시 네트워크의 컴퓨터에 연결할 수 있는 경우 및 다음 값 포함 될 수 있습니다.  
  
-   **사용 가능**  
  
     컴퓨터가 켜져 있고 원격 연결을 사용할 수 있습니다. 이 상태를 표시 하는 경우에 사용자 여전히 못할 제 3 자 방화벽을 차단 하는 연결 하는 경우이 컴퓨터에 연결 합니다.  
  
-   **오프 라인 상태 이거나 대기**  
  
     컴퓨터 꺼져 있거나 절전 또는 최대 절전 모드로 설정 되어 있습니다. 오프 라인 상태 이거나 대기 중인 컴퓨터 경우 컴퓨터를 사용할 수 없을 때 알 수 있도록 상태 실시간으로 업데이트 됩니다.  
  
-   **지원 되지 않는 운영 체제**  
  
     운영 체제 컴퓨터에서 원격 데스크톱을 지원 하지 않습니다. 서버에서 변경 되는 경우 업데이트를이 상태에 대 한 최장 6 시간까지 걸릴 수 있습니다.  
  
-   **연결 사용 안 함**  
  
     컴퓨터 연결이 방화벽으로 차단 또는 컴퓨터에서 또는 그룹 정책을 통해 원격 데스크톱에서 사용할 수 없습니다. 서버에서 변경 되는 경우 업데이트를이 상태에 대 한 최장 6 시간까지 걸릴 수 있습니다.  
  
##  <a name="BKMK_8"></a>컴퓨터 속성 보기  
 **디바이스** Windows Server Essentials 대시보드의 섹션 네트워크 컴퓨터 목록이 표시 됩니다. 또한 목록 각 컴퓨터에 대 한 추가 정보를 제공합니다.  
  
#### <a name="to-view-a-list-of-computers"></a>컴퓨터의 목록을 보려면  
  
1.  Windows Server Essentials 대시보드를 엽니다.  
  
2.  주 탐색 모음에서 클릭 **디바이스**합니다.  
  
3.  대시보드는 컴퓨터의 현재 목록이 표시 됩니다.  
  
#### <a name="to-view-or-change-properties-for-a-computer"></a>컴퓨터에 대 한 속성 보거나 변경 하려면  
  
1.  컴퓨터의 목록에서 보거나 속성을 변경 하려면 원하는 계정을 선택 합니다.  
  
2.  에 **< Computername\ > 작업** 창 클릭 **컴퓨터 속성 보기**합니다. **속성** 컴퓨터에 대 한 페이지가 나타납니다.  
  
3.  해당 컴퓨터에 대 한 속성을 표시 하려면 탭을 클릭 합니다.  
  
4.  컴퓨터 속성에 변경 내용을 저장 하려면 **적용**합니다.  
  
## <a name="see-also"></a>참조 하십시오  
  
-   [원격 Web Access 관리](Manage-Remote-Web-Access-in-Windows-Server-Essentials.md)  
  
-   [사용 하 여 원격 웹 액세스](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md)  
  
-   [대시보드를 사용 하 여 사용자 계정 관리](Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage8)  
  
-   [Windows Server Essentials 관리](Manage-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials을 사용 하 여](../use/Use-Windows-Server-Essentials.md)
