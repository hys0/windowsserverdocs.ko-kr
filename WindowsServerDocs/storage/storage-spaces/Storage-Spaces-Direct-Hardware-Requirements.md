---
title: 저장소 공간 다이렉트 하드웨어 요구 사항
ms.prod: windows-server
description: 저장소 공간 다이렉트 테스트에 대한 최소 하드웨어 요구 사항
ms.author: eldenc
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: eldenchristensen
ms.date: 08/05/2019
ms.localizationpriority: medium
ms.openlocfilehash: 63a7152ec6abb318a096ac321ae7ccfaaef4d199
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402936"
---
# <a name="storage-spaces-direct-hardware-requirements"></a>저장소 공간 다이렉트 하드웨어 요구 사항

> 적용 대상: Windows Server 2019, Windows Server 2016

이 항목에서는 스토리지 공간 다이렉트에 대 한 최소 하드웨어 요구 사항에 대해 설명 합니다.

프로덕션의 경우 Microsoft는 배포 도구 및 절차를 비롯 한 파트너의 검증 된 하드웨어/소프트웨어 솔루션을 구입 하는 것이 좋습니다. 이러한 솔루션은 호환성 및 안정성을 보장 하기 위해 참조 아키텍처에 대해 설계, 조합 및 유효성 검사를 수행 하므로 신속 하 게 시작 하 고 실행할 수 있습니다. Windows Server 2019 솔루션은 [AZURE STACK HCI solutions 웹 사이트](https://azure.microsoft.com/overview/azure-stack/hci)를 참조 하세요. Windows Server 2016 솔루션에 대 한 자세한 내용은 [Windows Server 소프트웨어 정의](https://microsoft.com/wssd)를 자세히 알아보세요.

   > [!TIP]
   > 스토리지 공간 다이렉트를 평가 하 고 하드웨어는 없는 경우 [게스트 가상 컴퓨터 클러스터에서 스토리지 공간 다이렉트 사용](storage-spaces-direct-in-vm.md)에 설명 된 대로 Hyper-v 또는 Azure virtual machines를 사용 합니다.

## <a name="base-requirements"></a>기본 요구 사항

시스템, 구성 요소, 장치 및 드라이버는 [Windows Server 카탈로그](https://www.windowsservercatalog.com)를 기준으로 **Windows server 2016 인증** 되어야 합니다. 또한 서버, 드라이브, 호스트 버스 어댑터 및 네트워크 어댑터에는 아래 그림과 같이 **소프트웨어 정의 데이터 센터 (sddc) 표준** 및/또는 **소프트웨어 정의 데이터 센터 (sddc) 프리미엄 추가 AQs (소프트웨어 정의 데이터 센터** )가 있는 것이 좋습니다. 표에서. SDDC AQs이 포함 된 1000 개 이상의 구성 요소가 있습니다.

![SDDC AQs을 보여 주는 Windows Server 카탈로그의 스크린샷](media/hardware-requirements/sddc-aqs.png)

완전히 구성 된 클러스터 (서버, 네트워킹 및 저장소)는 장애 조치(Failover) 클러스터 관리자에서 마법사 당 모든 [클러스터 유효성 검사 테스트](https://technet.microsoft.com/library/cc732035(v=ws.10).aspx) 를 통과 하거나 PowerShell에서 `Test-Cluster` [cmdlet](https://docs.microsoft.com/powershell/module/failoverclusters/test-cluster?view=win10-ps) 을 사용 해야 합니다.

또한 다음과 같은 요구 사항이 적용 됩니다.

## <a name="servers"></a>서버

- 최소 2대~최대 16대의 서버
- 모든 서버를 제조업체 및 모델로 동일 하 게 하는 것이 좋습니다.

## <a name="cpu"></a>CPU

- Intel Nehalem 이상 호환 프로세서 디스크나
- AMD EPYC 이상 호환 프로세서

## <a name="memory"></a>메모리

- Windows Server, Vm 및 기타 앱 또는 워크 로드에 대 한 메모리 항목과
- 스토리지 공간 다이렉트 메타 데이터의 경우 각 서버에서 캐시 드라이브 용량의 1tb (테라바이트) 당 4gb RAM

## <a name="boot"></a>Boot

- [이제 SATADOM을 포함](https://cloudblogs.microsoft.com/windowsserver/2017/08/30/announcing-support-for-satadom-boot-drives-in-windows-server-2016/) 하는 Windows Server에서 지원 되는 부팅 장치
- RAID 1 미러가 필요 **하지** 않지만 부팅에 대해 지원 됩니다.
- 권장: 200 GB의 최소 크기

## <a name="networking"></a>네트워킹

스토리지 공간 다이렉트에는 각 노드 간에 안정적이 고 대기 시간이 짧은 네트워크 연결이 필요 합니다.  

작은 규모 2-3 노드에 대 한 최소 상호 연결
- 10gbps NIC (네트워크 인터페이스 카드) 이상
- 중복 및 성능을 위해 각 노드에서 두 개 이상의 네트워크 연결이 권장 됩니다.

고성능, 규모 확장 또는 4 +의 배포에 권장 되는 상호 연결 
- RDMA (원격 직접 메모리 액세스)를 지 원하는 Nic (iWARP (권장) 또는 RoCE)
- 중복 및 성능을 위해 각 노드에서 두 개 이상의 네트워크 연결이 권장 됩니다.
- 25gbps NIC 이상

스위치 또는 switchless 노드 상호 간의 상호 교환
- 켜져 네트워크 스위치는 대역폭 및 네트워킹 유형을 처리 하도록 적절히 구성 되어야 합니다.  RoCE 프로토콜을 구현 하는 RDMA를 사용 하는 경우 네트워크 장치 및 스위치 구성이 훨씬 더 중요 합니다. 
- Switchless: 직접 연결을 사용 하 여 노드를 상호 연결 하 여 스위치를 사용 하지 않을 수 있습니다.  모든 노드에서 클러스터의 다른 모든 노드에 직접 연결 해야 합니다.


## <a name="drives"></a>드라이브

스토리지 공간 다이렉트는 각각 하나의 서버에 물리적으로 연결 된 직접 연결 된 SATA, SAS 또는 NVMe 드라이브와 함께 작동 합니다. 드라이브 선택에 대한 자세한 도움말은 [드라이브 선택](choosing-drives.md) 항목을 참조하세요.

- SATA, SAS 및 NVMe (M. 2, U. 2, 추가 카드) 드라이브가 모두 지원 됩니다.
- 512n, 512n 및 4K 기본 드라이브가 모두 지원 됩니다.
- 반도체 드라이브는 [전원 손실 방지 기능을](https://blogs.technet.microsoft.com/filecab/2016/11/18/dont-do-it-consumer-ssd/) 제공 해야 합니다.
- 모든 서버에서 드라이브의 수와 유형이 동일 합니다. [드라이브 대칭 고려 사항을](drive-symmetry-considerations.md) 참조 하세요.
- 캐시 장치는 32 GB 이상 이어야 합니다.
- 영구적 메모리 장치를 캐시 장치로 사용할 경우에는 NVMe 또는 SSD 용량 장치 (Hdd를 사용할 수 없음)를 사용 해야 합니다.
- NVMe 드라이버는 Microsoft에서 제공 하는 Windows에 포함 되어 있습니다. (stornvme. sys)
- 권장: 용량 드라이브 수는 캐시 드라이브 수의 전체 배수입니다.
- 권장: 캐시 드라이브에는 높은 쓰기 endurance 있어야 합니다. 즉, 하루에 3 개 이상의 드라이브 쓰기 (DWPD) 또는 최소 4tb 쓰기 (TBW)를 수행 해야 합니다. [에 대 스토리지 공간 다이렉트 한 드라이브 쓰기 (DWPD), 테라바이트 기록 (TBW) 및 최소 권장 사항 이해를 참조 하세요. ](https://blogs.technet.microsoft.com/filecab/2017/08/11/understanding-dwpd-tbw/)

스토리지 공간 다이렉트에 대 한 드라이브를 연결 하는 방법은 다음과 같습니다.

- 직접 연결 된 SATA 드라이브
- 직접 연결 된 NVMe 드라이브
- Sas 드라이브를 사용 하는 SAS 호스트 버스 어댑터 (HBA)
- SATA 드라이브를 사용 하는 SAS 호스트 버스 어댑터 (HBA)
- **지원 되지 않음:** RAID 컨트롤러 카드나 SAN (파이버 채널, iSCSI, FCoE) 저장소. HBA (호스트 버스 어댑터) 카드는 간단한 통과 모드를 구현 해야 합니다.

![지원 되는 드라이브 상호 간의 다이어그램](media/hardware-requirements/drive-interconnect-support-1.png)

드라이브는 단일 서버에만 연결 된 외부 인클로저 또는 서버에 대 한 내부 일 수 있습니다. 슬롯 매핑 및 식별에는 SES (SCSI 엔클로저 서비스)가 필요 합니다. 각 외부 인클로저는 고유 ID를 제공 해야 합니다.

- 서버 내부 드라이브
- 하나의 서버에 연결 된 외부 인클로저 ("JBOD")의 드라이브
- **지원 되지 않음:** 여러 경로에서 드라이브에 액세스할 수 있는 여러 서버 또는 모든 형태의 MPIO (다중 경로 IO)에 연결 된 공유 SAS 인클로저.

![지원 되는 드라이브 상호 간의 다이어그램](media/hardware-requirements/drive-interconnect-support-2.png)

### <a name="minimum-number-of-drives-excludes-boot-drive"></a>최소 드라이브 수 (부팅 드라이브 제외)

- 캐시로 사용되는 드라이브가 있는 경우 서버당 최소 2개 이상이어야 함
- 용량 드라이브(캐시 이외)가 서버당 최소 4개 이상이어야 함

| 보유 드라이브 종류   | 필요한 최소 수 |
|-----------------------|-------------------------|
| 모든 영구 메모리 (동일한 모델) | 영구적 메모리 4 개 |
| 모두 NVMe(동일한 모델) | NVMe 4개                  |
| 모두 SSD(동일한 모델)  | SSD 4개                   |
| 영구적 메모리 + NVMe 또는 SSD | 2 영구 메모리 + 4 NVMe 또는 SSD |
| NVMe + SSD            | NVMe 2개 + SSD 4개          |
| NVMe + HDD            | NVMe 2개 + HDD 4개          |
| SSD + HDD             | SSD 2개 + HDD 4개           |
| NVMe + SSD + HDD      | NVMe 2개 + 기타 4개       |

   >[!NOTE]
   > 이 표에서는 최소 하드웨어 배포를 제공 합니다. Microsoft Azure와 같이 가상 컴퓨터 및 가상화 된 저장소를 사용 하 여 배포 하는 경우 [게스트 가상 컴퓨터 클러스터에서 스토리지 공간 다이렉트 사용](storage-spaces-direct-in-vm.md)을 참조 하세요.

### <a name="maximum-capacity"></a>최대 용량

| 최대값                | Windows Server 2019  | Windows Server 2016  |
| ---                     | ---------            | ---------            |
| 서버당 원시 용량 | 400 TB               | 100 TB               |
| 풀 용량           | 4 PB (4000 TB)      | 1 PB                 |
