---
title: Windows Server Essentials를 실행하는 서버 복원 또는 복구
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
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
ms.openlocfilehash: bb3cc834e0ab6641c14f5e9fbb6afe5c9f187c7c
ms.sourcegitcommit: e40fce7b8b4bc0bef278e676435306f14078cf00
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/05/2019
ms.locfileid: "68787168"
---
# <a name="restore-or-repair-your-server-running-windows-server-essentials"></a>Windows Server Essentials를 실행하는 서버 복원 또는 복구

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials
 
 이 항목에서는 Windows Server Essentials를 실행 하는 서버를 복원 또는 복구 하기 위한 개요와 지원 절차를 제공 하며 다음 섹션을 포함 합니다.  
  
-   [서버 시스템 복원 개요](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_Overview)  
  
-   [시스템 드라이브 복원 또는 복구](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_Restore)  
  
-   [서버의 파일 및 폴더 복원](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_RestoreFilesAndFolders)  
  
##  <a name="BKMK_Overview"></a>서버 시스템 복원 개요  
 복원을 수행할 때 서버 상태는 사용할 수 있는 복원 방법과 수행할 수 있는 복원이 포괄적인 정도에 영향을 줍니다.  
  
 서버를 복원하는 가장 일반적인 원인은 다음과 같습니다.  
  
- 서버의 바이러스를 예방하거나 삭제할 수 없습니다.  
  
- 서버 구성 설정이 잘못되어 서버를 시작할 수 없습니다.  
  
- 시스템 드라이브를 교체했습니다.  
  
- 서버를 사용 중지하고 새 서버에 복원하려고 합니다.  
  
  백업에서 서버를 복원하거나 서버를 공장 기본 설정으로 복원할 수 있습니다.  
  
- [백업에서 서버 복원](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_RestoreFromBackup)  
  
- [서버를 공장 기본 설정으로 다시 설정](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_FactoryReset)  
  
###  <a name="BKMK_RestoreFromBackup"></a>백업에서 서버 복원  
 이 섹션에서는 어떤 유형의 백업을 선택할지에 대한 지침을 제공합니다.  
  
 백업을 사용할 수 있는 경우 서버를 복원 하는 가장 좋은 방법은 제조업체의 설치 미디어를 사용 하 여 외부 백업에서 복원 하는 것입니다. 복원하면 선택한 백업에서 서버 설정 및 폴더가 복구됩니다. 백업 후 만들어진 설정을 구성하고 데이터를 복원하기만 하면 됩니다.  
  
 이전 백업에서 복원하여 서버를 복구하려는 경우 복원하려는 특정 백업을 선택해야 하며, 서버에 직접 연결된 외부 하드 드라이브에 유효한 백업 파일이 있어야 합니다.  
  
- **매우 최근에 성공적으로 수행한 서버의 백업이 있고**, 백업에 중요한 모든 데이터가 포함되어 있음을 아는 경우 선택은 매우 간단합니다. 마지막 양호한 백업 후에 만들어진 데이터를 다시 만들고 백업 후에 수행된 설정 변경을 다시 구성하기만 하면 됩니다.  
  
- **바이러스로 인해 서버를 복원하는 경우** 바이러스를 받기 전에 발생한 알고 있는 백업을 선택합니다. 감염되지 않은 백업을 선택하기 위해 며칠을 거슬러 올라가야 할 수도 있습니다.  
  
- **잘못된 구성 설정으로 인해 서버를 복원하는 경우** 서버에서 문제를 발생시킨 구성 설정 변경 이전에 수행된 알고 있는 백업을 선택합니다.  
  
  백업에서 복원할 때 정확한 프로세스 및 필요한 추가 작업은 서버에 있는 하드 드라이브의 수와 시스템 드라이브가 교체되었는지 여부에 따라 다릅니다.  
  
- **서버에 단일 하드 드라이브가 있고 드라이브가 교체되지 않은 경우** 서버 복원 시 드라이브 파티션 정보는 원래대로 유지됩니다. 시스템 볼륨이 복원되고, 나머지 볼륨의 데이터는 보존됩니다.  
  
- **서버에 단일 하드 드라이브가 있고 드라이브가 교체된 경우** 시스템 볼륨이 복원된 후 수동으로 폴더를 데이터 볼륨으로 복원해야 합니다. 모든 비기본 공유 폴더는 서버 저장소가 다시 만들어질 때 만들어지지 않으므로 수동으로 만들어야 합니다.  
  
- **서버에 여러 하드 드라이브가 있고 드라이브 0(시스템 볼륨이 포함되어 있음)이 교체되지 않은 경우**서버 복원 시 드라이브 파티션 정보는 원래대로 유지됩니다. 시스템 볼륨이 복원되고, 나머지 모든 볼륨의 데이터는 보존됩니다.  
  
- **서버에 여러 하드 드라이브가 있고 드라이브 0(시스템 볼륨이 포함되어 있음)이 교체된 경우**시스템 볼륨이 복원된 후 이전에 드라이브 0에 저장된 모든 공유 폴더를 수동으로 복원해야 합니다.  
  
###  <a name="BKMK_FactoryReset"></a>서버를 공장 기본 설정으로 다시 설정  
 복원할 수 있는 백업이 없거나 다른 이유로 인해 이전 서버 구성을 복원하지 않고 전체 시스템 복원을 수행하려고 하거나 수행해야 하는 경우, 서버 하드웨어 제조업체의 설치 또는 복구 미디어를 사용하여 서버를 공장 기본 설정으로 다시 설정하는 복원을 수행할 수 있습니다.  
  
 공장 기본 설정으로 다시 설정하여 서버를 복원하는 경우 모든 기존 설정 및 서버에 설치된 응용 프로그램이 삭제되므로 서버를 다시 구성해야 합니다. 공장 기본 설정 후에는 서버가 다시 시작됩니다.  
  
 공장 기본 설정을 수행할 때 데이터를 유지하거나 삭제하도록 선택할 수 있으며, 각각의 경우 영향은 다음과 같습니다.  
  
-   모든 데이터를 유지하도록 선택하는 경우 시스템 볼륨의 모든 데이터는 삭제되지만 다른 볼륨의 데이터는 보존됩니다.  
  
    > [!CAUTION]
    >  디스크 설정이 기본 설정과 일치하지 않으면 디스크에 있는 모든 데이터가 삭제됩니다. 시스템 디스크를 교체한 경우 새 디스크가 원본 디스크의 시스템 볼륨 보다 커야 합니다.  
    >   
    >  시스템 드라이브에 대한 파티션 정보를 읽을 수 없거나 시스템 드라이브를 교체하는 경우 시스템 드라이브의 모든 데이터는 모든 데이터를 유지하도록 선택할 경우에도 제거됩니다.  
  
-   서버를 서비스 해제하거나 용도를 변경하는 경우 모든 데이터를 삭제하도록 선택합니다. 서버 구성, 기타 설정 및 시스템 볼륨의 데이터 외에, 다른 모든 데이터는 삭제되고 서버의 모든 하드 드라이브가 다시 포맷됩니다.  
  
> [!NOTE]
>  서버에 저장소 공간이 구성되어 있는 경우 공장 기본 설정을 수행하기 전에 **저장소 공간 관리** 콘솔의 **고급** 섹션을 사용하여 모든 저장소 공간을 수동으로 제거해야 합니다.  
  
 공장 기본 설정 후에는 다음 작업을 수행해야 합니다.  
  
-   **서버 다시 구성.** 서버에서 서버 구성 마법사를 사용하여 구성 설정을 다시 입력합니다. 클라이언트 컴퓨터에서 원격으로 관리 되는 Windows server Essentials 서버를 구성 하려면 웹 브라우저를 열고 주소 표시줄에 **http://** _< 서버 이름\>_  를 입력 합니다.  
  
-   **서버에 클라이언트 컴퓨터 다시 연결.** 컴퓨터가 이전에 서버에 연결 된 경우 컴퓨터를 서버에 다시 연결 하기 전에 컴퓨터에서 Windows Server Essentials Connector 소프트웨어를 제거 해야 합니다. 자세한 내용은 [Uninstall the Connector software](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_13) 및 [Connect computers to the server](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_9)을 참조하세요.  
  
##  <a name="BKMK_Restore"></a>시스템 드라이브 복원 또는 복구  
 서버 복원의 첫 번째 단계는 서버 시스템 드라이브를 복원하거나 복구하는 것입니다. 시스템 드라이브를 복원한 후에는 서버의 데이터 드라이브를 복원하고 복원에서 손실된 모든 공유를 복원하는 데 필요한 모든 작업을 수행합니다.  
  
 다음과 같은 세 가지 방법을 사용하여 복원을 수행할 수 있습니다.  
  
-   [설치 미디어를 사용하여 서버 복원 또는 복구](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_Restore_1). 서버 제조업체의 설치 미디어를 사용하여 백업에서 복원합니다.  
  
-   **설치 미디어를 사용하여 서버를 기본 공장 설정으로 복원**. 서버에서 이렇게 하는 방법을 알아보려면 서버 제조업체의 설명서를 참조하세요.  
  
-   [복구 DVD를 사용하여 클라이언트 컴퓨터에서 서버 복원 또는 다시 설정](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_Restore_2). Windows Server Essentials를 실행 하는 원격 관리 서버를 복원 해야 하는 경우 서버 제조업체의 복원 DVD를 사용 하 여 클라이언트 컴퓨터에서 복원을 수행 해야 합니다.  
  
###  <a name="BKMK_Restore_1"></a>설치 미디어를 사용 하 여 서버 복원 또는 복구  
 다음 절차에서는 Windows Server Essentials 설치 미디어를 사용 하 여 백업에서 서버 시스템 드라이브를 복원 하는 방법에 대해 설명 합니다. (설치 미디어를 사용하여 공장 기본 설정으로 복원하는 방법을 알아보려면 서버 제조업체의 설명서를 참조하세요.)  
  
> [!NOTE]
>  서버에서 저장소 공간을 사용 하는 경우 데이터를 새 서버로 복원 하려면 먼저 시스템 드라이브를 복구한 다음 Windows Server Essentials 대시보드에 로그온 하 고 이전 서버에서와 비슷한 방법으로 저장소 공간을 구성한 후 dat를 복구 해야 합니다. 볼륨.  
  
##### <a name="to-restore-the-server-system-drive-from-a-backup-using-installation-media"></a>설치 미디어를 사용하여 백업에서 서버 시스템 드라이브를 복원하려면  
  
1.  서버 DVD 드라이브에 Windows Server Essentials 설치 DVD를 삽입 하 고 서버를 다시 시작한 후 아무 키나 눌러 DVD에서 시작 합니다.  
  
    > [!NOTE]
    >  복원 프로세스가 자동으로 시작되지 않으면 서버의 BIOS 설정을 확인하여 DVD 드라이브가 부팅 메뉴에 첫 번째로 표시되는지 확인합니다.  
  
     -또는-  
  
     제조업체가 서버에 설치 미디어를 미리 로드한 경우 시작 시 F8 키를 눌러 설치 미디어에서 시작합니다.  
  
2.  Windows Server 파일이 로드되고 나면 언어 및 기타 기본 설정을 선택하고 **다음**을 클릭합니다.  
  
3.  마법사의 다음 페이지에서 **컴퓨터 복구**를 클릭합니다.  
  
    > [!CAUTION]
    >  **지금 설치** 옵션은 선택하지 마세요. 해당 옵션은 모든 구성 설정 및 시스템 드라이브의 모든 데이터를 삭제하는 전체 시스템 설치를 안내합니다.  
  
4.  **옵션 선택** 페이지에서 **문제 해결**을 클릭합니다.  
  
5.  **시스템 이미지 복구** 페이지에서 현재 시스템을 선택 하 고, **windows Server Essentials** 또는 **windows server essentials**중 하나를 선택 합니다.  
  
     이미지로 컴퓨터 다시 설치 마법사가 열립니다.  
  
6.  **시스템 이미지 백업을 선택합니다.** 페이지에서 최신 백업을 사용하도록 선택하거나 이전 백업을 선택할 수 있습니다. 시스템이 서버 복원 또는 복구를 위해 선택한 백업 당시의 상태로 복원됩니다. 백업이 저장된 후 추가된 데이터나 수행된 설정 변경 내용을 다시 만들어야 합니다.  
  
     다음 옵션 중 하나를 선택한 후 **다음**을 클릭합니다.  
  
    -   **사용 가능한 최신 시스템 이미지 사용(권장)**  
  
    -   **시스템 이미지 선택**  
  
    > [!NOTE]
    >  매우 최근에 성공적으로 수행한 서버의 백업이 있고, 백업에 중요한 모든 데이터가 포함되어 있음을 아는 경우 선택은 매우 간단합니다. 마지막 양호한 백업 후에 만들어진 데이터를 다시 만들고 백업 후에 수행된 설정 변경을 다시 구성하기만 하면 됩니다.  
    >   
    >  바이러스로 인해 서버를 복원하는 경우 바이러스를 받기 전에 발생한 알고 있는 백업을 선택합니다. 감염되지 않은 백업을 선택하기 위해 며칠을 거슬러 올라가야 할 수도 있습니다.  
    >   
    >  잘못된 구성 설정으로 인해 서버를 복원하는 경우 서버에서 문제를 발생시킨 구성 설정 변경 이전에 수행된 알고 있는 백업을 선택합니다.  
  
7.  마법사의 지침에 따라 시스템 복원을 완료합니다.  
  
8.  서버가 복원되고 나면 설치 DVD를 제거한 후(설치 DVD를 사용한 경우) 서버를 다시 시작합니다.  
  
> [!NOTE]
>  서버의 폴더를 복원 및 공유하려면 추가 단계를 수행해야 할 수 있습니다. 자세한 내용은 [Restore files and folders on the server](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_RestoreFilesAndFolders)를 참조하세요.  
  
###  <a name="BKMK_Restore_2"></a>복구 DVD를 사용 하 여 클라이언트 컴퓨터에서 서버 복원 또는 다시 설정  
 Windows Server Essentials에서는 사용자가 만든 부팅 가능 USB 플래시 드라이브에서 서버를 시작한 후 서버 제조업체에서 받은 복구 DVD를 사용 하 여 클라이언트 컴퓨터에서 서버를 복구할 수 있습니다. 클라이언트 컴퓨터는 서버와 동일한 네트워크에 있어야 합니다. 이 방법은 Windows Server Essentials에서 사용할 수 없습니다.  
  
 다음 절차에서는 서버 복원을 수행하는 일반적인 단계를 설명합니다. 단계는 백업에서 복원하는 경우나 공장 기본 설정으로 복원하는 경우에 동일하게 적용됩니다. 보다 구체적인 지침은 서버 제조업체의 설명서를 참조하세요.  
  
##### <a name="to-restore-or-reset-the-server-from-a-client-computer-using-the-recovery-dvd"></a>복구 DVD를 사용하여 클라이언트 컴퓨터에서 서버를 복원 또는 다시 설정하려면  
  
1.  서버 제조업체에서 받은 Windows Server Essentials Server 복구 미디어를 클라이언트 컴퓨터에 삽입 합니다.  
  
     서버 복구 마법사가 열립니다.  
  
2.  마법사의 지침에 따라 서버를 복구 모드로 시작하는 데 사용할 부팅 가능 USB 플래시 드라이브를 만듭니다.  
  
3.  서버 복구 마법사가 부팅 가능 USB 플래시 드라이브를 준비하고 나면 서버에 플래시 드라이브를 삽입하고 서버를 복구 모드로 시작합니다. 서버를 복구 모드로 시작하는 방법을 알아보려면 서버 하드웨어 제조업체의 설명서를 참조하세요.  
  
     서버를 복구 모드로 시작하고 나면 서버 복구 마법사가 서버를 찾은 후 연결을 설정합니다.  
  
4.  마법사의 지침에 따라 설치 복원을 완료합니다.  
  
> [!NOTE]
>  이 서버 복구 방법에서는 복구하는 동안 서버에 연결된 외부 저장 장치를 무시합니다. 외부 저장 장치에 있는 데이터를 지우려면 수동으로 지워야 합니다.  
  
> [!NOTE]
>  서버에 추가 공유 폴더를 만든 경우 백업에서 데이터를 복원하고 나면 서버에서 추가 공유 폴더가 인식되지 않을 수 있습니다. 해당 폴더를 다시 공유해야 합니다. 자세한 내용은 [Restore files and folders on the server](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_RestoreFilesAndFolders)를 참조하세요.  
  
##  <a name="BKMK_RestoreFilesAndFolders"></a>서버의 파일 및 폴더 복원  
 서버를 복원 또는 복구하는 데 사용한 방법과 서버에 사용되는 저장소 유형에 따라, 시스템 드라이브를 복원한 후 데이터 볼륨을 복구해야 할 수 있습니다. 일부 경우에는 서버에서 기존 폴더를 인식하도록 해당 폴더를 다시 공유해야 할 수 있습니다.  
  
 다음은 파일 및 폴더를 복원해야 할 수 있는 몇 가지 예입니다.  
  
-   [서버 백업에서 파일 및 폴더 복원](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_RestoreFilesFromBackup). 시스템 디스크를 교체했거나 시스템 디스크의 파티션 정보를 읽을 수 없는 경우 시스템을 복원할 수 있지만 이 디스크에 있는 다른 볼륨의 데이터는 복원할 수 없습니다. 다른 데이터 볼륨의 파일 및 폴더를 복원하려면 파일 및 폴더 복원 마법사를 사용해야 합니다.  
  
-   [Restore shared folders on the server](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_ConfigreSharedFolders)을 차례로 클릭합니다. 서버에 추가 공유 폴더를 만든 경우 백업에서 시스템 드라이브를 복원하고 나면 공유 폴더는 여전히 데이터 파티션에 있거나 데이터 파티션으로 복원되었지만 서버에서 인식되지 않을 수 있습니다. 해당 폴더를 다시 공유해야 합니다.  
  
###  <a name="BKMK_RestoreFilesFromBackup"></a>서버 백업에서 파일 및 폴더 복원  
 파일 및 폴더 복원 마법사를 사용하면 하드 디스크의 작동이 중지되거나 파일이 실수로 지워진 경우 데이터를 보호하는 데 도움이 됩니다. Windows Server Essentials Backup을 사용 하면 하드 드라이브에 있는 모든 데이터의 복사본을 만들고 외부 저장 장치에 데이터를 저장할 수 있습니다. 하드 드라이브에 있는 원래 데이터가 실수로 지워지거나, 덮어써지거나, 오작동으로 인해 액세스 불가능하게 되는 경우 백업에서 데이터를 복원할 수 있습니다. 파일 또는 폴더 복원 마법사를 사용하면 기존 백업에서 단일 파일 또는 폴더, 여러 파일 또는 폴더나 전체 하드 드라이브를 복원할 수 있습니다.  
  
 시스템을 복원한 후 파일 및 폴더 복원 마법사를 사용하여, 복원하는 동안 보존되지 않았던 파일 및 폴더를 복원해야 할 수 있습니다. 예를 들어 시스템 디스크를 교체했거나 시스템 디스크의 파티션 정보를 읽을 수 없는 경우 시스템 디스크에 있는 다른 볼륨의 데이터를 복원할 수 없습니다.  
  
> [!NOTE]
>  파일 및 폴더 복원 마법사를 사용하여 전체 시스템 드라이브를 복원할 수는 없습니다. 전체 시스템을 복원 하는 방법에 대 한 정보를 참조 하세요 [복원 하거나 설치 미디어를 사용 하 여 서버를 복구](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_Restore_1) 또는 [복원 또는 복구 DVD를 사용 하 여 클라이언트 컴퓨터에서 서버를 다시 설정](Restore-or-repair-your-server-running-Windows-Server-Essentials.md#BKMK_Restore_2)합니다.  
  
##### <a name="to-restore-files-and-folders-from-a-server-backup"></a>서버 백업에서 파일 및 폴더를 복원하려면  
  
1.  Windows Server Essentials 대시보드를 열고 **장치** 탭을 클릭 합니다.  
  
2.  서버 이름을 클릭하고 **작업** 창에서 **서버에 대한 파일 또는 폴더 복원**을 클릭합니다.  
  
     파일 및 폴더 복원 마법사가 열립니다.  
  
3.  마법사의 지침에 따라 파일이나 폴더를 복원합니다.  
  
> [!WARNING]
>  파일과 폴더를 백업 하 고 복원 하는 방법에 대 한 자세한 내용은 [백업 및 복원 관리](Manage-Backup-and-Restore-in-Windows-Server-Essentials.md)를 참조 하세요.  
  
###  <a name="BKMK_ConfigreSharedFolders"></a>서버의 공유 폴더 복원  
 서버의 시스템 드라이브를 복원한 후 공유 폴더가 여전히 데이터 파티션에 있거나 데이터 파티션으로 복원 된 경우 서버에서 폴더를 인식할 수 있도록 공유 폴더를 다시 구성 해야 할 수 있습니다. 다음 절차에서는 이전에 공유된 공유 폴더를 추가하는 방법을 설명합니다.  
  
##### <a name="to-add-an-existing-folder-to-the-server-shared-folders"></a>서버 공유 폴더에 기존 폴더를 추가하려면  
  
1.  파일 탐색기에서 하드 드라이브의 공유 폴더를 찾습니다.  
  
2.  공유 폴더를 마우스 오른쪽 단추로 클릭하고 **속성**, **공유** 탭을 차례로 클릭한 후 폴더 사용 권한을 기록해 둡니다.  
  
3.  Windows Server Essentials 대시보드에 로그온 하 고 **저장소** 탭을 클릭 한 다음 **서버 폴더 작업** 창에서 **폴더 추가** 를 클릭 합니다.  
  
     폴더 추가 마법사가 열립니다.  
  
4.  **이름** 상자에 공유의 이름을 입력합니다.  
  
5.  **찾아보기**를 클릭 하 *< 드라이브\>\\<\>ServerName*\serverfolders (예: *: d:\contoso\serverfolders*)로 이동 하 고 공유 하려는 폴더를 선택한 다음 **확인**을 클릭 합니다.  
  
6.  **다음**을 클릭합니다.  
  
7.  2단계에서 기록해 두었던 사용 권한을 지정한 후 **폴더 추가**를 클릭합니다.  
  
    > [!IMPORTANT]
    >  이러한 사용 권한은 Windows Server Essentials 대시보드를 사용 하 여 폴더에 추가 되지 않은 모든 기존 사용 권한을 대체 합니다.  
  
> [!IMPORTANT]
>  공유 폴더 목록에 폴더를 추가하는 작업을 완료한 후 폴더가 서버 백업에 포함되어 있는지 확인합니다. 서버 백업에 폴더를 추가하는 방법에 대한 자세한 내용은 [서버 백업 설정 또는 사용자 지정](Set-up-or-customize-server-backup.md)을 참조하세요.  
  
## <a name="see-also"></a>참조  
  
-   [백업 및 복원 관리](Manage-Backup-and-Restore-in-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials 관리](Manage-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials 사용](../use/Use-Windows-Server-Essentials.md)
