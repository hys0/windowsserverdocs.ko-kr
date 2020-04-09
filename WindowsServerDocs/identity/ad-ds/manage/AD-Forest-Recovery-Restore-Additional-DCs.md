---
title: AD 포리스트 복구-나머지 Dc 다시 배포
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adds
ms.openlocfilehash: 17e5ceec74277c888232d17adca5c2bbb305af97
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80823626"
---
# <a name="ad-forest-recovery---redeploy-remaining-dcs"></a>AD 포리스트 복구-나머지 Dc 다시 배포

>적용 대상: Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 R2

이 지점 까지의 단계는 모든 포리스트에 적용 됩니다. 즉, 각 도메인에 대 한 유효한 백업을 찾고, 격리 된 도메인을 복구 하 고, 다시 연결 하 여 글로벌 카탈로그를 다시 설정 하 고, 정리 합니다. 다음 단계에서는 포리스트를 다시 배포 합니다. 이 작업을 수행 하는 방법은 포리스트 디자인, 서비스 수준 계약, 사이트 구조, 사용 가능한 대역폭 및 기타 여러 요소에 따라 크게 달라 집니다. 비즈니스 요구 사항에 가장 적합 한 방식으로이 섹션의 원칙과 제안에 따라 고유한 재배포 계획을 디자인 해야 합니다.  
  
다음 단계는 포리스트 복구가 수행 되기 전에 존재 했던 모든 Dc에 AD DS를 설치 하는 것입니다. Dc가 있는 경우 AD DS 서비스를 강제로 제거 하거나 Dc를 다시 설치할 수 있어야 합니다. 포리스트 복구 중에 해당 메타 데이터가 제거 되었으므로 이러한 Dc의 모든 기존 백업을 다시 사용할 수 없습니다. 복잡 하지 않은 환경에서는 복구 된 Dc를 프로덕션 네트워크에 다시 연결 하 고 필요에 따라 새 Dc를 승격 하는 것 처럼 재배포 프로세스를 간단 하 게 수행할 수 있습니다.  
  
전 세계 인프라를 사용 하는 대기업에서는 보다 정교한 계획이 필요 합니다. 첫 번째 단계는 AD를 서비스로 복원 하는 것입니다. 즉, 모든 중요 한 사업부와 응용 프로그램이 작업을 다시 시작할 수 있도록 전략적으로 배치 된 Dc를 설치 합니다. 이로 인해 지점에서 일시적으로 성능이 저하 되는 것이 허용 될 수 있습니다. 두 번째 단계로, 남아 있고 중요 하지 않은 모든 Dc가 다시 배포 됩니다.  
  
 추가 Dc를 설치 하는 방법에는 두 가지가 있습니다. 두 방법 모두 자동화할 수 있습니다.  
  
- 복제  
   - Windows Server 2012를 실행 하는 가상화 된 환경의 경우 복제는 많은 수의 Dc를 복구 하는 가장 빠르고 간단한 방법입니다. 백업에서 가상화 된 단일 DC를 복원한 후 도메인에 있는 모든 가상화 된 Dc의 복구를 자동화할 수 있습니다.  
   - 복제 및 필수 구성 요소에 대 한 자세한 내용은 [Active Directory Domain Services (AD DS) 가상화 소개 (수준 100)](https://technet.microsoft.com/library/hh831734.aspx)를 참조 하세요.  
- Windows Server 2012 (또는 이전 버전의 Windows Server를 실행 하는 서버의 Dcpromo.exe) 또는 사용자 인터페이스를 사용 하 여 windows Server를 실행 하는 서버에서 Windows PowerShell을 사용 하 여 AD DS 다시 설치  
   - AD DS를 신속 하 게 다시 설치 하려면 IFM (미디어에서 설치) 옵션을 사용 하 여 설치 중에 복제 트래픽을 줄일 수 있습니다. **Ntdsutil ifm** 명령을 사용 하 여 설치 미디어를 만드는 방법에 대 한 자세한 내용은 [미디어에서 AD DS 설치](https://technet.microsoft.com/library/cc770654\(WS.10\).aspx)를 참조 하세요.  

백업에서 복원 하는 것과는 반대로, 가상화 된 DC 복제를 통해 또는 AD DS를 설치 하 여 포리스트에서 복구 되는 각 복제본 DC에 대해 다음과 같은 추가 사항을 고려 합니다.  
  
- 복제 원본으로 사용 되는 DC의 모든 소프트웨어는 복제할 수 있어야 합니다. 복제할 수 없는 응용 프로그램 및 서비스는 복제를 시작 하기 전에 제거 해야 합니다. 가능 하지 않은 경우 다른 가상화 된 DC를 원본으로 선택 해야 합니다.  
- 복원 하기 위해 첫 번째 가상화 된 DC에서 가상화 된 추가 Dc를 복제 하는 경우 VHDX 파일이 복사 되는 동안 원본 DC를 종료 해야 합니다. 그러면 복제 가상 Dc가 처음으로 시작 될 때 실행 중이 고 온라인으로 사용할 수 있어야 합니다. 첫 번째 복구 된 DC에 대해 종료에 필요한 가동 중지 시간을 사용할 수 없는 경우 복제를 위한 원본으로 작동 하도록 AD DS를 설치 하 여 가상화 된 추가 DC를 배포 합니다.  
- 복제 된 가상화 된 DC의 호스트 이름 또는 AD DS를 설치 하려는 서버에 대 한 제한은 없습니다. 이전에 사용 중인 새 호스트 이름 또는 호스트 이름을 사용할 수 있습니다. DNS 호스트 이름 구문에 대 한 자세한 내용은 [Dns 컴퓨터 이름 만들기](https://technet.microsoft.com/library/cc785282.aspx) ([https://go.microsoft.com/fwlink/?LinkId=74564](https://go.microsoft.com/fwlink/?LinkId=74564))를 참조 하십시오.  
- 포리스트의 첫 번째 DNS 서버 (루트 도메인에 복원 된 첫 번째 DC)를 사용 하 여 각 서버를 네트워크 어댑터의 TCP/IP 속성에 있는 기본 설정 DNS 서버로 구성 합니다. 자세한 내용은 [DNS를 사용 하도록 Tcp/ip 구성](https://technet.microsoft.com/library/cc779282.aspx)을 참조 하세요.  
- 여러 Rodc를 중앙 위치에 배포 하는 경우 가상화 된 DC 복제로 도메인의 모든 Rodc를 다시 배포 하거나, 지점 등의 격리 된 위치에 개별적으로 배포 하는 경우 AD DS를 제거 하 고 다시 설치 하 여 기존에 다시 작성 하는 방법으로 도메인의 모든 Rodc를 다시 배포 합니다.  
   - Rodc를 다시 빌드하면 느린 개체가 포함 되지 않으며 나중에 복제 충돌이 발생 하지 않도록 방지할 수 있습니다. RODC에서 AD DS를 제거 하는 경우 *DC 메타 데이터를 유지 하는 옵션을 선택*합니다. 이 옵션을 사용 하면 RODC에 대 한 krbtgt 계정이 유지 되 고 위임 된 RODC 관리자 계정 및 암호 복제 정책 (PRP)에 대 한 사용 권한이 유지 되며, RODC에서 AD DS을 제거 하 고 다시 설치 하는 데 도메인 관리자 자격 증명을 사용 하지 않아도 됩니다. 또한 원래 RODC에 설치 된 경우 DNS 서버 및 글로벌 카탈로그 역할을 유지 합니다.  
   - Dc (Rodc 또는 쓰기 가능 Dc)를 다시 작성 하는 경우 다시 설치 하는 동안 복제 트래픽이 증가할 수 있습니다. 이러한 영향을 줄이기 위해 RODC 설치 일정을 엇갈리게 지정할 수 있으며 IFM (미디어에서 설치) 옵션을 사용할 수 있습니다. IFM 옵션을 사용 하는 경우 신뢰 하는 쓰기 가능한 DC에서 **ntdsutil IFM** 명령을 실행 하 여 손상 된 데이터를 사용 하지 않도록 합니다. 이렇게 하면 AD DS 다시 설치가 완료 된 후 RODC에 손상이 나타나지 않도록 방지할 수 있습니다. IFM에 대 한 자세한 내용은 [미디어에서 AD DS 설치](https://technet.microsoft.com/library/cc770654\(WS.10\).aspx)를 참조 하세요.  
   - Rodc를 다시 작성 하는 방법에 대 한 자세한 내용은 [Rodc 제거 및 다시 설치](https://technet.microsoft.com/library/cc835490\(WS.10\).aspx)를 참조 하세요.  
- 포리스트 오작동 전에 DC가 DNS 서버 서비스를 실행 하 고 있는 경우 AD DS 설치 하는 동안 DNS 서버 서비스를 설치 하 고 구성 합니다. 그렇지 않으면 다른 DNS 서버를 사용 하 여 이전 DNS 클라이언트를 구성 합니다.  
- 사용자 또는 응용 프로그램에 대 한 인증 또는 쿼리 로드를 공유 하는 추가 글로벌 카탈로그가 필요한 경우 복제 하기 전에 원본 가상화 된 DC에 글로벌 카탈로그를 추가 하거나 AD DS 설치 하는 동안 DC를 글로벌 카탈로그 서버로 만들 수 있습니다.  
  
## <a name="next-steps"></a>다음 단계

- [AD 포리스트 복구 - 필수 조건](AD-Forest-Recovery-Prerequisties.md)  
- [AD 포리스트 복구-사용자 지정 포리스트 복구 계획 고안](AD-Forest-Recovery-Devising-a-Plan.md)  
- [AD 포리스트 복구-문제 식별](AD-Forest-Recovery-Identify-the-Problem.md)
- [AD 포리스트 복구-복구 방법을 결정 합니다.](AD-Forest-Recovery-Determine-how-to-Recover.md)
- [AD 포리스트 복구-초기 복구 수행](AD-Forest-Recovery-Perform-initial-recovery.md)  
- [AD 포리스트 복구 - 절차](AD-Forest-Recovery-Procedures.md)  
- [AD 포리스트 복구-질문과 대답](AD-Forest-Recovery-FAQ.md)  
- [AD 포리스트 복구-다중 도메인 포리스트 내에서 단일 도메인 복구](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)  
- [AD 포리스트 복구-Windows Server 2003 도메인 컨트롤러를 사용 하 여 포리스트 복구](AD-Forest-Recovery-Windows-Server-2003.md)
