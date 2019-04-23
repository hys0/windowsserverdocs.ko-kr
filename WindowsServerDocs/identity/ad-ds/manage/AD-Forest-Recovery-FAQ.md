---
title: AD 포리스트 복구 - FAQ
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: ac9e5a3d-8b1e-41b7-8e02-f64b7acf1359
ms.technology: identity-adds
ms.openlocfilehash: 36c9560b490cc28f006770c869bdcdf2b152dd74
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59878454"
---
# <a name="ad-forest-recovery---faq"></a>AD 포리스트 복구 - FAQ

>적용 대상: Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 R2, Windows Server 2003

이 문서에는 포리스트 복구에 대 한 질문과 대답 (Faq):  

## <a name="general-recovery"></a>일반 복구

**Q: 복구 속도를 어떻게 해야 합니까?**

복구 속도이 가이드의 주요 목표 하지는 않지만 하 여 더 짧은 복구 시간을 얻을 수 있습니다.  
  
- 자세한 포리스트 복구 계획 만들기, 정기적으로 업데이트 및 일년에 한 번 이상 적절 한 크기의 시뮬레이션 된 테스트 환경에서 실행  
- 가상화 된 도메인 컨트롤러 (DC) 복제를 사용 하 여  
   - 가상화 된 DC 복제 속도를 DC 각 도메인에 있는 백업에서 복원 된 후 실행 하는 추가 Dc를 가져오는 프로세스를 높여 줍니다. 설치 후 중요 하지 않은 복제 완료 한 시간이 오래 걸리는 AD DS 설치 완료를 기다리지 않고 추가 가상화 된 Dc는 복제할 수 있습니다.  
   - 가상 Dc 호스팅되는 잘 연결 된 데이터 센터의 상대적으로 적은 수의 잠재적으로 포리스트 복구 중 복제에서 가장을 활용 합니다. 그러나 동일한 도메인에 대 한 여러 가상화 된 Dc 같은 하이퍼바이저 호스트에 배치 됩니다 모든 환경 활용 해야 합니다.  
- 읽기 전용 도메인 컨트롤러 (Rodc) 배포  
   - Rodc는 쓰기 가능한 Dc와 마찬가지로 네트워크에서 연결을 끊을 수 없기 때문에 비즈니스 연속성 복구 프로세스 동안 제공할 수 있습니다. Rodc는 아웃 바운드 복제를 수행 하지 않습니다. 따라서 복구 환경으로 다시 손상을 일으킬 수 있는 데이터를 복제에 대 한 쓰기 가능한 Dc 발생할 수 있는 동일한 위험을 제공 하지 않습니다.  
  
포리스트 복구 프로세스의 기간에 영향을 주는 다른 요소는 다음과 같습니다.  
  
- Dc 백업에서 복원한 경우 하는 시간이 걸립니다.  
   - 테이프와 같은 물리적 백업 미디어를 찾습니다.  
   - 운영 체제를 다시 설치 합니다.  
   - 백업 미디어에서 데이터를 복원 합니다.  
      - 운영 체제를 다시 설치 하 고 시스템 상태 복원 대신 전체 서버 복구를 수행 하 여 백업에서 데이터를 복원 하는 데 필요한 시간을 줄일 수 있습니다. 전체 서버 복구 이진 기반 이기 때문에 시스템 상태 복원을 보다 훨씬 빨리 완료 됩니다.  
      - 그러나 서버에서 시스템 상태 데이터 복원 하지 않으려는 경우는 제외 되는 데이터가 포함 된 경우 전체 서버 복구 되지 않을 수 있습니다 시스템 상태 복원 실행 가능한 대안이 있습니다. 특히, 서버에 대 한 시스템 상태 복원 대신 전체 서버 복구를 수행 하는 장점 및 그에 따라 준비 적절 한 나중에 복원 하려는 백업 유형을 수행 하 여 합니다.  
- Dc를 다시 작성 하는 경우 네트워크 기반의 승격에 대 한 데이터를 복제 하는 시간이 걸립니다.  
   - 다음 단계를 수행 하 여 Dc를 복원 하는 데 필요한 시간을 줄일 수 있습니다.  
- 백업 미디어를 검색 하기 위한 시간을 줄이려면:  
   - Active Directory 데이터베이스를 탑재 도구 (Dsamain.exe)를 사용 하 여 복원 작업에 사용할 최상의 백업을 확인 합니다. Active Directory 데이터베이스를 탑재 도구를 사용 하는 방법에 대 한 자세한 내용은 참조는 [Active Directory 데이터베이스를 탑재 도구 단계별 가이드](https://go.microsoft.com/fwlink/?LinkId=132577) (https://go.microsoft.com/fwlink/?LinkId=132577)합니다.  
   - 백업 미디어를 명확 하 게 레이블 지정 및을 편리 하 고에 구성 된 방식으로 미디어를 저장 합니다. 아직 보호 빠른 검색을 허용 하는 위치입니다.  
   - 저장 영역 네트워크 (SAN)를 사용 하 여 볼륨 섀도 복사본 서비스를 사용 하 여 시간상에서 다른 지점에서는 백업을 유지 합니다. 자세한 내용은 [Windows Server 2003 Active Directory 빠른 복구 가상 디스크 서비스 볼륨 섀도 복사본 서비스와](https://go.microsoft.com/fwlink/?LinkId=70781) (https://go.microsoft.com/fwlink/?LinkId=70781)합니다.  
- 운영 체제를 다시 설치 하는 대신 Dc에서 AD DS 제거를 적용 합니다. AD DS의 범위 내에서 순수 하 게 되도록 포리스트 실패의 원인을 식별 하는 경우 Dc에 운영 체제를 다시 설치할 필요가 없습니다.  
   - Windows Server 2008 이상을 실행 하는 DC에서 AD DS 제거를 강제 적용 하는 방법에 대 한 자세한 내용은 참조 하세요. [Windows Server 2008 도메인 컨트롤러의 제거를 강제로](https://go.microsoft.com/fwlink/?LinkId=132627) (https://go.microsoft.com/fwlink/?LinkId=132627)합니다. Windows Server 2003을 실행 하는 DC에서 AD DS 제거를 강제 적용 하는 방법에 대 한 자세한 내용은 참조 하세요. [332199 문서](https://go.microsoft.com/fwlink/?LinkId=70780) Microsoft 기술 자료 (https://go.microsoft.com/fwlink/?LinkId=70780)합니다.  
- 더 빠른 테이프 장치를 사용 하거나 디스크 백업에 필요한 시간을 줄이기 위해 복원 작업 합니다.  
  
또한 각 도메인의 Dc를 다시 작성 하려면 IFM (미디어) 기능에서 설치를 사용 하 여 AD DS 설치를 가속화는 것이 도움이 됩니다. IFM에는 각 도메인의 Dc에서에서 다시 작성할 때 발생 하는 복제 대기 시간이 줄어듭니다.  
  
기업에 더 적극적으로 서비스 수준 계약 (SLA) 변경 속도 복구 하는 포리스트 복구 절차를 고려할 수 있습니다.  
  
**Q: 포리스트 복구 프로세스를 자동화할 수 있나요?**

포리스트 복구 프로세스가 복잡 하 고 중요 한 특성으로 인해의 종단 간 자동화 되지 현재입니다. 포리스트 복구 프로세스가 어렵습니다 더 물류 및 조직 프로세스 자동화의 기술적인 문제 보다 비즈니스 연속성을 복원 합니다. 따라서 개별 사용자는 환경을 관리는 해당 환경에 관련 된 포리스트 복구 계획을 만들 하 고 성공적으로 자동화할 수 있는 섹션의 자동화 해야 합니다.  
  
명령줄 도구를 사용 하 여 대부분의 포리스트 복구 단계를 수행할 수 있습니다. 따라서 대부분의 단계는 스크립트 가능 합니다. 예를 들어 Ntdsutil.exe 포리스트 복구 프로세스에서 가장 자주 사용 되는 도구 중 하나입니다.  
  
스크립트를 빠르게 복구할 수 있습니다, 있지만 실제 환경에서 적용 하기 전에 이러한 스크립트 철저히 테스트 해야 합니다. 또한 새 도메인 또는 DC를 추가 또는 새 버전의 Active Directory와 같은 Active Directory 환경에서 변경 내용에 따라 업데이트 해야 합니다.

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
