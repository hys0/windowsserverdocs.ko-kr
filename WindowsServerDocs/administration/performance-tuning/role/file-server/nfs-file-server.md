---
title: NFS 파일 서버 성능 조정
description: NFS 파일 서버 성능 조정
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
author: phstee
ms.author: RoopeshB, NedPyle
ms.date: 10/16/2017
ms.openlocfilehash: 06a2a7206d3673046bd5a926a657bac91b02bf5f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59879014"
---
# <a name="performance-tuning-nfs-file-servers"></a>NFS 파일 서버를 튜닝 하는 성능

## <a href="" id="servicesnfs"></a>NFS 모델에 대 한 서비스


다음 섹션에서는 클라이언트-서버 통신에 대 한 네트워크 파일 시스템 (NFS) 모델에 대 한 Microsoft 서비스에 대 한 정보를 제공합니다. NFS v2 및 NFS v3를 여전히 가장 광범위 하 게 프로토콜의 버전을 배포 하므로 MaxConcurrentConnectionsPerIp 제외 하 고 레지스트리 키의 모든 NFS v2 및 NFS v3에만 적용 됩니다.

없는 레지스트리 튜닝 하는 것이 NFS v4.1 프로토콜에 대 한 필요 합니다.

### <a name="service-for-nfs-model-overview"></a>서비스에 대 한 NFS 모델 개요

NFS 용 Microsoft Services 혼합된 된 Windows 및 UNIX 환경에 있는 기업의 파일 공유 솔루션을 제공 합니다. 이 통신 모델은 서버 및 클라이언트 컴퓨터의 구성 됩니다. 클라이언트에서 응용 프로그램 (Rdbss.sys) 리디렉터 및 NFS 미니 리디렉터 (Nfsrdr.sys)를 통해 서버에 있는 파일을 요청 합니다. 소형 리디렉터의 TCP/IP 통해 해당 요청을 보내도록 NFS 프로토콜을 사용 합니다. 서버는 TCP/IP 통해 클라이언트에서 여러 요청을 받고 저장소 스택의 액세스 하는 로컬 파일 시스템 (Ntfs.sys)에 요청을 라우팅합니다.

다음 그림에는 NFS 용 통신 모델을 보여 줍니다.

![nfs 통신 모델](../../media/perftune-guide-nfs-model.png)

### <a name="tuning-parameters-for-nfs-file-servers"></a>NFS 파일 서버에 대 한 매개 변수를 튜닝합니다.

다음 레지스트리\_DWORD 레지스트리 설정을 NFS 파일 서버의 성능에 영향을 줄 수 있습니다.

-   **OptimalReads**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\OptimalReads
    ```

    기본값은 0입니다. 이 매개 변수 파일에 대 한 파일을 열지 여부 결정\_RANDOM\_액세스 또는 파일에 대 한\_순차\_I/O 워크 로드 특성에 따라 전용입니다. 이 값을 1로 설정 파일을 파일에 대 한 열 수를 강제로\_RANDOM\_액세스 합니다. 파일\_RANDOM\_프리페치에서 파일 시스템 및 캐시 관리자 수 없습니다.

    >[!NOTE]
    > 이 설정은 증가 시스템 파일 캐시에서 잠재적 영향을 있을 수 있으므로 신중 하 게 평가 되어야 합니다.


-   **RdWrHandleLifeTime**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\RdWrHandleLifeTime
    ```

    기본값은 5입니다. 이 매개 변수 파일 핸들이 캐시에 있는 NFS 캐시 항목의 수명을 제어합니다. 매개 변수 처리 연결 된 열려 있는 NTFS 파일에 있는 캐시 항목을 가리킵니다. 실제 수명 RdWrThreadSleepTime 곱한 RdWrHandleLifeTime 거의 같습니다. 최소값은 1이 고 최대값은 60입니다.

-   **RdWrNfsHandleLifeTime**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\RdWrNfsHandleLifeTime
    ```

    기본값은 5입니다. 이 매개 변수 파일 핸들이 캐시에 있는 NFS 캐시 항목의 수명을 제어합니다. 매개 변수에 연결 된 열려 있는 NTFS 파일 처리 되지 않은 캐시 엔트리를 가리킵니다. NFS 용 서비스는 파일 시스템을 사용 하 여 열린 핸들을 유지 하지 않고 파일의 파일 특성을 저장 하려면 이러한 캐시 항목을 사용 합니다. 실제 수명 RdWrThreadSleepTime 곱한 RdWrNfsHandleLifeTime 거의 같습니다. 최소값은 1이 고 최대값은 60입니다.

-   **RdWrNfsReadHandlesLifeTime**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\RdWrNfsReadHandlesLifeTime
    ```

    기본값은 5입니다. 이 매개 변수 파일 핸들이 캐시에서 캐시 항목을 읽을 NFS의 수명을 제어 합니다. 실제 수명 RdWrThreadSleepTime 곱한 RdWrNfsReadHandlesLifeTime 거의 같습니다. 최소값은 1이 고 최대값은 60입니다.

-   **RdWrThreadSleepTime**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\RdWrThreadSleepTime
    ```

    기본값은 5입니다. 이 매개 변수는 파일 핸들 캐시에서 정리 스레드를 실행 하기 전에 대기 간격을 제어 합니다. 틱 값 이며 명확 하지 않습니다. 틱은 약 100 나노초에 해당 합니다. 최소값은 1이 고 최대값은 60입니다.

-   **FileHandleCacheSizeinMB**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\FileHandleCacheSizeinMB
    ```

    기본값은 4입니다. 이 매개 변수는 파일 핸들 캐시 항목에서 사용할 최대 메모리를 지정 합니다. 최소값은 1이 고 최대값은 1\*1024\*1024\*1024 (1073741824).

-   **LockFileHandleCacheInMemory**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\LockFileHandleCacheInMemory
    ```

    기본값은 0입니다. 이 매개 변수는 FileHandleCacheSizeInMB 하 여 지정 된 캐시 크기에 할당 되는 물리적 페이지 메모리에서 잠겨 있는지 여부를 지정 합니다. 이 작업을 사용 하면이 값을 1로 설정 합니다. 페이지는 메모리에서 잠긴 (없습니다 디스크에 페이징), 파일 핸들을 확인 하는 성능을 개선 하지만 응용 프로그램에 사용할 수 있는 메모리의 양이 줄어듭니다.

-   **MaxIcbNfsReadHandlesCacheSize**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\MaxIcbNfsReadHandlesCacheSize
    ```

    기본값은 64입니다. 이 매개 변수는 읽기 데이터 캐시에 대 한 볼륨당 핸들의 최대 수를 지정합니다. 1GB 이상의 메모리에 있는 시스템 에서만 읽기 캐시 항목이 만들어집니다. 최소값은 0이 고 최대값은 0xFFFFFFFF입니다.

-   **HandleSigningEnabled**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\HandleSigningEnabled
    ```

    기본값은 1입니다. 이 매개 변수를 NFS 파일 서버에 의해 지정 된 핸들은 암호화 된 서명 되었는지 여부를 제어 합니다. 0으로 설정 하면 핸들 서명 사용 하지 않도록 설정 합니다.

-   **RdWrNfsDeferredWritesFlushDelay**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\RdWrNfsDeferredWritesFlushDelay
    ```

    기본값은 60입니다. 이 매개 변수는 NFS V3 불안정 쓰기 데이터 캐싱 기간을 제어 하는 소프트 제한입니다. 최소값은 1이 고 최대값은 600입니다. 실제 수명 RdWrThreadSleepTime 곱한 RdWrNfsDeferredWritesFlushDelay 거의 같습니다.

-   **CacheAddFromCreateAndMkDir**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\CacheAddFromCreateAndMkDir
    ```

    기본값은 1 (사용). 이 매개 변수는 NFS V2 및 V3 만들고 MKDIR RPC 프로시저 처리기 파일에 유지 되는 동안 열려 있는 핸들이 캐시를 처리 하는지 여부를 제어 합니다. 이 값을 캐시 만들기 및 MKDIR 코드 경로에 추가 항목을 사용 하지 않도록 설정 하려면 0을 설정 합니다.

-   **AdditionalDelayedWorkerThreads**

    ```
    HKLM\SYSTEM\CurrentControlSet\Control\SessionManager\Executive\AdditionalDelayedWorkerThreads
    ```

    지정 된 작업을 큐에 대해 생성 된 지연 된 작업자 스레드 수를 늘립니다. 시간이 중요 한 고려 되지 않습니다 하 고 작업 항목을 기다리는 동안는 페이징할 메모리 스택을 해당를 가질 수 있는 작업자 스레드 프로세스 작업 항목을 지연 합니다. 스레드 수가 부족 줄어듭니다 속도 직장 항목 처리 됩니다. 너무 큰 값 시스템 리소스를 불필요 하 게 사용 합니다.

-   **NtfsDisable8dot3NameCreation**

    ```
    HKLM\System\CurrentControlSet\Control\FileSystem\NtfsDisable8dot3NameCreation
    ```

    Windows Server 2012 및 Windows Server 2012 R2의 기본값은 2입니다. Windows Server 2012 이전 버전에서 기본값은 0입니다. 이 매개 변수는 NTFS에는 8.3 형식이 짧은 이름을 생성 하는지 여부를 결정 하 고 확장 된 문자 집합의 문자를 포함 하는 파일 이름에 대 한 긴 파일 이름에 대 한 명명 규칙 (MSDOS). 이 항목의 값이 0 인 경우 파일 이름을 두의 수: 사용자 지정 하는 이름 및 NTFS를 생성 하는 약식 이름입니다. 사용자 지정 이름을 8.3 형식이 명명 규칙을 따르므로, NTFS 짧은 이름을 생성 하지 않습니다. 값이 2 이면 볼륨당이 매개 변수를 구성할 수 있습니다.

    >[!NOTE]
    > 시스템 볼륨에 8.3 형식이 기본적으로 사용할 수 있습니다. Windows Server 2012 및 Windows Server 2012 R2의 다른 모든 볼륨 8.3 형식이 기본적으로 사용 하지 않도록 설정 했습니다. 이 값을 변경 하는 파일의 내용을 변경 되지 않지만 NTFS 표시 하 고 파일을 관리 하는 방법을 변경 하는 파일에 대 한 약식 이름 특성 생성을 방지 하기. 대부분의 파일 서버에 대 한 권장된 설정은 1 (해제)입니다.


-   **NtfsDisableLastAccessUpdate**

    ```
    HKLM\System\CurrentControlSet\Control\FileSystem\NtfsDisableLastAccessUpdate
    ```

    기본값은 1입니다. 이 시스템 전역 스위치 마지막 파일 또는 디렉터리 액세스에 대 한 날짜 및 시간 스탬프의 업데이트를 사용 하지 않도록 설정 하 여 대기 시간 및 디스크 I/O 부하를 줄입니다.

-   **MaxConcurrentConnectionsPerIp**

    ```
    HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\Rpcxdr\Parameters\MaxConcurrentConnectionsPerIp
    ```

    MaxConcurrentConnectionsPerIp 매개 변수의 기본값은 16입니다. IP 주소당 연결 수를 늘리려면 8192 최대이 값을 늘릴 수 있습니다.
