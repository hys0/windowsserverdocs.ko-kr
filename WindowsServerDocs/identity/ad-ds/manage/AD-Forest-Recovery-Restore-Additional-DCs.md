---
title: AD 포리스트 복구-Dc 남은 재배포
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adds
ms.openlocfilehash: af9ec02a480b35e573edebcdd5928451174b6c1d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59812004"
---
# <a name="ad-forest-recovery---redeploy-remaining-dcs"></a>AD 포리스트 복구-Dc 남은 재배포

>적용 대상: Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 R2

이 시점까지 단계는 모든 포리스트에 적용: 각 도메인에 대 한 유효한 백업의 찾을, 격리 된 상태에서 도메인을 복구, 다시 연결, 글로벌 카탈로그를 다시 설정 및 정리 합니다. 다음 단계에서는 포리스트를 다시 배포 합니다. 포리스트 디자인, 서비스 수준 계약, 사이트 구조, 사용 가능한 대역폭 및 기타 다양 한 요인에이 작업을 수행 하는 방법은 크게 다릅니다. 디자인 원칙 및 비즈니스 요구 사항에 가장 적합 한 방식으로이 섹션에서는 제안에 따라 사용자 고유의 재배포 계획 해야 합니다.  
  
다음 단계는 포리스트 복구를 수행 하기 전에 있던 모든 Dc에서 AD DS를 설치 하는 것입니다. Dc가 여전히 존재 하는 경우 AD DS 서비스를 강제로 제거 해야 합니다. 또는 Dc를 다시 설치할 수 있습니다. 포리스트 복구 하는 동안 해당 메타 데이터 제거 되었으므로 이러한 Dc에 대 한 기존 백업은 다시 사용할 수 없습니다. 복잡 하지 않은 환경에서이 재배포 프로세스는 프로덕션 네트워크에 복구 된 Dc를 다시 연결 하 고 필요에 따라 새 Dc를 승격 처럼 간단할 수 있습니다.  
  
전 세계 인프라를 사용 하 여 직면 한 대기업에서는 보다 복잡 한 계획을 필요 합니다. 첫 번째 단계는 일반적으로; 서비스로 서 AD를 복원 하려면 이 즉, 전략적으로 설치 하는 모든 중요 한 비즈니스 사업부 및 응용 프로그램 작업을 다시 시작할 수 있도록 Dc를 배치 합니다. 일시적으로 성능 이렇게 제한 하는 지사 사무소에 허용 수도 있습니다. 두 번째 단계로 나머지 모든 단계와 덜 중요 한 Dc는 다시 배포 합니다.  
  
 자동화할 수 있는 추가 Dc를 설치 하는 방법은 두 가지가 있습니다.  
  
- 복제  
   - Windows Server 2012를 실행 하는 가상화 된 환경에 대 한 복제는 많은 수의 Dc 복구 하려면 가장 빠르고 가장 간단한 방법입니다. 백업에서 단일 가상화 된 DC를 복원한 후 도메인의 모든 가상화 된 Dc의 복구를 자동화할 수 있습니다.  
   - 복제 및 필수 구성 요소에 대 한 자세한 내용은 참조 하세요. [Introduction to Active Directory Domain Services (AD DS) Virtualization (Level 100)](https://technet.microsoft.com/library/hh831734.aspx)합니다.  
- Windows Server 2012 (또는 이전 버전의 Windows Server를 실행 하는 서버의 Dcpromo.exe)를 실행 하는 서버에서 Windows PowerShell을 사용 하 여 또는 사용자 인터페이스를 사용 하 여 AD DS를 다시 설치  
   - AD DS를 설치 하는 다시 신속 하 게 처리를 설치 하는 동안 복제 트래픽을 줄이기 위해 IFM (미디어) 옵션에서 설치를 사용할 수 있습니다. 사용에 대 한 자세한 내용은 합니다 **ntdsutil ifm** 내용은 설치 미디어를 만드는 명령을 [미디어에서 AD DS 설치](https://technet.microsoft.com/library/cc770654\(WS.10\).aspx)합니다.  

가상화 된 DC를 복제 하거나 백업에서 복원) 하는 것 (아닌 AD DS를 설치 하 여 포리스트의 복구 되는 각 복제본 DC에 대 한 다음 추가 사항을 고려 하세요.  
  
- 복제 원본으로 사용 되는 DC의 모든 소프트웨어는 복제할 수 있어야 합니다. 응용 프로그램 및 서비스 복제할 수 없는 복제를 시작 하기 전에 제거 해야 합니다. 가능 하지 않은 경우 대체 가상화 된 DC는 원본으로 선택 해야 합니다.  
- 복원할 첫 번째 가상화 된 DC에서 추가 가상화 된 Dc를 복제 원본 DC를 해당 VHDX 파일이 복사 되는 동안 종료 해야 합니다. 복제본 가상 Dc가 될 때 실행 되 고 사용할 수 있는 온라인 수 해야 먼저 시작 합니다. 가동 중지 시간 종료에 필요한 첫 번째 복구 된 DC에 대 한 허용 되지 않는 경우 복제 원본으로 작동 하도록 AD DS를 설치 하 여 추가 가상화 된 DC를 배포 합니다.  
- 복제 된 가상화 된 DC 또는 AD DS를 설치 하려는 서버의 호스트 이름에 제한이 있습니다. 새 호스트 이름 또는 이전에 사용에서 된 호스트 이름을 사용할 수 있습니다. DNS 호스트 이름 구문에 대 한 자세한 내용은 참조 하십시오 [만드는 DNS 컴퓨터 이름](https://technet.microsoft.com/library/cc785282.aspx) ([https://go.microsoft.com/fwlink/?LinkId=74564](https://go.microsoft.com/fwlink/?LinkId=74564)).  
- 네트워크 어댑터의 TCP/IP 속성에서 기본 설정 DNS 서버로 포리스트 (루트 도메인에 복원 된 첫 번째 DC) 첫 번째 DNS 서버를 사용 하 여 각 서버를 구성 합니다. 자세한 내용은 [DNS를 사용 하려면 TCP/IP 구성](https://technet.microsoft.com/library/cc779282.aspx)합니다.  
- 가상화 된 DC를 복제 하 여 여러 Rodc 중앙 위치에 배포 된 경우 또는 제거 하 고 있는 격리 된 위치에 개별적으로 배포 된 경우에 AD DS를 다시 설치 하 여 다시 작성 하는 기존의 방법으로 도메인의 모든 Rodc를 다시 배포 지사 예:.  
   - Rodc를 다시 작성는 느린 개체를 포함 하지 않습니다 및 나중에 발생에서 복제의 충돌을 방지 하는 데 도움이 되도록 합니다. RODC에서 AD DS를 제거 해도 *DC 메타 데이터를 유지 하는 옵션을 선택*합니다. RODC krbtgt 계정 유지 및 위임 된 RODC 관리자 계정 및은 정책 PRP (암호 복제)에 대 한 권한을 유지 하 고 도메인 관리자 자격 증명을 사용 하 여 제거 하 고에 AD DS를 설치 하지 않아도 사용 하면이 옵션을 사용 하 여 RODC 합니다. 또한 유지 DNS 서버와 글로벌 카탈로그 역할 RODC에 원래 설치 되어 있는 경우.  
   - Dc (Rodc 또는 쓰기 가능한 Dc)를 다시 작성, 있을 경우 다시 설치 하는 동안 복제 트래픽 증가 합니다. 영향을 줄이려면 RODC 설치의 일정을 엇갈리게 배치 수 및 설치에서 IFM (미디어) 옵션을 사용할 수 있습니다. IFM 옵션을 사용 하는 경우 실행 합니다 **ntdsutil ifm** 으로 손상 된 데이터를 신뢰할 수 있는 쓰기 가능한 DC에서 명령을 합니다. 이렇게 하면 AD DS 설치를 사용 하는 완료 된 후 RODC에서 표시 가능한 손상을 방지 합니다. IFM에 대 한 자세한 내용은 참조 하세요. [미디어에서 AD DS 설치](https://technet.microsoft.com/library/cc770654\(WS.10\).aspx)합니다.  
   - Rodc를 다시 작성 하는 방법에 대 한 자세한 내용은 참조 하세요. [RODC 제거 및 다시 설치](https://technet.microsoft.com/library/cc835490\(WS.10\).aspx)합니다.  
- DC가 포리스트 오작동 전에 DNS 서버 서비스를 실행 하는 경우 설치 하 고 AD DS 설치 하는 동안 DNS 서버 서비스를 구성 합니다. 그렇지 않으면 다른 DNS 서버를 사용 하 여 이전 DNS 클라이언트를 구성 합니다.  
- 인증 또는 사용자 또는 응용 프로그램에 대 한 쿼리 로드를 공유 하려면 추가 글로벌 카탈로그에 필요한 경우 원본에 글로벌 카탈로그 DC를 복제 하기 전에 가상화 또는 가능 DC를 글로벌 카탈로그 서버를 AD DS 설치 하는 동안 추가할 수 있습니다.  
  
## <a name="next-steps"></a>다음 단계

- [AD 포리스트 복구-필수 구성 요소](AD-Forest-Recovery-Prerequisties.md)  
- [사용자 지정 포리스트 복구 계획을 고안 AD 포리스트 복구-](AD-Forest-Recovery-Devising-a-Plan.md)  
- [AD 포리스트 복구 문제를 식별 합니다.](AD-Forest-Recovery-Identify-the-Problem.md)
- [AD 포리스트 Recovery-복구 하는 방법 결정](AD-Forest-Recovery-Determine-how-to-Recover.md)
- [AD 포리스트 복구-초기 복구를 수행 합니다.](AD-Forest-Recovery-Perform-initial-recovery.md)  
- [AD 포리스트 복구 절차](AD-Forest-Recovery-Procedures.md)  
- [AD 포리스트 복구-질문과 대답](AD-Forest-Recovery-FAQ.md)  
- [AD 포리스트 복구-Multidomain 포리스트에 단일 도메인 복구](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)  
- [AD 포리스트 복구-Windows Server 2003 도메인 컨트롤러를 사용 하 여 포리스트 복구](AD-Forest-Recovery-Windows-Server-2003.md)
