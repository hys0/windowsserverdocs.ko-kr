---
title: "광고 숲 복구 Dc 남은 구슬"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adfs
ms.openlocfilehash: 66b0bc65b3b8e5dfbf5f1a85350dab60ac3a11c8
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="ad-forest-recovery---redeploy-remaining-dcs"></a>광고 숲 복구 Dc 남은 구슬

>Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 r 2에 적용 됩니다.

 이 지금까지 단계는 모든 숲에 적용: 유효한 백업을 각 도메인에 대 한, 격리에서 도메인 복구, 다시, 드, 초기화 찾아 정리 합니다. 다음이 단계에서 숲을 배포 됩니다. 이 작업을 수행 하는 방법은 됩니다 크게 숲 디자인, 수준 서비스 계약을 사이트 구조, 사용 가능한 대역폭 다양 한 요인에 따라 다릅니다. 디자인 원칙 및 제안을 여기서 비즈니스 요구에 가장 적합 한 하는 방식에서에 따라 고유한 재배포 계획 해야 합니다.  
  
 다음 단계에 숲 복구 발생 하기 전 포함 되어 있던 모든 Dc AD DS 설치 하는 것입니다. Dc 여전히 존재 AD DS 서비스 강제로, 제거 해야 하는 또는 Dc을 다시 설치할 수 있습니다. 해당 메타 데이터 숲 복구 하는 동안 제거 되었으므로이 Dc에 대 한 기존 백업은 다시 사용할 수 없습니다. 복잡 하지 않은 환경에서이 재배포 프로세스는 복구 Dc 프로덕션 네트워크에 다시 연결 하 고 필요에 따라 새로운 Dc 사항을 홍보 하기 위한 하기만 될 수 있습니다.  
  
 전 세계 인프라와 얼굴을 한 대기업, 계획을 더 정교 필요 합니다. 첫 번째 단계는 일반적으로 서비스로, 광고를 복원 하려면 이 따라서 전략적 설치 모든 중요 한 비즈니스 부서 및 응용 프로그램 작업을 다시 시작할 수 있도록 Dc 배치 합니다. 따라서 성능 줄였습니다 일시적으로을 지점에 적합 한 수 있습니다. 두 번째도 모든 남은 단계와 덜 중요 한 Dc 배포 됩니다.  
  
 자동는 추가 Dc 설치 두 가지가 있습니다.  
  
-   복제  
  
     Windows Server 2012를 실행 하는 가상화 환경에 대 한 복제 Dc 많은 복구할 수 있는 가장 빠르고 가장 간단한 방법은입니다. 단일 가상화 DC 백업에서 복원 된 후 도메인에 있는 모든 가상화 Dc 복구를 자동 수 있습니다.  
  
     복제 필수 구성 요소에 대 한 자세한 내용은 참조 [Active Directory Domain Services (AD DS) Virtualization (수준을 100) 소개](https://technet.microsoft.com/library/hh831734.aspx)합니다.  
  
-   Windows Server 2012 (또는 Windows Server의 이전 버전을 실행 하는 서버에 Dcpromo.exe)를 실행 하는 서버에서 Windows PowerShell를 사용 하 여 또는 사용자 인터페이스를 사용 하 여 AD DS 다시 설치  
  
     AD DS을 다시 설치를 신속 하는 설치 하는 동안 복제 사용량을 줄이기 위해 설치 미디어 (IFM) 옵션에서 사용할 수 있습니다. 사용에 대 한 자세한 내용은 **ntdsutil ifm** 설치 미디어를 만드는, 참조 명령을 [설치 AD DS 미디어에서](https://technet.microsoft.com/library/cc770654\(WS.10\).aspx)합니다.  
  
 다음과 같은 추가 지점을 수가 가장 각 복제본 DC 가상화 DC 복제 또는 (백업에서 복원) 반대 AD DS 설치로 숲에서 복구 되는 것이 좋습니다.  
  
-   Dc 복제 원본으로 사용 되는 모든 소프트웨어가 복제할 할 수 있어야 합니다. 응용 프로그램 및 서비스 복제할 수 없는 제거할지 복제을 시작 하기 전에 합니다. 수 없는 경우 원본으로 대체 가상화 DC 선택 해야 합니다.  
  
-   복원 하는 첫 번째 가상화 DC에서 추가 가상화 Dc을 복제할 소스 DC VHDX 파일 복사 되는 동안 종료 해야 합니다. 다음 복제 가상 Dc가 될 때 실행 되 고 사용 가능한 온라인 수 필요는 처음 시작 합니다. 작동 중지 종료 하 여 필요에 대 한 첫 번째 복구 DC 적합 하지 않은 경우 AD DS 역할을 복제할 소스를 설치 하 여 추가 가상화 DC을 배포 합니다.  
  
-   AD DS 설치 하려는 서버 또는 복제 가상화 DC의 호스트 이름에 제한이 있습니다. 새로운 호스트 이름이 나 이전에 사용 된 호스트 이름에 사용할 수 있습니다. DNS 호스트 이름 구문에 대 한 자세한 내용은 참조 [DNS 컴퓨터 이름을 만드는](https://technet.microsoft.com/library/cc785282.aspx) ([https://go.microsoft.com/fwlink/?LinkId=74564](https://go.microsoft.com/fwlink/?LinkId=74564)).  
  
-   네트워크 어댑터의 TCP/IP 속성에서 기본 설정된 DNS 서버 각 서버 (루트 도메인 복원 된 첫 번째 DC) 숲 속의 첫 번째 DNS 서버를 구성 합니다. 자세한 내용은 참조 [TCP/IP DNS 사용 하도록 구성](https://technet.microsoft.com/library/cc779282.aspx)합니다.  
  
-   여러 Rodc 중앙 위치에 배포 되는 경우 가상화 DC 복제 또는 제거한 AD DS 지사 같은 있는 격리 된 위치에서 개별적으로 배포 하는 경우 다시 설치 하 여 다시의 일반적인 방법으로 도메인에 있는 모든 Rodc을 배포 합니다.  
  
     Rodc 다시 지연 개체 포함 되어 있지 않으면 및 나중에 발생 복제 충돌을 방지 하는 데 도움이 될 수 있도록 보장 합니다. AD DS RODC에서 제거 *DC 메타 데이터를 유지 하도록 선택할*합니다. 이 옵션을 사용 하 여 RODC에 대 한 krbtgt 계정 유지 하 고 위임된 RODC 관리자 계정 및 암호 복제 정책 (PRP)에 대 한 사용 권한을 보유 하 고 사용자가 제거 하 고 rodc AD DS 설치 도메인 관리자 자격 증명을 사용 하는 데 하지 않도록 합니다. 또한 유지 DNS 서버 및 드 역할 원래 RODC에 설치 된 경우 됩니다.  
  
     Dc (Rodc 또는 쓰기 Dc)을 다시 작성 수 있으며 때 다시 설치 하는 동안 복제 교통 증가 합니다. 해당 영향을 줄이기 위해 RODC 설치 일정 분산 수 하 고 설치 IFM (미디어에서) 옵션을 사용할 수 있습니다. IFM 옵션을 사용 하는 경우 실행는 **ntdsutil ifm** 손상 된 데이터의 담은 신뢰할 수 있는 쓰기 DC 명령을 합니다. 이 손상을 AD DS 다시 설치를 완료 한 후 RODC에 표시 되지 않도록 방지할 수 있습니다. IFM에 대 한 자세한 내용은 참조 [미디어에서 설치 AD DS](https://technet.microsoft.com/library/cc770654\(WS.10\).aspx)합니다.  
  
     Rodc 다시 빌드에 대 한 자세한 내용은 참조 [RODC 제거 하 고 다시 설치](https://technet.microsoft.com/library/cc835490\(WS.10\).aspx)합니다.  
  
-   DC 된 숲 오류 하기 전에 DNS 서버 서비스를 실행 중인 경우 설치할 서비스 하 고 구성 DNS 서버 AD DS 설치 하는 동안 합니다. 그렇지 않은 경우 이전 DNS 클라이언트 다른 DNS 서버를 구성 합니다.  
  
-   글로벌 추가 카탈로그 인증 나 사용자 또는 응용 프로그램에 대 한 쿼리가 로드 공유 필요한 경우 원본에 드 복제 전에 DC 가상화 또는 AD DS 설치 하는 동안 드 서버 DC를 걸 수 있는 추가할 수 있습니다.  
  
## <a name="next-steps"></a>다음 단계
-   [광고 숲 복구 필수](AD-Forest-Recovery-Prerequisties.md)  
-   [사용자 지정 숲 복구 계획 고안-광고 숲 복구](AD-Forest-Recovery-Devising-a-Plan.md)  
- [광고 숲 복구-문제 식별](AD-Forest-Recovery-Identify-the-Problem.md)
-   [광고 숲 복구-복구 하는 방법을 확인](AD-Forest-Recovery-Determine-how-to-Recover.md)
-   [광고 숲 복구-초기 복구](AD-Forest-Recovery-Perform-initial-recovery.md)  
-   [광고 숲 복구 절차](AD-Forest-Recovery-Procedures.md)  
-   [광고 숲 복구-질문과 대답](AD-Forest-Recovery-FAQ.md)  
-   [광고 숲 복구-Multidomain 숲 내 단일 도메인 복구](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)  
-   [광고 숲 복구-Windows Server 2003 도메인 컨트롤러 관련 숲 복구](AD-Forest-Recovery-Windows-Server-2003.md)  