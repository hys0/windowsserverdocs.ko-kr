---
title: "Active Directory 숲 복구 계획 사항"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: c49b40b2-598d-49aa-85b4-766bce960e0d
ms.technology: identity-adfs
ms.openlocfilehash: 672e1f4d0de9bfb2cbe291c5ed715814c8acacd0
ms.sourcegitcommit: 84a2bdcb92ba6af45781fab9727617e50fa5e911
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/07/2017
---
#<a name="active-directory-forest-recovery-prerequisites"></a>복구 필수 active Directory 숲

>Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 r 2에 적용 됩니다.

다음 문서 숲 복구 계획 고안 하거나, 복구를 시도 하기 전에 잘 알고 있어야 필수에 설명 합니다.

## <a name="assumptions-for-using-this-guide"></a>이 가이드를 사용 하는 

1.  Microsoft 지원 전문가와 작동 하 고 있습니다.

    - 숲 속 전체 오류 원인을 확인 합니다. 이 가이드 오류 원인을 제안 되지 않거나 모든 절차 방지 실패 하는 것이 좋습니다.  
    - 모든 가능한 보상 평가합니다.  
    - Microsoft 지원에 문의에서 결론이 해당 복원은 전체 숲 상태로 오류가 발생 하기 전의입니다 오류를 복구 하는 가장 좋은 방법은 합니다. 대부분의 경우 숲 복구 최후의 수단 있어야 합니다.  </br></br>

2. 했는지 Active Directory 통합 시스템 DNS (도메인 이름)을 사용 하 여 하기 위한 권장 모범 사례. 특히, Active Directory 각 도메인에 대 한 Active Directory 통합 DNS 영역 있을 것입니다. 없는 경우이 가이드는 기본 원칙 숲 복구를 계속 사용할 수 있습니다. 그러나 DNS 복구 직접 환경에 대 한 특정 조치를 수행 해야 합니다. DNS Active Directory 통합 사용에 대 한 자세한 내용은 참조 [DNS Infrastructure 디자인](../../ad-ds/plan/Creating-a-DNS-Infrastructure-Design.md)합니다.
3. 이 가이드는 숲 복구에 대 한 일반 가이드로, 있지만 사용할 수 있는 모든 시나리오 적용 됩니다. 예를 들어 버전의 Windows Server 않고 전체 GUI Server Core 버전을 방법이 Windows Server 2008를 시작 합니다. 분명 Server Core 실행 Dc 방금 구성 된 숲 복구할 수 있지만,이 가이드는 방법은 없습니다. 그러나 여기에 대해 수시로 이야기 지침에 따라 사용자는 수 직접 명령줄 필요한 작업을 디자인 하 합니다.  
 
>![!NOTE]
> 이 가이드 목표 숲 복구 하 고 유지 하거나 전체 DNS 기능을 복원 하는, 복구 오류가 발생 하기 전에 구성에서 변경 되는 DNS 구성 될 수 있습니다. 숲 복구한 원래 DNS 구성으로 되돌릴 수 있습니다. 이 가이드 권장 사항 회사 네임의 다른 부분의 이름을 확인을 수행 하기 DNS 서버를 구성 하는 방법을 설명 하지 않는 DNS 영역 AD DS에 저장 되어 있지 않은 경우입니다.  

## <a name="concepts-for-using-this-guide"></a>이 가이드를 사용 하기 위한 개념
 복구 Active Directory 숲의 계획을 시작 하기 전에 다음 잘 알고 있어야 합니다.  
  
-   기본 Active Directory 개념  
  
-   (라고도 단일 마스터 작업 유연한 또는 FSMO) 작업 마스터 역할의 중요 합니다. 이러한 역할은 다음과 같습니다.  
  
    -   스키마 마스터  
  
    -   도메인 이름 지정 마스터  
  
    -   ID (RID) 상대 마스터  
  
    -   주 도메인 컨트롤러 (PDC) 에뮬레이터 마스터  
  
    -   Infrastructure 마스터  
  
 또한를 백업 및 AD DS 및 SYSVOL 정기적으로 환경에서 복원 합니다. 자세한 내용은 참조 [시스템 상태 데이터를 백업](AD-Forest-Recovery-Procedures.md) 및 [신뢰할 수의 Active Directory Domain Services 복원을 수행](AD-Forest-Recovery-Procedures.md)합니다.

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
