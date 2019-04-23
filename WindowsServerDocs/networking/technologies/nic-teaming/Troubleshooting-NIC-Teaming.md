---
title: NIC 팀 문제 해결
description: 이 항목에서는 Windows Server 2016에서 NIC 팀 문제 해결에 대 한 정보를 제공 합니다.
manager: dougkim
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
ms.date: 09/13/2018
ms.openlocfilehash: d39dc6a4dcf5dca8186b0599fb479ed5ae684e0f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856254"
---
# <a name="troubleshooting-nic-teaming"></a>NIC 팀 문제 해결

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 항목에서는 하드웨어 등 물리적 스위치 securities NIC 팀 문제를 해결 하는 방법을 설명 합니다.  표준 프로토콜 구현의 하드웨어 사양을 따르지 않는, NIC 팀 성능이 저하 될 수 있습니다. 또한 구성에 따라 NIC 팀에서 보낼 수 있습니다 패킷을 물리적 스위치에 보안 기능을 방해 하는 여러 MAC 주소를 사용 하 여 동일한 IP 주소입니다.

  
## <a name="hardware-that-doesnt-conform-to-specification"></a>사양에 맞지 않은 하드웨어  
  
정상적인 작업 중 NIC 팀에서 보낼 수 있습니다 패킷을 아직 여러 MAC 주소를 사용 하 여 동일한 IP 주소를 합니다. 프로토콜 표준에 따라 이러한 패킷의 수신자는 받는 패킷의 MAC 주소에 응답 하는 것이 아니라 특정 MAC 주소에 호스트 또는 VM의 IP 주소를 해결 해야 합니다.  주소 확인 프로토콜 (ARP 및 NDP)을 올바르게 구현 하는 클라이언트에 올바른 대상 MAC 주소를 사용 하 여 모드 해제 패킷 보내기-즉, VM 또는 해당 IP 주소를 소유 하는 호스트의 MAC 주소입니다. 
  
일부 포함 된 하드웨어 주소 확인 프로토콜을 올바르게 구현 하지 않는 없으며도 될 수 있습니다 명시적으로 확인 되지 IP 주소를 NDP 또는 ARP를 사용 하 여 MAC 주소입니다.  예를 들어 저장소 영역 네트워크 (SAN) 컨트롤러는이 방식으로 수행할 수 있습니다. 비 준수 장치 받은 패킷의 원본 MAC 주소를 복사 및 잘못 된 대상 MAC 주소에 전송 중인 패킷의 결과, 해당 나가는 패킷의 대상 MAC 주소를 사용 합니다. 따라서 알려진된 모든 대상 일치 하지 않으면 때문에 패킷은 Hyper-v 가상 스위치에 의해 삭제 됩니다.  
  
하는 경우 문제가 포함 된 하드웨어를 SAN 컨트롤러 또는 다른 연결, ARP 나를 NDP 하드웨어가 제대로 구현 하는 경우를 결정 하는 패킷 캡처를 수행 하 고 하드웨어 공급 업체에 지원을 요청 해야 합니다.  

  
## <a name="physical-switch-security-features"></a>실제 스위치 보안 기능  
구성에 따라 NIC 팀에서 보낼 수 있습니다 패킷을 물리적 스위치에 보안 기능을 방해 하는 여러 원본 MAC 주소를 사용 하 여 동일한 IP 주소입니다. 예를 들어 동적 ARP 검사 또는 IP 원본 가드를 실제 전환 하는 경우에 특히 않습니다 포트, 스위치 독립 모드에서 NIC 팀을 구성할 때 발생 하는 팀에 소속 됩니다. 보안 기능 스위치 연결 문제를 일으키는지를 확인 하려면 스위치 로그를 검사 합니다. 
  
## <a name="disabling-and-enabling-network-adapters-by-using-windows-powershell"></a>사용 하지 않도록 설정 하 고 Windows PowerShell을 사용 하 여 네트워크 어댑터를 사용 하도록 설정  

팀 인터페이스를 사용 하지 않으면 실패 NIC 팀에 대 한 일반적인 이유는 일련의 명령 실행 하는 경우 실수로 경우가 많습니다.  이 특정 명령 시퀀스는 모든 NIC 팀 인터페이스를 제거 하의 모든 Nic의 기본 실제 멤버를 사용 하지 않도록 설정 하므로 사용 하지 않도록 설정 NetAdapters 활성화 되지 않습니다. 

이 경우 NIC 팀 인터페이스를 더 이상 표시 되지 Get NetAdapter에이 인해 **Enable NetAdapter \***  NIC 팀을 사용 하도록 설정 하지 않습니다. 그러나 **사용 NetAdapter \***  명령, 사용 하도록 설정 멤버 Nic를 팀 인터페이스를 다시 만듭니다. 그런 다음 (짧은 시간 후)입니다. 될 때까지 "사용 안 함된" 상태로 유지 됩니다 팀 인터페이스를 다시 사용 하도록 설정, 네트워크 트래픽 흐름이 시작을 허용 합니다. 

다음 Windows PowerShell 명령 시퀀스는 실수로 팀 인터페이스를 비활성화할 수 있습니다.  
  
```PowerShell 
Disable-NetAdapter *  
Enable-NetAdapter *  
```  
  

  
## <a name="related-topics"></a>관련 항목  
- [NIC 팀](NIC-Teaming.md): 이 항목에서는 개요를 제공 네트워크 인터페이스 카드 (NIC) 팀의 Windows Server 2016에서. 1과 32 사이 그룹화 할 수 있습니다 NIC 팀 하나 이상의 소프트웨어 기반 가상 네트워크 어댑터에 실제 이더넷 네트워크 어댑터입니다. 이 가상 네트워크 어댑터에는 빠른 성능과 네트워크 어댑터 오류 발생 시 내결함성을 제공합니다.   

- [NIC 팀 MAC 주소 사용 및 관리](NIC-Teaming-MAC-Address-Use-and-Management.md): 스위치 독립 모드 주소 해시 또는 동적 부하 분산을 사용 하 여 NIC 팀을 구성한 경우 미디어 액세스 팀에서는 아웃 바운드 트래픽에 대해 기본 NIC 팀 구성원의 (MAC) 주소를 제어 합니다. 기본 NIC 팀 멤버가 팀 멤버의 초기 집합에서 운영 체제에서 선택한 네트워크 어댑터입니다.

- [NIC 팀 설정](nic-teaming-settings.md): 이 항목에서는 팀 같은 NIC 팀 속성의 개요를 제공 하 고 부하 분산 모드. 또한 제공 대기 어댑터 설정 및 기본 팀 인터페이스 속성에 대 한 세부 정보입니다. NIC 팀을 두 개 이상의 네트워크 어댑터가 있는 경우 내결함성을 위해 대기 어댑터를 지정할 필요가 없습니다.
  


