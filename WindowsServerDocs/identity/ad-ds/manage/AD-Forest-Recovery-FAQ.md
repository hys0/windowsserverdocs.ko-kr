---
title: "광고 숲 복구-FAQ"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: ac9e5a3d-8b1e-41b7-8e02-f64b7acf1359
ms.technology: identity-adfs
ms.openlocfilehash: 839e01c88b7ced22501154d8752c6c71cc52b696
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="ad-forest-recovery---faq"></a>광고 숲 복구-FAQ

>Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 R2, Windows Server 2003 적용 대상: Windows Server 2016

이 문서 (Faq)에 대 한 질문과를 숲 복구 포함 되어 있습니다.  
 
## <a name="general-recovery"></a>일반적인 복구
  
 
**복구 속도 q: 수행할 수 있나요?** 
 
복구 속도이 가이드 최우선 하지는 않지만 하 여 짧고 복구 시간을 얻을 수 있습니다.  
  
-   자세한 숲 복구 계획 정기적으로 업데이트 하 고 1 년에 한 번 이상 적절 한 크기의 시뮬레이트된 테스트 환경에서 연습 만들기  
  
-   DC (컨트롤러) 복제 가상화 도메인을 사용 하 여  
  
     DC 각 도메인에 백업에서 복원 하는 한 후 실행 하는 추가적인 Dc 다운로드 하는 프로세스를 빠르게 가상화 DC 복제 합니다. Dc 추가 가상화 걸리는 AD DS 설치를 완료 하 고 설치 후에 중요 한 복제 완성 하기 위해 대기 하는 것이 아니라 복제 될 수 있습니다.  
  
     여기서 가상 Dc 호스트 제대로 연결 된 데이터 센터의 적은 수의 사용자 숲 복구 하는 동안 복제에서 최고의 도움이 됩니다. 그러나 같은 도메인에 대 한 여러 가상화 Dc 같은 하이퍼바이저 호스트에 공존 하 든 환경 혜택 해야 합니다.  
  
-   읽기 전용 Rodc (도메인 컨트롤러)를 배포합니다.  
  
     도 삽 니다 쓸 수 Dc 네트워크에서 연결을 끊을 수 없기 때문에 Rodc 복구 과정 중 비즈니스 연속성을 제공할 수 있습니다. Rodc 아웃 바운드 복제를 수행 하지 않습니다. 따라서 동일한 쓸 수 Dc 손상 데이터 복구 환경으로 다시 복제 하기 위한 발생할 수 있는 위험을 제공 하지 않습니다.  
  
 숲 복구 과정의 기간에 영향을 주는 다른 요소는 다음과 같습니다.  
  
-   Dc 백업에서 복원 하면 데 시간이 걸립니다.  
  
    -   실제 백업 미디어를 테이프 등을 찾습니다.  
  
    -   운영 체제를 다시 설치 합니다.  
  
    -   미디어를 백업에서 데이터를 복원 합니다.  
  
     운영 체제를 다시 설치 하 고 전체 서버 복구 대신 상태 시스템 복원 수행 하 여 백업에서 데이터를 복원 하는 데 필요한 시간을 줄일 수 있습니다. 전체 서버 복구 이진 기반 이므로 시스템 상태로 복원 보다 훨씬 빠르게 완료 합니다.  
  
     그러나 시스템 상태 데이터를 복원 하려면에서 제외 되는 데이터는 서버에 포함 된 경우 전체 서버 복구 상태 시스템 복원 실행 가능한 대신 되지 않을 수 있습니다. 특히, 서버에 대 한 상태 시스템 복원 하는 대신 전체 서버 복구 수행의 혜택을 고려해 고 그에 따라 준비 적절 한 유형의 나중에 복원 하려면 백업이 수행 하 여 합니다.  
  
-   Dc을 다시 작성 하는 경우 네트워크 기반 프로 모션에 대 한 데이터를 복제 하는 데 시간이 걸립니다.  
  
 다음 단계를 수행 하 여 Dc 복원 하는 데 필요한 시간을 줄일 수 있습니다.  
  
-   검색 하 여 백업 미디어에 대 한 시간을 줄입니다.  
  
    -   Active Directory 데이터베이스 장착 도구 (Dsamain.exe)를 사용 하 여 좋은 백업을 복원 작업에 사용 하 여 확인 합니다. Active Directory 데이터베이스 장착 도구를 사용 하 여에 대 한 자세한 내용은 참조는 [Active Directory 데이터베이스 장착 도구 Step-by-Step 가이드](https://go.microsoft.com/fwlink/?LinkId=132577) (https://go.microsoft.com/fwlink/?LinkId=132577).  
  
    -   백업 미디어 명확 하 게을 구분 하 고 편리 하 고에서 항상 정리 된 방식 미디어 저장 아직 보안을 빠르게 검색할 수 있는 위치 합니다.  
  
    -   (산)는 저장 공간 영역 네트워크와 볼륨 섀도 복사본 서비스를 사용 하 여 다양 한 지점에서 백업을으로 유지 합니다. 자세한 내용은 참조 [Windows Server 2003 Active Directory 빨리 복구 볼륨 섀도 복사본 서비스 가상 디스크 서비스와](https://go.microsoft.com/fwlink/?LinkId=70781) (https://go.microsoft.com/fwlink/?LinkId=70781).  
  
-   운영 체제를 다시 설치 하는 대신 Dc에서 강제로 AD DS 제거 합니다. 순수한 AD DS 범위 내에 숲 전체의 오류 원인을 식별 하는 경우 Dc에 운영 체제를 다시 필요가 없습니다.  
  
     Windows Server 2008 이상을 실행 하는 DC에서 AD DS의 제거를 시작에 대 한 자세한 내용은 참조 [Windows Server 2008 도메인 컨트롤러의 제거 강제로](https://go.microsoft.com/fwlink/?LinkId=132627) (https://go.microsoft.com/fwlink/?LinkId=132627). Windows Server 2003을 실행 하는 DC에서 AD DS의 제거를 시작에 대 한 자세한 내용은 참조 [332199 문서](https://go.microsoft.com/fwlink/?LinkId=70780) 에 Microsoft 기술 자료 (https://go.microsoft.com/fwlink/?LinkId=70780).  
  
-   더 빠르게 테이프 디바이스를 사용 하 여 또는 하는 데 필요한 시간을 줄입니다 디스크 백업을 복원 작업입니다.  
  
 Dc 각 도메인에 다시 설치 미디어 (IFM) 기능에서 사용 하 여 설치 AD DS 가속 도와줄 수 있습니다. IFM 복제 대기 Dc 각 도메인에 다시 때 발생 하는 시간을 줄일 수 있습니다.  
  
 보다 적극적인 수준 서비스 계약 (SLA) 비즈니스 숲 복구 절차 복구 속도를 변경 것이 좋습니다.  
  

**Q: 숲 복구 과정을 자동화 수 있나요?**  
 숲 복구 과정의 복잡 한와 가장 비판적인 특성으로 인해의 없는 종단 간 자동화 현재입니다. 숲 복구 과정이 어렵습니다 더 물류 및 조직 기술적인 문제 프로세스 자동화 보다 비즈니스 연속성 복원 합니다. 환경을 관리 하는 개인 해당 환경에와 관련 된 숲 복구 옵션 만들기 고 성공적으로 자동화 된 섹션의 다음 자동화 해야 합니다.  
  
 명령줄 도구를 사용 하 여 대부분의 숲 복구 단계를 수행할 수 있습니다. 따라서 대부분의 단계 스크립트 됩니다. 예를 들어, Ntdsutil.exe 숲 복구 과정의 가장 자주 사용 하는 도구 중 하나입니다.  
  
 스크립트 빠르게 복구할 수 되지만 실제 환경에서 적용 하기 전에 이러한 스크립트 테스트 완전히 해야 합니다. 또한, Active Directory 환경 새 도메인 또는 DC, 추가 또는 새 버전의 Active Directory 등의 변경에 따라 업데이트 해야 합니다.

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
