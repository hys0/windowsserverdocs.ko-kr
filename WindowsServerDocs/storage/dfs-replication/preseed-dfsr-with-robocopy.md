---
title: Robocopy를 사용 하 여 DFS 복제를 위해 파일을 preseed
description: DFS 복제를 위해 파일을 preseed를 Robocopy.exe를 사용 하는 방법입니다.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 05/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: a7a14b1a1e0f91002b201869e4c68187ffaf3f8f
ms.sourcegitcommit: e0479b0114eac7f232e8b1e45eeede96ccd72b26
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/22/2018
ms.locfileid: "2082479"
---
# <a name="use-robocopy-to-preseed-files-for-dfs-replication"></a>Robocopy를 사용 하 여 DFS 복제를 위해 파일을 preseed

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

이 항목에서는 명령줄 도구, **Robocopy.exe**, Windows Server의 경우 파일 DFS (분산 시스템) 복제 (DFSR 또는 DFS-R 라고도 함)에 대 한 복제를 설정할 때 파일을 preseed를 사용 하는 방법에 설명 합니다. DFS 복제를 설정 하기 전에 파일을 preseeding, 하 여 새 복제 파트너를 추가 하거나 서버를 교체, 초기 동기화를 신속 하 고 Windows Server 2012 r 2의 DFS 복제 데이터베이스의 복제를 활성화할 수 있습니다. Robocopy 방법은 여러 preseeding 메서드; 중 하나 에 대 한 개요를 참조 [1 단계: DFS 복제를 위해 파일을 preseed](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn495046(v%3dws.11)>)합니다.

Robocopy (강력한 파일 복사본) 명령줄 유틸리티의 Windows Server와 함께 포함 됩니다. 이 유틸리티 복사 보안, 백업 API 지원, 다시 시도 기능 및 로깅을 포함 하는 광범위 한 옵션을 제공 합니다. 이후 버전 다중 스레딩 및 버퍼링 되지 않은 I/O 지원을 포함 합니다.

>[!IMPORTANT]
>Robocopy 단독으로 잠긴된 파일을 복사 하지 않습니다. 파일 서버에 오랜 시간 동안에 대 한 많은 파일을 잠글는 일반적으로 사용자를 다른 preseeding 메서드를 사용 하는 것이 좋습니다. Preseeding 원본 및 대상 서버에서 파일 목록 간에 완벽 하 게 일치 하는 필요 하지 않지만 효율성이 떨어지는 preseeding DFS 복제에 대 한 초기 동기화가 수행 하는 경우에 존재 하지 않는 더 많은 파일 됩니다. 잠금 충돌을 최소화 하려면 조직에 대 한 사용량이 많지 않은 시간 동안 Robocopy를 사용 합니다. 항상 어떤 파일이 단독 잠금 때문에 건너뛴 파악 하려면 preseeding 후 Robocopy 로그를 검사 합니다.

Robocopy를 사용 하 여 DFS 복제를 위해 파일을 preseed를 하려면 다음이 단계를 따릅니다.

1. [다운로드 하 고 Robocopy의 최신 버전을 설치 합니다.](#step-1:-download-and-install-the-latest-version-of-robocopy)
2. [파일 복제 되는 것을 안정을 합니다.](#step-2:-stabilize-files-that-will-be-replicated)
3. [대상 서버에 복제 된 파일을 복사 합니다.](#step-3:-copy-the-replicated-files-to-the-destination-server)

## <a name="prerequisites"></a>사전 요구 사항

Preseeding DFS 복제를 직접 포함 하지 않는, 때문에 Robocopy 가진 파일 복사본을 수행 하기 위한 요구 사항을 충족 해야 합니다.

- 원본 및 대상 서버에서 로컬 Administrators 그룹의 구성원 인 계정을 해야 합니다.

- 사용할 파일을 복사 하는 서버에서 Robocopy의 최신 버전을 설치-원본 서버 또는 대상 서버입니다. 운영 체제 버전에 대 한 최신 버전을 설치 해야 합니다. 자세한 내용은 [2 단계: 파일 복제 되는 것을 안정을](#step-2:-stabilize-files-that-will-be-replicated)합니다. Windows Server 2003 r 2를 실행 하는 서버에서 파일을 preseeding 하는 경우가 아니면 원본 또는 대상 서버의 Robocopy를 실행할 수 있습니다. 최신 운영 체제 버전에 일반적으로는 대상 서버 Robocopy의 최신 버전에 액세스할 수 있습니다.

- 충분 한 저장 공간이 대상 드라이브에 사용할 수 있는지 확인 합니다. 복사 하려는 경로에서 폴더를 만들지 마십시오: Robocopy 루트 폴더를 만들어야 합니다.
    
    >[!NOTE]
    >Preseeded 파일에 대해 할당할 공간을 결정 하는 경우 DFS 복제에 대 한 시간 및 저장소 요구 사항을 통해 예상 되는 데이터 증가 고려 합니다. 도움말을 계획 하는 것에 대 한 [DFS 복제 관리](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754771(v=ws.11)>)에서 [준비 폴더와 충돌 및 삭제 된 폴더의 할당량 크기를 편집](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754229(v=ws.11)) 을 참조 하십시오.

- 원본 서버의 프로세스 모니터] 또는 [파일 잠금 되는 응용 프로그램에 대 한 확인 하는데 사용할 수 있는 프로세스 탐색기를 설치할 수도 있습니다. 다운로드 정보 [프로세스 모니터](https://docs.microsoft.com/sysinternals/downloads/procmon) 및 [프로세스 탐색기](https://docs.microsoft.com/sysinternals/downloads/process-explorer)를 참조 하십시오.

## <a name="step-1-download-and-install-the-latest-version-of-robocopy"></a>1 단계: 다운로드 하 고 Robocopy의 최신 버전을 설치 합니다.

전에 Robocopy를 사용 하 여 파일을 preseed를 다운로드 하 고 **Robocopy.exe**의 최신 버전을 설치 해야 합니다. 이렇게 하면 DFS 복제 Robocopy의 배송 버전 내에서 문제로 인해 파일을 건너뛰고 하지 않습니다.

호환 되는 최신 Robocopy 버전에 대 한 원본 서버에서 실행 되는 Windows server 버전에 따라 달라 집니다. Robocopy에 대 한 Windows Server 2008 R2 또는 Windows Server 2008의 최신 버전으로 핫픽스를 다운로드 하는 방법에 대 한 정보를 파일 시스템 DFS (분산) 기술 및 Windows Server 2008에 대 한 현재 사용할 수 있는 핫픽스 목록이 [를 참조 하십시오. Windows Server 2008 R2](https://support.microsoft.com/help/968429/list-of-currently-available-hotfixes-for-distributed-file-system-dfs-t)합니다.

또는 찾을 수 있으며 다음 단계를 수행 하 여 운영 체제에 대 한 최신 핫픽스를 설치할 수 있습니다.

### <a name="locate-and-install-the-latest-version-of-robocopy-for-a-specific-version-of-windows-server"></a>찾아 특정 버전의 Windows Server에 대 한 Robocopy의 최신 버전을 설치 합니다.

1. 웹 브라우저에서 엽니다 [https://support.microsoft.com](https://support.microsoft.com/)합니다.

2. **검색 지원**다음을 입력 하는 문자열을 대체 `<operating system version>` 적절 한 운영 체제, 다음은 Enter 키를 누릅니다.
    
    ```robocopy.exe kbqfe "<operating system version>"```
    
    예, **robocopy.exe 프로그램 창을 "Windows Server 2008 r 2"를**입력 합니다.

3. 페이지를 찾아 가장 높은 ID 번호 (즉, 최신 버전)를 가진 핫픽스를 다운로드 합니다.

4. 서버에서 핫픽스를 설치 합니다.

## <a name="step-2-stabilize-files-that-will-be-replicated"></a>2 단계: 안정을 복제 될 파일

서버에서 Robocopy의 최신 버전을 설치한 후 다음 표에 설명 된 방법을 사용 하 여 차단 복사에서 잠긴된 파일을 해제 해야 합니다. 대부분의 응용 프로그램 파일을 단독으로 잠글 하지 않습니다. 그러나 정상 조건 동안 파일의 작은 비율 파일 서버에 고정 될 수 있습니다.

|잠금을 원본|설명|완화|
|---|---|---|
|사용자는 원격 공유에 있는 파일을 엽니다.|직원 표준 파일 서버에 연결 하 고 문서, 멀티미디어 콘텐츠 또는 기타 파일을 편집 합니다. 라고도 함 전통적인 홈 폴더 또는 공유 데이터 작업 합니다.|Robocopy 작업 하는 동안에 수행 사용량이, 업무 시간입니다. 이 최소화 Robocopy preseeding 하는 동안 건너뛸 해야 하는 파일의 수입니다.<br><br>Windows PowerShell **부여 SmbShareAccess** 및 **닫기를 SmbSession** cmdlet을 사용 하 여 복제 됩니다 하는 파일 공유에서 읽기 전용 액세스를 일시적으로 설정 하는 것이 좋습니다. 모든 사용자 또는 인증 된 사용자와 같은 일반적인 그룹에 대 한 사용 권한 읽기를 설정한 경우에 표준 사용자 되지 않을 (파일을 열 때 읽기 전용 액세스를 검색 하는 해당 응용 프로그램) 하는 경우 단독 잠금 파일을 열 수 있습니다.<br><br>임시 방화벽 규칙을 설정 하는 것도 고려할 SMB 포트 445로의 인바운드 파일에 대 한 액세스를 차단 또는 **차단 SmbShareAccess** cmdlet을 사용 하는 서버입니다. 그러나 이러한 두가지 방법은 사용자 작업을 매우 손상 된.|
|응용 프로그램 로컬 파일을 엽니다.|때때로 파일 서버에서 실행 되는 응용 프로그램 작업 파일을 잠급니다.|일시적으로 사용 하지 않도록 설정 하거나 파일 잠금 되는 응용 프로그램을 제거 합니다. 응용 프로그램 파일 잠금는 확인 하려면 프로세스 모니터] 또는 [프로세스 탐색기를 사용할 수 있습니다. 프로세스 모니터] 또는 [프로세스 탐색기를 다운로드 하려면 [프로세스 모니터](https://docs.microsoft.com/sysinternals/downloads/procmon) 및 [프로세스 탐색기](https://docs.microsoft.com/sysinternals/downloads/process-explorer) 페이지를 참고 하십시오.|

## <a name="step-3-copy-the-replicated-files-to-the-destination-server"></a>3 단계: 대상 서버로 복제 된 파일에 복사

복제 되는 것은 파일에 대 한 잠금을 최소화 한 후에 대상 서버에 원본 서버에서 파일 preseed 수 있습니다.

>[!NOTE]
>Robocopy 원본 컴퓨터 또는 대상 컴퓨터에서 실행할 수 있습니다. 다음 절차에서는 Robocopy 일반적으로 최신 운영 체제를 제공할 수 있는 모든 추가 Robocopy 기능을 활용 하는 최신 운영 체제를 실행 하는 대상 서버에서 실행에 대해 설명 합니다.

### <a name="preseed-the-replicated-files-onto-the-destination-server-with-robocopy"></a>Preseed Robocopy와 대상 서버에 복제 된 파일

1. 원본 및 대상 서버에서 로컬 Administrators 그룹의 구성원 인 계정 사용 하 여 대상 서버에 로그인 합니다.

2. 관리자 권한 명령 프롬프트를 엽니다.

3. 대상 서버에는 원본에서 파일을 preseed를 직접 원본, 대상 및 괄호로 묶인된 값에 대 한 로그 파일 경로 대체 하는 다음 명령을 실행 합니다.
    
    ```PowerShell
    robocopy "<source replicated folder path>" "<destination replicated folder path>" /e /b /copyall /r:6 /w:5 /MT:64 /xd DfsrPrivate /tee /log:<log file path> /v
    ```
    
    이 명령은 다음 매개 변수를 사용 하 고 대상 폴더를 원본 폴더의 모든 내용을 복사합니다.
    
    |매개 변수|설명|
    |---|---|
    |"< 소스 복제 된 폴더 경로 > \"|대상 서버에서 preseed를 원본 폴더를 지정 합니다.|
    |"\ < 대상 폴더 경로 복제 >"|Preseeded 파일을 저장할 폴더의 경로를 지정 합니다.<br><br>대상 폴더 대상 서버에 이미 존재 하지 해야 합니다. 일치 하는 파일 해시를 얻으려면 Robocopy 파일을 preseeds 때 루트 폴더를 만들어야 합니다.|
    |/e|하위 디렉터리와 해당 파일을으로 빈 하위 디렉터리에 복사합니다.|
    |/ b|백업 모드에서 파일을 복사 합니다.|
    |copyal /|모든 파일 정보, 데이터, 특성, 타임 스탬프, NTFS 액세스 제어 목록 (ACL), 소유자 정보를 포함 하 고 감사 정보를 복사 합니다.|
    |/r:6|6 번 작업 다시 시도 오류가 발생 합니다.|
    |/w:5|다시 시도 간격 (초)를 5에서 대기합니다.|
    |MT:64|동시에 64 파일을 복사합니다.|
    |/xd DfsrPrivate|DfsrPrivate 폴더를 제외합니다.|
    |/tee|로그 파일에 있는 뿐만 아니라 콘솔 창에 상태 출력을 씁니다.|
    |로그 / \ < 로그 파일 경로 >|쓸 로그 파일을 지정 합니다. 파일의 기존 내용을 덮어씁니다. (사용 하 여 기존 로그 파일에 있는 항목을 추가할 `/log+ <log file path>`.)|
    |/v|건너뛴 파일을 포함 하는 자세한 출력을 생성 합니다.|
    
    예 다음 명령은 대상 서버에서 D 데이터 드라이브를 복제 하는 원본 폴더의 E:\\RF01, 파일을 복제:
    
    ```PowerShell
    robocopy.exe "\\srv01\e$\rf01" "d:\rf01" /e /b /copyall /r:6 /w:5 /MT:64 /xd DfsrPrivate /tee /log:c:\temp\preseedsrv02.log
    ```
    
    >[!NOTE]
    >Robocopy를 사용 하 여 DFS 복제를 위해 파일을 preseed 위에서 설명한 매개 변수를 사용 하는 것이 좋습니다. 그러나 일부 해당 값을 변경 하거나 추가 매개 변수를 추가할 수 있습니다. 예 값을 설정 하려면 더 높은 (스레드 수가) */MT* 매개 변수에 대 한 용량 한다고는 테스트를 통해 찾을 수 있습니다. 또한 더 큰 파일을 복제 기본적으로 표시 됩니다 하는 경우에 버퍼링 되지 않은 I/O에 대 한 **/j** 옵션을 추가 하 여 복사본 성능을 향상 시킬 수 있습니다. Robocopy 매개 변수에 대 한 자세한 내용은 [Robocopy](https://docs.microsoft.com/windows-server/administration/windows-commands/robocopy) 명령줄 참조를 참조 하십시오.

    >[!WARNING]
    >Robocopy를 사용 하 여 DFS 복제를 위해 파일을 preseed를 데이터 손실을 방지 하려면 권장된 매개 변수를 다음과 같이 변경을 지정 하지 마십시오.
    >- (미러링 하는 디렉터리 트리) */mir* 매개 변수 또는 (하 고 파일을 이동 하는 다음 원본에서이 삭제) */mov* 매개 변수를 사용 하지 마십시오.
    >-  **/E**, **/ b**및 **/copyall** 옵션을 제거 하지 마십시오.

4. 복사를 완료 한 후에 모든 오류 또는 건너뛴된 파일에 대 한 로그를 검사 합니다. Robocopy를 사용 하 여 파일의 전체 집합을 다시 복사 하는 대신에 개별적으로 건너뛴된 파일을 복사 합니다. 파일 하기 때문에 건너뛴 경우 단독 잠금 나중에 Robocopy와 개별 파일을 복사 또는 시도 수락 파일만 초기 동기화 하는 동안 DFS 복제 하 여 실시간을 통한 복제를 필요 합니다.

## <a name="next-step"></a>다음 단계

비교 하 여 preseeded 파일의 유효성을 검사 하려면 Windows PowerShell 또는 **Dfsrdiag** 명령에서 **Get DfsrFileHash** cmdlet을 사용 합니다 초기 복사본을 완료 하 고 Robocopy를 사용 하 여 최대한 많은 건너뛴된 파일이 포함 된 문제를 해결 한 후 원본 및 대상 서버에서 파일 해시 합니다. 자세한 내용은 참조 하십시오. [2 단계: DFS 복제를 위해 Preseeded 파일의 유효성을 검사](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn495042(v%3dws.11)>)합니다.