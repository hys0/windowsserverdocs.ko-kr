---
title: Hyper-v에서 지원 되는 Debian 가상 컴퓨터
description: Linux integration services 및 각 버전에 포함 된 기능을 나열 합니다.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3cc62c10-02a3-4633-960c-23bf91a45bd5
author: shirgall
ms.author: kathydav
ms.date: 10/03/2016
ms.openlocfilehash: 6ec089f501a0999a4460501dbc4d03428d36af40
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59863834"
---
# <a name="supported-debian-virtual-machines-on-hyper-v"></a>Hyper-v에서 지원 되는 Debian 가상 컴퓨터

>적용 대상: Windows Server 2016에서 Hyper-v Server 2016, Windows Server 2012 R2, Hyper-V Server 2012 R2, Windows Server 2012 Hyper-V Server 2012, Windows Server 2008 R2, Windows 10, Windows 8.1, Windows 8, Windows 7.1, Windows 7

다음과 같은 기능 배포 맵을 각 버전에 존재 하는 기능을 나타냅니다. 알려진된 문제 및 각 배포에 대 한 대안 표 다음에 나열 됩니다.

## <a name="table-legend"></a>표의 범례

* **기본 제공** -LIS이 Linux 배포판의 일부로 포함 됩니다. Microsoft에서 제공한 LIS 다운로드 패키지는 모듈을 설치 하지 않으면이 배포에 대해 작동 하지 않습니다. LIS에서 기본 제공에 대 한 커널 모듈 버전 번호 (볼 수 있듯이 **lsmod**, 예를 들어)는 Microsoft에서 제공한 LIS 다운로드 패키지에 버전 번호가 다릅니다. 불일치가는 LIS에서 작성 된 지 오래 된 나타내지 않습니다.

* &#10004; -사용 가능한 기능

* (*빈*)-기능을 사용할 수 없음

|**기능**|**Windows Server 운영 체제 버전**|**9.0-9.6 (stretch)**|**8.0-8.11 (jessie)**|**7.0 7.11 (wheezy)**|
|-|-|-|-|-|
|**가용성**||기본 제공|기본 제공|(참고 6)에 기본 제공|
|**[Core](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_core)**|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|
|Windows Server 2016 정확한 시간|2019, 2016|&#10004;참고 8||
|**[Networking](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_Networking)**|
|Jumbo 프레임|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|
|VLAN 태깅, 트렁킹|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|
|실시간 마이그레이션|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|
|정적 IP 주입|2019, 2016, 2012 R2, 2012|||
|vRSS|2019, 2016, 2012 R2|&#10004;참고 8|||
|TCP 조각화와 체크섬 오프 로드|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;참고 8|||
|SR-IOV|2019, 2016|&#10004;참고 8||
|**[Storage](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_Storage)**|
|VHDX 크기 조정|2019, 2016, 2012 R2|&#10004; 참고 1|&#10004; 참고 1|&#10004; 참고 1|
|가상 파이버 채널|2019, 2016, 2012 R2|||
|가상 머신 백업|2019, 2016, 2012 R2|&#10004; 참고 4, 5|&#10004; 참고 4, 5|&#10004; 참고 4|
|TRIM 지원|2019, 2016, 2012 R2|&#10004;참고 8|||
|SCSI WWN|2019, 2016, 2012 R2|&#10004;참고 8||
|**[Memory](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_Memory)**|
|PAE 커널 지원|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|
|MMIO 간격 구성|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|
|동적 메모리-즉석 추가|2019, 2016, 2012 R2, 2012|&#10004;참고 8|||
|동적 메모리-Ballooning|2019, 2016, 2012 R2, 2012|&#10004;참고 8|||
|런타임 메모리 크기 조정|2019, 2016|&#10004;참고 8|||
|**[Video](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_Video)**|
|하이퍼-V-특정 비디오 장치|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;||
|**[기타](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_Misc)**|
|키-값 쌍|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004; 참고 4|&#10004; 참고 4||
|마스크 불가능 인터럽트|2019, 2016, 2012 R2|&#10004;|&#10004;|
|호스트에서 게스트로 파일 복사|2019, 2016, 2012 R2|&#10004; 참고 4|&#10004; 참고 4||
|lsvmbus 명령|2019, 2016, 2012 R2, 2012, 2008 R2|||
|Hyper-v 소켓|2019, 2016|&#10004;참고 8|||
|PCI 통과/DDA|2019, 2016|&#10004;참고 8|||
|**[2 세대 가상 컴퓨터](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_gen2)**|
|UEFI를 사용 하 여 부팅|2019, 2016, 2012 R2|&#10004; 참고 7|&#10004; 참고 7||
|보안 부팅|2019, 2016|||

## <a name="BKMK_notes"></a>참고 사항

1. 파일 시스템을 2TB 보다 큰 Vhd에 만들 수 없습니다.

2. Windows Server 2008 R2 SCSI 디스크 8 가지 항목에 만듭니다/개발/sd *입니다.

3. Windows Server 2012 r 2의 VM 코어 8 개 이상의 단일 vCPU로 라우팅되는 모든 인터럽트를 해야 합니다.

4. 키-값 쌍, fcopy, 및 VSS 데몬 Debian 8.3는 Debian 패키지를 수동으로 설치 된 "hyperv-데몬"부터 포함 되어 있습니다. Debian 7.x 및 8.0 8.2 hyperv 데몬 패키지에서 가져와야 [Debian backports](https://wiki.debian.org/Backports)합니다.

5. 가상 컴퓨터 백업 ext2 파일 시스템으로 작동 하지 않습니다. 이 파일 시스템 유형을 만들지 않도록 레이아웃 사용자 지정 해야, Debian 설치 프로그램에서 만든 기본 레이아웃 ext2 파일 시스템을 포함 합니다.

6. 커널에 포함 된 Debian 7.x는 지원 되지 않는 이전 커널을 사용 하는 동안 [Debian backports](https://wiki.debian.org/Backports) Debian 7.x Hyper-v 기능을 개선 했습니다.

7. Windows Server 2012 R2 2 세대 가상 컴퓨터는 기본적으로 사용 하도록 설정 하는 보안 부팅 및 일부 Linux 가상 컴퓨터에는 보안 부팅 옵션을 해제 하지 않는 한 부팅 되지 않습니다. 보안 부팅을 사용 하지 않도록 설정할 수는 **펌웨어** 섹션에 있는 가상 컴퓨터에 대 한 설정의 **Hyper-v 관리자** Powershell을 사용 하 여 비활성화할 수 있습니다.

   ```Powershell
   Set-VMFirmware -VMName "VMname" -EnableSecureBoot Off

   ```
8. 최신 업스트림 커널에서 기능 에서만 사용할 포함 된 커널을 사용 하 여 [Debian backports](https://wiki.debian.org/Backports)합니다.

관련 항목

* [CentOS 지원 및 Hyper-v Red Hat Enterprise Linux 가상 컴퓨터](Supported-CentOS-and-Red-Hat-Enterprise-Linux-virtual-machines-on-Hyper-V.md)

* [Hyper-v에서 지원 되는 Oracle Linux 가상 컴퓨터](Supported-Oracle-Linux-virtual-machines-on-Hyper-V.md)

* [Hyper-v에서 지원 되는 SUSE 가상 머신](Supported-SUSE-virtual-machines-on-Hyper-V.md)

* [Hyper-v에서 지원 되는 Ubuntu 가상 컴퓨터](Supported-Ubuntu-virtual-machines-on-Hyper-V.md)

* [Hyper-v에서 지원 되는 FreeBSD 가상 컴퓨터](Supported-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Hyper-v의 Linux 및 FreeBSD 가상 컴퓨터에 대 한 설명이](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Hyper-v에서 Linux를 실행 하는 것에 대 한 모범 사례](Best-Practices-for-running-Linux-on-Hyper-V.md)
