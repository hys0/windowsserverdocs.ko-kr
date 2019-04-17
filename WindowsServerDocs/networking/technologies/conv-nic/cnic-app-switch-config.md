---
title: 실제 스위치 구성 집약 nic
description: 이 항목은 Windows Server 2016 용 수렴 NIC 구성 가이드의 일부입니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 6d53c797-fb67-4b9e-9066-1c9a8b76d2aa
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 98a2e249aea38bd4d07dc1bcbc9b1ca98b98b6d6
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="physical-switch-configuration-for-converged-nic"></a>실제 스위치 구성 집약 nic

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

실제 스위치를 구성에 대 한 지침을 다음 섹션에서는 사용할 수 있습니다.

이들은 명령 및 사용 합니다. 귀하의 환경에 연결 되어 있는 Nic 포트를 확인 해야 합니다. 

>[!IMPORTANT]
>아니요 놓기 정책 고 VLAN는 SMB 구성 우선 순위를 설정 되어 있는지 확인 합니다.

## <a name="arista-switch-dcs-7050s-64-eos-4137m"></a>Arista 스위치 \ (dcs\ 7050s\-64, EOS\-4.13.7M\)

1.  En \ (관리자 모드로 전환, 일반적으로 password\ 요청)
2.  구성 \ 구성 mode\에 입력) (하려면
3.  실행 표시 \ (현재 실행 중인 configuration\ 표시)
4.  스위치 포트에 연결 되어 있는 사용자 Nic 알아봅니다. 이러한 예에서는 14 일 1,15/1,16/1,17/1.
5.  14 일 1,15/1,16/1,17/1 int eth \ (이러한 ports\에 대 한 구성 모드로 입력)
6.  Dcbx 모드 ieee
7.  우선 순위가 흐름 제어 모드
8.  Switchport 트렁크 기본 vlan 225
9.  Switchport 트렁크 vlan 100-225 허용
10. Switchport 모드 트렁크
11. 우선 순위 흐름 제어 우선 순위 3 아니요 놓기
12. Qos 신뢰 cos
13. 실행 표시 \ (해당 구성 올바르게 설정 되어 있는 ports\에서 확인)
14. Wr \ (설정을 간에 지속 스위치 reboot\)

### <a name="tips"></a>팁:
1.  없음 #command # 부정 명령
2.  새 VLAN 추가 하는 방법: int vlan 100 \ (저장 네트워크는 VLAN 100\) 하는 경우
3.  기존 Vlan 확인 하는 방법: vlan 표시
4.  Arista 스위치를 구성 하는 방법에 대 한 자세한 내용은 온라인 검색에 대 한: Arista EOS 설명서
5.  이 명령을 사용 하 여 PFC 설정을 확인 하려면: 우선 순위 흐름 제어 카운터를 이해도

## <a name="dell-switch-s4810-ftos-99-00"></a>Dell 스위치 \ (S4810, FTOS 9.9 \(0.0\)\)

    
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
    

## <a name="cisco-switch-nexus-3132-version-602u61"></a>Cisco 스위치 \ (원활한 연결 3132, 버전 6.0\(2\)U6\(1\)\)

### <a name="global"></a>전 세계
    
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
    

### <a name="port-specific"></a>포트 특정

    
    switchport mode trunk
    switchport trunk native vlan 99
    switchport trunk allowed vlan 99,2000,2050   çuse VLANs that already exists
    spanning-tree port type edge
    flowcontrol receive on (not supported with PFC in Cisco NX-OS)
    flowcontrol send on (not supported with PFC in Cisco NX-OS)
    no shutdown
    priority-flow-control mode on
    

## <a name="all-topics-in-this-guide"></a>이 가이드의 모든 항목

이 가이드는 다음 항목이 포함 되어 있습니다.

- [단일 네트워크 어댑터를 사용 하 여 집약된 NIC 구성](cnic-single.md)
- [집약된 NIC 어댑터당된 NIC 구성](cnic-datacenter.md)
- [실제 스위치 구성 집약 nic](cnic-app-switch-config.md)
- [NIC 구성 수렴 문제 해결](cnic-app-troubleshoot.md)
