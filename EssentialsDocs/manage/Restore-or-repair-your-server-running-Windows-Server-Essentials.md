---
title: "복원 하거나 복구 Windows Server Essentials 실행 하는 서버"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 27bf6f24-30c4-4935-9b24-069eb43e22f4
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: e1ebc539928d13b0d34dfe5a0ee57ce6e98088e9
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="restore-or-repair-your-server-running-windows-server-essentials"></a>복원 하거나 복구 Windows Server Essentials 실행 하는 서버

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.
 
 이 항목 개요 및 절차를 복원 하거나 복구 Windows Server Essentials 실행 하는 서버에 대 한 지원 제공 하 고 다음 섹션에 포함 되어 있습니다.  
  
-   [서버 시스템 복원 개요](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_Overview)  
  
-   [복원 하거나 복구 시스템 드라이브](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_Restore)  
  
-   [서버에서 파일 및 폴더 복원](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_RestoreFilesAndFolders)  
  
##  <a name="BKMK_Overview"></a>서버 시스템 복원 개요  
 복원을 수행 하면 server의 상태에 사용할 수 있는 복원 방법에 영향을 하 고 수행할 수 있는 방법을 포괄적인 복원 합니다.  
  
 서버 복원 하는 가장 일반적인 이유는 다음과 같습니다.  
  
-   서버에 바이러스가 inoculated 하거나 삭제할 수 없습니다.  
  
-   서버 구성 설정을 불량, 되며 서버를 시작할 수 없습니다.  
  
-   시스템 드라이브를 대체 있습니다.  
  
-   서버를 사용 중지 되는 하 고 새 서버에 복원 해야 합니다.  
  
 백업에서 서버를 복원 하거나 또는 서버를 공장 기본 설정으로 복원할 수 있습니다.  
  
-   [서버 백업에서 복원](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_RestoreFromBackup)  
  
-   [서버를 공장 기본 설정으로 다시 설정](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_FactoryReset)  
  
###  <a name="BKMK_RestoreFromBackup"></a>서버 백업에서 복원  
 이 섹션 백업 선택 하려면 어떤 종류의 지침을 제공 합니다.  
  
 백업 사용할 수 있는 경우 서버 복원 하는 데 적합 외부 백업에서 복원 하 제조업체의 설치 미디어를 사용 하는 것입니다. 복원 서버 설정 및 폴더 선택 백업에서 복구 됩니다. 설정을 구성 하 고 데이터를 백업 후 생성 복원 하기만 하면 됩니다.  
  
 이전 백업에서 복원 하 여 서버 복구를 선택 하면 특정 백업을 복원, 원하는 선택 해야 하 고 서버에 직접 연결 된 외장형 하드 드라이브에 백업 유효한 파일 있어야:  
  
-   **서버 매우 최근 백업이 있는지**를 백업에 포함 된 모든 중요 한 데이터, 사용자가 선택한은 매우 간단 알 수 있습니다. 만 하면 마지막 좋은 백업 및 재구성 설정을 변경한 후 백업 후 작성 된 데이터는 다시 해야 합니다.  
  
-   **바이러스 있어서 서버를 복원 하는 경우**를 알고 있는 백업 바이러스를 받기 전에 발생 선택 합니다. 돌아가서 며칠 깨끗 백업을 선택 해야 할 수 있습니다.  
  
-   **잘못 구성 설정으로 인해 서버의 복원 하려는 경우**를 알고 있는 백업 설정 서버의 문제를 일으키는 변경 구성 이전 발생 선택 합니다.  
  
 백업에서 복원 하는 경우 정확한 프로세스와이 필요한 후속 조치의는 서버 및 시스템 드라이브 대체 여부 하드 드라이브의 수에 따라 다릅니다.  
  
-   **서버에 단일 하드 드라이브 및 드라이브 바뀌지 경우**, 서버 복원 하는 경우 드라이브 파티션 정보 그대로 유지 됩니다. 시스템 볼륨을 복원 하 고 남은 볼륨의 데이터를 그대로 유지 됩니다.  
  
-   **서버에 단일 하드 드라이브 및 드라이브 바뀝니다 경우**, 시스템 볼륨 복원 되 고, 데이터 볼륨 폴더 수동으로 복원 해야 합니다. 기본 아닌 공유 폴더 서버 저장소 다시 만들 때 만들어지지는 때문에를 만들어야 합니다.  
  
-   **서버에 여러 개의 하드 드라이브 및 드라이브 0 (시스템 볼륨 포함)는 바뀌지 경우**, 서버 복원 하는 경우 드라이브 파티션 정보 그대로 유지 됩니다. 시스템 볼륨 복원 되 고, 모든 남은 볼륨의 데이터를 그대로 유지 됩니다.  
  
-   **서버에 여러 개의 하드 드라이브 및 드라이브 0 (시스템 볼륨 포함)를 교체한 경우**, 시스템 볼륨 복원 되 고, 이전에 0 드라이브에 저장 된 모든 공유 폴더를 수동으로 복원 해야 합니다.  
  
###  <a name="BKMK_FactoryReset"></a>서버를 공장 기본 설정으로 다시 설정  
 백업을 보낸 사람 또는 든 원 하거나 필요한 이전 서버 구성 복원 하지 않고 전체 시스템 복원을 수행 하려면 몇 가지 이유로 복원할 수 없는 경우 설치 또는 복구 미디어를 서버 하드웨어 제조업체에서 사용 하 여 서버를 공장 기본 설정으로 다시 설정 하는 복구를 수행할 수 있습니다.  
  
 서버를 공장 기본 설정으로 다시 설정 하 여를 복원 하면 기존 설정과 서버에 설치 된 응용 프로그램이 삭제 되 고 서버를 다시 구성 해야 합니다. 공장 초기화 서버를 다시 시작 합니다.  
  
 공장 초기화를 수행 하면 데이터를 유지 하거나, 삭제 다음과 같은 효과를 선택할 수 있습니다.  
  
-   모든 데이터를 모두 데이터 유지 하려는 경우 시스템 볼륨을 삭제 되지만 다른 볼륨의 데이터 유지 됩니다.  
  
    > [!CAUTION]
    >  디스크 설정 기본 설정을 일치 하지 않는 경우 디스크에 있는 모든 데이터가 삭제 됩니다. 시스템 디스크를 교체 하는 경우 새 디스크 원래 디스크의 시스템 볼륨 보다 커야 합니다.  
    >   
    >  파티션 시스템 드라이브에 대 한 정보를 읽을 수 없거나 시스템 드라이브를 교체 하는 경우 시스템 드라이브에 있는 모든 데이터가 제거 되 모든 데이터를 유지 하려는 경우에 합니다.  
  
-   서버를 재활용 하거나 제거 하려는 경우 모든 사용자의 데이터를 삭제를 선택 합니다. 서버 구성, 다른 설정 및 시스템 볼륨 데이터 뿐만 아니라 다른 모든 데이터를 삭제 하 고 서버에 모든 하드 드라이브 변경 합니다.  
  
> [!NOTE]
>  저장소 공간 서버에 공장 초기화를 수행 하기 전에 구성 하는 경우 사용 해야는 **고급** 의 섹션은 **저장소 공간을 관리** 모든 저장소 공간을 수동으로 제거 하는 콘솔 합니다.  
  
 공장 초기화 한 후 다음 작업을 수행 해야 합니다.  
  
-   **합니다.** 서버에서 서버 구성 마법사를 사용 하 여 구성 설정을 다시 입력 합니다. 클라이언트 컴퓨터에서 원격으로 관리 되는 Windows Server Essentials 서버를 구성 하려면 웹 브라우저를 열고 입력 **http://***< YourServerName\ >* 주소 표시줄에 있습니다.  
  
-   **클라이언트는 서버에는 컴퓨터를 다시 연결 합니다.** 컴퓨터 서버에 연결 했던 경우 다시 컴퓨터 서버에 연결 하기 전에 컴퓨터에서 Windows Server Essentials 커넥터 소프트웨어를 제거 해야 합니다. 자세한 내용은 참조 [커넥터 소프트웨어를 제거](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_13) 및 [서버에 컴퓨터를 연결](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_9)합니다.  
  
##  <a name="BKMK_Restore"></a>복원 하거나 복구 시스템 드라이브  
 서버 복원이 첫 번째 단계를 복원 하거나 복구 서버 시스템 드라이브 하는 것입니다. 시스템 드라이브를 복원한 후 복원 복원에서 빠진 공유 하는 서버에 데이터 드라이브 복원 하는 데 필요한 무엇이 든 구입 해야 합니다.  
  
 복원을 수행 하는 데 사용할 수 있는 세 가지 방법은 다음과 같습니다.  
  
-   [복원 하거나 복구 설치 미디어를 사용 하 여 서버](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_Restore_1)합니다. 백업에서 복원 하는 서버 제조업체에서 설치 미디어를 사용 합니다.  
  
-   **설치 미디어를 사용 하 여 서버를 공장 기본 설정으로 복원 하려면**합니다. 서버에이 작업을 수행 하는 방법을 알아보려면 서버 제조업체의 설명서를 참조 하세요.  
  
-   [복원 또는 초기화 복구 DVD를 사용 하는 클라이언트 컴퓨터에서 서버](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_Restore_2)합니다. Windows Server Essentials 실행 하는 원격 관리 서버 복원 해야 할 경우 서버 제조업체에서 복원 DVD를 사용 하 여 클라이언트 컴퓨터에서 복원을 수행 해야 합니다.  
  
###  <a name="BKMK_Restore_1"></a>복원 하거나 복구 설치 미디어를 사용 하 여 서버  
 다음 절차는 Windows Server Essentials 설치 미디어를 사용 하 여 서버 시스템 드라이브에 백업에서 복원 하는 방법을 설명 합니다. (를 공장 기본 설정으로 복원 하 여 설치 미디어를 사용 하는 방법을 알아보려면 설명서를 참조 서버 제조업체에서.)  
  
> [!NOTE]
>  저장소 공간을 사용 하는 서버 새 서버에 데이터를 복원 하는 경우 먼저 시스템 드라이브에서 복구 하 고 Windows Server Essentials 대시보드에 로그온, 저장소 공간에는 이전 서버의 유사한 방식 구성를 찾습니다 데이터 볼륨 복구 합니다.  
  
##### <a name="to-restore-the-server-system-drive-from-a-backup-using-installation-media"></a>설치 미디어를 사용 하 여 백업에서 시스템 서버 드라이브를 복원 하려면  
  
1.  서버 DVD 드라이브에 Windows Server Essentials 설치 DVD 넣은 서버를 다시 시작한 다음 아무 키나에서 DVD를 시작 합니다.  
  
    > [!NOTE]
    >  복원 프로세스 자동으로 시작 되지 않는 경우 DVD 드라이브에서 부팅 메뉴 먼저 표시 되도록 서버에 대 한 BIOS 설정을 확인 합니다.  
  
     또는  
  
     제조업체 로드 서버에 설치 미디어를 시작 설치 미디어에서를 시작할 때 f8 키를 누릅니다.  
  
2.  Windows Server 후 파일 로드에서 언어와 다른 기본 설정을 선택 하 고 클릭 한 다음 **다음**합니다.  
  
3.  마법사의 다음 페이지, 클릭 **컴퓨터 복구**합니다.  
  
    > [!CAUTION]
    >  선택 하지 않으면는 **지금 설치** 옵션이 있습니다. 해당 옵션은 모두 구성 설정 및 시스템 드라이브의 모든 데이터를 삭제 하는 전체 시스템 설치를 안내 합니다.  
  
4.  에 **옵션을 선택** 페이지, 클릭 **문제 해결**합니다.  
  
5.  에 **시스템 이미지 복구** 페이지에서 현재 선택? 중 하나 **Windows Server Essentials** 또는 **Windows Server Essentials**합니다.  
  
     컴퓨터가 다시 이미지 마법사가 열립니다.  
  
6.  에 **시스템 이미지 백업 선택** 최신 백업을 사용 하도록 선택할 수 페이지에서 나 이전 백업 선택할 수 있습니다. 시스템 복원 또는 수리 서버에 사용자가 선택한 백업 시에 포함 되어 상태로 복원 됩니다. 추가 하는 데이터 나 설정의 백업을 저장 된 후에 수행 된 변경 내용 다시 만들어야 합니다.  
  
     다음 옵션 중 하나를 선택 하 고 클릭 한 다음 **다음**:  
  
    -   **(권장) 최신 사용할 수 있는 시스템 이미지를 사용 하 여**  
  
    -   **시스템 이미지를 선택 합니다.**  
  
    > [!NOTE]
    >  서버, 최근 매우 성공적으로 백업 하는 경우 백업을 모든 중요 한 데이터를가지고 있는지 알아야 사용자가 선택한은 매우 간단 합니다. 만 하면 마지막 좋은 백업 및 재구성 설정을 변경한 후 백업 후 작성 된 데이터는 다시 해야 합니다.  
    >   
    >  바이러스 있어서 서버를 복원 하는 경우 바이러스를 받기 전에 발생 알고 있는 백업을 선택 합니다. 돌아가서 며칠 깨끗 백업을 선택 해야 할 수 있습니다.  
    >   
    >  잘못 구성 설정으로 인해 서버의 복원 하는 경우 발생 하는 문제를 일으키는 구성 설정 변경 하기 전에 알아야 백업을 선택 합니다.  
  
7.  시스템 복원이 완료 하 고 마법사의 지침을 따릅니다.  
  
8.  서버를 성공적으로 복원 하나를 사용 하는 경우 설치 DVD를 제거 하 고 서버를 다시 시작 합니다.  
  
> [!NOTE]
>  복원 하는 서버에 폴더 공유 추가 단계를 수행 해야 할 수 있습니다. 자세한 내용은 참조 [서버에서 파일 및 폴더 복원을](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_RestoreFilesAndFolders)합니다.  
  
###  <a name="BKMK_Restore_2"></a>복원 하거나 복구 DVD를 사용 하는 클라이언트 컴퓨터에서 서버를 다시 설정  
 Windows Server Essentials의 시작할 수 서버 부팅 가능한 USB 플래시 드라이브에서 사용자가 만든 있고 시간 서버 클라이언트 컴퓨터에서 DVD 서버 제조업체에서 제공한 복구를 사용 하 여 복구할 수 있습니다. 클라이언트 컴퓨터 서버와 같은 네트워크에 포함 되어 있어야 합니다. 이 방법은 Windows Server Essentials에서 사용할 수 없습니다.  
  
 다음 절차 서버 복원을 수행 하기 위한 일반 단계를 제공 합니다. 단계는 동일 하 게 적용 백업에서 복원을 수행 해도 또는 공장 기본 설정으로 복원 합니다. 더 자세한 지침 서버 제조업체에서 설명서를 참조 하세요.  
  
##### <a name="to-restore-or-reset-the-server-from-a-client-computer-using-the-recovery-dvd"></a>복원 하거나 복구 DVD를 사용 하는 클라이언트 컴퓨터에서 서버를 초기화 하려면  
  
1.  서버 클라이언트 컴퓨터에서 제조업체에서 받은 Windows Server Essentials 서버 복구 미디어를 삽입 합니다.  
  
     서버 복구할 마법사가 열립니다.  
  
2.  서버 복구 모드로 시작 하는 데 사용할 수 있는 부팅 가능한 USB 플래시 드라이브를 만들 수 마법사의 지침을 따릅니다.  
  
3.  부팅 가능한 USB 플래시 드라이브를 준비 하는 서버 복구 마법사, 후 서버에서 플래시 드라이브를 삽입 하 고 복구 모드로 서버를 시작 합니다. 서버 복구 모드로 시작 하는 방법을 알아보려면 서버 하드웨어 제조업체에서 설명서를 참조 합니다.  
  
     서버를 복구 모드로 시작한 후 서버 복구 마법사 서버를 찾아 연결을 설정 합니다.  
  
4.  서버 복원이 완료 하 고 마법사의 지침을 따릅니다.  
  
> [!NOTE]
>  이러한 서버 복구이 방법은 복구 하는 동안 서버에 연결 되어 있는 외부 저장 디바이스를 무시 합니다. 외부 저장 장치에 데이터를 지우려는 수동으로 이렇게 해야 하면 됩니다.  
  
> [!NOTE]
>  백업에서 데이터를 복원 하면 서버에 추가 공유 폴더를 만든 경우 서버에서 추가 공유 폴더 인식 되지 않을 수 있습니다. 해당 폴더를 다시 공유 해야 합니다. 자세한 내용은 참조 [서버에서 파일 및 폴더 복원을](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_RestoreFilesAndFolders)합니다.  
  
##  <a name="BKMK_RestoreFilesAndFolders"></a>서버에서 파일 및 폴더 복원  
 복원 하거나 복구 하면 서버 하는 데 사용 하 고 저장소 서버 유형을 사용 하는 방법에 따라 시스템 드라이브를 복원한 후 데이터 볼륨을 복구 해야 할 수 있습니다. 어떤 경우에 폴더를 공유 기존 다시 서버 인식 하 않도록 할 수 있습니다.  
  
 다음은 파일 및 폴더를 복원 해야 할 수도 때의 몇 가지 예입니다.  
  
-   [서버 백업에서 파일 및 폴더를 복원](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_RestoreFilesFromBackup)합니다. 시스템 디스크 대체 또는 시스템 디스크에 파티션이 정보를 읽을 수 없는 경우, 시스템 복원할 수 있지만 다른 볼륨의이 디스크에서 데이터를 복원할 수 없습니다. 복원할 파일 및 폴더 마법사를 사용 하 여 다른 데이터 볼륨을 파일 및 폴더를 복원 하려면 해야 합니다.  
  
-   [서버에서 공유 폴더를 복원](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_ConfigreSharedFolders)합니다. 만든 경우 공유 폴더를 추가 서버에 백업에서 시스템 드라이브를 복원한 후, 공유 폴더 데이터 파티션에 여전히 또는 데이터 파티션에 복원 된 있지만 서버에서 인식 하지 않을 수 있습니다. 해당 폴더를 다시 공유 해야 합니다.  
  
###  <a name="BKMK_RestoreFilesFromBackup"></a>서버 백업에서 파일 및 폴더를 복원  
 복원할 파일 및 폴더 마법사 하드 디스크의 작동이 중지 또는 실수로 파일 삭제 된 경우 데이터를 보호 하는 데 도움이 됩니다. Windows Server Essentials 백업을 사용 하 여 모든 데이터의 복사본 하드 드라이브에 만들고 외부 저장 장치에 데이터를 저장할 수 있습니다. 하드 드라이브에 원래 데이터가 삭제 실수로 하거나 덮어쓰거나 장으로 액세스할 수 없게 없으면 백업에서 데이터를 복원할 수 있습니다. 복원할 파일 또는 폴더 마법사 하나의 파일 또는 폴더, 여러 파일 또는 폴더 또는 전체 하드 드라이브가 기존 백업에서 복원 하는 데 도움이 됩니다.  
  
 시스템 복원을 후 복원할 파일 및 폴더 마법사 복원할 파일 및 폴더를 복원 하는 동안 유지 되지 않았습니다를 사용 하 여 해야 할 수 있습니다. 예를 들어, 시스템 디스크 대체 또는 시스템 디스크에 파티션이 정보를 읽을 수 없는 경우 데이터가 다른 볼륨 시스템 디스크에서 복원할 수 없습니다.  
  
> [!NOTE]
>  전체 시스템 드라이브를 복원 하려면 복원 된 파일 및 폴더 마법사를 사용할 수 없습니다. 전체 시스템을 복원 하는 방법에 대 한 정보를 참조 하세요. [복원 하거나 설치 미디어를 사용 하 여 서버 복구](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_Restore_1) 또는 [복원 하거나 복구 DVD를 사용 하는 클라이언트 컴퓨터에서 서버를 다시 설정](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_Restore_2)합니다.  
  
##### <a name="to-restore-files-and-folders-from-a-server-backup"></a>서버 백업에서 파일 및 폴더를 복원 하려면  
  
1.  Windows Server Essentials 대시보드 열고 클릭는 **디바이스** 탭 합니다.  
  
2.  서버를 이름을 클릭 한 다음 클릭 **복원할 파일 또는 폴더에 대 한 서버** 에 **작업** 창 합니다.  
  
     복원할 파일 및 폴더 마법사가 열립니다.  
  
3.  파일 또는 폴더를 복원 하 고 마법사의 지침을 따릅니다.  
  
> [!WARNING]
>  백업 및 복원 파일 및 폴더에 대 한 자세한 내용은 참조 [관리 백업 및 복원](Manage-Backup-and-Restore-in-Windows-Server-Essentials.md)합니다.  
  
###  <a name="BKMK_ConfigreSharedFolders"></a>서버에서 공유 폴더를 복원  
 공유 폴더 데이터 파티션에 여전히 또는 데이터 파티션에 복원 된 경우 s 서버 시스템 드라이브를 복원한 후 공유 폴더를 다시 폴더를 인식 하는 서버에 대 한 순서를 구성 해야 할 수 있습니다. 다음 절차 하기 전에 공유 된 공유 폴더를 추가 하는 방법을 설명 합니다.  
  
##### <a name="to-add-an-existing-folder-to-the-server-shared-folders"></a>서버에 기존 폴더를 추가 하려면 폴더를 공유  
  
1.  파일 탐색기의 하드 드라이브의 공유 폴더를 찾습니다.  
  
2.  공유 폴더를 마우스 오른쪽 단추로 클릭, **속성**를 클릭는 **공유** 탭을 클릭 한 다음 폴더 권한을 적어 둡니다.  
  
3.  Windows Server Essentials 대시보드에 로그온, 클릭는 **저장소** 탭을 클릭 한 다음 **폴더를 추가** 에 **서버 폴더 작업** 창 합니다.  
  
     추가 폴더 마법사가 열립니다.  
  
4.  공유에 대해 이름을 입력 하 고 **이름** 상자 합니다.  
  
5.  클릭 **검색**로 이동 *< drive\ > \\ < ServerName\ >*\ServerFolders (예를 들어 *d:\Contoso\ServerFolders*)를 공유 하 고 클릭 한 다음 원하는 폴더 선택 **확인**합니다.  
  
6.  클릭 **다음**합니다.  
  
7.  2 단계에서 적어 권한이 지정 하 고 클릭 **폴더 추가**합니다.  
  
    > [!IMPORTANT]
    >  이러한 권한은 되지 Windows Server Essentials 대시보드 사용 하 여 폴더에 추가 된 기존 권한을 바뀝니다.  
  
> [!IMPORTANT]
>  목록이 공유 폴더에 폴더 추가 마치면 폴더 서버 백업을에 포함 되어 있는지 확인 합니다. 서버 백업에 폴더 추가 대 한 정보를 참조 하세요. [설정 또는 사용자 지정 서버 백업](Set-up-or-customize-server-backup.md)합니다.  
  
## <a name="see-also"></a>참조 하십시오  
  
-   [관리 백업 및 복원](Manage-Backup-and-Restore-in-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials 관리](Manage-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials을 사용 하 여](../use/Use-Windows-Server-Essentials.md)
