---
title: "문제 해결 컴퓨터 백업 및 복원 Windows Server Essentials의 오류"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 06/25/2013
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5cc73aff-d2c0-4cf9-a23d-ef928ae5ddc9
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 37e79661442ba9f66a564b6c6c8fb57db1978454
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="troubleshoot-computer-backup-and-restore-errors-in-windows-server-essentials"></a>문제 해결 컴퓨터 백업 및 복원 Windows Server Essentials의 오류

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

이 절차를 사용 하 여 컴퓨터 백업을 백업 구성 문제, 불완전 하거나 실패 백업을, 백업 건강 경고 및을 파일, 폴더 또는 전체 시스템 복원을 문제를 비롯 한 Windows Server Essentials의 문제를 해결 합니다.  
  
> [!NOTE]
>  Windows Server Essentials 커뮤니티에서 가장 최근에 문제 해결 정보를 방문 하 여 [Windows Server Essentials 포럼](https://social.technet.microsoft.com/Forums//winserveressentials/threads)합니다.  
  
##  <a name="BKMK_TroubleshootBackupConfigurationIssues"></a>연결 된 컴퓨터에 대 한 백업 구성 문제 해결  
 이 절차를 사용 하 여 Windows Server Essentials 서버에 백업 하는 컴퓨터에 대 한 백업 구성 된 문제를 해결 합니다.  
  
### <a name="errors"></a>오류  
  
-   백업 구성 성공적으로 완료 되지 않았습니다.  
  
-   컴퓨터에 대 한 오류 수집 정보  
  
-   백업에서 제거 컴퓨터 오류  
  
### <a name="resolutions"></a>해결 방법  
  
##### <a name="to-troubleshoot-errors-that-occur-while-you-configure-backups-for-a-connected-computer"></a>연결 된 컴퓨터에 대 한 백업을 구성 하는 동안 발생 하는 오류를 해결 하려면  
  
1.  네트워크 장치를 통해 컴퓨터가 네트워크에 연결 되어 있는지 확인 합니다.  
  
2.  제대로 작동 하 고 컴퓨터에 연결 된 네트워크 디바이스도 전원이 켜져 네트워크에 연결 되어 있는지를 확인 합니다.  
  
3.  Windows Server 클라이언트 백업 서비스 및 Windows Server 클라이언트 컴퓨터 백업 공급자 서비스 서버에서 실행 되 고 있는지 확인 합니다.  
  
    ###### <a name="to-start-computer-backup-services-on-the-server"></a>서버에서 컴퓨터 백업 서비스를 시작 하려면  
  
    1.  서버에서 **시작**, 클릭 **관리 도구**을 차례로 클릭 하 고 **서비스**합니다.  
  
    2.  누른 다음 아래로 스크롤하여 **Windows Server 클라이언트 컴퓨터 백업 공급자 서비스**합니다. 서비스의 상태 없으면 **시작**를 서비스를 마우스 오른쪽 단추로 클릭 한 다음 **시작**합니다.  
  
    3.  클릭 **Windows Server 클라이언트 컴퓨터 백업 서비스**합니다. 서비스의 상태 없으면 **시작**를 서비스를 마우스 오른쪽 단추로 클릭 한 다음 **시작**합니다.  
  
    4.  닫기 **서비스**합니다.  
  
4.  Windows Server 클라이언트 컴퓨터 백업 공급자 서비스 클라이언트 컴퓨터에서 실행 되 고 있는지 확인 합니다.  
  
    ###### <a name="to-start-the-computer-backup-service-on-the-client-computer"></a>클라이언트 컴퓨터의 컴퓨터 백업 서비스를 시작 하려면  
  
    1.  클라이언트 컴퓨터에서 클릭 **시작**, 입력 **서비스** 에 **프로그램 및 파일 검색** 텍스트 상자 하 고 Enter 키를 누릅니다.  
  
    2.  누른 다음 아래로 스크롤하여 **Windows Server 클라이언트 컴퓨터 백업 공급자 서비스**합니다. 서비스의 상태 없으면 **시작**를 서비스를 마우스 오른쪽 단추로 클릭 한 다음 **시작**합니다.  
  
    3.  닫기 **서비스**합니다.  
  
5.  백업 데이터베이스에 오류가 있는지 확인 하려면 알림을 확인 합니다. 오류가 있는 경우 복구 백업 데이터베이스에 알림에 표시 지침을 따릅니다.  
  
6.  컴퓨터에서 Windows Server Essentials 커넥터 소프트웨어를 제거한 다음 다시 설치 합니다. 자세한 내용은 참조 항목 [커넥터 소프트웨어를 제거](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_13) 및 [커넥터 소프트웨어를 설치](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_11)합니다.  
  
##  <a name="BKMK_TroubleshootaBackupThatDidNotCompleteProperly"></a>올바르게 완료 되지 않은 백업 문제 해결  
 백업이 실패 상태에 있는 경우 성공 백업의 및 데이터가 사용할 수 복원할 수 있습니다. 그러나 백업에 완료 되지 않은 상태가 이면 구성 백업한 있지만 일부 데이터를 복원할 수에 사용할 수는 백업에 모든 항목 지정 됩니다.  
  
### <a name="errors"></a>오류  
  
-   백업을 완료 되지 않았습니다.  
  
-   백업이 실패  
  
### <a name="resolutions"></a>해결 방법  
  
##### <a name="to-identify-volumes-that-were-not-backed-up-successfully"></a>백업 되지 않았기 성공적으로 볼륨을 식별 하기 위해  
  
1.  Windows Server Essentials 대시보드 열고 클릭 **컴퓨터와 백업**합니다.  
  
2.  백업 무엇 하지 성공적으로 완료 장소와 클릭 한 다음 컴퓨터의 이름을 클릭 **컴퓨터 속성 보기** 에 **작업** 창 합니다.  
  
3.  클릭 한 다음 및 성공적으로 완료 되지 않은 백업을 클릭 **자세한 내용을 보려면**합니다.  
  
4.  에 **백업 세부 정보** 대화 상자에서 녹색 성공적으로 백업 된 모든 볼륨의 상태에 표시 됩니다.  
  
##### <a name="to-troubleshoot-an-unsuccessful-backup-of-a-volume"></a>볼륨 실패 백업을 문제를 해결 하려면  
  
1.  제대로 작동 하 고 하드 디스크 설정, 컴퓨터에 연결 되어 있는지를 확인 합니다.  
  
2.  실행 **chkdsk /f /r** 하드 디스크 오류 해결 (**/f**) 하 고 읽을 수 있는 정보 불량 섹터 복구 (**/r**). 실행 중인에 대 한 자세한 내용은 **chkdsk**, 참조 [CHKDSK](https://go.microsoft.com/fwlink/?LinkId=206562)합니다.  
  
3.  컴퓨터를 종료 하거나 백업을 실행 하는 동안에 네트워크에서 연결이 끊어진 하지 있는지 확인 합니다.  
  
4.  각 볼륨 실행 하는 백업에 대 한 충분 한 공간이 있는지 확인 합니다. 백업은 VSS 스냅숏을 만드는 클라이언트 컴퓨터에 추가 디스크 공간을 확보 해야 합니다. 시스템 예약된 하지 않은 모든 볼륨의 사용 가능한 디스크 공간 최소 10% 무료 있어야 합니다. 시스템 예약 볼륨의 볼륨의 크기는 500 MB 보다 작은 경우 VSS 32 활용 하려면 사용 가능한 공간이 스냅숏을; 만들려면 볼륨이 500MB 이상이 VSS 320MB의 여유 공간이 필요 합니다.  
  
     사용 가능한 공간이 부족 볼륨에 사용할 수 있는 경우 이러한 해결 방법 중 하나를 수행 합니다.  
  
    -   볼륨을 확장 합니다. 예약 시스템 볼륨을 제외 하 고 기본 또는 동적 볼륨을 확장할 수 있습니다.  
  
        ###### <a name="to-extend-a-volume"></a>볼륨을 확장 하  
  
        1.  제어판에서 클릭 **시스템 및 보안**합니다.  
  
        2.  아래에서 **관리 도구**, 클릭 **하드 디스크 파티션 만들기 및 포맷**합니다.  
  
        3.  확장을 볼륨을 마우스 오른쪽 단추로 클릭 합니다. 하는 경우 **볼륨 확장** 이 사용 하도록 설정 해당 옵션을 선택 합니다. 옵션을 사용 하지 않는 경우 볼륨을 확장할 수는 없습니다.  
  
        4.  볼륨을 확장 확장 볼륨 마법사의 단계를 따릅니다.  
  
    -   더 많은 공간을 확보 하려면 볼륨에서 콘텐츠를 삭제 합니다.  
  
        > [!NOTE]
        >  시스템 예약 볼륨의 공간을 확보 해야 하는 경우 시스템 복구 이미지를 다른 볼륨 이동할 수 있습니다. 자세한 내용은 [시스템 복구 이미지를 배포](https://technet.microsoft.com/library/dd744280\(v=ws.10\).aspx)합니다.  
  
    -   볼륨 클라이언트 백업에서 제외 합니다. 볼륨의 데이터 백업 복사본을 유지 하는 것이 중요 하지 않는 경우에이 작업을 수행 합니다.  
  
        > [!WARNING]
        >  클라이언트 백업에서 시스템 예약 볼륨을 제외 클라이언트 시스템을 백업 하지는 하 고 컴퓨터의 모든 시스템 복원을 수행할 수 없습니다.  
  
5.  다른 나타날 수를 성공적으로 완료 백업에 대 한 서버에서 디스크 공간이 부족 하는 서버에 알림에 대 한 확인 합니다. 문제 해결을 위해 경고의 지침을 따릅니다.  
  
6.  실행 **vssadmin** 섀도 복사본 서비스 VSS (볼륨) 문제를 해결 하는 명령 프롬프트에서 발행 합니다. 에 대 한 내용은 **vssadmin**, 참조 [VSSADMIN](https://go.microsoft.com/fwlink/?LinkID=94332)합니다.  
  
##  <a name="BKMK_TroubleshootBackupHealthAlertIssues"></a>백업 건강 경고 문제 해결  
  
### <a name="errors"></a>오류  
  
-   Windows Server 솔루션 컴퓨터 백업 공급자 서비스 작동 중지 됨  
  
-   Windows Server 솔루션 클라이언트 컴퓨터 백업 공급자 서비스가 작동을 중지  
  
### <a name="resolutions"></a>해결 방법  
  
##### <a name="to-troubleshoot-a-backup-health-alert"></a>백업 상태 경고를 문제를 해결 하려면  
  
1.  알림을 백업 데이터베이스에 문제가 있음을 알리는, 경우 문제 해결을 위해 경고의 지침을 따릅니다.  
  
2.  알림을 백업 서비스가 실행 되 고 있지는 메시지가 표시, 서버 또는 오류 메시지가 수신 되는 클라이언트 컴퓨터에서 서비스를 시작 하려고 합니다.  
  
    ###### <a name="to-start-backup-services-on-the-server"></a>서버에 백업 서비스를 시작 하려면  
  
    1.  서버에서 **시작**를 클릭 하 고 **관리 도구**을 차례로 클릭 하 고 **서비스**합니다.  
  
        > [!NOTE]
        >  서버를 원격으로 관리 하는 경우 서버 바탕 화면에 액세스 하려면 원격 데스크톱 연결을 사용 해야 합니다. 원격 데스크톱 연결을 사용 하 여에 대 한 정보를 참조 하세요. [원격 데스크톱 연결을 사용 하 여 다른 컴퓨터에 연결](https://windows.microsoft.com/windows-vista/Connect-to-another-computer-using-Remote-Desktop-Connection)합니다.  
  
    2.  누른 다음 아래로 스크롤하여 **Windows Server 클라이언트 컴퓨터 백업 공급자 서비스**합니다. 서비스의 상태 없으면 **시작**를 서비스를 마우스 오른쪽 단추로 클릭 한 다음 **시작**합니다.  
  
    3.  클릭 **Windows Server 클라이언트 컴퓨터 백업 서비스**합니다. 서비스의 상태 없으면 **시작**를 서비스를 마우스 오른쪽 단추로 클릭 한 다음 **시작**합니다.  
  
    4.  닫기 **서비스**합니다.  
  
    ###### <a name="to-start-backup-services-on-a-client-computer"></a>백업 서비스 클라이언트 컴퓨터를 시작 하려면  
  
    1.  클라이언트 컴퓨터에서 클릭 **시작**, 입력 **서비스** 에 **프로그램 및 파일 검색** 텍스트 상자를 클릭 하 고 있습니다.  
  
    2.  마우스 오른쪽 단추로 클릭 **Windows Server 클라이언트 컴퓨터 백업 공급자 서비스**을 차례로 클릭 하 고 **시작**합니다.  
  
    3.  닫는 **서비스**합니다.  
  
3.  이벤트 로그 클라이언트 컴퓨터 또는 서비스 또는 드라이버를 백업 관련 된 문제에 대 한 서버를 확인 합니다.  
  
4.  서버 또는 오류 메시지가 수신 되는 클라이언트 컴퓨터를 다시 부팅 합니다.  
  
5.  클라이언트 백업에 영향을 미칠 수 있는 기타 문제에 대 한 상태 알림을 확인 합니다.  
  
##  <a name="BKMK_FileAndFolder"></a>파일 또는 폴더 복원 문제 해결  
  
### <a name="errors"></a>오류  
  
-   파일 또는 폴더 복원 성공적으로 완료 되지 않았습니다.  
  
### <a name="resolutions"></a>해결 방법  
  
##### <a name="to-troubleshoot-an-unsuccessful-file-or-folder-restore"></a>실패 한 파일 또는 폴더 복원의 문제를 해결 하려면  
  
1.  네트워크 장치를 통해 컴퓨터가 네트워크에 연결 되어 있는지 확인 합니다.  
  
2.  제대로 작동 하 고 컴퓨터에 연결 된 네트워크 디바이스도 전원이 켜져 네트워크에 연결 되어 있는지를 확인 합니다.  
  
3.  백업 데이터베이스에 오류가 있는지 확인 하려면 알림을 확인 합니다. 오류가 있는 경우 복구 백업 데이터베이스에 알림에 표시 지침을 따릅니다.  
  
4.  다른 백업에서 파일 또는 폴더를 복원 해 보세요.  
  
5.  하 않도록는 **Windows Server 솔루션 컴퓨터 복원 드라이버** 제대로 작동 하 고 설치 합니다.  
  
    ###### <a name="to-check-the-status-of-the-windows-server-solution-computer-restore-driver"></a>Windows Server 솔루션 컴퓨터 복원 드라이버의 상태를 확인 하려면  
  
    1.  클릭 **시작**, 입력 **장치 관리자** 에 **프로그램 및 파일 검색** 텍스트 상자를 클릭 하 고 있습니다.  
  
    2.  장치 관리자에서 클릭 **시스템 장치**,으로 스크롤하고 **Windows Server 솔루션 컴퓨터 복원 드라이버**합니다.  
  
    3.  드라이버 표시 되지 않으면 다음과 같습니다.  
  
        1.  관리자 권한으로 명령 프롬프트를 열고 하 고 다음 명령을 실행 합니다.  
  
             **%ProgramFiles%\Windows Server\Bin\BackupDriverInstaller.exe 있나요?  저는**  
  
        2.  장치 관리자를 새로 고칩니다. 드라이버 나타나면 정상입니다.  
  
    4.  표시 되는 아이콘은 컴퓨터 모니터, 경우 드라이버가 설치 되어 실행 제대로 합니다. 장치 관리자를 닫습니다.  
  
    5.  표시 되는 아이콘 컴퓨터 모니터 없는 경우  
  
        1.  마우스 오른쪽 단추로 클릭 **Windows Server 솔루션 컴퓨터 복원 드라이버**을 차례로 클릭 하 고 **속성**합니다.  
  
        2.  클릭 하 고 **드라이버** 탭을 클릭 한 다음 **드라이버 업데이트**합니다.  
  
        3.  클릭 **업데이트 된 드라이버 소프트웨어 자동으로 검색**, 드라이버를 업데이트 하는 지침을 따릅니다.  
  
    6.  장치 관리자를 닫습니다.  
  
6.  컴퓨터에서 Windows Server Essentials 커넥터 소프트웨어를 제거한 다음 다시 설치 합니다. 자세한 내용은 참조 항목 [커넥터 소프트웨어를 제거](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_13) 및 [커넥터 소프트웨어를 설치](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_11)합니다.  
  
##  <a name="BKMK_Troubleshootfullsystemrestoreissues"></a>전체 시스템 복원을 문제 해결  
  
### <a name="errors"></a>오류  
  
-   전체 시스템 복원을 후 클라이언트 컴퓨터에 로그온 할 수 없습니다.  
  
### <a name="resolutions"></a>해결 방법  
 컴퓨터의 이름을 변경 하 고 나중에 변경 하기 전에 컴퓨터 이름, 복원 후 도메인 계정에 로그인 하려고 할 때 저장 된 백업 복원 해야 할 경우이 오류가 발생 합니다. "서버의 보안 데이터베이스가 워크스테이션 신뢰 관계에 대 한 계정을 않습니다." 네트워크 액세스를 컴퓨터에 다시, 커넥터 소프트웨어를 제거 하 고는 Windows 도메인에서 컴퓨터를 제거 다시 서버에 연결 합니다.  
  
##### <a name="to-regain-network-access-to-a-restored-computer-after-a-computer-name-change"></a>네트워크에 다시 액세스 컴퓨터를 복원한 후 컴퓨터 이름 변경 하려면  
  
1.  로컬 관리자는 컴퓨터에 로그온 합니다.  
  
2.  커넥터 소프트웨어를 제거 합니다. 자세한 내용은 참조 [커넥터 소프트웨어를 제거](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_13)합니다.  
  
3.  도메인에서 컴퓨터를 제거 합니다. 자세한 내용은 참조 [Windows 도메인에서 컴퓨터를 제거](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_8)합니다.  
  
4.  서버에 컴퓨터를 다시 연결 합니다. 자세한 내용은 참조 [서버에 컴퓨터를 연결](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_9)합니다.  
  
## <a name="see-also"></a>참조 하십시오  
  
-   [Windows Server Essentials 지원](Support-Windows-Server-Essentials.md)