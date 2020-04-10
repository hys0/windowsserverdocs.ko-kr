---
title: Hyper-v에서 지원 되는 Debian 가상 컴퓨터
description: 각 버전에 포함 된 Linux 통합 서비스 및 기능을 나열 합니다.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.topic: article
ms.assetid: 3cc62c10-02a3-4633-960c-23bf91a45bd5
author: shirgall
ms.author: kathydav
ms.date: 04/07/2020
ms.openlocfilehash: e5483b9547e67414bd66b3daad1a4b07c3cb7cfc
ms.sourcegitcommit: 7b1ebc4934998af2472962ca8cce1c872f39946f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/09/2020
ms.locfileid: "80994510"
---
# <a name="supported-debian-virtual-machines-on-hyper-v"></a>Hyper-v에서 지원 되는 Debian 가상 컴퓨터

>적용 대상: Windows Server 2019, Hyper-v Server 2019, Windows Server 2016, Hyper-v Server 2016, Windows Server 2012 R2, Hyper-v Server 2012 R2, Windows 10, Windows 8.1

다음과 같은 기능 배포 맵을 각 버전에 존재 하는 기능을 나타냅니다. 알려진된 문제 및 각 배포에 대 한 대안 표 다음에 나열 됩니다.

## <a name="table-legend"></a>표의 범례

* **기본 제공** -LIS이 Linux 배포판의 일부로 포함 됩니다. Microsoft에서 제공한 LIS 다운로드 패키지는 모듈을 설치 하지 않으면이 배포에 대해 작동 하지 않습니다. LIS에서 기본 제공에 대 한 커널 모듈 버전 번호 (볼 수 있듯이 **lsmod**, 예를 들어)는 Microsoft에서 제공한 LIS 다운로드 패키지에 버전 번호가 다릅니다. 불일치가는 LIS에서 작성 된 지 오래 된 나타내지 않습니다.

* &#10004; -사용 가능한 기능

* (*빈*)-기능을 사용할 수 없음

| **기능과**                                                                                                                                  | **Windows Server 운영 체제 버전** | **10.0-10.3 (buster)** | **9.0-9.12 (스트레치)** | **8.0-8.11 (jessie)** | **7.0-7.11 (wheezy)** |
|----------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------|-----------------------|-----------------------|-----------------------|-----------------------|
| **가용성**                                                                                                                             |                                             | 기본 제공              | 기본 제공              | 기본 제공              | 기본 제공 (참고 5)     |
| **[Core](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#core)**                                                   | 2019, 2016, 2012 R2          | &#10004;              | &#10004;              | &#10004;              | &#10004;              |
| Windows Server 2016 정확한 시간                                                                                                            | 2019, 2016                                  | &#10004; 참고 4       | &#10004; 참고 4       |                       |                       |
| **[Lan](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#networking)**                                       |                                             |                       |                       |                       |                       |
| Jumbo 프레임                                                                                                                                 | 2019, 2016, 2012 R2          | &#10004;              | &#10004;              | &#10004;              | &#10004;              |
| VLAN 태깅 및 트렁킹                                                                                                                    | 2019, 2016, 2012 R2          | &#10004;              | &#10004;              | &#10004;              | &#10004;              |
| 실시간 마이그레이션                                                                                                                               | 2019, 2016, 2012 R2          | &#10004;              | &#10004;              | &#10004;              | &#10004;              |
| 고정 IP 삽입                                                                                                                          | 2019, 2016, 2012 R2                   |                       |                       |                       |                       |
| vRSS                                                                                                                                         | 2019, 2016, 2012 R2                         | &#10004; 참고 4       | &#10004; 참고 4       |                       |                       |
| TCP 조각화 및 체크섬 오프 로드                                                                                                       | 2019, 2016, 2012 R2          | &#10004; 참고 4       | &#10004; 참고 4       |                       |                       |
| SR-IOV                                                                                                                                       | 2019, 2016                                  | &#10004; 참고 4       | &#10004; 참고 4       |                       |                       |
| **[저장할](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#storage)**                                             |                                             |                       |                       |                       |                       |
| VHDX 크기 조정                                                                                                                                  | 2019, 2016, 2012 R2                         | &#10004; 참고 1       | &#10004; 참고 1       | &#10004; 참고 1       | &#10004; 참고 1       |
| 가상 파이버 채널                                                                                                                        | 2019, 2016, 2012 R2                         |                       |                       |                       |                       |
| 라이브 가상 머신 백업                                                                                                                  | 2019, 2016, 2012 R2                         | &#10004;Note2 | &#10004;Note2 | &#10004;Note2 | &#10004;Note2 |
| TRIM 지원                                                                                                                                 | 2019, 2016, 2012 R2                         | &#10004; 참고 4       | &#10004; 참고 4       |                       |                       |
| SCSI WWN                                                                                                                                     | 2019, 2016, 2012 R2                         | &#10004; 참고 4       | &#10004; 참고 4       |                       |                       |
| **[Ram](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#memory)**                                               |                                             |                       |                       |                       |                       |
| PAE 커널 지원                                                                                                                           | 2019, 2016, 2012 R2          | &#10004;              | &#10004;              | &#10004;              | &#10004;              |
| MMIO 간격 구성                                                                                                                    | 2019, 2016, 2012 R2                         | &#10004;              | &#10004;              | &#10004;              | &#10004;              |
| 동적 메모리-즉석 추가                                                                                                                     | 2019, 2016, 2012 R2                   | &#10004; 참고 4       | &#10004; 참고 4       |                       |                       |
| 동적 메모리-Ballooning                                                                                                                  | 2019, 2016, 2012 R2                   | &#10004; 참고 4       | &#10004; 참고 4       |                       |                       |
| 런타임 메모리 크기 조정                                                                                                                        | 2019, 2016                                  | &#10004; 참고 4       | &#10004; 참고 4       |                       |                       |
| **[화면이](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#video)**                                                 |                                             |                       |                       |                       |                       |
| Hyper-v 관련 비디오 장치                                                                                                                | 2019, 2016, 2012 R2          | &#10004;              | &#10004;              | &#10004;              |                       |
| **[기타](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#miscellaneous)**                                 |                                             |                       |                       |                       |                       |
| 키-값 쌍                                                                                                                               | 2019, 2016, 2012 R2          | &#10004; 참고 2       | &#10004; 참고 2       | &#10004; 참고 2       |                       |
| 마스크 불가능 인터럽트                                                                                                                       | 2019, 2016, 2012 R2                         | &#10004;              | &#10004;              | &#10004;              |                       |
| 호스트에서 게스트로 파일 복사                                                                                                                 | 2019, 2016, 2012 R2                         | &#10004; 참고 2       | &#10004; 참고 2       | &#10004; 참고 2       |                       |
| lsvmbus 명령                                                                                                                              | 2019, 2016, 2012 R2          |                       |                       |                       |                       |
| Hyper-v 소켓                                                                                                                              | 2019, 2016                                  | &#10004; 참고 4       | &#10004; 참고 4       |                       |                       |
| PCI 통과/DDA                                                                                                                          | 2019, 2016                                  | &#10004; 참고 4       | &#10004; 참고 4       |                       |                       |
| **[2 세대 가상 컴퓨터](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#generation-2-virtual-machines)** |                                             |                       |                       |                       |                       |
| UEFI를 사용 하 여 부팅                                                                                                                              | 2019, 2016, 2012 R2                         | &#10004; 참고 3       | &#10004; 참고 3       | &#10004; 참고 3       |                       |
| 보안 부팅                                                                                                                                  | 2019, 2016                                  | &#10004;              |                       |                       |                       |


## <a name="notes"></a>참고

1. 파일 시스템을 2TB 보다 큰 Vhd에 만들 수 없습니다.

2. 키-값 쌍, fcopy, 및 VSS 데몬 Debian 8.3는 Debian 패키지를 수동으로 설치 된 "hyperv-데몬"부터 포함 되어 있습니다. Debian 7.x 및 8.0 8.2 hyperv 데몬 패키지에서 가져와야 [Debian backports](https://wiki.debian.org/Backports)합니다.

3. Windows Server 2012 R2 2 세대 가상 컴퓨터에는 기본적으로 보안 부팅이 사용 하도록 설정 되어 있으며 보안 부팅 옵션을 사용 하지 않는 경우 일부 Linux 가상 컴퓨터는 부팅 되지 않습니다. 보안 부팅을 사용하지 않도록 설정할 수는 **펌웨어** 섹션에 있는 가상 머신에 대한 설정의 **Hyper-v 관리자** Powershell을 사용하여 비활성화할 수 있습니다.

   ```Powershell
   Set-VMFirmware -VMName "VMname" -EnableSecureBoot Off
   ```
4. 최신 업스트림 커널 기능은 커널에 포함 된 [Debian backports](https://wiki.debian.org/Backports)를 사용 하는 경우에만 사용할 수 있습니다.

5. Debian 4.x는 지원 하지 않으며 이전 커널을 사용 하지만 Debian 4.x 용 Debian backports에 포함 된 커널에는 Hyper-v 기능이 향상 되었습니다.

관련 항목

* [Hyper-v에서 지원 되는 CentOS 및 Red Hat Enterprise Linux 가상 컴퓨터](Supported-CentOS-and-Red-Hat-Enterprise-Linux-virtual-machines-on-Hyper-V.md)

* [Hyper-v에서 지원 되는 Oracle Linux 가상 컴퓨터](Supported-Oracle-Linux-virtual-machines-on-Hyper-V.md)

* [Hyper-v에서 지원 되는 SUSE 가상 컴퓨터](Supported-SUSE-virtual-machines-on-Hyper-V.md)

* [Hyper-v에서 지원 되는 Ubuntu 가상 머신](Supported-Ubuntu-virtual-machines-on-Hyper-V.md)

* [Hyper-v에서 지원 되는 FreeBSD 가상 컴퓨터](Supported-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Hyper-v의 Linux 및 FreeBSD 가상 머신에 대 한 기능 설명](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Hyper-v에서 Linux를 실행 하기 위한 모범 사례](Best-Practices-for-running-Linux-on-Hyper-V.md)
