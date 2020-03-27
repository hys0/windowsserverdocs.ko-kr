---
title: NIC 팀 문제 해결
description: 이 항목에서는 Windows Server 2016의 NIC 팀 문제 해결에 대 한 정보를 제공 합니다.
manager: dougkim
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-nict
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fdee02ec-3a7e-473e-9784-2889dc1b6dbb
ms.author: lizross
author: eross-msft
ms.date: 09/13/2018
ms.openlocfilehash: 75b6ae2f2c7d6b4ab28aaedcc7309ccba3dcbd02
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80316376"
---
# <a name="troubleshooting-nic-teaming"></a>NIC 팀 문제 해결

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목에서는 하드웨어 및 물리적 스위치와 같은 NIC 팀 문제를 해결 하는 방법에 대해 설명 합니다.  표준 프로토콜의 하드웨어 구현이 사양을 따르지 않는 경우 NIC 팀 성능이 영향을 받을 수 있습니다. 또한 구성에 따라, NIC 팀은 여러 MAC 주소를 사용 하 여 동일한 IP 주소에서 패킷을 전송 하 여 실제 스위치의 보안 기능을 강화할 수 있습니다.

  
## <a name="hardware-that-doesnt-conform-to-specification"></a>사양을 준수 하지 않는 하드웨어  
  
정상적인 작업 중에는 NIC 팀이 동일한 IP 주소에서 여러 MAC 주소를 사용 하 여 패킷을 보낼 수 있습니다. 프로토콜 표준에 따라 이러한 패킷의 수신자는 수신 패킷에서 MAC 주소에 응답 하지 않고 특정 MAC 주소에 대 한 호스트 또는 VM의 IP 주소를 확인 해야 합니다.  주소 확인 프로토콜 (ARP 및 NDP)을 올바르게 구현 하는 클라이언트는 올바른 대상 MAC 주소 (즉, 해당 IP 주소를 소유 하는 VM 또는 호스트의 MAC 주소)로 패킷을 보냅니다. 
  
일부 임베디드 하드웨어는 주소 확인 프로토콜을 올바르게 구현 하지 않으며 ARP 또는 NDP를 사용 하 여 IP 주소를 MAC 주소로 명시적으로 확인 하지 못할 수도 있습니다.  예를 들어 SAN (저장 영역 네트워크) 컨트롤러는 이런 방식으로 수행할 수 있습니다. 순응 하지 않는 장치는 수신 된 패킷에서 원본 MAC 주소를 복사한 다음 해당 나가는 패킷에서 대상 MAC 주소로 사용 하 여 패킷이 잘못 된 대상 MAC 주소로 전송 되도록 합니다. 이 때문에 Hyper-v 가상 스위치가 알려진 대상과 일치 하지 않기 때문에 패킷이 해당 패킷을 삭제 합니다.  
  
SAN 컨트롤러나 기타 포함 된 하드웨어에 연결 하는 데 문제가 있는 경우 패킷 캡처를 사용 하 여 하드웨어가 ARP 또는 NDP를 올바르게 구현 하는지 확인 하 고 하드웨어 공급 업체에 지원을 요청 하세요.  

  
## <a name="physical-switch-security-features"></a>물리적 스위치 보안 기능  
구성에 따라, NIC 팀은 여러 원본 MAC 주소를 사용 하 여 동일한 IP 주소에서 패킷을 전송 하 여 실제 스위치의 보안 기능을 강화할 수 있습니다. 예를 들어 동적 ARP 검사 또는 IP 원본 가드, 특히 물리적 스위치에서 포트가 팀에 속해 있음을 인식 하지 못하는 경우 스위치 독립 모드에서 NIC 팀을 구성할 때 발생 합니다. 스위치 로그를 검사 하 여 스위치 보안 기능으로 인해 연결 문제가 발생 하는지 확인 합니다. 
  
## <a name="disabling-and-enabling-network-adapters-by-using-windows-powershell"></a>Windows PowerShell을 사용 하 여 네트워크 어댑터 사용 안 함 및 사용  

NIC 팀이 실패 하는 일반적인 이유는 팀 인터페이스를 사용 하지 않도록 설정 하는 것입니다. 대부분의 경우 명령 시퀀스를 실행 하는 경우 실수로 인해 발생 합니다.  Nic의 기본 실제 구성원을 모두 사용 하지 않도록 설정 하면 NIC 팀 인터페이스가 제거 되기 때문에 이러한 특정 명령 시퀀스는 사용 하지 않도록 설정 된 모든 NetAdapters를 사용 하도록 설정 하지 않습니다. 

이 경우 NIC 팀 인터페이스는 더 이상 Get-netadapter에 표시 되지 않으며,이로 인해 **get-netadapter \\** *는 nic 팀을 사용 하도록 설정 하지 않습니다. 그러나 **get-netadapter \\** * 명령은 멤버 nic를 사용 하도록 설정 하지만 (잠시 후) 팀 인터페이스를 다시 만듭니다. 팀 인터페이스는 다시 사용 하도록 설정 될 때까지 "사용 안 함" 상태로 유지 되므로 네트워크 트래픽이 전달 되기 시작 합니다. 

다음 Windows PowerShell 명령 시퀀스는 우연히 팀 인터페이스를 사용 하지 않도록 설정할 수 있습니다.  
  
```PowerShell 
Disable-NetAdapter *  
Enable-NetAdapter *  
```  
  

  
## <a name="related-topics"></a>관련 항목  
- [Nic 팀](NIC-Teaming.md):이 항목에서는 Windows Server 2016의 Nic (네트워크 인터페이스 카드) 팀에 대 한 개요를 제공 합니다. NIC 팀을 사용 하면 32 하나 이상의 실제 이더넷 네트워크 어댑터 간에 하나 이상의 소프트웨어 기반 가상 네트워크 어댑터로 그룹화 할 수 있습니다. 이 가상 네트워크 어댑터에는 빠른 성능과 네트워크 어댑터 오류 발생 시 내결함성을 제공합니다.   

- [Nic 팀 MAC 주소 사용 및 관리](NIC-Teaming-MAC-Address-Use-and-Management.md): 스위치 독립 모드를 사용 하 여 nic 팀을 구성 하 고 주소 해시 또는 동적 부하 분산을 사용 하는 경우 팀에서 아웃 바운드 트래픽에 대 한 기본 nic 팀 구성원의 MAC (미디어 액세스 제어) 주소를 사용 합니다. 기본 NIC 팀 구성원은 초기 팀 구성원 집합에서 운영 체제에 의해 선택 된 네트워크 어댑터입니다.

- [Nic 팀 설정](nic-teaming-settings.md):이 항목에서는 팀 및 부하 분산 모드와 같은 NIC 팀 속성에 대 한 개요를 제공 합니다. 또한 대기 어댑터 설정 및 주 팀 인터페이스 속성에 대 한 세부 정보도 제공 합니다. NIC 팀에 네트워크 어댑터가 두 개 이상 있는 경우 내결함성을 위해 대기 어댑터를 지정할 필요가 없습니다.
  


