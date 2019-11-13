---
title: SMB 파일 서버 성능 조정
description: SMB 파일 서버 성능 조정
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: article
author: phstee
ms.author: NedPyle; Danlo; DKruse
ms.date: 4/14/2017
ms.openlocfilehash: 5383d16ac4c98651aa6afe996dbad88a6d60ee7a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71370231"
---
# <a name="performance-tuning-for-smb-file-servers"></a>SMB 파일 서버 성능 조정

## <a name="smb-configuration-considerations"></a>SMB 구성 고려 사항
파일 서버 및 클라이언트에 필요 하지 않은 서비스 또는 기능을 사용 하도록 설정 하지 마세요. 여기에는 SMB 서명, 클라이언트 쪽 캐싱, 파일 시스템 미니 필터, 검색 서비스, 예약 된 작업, NTFS 암호화, NTFS 압축, IPSEC, 방화벽 필터, Teredo 및 SMB 암호화가 포함 될 수 있습니다.

성능 우선 모드 또는 변경 된 C 상태를 포함 하는 필요에 따라 BIOS 및 운영 체제 전원 관리 모드가 설정 되어 있는지 확인 합니다. 최신의 복원 력 및 가장 빠른 저장소 및 네트워킹 장치 드라이버가 설치 되어 있는지 확인 합니다.

파일 복사는 파일 서버에서 수행 되는 일반적인 작업입니다. Windows Server에는 명령 프롬프트를 사용 하 여 실행할 수 있는 몇 가지 기본 제공 파일 복사 유틸리티가 있습니다. Robocopy를 권장 합니다. Windows Server 2008 r 2에 도입 된 **Robocopy 옵션을 사용 하면 여러** 개의 작은 파일을 복사할 때 여러 스레드를 사용 하 여 원격 파일 전송 속도를 크게 향상 시킬 수 있습니다. 또한 로그를 NUL 장치 또는 파일로 리디렉션하여 **/log** 옵션을 사용 하 여 콘솔 출력을 줄이는 것이 좋습니다. Xcopy를 사용 하는 경우 기존 매개 변수에 **/q** 및 **/k** 옵션을 추가 하는 것이 좋습니다. 이전 옵션은 콘솔 출력을 줄여 CPU 오버 헤드를 줄이고, 후자는 네트워크 트래픽을 감소 시킵니다.

## <a name="smb-performance-tuning"></a>SMB 성능 튜닝


파일 서버 성능 및 사용 가능한 tunings은 각 클라이언트와 서버 간에 협상 되는 SMB 프로토콜 및 배포 된 파일 서버 기능에 따라 달라 집니다. 현재 사용할 수 있는 가장 높은 프로토콜 버전은 Windows Server 2016 및 Windows 10의 SMB 3.1.1입니다. 클라이언트에서 Windows PowerShell **SMBConnection** 을 사용 하 여 네트워크에서 사용 중인 SMB 버전을 확인할 수 있습니다. **SMBSession |** 서버에 대 한 FL.

### <a name="smb-30-protocol-family"></a>SMB 3.0 프로토콜 패밀리

SMB 3.0은 windows server 2012에서 도입 되었으며 windows server 2012 R2 (SMB 3.02) 및 Windows Server 2016 (SMB 3.1.1)에서 향상 되었습니다. 이 버전은 파일 서버의 성능 및 가용성을 크게 향상 시킬 수 있는 기술을 도입 했습니다. 자세한 내용은 [Windows Server 2012 및 2012 R2 2012의 smb](https://aka.ms/smb3plus) 및 [smb 3.1.1의 새로운 기능](https://aka.ms/smb311)을 참조 하세요.



### <a name="smb-direct"></a>SMB 다이렉트

SMB 다이렉트에는 짧은 대기 시간 및 낮은 CPU 사용률으로 높은 처리량을 위해 RDMA 네트워크 인터페이스를 사용 하는 기능이 도입 되었습니다.

SMB는 RDMA 지원 네트워크를 검색할 때마다 RDMA 기능을 자동으로 사용 하려고 시도 합니다. 그러나 어떤 이유로 든 SMB 클라이언트가 RDMA 경로를 사용 하 여 연결 하지 못하는 경우에는 대신 TCP/IP 연결을 계속 해 서 사용 합니다. SMB 다이렉트와 호환 되는 모든 RDMA 인터페이스는 TCP/IP 스택을 구현 하는 데 필요 하며, SMB 다중 채널은이를 인식 합니다.

Smb 다이렉트는 SMB 구성에 필요 하지 않지만, 대기 시간이 짧고 CPU 사용률을 낮추는 경우에는 항상 권장 됩니다.

SMB 다이렉트에 대 한 자세한 내용은 [Smb 다이렉트를 사용 하 여 파일 서버의 성능 향상](https://aka.ms/smbdirect)을 참조 하세요.

### <a name="smb-multichannel"></a>SMB 다중 채널

SMB 다중 채널을 통해 파일 서버는 여러 네트워크 연결을 동시에 사용할 수 있으며 처리량이 증가 합니다.

SMB 다중 채널에 대 한 자세한 내용은 [Smb 다중 채널 배포](https://aka.ms/smbmulti)를 참조 하세요.

### <a name="smb-scale-out"></a>SMB 스케일 아웃

SMB 스케일 아웃을 사용 하면 클러스터 구성의 SMB 3.0에서 클러스터의 모든 노드에 대 한 공유를 표시할 수 있습니다. 이 능동/능동 구성을 사용 하면 여러 볼륨, 공유 및 클러스터 리소스를 사용 하는 복잡 한 구성 없이 파일 서버 클러스터를 추가로 확장할 수 있습니다. 최대 공유 대역폭은 모든 파일 서버 클러스터 노드의 총 대역폭입니다. 총 대역폭은 더 이상 단일 클러스터 노드의 대역폭으로 제한 되지 않으며, 백업 저장소 시스템의 기능에 따라 달라 집니다. 노드를 추가하면 총 대역폭을 높일 수 있습니다.

SMB 스케일 아웃에 대 한 자세한 내용은 [응용 프로그램 데이터 개요](https://technet.microsoft.com/library/hh831349.aspx) 및 [규모 확장을](http://blogs.technet.com/b/filecab/archive/2013/12/05/to-scale-out-or-not-to-scale-out-that-is-the-question.aspx)위한 블로그 게시물에 대 한 스케일 아웃 파일 서버를 참조 하세요.

### <a name="performance-counters-for-smb-30"></a>SMB 3.0에 대 한 성능 카운터

다음 SMB 성능 카운터는 Windows Server 2012에서 도입 되었으며, SMB 2 이상 버전의 리소스 사용을 모니터링 하는 경우 기본 카운터 집합으로 간주 됩니다. 성능 카운터를 로컬, 원시 (.blg) 성능 카운터 로그에 기록 합니다. 와일드 카드 문자 (\*)를 사용 하 여 모든 인스턴스를 수집한 다음, msiexec.exe를 사용 하 여 사후 처리 중에 특정 인스턴스를 추출 하는 것은 비용이 저렴 합니다.

-   **SMB 클라이언트 공유**

    이러한 카운터는 SMB 2.0 이상 버전을 사용 하는 클라이언트에서 액세스 하는 서버의 파일 공유에 대 한 정보를 표시 합니다.

    Windows에서 일반 디스크 카운터에 대해 잘 알고 있는 경우 특정과을 확인할 수 있습니다. 실수로 인 한 ' s '입니다. SMB 클라이언트 공유 성능 카운터는 디스크 카운터와 정확히 일치 하도록 설계 되었습니다. 이러한 방식으로 현재 응용 프로그램 디스크 성능 튜닝에 대 한 지침을 쉽게 다시 사용할 수 있습니다. 카운터 매핑에 대 한 자세한 내용은 [공유 클라이언트 성능 카운터 블로그](http://blogs.technet.com/b/josebda/archive/2012/11/19/windows-server-2012-file-server-tip-new-per-share-smb-client-performance-counters-provide-great-insight.aspx)를 참조 하십시오.

-   **SMB 서버 공유**

    이러한 카운터는 서버의 SMB 2.0 이상 파일 공유에 대 한 정보를 표시 합니다.

-   **SMB 서버 세션**

    이러한 카운터는 SMB 2.0 이상을 사용 하는 SMB 서버 세션에 대 한 정보를 표시 합니다.

    서버 쪽 (서버 공유 또는 서버 세션)에서 카운터를 켜면 높은 IO 작업에 상당한 성능 영향을 줄 수 있습니다.

-   **키 필터 다시 시작**

    이러한 카운터는 키 다시 시작 필터에 대 한 정보를 표시 합니다.

-   **SMB 직접 연결**

    이러한 카운터는 연결 작업의 다양 한 측면을 측정 합니다. 컴퓨터에는 여러 SMB 직접 연결을 사용할 수 있습니다. SMB 직접 연결 카운터는 각 연결을 IP 주소 및 포트 쌍으로 나타냅니다. 여기서 첫 번째 IP 주소와 포트는 연결의 로컬 끝점을 나타내고 두 번째 IP 주소와 포트는 연결의 원격 끝점을 나타냅니다.

-   **실제 디스크, SMB, CSV FS 성능 카운터 관계**

    실제 디스크, SMB 및 CSV FS (파일 시스템) 카운터가 관련 된 방법에 대 한 자세한 내용은 다음 블로그 게시물 [클러스터 공유 볼륨 성능 카운터](http://blogs.msdn.com/b/clustering/archive/2014/06/05/10531462.aspx)를 참조 하세요.

## <a name="tuning-parameters-for-smb-file-servers"></a>SMB 파일 서버에 대 한 튜닝 매개 변수


다음 REG\_DWORD 레지스트리 설정은 SMB 파일 서버의 성능에 영향을 줄 수 있습니다.

- **Smb2CreditsMin** 및 **Smb2CreditsMax**

  ```
  HKLM\System\CurrentControlSet\Services\LanmanServer\Parameters\Smb2CreditsMin
  ```

  ```
  HKLM\System\CurrentControlSet\Services\LanmanServer\Parameters\Smb2CreditsMax
  ```

  기본값은 각각 512 및 8192입니다. 이러한 매개 변수를 통해 서버는 지정 된 경계 내에서 동적으로 클라이언트 작업 동시성을 제한할 수 있습니다. 일부 클라이언트는 높은 대역폭의 대기 시간이 긴 링크를 통해 파일을 복사 하는 등 동시성 한도가 더 높은 처리량을 높일 수 있습니다.
    
  > [!TIP]
  > Windows 10 및 Windows Server 2016 이전 버전에서는 클라이언트에 부여 되는 크레딧 수가 네트워크 대기 시간에 따라 부여할 최적의 크레딧 수를 결정 하려고 시도 하는 알고리즘에 따라 Smb2CreditsMin와 Smb2CreditsMax 사이에서 동적으로 다양 합니다. 및 신용 사용. Windows 10 및 Windows Server 2016에서 SMB 서버는 구성 된 최대 크레딧 수까지 요청 시 크레딧을 부여 하도록 변경 되었습니다. 이 변경의 일환으로, 서버의 메모리가 부족할 때 각 연결의 크레딧 크기를 줄이는 신용 조정 메커니즘이 제거 되었습니다. 제한에 의해 트리거되는 커널 메모리 부족 이벤트는 서버의 메모리가 부족 한 경우에만 신호를 발생 시킬 수 있습니다 (< 몇 MB). 서버는 더 이상 크레딧 창을 축소 하지 않으므로 Smb2CreditsMin 설정이 더 이상 필요 하지 않으며 이제 무시 됩니다.
  > 
  > 크레딧 대기 수\\SMB 클라이언트 공유를 모니터링 하 여 크레딧에 문제가 있는지 확인할 수 있습니다.

- **AdditionalCriticalWorkerThreads**

    ```
    HKLM\System\CurrentControlSet\Control\Session Manager\Executive\AdditionalCriticalWorkerThreads
    ```

    기본값은 0 이며,이는 추가 중요 한 커널 작업자 스레드가 추가 되지 않음을 의미 합니다. 이 값은 파일 시스템 캐시가 미리 읽기 및 쓰기에 필요한 요청에 사용 하는 스레드 수에 영향을 줍니다. 이 값을 사용 하면 저장소 하위 시스템에서 대기 중인 i/o가 더 많을 수 있으며, 특히 논리 프로세서가 많고 강력한 저장소 하드웨어를 사용 하는 시스템에서 i/o 성능을 향상 시킬 수 있습니다.

    >[!TIP]
    > 캐시 관리자 더티 데이터 (성능 카운터 캐시\\더티 페이지)의 양이 증가 하 여 많은 부분을 사용 하는 경우 값을 늘려야 할 수 있습니다 (25% 이상). 메모리 또는 시스템에서 동기 읽기 i/o를 많이 수행 하는 경우

- **MaxThreadsPerQueue**

  ```
  HKLM\System\CurrentControlSet\Services\LanmanServer\Parameters\MaxThreadsPerQueue
  ```

  기본값은 20입니다. 이 값을 늘려도 파일 서버가 동시 요청을 처리 하는 데 사용할 수 있는 스레드 수가 발생 합니다. 많은 수의 활성 연결을 처리 해야 하 고 저장소 대역폭과 같은 하드웨어 리소스가 충분 한 경우이 값을 늘려도 서버 확장성, 성능 및 응답 시간을 향상 시킬 수 있습니다.

  >[!TIP]
  > SMB2 작업 큐가 매우 큰 경우 (성능 카운터의 서버 작업 큐\\큐 길이\\SMB2 비블로킹 \*'이 (가) 100 이상) 증가 하는 경우 값이 증가 해야 함을 나타냅니다.

  >[!Note]
  >Windows 10 및 Windows Server 2016에서는 MaxThreadsPerQueue을 사용할 수 없습니다. 스레드 풀의 스레드 수는 "20 * NUMA 노드의 프로세서 수"입니다.
     

- **AsynchronousCredits**

  ``` 
  HKLM\System\CurrentControlSet\Services\LanmanServer\Parameters\AsynchronousCredits
  ```

  기본값은 512입니다. 이 매개 변수는 단일 연결에서 허용 되는 동시 비동기 SMB 명령의 수를 제한 합니다. 백 엔드 IIS 서버를 사용 하는 프런트 엔드 서버를 사용 하는 경우와 같이 일부 경우에는 많은 양의 동시성이 필요 합니다 (특히 파일 변경 알림 요청의 경우). 이러한 경우를 지원 하기 위해이 항목의 값을 늘릴 수 있습니다.

### <a name="smb-server-tuning-example"></a>SMB 서버 튜닝 예제

다음 설정은 대부분의 경우 파일 서버 성능에 대 한 컴퓨터를 최적화할 수 있습니다. 이 설정이 모든 컴퓨터에서 최적이거나 적합한 것은 아닙니다. 이 설정을 적용하기 전에 개별 설정이 미치게 될 영향을 먼저 평가해야 합니다.

| 매개 변수                       | 값 | 기본값 |
|---------------------------------|-------|---------|
| AdditionalCriticalWorkerThreads | 64    | 0       |
| MaxThreadsPerQueue              | 64    | 20      |


### <a name="smb-client-performance-monitor-counters"></a>SMB 클라이언트 성능 모니터 카운터

SMB 클라이언트 카운터에 대 한 자세한 내용은 [Windows Server 2012 파일 서버 팁: 새 공유 당 SMB 클라이언트 성능 카운터에서 뛰어난](http://blogs.technet.com/b/josebda/archive/2012/11/19/windows-server-2012-file-server-tip-new-per-share-smb-client-performance-counters-provide-great-insight.aspx)정보를 제공 합니다.
