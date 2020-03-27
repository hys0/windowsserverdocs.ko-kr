---
title: 수렴 형 NIC에 대 한 물리적 스위치 구성
description: 이 항목에서는 물리적 스위치를 구성 하기 위한 지침을 제공 합니다.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 6d53c797-fb67-4b9e-9066-1c9a8b76d2aa
manager: dougkim
ms.author: lizross
author: eross-msft
ms.date: 09/14/2018
ms.openlocfilehash: 57fc944461254e78635913ac298bacc26a0789f2
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80309610"
---
# <a name="physical-switch-configuration-for-converged-nic"></a>수렴 형 NIC에 대 한 물리적 스위치 구성

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목에서는 물리적 스위치를 구성 하기 위한 지침을 제공 합니다. 


명령 및 해당 용도로만 사용 됩니다. 사용자 환경에서 Nic가 연결 되는 포트를 결정 해야 합니다. 

>[!IMPORTANT]
>SMB가 구성 된 우선 순위에 대해 VLAN 및 삭제 방지 정책이 설정 되어 있는지 확인 합니다.

## <a name="arista-switch-dcs-7050s-64-eos-4137m"></a>Arista 스위치 \(dc\-7050s\-64, EOS\-4.13.7 M\)

1.  en \(관리 모드로 이동 하 여 일반적으로 암호를 요청\)
2.  구성 모드로 전환 하는 구성 \(\)
3.  실행 \(표시 현재 실행 중인 구성을 표시\)
4.  Nic가 연결 된 스위치 포트를 확인 합니다. 이 예에서는 14/1, 15/1, 16/1, 17/1입니다.
5.  int eth 14/1, 15/1, 16/1, 17/1 \(이러한 포트에 대 한 구성 모드로 전환\)
6.  dcbx 모드 ieee
7.  우선 순위-흐름 제어 모드
8.  switchport 트렁크 native vlan 225
9.  switchport 트렁크 허용 vlan 100-225
10. switchport 모드 트렁크
11. 우선 순위-흐름 제어 우선 순위 3 삭제 안 함
12. qos 트러스트 co
13. 실행 \(표시 포트에서 구성이 올바르게 설정 되어 있는지 확인\)
14. wr \(스위치 다시 부팅 전체에서 설정이 유지 되도록\)

### <a name="tips"></a>팁:
1.  No #command # 부정 명령
2.  새 VLAN을 추가 하는 방법: 저장소 네트워크가 VLAN 100에 있는 경우 int vlan 100 \(\)
3.  기존 Vlan을 확인 하는 방법: vlan 표시
4.  Arista 스위치를 구성 하는 방법에 대 한 자세한 내용은 온라인 검색: Arista EOS 수동
5.  이 명령을 사용 하 여 PFC 설정을 확인 합니다. 우선 순위 흐름 제어 카운터 정보를 표시 합니다.

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

## <a name="cisco-switch-nexus-3132-version-602u61"></a>Cisco 스위치 \(Nexus 3132, 버전 6.0\(2\)U6 옆\(1\)\)

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
    

### <a name="port-specific"></a>포트 관련

    
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

- [단일 네트워크 어댑터를 사용 하 여 수렴 형 NIC 구성](cnic-single.md)
- [수렴 형 NIC 팀 NIC 구성](cnic-datacenter.md)
- [수렴 형 NIC 구성 문제 해결](cnic-app-troubleshoot.md)

--- 