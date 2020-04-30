---
title: Hyper-v에서 Linux를 실행 하기 위한 모범 사례
description: 가상 머신에서 Linux를 실행 하기 위한 권장 사항을 제공 합니다.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.topic: article
ms.assetid: a08648eb-eea0-4e2b-87fb-52bfe8953491
author: shirgall
ms.author: kathydav
ms.date: 04/15/2020
ms.openlocfilehash: d8861369abe24ea0d34dce209a5d98e854c4c95d
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82072239"
---
# <a name="best-practices-for-running-linux-on-hyper-v"></a>Hyper-v에서 Linux를 실행 하기 위한 모범 사례

>적용 대상: Windows Server 2019, Windows Server 2016, Hyper-v 서버 2016, Windows Server 2012 R2, Hyper-v Server 2012 R2, Windows Server 2012, Hyper-v Server 2012, Windows Server 2008 R2, Windows 10, Windows 8.1, Windows 8, Windows 7.1, Windows 7

이 항목에는 Hyper-v에서 Linux 가상 머신을 실행하기 위한 권장 사항 목록이 포함되어 있습니다.

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

RHEL 6.x에서는 여기에 설명 된 대로 grub2 대신 레거시 grub v v0.97 EFI 부팅 로더를 사용할 수 있습니다.[https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/6/html/Installation_Guide/s1-netboot-pxe-config-efi.html](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/6/html/Installation_Guide/s1-netboot-pxe-config-efi.html)

RHEL 이외의 다른 Linux 배포에 6.x, grub v0.97 PxE 서버에서 Linux 커널을 로드를 구성 하려면 유사한 단계가 적용 될 수 있습니다.

또한 RHEL/CentOS 6.6 키보드 및 마우스의 입력에서는 작동 하지 않습니다 방지 하는 사전 설치 커널 메뉴에서 설치 옵션을 지정 합니다. 직렬 콘솔 설치 옵션을 선택할 수 있도록 구성 되어야 합니다.

* 에 **efidefault** PxE 서버에 파일을 다음 커널 매개 변수 추가 **"콘솔 ttyS1 ="**

* Hyper-v의 VM에서이 PowerShell cmdlet을 사용 하 여 COM 포트를 설정 합니다.

```Powershell
Set-VMComPort -VMName <Name> -Number 2 -Path \\.\pipe\dbg1

```

설치 전 커널 실행이 시작 파일을 지정 하는 또한 하지 않으려면 키보드 및 마우스 설치 하는 동안 입력 합니다.

## <a name="use-static-mac-addresses-with-failover-clustering"></a>장애 조치 (failover) 클러스터링과 함께 정적 MAC 주소 사용

Linux 가상 컴퓨터 장애 조치 클러스터링을 사용 하 여 배포할 각 가상 네트워크 어댑터에 대 한 정적 미디어 액세스 제어 (MAC) 주소에 구성 되어야 합니다. 일부 Linux 버전에서 네트워킹 구성 손실 될 수 있습니다 장애 조치 후 새 MAC 주소를 가상 네트워크 어댑터에 할당 되어 있습니다. 네트워크 구성을 잃지를 방지 하려면 각 가상 네트워크 어댑터에 정적 MAC 주소가 있는지 확인 합니다. Hyper-v 관리자 또는 장애 조치 클러스터 관리자에서 가상 머신의 설정을 편집 하여 MAC 주소를 구성할 수 있습니다.

## <a name="use-hyper-v-specific-network-adapters-not-the-legacy-network-adapter"></a>레거시 네트워크 어댑터가 아닌 Hyper-v 관련 네트워크 어댑터 사용

구성 하 고 향상 된 성능의 하이퍼-V 관련 네트워크 카드가 가상 이더넷 어댑터를 사용 합니다. 레거시 및 Hyper-V 특정 네트워크 어댑터가 모두 가상 머신에 연결된 경우 **ifconfig -a**의 출력에 있는 네트워크 이름이 **_tmp12000801310**과 같은 임의값을 표시할 수 있습니다. 이 문제를 방지하려면 Linux 가상 머신에서 하이퍼-V-특정 네트워크 어댑터를 사용하는 경우 모든 레거시 네트워크 어댑터를 제거합니다.

## <a name="use-io-scheduler-noopnone-for-better-disk-io-performance"></a>디스크 i/o 성능 향상을 위해 i/o scheduler noop/none 사용

Linux 커널은 요청 순서를 변경 하기 위해 두 개의 디스크 i/o 스케줄러 집합을 제공 합니다.  하나는 이전 ' blk ' 하위 시스템에 대 한 집합이 고, 한 집합은 최신 ' blk ' 하위 시스템에 대 한 집합입니다. 어떤 경우 든 현재 고체 상태 디스크를 사용 하는 경우 예약 결정을 기본 Hyper-v 하이퍼바이저에 전달 하는 스케줄러를 사용 하는 것이 좋습니다. ' Blk ' 하위 시스템을 사용 하는 Linux 커널의 경우 "noop" 스케줄러입니다. ' Blk-mq ' 하위 시스템을 사용 하는 Linux 커널의 경우 "none" 스케줄러입니다.

특정 디스크의 경우 사용 가능한 스케줄러는 다음 파일 시스템 위치에 표시 될 수 있습니다./sys/class/block///`<diskname>` 이 파일 시스템 위치에 작성 하 여 스케줄러를 변경할 수 있습니다. 다시 부팅을 유지 하려면 초기화 스크립트에 변경 내용을 추가 해야 합니다. 자세한 내용은 Linux 배포판 설명서를 참조 하세요.

## <a name="numa"></a>NUMA

2.6.37 이전 버전의 Linux 커널은 더 큰 VM 크기의 Hyper-V에서 NUMA를 지원하지 않습니다. 이 문제는 주로 업스트림 Red Hat 2.6.32 커널을 사용하는 이전 배포에 영향을 미치며, RHEL(Red Hat Enterprise Linux) 6.6(kernel-2.6.32-504)에서 해결되었습니다. 2.6.37 이전의 사용자 지정 커널 또는 2.6.32-504 이전의 RHEL 기반 커널을 실행하는 시스템의 경우 grub.conf의 커널 명령줄에 `numa=off` 부트 매개 변수를 설정해야 합니다. 자세한 내용은 [Red Hat KB 436883](https://access.redhat.com/solutions/436883)을 참조하세요.

## <a name="reserve-more-memory-for-kdump"></a>Kdump에 대 한 더 많은 메모리를 예약 합니다.

덤프 캡처 커널 부팅 시 공포 인 상태로 끝납니다, 경우에 커널에 대 한 더 많은 메모리를 예약 합니다. 예를 들어, 매개 변수를 변경 **crashkernel 384M-:128M =** 에 **crashkernel 384M-:256M =** Ubuntu grub 구성 파일에 있습니다.

## <a name="shrinking-vhdx-or-expanding-vhd-and-vhdx-files-can-result-in-erroneous-gpt-partition-tables"></a>GPT 파티션 테이블을 잘못 된 VHDX를 축소 하거나 VHD 및 VHDX 파일을 확장 될 수 있습니다.

Hyper-v는 파티션, 볼륨 또는 디스크에 있을 수 있는 파일 시스템 데이터 구조에 관계 없이 가상 디스크 (VHDX) 파일을 축소 수 있습니다. VHDX 파티션 종료 되기 전에 VHDX의 끝을 제공 하는 위치를 축소 되 데이터가 손실 될 수 있습니다 면 파티션을 읽을 때 파티션이 손상 또는 잘못 된 데이터를 될 수 있습니다을 반환할 수 있습니다.

VHD 또는 VHDX 크기를 조정한 후 관리자 fdisk와 같은 유틸리티를 사용 해야 하거나 parted 파티션, 볼륨 및 디스크의 크기에 대 한 변경 내용을 반영 하도록 파일 시스템 구조를 업데이트 합니다. 축소 하거나 VHD 또는 VHDX GUID 파티션 테이블 (GPT)이 있는 차트의 크기를 확장 하면 경고 파티션 레이아웃을 확인 하는 파티션 관리 도구가 사용 될 때 첫 번째 및 보조 GPT 헤더를 해결 하려면 관리자를 열라는 경고가 표시 됩니다. 이 단계를 직접 데이터 손실 없이 수행 해도 됩니다.

## <a name="see-also"></a>참고 항목

* [Windows에서 Hyper-v에 대 한 지원 되는 Linux 및 FreeBSD 가상 컴퓨터](Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md)

* [Hyper-v에 FreeBSD를 실행 하기 위한 모범 사례](Best-practices-for-running-FreeBSD-on-Hyper-V.md)

* [Hyper-V 클러스터 배포](https://technet.microsoft.com/library/jj863389.aspx)

* [Azure 용 Linux 이미지 만들기](https://docs.microsoft.com/azure/virtual-machines/linux/create-upload-generic)

* [Azure에서 Linux VM 최적화](https://docs.microsoft.com/azure/virtual-machines/linux/optimization)
