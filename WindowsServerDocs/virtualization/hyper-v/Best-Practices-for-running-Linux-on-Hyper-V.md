---
title: Hyper-v에서 Linux를 실행 하기 위한 모범 사례
description: 가상 머신에서 Linux를 실행 하는 것에 대 한 권장 사항을 제공 합니다.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a08648eb-eea0-4e2b-87fb-52bfe8953491
author: shirgall
ms.author: kathydav
ms.date: 3/1/2019
ms.openlocfilehash: 190a5e5d32140d6fa688bb9de98d05ec2f9783c3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59838684"
---
# <a name="best-practices-for-running-linux-on-hyper-v"></a>Hyper-v에서 Linux를 실행 하기 위한 모범 사례

>적용 대상: Windows Server 2019, Windows Server 2016에서 Hyper-v Server 2016, Windows Server 2012 R2, Hyper-V Server 2012 R2, Windows Server 2012 Hyper-V Server 2012, Windows Server 2008 R2, Windows 10, Windows 8.1, Windows 8, Windows 7.1, Windows 7

이 항목에는 Hyper-v에서 Linux 가상 컴퓨터를 실행 하기 위한 권장 사항 목록이 포함 되어 있습니다.

## <a name="tuning-linux-file-systems-on-dynamic-vhdx-files"></a>동적 VHDX 파일에서 Linux 파일 시스템을 튜닝

일부 Linux 파일 시스템 파일 시스템 비어 대개 하는 경우에 상당한 양의 실제 디스크 공간을 사용할 수 있습니다. 동적 VHDX 파일의 실제 디스크 공간 사용량을 줄이기 위해 다음 권장 사항을 따릅니다.

* VHDX를 만들 때 (32MB 기본값)에서 1 MB BlockSizeBytes PowerShell에서 다음과 같이 사용

```Powershell
PS > New-VHD -Path C:\MyVHDs\test.vhdx -SizeBytes 127GB -Dynamic -BlockSizeBytes 1MB
```

* Ext4 형식은 ext4 e x t 3 동적 VHDX 파일을 사용할 때 보다 공간을 효율적 이므로 e x t 3를 선호 합니다.

* 때 파일 시스템을 만드는 예를 들어, 4, 096 될 그룹 수를 지정 합니다.

```bash
# mkfs.ext4 -G 4096 /dev/sdX1

```

## <a name="grub-menu-timeout-on-generation-2-virtual-machines"></a>2 세대 가상 컴퓨터에서 grub 메뉴 제한 시간

에뮬레이션에 2 세대 가상 컴퓨터에서 제거 되 고 레거시 하드웨어로 인해 grub 메뉴 카운트다운 타이머가 카운트다운 너무 빨리 표시 될 grub 메뉴에 대 한 기본 항목을 즉시 로드 합니다. Grub EFI 지원 타이머를 사용 하 여 해결 될 때까지 수정 **/boot/grub/grub.conf**, /**등/기본/grub**, 또는 해당 하는 "시간 제한 100000 =" 기본값 대신 "timeout = 5".

## <a name="pxe-boot-on-generation-2-virtual-machines"></a>2 세대 가상 컴퓨터에서 PxE 부팅

없기 때문에 PIT 타이머에 2 세대 가상 컴퓨터를 PxE TFTP 서버에 대 한 네트워크 연결 종료가 중단 하 고 Grub 구성을 읽고 커널을 로드 하는 서버에서 부팅 로더를 방지 합니다.

RHEL에서 6.x, 여기에 설명 된 대로 grub2 대신 레거시 grub v0.97 EFI 부팅 로더를 사용할 수 있습니다. [https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/6/html/Installation_Guide/s1-netboot-pxe-config-efi.html](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/6/html/Installation_Guide/s1-netboot-pxe-config-efi.html)

RHEL 이외의 다른 Linux 배포에 6.x, grub v0.97 PxE 서버에서 Linux 커널을 로드를 구성 하려면 유사한 단계가 적용 될 수 있습니다.

또한 RHEL/CentOS 6.6 키보드 및 마우스의 입력에서는 작동 하지 않습니다 방지 하는 사전 설치 커널 메뉴에서 설치 옵션을 지정 합니다. 직렬 콘솔 설치 옵션을 선택할 수 있도록 구성 되어야 합니다.

* 에 **efidefault** PxE 서버에 파일을 다음 커널 매개 변수 추가 **"콘솔 ttyS1 ="**

* Hyper-v의 VM에서이 PowerShell cmdlet을 사용 하 여 COM 포트를 설정 합니다.

```Powershell
Set-VMComPort -VMName <Name> -Number 2 -Path \\.\pipe\dbg1

```

설치 전 커널 실행이 시작 파일을 지정 하는 또한 하지 않으려면 키보드 및 마우스 설치 하는 동안 입력 합니다.

## <a name="use-static-mac-addresses-with-failover-clustering"></a>정적 MAC 주소를 장애 조치 클러스터링 사용

Linux 가상 컴퓨터 장애 조치 클러스터링을 사용 하 여 배포할 각 가상 네트워크 어댑터에 대 한 정적 미디어 액세스 제어 (MAC) 주소에 구성 되어야 합니다. 일부 Linux 버전에서 네트워킹 구성 손실 될 수 있습니다 장애 조치 후 새 MAC 주소를 가상 네트워크 어댑터에 할당 되어 있습니다. 네트워크 구성을 잃지를 방지 하려면 각 가상 네트워크 어댑터에 정적 MAC 주소가 있는지 확인 합니다. Hyper-v 관리자 또는 장애 조치 클러스터 관리자에서 가상 컴퓨터의 설정을 편집 하 여 MAC 주소를 구성할 수 있습니다.

## <a name="use-hyper-v-specific-network-adapters-not-the-legacy-network-adapter"></a>레거시 네트워크 어댑터가 아닌 하이퍼-V-특정 네트워크 어댑터를 사용 합니다.

구성 하 고 향상 된 성능의 하이퍼-V 관련 네트워크 카드가 가상 이더넷 어댑터를 사용 합니다. 이전 및 하이퍼-V-특정 네트워크 어댑터는 가상 컴퓨터에 연결 하면 경우에 네트워크의 출력에 이름을 **ifconfig-a** 와 같은 임의의 값을 표시할 수 있습니다 **_tmp12000801310**합니다. 이 문제를 방지 하려면 Linux 가상 컴퓨터에서 하이퍼-V-특정 네트워크 어댑터를 사용 하는 경우 모든 레거시 네트워크 어댑터를 제거 합니다.

## <a name="use-io-scheduler-noop-for-better-disk-io-performance"></a>더 나은 디스크 I/O 성능에 대 한 I/O 스케줄러 NOOP를 사용 합니다.

Linux 커널에는 서로 다른 알고리즘을 사용 하 여 요청을 다시 정렬 하려면 네 명의 다른 I/O 스케줄러입니다. NOOP는 하이퍼바이저 수행 하기 위해 일정 의사 결정을 전달 하는 선입 선출 방식입니다. Hyper-v의 Linux 가상 컴퓨터를 실행 하는 경우 NOOP 스케줄러로 사용 하는 것이 좋습니다. 부팅 로더가 구성에서 특정 장치에 대 한 스케줄러를 변경 하려면 (/ 예를 들어 etc/grub.conf), 추가 **엘리베이터 noop =** 커널 매개 변수를 다음 다시 시작 하십시오.

## <a name="numa"></a>NUMA

Linux 커널 버전 이전 2.6.37 보다 지원 하지 않습니다 NUMA Hyper-v에서 더 큰 VM 크기를 사용 하 여. 이 문제에 주로 영향을 줍니다 이전 배포는 업스트림을 사용 하 여 Red Hat 2.6.32 커널을에서 Red Hat Enterprise Linux (RHEL) 6.6 (커널-2.6.32-504)를 수정 했습니다. 2.6.32-504 부트 매개 변수를 설정 해야 하는 보다 2.6.37 보다 오래 된 사용자 지정 커널 또는 오래 된 RHEL 기반 커널을 실행 하는 시스템 `numa=off` 의 경우 grub.conf의 커널 명령줄에 있습니다. 자세한 내용은 [Red Hat KB 436883](https://access.redhat.com/solutions/436883)합니다.

## <a name="reserve-more-memory-for-kdump"></a>Kdump에 대 한 더 많은 메모리를 예약 합니다.

덤프 캡처 커널 부팅 시 공포 인 상태로 끝납니다, 경우에 커널에 대 한 더 많은 메모리를 예약 합니다. 예를 들어, 매개 변수를 변경 **crashkernel 384M-:128M =** 에 **crashkernel 384M-:256M =** Ubuntu grub 구성 파일에 있습니다.

## <a name="shrinking-vhdx-or-expanding-vhd-and-vhdx-files-can-result-in-erroneous-gpt-partition-tables"></a>GPT 파티션 테이블을 잘못 된 VHDX를 축소 하거나 VHD 및 VHDX 파일을 확장 될 수 있습니다.

Hyper-v는 파티션, 볼륨 또는 디스크에 있을 수 있는 파일 시스템 데이터 구조에 관계 없이 가상 디스크 (VHDX) 파일을 축소 수 있습니다. VHDX 파티션 종료 되기 전에 VHDX의 끝을 제공 하는 위치를 축소 되 데이터가 손실 될 수 있습니다 면 파티션을 읽을 때 파티션이 손상 또는 잘못 된 데이터를 될 수 있습니다을 반환할 수 있습니다.

VHD 또는 VHDX 크기를 조정한 후 관리자 fdisk와 같은 유틸리티를 사용 해야 하거나 parted 파티션, 볼륨 및 디스크의 크기에 대 한 변경 내용을 반영 하도록 파일 시스템 구조를 업데이트 합니다. 축소 하거나 VHD 또는 VHDX GUID 파티션 테이블 (GPT)이 있는 차트의 크기를 확장 하면 경고 파티션 레이아웃을 확인 하는 파티션 관리 도구가 사용 될 때 첫 번째 및 보조 GPT 헤더를 해결 하려면 관리자를 열라는 경고가 표시 됩니다. 이 단계를 직접 데이터 손실 없이 수행 해도 됩니다.

## <a name="see-also"></a>참조

* [Windows의 Hyper-v에 대 한 지원 되는 Linux 및 FreeBSD 가상 컴퓨터](Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md)

* [Hyper-v에 FreeBSD를 실행 하는 것에 대 한 모범 사례](Best-practices-for-running-FreeBSD-on-Hyper-V.md)

* [Hyper-v 클러스터 배포](https://technet.microsoft.com/library/jj863389.aspx)

* [Azure 용 Linux 이미지 만들기](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/create-upload-generic)

* [Azure에서 Linux VM 최적화](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/optimization)
