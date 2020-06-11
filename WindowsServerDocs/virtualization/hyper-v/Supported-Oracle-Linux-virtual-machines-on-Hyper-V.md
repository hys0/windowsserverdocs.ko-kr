---
title: Hyper-v에서 지원 되는 Oracle Linux 가상 컴퓨터
description: 각 버전에 포함 된 Linux 통합 서비스 및 기능을 나열 합니다.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.topic: article
ms.assetid: c02fdb5b-62f3-43cb-a190-ab74b3ebcf77
author: shirgall
ms.author: kathydav
ms.date: 06/05/2020
ms.openlocfilehash: 67f38d11c032e9eb0b98da14c25e01a5f67cabae
ms.sourcegitcommit: 76a3b5f66e47e08e8235e2d152185b304d03b68b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/10/2020
ms.locfileid: "84663176"
---
# <a name="supported-oracle-linux-virtual-machines-on-hyper-v"></a>Hyper-v에서 지원 되는 Oracle Linux 가상 컴퓨터

>적용 대상: Windows Server 2019, Windows Server 2016, Hyper-v Server 2016, Windows Server 2012 R2, Hyper-v Server 2012 R2, Windows 10, Windows 8.1

다음과 같은 기능 배포 맵을 각 버전에 존재 하는 기능을 나타냅니다. 알려진된 문제 및 각 배포에 대 한 대안 표 다음에 나열 됩니다.

이 섹션의 내용은 다음과 같습니다.

* [Oracle Linux .x 시리즈](#oracle-linux-8x-series)
* [Oracle Linux 8.x 시리즈](#oracle-linux-7x-series)
* [Oracle Linux .x 시리즈](#oracle-linux-6x-series)
 
   
## <a name="table-legend"></a>표의 범례

* **기본 제공** -LIS이 Linux 배포판의 일부로 포함 됩니다. LIS에서 기본 제공에 대 한 커널 모듈 버전 번호 (볼 수 있듯이 **lsmod**, 예를 들어)는 Microsoft에서 제공한 LIS 다운로드 패키지에 버전 번호가 다릅니다. LIS에서 작성 된 지 오래 된 불일치를 나타내지 않습니다.

* & #10004; -사용 가능한 기능
* (*빈*)-기능을 사용할 수 없음
* **Rhck** -Red Hat 호환 커널
* **Uek (** Unbreakable Enterprise Kernel) 
   * UEK4-업스트림 Linux 커널 릴리스 4.1.12에 빌드 됨
   * UEK5-업스트림 Linux 커널 릴리스 4.14을 기반으로 합니다.
   * UEK6-업스트림 Linux 커널 릴리스 5.4을 기반으로 합니다.

## <a name="oracle-linux-8x-series"></a>Oracle Linux .x 시리즈

|       **기능**     |       **Windows Server 버전**      |       **8.0-8.1 (RHCK)** |
|-----------------------|---------------------------------------|-------------------|
|       **가용성**        |   |
|       **[코어](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#core)**      | 2019, 2016, 2012 R2 | &#10004; | 
|       Windows Server 2016 정확한 시간       | 2019, 2016 | &#10004; | 
|       **[네트워킹](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#networking)**      |   | 
|       Jumbo 프레임        | 2019, 2016, 2012 R2 | &#10004; | 
|       VLAN 태깅 및 트렁킹       | 2019, 2016, 2012 R2 | &#10004;  | 
|       실시간 마이그레이션      | 2019, 2016, 2012 R2 | &#10004; |
|       고정 IP 삽입     |  2019, 2016, 2012 R2 | & #10004; 참고 2 | 
|       vRSS     | 2019, 2016, 2012 R2 | &#10004; |
|       TCP 조각화 및 체크섬 오프 로드 | 2019, 2016, 2012 R2 | &#10004;|
|       SR-IOV  | 2019, 2016 |  &#10004;   |
|       **[스토리지](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#storage)** |  | 
|       VHDX 크기 조정  | 2019, 2016, 2012 R2 | &#10004; |
|       가상 파이버 채널 | 2019, 2016, 2012 R2 | & #10004; 참고 3  |
|       라이브 가상 머신 백업  | 2019, 2016, 2012 R2 | & #10004; 참고 5 |
|       TRIM 지원 | 2019, 2016, 2012 R2 | &#10004;  |
|       SCSI WWN | 2019, 2016, 2012 R2 | &#10004;  |
|       **[메모리](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#memory)** | |
|       PAE 커널 지원  | 2019, 2016, 2012 R2 |  해당 없음 |
|       MMIO 간격 구성  | 2019, 2016, 2012 R2 | &#10004; | 
|       동적 메모리-즉석 추가 | 2019, 2016, 2012 R2  | & #10004; Note 7, 8, 9 |
|       동적 메모리-Ballooning | 2019, 2016, 2012 R2 | & #10004; Note 7, 8, 9 |
|       런타임 메모리 크기 조정 | 2019, 2016  | &#10004;  |
|       **[비디오](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#video)** | |
|       Hyper-v 관련 비디오 장치 | 2019, 2016, 2012 R2 | &#10004;   | 
|       **[기타](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#miscellaneous)** | |
|       키-값 쌍  | 2019, 2016, 2012 R2 | &#10004;   | 
|       마스크 불가능 인터럽트 | 2019, 2016, 2012 R2 | &#10004;  | 
|       호스트에서 게스트로 파일 복사 | 2019, 2016, 2012 R2 | &#10004;  | 
|       lsvmbus 명령 | 2019, 2016, 2012 R2 | &#10004;  | 
|       Hyper-v 소켓 | 2019, 2016 | &#10004;  | 
|       PCI 통과/DDA | 2019, 2016 | &#10004; | 
| **[2세대 가상 컴퓨터](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#generation-2-virtual-machines)** | |  |
|       UEFI를 사용 하 여 부팅 | 2019, 2016, 2012 R2 |  & #10004; 참고 12  |   
|       보안 부팅 | 2019, 2016 |  &#10004; | 

## <a name="oracle-linux-7x-series"></a>Oracle Linux 8.x 시리즈

이 시리즈에는 64 비트 커널에만 합니다.

<table width="100%">
<tr height="50px">
<td width="20%" rowspan="2">

기능
</td>
<td width="20%" rowspan="2">

Windows Server 버전
</td>
<td width="30%" colspan="3">

7.5-7.8
</td>
<td width="30%" colspan="3">

7.3-7.4
</td>
</tr>
<tr>
<td width="20%" colspan="2">

RHCK
</td>
<td width="10%">

UEK5
</td>
<td width="20%" colspan="2">

RHCK
</td>
<td width="10%">

UEK4
</td>
</tr>
<tr>
<td width="20%">

가용성
</td>
<td width="20%">


</td>
<td width="10%">

LIS 4.3
</td>
<td width="10%">

기본 제공
</td>
<td width="10%">

기본 제공
</td>
<td width="10%">

LIS 4.3
</td>
<td width="10%">

기본 제공
</td>
<td width="10%">

기본 제공
</td>
</tr>
<tr height="50px">
<td width="20%">

**[코어](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#core)**
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

Windows Server 2016 정확한 시간
</td>
<td width="20%">

2019, 2016
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

</td>
<td width="10%">

</td>
</tr>
<tr height="50px">
<td width="20%">

 **[네트워킹](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#networking)** 
</td>
<td width="20%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
</tr>
<tr height="50px">
<td width="20%">

Jumbo 프레임
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">
VLAN 태깅 및 트렁킹
</td>
<td width="20%">
2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

실시간 마이그레이션
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

고정 IP 삽입
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

& #10004; 참고 2
</td>
<td width="10%">

& #10004; 참고 2
</td>
<td width="10%">

& #10004; 참고 2
</td>
<td width="10%">

& #10004; 참고 2
</td>
<td width="10%">

& #10004; 참고 2
</td>
<td width="10%">

& #10004; 참고 2
</td>
</tr>
<tr height="50px">
<td width="20%">

vRSS
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

TCP 조각화 및 체크섬 오프 로드
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

SR-IOV
</td>
<td width="20%">

2019, 2016
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

**[스토리지](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#storage)**
</td>
<td width="20%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
</tr>
<tr height="50px">
<td width="20%">

VHDX 크기 조정
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

가상 파이버 채널
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

& #10004; 참고 3
</td>
<td width="10%">

& #10004; 참고 3
</td>
<td width="10%">

& #10004; 참고 3
</td>
<td width="10%">

& #10004; 참고 3
</td>
<td width="10%">

& #10004; 참고 3
</td>
<td width="10%">

& #10004; 참고 3
</td>
</tr>
<tr height="50px">
<td width="20%">

라이브 가상 머신 백업
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

& #10004; 참고 5
</td>
<td width="10%">

& #10004; 참고 4, 5
</td>
<td width="10%">

& #10004; 참고 5
</td>
<td width="10%">

& #10004; 참고 5
</td>
<td width="10%">

& #10004; 참고 4, 5
</td>
<td width="10%">

& #10004; 참고 5
</td>
</tr>
<tr height="50px">
<td width="20%">

TRIM 지원
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

SCSI WWN
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

</td>
</tr>
<tr height="50px">
<td width="20%">

**[메모리](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#memory)**
</td>
<td width="20%">


</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
</tr>
<tr height="50px">
<td width="20%">

PAE 커널 지원
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

해당 없음
</td>
<td width="10%">

해당 없음
</td>
<td width="10%">

해당 없음
</td>
<td width="10%">

해당 없음
</td>
<td width="10%">

해당 없음
</td>
<td width="10%">

해당 없음
</td>
</tr>
<tr height="50px">
<td width="20%">

MMIO 간격 구성
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

동적 메모리 핫 추가
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004; Note 7, 8, 9
</td>
<td width="10%">

&#10004; Note 8, 9
</td>
<td width="10%">

&#10004; Note 8, 9
</td>
<td width="10%">

&#10004; Note 8, 9
</td>
<td width="10%">

&#10004; Note 8, 9
</td>
<td width="10%">

&#10004; Note 8, 9
</td>
</tr>
<tr height="50px">
<td width="20%">

동적 메모리 Ballooning
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004; Note 7, 8, 9
</td>
<td width="10%">

&#10004; Note 8, 9
</td>
<td width="10%">

&#10004; Note 8, 9
</td>
<td width="10%">

&#10004; Note 8, 9
</td>
<td width="10%">

&#10004; Note 8, 9
</td>
<td width="10%">

&#10004; Note 8, 9
</td>
</tr>
<tr height="50px">
<td width="20%">

런타임 메모리 크기 조정
</td>
<td width="20%">

2019, 2016
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">


</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">


</td>
<td width="10%">

</td>
</tr>
<tr height="50px">
<td width="20%">

**[비디오](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#video)**
</td>
<td width="20%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
</tr>
<tr height="50px">
<td width="20%">

Hyper-v 관련 비디오
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

**[기타](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#miscellaneous)**
</td>
<td width="20%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
</tr>
<tr height="50px">
<td width="20%">

키-값 쌍
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

마스크 불가능 인터럽트
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

호스트에서 게스트로 파일 복사
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

lsvmbus 명령
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">


</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">


</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

Hyper-v 소켓
</td>
<td width="20%">

2019, 2016
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">


</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">


</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

PCI 통과/DDA
</td>
<td width="20%">

2019, 2016
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

**[2세대 가상 컴퓨터](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#generation-2-virtual-machines)**
</td>
<td width="20%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
</tr>
<tr height="50px">
<td width="20%">

UEFI를 사용 하 여 부팅
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

& #10004; 참고 12
</td>
<td width="10%">

& #10004; 참고 12
</td>
<td width="10%">

& #10004; 참고 12
</td>
<td width="10%">

& #10004; 참고 12
</td>
<td width="10%">

& #10004; 참고 12
</td>
<td width="10%">

& #10004; 참고 12
</td>
</tr>
<tr height="50px">
<td width="20%">

보안 부팅
</td>
<td width="20%">

2019, 2016, 2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
</table>


## <a name="oracle-linux-6x-series"></a>Oracle Linux .x 시리즈

이 시리즈에는 64 비트 커널에만 합니다.

|       **기능**     |       **Windows Server 버전**      |       **6.8-6.10 (RHCK)** |       **6.8-6.10 (UEK4)**     | 
|-----------------------|---------------------------------------|-------------------|-------------------|
|       **가용성**     |   | LIS 4.3  | 기본 제공  |
|       **[코어](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#core)**      | 2019, 2016, 2012 R2 | &#10004; | &#10004;
|       Windows Server 2016 정확한 시간       | 2019, 2016 | | 
|       **[네트워킹](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#networking)**      |   |  |
|       Jumbo 프레임        | 2019, 2016, 2012 R2 | &#10004; | &#10004;|
|       VLAN 태깅 및 트렁킹       | 2019, 2016, 2012 R2 | & #10004; 참고 1 | & #10004; 참고 1 |
|       실시간 마이그레이션      | 2019, 2016, 2012 R2 | &#10004; | &#10004;|
|       고정 IP 삽입     |  2019, 2016, 2012 R2 | & #10004; 참고 2 | &#10004;|
|       vRSS     | 2019, 2016, 2012 R2 | &#10004; | &#10004;|
|       TCP 조각화 및 체크섬 오프 로드 | 2019, 2016, 2012 R2 | &#10004;|  &#10004; |
|       SR-IOV  | 2019, 2016 |    |  |
|       **[스토리지](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#storage)** |  |  |
|       VHDX 크기 조정  | 2019, 2016, 2012 R2 | &#10004; | &#10004; |
|       가상 파이버 채널 | 2019, 2016, 2012 R2 | & #10004; 참고 3  | & #10004; 참고 3 |
|       라이브 가상 머신 백업  | 2019, 2016, 2012 R2 | & #10004; 참고 5 | & #10004; 참고 5|
|       TRIM 지원 | 2019, 2016, 2012 R2 | &#10004;  | &#10004; |
|       SCSI WWN | 2019, 2016, 2012 R2 | &#10004;  | &#10004; |
|       **[메모리](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#memory)** | |  |
|       PAE 커널 지원  | 2019, 2016, 2012 R2 |  해당 없음 | 해당 없음
|       MMIO 간격 구성  | 2019, 2016, 2012 R2 | &#10004; | &#10004;  |
|       동적 메모리-즉석 추가 | 2019, 2016, 2012 R2  | & #10004; Note 6, 8, 9 | & #10004; Note 6, 8, 9 |
|       동적 메모리-Ballooning | 2019, 2016, 2012 R2 | & #10004; Note 6, 8, 9 | & #10004; Note 6, 8, 9 |
|       런타임 메모리 크기 조정 | 2019, 2016  |  | |
|       **[비디오](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#video)** | | |
|       Hyper-v 관련 비디오 장치 | 2019, 2016, 2012 R2 | &#10004;   | &#10004; |
|       **[기타](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#miscellaneous)** | | |
|       키-값 쌍  | 2019, 2016, 2012 R2 | &#10004; Note 10, 11   | &#10004; Note 10, 11  |
|       마스크 불가능 인터럽트 | 2019, 2016, 2012 R2 | &#10004;  | &#10004; |
|       호스트에서 게스트로 파일 복사 | 2019, 2016, 2012 R2 | &#10004;  | &#10004; |
|       lsvmbus 명령 | 2019, 2016, 2012 R2 | &#10004;  | &#10004; |
|       Hyper-v 소켓 | 2019, 2016 | &#10004;  | &#10004; |
|       PCI 통과/DDA | 2019, 2016 | &#10004; | &#10004; |
| **[2세대 가상 컴퓨터](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#generation-2-virtual-machines)** | |  |
|       UEFI를 사용 하 여 부팅 | 2019, 2016, 2012 R2 |  & #10004; 참고 12  | & #10004; 참고 12   
|       보안 부팅 | 2019, 2016 |  |  |



## <a name="notes"></a><a name="BKMK_notes"></a>참고

1. 이 Oracle Linux 버전에서는 작동 하지만 VLAN 트렁킹 태그를 지정 하는 VLAN 완료 되지 않습니다.

2. 가상 머신에서 지정된 가상 네트워크 어댑터에 대한 네트워크 관리자가 구성한 경우에 정적 IP 주입 작동하지 않습니다. 고정 IP의 원활한 작동을 위해 주입 있는지 확인 하십시오 하거나 네트워크 관리자가 꺼져 완전히 또는 해당 ifcfg ethX 파일을 통해 특정 네트워크 어댑터에 대 한 해제 되었습니다.

3.  가상 파이버 채널 장치를 사용 하는 동안 Windows Server 2012 r 2에서 논리 단위 번호 0 (LUN 0)이 채워져 있는지 확인 합니다. LUN 0 채워지지 않은 경우 Linux 가상 머신 파이버 채널 디바이스를 고유하게 탑재하지 못할 수 있습니다.

4. 기본 제공 LIS의 경우이 기능을 위해 "hyperv-디먼" 패키지를 설치 해야 합니다.

5.  가 없을 경우 열려 있는 파일 핸들 가상 머신 백업 작업 동안 다음 일부에서 백업 Vhd 복원 파일 시스템 일관성 검사 (fsck)를 수행하도록 할 수 있습니다. 가상 머신에 연결된 iSCSI 디바이스 또는 직접 연결된 스토리지(통과 디스크라고도 함)가있는 경우 실시간 백업 작업이 자동으로 실패할 수 있습니다.

6. 64 비트 가상 컴퓨터에만 동적 메모리 지원이 됩니다.

7. 이 배포에 기본적으로 즉석 추가 지원을 사용 되지 않습니다. Hot Add 지원을 사용 하도록 설정 하려면 다음과 같이 /etc/udev/rules.d/에서 udev 규칙을 추가 해야 합니다.

   1. 파일을 만듭니다 **/etc/udev/rules.d/100-balloon.rules**합니다. 파일에 대해 원하는 다른 이름을 사용할 수 있습니다.

   2. 파일에 다음 콘텐츠를 추가 합니다.`SUBSYSTEM=="memory", ACTION=="add", ATTR{state}="online"`

   3. Hot Add 지원을 사용 하도록 시스템을 재부팅 합니다.

   Linux Integration Services 다운로드가 설치에이 규칙을 만드는 동안 규칙 에서도 제거 됩니다 LIS를 제거 해도 제거 후 동적 메모리를 필요로 하는 경우 규칙을 다시 만들어야 하므로.

8. 게스트 운영 체제 메모리를 너무 낮게 실행 중인 경우 동적 메모리 작업이 실패할 수 있습니다. 다음은 몇 가지 모범 사례입니다.

   * 시작 메모리 및 최소 메모리는 공급 업체에서 권장 하는 메모리의 양을 보다 크거나 같은 이어야 합니다.

   * 시스템에서 전체 사용 가능한 메모리를 사용 하는 애플리케이션은 사용 가능한 RAM의 80%까지 사용 하는 데 제한 됩니다.

9. Windows Server 2016 또는 Windows Server 2012 R2 운영 체제에서 동적 메모리를 사용 하는 경우 **시작 메모리**, **최소 메모리**및 **최대 메모리** 매개 변수를 128 메가바이트 (mb)의 배수로 지정 합니다. 이렇게 하지 않으면 즉석 추가 오류를 발생할 수 있습니다 및 게스트 운영 체제의 증가 메모리 나타나지 않을 수 있습니다.

10. KVP (키/값 쌍) 인프라를 사용 하도록 설정 하려면 Oracle Linux ISO에서 hypervkvpd 또는 hyperv 디먼 rpm 패키지를 설치 합니다. 또는 Oracle Linux Yum 리포지토리에서 패키지를 직접 설치할 수 있습니다.

11. 키/값 쌍 (KVP) 인프라 없이 Linux 소프트웨어 업데이트가 제대로 작동 하지 않습니다. 이 기능으로는 문제를 참조 하는 경우 소프트웨어 업데이트를 다운로드 하려면 공급 업체에 문의 합니다.

12. Windows Server 2012 R2 2 세대 가상 컴퓨터에는 기본적으로 보안 부팅이 사용 하도록 설정 되어 있으며 보안 부팅 옵션을 사용 하지 않는 경우 일부 Linux 가상 컴퓨터는 부팅 되지 않습니다. **Hyper-v 관리자** 에서 가상 컴퓨터에 대 한 설정의 **펌웨어** 섹션에서 보안 부팅을 사용 하지 않도록 설정 하거나 Powershell을 사용 하 여 사용 하지 않도록 설정할 수 있습니다.

    ```Powershell
    Set-VMFirmware -VMName "VMname" -EnableSecureBoot Off
    ```

    Linux Integration Services 다운로드 기존 세대 2 Vm에 적용할 수 있지만 2 세대 기능을 전달 하지 않습니다.


참고 항목

* [Set-vmfirmware](https://technet.microsoft.com/library/dn464287.aspx)

* [CentOS 지원 및 hyper-v Red Hat Enterprise Linux 가상 컴퓨터](Supported-CentOS-and-Red-Hat-Enterprise-Linux-virtual-machines-on-Hyper-V.md)

* [Hyper-v에서 지원 되는 Debian 가상 컴퓨터](Supported-Debian-virtual-machines-on-Hyper-V.md)

* [Hyper-v에서 지원 되는 SUSE 가상 컴퓨터](Supported-SUSE-virtual-machines-on-Hyper-V.md)

* [Hyper-v에서 지원 되는 Ubuntu 가상 컴퓨터](Supported-Ubuntu-virtual-machines-on-Hyper-V.md)

* [Hyper-v에서 지원 되는 FreeBSD 가상 컴퓨터](Supported-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Hyper-v의 Linux 및 FreeBSD 가상 머신에 대 한 기능 설명](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Hyper-v에서 Linux를 실행 하기 위한 모범 사례](Best-Practices-for-running-Linux-on-Hyper-V.md)
