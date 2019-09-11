---
title: Robocopy를 사용 하 여 DFS 복제에 대 한 파일 사전 시드
description: Robocopy를 사용 하 여 DFS 복제에 대 한 파일을 사전 시드 하는 방법입니다.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 05/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4a0cad3c685c8609784c7096fe31d55294712c2e
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70871983"
---
# <a name="use-robocopy-to-preseed-files-for-dfs-replication"></a>Robocopy를 사용 하 여 DFS 복제에 대 한 파일 사전 시드

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

이 항목에서는 Windows Server에서 DFS (분산 파일 시스템) 복제 (DFSR 또는 DFS) 복제를 설정할 때 명령줄 도구인 **Robocopy**를 사용 하 여 파일을 사전 시드 하는 방법에 대해 설명 합니다. DFS 복제를 설정 하기 전에 파일을 미리 시드해야 합니다. 새 복제 파트너를 추가 하거나 서버를 교체 하 여 초기 동기화 속도를 높이고 Windows Server 2012 r 2에서 DFS 복제 데이터베이스의 복제를 사용 하도록 설정할 수 있습니다. Robocopy 메서드는 몇 가지 사전 시드 방법 중 하나입니다. 개요는 [1 단계: DFS 복제에 대 한 사전 초기값 파일](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn495046(v%3dws.11)>)을 참조 하세요.

Robocopy (강력한 파일 복사) 명령줄 유틸리티는 Windows Server에 포함 되어 있습니다. 유틸리티는 보안 복사, 백업 API 지원, 다시 시도 기능 및 로깅을 포함 하는 광범위 한 옵션을 제공 합니다. 최신 버전에는 다중 스레딩 및 버퍼링 되지 않은 i/o 지원이 포함 됩니다.

>[!IMPORTANT]
>Robocopy는 독점적으로 잠긴 파일을 복사 하지 않습니다. 사용자가 파일 서버에서 긴 기간 동안 많은 파일을 잠그는 경향이 있는 경우 다른 사전 시드 방법을 사용 하는 것이 좋습니다. 사전 시드가 원본 서버와 대상 서버에 있는 파일 목록과 완벽 하 게 일치 해야 하는 것은 아니지만 초기 동기화가 DFS 복제에 대해 수행 될 때 존재 하지 않는 파일은 더 많이 존재 하지 않습니다. 잠금 충돌을 최소화 하려면 조직의 사용량이 많지 않은 시간에 Robocopy를 사용 합니다. 사전 시드 후에는 항상 Robocopy 로그를 검사 하 여 전용 잠금으로 인해 건너뛴 파일을 파악 해야 합니다.

Robocopy를 사용 하 여 DFS 복제에 대 한 사전 시드 파일을 사용 하려면 다음 단계를 수행 합니다.

1. [최신 버전의 Robocopy를 다운로드 하 여 설치 합니다.](#step-1-download-and-install-the-latest-version-of-robocopy)
2. [복제 되는 안정화 파일.](#step-2-stabilize-files-that-will-be-replicated)
3. [복제 된 파일을 대상 서버에 복사 합니다.](#step-3-copy-the-replicated-files-to-the-destination-server)

## <a name="prerequisites"></a>사전 요구 사항

시드하십시오 DFS 복제 직접 관련 되지 않으므로 Robocopy를 사용 하 여 파일을 복사 하는 데 필요한 요구 사항만 충족 하면 됩니다.

- 원본 서버와 대상 서버에서 로컬 관리자 그룹의 구성원 인 계정이 필요 합니다.

- 원본 서버 또는 대상 서버와 같이 파일을 복사 하는 데 사용할 서버에 Robocopy의 최신 버전을 설치 합니다. 운영 체제 버전에 대 한 최신 버전을 설치 해야 합니다. 자세한 내용은 2 단계: [ 복제](#step-2-stabilize-files-that-will-be-replicated)되는 안정화 파일. Windows Server 2003 r 2를 실행 하는 서버에서 파일을 사전 시드해야 하지 않는 한 원본 또는 대상 서버에서 Robocopy를 실행할 수 있습니다. 일반적으로 최신 운영 체제 버전을 포함 하는 대상 서버는 Robocopy의 최신 버전에 대 한 액세스를 제공 합니다.

- 대상 드라이브에 사용할 수 있는 저장소 공간이 충분 한지 확인 하십시오. 복사할 경로에 폴더를 만들지 마십시오. Robocopy는 루트 폴더를 만들어야 합니다.
    
    >[!NOTE]
    >미리 시드 된 파일에 할당할 공간의 크기를 결정할 때는 시간이 지남에 따라 예상 되는 데이터 증가와 DFS 복제에 대 한 저장소 요구 사항을 고려해 야 합니다. 계획 도움말은 [DFS 복제 관리](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754771(v=ws.11)>)에서 [준비 폴더의 할당량 크기와 충돌 및 삭제 된 폴더 편집](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754229(v=ws.11)) 을 참조 하세요.

- 원본 서버에서 필요에 따라 프로세스 모니터 또는 프로세스 탐색기를 설치 합니다 .이 탐색기는 파일을 잠그는 응용 프로그램을 확인 하는 데 사용할 수 있습니다. 다운로드 정보는 [프로세스 모니터](https://docs.microsoft.com/sysinternals/downloads/procmon) 및 [프로세스 탐색기](https://docs.microsoft.com/sysinternals/downloads/process-explorer)를 참조 하세요.

## <a name="step-1-download-and-install-the-latest-version-of-robocopy"></a>1단계: 최신 버전의 Robocopy를 다운로드 하 여 설치 합니다.

Robocopy를 사용 하 여 파일을 미리 시드 하려면 먼저 **robocopy**의 최신 버전을 다운로드 하 여 설치 해야 합니다. 이렇게 하면 DFS 복제 Robocopy의 배달 버전에 포함 된 문제로 인해 파일을 건너뛰지 않습니다.

호환 되는 최신 Robocopy 버전의 소스는 서버에서 실행 중인 Windows Server 버전에 따라 다릅니다. Windows server 2008 R2 또는 Windows Server 2008 용 Robocopy의 최신 버전을 사용 하 여 핫픽스를 다운로드 하는 방법에 대 한 자세한 내용은 [Windows server 2008 및의 분산 파일 시스템 (DFS) 기술에 대해 현재 사용할 수 있는 핫픽스 목록을 참조 하십시오. Windows Server 2008 R2](https://support.microsoft.com/help/968429/list-of-currently-available-hotfixes-for-distributed-file-system-dfs-t).

또는 다음 단계를 수행 하 여 운영 체제에 대 한 최신 핫픽스를 찾아서 설치할 수 있습니다.

### <a name="locate-and-install-the-latest-version-of-robocopy-for-a-specific-version-of-windows-server"></a>특정 버전의 Windows Server에 대 한 Robocopy의 최신 버전 찾기 및 설치

1. 웹 브라우저에서를 엽니다 [https://support.microsoft.com](https://support.microsoft.com/).

2. **검색 지원**에서 다음 문자열을 입력 하 고를 `<operating system version>` 적절 한 운영 체제로 바꾸고 enter 키를 누릅니다.
    
    ```robocopy.exe kbqfe "<operating system version>"```
    
    예를 들어 **robocopy kbqfe "Windows Server 2008 R2"** 를 입력 합니다.

3. 가장 높은 ID 번호 (최신 버전)를 사용 하 여 핫픽스를 찾아서 다운로드 합니다.

4. 서버에 핫픽스를 설치 합니다.

## <a name="step-2-stabilize-files-that-will-be-replicated"></a>2단계: 복제 되는 안정화 파일

서버에 Robocopy의 최신 버전을 설치한 후에는 다음 표에 설명 된 방법을 사용 하 여 잠긴 파일이 복사를 차단 하지 않도록 해야 합니다. 대부분의 응용 프로그램은 파일을 단독으로 잠그지 않습니다. 그러나 정상적인 작업 중에는 파일 서버에서 작은 비율의 파일을 잠글 수 있습니다.

|잠금 원본|설명|완화 방법|
|---|---|---|
|사용자가 공유에서 파일을 원격으로 열 수 있습니다.|직원은 표준 파일 서버에 연결 하 고 문서, 멀티미디어 콘텐츠 또는 기타 파일을 편집 합니다. 기존 홈 폴더 또는 공유 데이터 워크 로드 라고도 합니다.|업무 외 시간에는 Robocopy 작업만 수행 합니다. 이렇게 하면 사전 시드 중 Robocopy에서 건너뛰어야 하는 파일 수가 최소화 됩니다.<br><br>Windows PowerShell **SmbShareAccess** 및 **SmbSession** cmdlet을 사용 하 여 복제 되는 파일 공유에 대 한 읽기 전용 액세스를 일시적으로 설정 하는 것이 좋습니다. 모든 사용자 또는 인증 된 사용자와 같은 공용 그룹에 대 한 사용 권한을 설정 하면 표준 사용자가 단독 잠금으로 파일을 열 가능성이 떨어질 수 있습니다 (파일이 열릴 때 응용 프로그램에서 읽기 전용 액세스를 검색 하는 경우).<br><br>파일에 대 한 액세스를 차단 하거나 **SmbShareAccess** cmdlet을 사용할 수 있도록 해당 서버에 대 한 SMB 포트 445 인바운드에 대 한 임시 방화벽 규칙을 설정 하는 것이 좋습니다. 그러나 이러한 두 메서드는 사용자 작업에 매우 방해가 됩니다.|
|응용 프로그램이 로컬에서 파일을 엽니다.|파일 서버에서 실행 되는 응용 프로그램 워크 로드는 간혹 파일을 잠급니다.|파일을 잠그는 응용 프로그램을 일시적으로 사용 하지 않도록 설정 하거나 제거 합니다. 프로세스 모니터 또는 프로세스 탐색기를 사용 하 여 파일을 잠그는 응용 프로그램을 확인할 수 있습니다. 프로세스 모니터 또는 프로세스 탐색기를 다운로드 하려면 [프로세스 모니터](https://docs.microsoft.com/sysinternals/downloads/procmon) 및 [프로세스 탐색기](https://docs.microsoft.com/sysinternals/downloads/process-explorer) 페이지를 방문 하세요.|

## <a name="step-3-copy-the-replicated-files-to-the-destination-server"></a>3단계: 복제 된 파일을 대상 서버에 복사 합니다.

복제 될 파일에 대 한 잠금을 최소화 한 후에 원본 서버에서 대상 서버로 파일의 초기값을 지정할 수 있습니다.

>[!NOTE]
>원본 컴퓨터 또는 대상 컴퓨터에서 Robocopy를 실행할 수 있습니다. 다음 절차에서는 최신 운영 체제를 실행 하는 대상 서버에서 Robocopy를 실행 하 여 최신 운영 체제에서 제공할 수 있는 추가 Robocopy 기능을 활용 하는 방법을 설명 합니다.

### <a name="preseed-the-replicated-files-onto-the-destination-server-with-robocopy"></a>Robocopy를 사용 하 여 복제 된 파일을 대상 서버에 사전 시드

1. 원본 및 대상 서버에서 로컬 관리자 그룹의 구성원 인 계정을 사용 하 여 대상 서버에 로그인 합니다.

2. 관리자 권한 명령 프롬프트를 엽니다.

3. 원본 서버에서 대상 서버로 파일을 사전 초기값으로 지정 하려면 다음 명령을 실행 합니다 .이 명령은 대괄호로 묶은 값에 대해 고유한 원본, 대상 및 로그 파일 경로를 대체 합니다.
    
    ```PowerShell
    robocopy "<source replicated folder path>" "<destination replicated folder path>" /e /b /copyall /r:6 /w:5 /MT:64 /xd DfsrPrivate /tee /log:<log file path> /v
    ```
    
    이 명령은 다음 매개 변수를 사용 하 여 원본 폴더의 모든 내용을 대상 폴더에 복사 합니다.
    
    |매개 변수|설명|
    |---|---|
    |"\<원본 복제 폴더 경로\>"|대상 서버에서 사전 초기값으로 원본 폴더를 지정 합니다.|
    |"\<대상 복제 된 폴더\>경로"|사전 시드 된 파일을 저장할 폴더의 경로를 지정 합니다.<br><br>대상 폴더가 대상 서버에 아직 없어야 합니다. 일치 하는 파일 해시를 가져오기 위해 Robocopy는 파일의 초기값으로 루트 폴더를 만들어야 합니다.|
    |/e|하위 디렉터리와 해당 파일 뿐만 아니라 빈 하위 디렉터리를 복사 합니다.|
    |/b|백업 모드에서 파일을 복사 합니다.|
    |/copyall|데이터, 특성, 타임 스탬프, NTFS ACL (액세스 제어 목록), 소유자 정보 및 감사 정보를 비롯 한 모든 파일 정보를 복사 합니다.|
    |/r: 6|오류가 발생 하는 경우 작업을 6 번 다시 시도 합니다.|
    |/w: 5|재시도 사이에 5 초 동안 기다립니다.|
    |MT: 64|64 파일을 동시에 복사 합니다.|
    |/xd DfsrPrivate|DfsrPrivate 폴더를 제외 합니다.|
    |/tee|로그 파일 뿐만 아니라 콘솔 창에 상태 출력을 씁니다.|
    |/log \<로그 파일 경로 >|쓸 로그 파일을 지정 합니다. 파일의 기존 내용을 덮어씁니다. (기존 로그 파일에 항목을 추가 하려면를 사용 `/log+ <log file path>`합니다.)|
    |/v|건너뛴 파일이 포함 된 자세한 정보 출력을 생성 합니다.|
    
    예를 들어 다음 명령은 원본 복제 폴더 E:\\RF01의 파일을 대상 서버의 데이터 드라이브 D에 복제 합니다.
    
    ```PowerShell
    robocopy.exe "\\srv01\e$\rf01" "d:\rf01" /e /b /copyall /r:6 /w:5 /MT:64 /xd DfsrPrivate /tee /log:c:\temp\preseedsrv02.log
    ```
    
    >[!NOTE]
    >Robocopy를 사용 하 여 DFS 복제에 대 한 파일을 미리 시드 하는 경우 위에 설명 된 매개 변수를 사용 하는 것이 좋습니다. 그러나 해당 값의 일부를 변경 하거나 매개 변수를 더 추가할 수 있습니다. 예를 들어, */mt* 매개 변수에 대해 더 높은 값 (스레드 수)을 설정 하기 위한 용량이 있는지 테스트를 확인할 수 있습니다. 또한 주로 큰 파일을 복제 하는 경우 버퍼링 되지 않은 i/o에 대해 **/j** 옵션을 추가 하 여 복사 성능을 높일 수 있습니다. Robocopy 매개 변수에 대 한 자세한 내용은 [robocopy](https://docs.microsoft.com/windows-server/administration/windows-commands/robocopy) 명령줄 참조를 참조 하세요.

    >[!WARNING]
    >Robocopy를 사용 하 여 DFS 복제에 대 한 파일을 미리 시드 하는 경우 데이터 손실을 방지 하려면 권장 되는 매개 변수를 다음과 같이 변경 하지 마십시오.
    >- */Mir* 매개 변수를 사용 하지 마세요 (디렉터리 트리를 미러링) 또는 */sv* 매개 변수 (파일을 이동한 다음 소스에서 삭제).
    >-  **/E**, **/b**및 **/stall** 옵션은 제거 하지 마십시오.

4. 복사가 완료 되 면 로그에서 오류 또는 건너뛴 파일을 검사 합니다. Robocopy를 사용 하 여 전체 파일 집합을 다시 복사 하는 대신 건너뛴 파일을 개별적으로 복사 합니다. 배타적 잠금으로 인해 파일을 건너뛴 경우 나중에 Robocopy를 사용 하 여 개별 파일을 복사 하거나 이러한 파일에 초기 동기화 중에 DFS 복제 하 여 실시간 복제를 수행 해야 한다는 것을 허용 합니다.

## <a name="next-step"></a>다음 단계

초기 복사를 완료 한 후 Robocopy를 사용 하 여 가능한 많은 건너뛴 파일의 문제를 해결 한 후 Windows PowerShell 또는 **Dfsrdiag** 명령에서 **DfsrFileHash** cmdlet을 사용 하 여 다음을 비교 하 여 사전 시드 된 파일의 유효성을 검사 합니다. 원본 및 대상 서버의 파일 해시 자세한 내용은 2 [단계: DFS 복제](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn495042(v%3dws.11)>)에 대해 preseeded 파일의 유효성을 검사 합니다.
