---
title: NIC 팀 MAC 주소 사용 및 관리
description: 이 항목에서는 Windows Server 2016에 (MAC) 주소 NIC 팀에서는 미디어 액세스 제어 하는 방법에 대 한 정보를 제공 합니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-nict
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 26d105e0-afc3-44b5-bb5e-0c884a4c5d62
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 6ab624665c964b100e6b1ed633120299b55e37df
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="nic-teaming-mac-address-use-and-management"></a>NIC 팀 MAC 주소 사용 및 관리

>Windows Server 2016 적용 됩니다.

NIC 팀 독립 모드로 전환 하 고 주소 해시 또는 동적 부하 분산을 구성할 때 미디어 액세스 팀에서는 기본 NIC 팀 멤버 아웃 바운드 교통량 (MAC) 주소를 제어 합니다. 기본 NIC 팀 멤버 팀원의 초기 설정에서 운영 체제에서 선택한 네트워크 어댑터입니다.  
  
기본 팀원을 만든 다음 하거나 호스트 컴퓨터를 다시 시작한 후 팀에 연결 하려면 첫 번째 팀원이입니다. 각 부팅 시 명확 하지 않은 방법으로 주 팀원 수 변하므로 NIC 사용 작업 또는 기타 재구성 활동 기본 팀원 변경 하 고 팀의 MAC 주소 수 다를 수 있습니다.  
  
대부분의 경우가 문제를 인해 하지 않는 경우에는 몇 가지 문제가 발생할 수 있습니다.  
  
기본 팀원 팀에서 제거 하 고 다음 작업에 배치 MAC 주소 충돌 있을 수 있습니다. 이 충돌을 해결를 해제 한 다음 팀 인터페이스를 설정 합니다. 사용 하지 않도록 설정 하 고 다음 팀 인터페이스 사용할 수 있게 하는 과정에서 남은 팀원을 MAC 주소 충돌이 발생 하지 않게 새로운 MAC 주소를 선택 하 고 인터페이스를 하면 됩니다.  
  
하도록 설정할 수 있습니다 NIC 팀의 MAC 주소 특정 MAC 주소를 기본 팀 인터페이스를 설정 하 여 모든 물리적 NIC.의 MAC 주소를 구성할 때 할 수 있는 것 처럼  
  
## <a name="mac-address-use-on-transmitted-packets"></a>전송된 패킷을에 MAC 주소 사용  
NIC 팀 독립 모드로 전환 하 고 주소 해시 또는 동적 부하 분산을 구성할 때 (예: 단일 VM) 원천에서 패킷은 동시에 여러 팀원에서 배포 됩니다. 스위치 혼란 하지 않도록 하 고 알람을 퍼 덕 MAC 방지 MAC 주소 소스에서 기본 팀원 이외의 팀원에 전송 된 프레임 다른 MAC 주소를으로 대체 됩니다. 이 때문 각 팀원 다른 MAC 주소를 사용 하 고 MAC 주소 충돌 하지 않으면 및 오류가 발생할 때까지 수 없습니다.  
  
오류가 기본으로 만들기 NIC에서 감지 되 면 NIC 팀 소프트웨어 역할 임시 기본 팀 멤버 (즉, 이제 텍스트 주 팀 멤버와 스위치를 하나)을 선택 하는 팀 멤버에 기본 팀 멤버의 MAC 주소를 사용 하 여 시작 합니다.  이러한 변경 MAC 주소 원본으로 주 팀 멤버의 MAC 주소를 가진 기본 팀원 보낼 진행 된 교통에만 적용 됩니다. 다른 교통 계속 어떤 소스 MAC 주소 오류가 발생 하기 전에 사용 하는 것으로 전송 합니다.  
  
다음은 목록을 팀은 어떻게 구성 되어 있는지에 따라 NIC 팀 MAC 주소 교체 동작을 설명 하는 다음과 같습니다.  
  
1.  **주소 해시 배포와 함께 스위치 독립 모드**  
  
    -   모든 ARP 및 NS 패킷은 기본 팀원에서 보낸  
  
    -   기본 팀원 이외의 Nic 전송 된 모든 소통 전송 되는 NIC 일치 하도록 수정 소스 MAC 주소와 함께 보낼  
  
    -   기본 팀원 전송 된 모든 소통 원본 (팀의 MAC 주소 소스 될 수 있음)는 MAC 주소를 전송  
  
2.  **Hyper-v 포트 배포와 함께 스위치 독립 모드**  
  
    -   팀 멤버 모든 vmSwitch 포트는 관련  
  
    -   모든 패킷이 팀원을 포트는 관련된에 전송  
  
    -   완료 MAC 교체 소스가 없습니다.  
  
3.  **동적 배포와 함께 스위치 독립 모드**  
  
    -   팀 멤버 모든 vmSwitch 포트는 관련  
  
    -   모든 ARP/NS 패킷은 있는 포트는 관련된 팀원에서 보낸  
  
    -   관련된 팀원 있는 팀원 보낸 패킷을 MAC 주소 교체 완료 소스가 없습니다.  
  
    -   관련된 팀원 이외의 팀원 보낸 패킷을 소스 MAC 주소 교체 완료는  
  
4.  **종속 스위치 모드로 (모든 배포)**  
  
    -   수행 MAC 주소 교체 소스가 없습니다.  
  
## <a name="see-also"></a>참조 하십시오  
[새 NIC 팀 호스트 컴퓨터 또는 VM 만들기](Create-a-New-NIC-Team-on-a-Host-Computer-or-VM.md)  
[NIC 팀](NIC-Teaming.md)  
  


