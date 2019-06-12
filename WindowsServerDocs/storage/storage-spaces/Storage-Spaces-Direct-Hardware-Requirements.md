---
title: 저장소 공간 다이렉트 하드웨어 요구 사항
ms.prod: windows-server-threshold
description: 저장소 공간 다이렉트 테스트에 대한 최소 하드웨어 요구 사항
ms.author: eldenc
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: eldenchristensen
ms.date: 06/04/2019
ms.localizationpriority: medium
ms.openlocfilehash: f2031afada302c0f73621a75f572c8547620db16
ms.sourcegitcommit: cd12ace92e7251daaa4e9fabf1d8418632879d38
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2019
ms.locfileid: "66501655"
---
# <a name="storage-spaces-direct-hardware-requirements"></a>저장소 공간 다이렉트 하드웨어 요구 사항

> 적용 대상: Windows Server 2019, Windows Server 2016

이 항목에서는 저장소 공간 다이렉트에 대 한 최소 하드웨어 요구 사항을 설명 합니다.

프로덕션 환경에서는 파트너에서 유효성이 검사 된 하드웨어/소프트웨어 솔루션을 구매 권장 배포 도구 및 절차 포함는 합니다. 이러한 솔루션 설계, 조립 및 호환성 및 안정성 얻게 되므로 신속 하 게 실행 하기 위한이 참조 아키텍처에 대해 유효성이 검사 됩니다. Windows Server 2019 솔루션에 대 한 참조를 [Azure Stack HCI solutions 웹 사이트](https://azure.microsoft.com/overview/azure-stack/hci)합니다. Windows Server 2016 솔루션에 대 한 자세한 내용은 [Windows Server 소프트웨어 정의](https://microsoft.com/wssd)합니다.

![Windows Server 소프트웨어 정의 파트너 로고](media/hardware-requirements/wssd-partners.png)

   > [!TIP]
   > 저장소 공간 다이렉트를 평가 하 고 싶지만 하드웨어 없습니다? 에 설명 된 대로 Hyper-v 또는 Azure virtual machines를 사용 하 여 [를 사용 하 여 저장소 공간 다이렉트 게스트 가상 컴퓨터 클러스터에서](storage-spaces-direct-in-vm.md)합니다.

## <a name="base-requirements"></a>기본 요구 사항

시스템, 구성 요소, 장치 및 드라이버 여야 **Windows Server 2016 Certified** 당 합니다 [Windows Server 카탈로그](https://www.windowsservercatalog.com)합니다. 또한 서버, 드라이브, 호스트 버스 어댑터 및 네트워크 어댑터는 좋습니다 합니다 **소프트웨어 정의 데이터 센터 (SDDC) 표준** 및/또는 **소프트웨어 정의 데이터 센터 (SDDC) Premium** (AQs), 다음 그림과 같이 한정자를 추가 합니다. SDDC AQs를 사용 하 여 1,000 개 구성 요소가 있습니다.

![Windows Server 카탈로그 SDDC AQs를 보여 주는 스크린샷](media/hardware-requirements/sddc-aqs.png)

완전히 구성 된 클러스터 (서버, 네트워킹 및 저장소)는 모두 통과 해야 [클러스터 유효성 검사 테스트](https://technet.microsoft.com/library/cc732035(v=ws.10).aspx) 장애 조치 클러스터 관리자 또는 마법사 당 합니다 `Test-Cluster` [cmdlet](https://docs.microsoft.com/powershell/module/failoverclusters/test-cluster?view=win10-ps) powershell에서.

또한 다음 요구 사항이 적용 됩니다.

## <a name="servers"></a>서버

- 최소 2대~최대 16대의 서버
- 모든 서버가 동일한 제조업체 및 모델을는 것이 좋습니다.

## <a name="cpu"></a>CPU

- Intel Nehalem 또는 호환 프로세서 이상; 또는
- AMD EPYC 또는 호환 프로세서 이상

## <a name="memory"></a>메모리

- Windows Server, Vm 및 다른 앱 또는 워크 로드;에 대 한 메모리 더하기
- 4GB의 RAM (테라바이트)의 저장소 공간 다이렉트 메타 데이터에 대 한 각 서버에서 캐시 드라이브 용량 단위

## <a name="boot"></a>Boot

- Windows Server에서 지원 되는 모든 부팅 장치는 [이제 SATADOM 포함 되어 있습니다.](https://cloudblogs.microsoft.com/windowsserver/2017/08/30/announcing-support-for-satadom-boot-drives-in-windows-server-2016/)
- RAID 1 미러가 **되지** 필수는 아니지만 부팅용으로 지원
- 권장: 최소 크기를 200GB

## <a name="networking"></a>네트워킹

최소 (예: 소규모 2 ~ 3 노드)
- 10gbps 네트워크 인터페이스
- 2-노드는 직접 연결 (switchless)

권장 (높은 성능, 규모 또는 4 + 노드 배포에)
- 된 Nic를 지 원하는 경우 원격 직접 메모리 액세스 (RDMA) (권장) iWARP 또는 RoCE
- 중복 및 성능에 대 한 두 개 이상의 Nic
- 25 Gbps 네트워크 인터페이스 이상

## <a name="drives"></a>드라이브

저장소 공간 다이렉트 직접 연결 SATA, SAS 또는 NVMe 드라이브와 하나의 서버에 실제로 첨부 되는 작동 합니다. 드라이브 선택에 대한 자세한 도움말은 [드라이브 선택](choosing-drives.md) 항목을 참조하세요.

- SATA, SAS 및 NVMe M.2, U.2와 카드에서 추가 드라이브 모두 지원 됩니다.
- 512n, 512e, 및 4k 기본 드라이브 모두 지원
- 반도체 드라이브를 제공 해야 [전원 손실 방지](https://blogs.technet.microsoft.com/filecab/2016/11/18/dont-do-it-consumer-ssd/)
- 동일한 수와 모든 서버 – 드라이브 유형의 참조 [드라이브 대칭 고려 사항](drive-symmetry-considerations.md)
- 캐시 장치 32GB 여야 합니다. 크거나
- 영구 메모리 장치를 사용 하 여 캐시 장치로, NVMe SSD 용량 장치 (Hdd를 사용할 수 없음) 사용 해야 합니다.
- NVMe 드라이버는 Microsoft의 기본 또는 NVMe 드라이버를 업데이트 합니다.
- 권장: 캐시 드라이브 수가의 전체 배수가 용량 드라이브 수
- 권장: 캐시 드라이브 높은 쓰기 지속 시간과 있어야 합니다.: 3 개 이상의 드라이브 쓰기-매일 (DWPD) 또는 4tb 이상 (TBW) – 하루 기록 참조 [테라바이트 기록 (TBW) 및 최소 저장소에 대 한 권장 이해 드라이브 (DWPD) 하루 기록 공간 다이렉트](https://blogs.technet.microsoft.com/filecab/2017/08/11/understanding-dwpd-tbw/)

저장소 공간 다이렉트에 대 한 드라이브 수 연결 하는 방법을 다음과 같습니다.

- SATA 드라이브 직접 연결
- NVMe 드라이브 직접 연결
- SAS 드라이브를 사용 하 여 SAS 호스트 버스 어댑터 (HBA)
- SATA 드라이브를 사용 하 여 SAS 호스트 버스 어댑터 (HBA)
- **지원 되지 않습니다.** RAID 컨트롤러 카드 또는 SAN (파이버 채널, iSCSI, FCoE) 저장소입니다. 호스트 버스 어댑터 (HBA) 카드는 간단한 통과 모드를 구현 해야 합니다.

![지원 되는 드라이브의 다이어그램에 상호 연결](media/hardware-requirements/drive-interconnect-support-1.png)

드라이브를 서버에 내부 수 또는 꺼내서 외장 하나만 연결 된 서버. 인클로저 서비스 SES (SCSI) 슬롯 매핑 및 식별을 위한 필요합니다. 각 외부 엔클로저는 고유 식별자 (고유 ID)를 제공 해야 합니다.

- 서버에 내부 드라이브
- 드라이브를 꺼내서 외장 "JBOD (") 하나의 서버에 연결
- **지원 되지 않습니다.** 공유 SAS 엔클로저 모든 폼의 다중 경로 IO (MPIO) 드라이브 여러 경로 통해 액세스할 수 있는 여러 서버에 연결 합니다.

![지원 되는 드라이브의 다이어그램에 상호 연결](media/hardware-requirements/drive-interconnect-support-2.png)

### <a name="minimum-number-of-drives-excludes-boot-drive"></a>드라이브의 최소 수 (부팅 드라이브 제외)

- 캐시로 사용되는 드라이브가 있는 경우 서버당 최소 2개 이상이어야 함
- 용량 드라이브(캐시 이외)가 서버당 최소 4개 이상이어야 함

| 보유 드라이브 종류   | 필요한 최소 수 |
|-----------------------|-------------------------|
| 모든 영구 메모리 (동일한 모델) | 4 영구 메모리 |
| 모두 NVMe(동일한 모델) | NVMe 4개                  |
| 모두 SSD(동일한 모델)  | SSD 4개                   |
| 영구 메모리 + NVMe 또는 SSD | 영구 메모리 2 + 4 NVMe 또는 SSD |
| NVMe + SSD            | NVMe 2개 + SSD 4개          |
| NVMe + HDD            | NVMe 2개 + HDD 4개          |
| SSD + HDD             | SSD 2개 + HDD 4개           |
| NVMe + SSD + HDD      | NVMe 2개 + 기타 4개       |

   >[!NOTE]
   > 이 표에서 하드웨어 배포에 대 한 최소값을 제공합니다. Virtual machines 배포 및 가상화 된 경우에 Microsoft Azure와 같은 저장소 볼 [를 사용 하 여 저장소 공간 다이렉트 게스트 가상 컴퓨터 클러스터에서](storage-spaces-direct-in-vm.md)합니다.

### <a name="maximum-capacity"></a>최대 용량

| 최대값                | Windows Server 2019  | Windows Server 2016  |
| ---                     | ---------            | ---------            |
| 서버당 원시 용량 | 100TB               | 100TB               |
| 풀 용량           | 4 PB (4,000 TB)      | 1 PB                 |