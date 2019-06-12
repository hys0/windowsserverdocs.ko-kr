---
title: Hyper-v에서 지원 되는 FreeBSD 가상 컴퓨터
description: Linux integration services 및 각 버전에 포함 된 기능을 나열 합니다.
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
ms.openlocfilehash: f11ef246ce4ac4f8773f046a25badd83cff106d0
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447728"
---
# <a name="supported-freebsd-virtual-machines-on-hyper-v"></a>Hyper-v에서 지원 되는 FreeBSD 가상 컴퓨터

>적용 대상: Windows Server 2016에서 Hyper-v Server 2016, Windows Server 2012 R2, Hyper-V Server 2012 R2, Windows Server 2012 Hyper-V Server 2012, Windows Server 2008 R2, Windows 10, Windows 8.1, Windows 8, Windows 7.1, Windows 7

다음과 같은 기능 배포 맵을 각 버전의 기능을 나타냅니다. 알려진된 문제 및 각 배포에 대 한 대안 표 다음에 나열 됩니다.

## <a name="table-legend"></a>표의 범례

* **기본 제공** -(FreeBSD Integration Service) BIS이 FreeBSD 릴리스의 일부로 포함 됩니다.

* &#10004; -사용 가능한 기능

* (*빈*)-기능을 사용할 수 없음

|**기능**|**Windows Server 운영 체제 버전**|**11.1/11.2**|**11.0**|**10.3**|**10.2**|**10.0 - 10.1**|**9.1 - 9.3, 8.4**|
|-|-|-|-|-|-|-|-|
|**가용성**||기본 제공|기본 제공|기본 제공|기본 제공|기본 제공|[포트](https://svnweb.freebsd.org/ports/branches/2015Q1/emulators/hyperv-is/) |
|**[Core](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#core)**|2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004; |
|Windows Server 2016 정확한 시간|2016|&#10004;||||||
|**[Networking](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#networking)**||||||||
|Jumbo 프레임|2016, 2012 R2, 2012, 2008 R2|&#10004; 참고 3|&#10004; 참고 3|&#10004; 참고 3|&#10004; 참고 3|&#10004; 참고 3|&#10004; 참고 3|
|VLAN 태깅, 트렁킹|2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|실시간 마이그레이션|2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|정적 IP 주입|2016, 2012 R2, 2012|&#10004; 참고 4|&#10004; 참고 4|&#10004; 참고 4|&#10004; 참고 4|&#10004; 참고 4|&#10004;|
|vRSS|2016, 2012 R2|&#10004;|&#10004;|||||
|TCP 조각화와 체크섬 오프 로드|2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|||
|큰 오프 로드 (LRO)를 수신 합니다.|2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;||||
|SR-IOV|2016|||||||
|**[Storage](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#storage)**||참고 1|참고 1|참고 1|참고 1|참고 1, 2|참고 1, 2|
|VHDX 크기 조정|2016, 2012 R2|&#10004; 참고 7|&#10004; 참고 7|||||
|가상 파이버 채널|2016, 2012 R2|||||||
|가상 머신 백업|2016, 2012 R2|&#10004;||||||
|TRIM 지원|2016, 2012 R2|&#10004;||||||
|SCSI WWN|2016, 2012 R2|||||||
|**[Memory](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#memory)**||||||||
|PAE 커널 지원|2016, 2012 R2, 2012, 2008 R2|||||||
|MMIO 간격 구성|2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|동적 메모리-즉석 추가|2016, 2012 R2, 2012|||||||
|동적 메모리-Ballooning|2016, 2012 R2, 2012|||||||
|런타임 메모리 크기 조정|2016|||||||
|**[Video](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#video)**||||||||
|Hyper-v 특정 비디오 장치|2016, 2012 R2, 2012, 2008 R2|||||||
|**[기타](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#miscellaneous)**||||||||
|키/값 쌍|2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;참고 6|&#10004; 참고 5, 6|&#10004;참고 6|
|마스크 불가능 인터럽트|2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|호스트에서 게스트로 파일 복사|2016, 2012 R2|||||||
|lsvmbus 명령|2016, 2012 R2, 2012, 2008 R2|||||||
|Hyper-v 소켓|2016|||||||
|PCI 통과/DDA|2016|&#10004;||||||
|**[2 세대 가상 컴퓨터](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#generation-2-virtual-machines)**||||||||
|UEFI를 사용 하 여 부팅|2016, 2012 R2|&#10004;||||||
|보안 부팅|2016|||||||

## <a name="BKMK_notes"></a>참고 사항

1. 에 대 한 제안 [레이블을 디스크 장치]( https://www.freebsd.org/doc/handbook/geom-glabel.html) 시작 하는 동안 루트 탑재 오류를 방지 하려면.

2. 가상 DVD 드라이브 BIS 드라이버가 FreeBSD에서 로드 될 때 인식 하지 못하는 8.x 및 9.x 명령을 통해 레거시 ATA 드라이버를 사용 하지 않으면.
    ```sh
    # echo ‘hw.ata.disk_enable=1’ >> /boot/loader.conf
    # shutdown -r now
    ```

3. 9126는 지원 되는 최대 MTU 크기입니다.

4. 장애 조치 시나리오에서 복제 서버에서 정적 IPv6 주소를 설정할 수 없습니다. IPv4 주소를 대신 사용 합니다.

5. KVP 포트 FreeBSD 10.0에 의해 제공 됩니다. 참조 된 [FreeBSD 10.0 포트](https://svnweb.freebsd.org/ports/branches/2015Q1/emulators/hyperv-is/) 대 한 자세한 내용은 freebsd.org에 있습니다.

6. KVP은 Windows Server 2008 r 2에서 작동 하지 않을 수 있습니다.

7. VHDX 온라인 크기 조정 작업을 제대로 FreeBSD 11.0에 특별 한 수동 단계는 호스트의 VHDX 디스크 크기를 조정 후 11.0 +에서 고정 된 트림 버그 해결-디스크 쓰기에 대 한 열고 실행 하려면 다음과 같이 "recover gpart" 필요 합니다.
    ```sh
    # dd if=/dev/da1 of=/dev/da1 count=0
    # gpart recover da1
    ```
   **추가 참고 사항**: 10 안정적이 고 11 안정적인의 기능 행렬은 FreeBSD 11.1 릴리스를 사용 하 여 동일 합니다. 또한, FreeBSD 10.2 및 이전 버전 (10.1, 10.0, 9.x, 8.x) 수명 종료 됩니다. 참조 하세요 [여기](https://security.freebsd.org/) 최신 목록은 지원 되는 버전 및 최신 보안 권고 합니다.

**추가 참고 사항**: 10 안정적이 고 11 안정적인의 기능 행렬은 FreeBSD 11.1 릴리스를 사용 하 여 동일 합니다. 또한, FreeBSD 10.2 및 이전 버전 (10.1, 10.0, 9.x, 8.x) 수명 종료 됩니다. 참조 하세요 [여기](https://security.freebsd.org/) 최신 목록은 지원 되는 버전 및 최신 보안 권고 합니다.

## <a name="see-also"></a>관련 항목

* [Hyper-v의 Linux 및 FreeBSD 가상 컴퓨터에 대 한 설명이](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md)
* [Hyper-v에 FreeBSD를 실행 하는 것에 대 한 모범 사례](Best-practices-for-running-FreeBSD-on-Hyper-V.md)
