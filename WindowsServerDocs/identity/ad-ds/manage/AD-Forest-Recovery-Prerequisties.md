---
title: Active Directory 포리스트 복구 계획에 대 한 필수 구성 요소
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: c49b40b2-598d-49aa-85b4-766bce960e0d
ms.technology: identity-adds
ms.openlocfilehash: c8945dd5ccccb27826dd96413b56a070a7452789
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59842174"
---
# <a name="active-directory-forest-recovery-prerequisites"></a>Active Directory 포리스트 복구 필수 구성 요소

>적용 대상: Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 R2

다음 문서는 포리스트 복구 계획을 고안 하거나 복구를 시도 하기 전에 잘 알고 있어야 하는 필수 구성 요소를 설명 합니다.

## <a name="assumptions-for-using-this-guide"></a>이 가이드를 사용 하 여 가정

1. Microsoft 지원 전문가 함께 수행한 및:
   - 포리스트 오류의 원인을 확인 합니다. 이 가이드 실패의 원인을 제안 하지 않거나 모든 절차 실패를 방지 하는 것이 좋습니다.
   - 모든 가능한 구제를 평가 합니다.  
   - Microsoft 지원과 상담에서 결과, 해당 포리스트 전체 상태로 오류가 발생 하기 전에 복원은 오류 로부터 복구 하는 가장 좋은 방법은입니다. 대부분의 경우에 포리스트 복구는 마지막 옵션은 있어야 합니다.

2. Active Directory-통합 된 도메인 이름 시스템 (DNS)를 사용 하 여에 대 한 Microsoft 모범 사례 권장 사항을 수행 합니다. 특히 각 Active Directory 도메인에 대 한 Active Directory 통합 DNS 영역을 있어야 합니다. 
   - 없는 경우 포리스트 복구를 수행 하려면이 가이드의 기본 원칙을 사용할 수 있습니다. 그러나 사용자 고유의 환경을 기반으로 하는 DNS 복구를 위해 특정 조치를 수행 해야 합니다. Active Directory 통합 DNS를 사용 하는 방법에 대 한 자세한 내용은 참조 하세요. [DNS 인프라 디자인 만들기](../../ad-ds/plan/Creating-a-DNS-Infrastructure-Design.md)합니다.

3. 이 가이드는 포리스트 복구를 위한 일반 지침으로, 하지만 일부 경우가 설명 되어 있습니다. 예를 들어 Windows Server 2008 부터는 경우 전체 GUI를 하지 않고 Windows Server의 전체 버전 하 여 Server Core 버전 Server Core를 실행 하는 Dc만 구성 된 포리스트를 복구 하는 아니지만이 가이드에 자세한 지침이 없습니다. 그러나 여기에 설명 된 지침에 따라 있습니다 됩니다 수 필수 명령줄 작업을 직접 디자인.  

> ![!NOTE]
> 이 가이드의 목표는 포리스트를 복구 하 고 유지 관리 또는 전체 DNS 기능을 복원 하려면, 복구 실패 하기 전에 구성에서 변경 되는 DNS 구성에서 발생할 수 있습니다. 포리스트를 복구한 후에 원래 DNS 구성으로 되돌릴 수 있습니다. 이 가이드의 권장 사항을 회사 네임 스페이스의 다른 부분에 대 한 이름 확인을 수행 하기 위해 DNS 서버를 구성 하는 방법을 설명 하지는 AD DS에 저장 되지 않은 DNS 영역이 있는 경우.  

## <a name="concepts-for-using-this-guide"></a>이 가이드를 사용 하 여에 대 한 개념

Active Directory 포리스트 복구 계획을 시작 하기 전에 다음을 사용 하 여 알아두어야 하 합니다.  
  
- 기본 Active Directory 개념  
- 작업 마스터 역할 (신축 단일 마스터 작업 또는 FSMO 라고도 함)의 중요도입니다. 이러한 역할은 다음과 같습니다.  
   - 스키마 마스터
   - 도메인 명명 마스터
   - 상대 ID (RID) 마스터
   - 주 도메인 컨트롤러 (PDC) 에뮬레이터 마스터
   - 인프라 마스터

또한를 백업 해야 하 고 정기적으로 랩 환경에서 AD DS 및 SYSVOL을 복원 합니다. 자세한 내용은 [시스템 상태 데이터를 백업](AD-Forest-Recovery-Procedures.md) 하 고 [Active Directory Domain Services의 신뢰할 수 없는 복원을 수행](AD-Forest-Recovery-Procedures.md)합니다.

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
