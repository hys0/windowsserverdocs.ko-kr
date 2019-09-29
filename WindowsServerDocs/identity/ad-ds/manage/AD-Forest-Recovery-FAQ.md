---
title: AD 포리스트 복구 - FAQ
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: ac9e5a3d-8b1e-41b7-8e02-f64b7acf1359
ms.technology: identity-adds
ms.openlocfilehash: 49cd12621c6ddf89393f0463e4856555ca241491
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71369106"
---
# <a name="ad-forest-recovery---faq"></a>AD 포리스트 복구 - FAQ

>적용 대상: Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 R2, Windows Server 2003

이 문서에는 포리스트 복구와 관련 된 Faq (질문과 대답)가 포함 되어 있습니다.  

## <a name="general-recovery"></a>일반 복구

**대답 복구 속도를 높이기 위해 수행할 수 있는 작업은 무엇 인가요?**

복구 속도는이 가이드의 주요 목표가 아니지만 다음과 같은 방법으로 복구 시간을 단축할 수 있습니다.  
  
- 자세한 포리스트 복구 계획을 만들고, 정기적으로 업데이트 하 고, 1 년에 한 번 이상 적절 한 크기의 시뮬레이션 된 테스트 환경에서이를 연습 합니다.  
- 가상화 된 DC (도메인 컨트롤러) 복제 사용  
   - 가상화 된 DC 복제는 각 도메인의 백업에서 하나의 DC가 복원 된 후 추가 Dc를 실행 하는 프로세스를 신속 하 게 합니다. 설치가 완료 될 때까지 시간이 오래 AD DS 걸릴 수 있으며 설치가 완료 되 면 중요 하지 않은 복제가 완료 될 때까지 대기 하지 않고 가상화 된 추가 Dc를 복제할 수 있습니다.  
   - 가상 Dc가 상대적으로 적은 수의 잘 연결 된 데이터 센터에서 호스트 되는 포리스트는 복구 중 복제에서 가장 많은 이점을 누릴 수 있습니다. 그러나 동일한 도메인에 대해 여러 가상화 된 Dc가 동일한 하이퍼바이저 호스트에 동일한 위치에 배치 되는 환경은 이익이 됩니다.  
- Rodc (읽기 전용 도메인 컨트롤러) 배포  
   - Rodc는 쓰기 가능한 Dc에서 네트워크와의 연결을 끊을 필요가 없기 때문에 복구 프로세스 동안 비즈니스 연속성을 제공할 수 있습니다. Rodc는 아웃 바운드 복제를 수행 하지 않습니다. 따라서 쓰기 가능 Dc가 손상 된 데이터를 복구 된 환경으로 다시 복제 하는 것과 동일한 위험을 제공 하지는 않습니다.  
  
포리스트 복구 프로세스의 기간에 영향을 주는 다른 요소는 다음과 같습니다.  
  
- 백업에서 Dc를 복원 하는 경우 다음 작업을 수행 하는 데 시간이 걸립니다.  
   - 테이프와 같은 물리적 백업 미디어를 찾습니다.  
   - 운영 체제를 다시 설치 합니다.  
   - 백업 미디어에서 데이터를 복원 합니다.  
      - 시스템 상태 복원 대신 전체 서버 복구를 수행 하 여 운영 체제를 다시 설치 하 고 백업에서 데이터를 복원 하는 데 필요한 시간을 줄일 수 있습니다. 전체 서버 복구는 이진 기반 이므로 시스템 상태 복원 보다 훨씬 더 빨리 완료 됩니다.  
      - 그러나 서버에 복원 하지 않으려는 시스템 상태 데이터에서 제외 되는 데이터가 포함 되어 있는 경우 전체 서버 복구는 시스템 상태 복원에 대 한 대안이 될 수 있습니다. 서버에 대 한 시스템 상태 복원 대신 전체 서버 복구를 수행 하는 이점을 고려 하 고 나중에 복원 하려는 적절 한 유형의 백업을 수행 하 여 적절 하 게 준비 하십시오.  
- Dc를 다시 빌드하면 네트워크 기반 승격을 위해 데이터를 복제 하는 데 시간이 걸립니다.  
   - 다음 단계를 수행 하 여 Dc를 복원 하는 데 필요한 시간을 줄일 수 있습니다.  
- 다음 방법으로 백업 미디어를 검색 하는 시간을 줄입니다.  
   - Active Directory 데이터베이스 탑재 도구 (Dsamain .exe)를 사용 하 여 복원 작업에 사용할 최상의 백업을 식별 합니다. Active Directory 데이터베이스 탑재 도구를 사용 하는 방법에 대 한 자세한 내용은 [Active Directory 데이터베이스 탑재 도구 단계별 가이드](https://go.microsoft.com/fwlink/?LinkId=132577) (https://go.microsoft.com/fwlink/?LinkId=132577) 을 참조 하세요.  
   - 백업 미디어에 대 한 레이블을 명확 하 게 지정 하 고 신속 하 게 안전 하 게 안전 하 게 저장할 수 있는 위치에 미디어를 저장 합니다.  
   - SAN (저장 영역 네트워크)과 함께 볼륨 섀도 복사본 서비스를 사용 하 여 다른 시점에서 백업을 유지 관리 합니다. 자세한 내용은 [Windows Server 2003 Active Directory 볼륨 섀도 복사본 서비스 및 가상 디스크 서비스를 사용 하 여 빠른 복구](https://go.microsoft.com/fwlink/?LinkId=70781) (https://go.microsoft.com/fwlink/?LinkId=70781) )를 참조 하세요.  
- 운영 체제를 다시 설치 하는 대신 Dc에서 AD DS의 제거를 강제로 수행 합니다. 포리스트 전체 오류의 원인이 AD DS 범위 내에서 순수 하 게 확인 된 경우 Dc에 운영 체제를 다시 설치할 필요가 없습니다.  
   - Windows Server 2008 이상을 실행 하는 DC에서 AD DS를 강제로 제거 하는 방법에 대 한 자세한 내용은 [Windows server 2008 도메인 컨트롤러 강제 제거](https://go.microsoft.com/fwlink/?LinkId=132627) (https://go.microsoft.com/fwlink/?LinkId=132627) 을 참조 하세요. Windows Server 2003를 실행 하는 DC에서 AD DS를 강제로 제거 하는 방법에 대 한 자세한 내용은 Microsoft 기술 자료 [문서 332199](https://go.microsoft.com/fwlink/?LinkId=70780) (https://go.microsoft.com/fwlink/?LinkId=70780) 을 참조 하십시오.  
- 더 빠른 테이프 장치 또는 디스크 백업을 사용 하 여 복원 작업에 필요한 시간을 줄일 수 있습니다.  
  
IFM (미디어에서 설치) 기능을 사용 하 여 각 도메인의 Dc를 다시 작성 하 여 AD DS 설치를 가속화 할 수도 있습니다. IFM을 통해 각 도메인에서 Dc를 다시 작성할 때 발생 하는 복제 대기 시간을 줄일 수 있습니다.  
  
더 적극적인 SLA (서비스 수준 계약)가 있는 비즈니스는 복구 속도를 높이기 위해 포리스트 복구 절차를 변경 하는 것을 고려할 수 있습니다.  
  
**대답 포리스트 복구 프로세스를 자동화할 수 있나요?**

포리스트 복구 프로세스의 복잡 하 고 중요 한 특성으로 인해 현재는 종단 간 자동화가 없습니다. 포리스트 복구 프로세스는 프로세스 자동화의 기술적 문제 보다 비즈니스 연속성을 복원 하는 것이 더 로지스틱 하 고 조직의 과제입니다. 따라서 환경을 관리 하는 개인은 해당 환경에 해당 하는 포리스트 복구 계획을 만든 다음 자동화를 성공적으로 수행할 수 있는 섹션을 자동화 해야 합니다.  
  
대부분의 경우 명령줄 도구를 사용 하 여 포리스트 복구 단계를 수행할 수 있습니다. 따라서 대부분의 단계를 스크립팅할 수 있습니다. 예를 들어 Ntdsutil.exe는 포리스트 복구 프로세스에서 가장 자주 사용 되는 도구 중 하나입니다.  
  
스크립트는 복구 속도를 높일 수 있지만 이러한 스크립트를 실제 환경에 적용 하기 전에 철저 하 게 테스트 해야 합니다. 또한 새 도메인 이나 DC 추가 또는 Active Directory의 새 버전 등 Active Directory 환경의 변경 내용에 따라 업데이트 해야 합니다.

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
