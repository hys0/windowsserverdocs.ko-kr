---
title: DFS 복제에 대 한 파일을 미리 시드하고를 Robocopy를 사용 하 여
description: DFS 복제에 대 한 파일을 미리 시드하고를 Robocopy.exe를 사용 하는 방법입니다.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 05/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: a7a14b1a1e0f91002b201869e4c68187ffaf3f8f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59865084"
---
# <a name="use-robocopy-to-preseed-files-for-dfs-replication"></a>DFS 복제에 대 한 파일을 미리 시드하고를 Robocopy를 사용 하 여

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

이 항목에서는 명령줄 도구를 사용 하는 방법에 설명 **Robocopy.exe**, Windows Server의 분산 파일 시스템 (DFS) 복제 (DFSR 또는 Dfs-r 라고도 함)에 대 한 복제를 설정할 때 파일을 미리 시드하고 하 합니다. DFS 복제를 설정 하기 전에 파일을 preseeding, 새 복제 파트너를 추가 또는 교체 서버에서 초기 동기화의 속도 Windows Server 2012 R2에서 DFS 복제 데이터베이스의 복제를 사용 하도록 설정 합니다. Robocopy 메서드를 사용 하면 여러 preseeding 메서드 중 하나인 개요를 보려면 [1 단계: DFS 복제에 대 한 파일을 미리 시드하고](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn495046(v%3dws.11)>)합니다.

Robocopy (강력한 파일 복사) 명령줄 유틸리티의 Windows Server를 사용 하 여 포함 되어 있습니다. 유틸리티 복사 보안, 백업 API 지원, 다시 시도 기능 및 로깅을 포함 하는 광범위 한 옵션을 제공 합니다. 이후 버전에는 다중 스레딩 및 버퍼링 되지 않은 I/O 지원을 포함 됩니다.

>[!IMPORTANT]
>Robocopy는 단독으로 잠긴된 파일을 복사 하지 않습니다. 사용자, 파일 서버에서 오랫동안 많은 파일을 잠글 경우 다른 preseeding 메서드를 사용 하는 것이 좋습니다. Preseeding 원본 및 대상 서버에서 파일 목록 간의 완벽 한 일치 하는 필요 하지 않지만 떨어집니다 preseeding DFS 복제에 대 한 초기 동기화가 수행 하는 경우 존재 하지 않는 파일이 많을 수록 됩니다. 잠금 충돌을 최소화 하려면 조직에 대 한 사용량이 적은 시간 동안 Robocopy를 사용 합니다. 항상 파일 배타적 잠금으로 인해 건너뛴 이해 하도록 preseeding 후 Robocopy 로그를 검사 합니다.

Robocopy를 사용 하 여 DFS 복제에 대 한 파일을 미리 시드하고 하려면 다음이 단계를 수행 합니다.

1. [다운로드 하 고 Robocopy의 최신 버전을 설치 합니다.](#step-1:-download-and-install-the-latest-version-of-robocopy)
2. [복제할 파일을 안정화 합니다.](#step-2:-stabilize-files-that-will-be-replicated)
3. [대상 서버에 복제 된 파일을 복사 합니다.](#step-3:-copy-the-replicated-files-to-the-destination-server)

## <a name="prerequisites"></a>사전 요구 사항

Preseeding DFS 복제 직접 포함 되지 않은, 때문에 Robocopy 사용 하 여 파일 복사를 수행 하는 것에 대 한 요구 사항을 충족 해야 합니다.

- 원본 및 대상 서버의 로컬 관리자 그룹의 구성원 인 계정이 필요 합니다.

- 파일을 복사 하는 데 사용할 서버인 Robocopy의 최신 버전 설치-원본 서버나 대상 서버 운영 체제 버전에 대 한 최신 버전을 설치 해야 합니다. 자세한 내용은 [2 단계: 복제할 파일 안정화](#step-2:-stabilize-files-that-will-be-replicated)합니다. Windows Server 2003 R2를 실행 하는 서버에서 파일, preseeding 하는 경우가 아니면 Robocopy 원본 또는 대상 서버에서 실행할 수 있습니다. 일반적으로 최신 운영 체제 버전에는 대상 서버 Robocopy의 최신 버전에 액세스할 수 있습니다.

- 충분 한 저장소 공간이 대상 드라이브에 사용할 수 있는지 확인 합니다. 경로 복사 하려는 폴더를 만들지 마세요. Robocopy는 루트 폴더를 만들어야 합니다.
    
    >[!NOTE]
    >Preseeded 파일에 할당할 공간을 결정 하는 경우 DFS 복제에 대 한 시간 및 저장소 요구 사항을 통해 예상 되는 데이터 증가 고려 합니다. 계획 도움말을 참조 하세요 [준비 폴더와 충돌 및 삭제 하는 폴더의 할당량 크기 편집](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754229(v=ws.11)) 에 [DFS 복제 관리](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754771(v=ws.11)>)합니다.

- 원본 서버에서 필요에 따라 프로세스 모니터 또는 파일을 사용 하는 응용 프로그램에 대 한 확인 하는 데 사용할 수 있는 프로세스 탐색기를 설치 합니다. 다운로드 정보를 참조 하세요 [Process Monitor](https://docs.microsoft.com/sysinternals/downloads/procmon) 하 고 [Process Explorer](https://docs.microsoft.com/sysinternals/downloads/process-explorer)합니다.

## <a name="step-1-download-and-install-the-latest-version-of-robocopy"></a>1단계: Robocopy의 최신 버전 다운로드 및 설치

Robocopy를 사용 하 여 파일을 미리 시드하고 먼저 다운로드 하 고 최신 버전의를 설치 해야 **Robocopy.exe**합니다. 이렇게 하면 DFS 복제가 Robocopy의 배송 버전 내의 문제로 인해 파일을 건너뛰지 않습니다.

호환 되는 최신 Robocopy 버전에 대 한 원본 서버에서 실행 되는 Windows Server의 버전에 따라 달라 집니다. Robocopy에 대 한 Windows Server 2008 R2 또는 Windows Server 2008의 최신 버전을 사용 하 여 핫픽스를 다운로드 하는 방법에 대 한 내용은 [Windows Server 2008에서 파일 시스템 (DFS (분산) 기술에 대 한 현재 사용할 수 있는 핫픽스 목록은 및 Windows Server 2008 R2](https://support.microsoft.com/help/968429/list-of-currently-available-hotfixes-for-distributed-file-system-dfs-t)합니다.

또는 찾습니다 하 고 다음 단계를 수행 하 여 운영 체제에 대 한 최신 핫픽스를 설치할 수 있습니다.

### <a name="locate-and-install-the-latest-version-of-robocopy-for-a-specific-version-of-windows-server"></a>검색 및 특정 버전의 Windows Server에 대 한 Robocopy의 최신 버전 설치

1. 웹 브라우저에서 엽니다 [ https://support.microsoft.com ](https://support.microsoft.com/)합니다.

2. **검색 지원**, 다음을 입력 문자열 대체 `<operating system version>` 적절 한 운영 체제, Enter 키를 눌러 다음:
    
    ```robocopy.exe kbqfe "<operating system version>"```
    
    예를 들어 입력 **robocopy.exe 프로그램 창을 "Windows Server 2008 R2"** 합니다.

3. 찾은 ID 번호가 가장 높은 (즉, 최신 버전)를 사용 하 여 핫픽스를 다운로드 합니다.

4. 서버에 핫픽스를 설치 합니다.

## <a name="step-2-stabilize-files-that-will-be-replicated"></a>2단계: 복제할 파일 안정화

서버의 Robocopy의 최신 버전을 설치한 후 다음 표에 설명 된 메서드를 사용 하 여 차단 복사에서 잠긴된 파일을 해제 해야 합니다. 대부분의 응용 프로그램 단독으로 파일을 잠그지 않습니다. 그러나 정상 작동 중 적은 비율 파일의 파일 서버에 잠겨 있습니다.

|원본 잠금|설명|완화 방법|
|---|---|---|
|사용자는 원격 공유의 파일을 엽니다.|직원 표준 파일 서버에 연결한 문서, 멀티미디어 콘텐츠 또는 기타 파일을 편집 합니다. 라고도 기존 홈 폴더 또는 공유 데이터 워크 로드.|작업만 수행할 Robocopy 중, 사용량이 적은 업무 외 시간입니다. Robocopy preseeding 중 건너뛰어야 하는 파일의 수를 최소화 합니다.<br><br>일시적으로 Windows PowerShell을 사용 하 여 복제할 파일 공유에 대 한 읽기 전용 액세스를 설정 하는 것이 좋습니다 **부여 SmbShareAccess** 하 고 **Close SmbSession** cmdlet. Everyone 또는 Authenticated Users와 같은 일반 그룹에 대 한 권한이 읽기로 설정 하면 표준 사용자 (파일을 열면 읽기 전용 액세스를 검색 하는 응용 프로그램) 하는 경우 배타적 잠금을 사용 하 여 파일을 열려는 지 못할 수 있습니다.<br><br>임시 방화벽 규칙 설정 하는 것도 고려할 SMB 포트 445를 파일에 대 한 액세스를 차단 하거나 사용 하 여 해당 서버에 인바운드 합니다 **블록 SmbShareAccess** cmdlet. 그러나 두 이러한 메서드는 사용자 작업에 지장을 주지 매우입니다.|
|응용 프로그램 로컬 파일을 엽니다.|파일을 잠그지 하는 경우에 따라 파일 서버에서 실행 하는 응용 프로그램 워크 로드.|일시적으로 사용 하지 않도록 설정 하거나 파일을 사용 하는 응용 프로그램을 제거 합니다. 응용 프로그램 파일을 사용 중인 결정할 프로세스 모니터 또는 프로세스 탐색기를 사용할 수 있습니다. 프로세스 모니터 또는 프로세스 탐색기를 다운로드 하려면 다음을 방문 합니다 [프로세스 모니터](https://docs.microsoft.com/sysinternals/downloads/procmon) 하 고 [Process Explorer](https://docs.microsoft.com/sysinternals/downloads/process-explorer) 페이지.|

## <a name="step-3-copy-the-replicated-files-to-the-destination-server"></a>3단계: 대상 서버에 복제 된 파일을 복사 합니다.

복제할 파일에 대 한 잠금을 최소화 한 후 대상 서버에 원본 서버에서 파일을 미리 시드하고 수 있습니다.

>[!NOTE]
>Robocopy는 원본 컴퓨터 또는 대상 컴퓨터에서 실행할 수 있습니다. 다음 절차에서는 일반적으로 최신 운영 체제를 제공할 수 있는 모든 추가 Robocopy 기능을 활용 하려면 최신 운영 체제를 실행 하는 대상 서버의 Robocopy를 실행 합니다.

### <a name="preseed-the-replicated-files-onto-the-destination-server-with-robocopy"></a>Robocopy 사용 하 여 대상 서버에 복제 된 파일을 미리 시드하십시오

1. 원본 및 대상 서버의 로컬 관리자 그룹의 구성원 인 계정 사용 하 여 대상 서버에 로그인 합니다.

2. 관리자 권한 명령 프롬프트를 엽니다.

3. 원본에서 대상 서버로 파일을 미리 시드하고에 고유한 소스, 대상 및 대괄호로 묶은 값에 대 한 로그 파일 경로 대체 하 고 다음 명령을 실행 합니다.
    
    ```PowerShell
    robocopy "<source replicated folder path>" "<destination replicated folder path>" /e /b /copyall /r:6 /w:5 /MT:64 /xd DfsrPrivate /tee /log:<log file path> /v
    ```
    
    이 명령은 다음 매개 변수를 사용 하 여 대상 폴더를 원본 폴더의 모든 내용을 복사합니다.
    
    |매개 변수|설명|
    |---|---|
    |"\<원본 폴더 경로 복제\>"|대상 서버에서 미리 시드하고 원본 폴더를 지정 합니다.|
    |"\<대상 폴더 경로 복제\>"|Preseeded 파일을 보관할 폴더 경로를 지정 합니다.<br><br>대상 폴더 대상 서버에 이미 존재 하지 해야 합니다. 일치 하는 파일 해시를 가져오려면 Robocopy 파일 preseeds 해당 하는 경우 루트 폴더를 만들어야 합니다.|
    |/e|하위 디렉터리 및 해당 파일 뿐만 아니라 빈 디렉터리를 복사합니다.|
    |/b|백업 모드에서 파일을 복사 합니다.|
    |/copyal|감사 정보 및 데이터, 특성, 타임 스탬프, NTFS ACL (액세스 제어 목록), 소유자 정보를 포함 하 여 모든 파일 정보를 복사 합니다.|
    |/r:6|6 배 작업 다시 시도 오류가 발생 합니다.|
    |/w:5|다시 시도 간에 5 초 동안 대기합니다.|
    |MT:64|64 파일을 동시에 복사합니다.|
    |/xd DfsrPrivate|DfsrPrivate 폴더를 제외합니다.|
    |/tee|로그 파일 뿐만 아니라 콘솔 창에 상태 출력을 씁니다.|
    |로그 \<로그 파일 경로 >|쓸 로그 파일을 지정 합니다. 파일의 기존 내용을 덮어씁니다. (기존 로그 파일에 항목 추가를 사용 하 여 `/log+ <log file path>`.)|
    |/v|건너뛴 포함 하는 자세한 정보 출력을 생성 합니다.|
    
    다음 명령은 e: 복제 원본 폴더에서 파일을 복제 하는 예를 들어\\RF01, 대상 서버에서 데이터 드라이브 D:
    
    ```PowerShell
    robocopy.exe "\\srv01\e$\rf01" "d:\rf01" /e /b /copyall /r:6 /w:5 /MT:64 /xd DfsrPrivate /tee /log:c:\temp\preseedsrv02.log
    ```
    
    >[!NOTE]
    >Robocopy를 사용 하 여 DFS 복제에 대 한 파일을 미리 시드하고 위에 설명 된 매개 변수를 사용 하는 것이 좋습니다. 그러나 해당 값의 일부를 변경할 수도 있고 추가 매개 변수를 추가할 수 있습니다. 예를 들어 할에 대 한 (스레드 개수) 값을 높게 설정 하는 역량을 보유 하는 테스트를 통해 합니다 */MT* 매개 변수입니다. 또한 경우 주로 더 큰 파일을 복제할 수 있습니다를 추가 하 여 복사 성능을 향상 시키기 위해 합니다 **/j** 버퍼링 되지 않은 I/O에 대 한 옵션입니다. Robocopy 매개 변수에 대 한 자세한 내용은 참조는 [Robocopy](https://docs.microsoft.com/windows-server/administration/windows-commands/robocopy) 명령줄 참조 합니다.

    >[!WARNING]
    >Robocopy를 사용 하 여 DFS 복제에 대 한 파일을 미리 시드하고 때 잠재적인 데이터 손실을 방지 하려면 권장 되는 매개 변수를 다음과 같이 변경할 하지 않습니다.
    >- 사용 하지 않는 합니다 */mir* (즉 디렉터리 트리를 미러링합니다) 매개 변수 또는 */mov* (하는 매개 변수 파일을 이동한 다음 원본에서 삭제).
    >-  제거 하지 마십시오 합니다 **/e**를 **/b**, 및 **/copyall** 옵션입니다.

4. 복사 완료 된 후에 오류 또는 건너뛴된 파일에 대 한 로그를 검토 하세요. Robocopy를 사용 하 여 파일의 전체 집합을 다시 복사 하는 대신에 개별적으로 건너뛴된 파일에 복사 합니다. 파일 때문에 건너뛴 경우 배타적 잠금을 나중 Robocopy 사용 하 여 개별 파일을 복사 또는 시도 파일과 초기 동기화 동안 DFS 복제에서 네트워크를 통해 복제 해야는 허용 합니다.

## <a name="next-step"></a>다음 단계

사용할 초기 복사를 완료 하 고 최대한 많은 건너뛴된 파일을 사용 하 여 문제를 해결 하는 Robocopy를 사용 합니다 **Get DfsrFileHash** Windows PowerShell cmdlet 또는 **Dfsrdiag** 명령 원본 및 대상 서버에서 파일 해시를 비교 하 여 preseeded 파일의 유효성을 검사 합니다. 자세한 내용은 참조 하세요. [2 단계: DFS 복제용 Preseeded 파일 유효성을 검사](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn495042(v%3dws.11)>)합니다.