---
title: Hyper-v에서 지원 되는 Oracle Linux 가상 컴퓨터
description: Linux integration services 및 각 버전에 포함 된 기능을 나열 합니다.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c02fdb5b-62f3-43cb-a190-ab74b3ebcf77
author: shirgall
ms.author: kathydav
ms.date: 06/01/2017
ms.openlocfilehash: e353ea0b444c07557de99db4472f565decb37349
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447754"
---
# <a name="supported-oracle-linux-virtual-machines-on-hyper-v"></a>Hyper-v에서 지원 되는 Oracle Linux 가상 컴퓨터

>적용 대상: Windows Server 2016에서 Hyper-v Server 2016, Windows Server 2012 R2, Hyper-V Server 2012 R2, Windows Server 2012 Hyper-V Server 2012, Windows Server 2008 R2, Windows 10, Windows 8.1, Windows 8, Windows 7.1, Windows 7

다음과 같은 기능 배포 맵을 각 버전에 존재 하는 기능을 나타냅니다. 알려진된 문제 및 각 배포에 대 한 대안 표 다음에 나열 됩니다.

섹션 내용

* [Red Hat 호환 커널 시리즈](Supported-Oracle-Linux-virtual-machines-on-Hyper-V.md#BKMK_rhc)

* [Unbreakable Enterprise Kernel 시리즈](Supported-Oracle-Linux-virtual-machines-on-Hyper-V.md#BKMK_uek)

* [참고](Supported-Oracle-Linux-virtual-machines-on-Hyper-V.md#BKMK_notes)

## <a name="table-legend"></a>표의 범례

* **기본 제공** -LIS이 Linux 배포판의 일부로 포함 됩니다. LIS에서 기본 제공에 대 한 커널 모듈 버전 번호 (볼 수 있듯이 **lsmod**, 예를 들어)는 Microsoft에서 제공한 LIS 다운로드 패키지에 버전 번호가 다릅니다. LIS에서 작성 된 지 오래 된 불일치를 나타내지 않습니다.

* &#10004; -사용 가능한 기능

* (*빈*)-기능을 사용할 수 없음

* **UEK R\*x QU\*y** -Unbreakable Enterprise Kernel (UEK) 여기서 *x* 릴리스 번호 및 *y* 분기별 업데이트 됩니다.

## <a name="BKMK_rhc"></a>Red Hat 호환 커널 시리즈

6.x 계열에 대 한 32 비트 커널 PAE 설정입니다. Oracle Linux RHCK 6.0-6.3에 대 한 기본 제공 LIS 지원이 있습니다. Oracle Linux 7.x 커널은 64 비트 전용.

| **기능**                                                                                                              | **Windows server 버전**   | **7.5-7.6**         | **7.4**             | **6.4-6.8 및 7.0 7.3**                                             | **6.4-6.8 및 7.0 7.2**                                             | **RHCK 7.0-7.2**         | **RHCK 6.8**             | **RHCK 6.6, 6.7**        | **RHCK 6.5**              | **RHCK6.4**               |
|--------------------------------------------------------------------------------------------------------------------------|------------------------------|---------------------|---------------------|---------------------------------------------------------------------|---------------------------------------------------------------------|--------------------------|--------------------------|--------------------------|---------------------------|---------------------------|
| **가용성**                                                                                                         |                              | 기본 제공            | 기본 제공            | [LIS 4.2](https://www.microsoft.com/download/details.aspx?id=55106) | [LIS 4.1](https://www.microsoft.com/download/details.aspx?id=51612) | 기본 제공                 | 기본 제공                 | 기본 제공                 | 기본 제공                  | 기본 제공                  |
| **[Core](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#core)**                          | 2016, 2012 R2, 2012, 2008 R2 | &#10004;            | &#10004;            | &#10004;                                                            | &#10004;                                                            | &#10004;                 | &#10004;                 | &#10004;                 | &#10004;                  |                           |
| Windows Server 2016 정확한 시간                                                                                        | 2016                         |                     |                     |                                                                     |                                                                     |                          |                          |                          |                           |                           |
| **[Networking](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#networking)**              |                              |                     |                     |                                                                     |                                                                     |                          |                          |                          |                           |                           |
| Jumbo 프레임                                                                                                             | 2016, 2012 R2, 2012, 2008 R2 | &#10004;            | &#10004;            | &#10004;                                                            | &#10004;                                                            | &#10004;                 | &#10004;                 | &#10004;                 | &#10004;                  | &#10004;                  |
| VLAN 태깅, 트렁킹                                                                                                | 2016, 2012 R2, 2012, 2008 R2 | &#10004;            | &#10004;            | &#10004; (6.4 6.8에 대 한 참고 1)                                       | &#10004; (6.4 6.8에 대 한 참고 1)                                       | &#10004;                 | &#10004; 참고 1          | &#10004; 참고 1          | &#10004; 참고 1           | &#10004; 참고 1           |
| 실시간 마이그레이션                                                                                                           | 2016, 2012 R2, 2012, 2008 R2 | &#10004;            | &#10004;            | &#10004;                                                            | &#10004;                                                            | &#10004;                 | &#10004;                 | &#10004;                 | &#10004;                  | &#10004;                  |
| 정적 IP 주입                                                                                                      | 2016, 2012 R2, 2012          | &#10004; 참고 14    | &#10004; 참고 14    | &#10004;                                                            | &#10004;                                                            | &#10004;                 | &#10004;                 | &#10004;                 | &#10004;                  | &#10004;                  |
| vRSS                                                                                                                     | 2016, 2012 R2                | &#10004;            | &#10004;            | &#10004;                                                            | &#10004;                                                            | &#10004;                 | &#10004;                 | &#10004;                 |                           |                           |
| TCP 조각화와 체크섬 오프 로드                                                                                   | 2016, 2012 R2, 2012, 2008 R2 | &#10004;            | &#10004;            | &#10004;                                                            | &#10004;                                                            | &#10004;                 | &#10004;                 | &#10004;                 |                           |                           |
| SR-IOV                                                                                                                   | 2016                         | &#10004;            | &#10004;            |                                                                     |                                                                     |                          |                          |                          |                           |                           |
| **[Storage](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#storage)**                    |                              |                     |                     |                                                                     |                                                                     |                          |                          |                          |                           |                           |
| VHDX 크기 조정                                                                                                              | 2016, 2012 R2                | &#10004;            | &#10004;            | &#10004;                                                            | &#10004;                                                            | &#10004;                 | &#10004;                 | &#10004;                 | &#10004;                  |                           |
| 가상 파이버 채널                                                                                                    | 2016, 2012 R2                | &#10004; 참고 2     | & #10004; 참고 2     | & #10004; 참고 2                                                     | & #10004; 참고 2                                                     | & #10004; 참고 2          | & #10004; 참고 2          | & #10004; 참고 2          | &#10004; 참고 2           |                           |
| 가상 머신 백업                                                                                              | 2016, 2012 R2                | &#10004;11,3 참고  | &#10004;참고 11, 3 | &#10004; 참고 3, 4                                                  | &#10004; 참고 3, 4                                                  | &#10004; Note 3, 4, 11   | &#10004; Note 3, 4, 11   | &#10004; Note 3, 4, 11   | &#10004; Note 3, 4, 5, 11 | &#10004; Note 3, 4, 5, 11 |
| TRIM 지원                                                                                                             | 2016, 2012 R2                | &#10004;            | &#10004;            | &#10004;                                                            | &#10004;                                                            | &#10004;                 | &#10004;                 |                          |                           |                           |
| SCSI WWN                                                                                                                 | 2016, 2012 R2                | &#10004;            |                     | &#10004;                                                            | &#10004;                                                            |                          |                          |                          |                           |                           |
| **[Memory](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#memory)**                      |                              |                     |                     |                                                                     |                                                                     |                          |                          |                          |                           |                           |
| PAE 커널 지원                                                                                                       | 2016, 2012 R2, 2012, 2008 R2 | 해당 사항 없음                 | 해당 사항 없음                 | &#10004; (6.x에만 해당)                                                 | &#10004; (6.x에만 해당)                                                 | 해당 사항 없음                      | &#10004;                 | &#10004;                 | &#10004;                  | &#10004;                  |
| MMIO 간격 구성                                                                                                | 2016, 2012 R2                | &#10004;            | &#10004;            | &#10004;                                                            | &#10004;                                                            | &#10004;                 | &#10004;                 | &#10004;                 | &#10004;                  | &#10004;                  |
| 동적 메모리-즉석 추가                                                                                                 | 2016, 2012 R2, 2012          | &#10004;참고 8, 9  | &#10004;참고 8, 9  | &#10004; Note 7, 8, 9, 10 (참고 6.4 6.7에 대 한 6)                      | &#10004; Note 7, 8, 9, 10 (참고 6.4 6.7에 대 한 6)                      | &#10004; Note 6, 7, 8, 9 | &#10004; Note 6, 7, 8, 9 | &#10004; Note 6, 7, 8, 9 | &#10004; Note 6, 7, 8, 9  |                           |
| 동적 메모리-Ballooning                                                                                              | 2016, 2012 R2, 2012          | &#10004;참고 8, 9  | &#10004;참고 8, 9  | &#10004; Note 7, 9, 10 (참고 6.4 6.7에 대 한 6)                         | &#10004; Note 7, 9, 10 (참고 6.4 6.7에 대 한 6)                         | &#10004; Note 6, 8, 9    | &#10004; Note 6, 8, 9    | &#10004; Note 6, 8, 9    | &#10004; Note 6, 8, 9     | &#10004; Note 6, 8, 9, 10 |
| 런타임 메모리 크기 조정                                                                                                    | 2016                         |                     |                     |                                                                     |                                                                     |                          |                          |                          |                           |                           |
| **[Video](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#video)**                        |                              |                     |                     |                                                                     |                                                                     |                          |                          |                          |                           |                           |
| 하이퍼-V-특정 비디오 장치                                                                                            | 2016,2012 R2, 2012, 2008 R2  | &#10004;            | &#10004;            | &#10004;                                                            | &#10004;                                                            | &#10004;                 | &#10004;                 | &#10004;                 | &#10004;                  |                           |
| **[기타](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#miscellaneous)**                 |                              |                     |                     |                                                                     |                                                                     |                          |                          |                          |                           |                           |
| 키-값 쌍                                                                                                           | 2016, 2012 R2, 2012, 2008 R2 | &#10004;            | &#10004;            | &#10004;                                                            | &#10004;                                                            | &#10004; 참고 12         | &#10004; 참고 12         | &#10004; 참고 12         | &#10004; 참고 12          | &#10004; 참고 12          |
| 마스크 불가능 인터럽트                                                                                                   | 2016, 2012 R2                | &#10004;            | &#10004;            | &#10004;                                                            | &#10004;                                                            | &#10004;                 | &#10004;                 | &#10004;                 | &#10004;                  | &#10004;                  |
| 호스트에서 게스트로 파일 복사                                                                                             | 2016, 2012 R2                | &#10004;            | &#10004;            | &#10004;                                                            | &#10004;                                                            |                          | &#10004;                 |                          |                           |                           |
| lsvmbus 명령                                                                                                          | 2016, 2012 R2, 2012, 2008 R2 |                     |                     | &#10004;                                                            | &#10004;                                                            |                          |                          |                          |                           |                           |
| Hyper-v 소켓                                                                                                          | 2016                         |                     |                     | &#10004;                                                            | &#10004;                                                            |                          |                          |                          |                           |                           |
| PCI 통과/DDA                                                                                                      | 2016                         | &#10004;            | &#10004;            |                                                                     |                                                                     |                          |                          |                          |                           |                           |
| **[2 세대 가상 컴퓨터](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#generation-2-virtual-machines)** |                              |                     |                     |                                                                     |                                                                     |                          |                          |                          |                           |                           |
| UEFI를 사용 하 여 부팅                                                                                                          | 2016, 2012 R2                | &#10004; 참고 13    | &#10004; 참고 13    | &#10004; 참고 13                                                    | &#10004; 참고 13                                                    | &#10004; 참고 13         | &#10004; 참고 13         |                          |                           |                           |
| 보안 부팅                                                                                                              | 2016                         | &#10004;            | &#10004;            |                                                                     |                                                                     |                          |                          |                          |                           |                           |


## <a name="BKMK_uek"></a>Unbreakable Enterprise Kernel 시리즈

Oracle Linux Unbreakable Enterprise Kernel (UEK)는 64 비트 전용 되었으며 LIS 기본 제공 지원 해야 합니다.

|**기능**|**Windows server 버전**|**UEK R4**|**UEK R3 QU3**|**UEK R3 QU2**|**UEK R3 QU1**|
|-|-|-|-|-|-|
|**가용성**||기본 제공|기본 제공|기본 제공|기본 제공|
|**[Core](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#core)**|2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows Server 2016 정확한 시간|2016|||||
|**[Networking](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#networking)**||||||
|Jumbo 프레임|2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|
|VLAN 태깅, 트렁킹|2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|
|실시간 마이그레이션|2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|
|정적 IP 주입|2016, 2012 R2, 2012|&#10004;|&#10004;|&#10004;||
|vRSS|2016, 2012 R2|&#10004;||||
|TCP 조각화와 체크섬 오프 로드|2016, 2012 R2, 2012, 2008 R2|&#10004;||||
|SR-IOV|2016|||||
|**[Storage](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#storage)**||||||
|VHDX 크기 조정|2016, 2012 R2|&#10004;|&#10004;|&#10004;||
|가상 파이버 채널|2016, 2012 R2|&#10004;|&#10004;|&#10004;||
|가상 머신 백업|2016, 2012 R2|&#10004; Note 3, 4, 5, 11|&#10004; Note 3, 4, 5, 11|&#10004; Note 3, 4, 5, 11||
|TRIM 지원|2016, 2012 R2|&#10004;||||
|SCSI WWN|2016, 2012 R2|||||
|**[Memory](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#memory)**|
|PAE 커널 지원|2016, 2012 R2, 2012, 2008 R2|해당 사항 없음|해당 사항 없음|해당 사항 없음|해당 사항 없음|
|MMIO 간격 구성|2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|
|동적 메모리-즉석 추가|2016, 2012 R2, 2012|&#10004;||||
|동적 메모리-Ballooning|2016, 2012 R2, 2012|&#10004;||||
|런타임 메모리 크기 조정|2016|||||
|**[Video](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#video)**||||||
|하이퍼-V-특정 비디오 장치|2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;||
|**[기타](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#miscellaneous)**||||||
|키-값 쌍|2016, 2012 R2, 2012, 2008 R2|&#10004; 참고 11, 12|& #10004; 참고 11, 12|& #10004; 참고 11, 12|&#10004; 참고 11, 12|
|마스크 불가능 인터럽트|2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|
|호스트에서 게스트로 파일 복사|2016, 2012 R2|&#10004; 참고 11|&#10004; 참고 11|&#10004; 참고 11|&#10004; 참고 11|
|lsvmbus 명령|2016, 2012 R2, 2012, 2008 R2|||||
|Hyper-v 소켓|2016|||||
|PCI 통과/DDA|2016|||||
|**[2 세대 가상 컴퓨터](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#generation-2-virtual-machines)**|
|UEFI를 사용 하 여 부팅|2016, 2012 R2|&#10004;||||
|보안 부팅|2016|&#10004;||||

## <a name="BKMK_notes"></a>참고 사항

1. 이 Oracle Linux 버전에서는 작동 하지만 VLAN 트렁킹 태그를 지정 하는 VLAN 완료 되지 않습니다.

2. 가상 파이버 채널 장치를 사용 하는 동안 논리 단위 번호 (LUN 0) 0 채워졌는지 확인 합니다. LUN 0 채워지지 않은 경우 Linux 가상 컴퓨터 파이버 채널 장치를 고유 하 게 탑재 하지 못할 수 있습니다.

3. 가 없을 경우 열려 있는 파일 핸들 가상 컴퓨터 백업 작업 동안 다음 일부에서 백업 Vhd 복원 파일 시스템 일관성 검사 (fsck)를 수행 하도록 할 수 있습니다.

4. 라이브 백업 작업은 가상 컴퓨터에 연결 된 iSCSI 장치 또는 직접 연결 저장소 (통과 디스크 라고도 함) 하는 경우 자동으로 실패할 수 있습니다.

5. 백업 지원 라이브 6.4/6.5/UEKR3 Oracle Linux에 대 한 QU2 QU3를 통해 사용할 수 있는 [Linux에 대 한 Hyper-v 백업 Essentials](https://github.com/LIS/backupessentials/tree/1.0)합니다.

6. 64 비트 가상 컴퓨터에만 동적 메모리 지원이 됩니다.

7. 이 배포에 기본적으로 즉석 추가 지원을 사용 되지 않습니다. Hot Add 지원을 사용 하도록 설정 하려면 다음과 같이 /etc/udev/rules.d/에서 udev 규칙을 추가 해야 합니다.

   1. 파일을 만듭니다 **/etc/udev/rules.d/100-balloon.rules**합니다. 파일에 대해 원하는 다른 이름을 사용할 수 있습니다.

   2. 파일에 다음 콘텐츠를 추가 합니다. `SUBSYSTEM=="memory", ACTION=="add", ATTR{state}="online"`

   3. Hot Add 지원을 사용 하도록 시스템을 재부팅 합니다.

   Linux Integration Services 다운로드가 설치에이 규칙을 만드는 동안 규칙 에서도 제거 됩니다 LIS를 제거 해도 제거 후 동적 메모리를 필요로 하는 경우 규칙을 다시 만들어야 하므로.

8. 게스트 운영 체제 메모리를 너무 낮게 실행 중인 경우 동적 메모리 작업이 실패할 수 있습니다. 다음은 몇 가지 모범 사례입니다.

   * 시작 메모리 및 최소 메모리는 공급 업체에서 권장 하는 메모리의 양을 보다 크거나 같은 이어야 합니다.

   * 시스템에서 전체 사용 가능한 메모리를 사용 하는 응용 프로그램은 사용 가능한 RAM의 80%까지 사용 하는 데 제한 됩니다.

9. 동적 메모리를 Windows Server 2016 또는 Windows Server 2012 R2 운영 체제에서 사용 하는 경우 지정 **시작 메모리**, **최소 메모리**, 및 **최대 메모리** 128 메가바이트 (MB)의 배수로 매개 변수입니다. 이렇게 하지 않으면 즉석 추가 오류를 발생할 수 있습니다 및 게스트 운영 체제의 증가 메모리 나타나지 않을 수 있습니다.

10. LIS 3.5 또는 LIS 4.0을 사용 하 여 포함 하 여, 특정 배포만 Ballooning 지원 하 고 핫 추가 지원을 제공 하지 않습니다. 이러한 시나리오에서는 동적 메모리 기능을 최대 메모리 매개 변수 값으로 시작 메모리 매개 변수를 설정 하 여 사용할 수 있습니다. 이 결과 부팅 시간 및 호스트의 메모리 요구 사항에 따라를 다음 나중에 가상 컴퓨터에 핫 추가 되는 모든 필수 메모리에 Hyper-v 수 자유롭게 할당 또는 Ballooning를 사용 하 여 게스트에서 메모리 할당을 취소 합니다. 구성 하십시오 **시작 메모리** 및 **최소 메모리** 이나 그 위에 분포에 대해 권장 되는 값입니다.

11. Oracle Linux Hyper-v 데몬 기본적으로 설치 되지 않습니다. 이러한 데몬을 사용 하려면 hyperv 데몬 패키지를 설치 합니다. 이 패키지가와 충돌 Linux 통합 서비스를 다운로드 하 고 다운로드 한 LIS 시스템에 설치 되지 않아야 합니다.

12. 키/값 쌍 (KVP) 인프라 없이 Linux 소프트웨어 업데이트가 제대로 작동 하지 않습니다. 이 기능으로는 문제를 참조 하는 경우 소프트웨어 업데이트를 다운로드 하려면 공급 업체에 문의 합니다.

13. OnWindows Server 2012 R2Generation 2 가상 컴퓨터는 기본적으로 사용 하도록 설정 하는 보안 부팅 및 일부 Linux 가상 컴퓨터에는 보안 부팅 옵션을 해제 하지 않는 한 부팅 되지 않습니다. 보안 부팅을 사용 하지 않도록 설정할 수는 **펌웨어** 섹션에 있는 가상 컴퓨터에 대 한 설정의 **Hyper-v 관리자** Powershell을 사용 하 여 비활성화할 수 있습니다.

    ```Powershell
    Set-VMFirmware -VMName "VMname" -EnableSecureBoot Off
    ```

    Linux Integration Services 다운로드 기존 세대 2 Vm에 적용할 수 있지만 2 세대 기능을 전달 하지 않습니다.

14. 가상 컴퓨터에서 지정 된 가상 네트워크 어댑터에 대 한 네트워크 관리자가 구성한 경우에 정적 IP 주입 작동 하지 않습니다. 고정 IP의 원활한 작동을 위해 주입 있는지 확인 하십시오 하거나 네트워크 관리자가 꺼져 완전히 또는 해당 ifcfg ethX 파일을 통해 특정 네트워크 어댑터에 대 한 해제 되었습니다.


관련 항목

* [Set-VMFirmware](https://technet.microsoft.com/library/dn464287.aspx)

* [CentOS 지원 및 Hyper-v Red Hat Enterprise Linux 가상 컴퓨터](Supported-CentOS-and-Red-Hat-Enterprise-Linux-virtual-machines-on-Hyper-V.md)

* [Hyper-V에서 지원되는 Debian 가상 머신](Supported-Debian-virtual-machines-on-Hyper-V.md)

* [Hyper-v에서 지원 되는 SUSE 가상 머신](Supported-SUSE-virtual-machines-on-Hyper-V.md)

* [Hyper-v에서 지원 되는 Ubuntu 가상 컴퓨터](Supported-Ubuntu-virtual-machines-on-Hyper-V.md)

* [Hyper-v에서 지원 되는 FreeBSD 가상 컴퓨터](Supported-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Hyper-v의 Linux 및 FreeBSD 가상 컴퓨터에 대 한 설명이](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Hyper-v에서 Linux를 실행 하는 것에 대 한 모범 사례](Best-Practices-for-running-Linux-on-Hyper-V.md)
