---
title: 저장소 공간 다이렉트 하드웨어 요구 사항
ms.prod: windows-server-threshold
description: 저장소 공간 다이렉트 테스트에 대한 최소 하드웨어 요구 사항
ms.author: eldenc
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: eldenchristensen
ms.date: 04/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 84d10ab3e25500720dd13e2ba057dc3c5bf05a6f
ms.sourcegitcommit: 515b4fd5c40fcbae0e12a2c30090384533972353
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/29/2018
ms.locfileid: "8232532"
---
# 저장소 공간 다이렉트 하드웨어 요구 사항

> 적용 대상: Windows Server 2016, Windows Server Insider Preview

이 항목에서는 저장소 공간 다이렉트에 대 한 최소 하드웨어 요구 사항을 설명 합니다.

프로덕션 환경에 대 한 Microsoft 배포 도구 및 절차가 포함 하는 파트너 로부터 이러한 [Windows Server 소프트웨어 정의](https://microsoft.com/wssd) 하드웨어/소프트웨어 제품을 권장 합니다. 설계, 조립 되며 호환성 및 안정성 얻기 및 신속 하 게 실행 되도록 하는 참조 아키텍처에 대해 유효성이 검사 됩니다. 자세한 내용 [https://microsoft.com/wssd](https://microsoft.com/wssd).

![Windows Server 소프트웨어 정의 된 파트너의 로고](media/hardware-requirements/wssd-partners.png)

   > [!TIP]
   > 저장소 공간 다이렉트를 평가 하 고 싶지만 하드웨어가 없습니다? [사용 하 여 저장소 공간 다이렉트 클러스터의 게스트 가상 컴퓨터에](storage-spaces-direct-in-vm.md)설명 된 대로 Hyper-v 또는 Azure 가상 컴퓨터를 사용 합니다.

## 기본 요구 사항

시스템, 구성 요소, 장치 및 드라이버는 [Windows Server 카탈로그](https://www.windowsservercatalog.com)당 **Windows Server 2016 인증** 이어야 합니다. 또한, 서버, 드라이브, 호스트 버스 어댑터 및 네트워크 어댑터는 좋습니다 **Software-Defined 데이터 센터 (SDDC) 표준** 및/또는 **Software-Defined 데이터 센터 (SDDC) 프리미엄** 추가 자격 (AQs)과 같이 아래 합니다. SDDC AQs 1, 000 개 구성 요소가 있습니다.

![Windows Server 카탈로그 SDDC AQs를 보여 주는 스크린샷](media/hardware-requirements/sddc-aqs.png)

장애 조치 클러스터 관리자 또는 완전히 구성 된 클러스터 (서버, 네트워킹 및 저장소) 마법사 당 모든 [클러스터 유효성 검사 테스트](https://technet.microsoft.com/library/cc732035(v=ws.10).aspx) 를 통과 해야 합니다 `Test-Cluster` powershell에서 [cmdlet](https://docs.microsoft.com/powershell/module/failoverclusters/test-cluster?view=win10-ps) 입니다.

또한 다음과 같은 요구 사항이 적용 됩니다.

## 서버

- 최소 2대~최대 16대의 서버
- 모든 서버는 동일한 제조업체 및 모델 된다는 것이 좋습니다.

## CPU

- Intel Nehalem 또는 나중 호환 프로세서입니다. 또는
- AMD EPYC 또는 나중 호환 프로세서

## 메모리

- Windows Server, Vm, 및 다른 앱 이나; 워크 로드에 대 한 메모리 더하기
- 4GB의 RAM (테라바이트)의 저장소 공간 다이렉트 메타 데이터에 대 한 각 서버의 캐시 드라이브 용량 테라바이트 당

## Boot

- 어떤 [SATADOM 포함](https://cloudblogs.microsoft.com/windowsserver/2017/08/30/announcing-support-for-satadom-boot-drives-in-windows-server-2016/) 하는 Windows Server에서 지 원하는 모든 부팅 장치
- RAID 1 미러는 **필요한 아니라 부팅에 대 한 지원**
- 200GB 최소 크기 권장 사항:

## 네트워킹

최소 (에 대해 소규모 2 ~ 3 노드)
- 10 g b p s 네트워크 인터페이스
- 2-노드를 사용 하 여 직접 연결 (switchless)는 지원

권장 사항 (고성능, 배율, 또는 4 + 노드의 배포)
- NICs, 원격 직접 메모리 액세스 (RDMA) (권장) iWARP 또는 RoCE
- 중복성 및 성능을 위한 Nic를 두 개 이상의
- 25 g b p s 네트워크 인터페이스 이상

## 드라이브

저장소 공간 다이렉트 작동 직접 연결 SATA, SAS 또는 NVMe 드라이브는 단 하나의 서버에 물리적으로 연결 됩니다. 드라이브 선택에 대한 자세한 도움말은 [드라이브 선택](choosing-drives.md) 항목을 참조하세요.

- SATA, SAS 및 NVMe (M.2, U.2, 및 추가 카드) 드라이브 모두 지원
- 512n, 512e 및 4k 기본 드라이브가 모두 지원 됩니다.
- 솔리드 스테이트 드라이브 [시 보호 기능](https://blogs.technet.microsoft.com/filecab/2016/11/18/dont-do-it-consumer-ssd/) 을 제공 해야 합니다.
- 동일한 번호와 유형의 드라이브에서 모든 서버 – 참조 [드라이브 대칭 고려 사항](drive-symmetry-considerations.md)
- NVMe 드라이버는 Microsoft의 기본 또는 NVMe 드라이버를 업데이트 합니다.
- 권장 사항: 용량 드라이브 수는 캐시 드라이브 수의 배수
- 권장: 캐시 드라이브는 쓰기 내구성이 높아야: 최소한 3 드라이브-쓰기-매일 (DWPD) 또는 하루 – (TBW)를 작성 하는 4 개 이상의 테라바이트 [Understanding drive 저장소에 대 한 권장 테라바이트 기록 (TBW), 및 최소 day (DWPD), 당 쓰기 참조 공간 다이렉트](https://blogs.technet.microsoft.com/filecab/2017/08/11/understanding-dwpd-tbw/)

저장소 공간 다이렉트 용 드라이브를 연결할 수 방법을 다음과 같습니다.

1. SATA 드라이브 직접 연결
2. NVMe 드라이브 직접 연결
3. SAS 드라이브를 사용 하 여 SAS 호스트 버스 어댑터 (HBA)
4. SATA 드라이브를 사용 하 여 SAS 호스트 버스 어댑터 (HBA)
5. **지원 되지 않습니다:** RAID 컨트롤러 카드 또는 SAN (파이버 채널, iSCSI, FCoE) 저장소. 호스트 버스 어댑터 (HBA) 카드 단순 통과 모드를 구현 해야 합니다.

![지원 되는 드라이브의 다이어그램 상호 연결](media/hardware-requirements/drive-interconnect-support-1.png)

드라이브 서버에 내부 또는 외부 케이스에 단 하나의에 연결 된 서버입니다. SES SCSI 엔클로저 서비스 ()는 슬롯 매핑 및 식별 규칙이 존재 필요 합니다. 각 외부 엔클로저는 고유 식별자 (고유 ID)을 제시 해야 합니다.

1. 내부 서버에 드라이브
2. 하나의 서버에 연결 된 외부 인클로저 ("JBOD")에서 드라이브
3. **지원 되지 않습니다:** 공유 엔클로저가 포함의 IO MPIO (다중 경로) 드라이브는 여러 경로에서 액세스할 수 있는 형식 또는 여러 서버에 연결 합니다.

![지원 되는 드라이브의 다이어그램 상호 연결](media/hardware-requirements/drive-interconnect-support-2.png)

### 최소 드라이브 수 (부팅 드라이브는 제외)

- 캐시로 사용되는 드라이브가 있는 경우 서버당 최소 2개 이상이어야 함
- 용량 드라이브(캐시 이외)가 서버당 최소 4개 이상이어야 함

| 보유 드라이브 종류   | 필요한 최소 수 |
|-----------------------|-------------------------|
| 모두 NVMe(동일한 모델) | NVMe 4개                  |
| 모두 SSD(동일한 모델)  | SSD 4개                   |
| NVMe + SSD            | NVMe 2개 + SSD 4개          |
| NVMe + HDD            | NVMe 2개 + HDD 4개          |
| SSD + HDD             | SSD 2개 + HDD 4개           |
| NVMe + SSD + HDD      | NVMe 2개 + 기타 4개       |

   >[!NOTE]
   > 이 표에서 하드웨어 배포에 대 한 최소를 제공합니다. 가상 컴퓨터를 사용 하 여 배포 하 고 Microsoft azure에서 저장소와 같은 가상화 [를 사용 하 여 저장소 공간 다이렉트 게스트 가상 컴퓨터 클러스터에서](storage-spaces-direct-in-vm.md)참조 하세요.

### 최대 용량

- 서버당 최대 100 2tb (테라바이트) 원시 저장소 용량은 권장 사항:
- 최대 1 페타바이트 (1, 000 테라바이트) 원시 풀의 용량 저장소
