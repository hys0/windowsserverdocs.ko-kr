---
title: Robocopy를 사용하여 DFS 복제용 파일 미리 시드
description: Robocopy.exe를 사용하여 DFS 복제용 파일을 미리 시드하는 방법을 설명합니다.
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 05/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: ea5cd954dde6d4fa8fcaa7874f75cb9588115ab1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402131"
---
# <a name="use-robocopy-to-preseed-files-for-dfs-replication"></a>Robocopy를 사용하여 DFS 복제용 파일 미리 시드

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

이 토픽에서는 Windows Server에서 DFSR 또는 DFS-R이라고도 하는 DFS(분산 파일 시스템) 복제를 설정할 때 명령줄 도구 **Robocopy.exe**를 사용하여 파일을 미리 시드하는 방법을 설명합니다. DFS 복제를 설정하기 전에 파일을 미리 시드하여 새 복제 파트너를 추가하거나 서버를 교체하면 초기 동기화 속도를 높이고 Windows Server 2012 R2에서 DFS 복제 데이터베이스 복제를 사용하도록 설정할 수 있습니다. Robocopy 메서드는 여러 사전 시드 방법 중 하나입니다. 개요는 [1단계: DFS 복제용 파일 미리 시드](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn495046(v%3dws.11)>)를 참조하세요.

Robocopy(강력한 파일 복사) 명령줄 유틸리티는 Windows Server에 포함되어 있습니다. 이 유틸리티는 복사 보안, 백업 API 지원, 다시 시도 기능 및 로깅을 비롯한 광범위한 옵션을 제공합니다. 이후 버전에는 다중 스레딩 및 버퍼링되지 않은 I/O 지원이 포함됩니다.

>[!IMPORTANT]
>Robocopy는 배타적으로 잠긴 파일을 복사하지 않습니다. 사용자가 파일 서버에서 여러 파일을 장기간 잠그는 경향이 있는 경우 다른 사전 시드 방법을 고려해야 합니다. 원본 서버와 대상 서버의 파일 목록이 완벽하게 일치하지 않아도 미리 시드를 사용할 수 있지만, DFS 복제를 위해 초기 동기화를 수행할 때 존재하지 않는 파일이 많을수록 미리 시드의 효율성이 떨어집니다. 잠금 충돌을 최소화하려면 조직의 사용량이 많지 않은 시간에 Robocopy를 사용하세요. 미리 시드 후에는 항상 Robocopy 로그를 검사하여 배타적 잠금으로 인해 건너뛴 파일을 파악해야 합니다.

Rbocopy를 사용하여 DFS 복제용 파일 미리 시드하려면 다음 단계를 수행합니다.

1. [최신 버전의 Robocopy를 다운로드하여 설치](#step-1-download-and-install-the-latest-version-of-robocopy)
2. [복제할 파일 안정화](#step-2-stabilize-files-that-will-be-replicated)
3. [복제된 파일을 대상 서버에 복사](#step-3-copy-the-replicated-files-to-the-destination-server)

## <a name="prerequisites"></a>필수 구성 요소

미리 시드는 DFS 복제와 직접적인 관련이 없으므로 Robocopy를 사용하여 파일을 복사하기 위한 요구 사항만 충족하면 됩니다.

- 원본 서버와 대상 서버에서 로컬 관리자 그룹의 구성원인 사용자 계정이 필요합니다.

- 파일 복사에 사용할 서버(원본 서버 또는 대상 서버)에 최신 버전의 Robocopy를 설치합니다. 운영 체제 버전에 맞는 최신 버전을 설치해야 합니다. 자세한 지침은 [2단계: 복제할 파일 안정화](#step-2-stabilize-files-that-will-be-replicated)를 참조하세요. Windows Server 2003 R2를 실행하는 서버의 파일을 미리 시드하지 않는 한, 원본 또는 대상 서버에서 Robocopy를 실행할 수 있습니다. 일반적으로 좀 더 최신 운영 체제 버전을 실행하는 대상 서버에서는 최신 버전의 Robocopy에 액세스할 수 있습니다.

- 대상 드라이브에 사용할 수 있는 스토리지 공간이 충분한지 확인하세요. 복사할 경로에 폴더를 만들지 마세요. Robocopy가 루트 폴더를 만들어야 합니다.
    
    >[!NOTE]
    >미리 시드된 파일에 할당할 공간의 크기를 결정할 때, 향후 예상되는 데이터 증가 속도와 DFS 복제에 필요한 스토리지 요구 사항을 고려해야 합니다. 계획에 대한 도움말은 [DFS 복제 관리](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754771(v=ws.11)>)의 [준비 폴더와 충돌 및 삭제된 항목 폴더의 할당량 크기 편집](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754229(v=ws.11))을 참조하세요.

- 원본 서버에서, 필요하다면 파일을 잠그는 애플리케이션을 확인하는 데 사용할 수 있는 프로세스 모니터 또는 프로세스 탐색기를 설치합니다. 다운로드 정보는 [프로세스 모니터](https://docs.microsoft.com/sysinternals/downloads/procmon) 및 [프로세스 탐색기](https://docs.microsoft.com/sysinternals/downloads/process-explorer)를 참조하세요.

## <a name="step-1-download-and-install-the-latest-version-of-robocopy"></a>1단계: 최신 버전의 Robocopy를 다운로드하여 설치

Robocopy를 사용하여 파일을 미리 시드할 것이므로, 최신 버전의 **Robocopy**를 다운로드하여 설치해야 합니다. 이렇게 하면 Robocopy의 배송 버전에 포함된 이슈 때문에 DFS 복제에서 파일을 건너뛰지 않습니다.

호환되는 최신 Robocopy 버전의 소스는 서버에서 실행 중인 Windows Server 버전에 따라 다릅니다. Windows Server 2008 R2 또는 Windows Server 2008용 Robocopy의 최신 버전을 사용하여 핫픽스를 다운로드하는 방법에 대한 자세한 내용은 [현재 Windows Server 2008 및 Windows Server 2008 R2에서 DFS(분산 파일 시스템) 기술에 사용 가능한 핫픽스 목록](https://support.microsoft.com/help/968429/list-of-currently-available-hotfixes-for-distributed-file-system-dfs-t)을 참조하세요.

또는 다음 단계를 수행하여 운영 체제에 맞는 최신 핫픽스를 찾아 설치할 수 있습니다.

### <a name="locate-and-install-the-latest-version-of-robocopy-for-a-specific-version-of-windows-server"></a>특정 버전의 Windows Server에 맞는 최신 버전의 Robocopy를 찾아 설치

1. 웹 브라우저에서 [https://support.microsoft.com](https://support.microsoft.com/)을 엽니다.

2. **지원 검색**에 다음 문자열을 입력하고, `<operating system version>`을 적절한 운영 체제로 바꾼 다음, Enter 키를 누릅니다.
    
    ```robocopy.exe kbqfe "<operating system version>"```
    
    예를 들어 **robocopy.exe kbqfe "Windows Server 2008 R2"** 를 입력합니다.

3. ID 번호가 가장 높은(즉, 최신 버전) 핫픽스를 찾아 다운로드합니다.

4. 서버에 핫픽스를 설치합니다.

## <a name="step-2-stabilize-files-that-will-be-replicated"></a>2단계: 복제할 파일 안정화

서버에 최신 버전의 Robocopy를 설치한 후에는 다음 표에 설명된 방법을 사용하여 잠긴 파일이 복사를 차단하지 않도록 해야 합니다. 대부분의 애플리케이션은 파일을 배타적으로 잠그지 않습니다. 그러나 정상 작업 중에 파일 서버에서 소수의 파일이 잠길 수 있습니다.

|잠금의 원인|설명|완화 방법|
|---|---|---|
|사용자가 공유의 파일을 원격으로 엽니다.|직원이 표준 파일 서버에 연결하여 문서, 멀티미디어 콘텐츠 또는 기타 파일을 편집합니다. 전통적인 홈 폴더 또는 공유 데이터 워크로드라고도 합니다.|사용량이 많지 않은 업무 외 시간에만 Robocopy 작업을 수행합니다. 이렇게 하면 미리 시드 중에 Robocopy에서 건너뛰어야 하는 파일 수를 최소화할 수 있습니다.<br><br>Windows PowerShell **Grant-SmbShareAccess** 및 **Close-SmbSession**을 사용하여 복제될 파일 공유에 대한 읽기 전용 액세스를 일시적으로 설정하는 방안을 고려해 봅니다. [모두] 또는 [인증된 사용자] 같은 공용 그룹에 읽기 권한을 설정하면 표준 사용자가 배타적 잠금을 사용하여 파일을 열 가능성을 낮출 수 있습니다(파일이 열릴 때 애플리케이션에서 읽기 전용 액세스를 탐지하는 경우).<br><br>해당 서버의 인바운드 SMB 포트 445에 대한 임시 방화벽 규칙을 설정하거나 **Block-SmbShareAccess** cmdlet을 사용하는 방법을 생각해 볼 수도 있습니다. 그러나 이러한 방법은 사용자 작업에 큰 방해가 됩니다.|
|애플리케이션이 파일을 로컬로 엽니다.|파일 서버에서 실행되는 애플리케이션 워크로드가 가끔 파일을 잠급니다.|파일을 잠그는 애플리케이션을 일시적으로 사용하지 않도록 설정하거나 제거합니다. 프로세스 모니터 또는 프로세스 탐색기를 사용하여 파일을 잠그는 애플리케이션을 확인할 수 있습니다. 프로세스 모니터 또는 프로세스 탐색기를 다운로드하려면 [프로세스 모니터](https://docs.microsoft.com/sysinternals/downloads/procmon) 및 [프로세스 탐색기](https://docs.microsoft.com/sysinternals/downloads/process-explorer) 페이지를 방문하세요.|

## <a name="step-3-copy-the-replicated-files-to-the-destination-server"></a>3단계: 복제된 파일을 대상 서버에 복사

복제할 파일의 잠금을 최소화한 후에는 원본 서버에서 대상 서버로 파일을 미리 시드할 수 있습니다.

>[!NOTE]
>원본 컴퓨터 또는 대상 컴퓨터에서 Robocopy를 실행할 수 있습니다. 다음 절차에서는 일반적으로 좀 더 최신 운영 체제를 실행하는 대상 서버에서 Robocopy를 실행하여 최신 운영 체제에서 제공하는 추가 Robocopy 기능을 활용하는 방법을 설명합니다.

### <a name="preseed-the-replicated-files-onto-the-destination-server-with-robocopy"></a>Robocopy를 사용하여 복제된 파일을 대상 서버에 미리 시드

1. 원본 서버와 대상 서버 모두에서 로컬 관리자 그룹의 구성원인 계정으로 대상 서버에 로그인합니다.

2. 관리자 권한 명령 프롬프트를 엽니다.

3. 원본 서버에서 대상 서버로 파일을 미리 시드하려면 다음 명령을 실행하고, 대괄호 안의 값을 해당하는 원본, 대상 및 로그 파일 경로로 바꿉니다.
    
    ```PowerShell
    robocopy "<source replicated folder path>" "<destination replicated folder path>" /e /b /copyall /r:6 /w:5 /MT:64 /xd DfsrPrivate /tee /log:<log file path> /v
    ```
    
    이 명령은 다음 매개 변수를 사용하여 원본 폴더의 모든 내용을 대상 폴더에 복사합니다.
    
    |매개 변수|설명|
    |---|---|
    |"\<source replicated folder path\>"|대상 서버에서 미리 시드할 원본 폴더를 지정합니다.|
    |"\<destination replicated folder path\>"|미리 시드된 파일을 저장할 폴더 경로를 지정합니다.<br><br>대상 폴더가 아직 대상 서버에 없어야 합니다. 일치하는 파일 해시를 가져오려면 Robocopy가 파일을 미리 시드할 때 루트 폴더를 만들어야 합니다.|
    |/e|하위 디렉터리와 해당 파일, 그리고 빈 하위 디렉터리를 복사합니다.|
    |/b|백업 모드에서 파일을 복사 합니다.|
    |/copyall|데이터, 특성, 타임스탬프, NTFS ACL(액세스 제어 목록), 소유자 정보 및 감사 정보를 비롯한 모든 파일 정보를 복사합니다.|
    |/r:6|오류가 발생하는 경우 작업을 6회 다시 시도합니다.|
    |/w:5|다시 시도 사이에 5초 동안 기다립니다.|
    |MT:64|64개 파일을 동시에 복사합니다.|
    |/xd DfsrPrivate|DfsrPrivate 폴더를 제외합니다.|
    |/tee|로그 파일뿐 아니라 콘솔 창에도 상태 출력을 씁니다.|
    |/log \<log file path>|기록할 로그 파일을 지정합니다. 파일의 기존 콘텐츠를 덮어씁니다. (기존 로그 파일에 항목을 추가하려면 `/log+ <log file path>`를 사용합니다.)|
    |/v|건너뛴 파일을 포함하는 자세한 정보 출력을 생성합니다.|
    
    예를 들어 다음 명령은 복제된 원본 폴더 E:\\RF01의 파일을 대상 서버의 데이터 드라이브 D에 복제합니다.
    
    ```PowerShell
    robocopy.exe "\\srv01\e$\rf01" "d:\rf01" /e /b /copyall /r:6 /w:5 /MT:64 /xd DfsrPrivate /tee /log:c:\temp\preseedsrv02.log
    ```
    
    >[!NOTE]
    >Robocopy를 사용하여 DFS 복제용 파일을 미리 시드하는 경우에는 위에 설명된 매개 변수를 사용하는 것이 좋습니다. 그러나 일부 값을 변경하거나 매개 변수를 더 추가할 수 있습니다. 예를 들어 */MT* 매개 변수의 값(스레드 수)을 더 높게 설정할 수 있는 용량이 있는지 테스트를 통해 확인할 수 있습니다. 또한 주로 큰 파일을 복제하는 경우 버퍼링되지 않은 I/O에 대한 **/j** 옵션을 추가하여 복사 성능을 높일 수 있습니다. Robocopy 매개 변수에 대한 자세한 내용은 [Robocopy](https://docs.microsoft.com/windows-server/administration/windows-commands/robocopy) 명령줄 참조에서 확인할 수 있습니다.

    >[!WARNING]
    >Robocopy를 사용하여 DFS 복제용 파일을 미리 시드할 때 데이터 손실을 방지하려면 권장 매개 변수를 다음과 같이 변경하지 마세요.
    >- 디렉터리 트리를 미러링하는 */mir* 매개 변수 또는 파일을 옮긴 후 원본에서 제거하는 */mov* 매개 변수를 사용하지 마세요.
    >-  **/e**, **/b** 및 **/copyall** 옵션을 제거하지 마세요.

4. 복사가 완료되면 로그를 검사하여 오류 또는 건너뛴 파일을 확인합니다. 전체 파일 세트를 다시 복사하는 대신, Robocopy를 사용하여 건너뛴 파일을 개별적으로 복사합니다. 배타적 잠금 때문에 파일을 건너뛴 경우 나중에 Robocopy를 사용하여 파일을 개별적으로 복사하거나, 초기 동기화 중에 DFS 복제를 통해 이러한 파일을 유선으로 복제할 것을 수락합니다.

## <a name="next-step"></a>다음 단계

초기 복사를 완료하고 Robocopy를 사용하여 건너뛴 파일 이슈를 최대한 해결한 후에는 Windows PowerShell의 **Get-DfsrFileHash** cmdlet 또는 **Dfsrdiag** 명령으로 원본 및 대상 서버의 파일 해시를 비교하여 미리 시드된 파일의 유효성을 검사합니다. 자세한 지침은 [2단계: DFS 복제용으로 미리 시드한 파일의 유효성 검사](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn495042(v%3dws.11)>)를 참조하세요.
