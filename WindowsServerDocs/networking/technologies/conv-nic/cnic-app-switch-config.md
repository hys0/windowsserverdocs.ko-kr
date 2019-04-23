---
title: 수렴 된 NIC에 대 한 물리적 스위치 구성
description: 이 항목에서는 제공 하면 지침을 사용 하 여 물리적 스위치를 구성 합니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 6d53c797-fb67-4b9e-9066-1c9a8b76d2aa
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/14/2018
ms.openlocfilehash: e31d7b83fee84d9055d938f77b49389205786244
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829404"
---
# <a name="physical-switch-configuration-for-converged-nic"></a>수렴 된 NIC에 대 한 물리적 스위치 구성

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 항목에서는 제공 하면 지침을 사용 하 여 물리적 스위치를 구성 합니다. 


여기에 명령 및 해당 용도로 사용 됩니다. 사용자 환경에서 Nic 연결 되어 있는 포트를 결정 합니다. 

>[!IMPORTANT]
>SMB는 구성 된 우선 순위에 대 한 VLAN 및 놓기 없음 정책 설정 되어 있는지 확인 합니다.

## <a name="arista-switch-dcs-7050s-64-eos-4137m"></a>Arista 스위치 \(dcs\-7050s\-64 EOS\-4.13.7M\)

1.  en \(관리자 모드로 전환, 일반적으로 암호 요청\)
2.  config \(구성 모드를 입력 합니다.\)
3.  실행 표시 \(현재 실행 중인 구성을 보여 줍니다.\)
4.  Nic에는 연결 하는 스위치 포트에 대해 알아봅니다. 이러한 예제에서는 이러한 속성은 14/1,15/1,16/1,17/1입니다.
5.  int eth 14/1,15/1,16/1,17/1 \(이러한 포트에 대 한 구성 모드로 입력\)
6.  dcbx 모드 ieee
7.  모드의 경우 우선 순위 흐름 제어
8.  switchport 트렁크 기본 vlan 225
9.  switchport 트렁크 vlan 100 225 허용
10. switchport 모드 트렁크
11. 우선 순위 흐름 제어 우선 순위 3 놓기 못함
12. cos qos 신뢰
13. 실행 표시 \(해당 구성이 포트에 올바르게 설치 확인\)
14. 쓰기 \(스위치 재부팅 간에 유지 설정 하려면\)

### <a name="tips"></a>팁:
1.  없는 #command # 명령의 부정합니다.
2.  새 VLAN을 추가 하는 방법: int vlan 100 \(저장소 네트워크 VLAN 100 이면\)
3.  기존 Vlan을 확인 하는 방법: vlan 표시
4.  Arista 스위치를 구성 하는 방법에 대 한 자세한 내용은 온라인 검색: Arista EOS 수동
5.  이 명령을 사용 하 여 PFC 설정을 확인 합니다: 우선 순위 흐름 제어 카운터 세부 정보를 표시 합니다.

--- 

## <a name="dell-switch-s4810-ftos-99-00"></a>Dell 스위치 \(S4810, FTOS 9.9 \(0.0\)\)

    
    !
    dcb enable
    ! put pfc control on qos class 3
    configure
    dcb-map dcb-smb
    priority group 0 bandwidth 90 pfc on
    priority group 1 bandwidth 10 pfc off
    priority-pgid 1 1 1 0 1 1 1 1
    exit
    ! apply map to ports 0-31
    configure
    interface range ten 0/0-31
    dcb-map dcb-smb
    exit
    
--- 

## <a name="cisco-switch-nexus-3132-version-602u61"></a>Cisco 스위치 \(Nexus 3132 버전 6.0\(2\)U6\(1\)\)

### <a name="global"></a>전역
    
    class-map type qos match-all RDMA
    match cos 3
    class-map type queuing RDMA
    match qos-group 3
    policy-map type qos QOS_MARKING
    class RDMA
    set qos-group 3
    class class-default
    policy-map type queuing QOS_QUEUEING
    class type queuing RDMA
    bandwidth percent 50
    class type queuing class-default
    bandwidth percent 50
    class-map type network-qos RDMA
    match qos-group 3
    policy-map type network-qos QOS_NETWORK
    class type network-qos RDMA
    mtu 2240
    pause no-drop
    class type network-qos class-default
    mtu 9216
    system qos
    service-policy type qos input QOS_MARKING
    service-policy type queuing output QOS_QUEUEING
    service-policy type network-qos QOS_NETWORK
    

### <a name="port-specific"></a>특정 포트

    
    switchport mode trunk
    switchport trunk native vlan 99
    switchport trunk allowed vlan 99,2000,2050   çuse VLANs that already exists
    spanning-tree port type edge
    flowcontrol receive on (not supported with PFC in Cisco NX-OS)
    flowcontrol send on (not supported with PFC in Cisco NX-OS)
    no shutdown
    priority-flow-control mode on
    
--- 

## <a name="related-topics"></a>관련 항목

- [단일 네트워크 어댑터로 수렴 형 된 NIC 구성](cnic-single.md)
- [수렴 형 된 NIC 팀으로 구성 된 NIC 구성](cnic-datacenter.md)
- [수렴 형 NIC 구성 문제 해결](cnic-app-troubleshoot.md)

--- 