---
title: Hyper-v의 Linux 및 FreeBSD 가상 머신에 대 한 기능 설명
description: 가상 머신에서 Linux 및 FreeBSD를 사용 하는 경우 네트워킹, 저장소, 메모리 등의 핵심 구성 요소에 영향을 주는 기능을 설명 합니다.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a9ee931d-91fc-40cf-9a15-ed6fa6965cb6
author: shirgall
ms.author: kathydav
ms.date: 10/03/2016
ms.openlocfilehash: 1690230d326d7e32175ccde5da1e5fae421a76d0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71366802"
---
# <a name="feature-descriptions-for-linux-and-freebsd-virtual-machines-on-hyper-v"></a>Hyper-v의 Linux 및 FreeBSD 가상 머신에 대 한 기능 설명

>적용 대상: Windows Server 2016, Hyper-v Server 2016, Windows Server 2012 R2, Hyper-v server 2012 R2, Windows Server 2012, Hyper-v Server 2012, Windows Server 2008 R2, Windows 10, Windows 8.1, Windows 8, Windows 7.1, Windows 7

이 문서에서는 가상 머신에서 Linux 및 FreeBSD를 사용할 때 코어, 네트워킹, 저장소, 메모리 등의 구성 요소에서 사용할 수 있는 기능을 설명 합니다.

## <a name="core"></a>Core

|**기능**|**설명**|
|-|-|
|통합 종료|이 기능을 사용 하면 관리자가 Hyper-v 관리자에서 가상 컴퓨터를 종료할 수 있습니다. 자세한 내용은 참조 [운영 체제 종료](https://technet.microsoft.com/library/dn798297(WS.11).aspx#BKMK_Shutdown)합니다.|
|시간 동기화|이 기능을 사용 하면 가상 머신 내에서 유지 관리 되는 시간이 호스트에서 유지 관리 되는 시간과 동기화 된 상태로 유지 됩니다. 자세한 내용은 참조 [시간 동기화](https://technet.microsoft.com/library/dn798297(WS.11).aspx#BKMK_time)합니다.|
|Windows Server 2016 정확한 시간|이 기능을 통해 게스트는 Windows Server 2016 정확한 시간 기능을 사용할 수 있으므로 호스트와의 시간 동기화를 1ms 정확도가 향상 됩니다. 자세한 내용은 [Windows Server 2016 정확한 시간](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-2016-accurate-time) 을 참조 하세요.|
|다중 처리 지원|이 기능을 사용 하면 가상 컴퓨터에서 여러 가상 Cpu를 구성 하 여 호스트에서 여러 프로세서를 사용할 수 있습니다.|
|하트비트|이 기능을 사용 하면 호스트에서 가상 컴퓨터의 상태를 추적할 수 있습니다. 자세한 내용은 참조 [하트 비트](https://technet.microsoft.com/library/dn798297(WS.11).aspx#BKMK_heartbeat)합니다.|
|통합 마우스 지원|이 기능을 사용 하면 가상 컴퓨터의 바탕 화면에서 마우스를 사용할 수 있으며 가상 컴퓨터의 Windows Server 데스크톱과 Hyper-v 콘솔 간에 마우스를 원활 하 게 사용할 수 있습니다.|
|Hyper-v 특정 저장 장치|이 기능은 가상 컴퓨터에 연결 된 저장 장치에 대 한 고성능 액세스를 부여 합니다.|
|Hyper-v가 특정 네트워크 장치|이 기능은 가상 컴퓨터에 연결 된 네트워크 어댑터에 대 한 고성능 액세스를 부여 합니다.|

## <a name="networking"></a>네트워킹

|**기능**|**설명**|
|-|-|
|Jumbo 프레임|이 기능을 사용 하면 관리자가 1500 바이트를 초과 하는 네트워크 프레임의 크기를 늘릴 수 있으므로 네트워크 성능이 크게 향상 됩니다.|
|VLAN 태깅 및 트렁킹|이 기능을 사용 하면 가상 컴퓨터에 대 한 가상 LAN (VLAN) 트래픽을 구성할 수 있습니다.|
|실시간 마이그레이션|이 기능을 사용 하면 한 호스트에서 다른 호스트로 가상 컴퓨터를 마이그레이션할 수 있습니다. 자세한 내용은 [가상 컴퓨터 실시간 마이그레이션 개요](https://technet.microsoft.com/library/hh831435.aspx)를 참조 하세요.|
|고정 IP 삽입|이 기능을 사용 하면 다른 호스트의 복제본으로 장애 조치 (failover) 된 후 가상 컴퓨터의 고정 IP 주소를 복제할 수 있습니다. 이러한 IP 복제는 장애 조치 (failover) 이벤트가 발생 한 후 네트워크 워크 로드가 계속 원활 하 게 작동 되도록 합니다.|
|vRSS (가상 수신측 배율)|가상 네트워크 어댑터의 부하를 가상 컴퓨터의 여러 가상 프로세서에 분산 합니다. 자세한 내용은 [Windows Server 2012 r 2의 가상 수신측 배율](https://technet.microsoft.com/library/dn383582.aspx)(영문)을 참조 하세요.|
|TCP 조각화 및 체크섬 오프 로드|네트워크 데이터를 전송 하는 동안 게스트 CPU에서 호스트 가상 스위치 또는 네트워크 어댑터로의 조각화 및 체크섬 작업을 전송 합니다.|
|큰 오프 로드 (LRO)를 수신 합니다.|CPU 오버 헤드 감소, 더 큰 버퍼로 여러 패킷으로 집계 하 여 고대역폭 연결의 인바운드 처리량이 늘어납니다.|
|SR-IOV|단일 루트 i/o 장치는 DDA를 사용 하 여 대기 시간이 줄어들고 처리량이 증가 하도록 하는 특정 NIC 카드의 일부에 대 한 게스트 액세스를 허용 합니다. SR-IOV를 사용 하려면 게스트의 호스트 및 virtual function (VF) 드라이버에서 최신 PF (물리적 함수) 드라이버가 필요 합니다.|

## <a name="storage"></a>스토리지

|**기능**|**설명**|
|-|-|
|VHDX 크기 조정|관리자는이 기능을 사용 하 여 가상 컴퓨터에 연결 된 고정 크기 .vhdx 파일의 크기를 조정할 수 있습니다. 자세한 내용은 참조 [온라인 가상 하드 디스크 크기 조정 개요](https://technet.microsoft.com/library/dn282286.aspx)합니다.|
|가상 파이버 채널|이 기능을 통해 가상 머신은 파이버 채널 장치를 인식 하 고 기본적으로 탑재할 수 있습니다. 자세한 내용은 참조 [Hyper-v 가상 파이버 채널 개요](https://technet.microsoft.com/library/hh831413.aspx)합니다.|
|라이브 가상 머신 백업|이 기능을 통해 실시간 가상 컴퓨터의 가동 중지 시간을 줄일 수가 있습니다.<br /><br />가상 컴퓨터에 SMB (서버 메시지 블록) 공유 또는 iSCSI 볼륨과 같은 원격 저장소에서 호스트 되는 Vhd (가상 하드 디스크)가 있는 경우 백업 작업이 실패 합니다. 또한 백업 대상이 백업 하는 볼륨과 동일한 볼륨에 존재 하지 않는지 확인 합니다.|
|TRIM 지원|트리밍 힌트는 이전에 할당 된 특정 섹터가 앱에서 더 이상 필요 하지 않으며 제거할 수 있음을 드라이브에 알립니다. 이 프로세스는 일반적으로 응용 프로그램에서 파일을 통해 많은 공간을 할당 한 다음 파일에 대 한 할당을 자체 관리 (예: 가상 하드 디스크 파일) 할 때 사용 됩니다.|
|SCSI WWN|Storvsc 드라이버에서 포트 및 가상 컴퓨터에 연결 된 장치는 노드 이름 WWN (World Wide) 정보를 추출 하 고 적절 한 sysfs 파일을 만듭니다. |

## <a name="memory"></a>메모리

|**기능**|**설명**|
|-|-|
|PAE 커널 지원|실제 주소 PAE (확장) 기술을 통해 4GB 보다 큰 실제 주소 공간에 액세스 하는 32 비트 커널을 있습니다. RHEL 같은 기존 Linux 배포 5.x PAE 사용 하도록 설정 된 별도 커널에 제공 하는 데 사용 합니다. 새로운 배포 RHEL 같은 6.x 미리 구축한 PAE 지원 합니다.|
|MMIO 간격 구성|이 기능을 사용 하 여 어플라이언스 제조업체는 메모리 매핑된 i/o (MMIO) 간격의 위치를 구성할 수 있습니다. MMIO 간격은 일반적으로 어플라이언스의 충분 한 운영 체제 (JeOS)와 어플라이언스를 구동 하는 실제 소프트웨어 인프라 간에 사용 가능한 실제 메모리를 나누는 데 사용 됩니다.|
|동적 메모리-즉석 추가|호스트 수 동적으로 늘리거나 가상 컴퓨터에 사용할 수 있는 메모리의 양을 작업 중인 동안. 프로 비전 하기 전에 관리자가 가상 컴퓨터 설정 패널의 동적 메모리를 사용 하 고 가상 컴퓨터에 대 한 시작 메모리, 최소 메모리 및 최대 메모리를 지정 합니다. 가상 컴퓨터 인 경우 동적 메모리를 해제할 수 없는 작업 및 최소값 및 최대값 설정을 변경할 수 있습니다. (것은 128MB의 배수로으로 이러한 메모리 크기를 지정 하는 것이 좋습니다.)<br /><br />가상 컴퓨터를 먼저 사용할 수 있는 시작할 때 메모리와 같은지를 **시작 메모리**합니다. 응용 프로그램 작업으로 인해 메모리 수요가 증가 하면 커널 해당 버전에서 지원 되는 경우 Hyper-v Hot-add 메커니즘을 통해 가상 컴퓨터에 메모리를 할당할 동적으로 수 있습니다. 값에 의해 할당 된 메모리의 최대 크기는 제한 된 **최대 메모리** 매개 변수입니다.<br /><br />Hyper-v 관리자의 메모리 탭에는 가상 컴퓨터에 할당 된 메모리의 양을 표시 됩니다 하지만 가상 컴퓨터 내에서 메모리 통계 최고 할당 된 메모리 양이 표시 됩니다.<br /><br />자세한 내용은 참조 [Hyper-v 동적 메모리 개요](https://technet.microsoft.com/library/hh831766.aspx)합니다.<br /><br />|
|동적 메모리-Ballooning|호스트 수 동적으로 늘리거나 가상 컴퓨터에 사용할 수 있는 메모리의 양을 작업 중인 동안. 프로 비전 하기 전에 관리자가 가상 컴퓨터 설정 패널의 동적 메모리를 사용 하 고 가상 컴퓨터에 대 한 시작 메모리, 최소 메모리 및 최대 메모리를 지정 합니다. 가상 컴퓨터 인 경우 동적 메모리를 해제할 수 없는 작업 및 최소값 및 최대값 설정을 변경할 수 있습니다. (것은 128MB의 배수로으로 이러한 메모리 크기를 지정 하는 것이 좋습니다.)<br /><br />가상 컴퓨터를 먼저 사용할 수 있는 시작할 때 메모리와 같은지를 **시작 메모리**합니다. 응용 프로그램 작업으로 인해 메모리 수요가 증가 하면 Hyper-v Hot-add 메커니즘 (위 참조)을 통해 가상 컴퓨터에 더 많은 메모리를 동적으로 할당할 수 있습니다. 메모리 수요가 감소 하는 대로 Hyper-v 수 자동으로 프로 비전을 해제 풍선 메커니즘을 통해 가상 컴퓨터에서 메모리입니다. Hyper-v는 프로 비전을 해제할 메모리 아래는 **최소 메모리** 매개 변수입니다.<br /><br />Hyper-v 관리자의 메모리 탭에는 가상 컴퓨터에 할당 된 메모리의 양을 표시 됩니다 하지만 가상 컴퓨터 내에서 메모리 통계 최고 할당 된 메모리 양이 표시 됩니다.<br /><br />자세한 내용은 참조 [Hyper-v 동적 메모리 개요](https://technet.microsoft.com/library/hh831766.aspx)합니다.<br /><br />|
|런타임 메모리 크기 조정|관리자가 설정할 수 사용 가능한 메모리 양을 가상 컴퓨터에 작업 중인 ("핫" 추가) 하는 메모리 증가 또는 감소 ("핫 제거"). 메모리가 풍선 드라이버를 통해 Hyper-v로 반환 됩니다 ("동적 메모리-Ballooning" 참조). 풍선 드라이버는 "바닥" 이라고 하는 ballooning 후에 사용 가능한 최소 메모리를 유지 하므로 할당 된 메모리는 현재 수요와이 층 크기에 따라 감소할 수 없습니다. Hyper-v 관리자의 메모리 탭에는 가상 컴퓨터에 할당 된 메모리의 양을 표시 됩니다 하지만 가상 컴퓨터 내에서 메모리 통계 최고 할당 된 메모리 양이 표시 됩니다. (것은 여러 128MB의 메모리 값을 지정 하는 것이 좋습니다.)|

## <a name="video"></a>비디오

|**기능**|**설명**|
|-|-|
|Hyper-v 관련 비디오 장치|이 기능은 가상 컴퓨터에 대 한 고성능 그래픽과 뛰어난 해상도를 제공 합니다. 이 장치는 고급 세션 모드 또는 RemoteFX 기능을 제공 하지 않습니다.|

## <a name="miscellaneous"></a>기타

|**기능**|**설명**|
|-|-|
|KVP (키-값 쌍) 교환|이 기능은 가상 컴퓨터에 대 한 KVP (키/값 쌍) exchange 서비스를 제공 합니다. 일반적으로 관리자는 KVP 메커니즘을 사용 하 여 가상 머신에서 사용자 지정 데이터 읽기 및 쓰기 작업을 수행 합니다. 자세한 내용은 [Data 교환: 키-값 쌍을 사용 하 여 Hyper-v @ no__t에서 호스트 및 게스트 간에 정보를 공유 합니다.|
|마스크 불가능 인터럽트|이 기능을 사용 하면 관리자가 가상 컴퓨터에 대 한 비 마스크 인터럽트 (NMI)를 실행할 수 있습니다. NMIs는 응용 프로그램 버그로 인해 응답 하지 않는 운영 체제의 크래시 덤프를 가져오는 데 유용 합니다. 를 다시 시작한 후에 이러한 크래시 덤프를 진단할 수 있습니다.|
|호스트에서 게스트로 파일 복사|이 기능을 사용 하면 네트워크 어댑터를 사용 하지 않고 호스트 물리적 컴퓨터에서 게스트 가상 컴퓨터로 파일을 복사할 수 있습니다. 자세한 내용은 참조 [게스트 서비스](https://technet.microsoft.com/library/dn798297(WS.11).aspx#BKMK_guest)합니다.|
|lsvmbus 명령|이 명령은 lspci와 같은 정보 명령과 유사한 Hyper-v 가상 컴퓨터 버스 (VMBus)의 장치에 대 한 정보를 가져옵니다.|
|Hyper-v 소켓|호스트 및 게스트 운영 체제 간에 추가 통신 채널입니다. 로드 하 고 Hyper-v 소켓 커널 모듈을 사용 하 여, 참조 [통합 서비스를 직접 만들](https://msdn.microsoft.com/virtualization/hyperv_on_windows/develop/make_mgmt_service)합니다.|
|PCI 통과/DDA|Windows Server 2016 불연속 장치 할당 메커니즘을 통해 관리자는 PCI Express 장치를 통해 전달할 수 있습니다. 일반적인 장치는 네트워크 카드, 그래픽 카드 및 특수 저장 장치입니다. 가상 컴퓨터에 노출 된 하드웨어를 사용 하 여 적절 한 드라이버가 필요 합니다. 하드웨어를 사용할 수 있도록 가상 컴퓨터에 할당 되어야 합니다.<br /><br />자세한 내용은 참조 [불연속 장치 할당-설명 및 배경](https://blogs.technet.microsoft.com/virtualization/2015/11/19/discrete-device-assignment-description-and-background/)합니다.<br /><br />DDA는 SR-IOV 네트워킹에 대 한 필수 조건입니다. 가상 포트는 가상 컴퓨터에 할당 해야 하 고 가상 컴퓨터 장치 멀티플렉싱에 대 한 올바른 VF (가상 함수) 드라이버를 사용 해야 합니다.|

## <a name="generation-2-virtual-machines"></a>2세대 가상 컴퓨터

|**기능**|**설명**|
|-|-|
|UEFI를 사용 하 여 부팅|이 기능을 사용 하면 UEFI (UEFI(Unified Extensible Firmware Interface))를 사용 하 여 가상 컴퓨터를 부팅할 수 있습니다.<br /><br />자세한 내용은 [2세대 가상 컴퓨터 개요](https://technet.microsoft.com/library/dn282285.aspx)를 참조하십시오.|
|보안 부팅|이 기능을 사용 하면 가상 머신에서 UEFI 기반 보안 부팅 모드를 사용할 수 있습니다. 가상 컴퓨터가 보안 모드로 부팅 되 면 UEFI 데이터 저장소에 있는 서명을 사용 하 여 다양 한 운영 체제 구성 요소가 확인 됩니다.<br /><br />자세한 내용은 [보안 부팅](https://technet.microsoft.com/library/dn486875.aspx)을 참조하세요.|

## <a name="see-also"></a>관련 항목

* [Hyper-v에서 지원 되는 CentOS 및 Red Hat Enterprise Linux 가상 컴퓨터](Supported-CentOS-and-Red-Hat-Enterprise-Linux-virtual-machines-on-Hyper-V.md)

* [Hyper-V에서 지원되는 Debian 가상 머신](Supported-Debian-virtual-machines-on-Hyper-V.md)

* [Hyper-v에서 지원 되는 Oracle Linux 가상 컴퓨터](Supported-Oracle-Linux-virtual-machines-on-Hyper-V.md)

* [Hyper-v에서 지원 되는 SUSE 가상 컴퓨터](Supported-SUSE-virtual-machines-on-Hyper-V.md)

* [Hyper-v에서 지원 되는 Ubuntu 가상 머신](Supported-Ubuntu-virtual-machines-on-Hyper-V.md)

* [Hyper-v에서 지원 되는 FreeBSD 가상 컴퓨터](Supported-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Hyper-v에서 Linux를 실행 하기 위한 모범 사례](Best-Practices-for-running-Linux-on-Hyper-V.md)

* [Hyper-v에서 FreeBSD 실행에 대 한 모범 사례](Best-practices-for-running-FreeBSD-on-Hyper-V.md)