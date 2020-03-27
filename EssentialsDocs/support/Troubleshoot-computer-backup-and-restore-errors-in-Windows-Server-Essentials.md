---
title: Windows Server Essentials의 컴퓨터 백업 및 복원 오류 문제 해결
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.custom: na
ms.date: 06/25/2013
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5cc73aff-d2c0-4cf9-a23d-ef928ae5ddc9
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 28e3564c93f192563626bfb44992ef9bc4a49598
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80313247"
---
# <a name="troubleshoot-computer-backup-and-restore-errors-in-windows-server-essentials"></a>Windows Server Essentials의 컴퓨터 백업 및 복원 오류 문제 해결

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

다음 절차를 통해 백업 구성 문제, 불완전한 백업 또는 실패한 백업, 백업 상태 경고 및 파일, 폴더 또는 전체 시스템 복원 문제 등 Windows Server Essentials의 컴퓨터 백업 문제를 해결할 수 있습니다.  
  
> [!NOTE]
>  Windows Server Essentials 커뮤니티의 최신 문제 해결 정보는 [Windows Server Essentials 포럼](https://social.technet.microsoft.com/Forums//winserveressentials/threads)을 참조 하세요.  
  
##  <a name="troubleshoot-backup-configuration-issues-for-a-connected-computer"></a><a name="BKMK_TroubleshootBackupConfigurationIssues"></a>연결 된 컴퓨터의 백업 구성 문제 해결  
 다음 절차를 통해 Windows Server Essentials 서버에 백업된 컴퓨터의 백업 구성 문제를 해결할 수 있습니다.  
  
### <a name="errors"></a>오류  
  
-   백업 구성이 완료되지 않았습니다.  
  
-   컴퓨터에 대한 정보를 수집하는 동안 오류가 발생했습니다.  
  
-   백업에서 컴퓨터를 제거하는 동안 오류가 발생했습니다.  
  
### <a name="resolutions"></a>해결 방법  
  
##### <a name="to-troubleshoot-errors-that-occur-while-you-configure-backups-for-a-connected-computer"></a>연결된 컴퓨터에 대한 백업을 구성하는 동안 발생하는 오류 문제를 해결하려면  
  
1.  컴퓨터가 네트워크 장치를 통해 네트워크에 연결되어 있는지 확인합니다.  
  
2.  컴퓨터가 연결된 네트워크 장치가 네트워크에도 연결되어 있고 전원이 켜져 있으며 제대로 작동하는지 확인합니다.  
  
3.  Windows Server Client Backup Service 및 Windows Server Client Computer Backup Provider Service가 서버에서 실행되고 있는지 확인합니다.  
  
    ###### <a name="to-start-computer-backup-services-on-the-server"></a>서버에서 컴퓨터 백업 서비스를 시작하려면  
  
    1.  서버에서 **시작**, **관리 도구** 및 **서비스**를 차례로 클릭합니다.  
  
    2.  아래로 스크롤하여 **Windows Server Client Computer Backup Provider Service**를 클릭합니다. 서비스의 상태가 **시작됨**이 아니면 서비스를 마우스 오른쪽 단추로 클릭한 후 **시작**을 클릭합니다.  
  
    3.  **Windows Server Client Computer Backup Service**를 클릭합니다. 서비스의 상태가 **시작됨**이 아니면 서비스를 마우스 오른쪽 단추로 클릭한 후 **시작**을 클릭합니다.  
  
    4.  **서비스**를 닫습니다.  
  
4.  Windows Server Client Computer Backup Provider Service가 클라이언트 컴퓨터에서 실행되고 있는지 확인합니다.  
  
    ###### <a name="to-start-the-computer-backup-service-on-the-client-computer"></a>클라이언트 컴퓨터에서 컴퓨터 백업 서비스를 시작하려면  
  
    1.  클라이언트 컴퓨터에서 **시작**을 클릭하고 **프로그램 및 파일 검색** 텍스트 상자에 **서비스**를 입력한 후 Enter 키를 누릅니다.  
  
    2.  아래로 스크롤하여 **Windows Server Client Computer Backup Provider Service**를 클릭합니다. 서비스의 상태가 **시작됨**이 아니면 서비스를 마우스 오른쪽 단추로 클릭한 후 **시작**을 클릭합니다.  
  
    3.  **서비스**를 닫습니다.  
  
5.  경고를 확인하여 백업 데이터베이스에 오류가 있는지 확인합니다. 오류가 있는 경우 경고의 지침에 따라 백업 데이터베이스를 복구합니다.  
  
6.  컴퓨터에서 Windows Server Essentials Connector 소프트웨어를 제거한 후 다시 설치합니다. 자세한 내용은 [Connector 소프트웨어 제거](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_13)(영문) 및 [Connector 소프트웨어 설치](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_11)(영문) 항목을 참조하세요.  
  
##  <a name="troubleshoot-a-backup-that-did-not-complete-properly"></a><a name="BKMK_TroubleshootaBackupThatDidNotCompleteProperly"></a>제대로 완료 되지 않은 백업 문제 해결  
 백업 상태가 실패인 경우 백업에 성공한 부분이 없으며 복원에 사용할 수 있는 데이터가 없습니다. 그러나 백업의 상태가 완료 안 됨인 경우 백업 구성에 지정된 항목 중 일부가 백업되지 않았지만 일부 데이터는 복원에 사용할 수도 있습니다.  
  
### <a name="errors"></a>오류  
  
-   백업이 완료되지 않았습니다.  
  
-   백업에 실패했습니다.  
  
### <a name="resolutions"></a>해결 방법  
  
##### <a name="to-identify-volumes-that-were-not-backed-up-successfully"></a>백업되지 않은 볼륨을 식별하려면  
  
1.  Windows Server Essentials Dashboard를 연 후 **컴퓨터 및 백업**을 클릭합니다.  
  
2.  백업이 완료되지 않은 컴퓨터의 이름을 클릭한 후 **작업** 창에서 **컴퓨터 속성 보기**를 클릭합니다.  
  
3.  완료되지 않은 백업을 클릭한 후 **자세히 보기**를 클릭합니다.  
  
4.  **백업 세부 정보** 대화 상자에서 백업된 모든 볼륨의 상태에 녹색 확인 표시가 표시되어 있습니다.  
  
##### <a name="to-troubleshoot-an-unsuccessful-backup-of-a-volume"></a>볼륨의 실패한 백업 문제를 해결하려면  
  
1.  하드 디스크가 컴퓨터에 연결되어 있고 켜져 있으며 제대로 작동하는지 확인합니다.  
  
2.  **chkdsk /f /r**을 실행하여 하드 디스크에 대한 모든 오류를 해결하고( **/f**), 모든 불량 섹터에서 읽을 수 있는 정보를 복구합니다( **/r**). **chkdsk**를 실행하는 방법에 대한 자세한 내용은 [CHKDSK](https://go.microsoft.com/fwlink/?LinkId=206562)를 참조하세요.  
  
3.  백업이 실행되는 동안 컴퓨터가 종료되거나 네트워크에서 연결이 끊어지지 않았는지 확인합니다.  
  
4.  각 볼륨에 백업을 실행하기 위한 사용 가능한 공간이 충분한지 확인합니다. 백업을 실행하려면 클라이언트 컴퓨터에 VSS 스냅샷을 만들기 위한 추가 디스크 공간이 필요합니다. 시스템에서 사용하지 않는 모든 볼륨에서는 사용 가능한 디스크 공간의 10% 이상을 사용할 수 있어야 합니다. 시스템에서 사용하는 볼륨에서 볼륨 크기가 500MB 미만인 경우 VSS에 스냅샷을 만들기 위해 사용 가능한 공간이 32MB 필요하고, 볼륨이 500MB 이상인 경우 VSS에 사용 가능한 공간이 320MB 필요합니다.  
  
     볼륨에서 사용 가능한 공간이 부족한 경우 다음 해결 방법 중 하나를 시도해 보세요.  
  
    -   볼륨을 확장합니다. 시스템에서 사용하는 볼륨을 제외한 모든 기본 또는 동적 볼륨을 확장할 수 있습니다.  
  
        ###### <a name="to-extend-a-volume"></a>볼륨을 확장하려면  
  
        1.  제어판에서 **시스템 및 보안**을 클릭합니다.  
  
        2.  **관리 도구**에서 **하드 디스크 파티션 만들기 및 포맷**을 클릭합니다.  
  
        3.  확장하려는 볼륨을 마우스 오른쪽 단추로 클릭합니다. **볼륨 확장**이 사용하도록 설정된 경우 해당 옵션을 선택합니다. 이 옵션이 사용하도록 설정되지 않은 경우 볼륨을 확장할 수 없습니다.  
  
        4.  볼륨 확장 마법사의 단계에 따라 볼륨을 확장합니다.  
  
    -   볼륨에서 콘텐츠를 삭제하여 더 많은 공간을 사용할 수 있도록 만듭니다.  
  
        > [!NOTE]
        >  시스템에서 사용하는 볼륨에서 공간을 확보해야 경우 시스템 복구 이미지를 다른 볼륨으로 이동할 수 있습니다. 자세한 내용은 [시스템 복구 이미지 배포](https://technet.microsoft.com/library/dd744280\(v=ws.10\).aspx)를 참조하세요.  
  
    -   클라이언트 백업에서 볼륨을 제외합니다. 볼륨에 데이터의 백업 복사본을 유지하는 것이 중요하지 않은 경우에만 이렇게 하세요.  
  
        > [!WARNING]
        >  클라이언트 백업에서 시스템에서 사용하는 볼륨을 제외하면 클라이언트 시스템이 백업되지 않아 컴퓨터에서 전체 시스템 복원을 수행할 수 없습니다.  
  
5.  서버에 백업을 완료하기 위한 공간이 충분하지 않음을 나타낼 수 있는, 서버에 대한 다른 경고를 확인합니다. 경고의 지침에 따라 문제를 해결합니다.  
  
6.  명령 프롬프트에서 **vssadmin**을 실행하여 VSS(볼륨 섀도 복사본 서비스) 문제를 해결합니다. **vssadmin**에 대한 자세한 내용은 [VSSADMIN](https://go.microsoft.com/fwlink/?LinkID=94332)(영문)을 참조하세요.  
  
##  <a name="troubleshoot-backup-health-alert-issues"></a><a name="BKMK_TroubleshootBackupHealthAlertIssues"></a>백업 상태 경고 문제 해결  
  
### <a name="errors"></a>오류  
  
-   Windows Server Solutions Computer Backup Provider Service의 작동이 중지되었습니다.  
  
-   Windows Server 솔루션 클라이언트 컴퓨터 백업 공급자 서비스의 작동이 중지되었습니다.  
  
### <a name="resolutions"></a>해결 방법  
  
##### <a name="to-troubleshoot-a-backup-health-alert"></a>백업 상태 경고 문제를 해결하려면  
  
1.  경고에 백업 데이터베이스에 문제가 있다고 표시되는 경우 경고의 지침에 따라 문제를 해결합니다.  
  
2.  경고에 백업 서비스가 실행되고 있지 않다고 표시되는 경우 오류 메시지를 받은 서버 또는 클라이언트 컴퓨터에서 서비스를 시작해 봅니다.  
  
    ###### <a name="to-start-backup-services-on-the-server"></a>서버에서 백업 서비스를 시작하려면  
  
    1.  서버에서 **시작**, **관리 도구** 및 **서비스**를 차례로 클릭합니다.  
  
        > [!NOTE]
        >  서버를 원격으로 관리하는 경우 원격 데스크톱 연결을 사용하여 서버 데스크톱에 액세스해야 합니다. 원격 데스크톱 연결을 사용하는 방법에 대한 자세한 내용은 [원격 데스크톱 연결을 사용하여 다른 컴퓨터에 연결](https://windows.microsoft.com/windows-vista/Connect-to-another-computer-using-Remote-Desktop-Connection)을 참조하세요.  
  
    2.  아래로 스크롤하여 **Windows Server Client Computer Backup Provider Service**를 클릭합니다. 서비스의 상태가 **시작됨**이 아니면 서비스를 마우스 오른쪽 단추로 클릭한 후 **시작**을 클릭합니다.  
  
    3.  **Windows Server Client Computer Backup Service**를 클릭합니다. 서비스의 상태가 **시작됨**이 아니면 서비스를 마우스 오른쪽 단추로 클릭한 후 **시작**을 클릭합니다.  
  
    4.  **서비스**를 닫습니다.  
  
    ###### <a name="to-start-backup-services-on-a-client-computer"></a>클라이언트 컴퓨터에서 백업 서비스를 시작하려면  
  
    1.  클라이언트 컴퓨터에서 **시작**을 클릭하고 **프로그램 및 파일 검색** 텍스트 상자에 **서비스**를 입력한 후 Enter 키를 클릭합니다.  
  
    2.  **Windows Server Client Computer Backup Provider Service**를 마우스 오른쪽 단추로 클릭한 후 **시작**을 클릭합니다.  
  
    3.  **서비스**를 닫습니다.  
  
3.  클라이언트 컴퓨터 또는 서버에서 백업 서비스 또는 드라이버에 관련된 문제가 있는지 이벤트 로그를 확인합니다.  
  
4.  오류 메시지를 받은 서버 또는 클라이언트 컴퓨터를 다시 부팅합니다.  
  
5.  클라이언트 백업에 영향을 미칠 수 있는 다른 문제가 있는지 상태 경고를 확인합니다.  
  
##  <a name="troubleshoot-a-file-or-folder-restore"></a><a name="BKMK_FileAndFolder"></a>파일 또는 폴더 복원 문제 해결  
  
### <a name="errors"></a>오류  
  
-   파일 또는 폴더 복원이 완료되지 않았습니다.  
  
### <a name="resolutions"></a>해결 방법  
  
##### <a name="to-troubleshoot-an-unsuccessful-file-or-folder-restore"></a>실패한 파일 또는 폴더 복원 문제를 해결하려면  
  
1.  컴퓨터가 네트워크 장치를 통해 네트워크에 연결되어 있는지 확인합니다.  
  
2.  컴퓨터가 연결된 네트워크 장치가 네트워크에도 연결되어 있고 전원이 켜져 있으며 제대로 작동하는지 확인합니다.  
  
3.  경고를 확인하여 백업 데이터베이스에 오류가 있는지 확인합니다. 오류가 있는 경우 경고의 지침에 따라 백업 데이터베이스를 복구합니다.  
  
4.  다른 백업에서 파일 또는 폴더를 복원해 봅니다.  
  
5.  **Windows Server Solution Computer Restore Driver**가 설치되어 있으며 제대로 작동하는지 확인합니다.  
  
    ###### <a name="to-check-the-status-of-the-windows-server-solution-computer-restore-driver"></a>Windows Server Solution Computer Restore Driver의 상태를 확인하려면  
  
    1.  **시작**을 클릭하고 **프로그램 및 파일 검색** 텍스트 상자에 **장치 관리자**를 입력한 후 Enter 키를 클릭합니다.  
  
    2.  장치 관리자에서 **시스템 장치**를 클릭하고 **Windows Server Solutions Computer Restore Driver**로 스크롤합니다.  
  
    3.  드라이버가 표시되지 않는 경우  
  
        1.  관리자 권한으로 명령 프롬프트를 열고 다음 명령을 실행합니다.  
  
             **%ProgramFiles%\Windows Server\Bin\BackupDriverInstaller.exe? -i**  
  
        2.  장치 관리자를 새로 고칩니다. 드라이버가 표시되어야 합니다.  
  
    4.  표시된 아이콘이 컴퓨터 모니터인 경우 드라이버가 설치되어 있고 제대로 실행되고 있는 것입니다. 장치 관리자를 닫습니다.  
  
    5.  표시된 아이콘이 컴퓨터 모니터가 아닌 경우  
  
        1.  **Windows Server Solutions Computer Restore Driver**를 마우스 오른쪽 단추로 클릭한 후 **속성**을 클릭합니다.  
  
        2.  **드라이버** 탭을 클릭한 후 **드라이버 업데이트**를 클릭합니다.  
  
        3.  **업데이트된 드라이버 소프트웨어 자동으로 검색**을 클릭한 후 지침에 따라 드라이버를 업데이트합니다.  
  
    6.  장치 관리자를 닫습니다.  
  
6.  컴퓨터에서 Windows Server Essentials Connector 소프트웨어를 제거한 후 다시 설치합니다. 자세한 내용은 [Connector 소프트웨어 제거](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_13)(영문) 및 [Connector 소프트웨어 설치](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_11)(영문) 항목을 참조하세요.  
  
##  <a name="troubleshoot-a-full-system-restore"></a><a name="BKMK_Troubleshootfullsystemrestoreissues"></a>전체 시스템 복원 문제 해결  
  
### <a name="errors"></a>오류  
  
-   전체 시스템 복원 후에 클라이언트 컴퓨터에 로그온할 수 없습니다.  
  
### <a name="resolutions"></a>해결 방법  
 컴퓨터의 이름을 변경하고 나중에 컴퓨터 이름이 변경되기 전에 저장된 백업으로 복원해야 할 경우, 복원 후 도메인 계정에 로그온하려고 하면 "서버의 보안 데이터베이스가 이 워크스테이션 트러스트 관계를 위한 컴퓨터 계정을 가지고 있지 않습니다." 오류가 표시됩니다. 다시 컴퓨터에 대한 네트워크 액세스 권한을 얻으려면 Connector 소프트웨어를 제거하고 Windows 도메인에서 컴퓨터를 제거한 후 서버에 다시 연결합니다.  
  
##### <a name="to-regain-network-access-to-a-restored-computer-after-a-computer-name-change"></a>컴퓨터 이름 변경 후 복원된 컴퓨터에 대한 네트워크 액세스 권한을 다시 얻으려면  
  
1.  로컬 관리자로 컴퓨터에 로그온합니다.  
  
2.  Connector 소프트웨어를 제거합니다. 자세한 내용은 [Connector 소프트웨어 제거](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_13)(영문)를 참조하세요.  
  
3.  도메인에서 컴퓨터를 제거합니다. 자세한 내용은 [Windows 도메인에서 컴퓨터 제거](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_8)(영문)를 참조하세요.  
  
4.  서버에 컴퓨터를 다시 연결합니다. 자세한 내용은 [서버에 컴퓨터 연결](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_9)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
  
-   [Windows Server Essentials 지원](Support-Windows-Server-Essentials.md)