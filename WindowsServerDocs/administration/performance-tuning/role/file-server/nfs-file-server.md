---
title: NFS 파일 서버 성능 조정
description: NFS 파일 서버 성능 조정
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: article
author: phstee
ms.author: RoopeshB, NedPyle
ms.date: 10/16/2017
ms.openlocfilehash: 07e5005c1bc38e791e847c8965cbc9a6c0ac96f4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71355176"
---
# <a name="performance-tuning-nfs-file-servers"></a>NFS 파일 서버 성능 조정

## <a href="" id="servicesnfs"></a>NFS 용 서비스 모델


다음 섹션에서는 클라이언트 서버 통신용 Microsoft 서비스 NFS (네트워크 파일 시스템) 모델에 대 한 정보를 제공 합니다. NFS v2 및 NFS v3은 여전히 가장 널리 배포 되는 프로토콜 버전 이므로 MaxConcurrentConnectionsPerIp를 제외한 모든 레지스트리 키는 NFS v2 및 NFS v3에만 적용 됩니다.

NFS v 4.1 프로토콜에는 레지스트리 조정이 필요 하지 않습니다.

### <a name="service-for-nfs-model-overview"></a>NFS 용 서비스 모델 개요

NFS 용 Microsoft 서비스는 혼합 된 Windows 및 UNIX 환경을 포함 하는 기업에 대 한 파일 공유 솔루션을 제공 합니다. 이 통신 모델은 클라이언트 컴퓨터와 서버로 구성 됩니다. 리디렉터 (Rdbss) 및 NFS 미니 리디렉터 (Nfsrdr .sys)를 통해 서버에 있는 클라이언트 요청 파일의 응용 프로그램입니다. 미니 리디렉터는 NFS 프로토콜을 사용 하 여 TCP/IP를 통해 요청을 보냅니다. 서버는 TCP/IP를 통해 클라이언트로부터 여러 요청을 수신 하 고 해당 요청을 로컬 파일 시스템 (http.sys)로 라우팅합니다 .이는 저장소 스택에 액세스 합니다.

다음 그림은 NFS에 대 한 통신 모델을 보여 줍니다.

![nfs 통신 모델](../../media/perftune-guide-nfs-model.png)

### <a name="tuning-parameters-for-nfs-file-servers"></a>NFS 파일 서버에 대 한 튜닝 매개 변수

다음 REG\_DWORD 레지스트리 설정은 NFS 파일 서버의 성능에 영향을 줄 수 있습니다.

-   **OptimalReads**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\OptimalReads
    ```

    기본값은 0입니다. 이 매개 변수는 작업 i/o 특성에 따라 파일\_임의\_액세스를 위한 파일을 열지, 아니면 파일\_순차적\_만 열지를 결정 합니다. 파일\_임의\_액세스에 대해 파일을 열도록 하려면이 값을 1로 설정 합니다. 파일\_임의\_액세스를 사용 하면 파일 시스템 및 캐시 관리자가 프리페치 되지 않습니다.

    >[!NOTE]
    > 이 설정은 시스템 파일 캐시 증가에 잠재적 영향을 줄 수 있으므로 신중 하 게 평가 해야 합니다.


-   **RdWrHandleLifeTime**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\RdWrHandleLifeTime
    ```

    기본값은 5입니다. 이 매개 변수는 파일 핸들 캐시에서 NFS 캐시 항목의 수명을 제어 합니다. 매개 변수는 연결 된 열린 NTFS 파일 핸들이 있는 캐시 항목을 참조 합니다. 실제 수명은 RdWrHandleLifeTime에 RdWrThreadSleepTime를 곱한 값과 거의 같습니다. 최소값은 1이 고 최대값은 60입니다.

-   **RdWrNfsHandleLifeTime**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\RdWrNfsHandleLifeTime
    ```

    기본값은 5입니다. 이 매개 변수는 파일 핸들 캐시에서 NFS 캐시 항목의 수명을 제어 합니다. 매개 변수가 연결 된 열린 NTFS 파일 핸들이 없는 캐시 항목을 참조 하는 경우 NFS 용 서비스는 파일 시스템을 사용 하 여 열린 핸들을 유지 하지 않고 파일의 파일 특성을 저장 하는 데 이러한 캐시 항목을 사용 합니다. 실제 수명은 RdWrNfsHandleLifeTime에 RdWrThreadSleepTime를 곱한 값과 거의 같습니다. 최소값은 1이 고 최대값은 60입니다.

-   **RdWrNfsReadHandlesLifeTime**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\RdWrNfsReadHandlesLifeTime
    ```

    기본값은 5입니다. 이 매개 변수는 파일 핸들 캐시에서 NFS 읽기 캐시 항목의 수명을 제어 합니다. 실제 수명은 RdWrNfsReadHandlesLifeTime에 RdWrThreadSleepTime를 곱한 값과 거의 같습니다. 최소값은 1이 고 최대값은 60입니다.

-   **RdWrThreadSleepTime**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\RdWrThreadSleepTime
    ```

    기본값은 5입니다. 이 매개 변수는 파일 핸들 캐시에서 정리 스레드를 실행 하기 전의 대기 간격을 제어 합니다. 값은 틱 이며 비결 정적입니다. 틱은 약 100 나노초와 동일 합니다. 최소값은 1이 고 최대값은 60입니다.

-   **FileHandleCacheSizeinMB**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\FileHandleCacheSizeinMB
    ```

    기본값은 4입니다. 이 매개 변수는 파일 핸들 캐시 항목에서 사용 되는 최대 메모리를 지정 합니다. 최소값은 1이 고 최대값은 1\*1024\*1024\*1024 (1073741824)입니다.

-   **LockFileHandleCacheInMemory**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\LockFileHandleCacheInMemory
    ```

    기본값은 0입니다. 이 매개 변수는 FileHandleCacheSizeInMB로 지정 된 캐시 크기에 할당 된 물리적 페이지가 메모리에 잠겨 있는지 여부를 지정 합니다. 이 값을 1로 설정 하면이 작업을 수행할 수 있습니다. 페이지는 메모리에서 잠겨 있으므로 (디스크에 페이징 되지 않음) 파일 핸들을 확인 하는 성능을 향상 시키지만 응용 프로그램에 사용할 수 있는 메모리를 줄입니다.

-   **MaxIcbNfsReadHandlesCacheSize**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\MaxIcbNfsReadHandlesCacheSize
    ```

    기본값은 64입니다. 이 매개 변수는 읽기 데이터 캐시에 대 한 볼륨당 최대 핸들 수를 지정 합니다. 읽기 캐시 항목은 메모리가 1gb를 초과 하는 시스템 에서만 생성 됩니다. 최소값은 0이 고 최대값은 0xFFFFFFFF입니다.

-   **HandleSigningEnabled**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\HandleSigningEnabled
    ```

    기본값은 1입니다. 이 매개 변수는 NFS 파일 서버에서 제공 하는 핸들이 암호화 된 서명 인지 여부를 제어 합니다. 0으로 설정 하면 핸들 서명이 사용 되지 않습니다.

-   **RdWrNfsDeferredWritesFlushDelay**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\RdWrNfsDeferredWritesFlushDelay
    ```

    기본값은 60입니다. 이 매개 변수는 NFS V3 불안정 한 쓰기 데이터 캐싱의 기간을 제어 하는 소프트 시간 제한입니다. 최소값은 1이 고 최대값은 600입니다. 실제 수명은 RdWrNfsDeferredWritesFlushDelay에 RdWrThreadSleepTime를 곱한 값과 거의 같습니다.

-   **CacheAddFromCreateAndMkDir**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\CacheAddFromCreateAndMkDir
    ```

    기본값은 1 (사용)입니다. 이 매개 변수는 NFS V2 및 V3 CREATE 및 MKDIR RPC 프로시저 처리기 중에 열린 핸들이 파일 핸들 캐시에 보관 되는지 여부를 제어 합니다. CREATE 및 MKDIR 코드 경로에서 캐시에 항목을 추가 하지 않으려면이 값을 0으로 설정 합니다.

-   **Additionaldelayed는 Threads**

    ```
    HKLM\SYSTEM\CurrentControlSet\Control\SessionManager\Executive\AdditionalDelayedWorkerThreads
    ```

    지정 된 작업 큐에 대해 만들어진 지연 된 작업자 스레드 수를 늘립니다. 지연 된 작업자 스레드는 시간이 중요 한 것으로 간주 되지 않으며 작업 항목을 기다리는 동안 메모리 스택을 페이징할 수 있는 작업 항목을 처리 합니다. 스레드 수가 부족 하 여 작업 항목의 처리 속도를 줄일 수 있습니다. 너무 높은 값은 시스템 리소스를 불필요 하 게 소비 합니다.

-   **NtfsDisable8dot3NameCreation**

    ```
    HKLM\System\CurrentControlSet\Control\FileSystem\NtfsDisable8dot3NameCreation
    ```

    Windows Server 2012 및 Windows Server 2012 r 2의 기본값은 2입니다. Windows Server 2012 이전 릴리스의 경우 기본값은 0입니다. 이 매개 변수는 긴 파일 이름 및 확장 문자 집합의 문자를 포함 하는 파일 이름에 대해 8.3 (MSDOS.SYS) 명명 규칙에서 짧은 이름을 생성 하는지 여부를 결정 합니다. 이 항목의 값이 0 인 경우 파일에는 사용자가 지정 하는 이름과 NTFS에서 생성 하는 짧은 이름을 사용할 수 있습니다. 사용자 지정 이름이 8.3 명명 규칙을 따르는 경우에는 NTFS에서 짧은 이름을 생성 하지 않습니다. 값 2는이 매개 변수를 볼륨당 구성할 수 있음을 의미 합니다.

    >[!NOTE]
    > 시스템 볼륨에는 기본적으로 8.3이 사용 됩니다. Windows Server 2012 및 Windows Server 2012 r 2의 다른 모든 볼륨은 기본적으로 8.3을 사용 하지 않도록 설정 되어 있습니다. 이 값을 변경 해도 파일의 내용이 변경 되지는 않지만 파일의 짧은 이름 특성 생성을 피할 수 있습니다 .이 경우 NTFS에서 파일을 표시 하 고 관리 하는 방법도 변경 됩니다. 대부분의 파일 서버에 대해 권장 되는 설정은 1 (사용 안 함)입니다.


-   **NtfsDisableLastAccessUpdate**

    ```
    HKLM\System\CurrentControlSet\Control\FileSystem\NtfsDisableLastAccessUpdate
    ```

    기본값은 1입니다. 이 시스템 전역 스위치는 마지막 파일 또는 디렉터리 액세스에 대 한 날짜 및 시간 스탬프 업데이트를 사용 하지 않도록 설정 하 여 디스크 i/o 로드 및 대기 시간을 줄입니다.

-   **MaxConcurrentConnectionsPerIp**

    ```
    HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\Rpcxdr\Parameters\MaxConcurrentConnectionsPerIp
    ```

    MaxConcurrentConnectionsPerIp 매개 변수의 기본값은 16입니다. 이 값을 최대 8192까지 늘려 IP 주소 당 연결 수를 늘릴 수 있습니다.
