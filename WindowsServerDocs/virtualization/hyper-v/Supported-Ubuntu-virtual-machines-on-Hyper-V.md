---
title: Hyper-v에서 지원 되는 Ubuntu 가상 컴퓨터
description: 각 버전에 포함 된 Linux 통합 서비스 및 기능을 나열 합니다.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 95ea5f7c-25c6-494b-8ffd-2a77f631ee94
author: shirgall
ms.author: shirgall
ms.date: 06/13/2019
ms.openlocfilehash: ed1c1a9f678dd7cb68b59d2df239ca278b7a3688
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71365484"
---
# <a name="supported-ubuntu-virtual-machines-on-hyper-v"></a>Hyper-v에서 지원 되는 Ubuntu 가상 컴퓨터

>적용 대상: Windows Server 2019, 2016, Hyper-v 서버 2019, 2016, Windows Server 2012 R2, Hyper-v Server 2012 R2, Windows Server 2012, Hyper-v Server 2012, Windows Server 2008 R2, Windows 10, Windows 8.1, Windows 8, Windows 7.1, Windows 7

Ubuntu 12.04 부터는 게스트 가상 컴퓨터로 사용 하기에 적합 한 커널을 설치 하는 "linux 가상" 패키지를 로드 합니다. 이 패키지는 항상 최신 최소한의 일반 커널 이미지와 가상 컴퓨터에 사용 되는 헤더에 따라 달라 집니다. 사용은 선택 사항, linux 가상 커널 적은 드라이버 로드 및 수 더 빠르게 부팅를 일반 이미지 보다 메모리 오버 헤드를 줄일 합니다.

모든 Hyper-v를 사용 하려면, 적절 한 linux 도구 및 가상 컴퓨터와 도구 및 사용에 대 한 디먼을 설치 하려면 linux 클라우드 도구 패키지를 설치 합니다. Linux 가상 커널을 사용할 때 linux 도구 가상 및 linux 컴퓨터 클라우드 도구-가상를 로드 합니다.

다음과 같은 기능 배포 맵을 각 버전의 기능을 나타냅니다. 알려진된 문제 및 각 배포에 대 한 대안 표 다음에 나열 됩니다.

## <a name="table-legend"></a>표의 범례

* **기본 제공** -LIS이 Linux 배포판의 일부로 포함 됩니다. Microsoft에서 제공한 LIS 다운로드 패키지 설치 안 함이 배포에 대 한 작동 하지 않습니다. LIS에서 기본 제공에 대 한 커널 모듈 버전 번호 (볼 수 있듯이 **lsmod**, 예를 들어)는 Microsoft에서 제공한 LIS 다운로드 패키지에 버전 번호가 다릅니다. LIS에서 작성 된 지 오래 된 불일치를 나타내지 않습니다.

* &#10004; -사용 가능한 기능

* (*빈*)-기능을 사용할 수 없음

|**기능**|**Windows Server 운영 체제 버전**|**18.10/19.04**|**18.04 LTS**|**16.04 LTS**|**14.04 LTS**|**12.04 LTS**|
|-|-|-|-|-|-|-|
|**가용성**||기본 제공|기본 제공|기본 제공|기본 제공|기본 제공|
|**[Core](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#core)**|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows Server 2016 정확한 시간|2019, 2016|&#10004;|&#10004;|&#10004;|||
|**[Lan](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#networking)**|||||||
|Jumbo 프레임|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|VLAN 태깅 및 트렁킹|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|실시간 마이그레이션|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|고정 IP 삽입|2019, 2016, 2012 R2, 2012|&#10004; 참고 1|&#10004; 참고 1|&#10004; 참고 1|&#10004; 참고 1|&#10004; 참고 1|
|vRSS|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;||
|TCP 조각화 및 체크섬 오프 로드|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;||
|SR-IOV|2019, 2016|&#10004;|&#10004;|&#10004;|||
|**[저장할](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#storage)**||||||
|VHDX 크기 조정|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;||
|가상 파이버 채널|2019, 2016, 2012 R2|&#10004; 참고 2|&#10004; 참고 2|&#10004; 참고 2|&#10004; 참고 2||
|라이브 가상 머신 백업|2019, 2016, 2012 R2|&#10004;참고 3, 4, 6|&#10004; Note 3, 4, 5|&#10004; Note 3, 4, 5|&#10004; Note 3, 4, 5||
|TRIM 지원|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|SCSI WWN|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;||
|**[Ram](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#memory)**||||||
|PAE 커널 지원|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|MMIO 간격 구성|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|동적 메모리-즉석 추가|2019, 2016, 2012 R2, 2012|&#10004; Note 7, 8, 9|&#10004; Note 7, 8, 9|&#10004; Note 7, 8, 9|&#10004; Note 7, 8, 9||
|동적 메모리-Ballooning|2019, 2016, 2012 R2, 2012|&#10004; Note 7, 8, 9|&#10004; Note 7, 8, 9|&#10004; Note 7, 8, 9|&#10004; Note 7, 8, 9||
|런타임 메모리 크기 조정|2019, 2016|&#10004;|&#10004;|&#10004;|&#10004;||
|**[화면이](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#video)**|||||||
|Hyper-v 특정 비디오 장치|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;||
|**[기타](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#miscellaneous)**||||||
|키/값 쌍|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;참고 6, 10|&#10004; 참고 5, 10|&#10004; 참고 5, 10|&#10004; 참고 5, 10|&#10004; 참고 5, 10|
|마스크 불가능 인터럽트|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|호스트에서 게스트로 파일 복사|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;||
|lsvmbus 명령|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;||
|Hyper-v 소켓|2019, 2016||||||
|PCI 통과/DDA|2019, 2016|&#10004;|&#10004;|&#10004;|&#10004;||
|**[2 세대 가상 컴퓨터](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#generation-2-virtual-machines)**||||||
|UEFI를 사용 하 여 부팅|2019, 2016, 2012 R2|&#10004; 참고 11, 12|&#10004; 참고 11, 12|&#10004; 참고 11, 12|&#10004; 참고 11, 12||
|보안 부팅|2019, 2016|&#10004;|&#10004;|&#10004;|&#10004;||

## <a name="notes"></a>참고

1. 정적 IP 주입 하는 경우 작동 하지 않을 수 **네트워크 관리자** 가 가상 컴퓨터에는 지정 된 하이퍼-V-특정 네트워크 어댑터 구성 되었습니다. 고정 IP를 원활 하 게 작동 되도록 주입 확인 네트워크 관리자 완전히 해제 하 여 특정 네트워크 어댑터에 대 한 해제 되었습니다 해당 **ifcfg ethX** 파일입니다.

2. 가상 파이버 채널 장치를 사용 하는 동안 논리 단위 번호 (LUN 0) 0 채워졌는지 확인 합니다. LUN 0 채워지지 않은 경우 Linux 가상 컴퓨터 파이버 채널 장치를 고유 하 게 탑재 하지 못할 수 있습니다.

3. 열려 있는 경우 가상 컴퓨터 백업 작업 중 파일을 처리 한 다음 일부 코너 케이스에서 백업 Vhd 파일 시스템 일관성 검사를 수행 하도록 할 수 (`fsck`) 복원 합니다.

4. 라이브 백업 작업은 가상 컴퓨터에 연결 된 iSCSI 장치 또는 직접 연결 저장소 (통과 디스크 라고도 함) 하는 경우 자동으로 실패할 수 있습니다.

5. 장기 지원 (LTS) 릴리스에서 최신 Linux 통합 서비스에 대 한 최신 가상 하드웨어 사용 (HWE) 커널을 사용합니다.

   14.04, 16.04 및 18.04에 Azure 튜닝 커널을 설치 하려면 루트 (또는 sudo)로 다음 명령을 실행 합니다.

   ```bash
   # apt-get update
   # apt-get install linux-azure
   ```

   12.04에 별도의 가상 커널이 없습니다. 12.04에 일반 HWE kernel를 설치 하려면 루트 (또는 sudo)로 다음 명령을 실행 합니다.

   ```bash
   # apt-get update
   # apt-get install linux-generic-lts-trusty
   ```

   Ubuntu 12.04에서 다음 Hyper-v 디먼는 별도로 설치 된 패키지에 있습니다.

   * **VSS 스냅숏을 데몬** -이 디먼 라이브 Linux 가상 컴퓨터 백업을 만드는 데 필요 합니다.
   * **KVP 데몬** -이 디먼 설정 및 내부 형식과 외부 키/값 쌍을 쿼리할 수 있습니다.
   * **fcopy 데몬** -이 데몬 호스트와 게스트 사이 서비스를 복사 하는 파일을 구현 합니다.

   12.04에 KVP 디먼을 설치 하려면 루트 (또는 sudo)로 다음 명령을 실행 합니다.

   ```bash
   # apt-get install hv-kvp-daemon-init linux-tools-lts-trusty linux-cloud-tools-generic-lts-trusty
   ```

   커널 업데이트 될 때마다 사용 하도록 가상 컴퓨터를 다시 부팅 해야 합니다.

6. Ubuntu 18.10 또는 19.04에서 최신 가상 커널을 사용 하 여 최신 Hyper-v 기능을 제공 합니다.

   18.10 또는 19.04에서 가상 커널을 설치 하려면 루트 (또는 sudo)로 다음 명령을 실행 합니다.

   ```bash
   # apt-get update
   # apt-get install linux-azure
   ```

   커널 업데이트 될 때마다 사용 하도록 가상 컴퓨터를 다시 부팅 해야 합니다.

7. 64 비트 가상 컴퓨터에만 동적 메모리 지원이 됩니다.

8. 게스트 운영 체제 메모리를 너무 낮게 실행 중인 경우 동적 메모리 작업이 실패할 수 있습니다. 다음은 몇 가지 모범 사례입니다.

   * 시작 메모리 및 최소 메모리는 공급 업체에서 권장 하는 메모리의 양을 보다 크거나 같은 이어야 합니다.

   * 시스템에서 전체 사용 가능한 메모리를 사용 하는 응용 프로그램은 사용 가능한 RAM의 80%까지 사용 하는 데 제한 됩니다.

9. Windows Server 2019, Windows Server 2016 또는 Windows Server 2012/2012 R2 운영 체제에서 동적 메모리를 사용 하는 경우 **시작 메모리**, **최소 메모리**및 **최대 메모리** 매개 변수를 128 메가바이트 (mb)의 배수로 지정 합니다. 이렇게 하지 않으면 Hot-add 오류가 발생할 수 있으므로 및 게스트 운영 체제에 증가 하는 메모리를 확인할 수 있습니다.

10. Windows Server 2019, Windows Server 2016 또는 Windows Server 2012 r 2에서는 키/값 쌍 인프라가 Linux 소프트웨어 업데이트가 없으면 제대로 작동 하지 않을 수 있습니다. 이 기능으로는 문제를 참조 하는 경우 소프트웨어 업데이트를 다운로드 하려면 공급 업체에 문의 합니다.

11. Windows Server 2012 r 2에서 2 세대 가상 컴퓨터 수 있으며 일부 Linux 가상 컴퓨터는 보안 부팅 옵션을 해제 하지 않는 한 부팅 하 고 기본적으로 사용 하도록 설정 하는 보안 부팅 보안 부팅을 사용 하지 않도록 설정할 수는 **펌웨어** 섹션에 있는 가상 컴퓨터에 대 한 설정의 **Hyper-v 관리자** Powershell을 사용 하 여 비활성화할 수 있습니다.

    ```Powershell
    Set-VMFirmware -VMName "VMname" -EnableSecureBoot Off
    ```

12. 새로운 2 세대 가상 컴퓨터를 만들거나 기존 가상 컴퓨터를 세대 2 VHD의 VHD를 복사 하려면 먼저 다음이 단계를 따르십시오.

    1. 기존 2 세대 가상 컴퓨터에 로그인 합니다.

    2. EFI 부팅 디렉터리에 디렉터리를 변경 합니다.

       ```bash
       # cd /boot/efi/EFI
       ```

    3. 부팅 라는 새 디렉터리를 ubuntu 디렉터리에 복사 합니다.

       ```bash
       # sudo cp -r ubuntu/ boot
       ```

    4. 새로 만든된 부팅 디렉터리에 디렉터리를 변경 합니다.

       ```bash
       # cd boot
       ```

    5. Shimx64.efi 파일을 이름을 바꿉니다.

       ```bash
       # sudo mv shimx64.efi bootx64.efi
       ```

## <a name="see-also"></a>관련 항목

* [Hyper-v에서 지원 되는 CentOS 및 Red Hat Enterprise Linux 가상 컴퓨터](Supported-CentOS-and-Red-Hat-Enterprise-Linux-virtual-machines-on-Hyper-V.md)

* [Hyper-V에서 지원되는 Debian 가상 머신](Supported-Debian-virtual-machines-on-Hyper-V.md)

* [Hyper-v에서 지원 되는 Oracle Linux 가상 컴퓨터](Supported-Oracle-Linux-virtual-machines-on-Hyper-V.md)

* [Hyper-v에서 지원 되는 SUSE 가상 컴퓨터](Supported-SUSE-virtual-machines-on-Hyper-V.md)

* [Hyper-v의 Linux 및 FreeBSD 가상 머신에 대 한 기능 설명](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Hyper-v에서 Linux를 실행 하기 위한 모범 사례](Best-Practices-for-running-Linux-on-Hyper-V.md)

* [Set-vmfirmware](https://technet.microsoft.com/library/dn464287.aspx)

* [2 세대 VM의 Ubuntu 14.04-이혜준 Armstrong의 가상화 블로그](https://blogs.msdn.com/b/virtual_pc_guy/archive/2014/06/09/ubuntu-14-04-in-a-generation-2-vm.aspx)
