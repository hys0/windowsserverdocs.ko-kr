---
title: SMB 파일 서버 성능 조정
description: SMB 파일 서버 성능 조정
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
author: phstee
ms.author: NedPyle; Danlo; DKruse
ms.date: 4/14/2017
ms.openlocfilehash: 87ad8058f7353c938087b1211e0f17820f0bd2ae
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66435652"
---
# <a name="performance-tuning-for-smb-file-servers"></a>SMB 파일 서버 성능 조정

## <a name="smb-configuration-considerations"></a>SMB 구성 고려 사항
파일 서버 및 클라이언트가 필요 하지 않은 기능이 나 서비스를 사용 하지 마십시오. SMB 서명, 클라이언트 쪽 캐싱, 파일 시스템 미니 필터, 검색 서비스, 예약 된 작업, NTFS 암호화, NTFS 압축, IPSEC, 방화벽 필터, Teredo 및 SMB 포함 될 수 있습니다 이러한 암호화 합니다.

성능 우선 모드에 포함 될 수 있습니다 또는 C-상태를 변경 하는 BIOS 및 운영 체제 전원 관리 모드를 필요에 따라 설정 되어 있는지 확인 합니다. 최신 복원 력이 가장 쉽고 빠른 저장소 및 네트워킹 장치 드라이버가 설치 되어 있는지 확인 합니다.

파일 서버에서 수행 하는 일반적인 작업은 파일을 복사 합니다. Windows Server 명령 프롬프트를 사용 하 여 실행할 수 있는 몇 가지 기본 제공 파일 복사 유틸리티에 있습니다. Robocopy는 사용 하는 것이 좋습니다. Windows Server 2008 R2에 도입 된 **/mt** Robocopy 옵션이 여러 작은 파일을 복사 하는 경우에 여러 스레드를 사용 하 여 원격 파일 전송 속도 크게 개선할 수 있습니다. 사용 하는 것이 좋습니다 합니다 **로그** 로그 NUL 장치 또는 파일로 리디렉션하여 콘솔 출력을 줄이려면 옵션을 합니다. Xcopy를 사용 하면 추가 하는 것이 좋습니다 합니다 **/q** 하 고 **/k** 기존 매개 변수 옵션입니다. 첫 번째 옵션 CPU 오버 헤드가 콘솔 출력을 줄여 줄어들고 후자 네트워크 트래픽이 줄어듭니다.

## <a name="smb-performance-tuning"></a>SMB 성능 튜닝


파일 서버 성능 및 사용 가능한 tunings 각 클라이언트와 서버 사이의 협상 되는 SMB 프로토콜에 배포 된 파일 서버 기능에 따라 달라 집니다. 현재 사용 가능한 가장 높은 프로토콜 버전 SMB 3.1.1 Windows Server 2016 및 Windows 10의 경우 Windows PowerShell을 사용 하 여 네트워크에서 사용 되는 SMB 버전을 확인할 수 있습니다 **Get SMBConnection** 클라이언트에서 및 **Get SMBSession | FL** 서버의 합니다.

### <a name="smb-30-protocol-family"></a>SMB 3.0 프로토콜 제품군

SMB 3.0 Windows Server 2012에서 도입 되었으며 (SMB 3.02) Windows Server 2012 R2 및 Windows Server 2016 (SMB 3.1.1)에서 더욱 향상 되었습니다. 이 버전의 파일 서버 성능 및 가용성에 크게 향상 시킬 수 있는 기술을 도입 되었습니다. 자세한 내용은 참조 하세요. [SMB Windows Server 2012 및 2012 R2 2012](https://aka.ms/smb3plus) 하 고 [3.1.1 SMB의 새로운 기능](https://aka.ms/smb311).



### <a name="smb-direct"></a>SMB 다이렉트

SMB 다이렉트 짧은 대기 시간 및 낮은 CPU 사용률을 사용 하 여 높은 처리량에 대 한 RDMA 네트워크 인터페이스를 사용 하는 기능을 도입 했습니다.

SMB는 RDMA 가능 네트워크에 검색 될 때마다 자동으로 RDMA 기능을 사용 하려고 합니다. 그러나 어떤 이유로 든 SMB 클라이언트가 연결 하지 못하는 경우 RDMA 경로 사용 하 여, TCP/IP 연결을 대신 사용 하려면 단순히 계속 됩니다. SMB 다이렉트와 호환 되는 모든 RDMA 인터페이스는 TCP/IP 스택을 구현 하는 데 필요한 및 SMB 다중 채널은 주의 합니다.

SMB 다이렉트에서는 필요 하지 않습니다 모든 SMB 구성 하지만 ' s 항상 더 낮은 대기 시간 및 낮은 CPU 사용률을 원하는 파트너에 대 한 것이 좋습니다.

SMB 다이렉트에 대 한 자세한 내용은 참조 하세요. [SMB 다이렉트를 사용 하 여 파일 서버의 성능 향상](https://aka.ms/smbdirect)합니다.

### <a name="smb-multichannel"></a>SMB 다중 채널

SMB 다중 채널 파일 서버가 동시에 여러 네트워크 연결을 사용할 수 있도록 하 고 향상 된 처리량을 제공 합니다.

SMB 다중 채널에 대 한 자세한 내용은 참조 하세요. [SMB 다중 채널 배포](https://aka.ms/smbmulti)합니다.

### <a name="smb-scale-out"></a>SMB 스케일 아웃

SMB 스케일 아웃 클러스터의 모든 노드에서 공유를 표시 하려면 클러스터 구성에서 SMB 3.0을 허용 합니다. 이 능동/능동 구성을 여러 볼륨, 공유 및 클러스터 리소스를 사용 하 여 복잡 한 구성 없이 확장 파일 서버 클러스터 또한 수 있습니다. 최대 공유 대역폭은 모든 파일 서버 클러스터 노드의 총 대역폭입니다. 총 대역폭을 단일 클러스터 노드의 대역폭으로 제한 되지 않습니다 하지만 대신 백업 저장소 시스템의 기능에 따라 달라 집니다. 노드를 추가하면 총 대역폭을 높일 수 있습니다.

SMB 스케일 아웃에 대 한 자세한 정보를 참조 하세요. [스케일 아웃 파일 서버에 대 한 응용 프로그램 데이터 개요](https://technet.microsoft.com/library/hh831349.aspx) 및 블로그 게시물 [스케일 아웃 또는 수평적 필요가 냐 그것이 문제다](http://blogs.technet.com/b/filecab/archive/2013/12/05/to-scale-out-or-not-to-scale-out-that-is-the-question.aspx)합니다.

### <a name="performance-counters-for-smb-30"></a>SMB 3.0에 대 한 성능 카운터

Windows Server 2012에서 도입 된 다음 SMB 성능 카운터 및 SMB 2 및 더 높은 버전의 리소스 사용량을 모니터링 하는 경우 기본 카운터 집합을 간주 됩니다. 로컬, 성능 카운터를 로그 (.blg) 원시 성능 카운터 로그 합니다. 와일드 카드 문자를 사용 하 여 모든 인스턴스를 수집 하는 것 (\*), 한 다음 후 처리 동안 Relog.exe를 사용 하 여 특정 인스턴스를 추출 합니다.

-   **SMB 클라이언트 공유**

    이러한 카운터는 SMB 2.0 이상 버전을 사용 하는 클라이언트에서 액세스 하는 서버에서 파일 공유에 대 한 정보를 표시 합니다.

    경우 있습니다 ' Windows에서 정기적인 디스크 카운터를 사용 하 여 친숙 하면서도 다시 특정 매우 유사한을 확인할 수 있습니다. ' s 실수로 없습니다. SMB 클라이언트 공유 성능 카운터는 디스크 카운터를 정확 하 게 일치 하도록 설계 되었습니다. 응용 프로그램 디스크 성능 조정에 대 한 모든 지침을 쉽게 다시 사용할 수 있습니다 이러한 방식으로 현재 해야 합니다. 카운터 매핑에 대 한 자세한 내용은 참조 하세요. [공유 클라이언트 성능 카운터 블로그 당](http://blogs.technet.com/b/josebda/archive/2012/11/19/windows-server-2012-file-server-tip-new-per-share-smb-client-performance-counters-provide-great-insight.aspx)합니다.

-   **SMB 서버 공유**

    이러한 카운터는 서버에서 SMB 2.0 또는 더 높은 파일 공유에 대 한 정보를 표시합니다.

-   **SMB 서버 세션**

    이러한 카운터는 SMB 2.0 이상을 사용 하는 SMB 서버 세션에 대 한 정보를 표시 합니다.

    서버 쪽 (서버 공유 또는 서버 세션)에서 카운터를 설정 하면 성능에 상당한 영향이 높은 IO 워크 로드에 대 한 있을 수 있습니다.

-   **키 필터를 다시 시작**

    이러한 카운터를 다시 시작 키 필터에 대 한 정보를 표시합니다.

-   **SMB 다이렉트 연결**

    이러한 카운터는 연결 작업의 다양 한 측면을 측정합니다. 컴퓨터에는 SMB 다이렉트는 여러 연결이 있을 수 있습니다. SMB 다이렉트 연결 카운터 IP 주소 및 포트, 여기서 첫 번째 IP 주소 및 포트를 나타내는 연결의 로컬 끝점 및 두 번째 IP 주소 및 포트를 나타내는 연결의 원격 끝점의 쌍으로 각 연결을 나타냅니다.

-   **실제 디스크, SMB, CSV FS 성능 카운터 관계**

    실제 디스크, SMB 및 CSV FS (파일 시스템) 카운터와 관련 된 방법에 대 한 자세한 내용은 다음 블로그 게시물을 참조 하세요. [클러스터 공유 볼륨 성능 카운터](http://blogs.msdn.com/b/clustering/archive/2014/06/05/10531462.aspx)합니다.

## <a name="tuning-parameters-for-smb-file-servers"></a>SMB 파일 서버에 대 한 튜닝 매개 변수


다음 레지스트리\_DWORD 레지스트리 설정에는 SMB 파일 서버의 성능에 영향을 줄 수 있습니다.

- **Smb2CreditsMin** 고 **Smb2CreditsMax**

  ```
  HKLM\System\CurrentControlSet\Services\LanmanServer\Parameters\Smb2CreditsMin
  ```

  ```
  HKLM\System\CurrentControlSet\Services\LanmanServer\Parameters\Smb2CreditsMax
  ```

  기본값은 각각 512에서 8192입니다. 이러한 매개 변수는 지정된 된 경계 내에서 동적으로 클라이언트 작업 동시성을 제한 하는 서버를 사용 합니다. 일부 클라이언트에 높은 대역폭, 대기 시간이 긴 연결을 통해 파일 복사 하 여 한도가 더 높은 동시성, 예를 들어, 향상 된 처리량을 얻을 수 있습니다.
    
  > [!TIP]
  > Windows 10 및 Windows Server 2016 이전의 클라이언트에 부여 하는 학점 수가 다양 한 동적으로 Smb2CreditsMin 사이의 네트워크 대기 시간에 따라 최적의 부여할 학점 수를 확인 하려고 하는 알고리즘을 기반으로 Smb2CreditsMax 및 크레딧 사용 합니다. Windows 10 및 Windows Server 2016에서 무조건 크레딧 크레딧의 구성 된 최대 수는 요청 시 권한을 부여 하려면 SMB 서버 변경 되었습니다. 이 변경의 일환으로, 조정 메커니즘을 서버 메모리가 부족할 때 각 연결의 신용 창의 크기를 줄일 수, 신용 제거 되었습니다. 서버 메모리가 부족 하므로 때 제한 트리거한 커널의 메모리 이벤트가 신호 (< 몇 MB) 쓸모 없게 하는 것에 대 한 합니다. 서버에는 더 이상 신용 windows 축소 하므로 Smb2CreditsMin 설정 기능이 더 이상 필요 하 고 이제 무시 됩니다.
  > 
  > SMB 클라이언트 공유를 모니터링할 수 있습니다\\신용 지연 되는 경우 수/초에 크레딧 사용 하 여 문제가 있는지 확인 합니다.

- **AdditionalCriticalWorkerThreads**

    ```
    HKLM\System\CurrentControlSet\Control\Session Manager\Executive\AdditionalCriticalWorkerThreads
    ```

    기본값은 0으로, 중요 한 커널 추가 작업자 스레드가 없고 추가 된 것을 의미 합니다. 이 값에 미리 읽기 및 쓰기 요청에 대 한 파일 시스템 캐시를 사용 하는 스레드 수가 달라 집니다. 이 값을 발생 시키는 저장소 하위 시스템의 I/O를 대기 중인 더 많은 논리 프로세서와 강력한 저장소 하드웨어를 사용 하 여 시스템에서 특히 I/O 성능을 높일 수 있다는 대해 허용할 수 있습니다.

    >[!TIP]
    > 값을 캐시 관리자 양을 더티 데이터 경우 늘려야 할 수 있습니다 (성능 카운터 캐시\\더티 페이지) 차지할 (개 ~ 25%) 증가 메모리 또는 시스템 동기 많이 수행 하는 경우 읽기 I/o입니다.

- **MaxThreadsPerQueue**

  ```
  HKLM\System\CurrentControlSet\Services\LanmanServer\Parameters\MaxThreadsPerQueue
  ```

  기본값은 20입니다. 이 값을 늘리면 파일 서버 서비스 동시 요청 수를 사용할 수 있는 스레드 수를 발생 시킵니다. 많은 수의 활성 연결을 처리 해야 하는 경우 저장소 대역폭 등의 하드웨어 리소스가 충분 한 되어 서버 확장성, 성능 및 응답 시간 향상 수 값을 늘리면 합니다.

  >[!TIP]
  > 값을 늘려야 할 수 있는 표시가 SMB2 작업 큐에 점점 매우 큰 경우 (성능 카운터 ' 서버 작업 큐\\Queue Length\\SMB2 비차단 \*' ~ 100 보다 일관 되 게).

  >[!Note]
  >Windows 10 및 Windows Server 2016에서 MaxThreadsPerQueue 제공 되지 않습니다. 스레드 풀 스레드 수 "20 * NUMA 노드에서 프로세서에에서 개수"입니다.
     

- **AsynchronousCredits**

  ``` 
  HKLM\System\CurrentControlSet\Services\LanmanServer\Parameters\AsynchronousCredits
  ```

  기본값은 512입니다. 이 매개 변수는 단일 연결에서 허용 되는 동시 비동기 SMB 명령 수를 제한 합니다. 일부 경우 (때와 같이 백 엔드 IIS 서버를 사용 하 여 프런트 엔드 서버가) (특히 파일 변경 알림 요청)의 동시성을 많이 필요 합니다. 이러한 사례를 지원 하려면이 항목의 값을 늘릴 수 있습니다.

### <a name="smb-server-tuning-example"></a>SMB 서버 튜닝 예제

다음 설정은 대부분의 경우에서 파일 서버의 성능에 대 한 컴퓨터를 최적화할 수 있습니다. 이 설정이 모든 컴퓨터에서 최적이거나 적합한 것은 아닙니다. 이 설정을 적용하기 전에 개별 설정이 미치게 될 영향을 먼저 평가해야 합니다.

| 매개 변수                       | 값 | 기본값 |
|---------------------------------|-------|---------|
| AdditionalCriticalWorkerThreads | 64    | 0       |
| MaxThreadsPerQueue              | 64    | 20      |


### <a name="smb-client-performance-monitor-counters"></a>SMB 클라이언트 성능 모니터 카운터

SMB 클라이언트 카운터에 대 한 자세한 내용은 참조 하세요. [Windows Server 2012 파일 서버 팁: 새 공유 당 SMB 클라이언트 성능 카운터는 심층적인 시야를 제공 합니다.](http://blogs.technet.com/b/josebda/archive/2012/11/19/windows-server-2012-file-server-tip-new-per-share-smb-client-performance-counters-provide-great-insight.aspx)합니다.
