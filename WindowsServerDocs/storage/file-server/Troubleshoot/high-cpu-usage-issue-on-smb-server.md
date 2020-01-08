---
title: SMB 서버의 높은 CPU 사용량 문제
description: SMB 서버에서 CPU 사용량이 많은 문제를 해결 하는 방법을 소개 합니다.
author: Deland-Han
manager: dcscontentpm
audience: ITPro
ms.topic: article
ms.author: delhan
ms.date: 12/25/2019
ms.openlocfilehash: 8a14952ca90b6ee3bea901fd944d7c9843492fd4
ms.sourcegitcommit: 8cf04db0bc44fd98f4321dca334e38c6573fae6c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/03/2020
ms.locfileid: "75654344"
---
# <a name="high-cpu-usage-issue-on-the-smb-server"></a>SMB 서버의 높은 CPU 사용량 문제

이 문서에서는 SMB 서버에서 CPU 사용량이 많은 문제를 해결 하는 방법을 설명 합니다.

## <a name="high-cpu-usage-because-of-storage-performance-issues"></a>저장소 성능 문제로 인 한 높은 CPU 사용량

저장소 성능 문제로 인해 SMB 서버에서 CPU 사용량이 높아질 수 있습니다. 문제를 해결 하기 전에 srv2의 알려진 문제를 제거 하기 위해 최신 업데이트 롤업이 SMB 서버에 설치 되어 있는지 확인 합니다.

대부분의 경우 시스템 프로세스에서 CPU 사용량이 많은 문제를 확인할 수 있습니다. 계속 하기 전에 프로세스 탐색기를 사용 하 여 srv2 또는 http.sys가 과도 한 CPU 리소스를 사용 하 고 있는지 확인 합니다.

### <a name="storage-area-network-san-scenario"></a>SAN (저장 영역 네트워크) 시나리오

집계 수준에서 전반적인 SAN 성능이 좋은 것 처럼 보일 수 있습니다. 그러나 SMB 문제를 해결 하는 경우 개별 요청 응답 시간이 가장 중요 합니다.

일반적으로이 문제는 SAN의 일부 명령 큐 형태로 인해 발생할 수 있습니다. **Perfmon** 을 사용 하 여 **Microsoft Windows StorPort** 추적을 캡처하고이를 분석 하 여 저장소 응답성을 정확 하 게 결정할 수 있습니다.

### <a name="disk-io-latency"></a>디스크 IO 대기 시간

디스크 IO 대기 시간은 디스크 IO 요청을 만들고 완료 하는 시간 사이의 지연 시간을 측정 한 것입니다.

Perfmon에서 측정 된 IO 대기 시간은 하드웨어 계층에서 소요 된 모든 시간과 Microsoft 포트 드라이버 큐 (SCSI의 경우 Storport)에서 소요 된 시간을 포함 합니다. 실행 중인 프로세스에서 대량 StorPort 큐를 생성 하는 경우 측정 된 대기 시간이 증가 합니다. 이는 IO가 하드웨어 계층에 디스패치 되기 전에 대기 해야 하기 때문입니다.

Perfmon에서 다음 카운터는 실제 디스크 대기 시간을 보여 줍니다.

- "실제 디스크 성능 개체"-\> "Avg. Disk sec/Read counter"-평균 읽기 대기 시간을 표시 합니다.

- "실제 디스크 성능 개체"-\> "Avg. Disk sec/Write counter"-평균 쓰기 대기 시간을 보여 줍니다.

- "실제 디스크 성능 개체"-\> "Avg. Disk sec/Transfer counter"-읽기 및 쓰기에 대 한 결합 된 평균을 보여 줍니다.

"\_Total" 인스턴스는 컴퓨터에 있는 모든 실제 디스크의 대기 시간에 대 한 평균입니다. 각각의 다른 인스턴스는 개별 실제 디스크를 나타냅니다.

> [!NOTE]
> 이러한 카운터를 Avg. Disk transfer/sec와 혼동 하지 마십시오. 이러한 카운터는 완전히 다른 카운터입니다.

### <a name="windows-storage-stack-follows"></a>Windows 저장소 스택 팔 로우

이 섹션에서는 Windows 저장소 스택에 대해 간략하게 설명 합니다.

응용 프로그램은 IO 요청을 만들 때 스택의 맨 위에 있는 Windows IO 하위 시스템으로 요청을 보냅니다. 그러면 IO가 스택에서 하드웨어 "디스크" 하위 시스템으로 이동 합니다. 그런 다음 응답은 모든 백업으로 이동 합니다. 이 과정에서 각 계층은 해당 기능을 수행 하 고 다음 계층에 IO를 전달 합니다.

![스택 흐름](media/high-cpu-usage-issue-on-smb-server-1.png)

Perfmon은 초당 성능 데이터를 만들지 않습니다. 대신 Windows 내의 다른 하위 시스템에서 제공 하는 데이터를 사용 합니다.

"실제 디스크 성능 개체"의 경우 데이터는 저장소 스택의 "파티션 관리자" 수준에서 캡처됩니다.

이전 섹션에서 언급 한 카운터를 측정 하는 경우 "파티션 관리자" 수준 아래에서 요청에 소요 된 모든 시간을 측정 합니다. 파티션 관리자가 스택에서 IO 요청을 보내면 타임 스탬프를 기록 합니다. 반환 될 때 다시 스탬프 하 고 시간 차이를 계산 합니다. 시간 차이는 대기 시간입니다.

이 작업을 수행 하 여 다음 구성 요소에서 소요 된 시간을 고려 합니다.

- 클래스 드라이버-장치 유형 (예: 디스크, 테이프 등)을 관리 합니다.

- 포트 드라이버-SCSI, FC, SATA 등의 전송 프로토콜을 관리 합니다.

- 장치 미니 포트 드라이버-저장소 어댑터에 대 한 장치 드라이버입니다. Raid 컨트롤러 및 FC HBA와 같은 장치의 제조업체에서 제공 합니다.

- 디스크 하위 시스템-장치 미니 포트 드라이버 아래에 있는 모든 항목을 포함 합니다. 이는 단일 실제 하드 디스크에 연결 된 케이블 또는 저장 영역 네트워크 처럼 복잡할 수 있습니다. 문제가이 구성 요소에 의해 발생 한 것으로 확인 되 면 하드웨어 공급 업체에 문의 하 여 문제 해결에 대 한 자세한 내용을 확인 하십시오.

### <a name="disk-queuing"></a>디스크 큐

지정 된 시간에 디스크 하위 시스템에서 허용 하는 제한 된 양의 IO가 있습니다. 초과 IO는 디스크에서 IO를 다시 허용할 수 있을 때까지 큐에 대기 합니다. "파티션 관리자" 수준 아래의 큐에서 IO가 소비한 시간은 Perfmon 실제 디스크 대기 시간 측정에서 고려 됩니다. 큐가 커지고 IO가 더 오래 기다려야 하므로 측정 된 대기 시간도 증가 합니다.

"파티션 관리자" 수준 아래에는 다음과 같은 여러 개의 큐가 있습니다.

- Microsoft Port Driver 큐-SCSIport 또는 Storport 큐

- 제조업체에서 제공 하는 장치 드라이버 큐-OEM 장치 드라이버

- 하드웨어 큐-디스크 컨트롤러 큐, SAN 스위치 큐, 배열 컨트롤러 큐 및 하드 디스크 큐

또한 하드 디스크가 IO를 적극적으로 처리 하는 데 걸리는 시간과 완료 된 것으로 표시 되는 "파티션 관리자" 수준으로 돌아가는 요청에 대 한 이동 시간을 고려 합니다.

마지막으로, 포트 드라이버 큐 (SCSI Storport의 경우)에 특별히 주의 해야 합니다. 포트 드라이버는 제조업체에서 제공 하는 장치 미니 포트 드라이버로 전달 하기 전에 IO를 터치 하는 마지막 Microsoft 구성 요소입니다.

장치 미니 포트 드라이버가 더 많은 IO를 허용할 수 없는 경우 해당 큐 또는 하드웨어 큐의 채도가 포화 상태 이므로 포트 드라이버 큐에서 IO 누적을 시작 합니다. Microsoft Port Driver queue의 크기는 사용 가능한 시스템 메모리 (RAM)에 의해서만 제한 되며 매우 커질 수 있습니다. 이렇게 하면 측정 된 긴 대기 시간이 발생 합니다.

## <a name="high-cpu-caused-by-enumerating-folders"></a>폴더를 열거 하 여 발생 하는 높은 CPU 

이 문제를 해결 하려면 ABE (액세스 기반 열거) 기능을 사용 하지 않도록 설정 합니다.

ABE가 사용 하도록 설정 된 SMB 공유를 확인 하려면 다음 PowerShell 명령을 실행 합니다.

```PowerShell
Get-SmbShare | Select Name, FolderEnumerationMode
```

무제한 = ABE 사용 안 함 <br />
AccessBase = ABE 사용.


**서버 관리자**에서 ABE을 사용 하도록 설정할 수 있습니다. **파일 및 저장소 서비스** > **공유**로 Navigatie 공유를 마우스 오른쪽 단추로 클릭 하 고 **속성**을 선택한 다음 **설정** 으로 이동 하 여 **액세스 기반 열거 사용**을 선택 합니다.

![UI 옵션](media/high-cpu-usage-issue-on-smb-server-2.png)

또한 **ABELevel** 를 낮은 수준 (1 또는 2)으로 줄여서 성능을 향상 시킬 수 있습니다.

콘솔 또는 RDP 세션을 통해 로컬에서 폴더를 열어 열거 속도가 느려지는 경우 디스크 성능을 확인할 수 있습니다.
