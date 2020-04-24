---
title: 파일 서버의 성능 조정
description: Windows Server를 실행하는 파일 서버의 성능 튜닝
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: article
author: phstee
ms.author: nedpyle; danlo; dkruse; v-tea
ms.date: 12/12/2019
manager: dcscontentpm
audience: Admin
ms.openlocfilehash: 1236b961f77fe46f19b70a2c48d32f05585bd29c
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2020
ms.locfileid: "80851846"
---
# <a name="performance-tuning-for-file-servers"></a>파일 서버의 성능 조정

평균 부하, 최대 부하, 용량, 확장 계획 및 응답 시간을 고려하여 예상 파일 서버 부하를 충족하는 적절한 하드웨어를 선택해야 합니다. 하드웨어 병목 현상은 소프트웨어 튜닝의 효과를 제한합니다.

## <a name="general-tuning-parameters-for-clients"></a>클라이언트의 일반 튜닝 매개 변수

다음 REG\_DWORD 레지스트리 설정은 SMB 파일 서버와 상호 작용하는 클라이언트 컴퓨터의 성능에 영향을 줄 수 있습니다.

-   **ConnectionCountPerNetworkInterface**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\ConnectionCountPerNetworkInterface
    ```

    적용 대상: Windows 10, Windows 8.1, Windows 8, Windows Server 2016, Windows Server 2012 R2 및 Windows Server 2012

    기본값은 1이며, 기본값을 사용할 것을 강력하게 권장합니다. 유효 범위는 1-16입니다. 비 RSS 인터페이스용 서버에 대해 설정되는 인터페이스당 최대 연결 수입니다.


-   **ConnectionCountPerRssNetworkInterface**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\ConnectionCountPerRssNetworkInterface
    ```

    적용 대상: Windows 10, Windows 8.1, Windows 8, Windows Server 2016, Windows Server 2012 R2 및 Windows Server 2012

    기본값은 4이며, 기본값을 사용할 것을 강력하게 권장합니다. 유효 범위는 1-16입니다. RSS 인터페이스용 서버에 대해 설정되는 인터페이스당 최대 연결 수입니다.

-   **ConnectionCountPerRdmaNetworkInterface**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\ConnectionCountPerRdmaNetworkInterface
    ```

    적용 대상: Windows 10, Windows 8.1, Windows 8, Windows Server 2016, Windows Server 2012 R2 및 Windows Server 2012

    기본값은 2이며, 기본값을 사용할 것을 강력하게 권장합니다. 유효 범위는 1-16입니다. RDMA 인터페이스용 서버에 대해 설정되는 인터페이스당 최대 연결 수입니다.

-   **MaximumConnectionCountPerServer**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\MaximumConnectionCountPerServer
    ```

    적용 대상: Windows 10, Windows 8.1, Windows 8, Windows Server 2016, Windows Server 2012 R2 및 Windows Server 2012

    기본값은 32이며, 유효 범위는 1-64입니다. 모든 인터페이스에서 Windows Server 2012를 실행하는 단일 서버에 대해 설정되는 최대 연결 수입니다.

-   **DormantDirectoryTimeout**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\DormantDirectoryTimeout
    ```

    적용 대상: Windows 10, Windows 8.1, Windows 8, Windows Server 2016, Windows Server 2012 R2 및 Windows Server 2012

    기본값은 600초입니다. 디렉터리 임대를 통해 서버 디렉터리 핸들이 열려 있는 최대 시간입니다.

-   **FileInfoCacheLifetime**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\FileInfoCacheLifetime
    ```

    적용 대상: Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Vista, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 및 Windows Server 2008

    기본값은 10초입니다. 파일 정보 캐시 시간 제한입니다.

-   **DirectoryCacheLifetime**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\DirectoryCacheLifetime
    ```

    적용 대상: Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Vista, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 및 Windows Server 2008

    기본값은 10초입니다. 디렉터리 캐시 시간 제한입니다.

    > [!NOTE]  
    > 이 매개 변수는 디렉터리 임대가 없을 때 디렉터리 메타데이터의 캐싱을 제어합니다.
     
     > [!NOTE]  
     > Windows 10, 버전 1803의 알려진 문제는 Windows 10의 대량의 디렉터리를 캐시하는 기능에 영향을 줍니다. 컴퓨터를 Windows 10, 버전 1803으로 업그레이드한 후, 수천 개의 파일과 폴더가 포함된 네트워크 공유에 액세스하여 해당 공유에 있는 문서를 엽니다. 이들 두 작업을 수행하는 동안 상당한 지연이 발생합니다.
     >  
     > 이 문제를 해결하려면 Windows 10, 버전 1809 이상을 설치합니다.
     >  
     > 이 문제를 해결하려면 **DirectoryCacheLifetime**을 **0**으로 설정합니다.
     >  
     > 이 문제는 다음 버전의 Windows 10에 영향을 줍니다.  
     > - Windows 10 Enterprise, 버전 1803
     > - Windows 10 Pro for Workstations, 버전 1803
     > - Windows 10 Pro Education, 버전 1803
     > - Windows 10 Professional, 버전 1803
     > - Windows 10 Education, 버전 1803
     > - Windows 10 Home, 버전 1803
   
-   **DirectoryCacheEntrySizeMax**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\DirectoryCacheEntrySizeMax
    ```

    적용 대상: Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Vista, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 및 Windows Server 2008

    기본값은 64KB입니다. 디렉터리 캐시 항목의 최대 크기입니다.

-   **FileNotFoundCacheLifetime**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\FileNotFoundCacheLifetime
    ```

    적용 대상: Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Vista, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 및 Windows Server 2008

    기본값은 5초입니다. 파일을 찾을 수 없음 캐시 시간 제한입니다.

-   **CacheFileTimeout**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\CacheFileTimeout
    ```

    적용 대상: Windows 8.1, Windows 8, Windows Server 2012, Windows Server 2012 R2 및 Windows 7

    기본값은 10초입니다. 이 설정은 애플리케이션이 파일의 마지막 핸들을 닫은 후 리디렉터가 파일의 캐시 데이터를 유지하는 시간(초)을 제어합니다.

-   **DisableBandwidthThrottling**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\DisableBandwidthThrottling
    ```

    적용 대상: Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Vista, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 및 Windows Server 2008

    기본값은 0입니다. 기본적으로 SMB 리디렉터는 대기 시간이 긴 네트워크 연결의 처리량을 제한하며, 네트워크 관련 시간 제한을 방지할 목적으로 제한하는 경우도 가끔 있습니다. 이 레지스트리 값을 1로 설정하면 제한이 해제되어 대기 시간이 긴 네트워크 연결을 통해 더 높은 파일 전송 처리량을 사용할 수 있습니다.

-   **DisableLargeMtu**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\DisableLargeMtu
    ```

    적용 대상: Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Vista, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 및 Windows Server 2008

    기본값은 Windows 8만 0입니다. Windows 8에서는 SMB 리디렉터가 페이로드를 요청당 1MB씩 전송하며, 이로 인해 파일 전송 속도가 향상될 수 있습니다. 이 레지스트리 값을 1로 설정하면 요청 크기가 64KB로 제한됩니다. 이 설정을 적용하기 전에 설정이 미치게 될 영향을 먼저 평가해야 합니다.

-   **RequireSecuritySignature**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\RequireSecuritySignature
    ```

    적용 대상: Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Vista, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 및 Windows Server 2008

    기본값은 SMB 서명을 사용하지 않도록 설정하는 0입니다. 이 값을 1로 변경하면 SMB 통신에 SMB 서명이 사용되므로 SMB 서명이 해제된 컴퓨터와 SMB 통신이 불가능합니다. SMB 서명은 CPU 비용 및 네트워크 왕복을 늘리지만, 메시지 가로채기 공격을 차단하는 데 도움이 됩니다. SMB 서명이 필요 없는 경우 모든 클라이언트와 서버에서 이 레지스트리 값이 0인지 확인해야 합니다. 
    
    자세한 내용은 [SMB 서명 기본 사항](https://blogs.technet.microsoft.com/josebda/2010/12/01/the-basics-of-smb-signing-covering-both-smb1-and-smb2/)을 참조하세요.

-   **FileInfoCacheEntriesMax**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\FileInfoCacheEntriesMax
    ```

    적용 대상: Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Vista, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 및 Windows Server 2008

    기본값은 64이며, 유효 범위는 1-65536입니다. 이 값은 클라이언트에서 캐시할 수 있는 파일 메타데이터의 양을 결정하는 데 사용됩니다. 이 값을 늘리면 수많은 파일에 액세스할 때 네트워크 트래픽을 줄이고 성능을 높일 수 있습니다.

-   **DirectoryCacheEntriesMax**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\DirectoryCacheEntriesMax
    ```

    적용 대상: Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Vista, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 및 Windows Server 2008

    기본값은 16이며, 유효 범위는 1-4096입니다. 이 값은 클라이언트에서 캐시할 수 있는 디렉터리 정보의 양을 결정하는 데 사용됩니다. 이 값을 늘리면 큰 디렉터리에 액세스할 때 네트워크 트래픽을 줄이고 성능을 높일 수 있습니다.

-   **FileNotFoundCacheEntriesMax**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\FileNotFoundCacheEntriesMax
    ```

    적용 대상: Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Vista, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 및 Windows Server 2008

    기본값은 128이며, 유효 범위는 1-65536입니다. 이 값은 클라이언트에서 캐시할 수 있는 파일 이름 정보의 양을 결정하는 데 사용됩니다. 이 값을 늘리면 수많은 파일 이름에 액세스할 때 네트워크 트래픽을 줄이고 성능을 높일 수 있습니다.

-   **MaxCmds**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\MaxCmds
    ```

    적용 대상: Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Vista, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 및 Windows Server 2008

    기본값은 15입니다. 이 매개 변수는 세션의 미해결 요청 수를 제한합니다. 이 값을 늘리면 더 많은 메모리를 사용할 수 있지만, 더 깊은 요청 파이프라인을 사용하면 성능을 높일 수 있습니다. 또한 MaxMpxCt와 함께 이 값을 늘리면 FindFirstChangeNotification처럼 수많은 미해결 장기 파일 요청 때문에 발생하는 오류를 제거할 수 있습니다. 이 매개 변수는 SMB 2.0 서버와의 연결에 영향을 주지 않습니다.

-   **DormantFileLimit**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\DormantFileLimit
    ```

    적용 대상: Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Vista, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 및 Windows Server 2008

    기본값은 1023입니다. 이 매개 변수는 애플리케이션이 파일을 닫은 후 공유 리소스에서 열어 두어야 하는 최대 파일 수를 지정합니다.

### <a name="client-tuning-example"></a>클라이언트 튜닝 예제

클라이언트 컴퓨터의 일반 튜닝 매개 변수는 컴퓨터를 원격 파일 공유 액세스, 특히 대기 시간이 긴 일부 네트워크를 통한 액세스(예: 지사, 데이터 센터 간 통신, 홈 오피스, 모바일 광대역)에 적합하도록 최적화합니다. 이 설정이 모든 컴퓨터에서 최적이거나 적합한 것은 아닙니다. 이 설정을 적용하기 전에 개별 설정이 미치게 될 영향을 먼저 평가해야 합니다.

| 매개 변수                   | Value | Default |
|-----------------------------|-------|---------|
| DisableBandwidthThrottling  | 1     | 0       |
| FileInfoCacheEntriesMax     | 32768 | 64      |
| DirectoryCacheEntriesMax    | 4096  | 16      |
| FileNotFoundCacheEntriesMax | 32768 | 128     |
| MaxCmds                     | 32768 | 15      |

 

Windows 8부터 **Set-SmbClientConfiguration** 및 **Set-SmbServerConfiguration** Windows PowerShell cmdlet을 사용하여 이러한 여러 SMB 설정을 구성할 수 있습니다. 레지스트리 전용 설정은 Windows PowerShell을 사용하여 구성할 수도 있습니다.

```
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters" RequireSecuritySignature -Value 0 -Force
```
