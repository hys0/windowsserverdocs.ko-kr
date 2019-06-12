---
title: Hyper-v에 FreeBSD를 실행 하기 위한 모범 사례
description: FreeBSD virtual machines에서 실행 하기 위한 권장 사항을 제공 합니다.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0c66f1c8-2606-43a3-b4cc-166acaaf2d2a
author: shirgall
ms.author: kathydav
ms.date: 01/09/2017
ms.openlocfilehash: 6320ceb86093146592a54ab34b013f334f43ddb4
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447768"
---
# <a name="best-practices-for-running-freebsd-on-hyper-v"></a>Hyper-v에 FreeBSD를 실행 하기 위한 모범 사례

>적용 대상: Windows Server 2016에서 Hyper-v Server 2016, Windows Server 2012 R2, Hyper-V Server 2012 R2, Windows Server 2012 Hyper-V Server 2012, Windows Server 2008 R2, Windows 10, Windows 8.1, Windows 8, Windows 7.1, Windows 7

이 항목에서는 Hyper-v 가상 머신에서 게스트 운영 체제로 FreeBSD를 실행 하기 위한 권장 사항 목록이 포함 되어 있습니다.

## <a name="enable-carp-in-freebsd-102-on-hyper-v"></a>Hyper-v에 FreeBSD 10.2에서에서 CARP를 사용 하도록 설정

공용 주소 중복 프로토콜 (CARP)를 사용 하면 동일한 IP 주소를 공유할 수 있는 여러 호스트와 하나 이상의 서비스에 대 한 고가용성을 제공 하려면 가상 호스트 ID (VHID). 하나 이상의 호스트 실패, 다른 호스트로 투명 하 게 인계 사용자가 서비스 오류 알 수 있도록 합니다. CARP FreeBSD 10.2에서를 사용 하려면의 지침에 따라 합니다 [FreeBSD handbook](https://www.freebsd.org/doc/en/books/handbook/carp.html) Hyper-v 관리자에서 다음을 수행 합니다.

* 가상 컴퓨터에 네트워크 어댑터와 가상 스위치가 할당을 확인 합니다. 가상 컴퓨터를 선택 하 고 선택 **작업** > **설정을**합니다.

![선택한 네트워크 어댑터를 사용 하 여 가상 컴퓨터 설정의 스크린샷](media/Hyper-V_Settings_NetworkAdapter.png)

* MAC 주소 스푸핑을 사용 하도록 설정 합니다. 이렇게 하려면

   1. 가상 컴퓨터를 선택 하 고 선택 **작업** > **설정을**합니다.

   2. 확장 **네트워크 어댑터** 선택한 **고급 기능**합니다.

   3. 선택 **사용 하도록 설정 하는 MAC 주소 스푸핑**합니다.

## <a name="create-labels-for-disk-devices"></a>디스크 장치에 대 한 레이블 만들기

시작 하는 동안 새 장치는 검색 된 것으로 장치 노드가 만들어집니다. 이 새 장치가 추가 되 면 장치 이름을 변경할 수 의미할 수 있습니다. 시작 하는 동안 루트 탑재 오류를 받게 되 면 변경 하 고 충돌을 방지 하려면 각 IDE 파티션에 대 한 레이블을 만들어야 합니다. 자세한 내용은 [디스크 장치 레이블 지정](https://www.freebsd.org/doc/handbook/geom-glabel.html)합니다. 다음은 예제입니다. 

> [!IMPORTANT]
> 변경 하기 전에 프로그램 fstab의 백업 복사본을 확인 합니다.

1. 단일 사용자 모드로 시스템을 재부팅 합니다. FreeBSD 10.3 +에 대 한 부팅 메뉴 옵션 2를 선택 하 여이 수행할 수 있습니다 (FreeBSD에 대 한 옵션 4 8.x), 또는 부팅 프롬프트에서 '부팅-s'를 수행 합니다.

2. 단일 사용자 모드에서 프로그램 fstab (루트 및 swap)에 나열 된 IDE 디스크 파티션의 각 트림 레이블을 만듭니다. FreeBSD 10.3의 예는 다음과 같습니다.

   ```bash
   # cat  /etc/fstab
   # Device           Mountpoint      FStype  Options   Dump   Pass#
   /dev/da0p2         /               ufs     rw        1       1
   /dev/da0p3         none            swap    sw        0       0

   # glabel  label rootfs  /dev/da0p2
   # glabel  label swap   /dev/da0p3
   # exit
   ```

   트림 레이블에 대 한 추가 정보에서 찾을 수 있습니다. [디스크 장치 레이블 지정](https://www.freebsd.org/doc/handbook/geom-glabel.html)합니다.

3. 시스템은 다중 사용자 부팅을 사용 하 여 계속 합니다. 부팅에는 다음이 완료 되 면 /etc/fstab을 편집 및 해당 레이블은 기존 장치 이름을 바꿉니다. 최종 /etc/fstab이 같이 표시 됩니다.

   ```
   # Device                Mountpoint      FStype  Options         Dump    Pass#
   /dev/label/rootfs       /               ufs     rw              1       1
   /dev/label/swap         none            swap    sw              0       0
   ```

4. 시스템을 재부팅 이제 수 있습니다. 모든 잘 진행 하면 대로 일반적으로 하 고 탑재 표시 됩니다.

   ```
   # mount
   /dev/label/rootfs on / (ufs, local, journaled soft-updates)
   devfs on /dev (devfs, local, mutilabel)
   ```

## <a name="use-a-wireless-network-adapter-as-the-virtual-switch"></a>무선 네트워크 어댑터를 가상 스위치와 사용

호스트의 가상 스위치를 무선 네트워크 어댑터를 기반으로 하는 경우 시간을 줄일 ARP 만료 60 초는 다음 명령으로. 그렇지 않은 경우 VM의 네트워킹은 잠시 후 작업을 중지할 수 있습니다.


```
   # sysctl net.link.ether.inet.max_age=60
```


참조

* [Hyper-v에서 지원 되는 FreeBSD 가상 컴퓨터](Supported-FreeBSD-virtual-machines-on-Hyper-V.md)
