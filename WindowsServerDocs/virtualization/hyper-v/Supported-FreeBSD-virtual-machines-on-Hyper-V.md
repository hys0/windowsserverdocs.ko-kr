---
title: Hyper-v에서 지원 되는 FreeBSD 가상 컴퓨터
description: 각 버전에 포함 된 Linux 통합 서비스 및 기능을 나열 합니다.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 930e758f-bd50-46b4-a3a4-9857110f17b4
author: shirgall
ms.author: kathydav
ms.date: 08/30/2017
ms.openlocfilehash: 3ca1de87469c30a8cadbf047e77aff441145a499
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70869476"
---
# <a name="supported-freebsd-virtual-machines-on-hyper-v"></a>Hyper-v에서 지원 되는 FreeBSD 가상 컴퓨터

>적용 대상: Windows Server 2016, Hyper-v Server 2016, Windows Server 2012 R2, Hyper-v server 2012 R2, Windows Server 2012, Hyper-v Server 2012, Windows Server 2008 R2, Windows 10, Windows 8.1, Windows 8, Windows 7.1, Windows 7

다음과 같은 기능 배포 맵을 각 버전의 기능을 나타냅니다. 알려진된 문제 및 각 배포에 대 한 대안 표 다음에 나열 됩니다.

## <a name="table-legend"></a>표의 범례

* **기본 제공** -BIS (FreeBSD Integration Service)는이 FreeBSD 릴리스의 일부로 포함 됩니다.

* &#10004; -사용 가능한 기능

* (*빈*)-기능을 사용할 수 없음

|**기능**|**Windows Server 운영 체제 버전**|**11.1/11.2**|**11.0**|**10.3**|**10.2**|**10.0-10.1**|**9.1-9.3, 8.4**|
|-|-|-|-|-|-|-|-|
|**가용성**||기본 제공|기본 제공|기본 제공|기본 제공|기본 제공|[포트](https://svnweb.freebsd.org/ports/branches/2015Q1/emulators/hyperv-is/) |
|**[Core](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#core)**|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004; |
|Windows Server 2016 정확한 시간|2019, 2016|&#10004;||||||
|**[Lan](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#networking)**||||||||
|Jumbo 프레임|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004; 참고 3|&#10004; 참고 3|&#10004; 참고 3|&#10004; 참고 3|&#10004; 참고 3|&#10004; 참고 3|
|VLAN 태깅 및 트렁킹|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|실시간 마이그레이션|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|고정 IP 삽입|2019, 2016, 2012 R2, 2012|&#10004; 참고 4|&#10004; 참고 4|&#10004; 참고 4|&#10004; 참고 4|&#10004; 참고 4|&#10004;|
|vRSS|2019, 2016, 2012 R2|&#10004;|&#10004;|||||
|TCP 조각화 및 체크섬 오프 로드|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|||
|큰 오프 로드 (LRO)를 수신 합니다.|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;||||
|SR-IOV|2019, 2016|||||||
|**[저장할](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#storage)**||참고 1|참고 1|참고 1|참고 1|참고 1, 2|참고 1, 2|
|VHDX 크기 조정|2019, 2016, 2012 R2|&#10004; 참고 7|&#10004; 참고 7|||||
|가상 파이버 채널|2019, 2016, 2012 R2|||||||
|라이브 가상 머신 백업|2019, 2016, 2012 R2|&#10004;||||||
|TRIM 지원|2019, 2016, 2012 R2|&#10004;||||||
|SCSI WWN|2019, 2016, 2012 R2|||||||
|**[Ram](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#memory)**||||||||
|PAE 커널 지원|2019, 2016, 2012 R2, 2012, 2008 R2|||||||
|MMIO 간격 구성|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|동적 메모리-즉석 추가|2019, 2016, 2012 R2, 2012|||||||
|동적 메모리-Ballooning|2019, 2016, 2012 R2, 2012|||||||
|런타임 메모리 크기 조정|2019, 2016|||||||
|**[화면이](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#video)**||||||||
|Hyper-v 특정 비디오 장치|2019, 2016, 2012 R2, 2012, 2008 R2|||||||
|**[기타](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#miscellaneous)**||||||||
|키/값 쌍|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;참고 6|&#10004; 참고 5, 6|&#10004;참고 6|
|마스크 불가능 인터럽트|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|호스트에서 게스트로 파일 복사|2019, 2016, 2012 R2|||||||
|lsvmbus 명령|2019, 2016, 2012 R2, 2012, 2008 R2|||||||
|Hyper-v 소켓|2019, 2016|||||||
|PCI 통과/DDA|2019, 2016|&#10004;||||||
|**[2 세대 가상 컴퓨터](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#generation-2-virtual-machines)**||||||||
|UEFI를 사용 하 여 부팅|2019, 2016, 2012 R2|&#10004;||||||
|보안 부팅|2019, 2016|||||||

## <a name="BKMK_notes"></a>메모란

1. 시작 하는 동안 루트 탑재 오류를 방지 하기 위해 [디스크 장치에 레이블을]( https://www.freebsd.org/doc/handbook/geom-glabel.html) 알려 제안 합니다.

2. 다음 명령을 통해 레거시 ATA 드라이버를 사용 하도록 설정 하지 않으면 BIS 드라이버가 FreeBSD 및 4.x에 로드 되 면 가상 DVD 드라이브가 인식 되지 않을 수 있습니다.
    ```sh
    # echo ‘hw.ata.disk_enable=1' >> /boot/loader.conf
    # shutdown -r now
    ```

3. 9126는 지원 되는 최대 MTU 크기입니다.

4. 장애 조치 시나리오에서 복제 서버에서 정적 IPv6 주소를 설정할 수 없습니다. IPv4 주소를 대신 사용 합니다.

5. KVP는 FreeBSD 10.0의 포트에서 제공 됩니다. 자세한 내용은 FreeBSD.org의 [FreeBSD 10.0 ports](https://svnweb.freebsd.org/ports/branches/2015Q1/emulators/hyperv-is/) 를 참조 하세요.

6. KVP은 Windows Server 2008 r 2에서 작동 하지 않을 수 있습니다.

7. FreeBSD 11.0에서 VHDX 온라인 크기 조정이 제대로 작동 하도록 하려면 11.0 이상에서 고정 된 형상 버그를 해결 하기 위해 특별 한 수동 단계가 필요 합니다. 호스트에서 VHDX 디스크의 크기를 조정한 후 디스크를 쓰기용으로 열고 "gpart recover"를 다음과 같이 실행 합니다.
    ```sh
    # dd if=/dev/da1 of=/dev/da1 count=0
    # gpart recover da1
    ```
   **추가 참고 사항**: 안정적이 고 기병의 기능 행렬은 FreeBSD 11.1 릴리스와 동일 합니다. 또한 FreeBSD 10.2 및 이전 버전 (10.1, 10.0, 4.x, .x)은 수명이 종료 됩니다. 지원 되는 릴리스 및 최신 보안 권고의 최신 목록을 [보려면 여기](https://security.freebsd.org/) 를 참조 하세요.

**추가 참고 사항**: 안정적이 고 기병의 기능 행렬은 FreeBSD 11.1 릴리스와 동일 합니다. 또한 FreeBSD 10.2 및 이전 버전 (10.1, 10.0, 4.x, .x)은 수명이 종료 됩니다. 지원 되는 릴리스 및 최신 보안 권고의 최신 목록을 [보려면 여기](https://security.freebsd.org/) 를 참조 하세요.

## <a name="see-also"></a>관련 항목

* [Hyper-v의 Linux 및 FreeBSD 가상 머신에 대 한 기능 설명](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md)
* [Hyper-v에서 FreeBSD 실행에 대 한 모범 사례](Best-practices-for-running-FreeBSD-on-Hyper-V.md)
