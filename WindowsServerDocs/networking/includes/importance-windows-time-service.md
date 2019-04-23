---
author: shortpatti
ms.author: pashort
ms.date: 10/02/2018
ms.prod: windows-server-threshold
ms:topic: include
ms.openlocfilehash: 4e8e3234b89630bf16148eef644f0c6607ad38bd
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852344"
---
## <a name="importance-of-time-protocols"></a>시간 프로토콜의 중요성
시간 프로토콜 시간 정보를 교환 하 고 다음 정보를 사용 하 여 시계를 동기화 하려면 두 컴퓨터 간에 통신 합니다. Windows 시간 서비스 시간 프로토콜을 사용 하 여 클라이언트가 서버에서 시간 정보를 요청 하 고 수신 되는 정보를 기반으로 해당 클록을 동기화 합니다.
  
Windows 시간 서비스 NTP를 사용 하 여 네트워크를 통해 시간을 동기화 하는 데 있습니다. NTP 시계를 동기화 하는 데 필요한 분야 알고리즘을 포함 하는 인터넷 시간 프로토콜입니다. NTP은 보다 정확한 시간 프로토콜 보다는 네트워크 시간 프로토콜 SNTP () Windows;의 일부 버전에 사용 되는 그러나 W32Time 계속 SNTP Windows 2000 같은 시간 대의 SNTP 기반 서비스를 실행 하는 컴퓨터를 사용 하 여 이전 버전과 호환성을 사용 하도록 지원 합니다.

여러 가지 이유가 정확한 시간이 필요할 수 있습니다.  Windows에 대 한 일반적인 경우에는 정확도 클라이언트와 서버 간에 5 분을 필요로 하는 Kerberos입니다.  그러나는 정확도 등을 비롯 하 여 영향을 받을 수 있는 다른 여러 영역이 있습니다.


- 정부 규제 선택:
    - 미국에서 FINRA에 대 한 50ms 정확도
    - 1 ms ESMA (MiFID II) EU에 있습니다.
- 암호화 알고리즘
- 문서 Db 및 클러스터/SQL/Exchange 같은 분산된 시스템
- Bitcoin 트랜잭션에 대 한 Blockchain 프레임 워크
- 분산된 로그 및 위협 분석 
- AD 복제
- PCI (Payment 카드 업계), 현재 1 두 번째 정확도