---
title: Hyper-v에서 지원 되는 SUSE 가상 컴퓨터
description: 각 버전에 포함 된 Linux 통합 서비스 및 기능을 나열 합니다.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7ec0e14c-4498-4bd9-8fe6-b94260198efc
author: shirgall
ms.author: kathydav
ms.date: 10/03/2016
ms.openlocfilehash: 45517c1d381ba55c819b09b53ae563092e161b1e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71366730"
---
# <a name="supported-suse-virtual-machines-on-hyper-v"></a>Hyper-v에서 지원 되는 SUSE 가상 컴퓨터

>적용 대상: Windows Server 2016, Hyper-v Server 2016, Windows Server 2012 R2, Hyper-v server 2012 R2, Windows Server 2012, Hyper-v Server 2012, Windows Server 2008 R2, Windows 10, Windows 8.1, Windows 8, Windows 7.1, Windows 7

다음은 각 버전의 기능을 나타내는 기능 배포 맵입니다. 알려진된 문제 및 각 배포에 대 한 대안 표 다음에 나열 됩니다.

Hyper-v에 대 한 기본 제공 SUSE Linux Enterprise Service 드라이버 SUSE에 의해 인증 됩니다. 예제 구성은이 공지에서 볼 수 있습니다. [예 인증 게시판을 SUSE](https://www.suse.com/nbswebapp/yesBulletin.jsp?bulletinNumber=144176).

## <a name="table-legend"></a>표의 범례

* **내장** 된 LIS는이 Linux 배포의 일부로 포함 됩니다. Microsoft에서 제공한 LIS 다운로드 패키지는이 배포에 대해 작동 하지 않으므로 설치 하지 마세요. 기본 제공 LIS의 커널 모듈 버전 번호 (예: **lsmod**에 표시)는 Microsoft에서 제공 하는 lis 다운로드 패키지의 버전 번호와 다릅니다. LIS에서 작성 된 지 오래 된 불일치를 나타내지 않습니다.

* &#10004; -사용 가능한 기능

* (*빈*)-기능을 사용할 수 없음

SLES12 +는 64 비트 전용입니다.

|**기능**|**Windows Server 운영 체제 버전**|**SLES 15**|**SLES 12 SP3/SP4**|**SLES 12 SP2**|**SLES 12 SP1**|**SLES 11 SP4**|**SLES 11 SP3**|
|-|-|-|-|-|-|-|-|
|**Availability**||기본 제공|기본 제공|기본 제공|기본 제공|기본 제공|기본 제공|
|**[Core](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#core)**|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows Server 2016 정확한 시간|2019, 2016|&#10004;|&#10004;|&#10004;||||
|**[Lan](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#networking)**||||||||
|Jumbo 프레임|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|VLAN 태깅 및 트렁킹|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|실시간 마이그레이션|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|고정 IP 삽입|2019, 2016, 2012 R2, 2012|&#10004;참고 1|&#10004;참고 1|&#10004;참고 1|&#10004;참고 1|&#10004;참고 1|&#10004;참고 1|
|vRSS|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|||
|TCP 조각화 및 체크섬 오프 로드|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;||
|SR-IOV|2019, 2016|&#10004;|&#10004;|&#10004;||||
|**[저장할](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#storage)**||||||||
|VHDX 크기 조정|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|가상 파이버 채널|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|라이브 가상 머신 백업|2019, 2016, 2012 R2|&#10004; Note 2, 3, 8|&#10004; Note 2, 3, 8|&#10004; Note 2, 3, 8|&#10004; Note 2, 3, 8|&#10004; Note 2, 3, 8|&#10004; Note 2, 3, 8|
|TRIM 지원|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;||
|SCSI WWN|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;||||
|**[Ram](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#memory)**||||||||
|PAE 커널 지원|2019, 2016, 2012 R2, 2012, 2008 R2|해당 사항 없음|해당 사항 없음|해당 사항 없음|해당 사항 없음|&#10004;|&#10004;|
|MMIO 간격 구성|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|동적 메모리-즉석 추가|2019, 2016, 2012 R2, 2012|&#10004; 참고 5, 6|&#10004; 참고 5, 6|&#10004; 참고 5, 6|&#10004; 참고 5, 6|&#10004; 4, 5, 6 note|&#10004; 4, 5, 6 note|
|동적 메모리-Ballooning|2019, 2016, 2012 R2, 2012|&#10004; 참고 5, 6|&#10004; 참고 5, 6|&#10004; 참고 5, 6|&#10004; 참고 5, 6|&#10004; 4, 5, 6 note|&#10004; 4, 5, 6 note|
|런타임 메모리 크기 조정|2019, 2016|&#10004; 참고 5, 6|&#10004; 참고 5, 6|&#10004; 참고 5, 6||||
|**[화면이](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#video)**||||||||
|Hyper-v 관련 비디오 장치|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|**[기타](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#miscellaneous)**||||||||
|키/값 쌍|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004; 참고 7|&#10004; 참고 7|
|마스크 불가능 인터럽트|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|호스트에서 게스트로 파일 복사|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;||
|lsvmbus 명령|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;||||
|Hyper-v 소켓|2019, 2016|&#10004;|&#10004;|||||
|PCI 통과/DDA|2019, 2016|&#10004;|&#10004;|&#10004;|&#10004;|||
|**[2 세대 가상 컴퓨터](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#generation-2-virtual-machines)**||||||||
|UEFI를 사용 하 여 부팅|2019, 2016, 2012 R2|&#10004; 참고 9|&#10004; 참고 9|&#10004; 참고 9|&#10004; 참고 9|&#10004; 참고 9||
|보안 부팅|2019, 2016|&#10004;|&#10004;|&#10004;|&#10004;|||

## <a name="BKMK_notes"></a>메모란

1. 정적 IP 주입 하는 경우 작동 하지 않을 수 **네트워크 관리자** 가 가상 컴퓨터에는 지정 된 하이퍼-V-특정 네트워크 어댑터 구성 되었습니다. 고정 IP를 원활 하 게 작동 되도록 주입 확인 네트워크 관리자 완전히 해제 하 여 특정 네트워크 어댑터에 대 한 해제 되었습니다 해당 **ifcfg ethX** 파일입니다.

2. 가 없을 경우 열려 있는 파일 핸들 가상 컴퓨터 백업 작업 동안 다음 일부에서 백업 Vhd 복원 파일 시스템 일관성 검사 (fsck)를 수행 하도록 할 수 있습니다.

3. 라이브 백업 작업은 가상 컴퓨터에 연결 된 iSCSI 장치 또는 직접 연결 저장소 (통과 디스크 라고도 함) 하는 경우 자동으로 실패할 수 있습니다.

4. 게스트 운영 체제 메모리를 너무 낮게 실행 중인 경우 동적 메모리 작업이 실패할 수 있습니다. 다음은 몇 가지 모범 사례입니다.

   * 시작 메모리 및 최소 메모리는 공급 업체에서 권장 하는 메모리의 양을 보다 크거나 같은 이어야 합니다.

   * 시스템에서 전체 사용 가능한 메모리를 사용 하는 응용 프로그램은 사용 가능한 RAM의 80%까지 사용 하는 데 제한 됩니다.

5. 64 비트 가상 컴퓨터에만 동적 메모리 지원이 됩니다.

6. 동적 메모리를 Windows Server 2016 또는 Windows Server 2012 운영 체제에서 사용 하는 경우 지정 **시작 메모리**, **최소 메모리**, 및 **최대 메모리** 128 메가바이트 (MB)의 배수로 매개 변수입니다. 이렇게 하지 않으면 Hot-add 오류가 발생할 수 있으므로 및 게스트 운영 체제의 증가 메모리 나타나지 않을 수 있습니다.

7. Windows Server 2016 또는 Windows Server 2012 r 2에서 키/값 쌍 인프라 수 Linux 소프트웨어 업데이트가 없으면 제대로 작동 하지. 이 기능으로는 문제를 참조 하는 경우 소프트웨어 업데이트를 다운로드 하려면 공급 업체에 문의 합니다.

8. VSS 백업에는 단일 파티션을 여러 번 탑재 된 경우 실패 합니다.

9. Windows Server 2012 r 2에서 2 세대 가상 컴퓨터는 기본적으로 보안 부팅이 사용 하도록 설정 되어 있으며 2 세대 Linux 가상 컴퓨터는 보안 부팅 옵션을 사용 하지 않도록 설정 된 경우를 제외 하 고 부팅 되지 않습니다. Hyper-V 관리자 내 가상 컴퓨터에 대한 설정의 **펌웨어** 섹션에서 보안 부팅을 사용하지 않도록 설정하거나 Powershell을 사용하여 사용하지 않도록 설정할 수 있습니다.

   ```Powershell
   Set-VMFirmware -VMName "VMname" -EnableSecureBoot Off

   ```

## <a name="see-also"></a>관련 항목

* [Set-vmfirmware](https://technet.microsoft.com/library/dn464287.aspx)

* [Hyper-v에서 지원 되는 CentOS 및 Red Hat Enterprise Linux 가상 컴퓨터](Supported-CentOS-and-Red-Hat-Enterprise-Linux-virtual-machines-on-Hyper-V.md)

* [Hyper-V에서 지원되는 Debian 가상 머신](Supported-Debian-virtual-machines-on-Hyper-V.md)

* [Hyper-v에서 지원 되는 Oracle Linux 가상 컴퓨터](Supported-Oracle-Linux-virtual-machines-on-Hyper-V.md)

* [Hyper-v에서 지원 되는 Ubuntu 가상 머신](Supported-Ubuntu-virtual-machines-on-Hyper-V.md)

* [Hyper-v에서 지원 되는 FreeBSD 가상 컴퓨터](Supported-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Hyper-v의 Linux 및 FreeBSD 가상 머신에 대 한 기능 설명](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Hyper-v에서 Linux를 실행 하기 위한 모범 사례](Best-Practices-for-running-Linux-on-Hyper-V.md)
