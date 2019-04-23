---
author: shortpatti
ms.author: pashort
ms.date: 10/02/2018
ms.prod: windows-server-threshold
ms:topic: include
ms.openlocfilehash: d1bfc74c4daa751e3081b26c87dd0d2c88f5f095
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59879854"
---
대기 어댑터에 대 한 옵션은 **없음 (모든 어댑터 활성)** 또는 Standby 어댑터로 작동 하는 NIC 팀에서 특정 네트워크 어댑터를 선택 합니다. 대기 어댑터로 NIC를 구성한 경우 다른 모든 선택 되지 않은 팀 멤버는 활성 및 네트워크 트래픽이 전송 되었거나 활성 NIC를 실패할 때까지 어댑터에서 처리 합니다. 활성 NIC를 실패 한 후에 대기 NIC 활성화 되 고 네트워크 트래픽 프로세스입니다. 모든 팀 멤버 가져오기 서비스를 복원할 때 대기 상태로 대기 팀 멤버를 반환 합니다.  