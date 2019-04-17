---
title: NIC 팀 문제 해결
description: 이 항목에서는 Windows Server 2016에 NIC 팀 문제 해결에 대 한 정보를 제공 합니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-nict
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fdee02ec-3a7e-473e-9784-2889dc1b6dbb
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 634ec1a5eee0cd661ca89c2673e5b74abd458cd6
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="troubleshooting-nic-teaming"></a>NIC 팀 문제 해결

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 항목 NIC 팀, 문제 해결에 관한 정보를 제공 하 고의 NIC 팀 문제가 없음을 알 설명 하는 다음 섹션에 포함 되어 있습니다.  
  
-   [하드웨어 사양에 맞지 않는](#bkmk_hardware)  
  
-   [실제 스위치 보안 기능](#bkmk_switch)  
  
-   [사용 하지 않도록 설정 하 고 Windows PowerShell으로 사용](#bkmk_ps)  
  
## <a name="bkmk_hardware"></a>하드웨어 사양에 맞지 않는  
표준 프로토콜 하드웨어 구현 사양에 맞지 않는, NIC 팀 성능이 저하 될 수 있습니다.  
  
일반 작업 중 NIC 팀 보낼 수 있습니다 패킷을 동일한 IP 주소 로부터 아직 여러 다양 한 소스 미디어 액세스 제어 (MAC) 주소 합니다. 프로토콜 표준에 따라 이러한 패킷 수신기 패킷이 받았기 MAC 주소에 대 한 응답 하지 않고 특정 MAC 주소를 호스트 또는 VM의 IP 주소를 확인 해야 합니다.  올바른 대상 MAC 주소 (VM 또는 호스트 IP 주소를 소유 하 고 있는의 MAC 주소) 패킷을 제대로 IPv4의 주소 해상도 프로토콜 (ARP) 또는 IPv6의 이웃 검색 프로토콜 (NDP) 주소 해상도 프로토콜을 구현 하는 클라이언트 보냅니다.  
  
그러나 일부 하드웨어 내장, 올바르게를 구현 하지 않고 주소 해상도 프로토콜을도 해결 하지 못할 수도 명시적으로 IP 주소를 사용 하 여 ARP 또는 NDP MAC 주소를 합니다.  저장 공간 영역 네트워크 컨트롤러 이러한 방식으로 수행할 수 있는 디바이스의 예입니다. 장치를 하지 않은 준수 MAC 주소를 포함 하 여 원본 받은 패킷을에 복사한 대상에 해당 보내는 패킷 MAC 주소를 사용 합니다.  
  
따라서 패킷이 MAC 주소 잘못 목적지로 전송 됩니다. 모든 알려진된 대상 일치 하지 하기 때문에이 때문 패킷이 Hyper-v 가상 스위치 삭제 됩니다.  
  
시 문제가 발생 하는 데는 하드웨어에 포함 된 SAN 컨트롤러 또는 다른 연결, 패킷 캡처를 수행 하 고 ARP 또는 NDP, 하드웨어가 제대로 구현 여부를 결정와 하드웨어 제조업체에 지원을 요청 해야 합니다.  
  
## <a name="bkmk_switch"></a>실제 스위치 보안 기능  
구성에 따라 NIC 팀 보내어 패킷을 여러 다양 한 소스 MAC 주소와 동일한 IP 주소 로부터.  이 실제 스위치를 포트 팀의 일부는 없는 경우에 특히 실제 스위치 동적 ARP 검사 또는 IP 원본 등의 기능을 보호 보안을 여행 수 있습니다. 이 스위치 독립 모드 NIC 팀을 구성 하는 경우 발생할 수 있습니다.  스위치 보안 기능 NIC 팀와 연결 문제를 일으키는 여부를 확인 하기 위해 스위치 로그 조사 해야 합니다.  
  
## <a name="bkmk_ps"></a>사용 하지 않도록 설정 하 고 Windows PowerShell를 사용 하 여 네트워크 어댑터 사용  
실패 하는 NIC 팀에 대 한 일반적인 이유 팀 인터페이스를 사용할 수 없음을입니다. 대부분의 경우, 다음 Windows PowerShell 순서 대로 명령 실행 될 때 인터페이스 실수로 해제 됩니다.  
  
```  
Disable-NetAdapter *  
Enable-NetAdapter *  
```  
  
이 순서 명령 사용 하지 않도록 설정 하면 NetAdapters 모두 사용 되지 않습니다.  
  
NIC 팀 인터페이스 제거 되 고 더 이상 Get-NetAdapter에 표시를 사용 하면 모두 기본 물리적 구성원 Nic 비활성화 하기 때문입니다. 이 인해는 **사용 NetAdapter \ *** 명령은 어댑터를 제거 하기 때문에 NIC 팀을 설정 하지 않습니다.  
  
그러나 **사용 NetAdapter \ *** 명령 팀 인터페이스 만들어야 합니다 (잠시 후)는 회원 Nic, 활성화 하는 합니다. 이런이 경우 팀 인터페이스 다시 사용 하도록 설정 되지 않았으므로 때문에 여전히 "사용할 수 없습니다" 상태에에서는입니다. 다시는 후 팀 인터페이스를 사용 하면 다시 흐름을 시작 하려면 네트워크 교통을 수 있습니다.  
  
## <a name="see-also"></a>참조 하십시오  
[NIC 팀](NIC-Teaming.md)  
  


