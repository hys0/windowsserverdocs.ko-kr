---
title: Active Directory 포리스트 복구 계획을 위한 필수 구성 요소
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: c49b40b2-598d-49aa-85b4-766bce960e0d
ms.technology: identity-adds
ms.openlocfilehash: fddd5e236774c7f054ccd6332eb45d4f03afdf3f
ms.sourcegitcommit: a33404f92867089bb9b0defcd50960ff231eef3f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/04/2020
ms.locfileid: "77013008"
---
# <a name="active-directory-forest-recovery-prerequisites"></a>Active Directory 포리스트 복구 필수 구성 요소

> 적용 대상: Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 R2

다음 문서에서는 포리스트 복구 계획을 고안 복구를 시도 하기 전에 알아두어야 하는 필수 구성 요소에 대해 설명 합니다.

## <a name="assumptions-for-using-this-guide"></a>이 가이드 사용에 대 한 가정

1. Microsoft 지원 전문 및 다음 작업을 수행 했습니다.
   - 포리스트 전체 오류의 원인을 확인 했습니다. 이 가이드는 실패의 원인을 제안 하지 않으며 실패를 방지 하기 위한 절차를 권장 하지 않습니다.
   - 가능한 해결 방법을 확인 합니다.  
   - Microsoft 지원에서 실패 하기 전에 전체 포리스트를 해당 상태로 복원 하는 것은 실패에서 복구 하는 가장 좋은 방법입니다. 대부분의 경우에는 포리스트 복구가 마지막 옵션 이어야 합니다.

1. Active Directory – 통합 DNS (Domain Name System) 사용에 대 한 Microsoft 모범 사례 권장 사항을 따르고 있습니다. 특히 각 Active Directory 도메인에 대 한 Active Directory 통합 DNS 영역이 있어야 합니다.
   - 그렇지 않은 경우에도이 가이드의 기본 원칙을 사용 하 여 포리스트 복구를 수행할 수 있습니다. 그러나 사용자의 환경에 따라 DNS 복구를 위한 특정 측정값을 사용 해야 합니다. Active Directory-통합 DNS를 사용 하는 방법에 대 한 자세한 내용은 [Dns 인프라 디자인 만들기](../../ad-ds/plan/Creating-a-DNS-Infrastructure-Design.md)를 참조 하세요.

1. 이 가이드는 포리스트 복구를 위한 일반 가이드 이지만 모든 가능한 시나리오를 다루는 것은 아닙니다. 예를 들어 Windows Server 2008부터 전체 버전의 Windows Server 이지만 전체 GUI는 없는 Server Core 버전이 있습니다. Server Core를 실행 하는 Dc로만 구성 된 포리스트를 복구할 수 있지만이 가이드에는 자세한 지침이 없습니다. 그러나 여기서 설명 하는 지침에 따라 직접 필요한 명령줄 작업을 디자인할 수 있습니다.  

> [!NOTE]
> 이 가이드의 목표는 포리스트를 복구 하 고 전체 DNS 기능을 유지 관리 하거나 복원 하는 것 이지만, 복구로 인해 실패 하기 전에 구성에서 변경 된 DNS 구성이 발생할 수 있습니다. 포리스트가 복구 된 후 원래 DNS 구성으로 되돌릴 수 있습니다. 이 가이드의 권장 사항은 AD DS에 저장 되지 않은 DNS 영역이 있는 회사 네임 스페이스의 다른 부분에 대 한 이름 확인을 수행 하도록 DNS 서버를 구성 하는 방법에 대해서는 설명 하지 않습니다.  

## <a name="concepts-for-using-this-guide"></a>이 가이드의 사용에 대 한 개념

Active Directory 포리스트의 복구 계획을 시작 하기 전에 다음에 대해 잘 알고 있어야 합니다.  
  
- 기본 Active Directory 개념  
- 작업 마스터 역할의 중요도 (신축 단일 마스터 작업 또는 FSMO 라고도 함) 이러한 역할은 다음과 같습니다.  
  - 스키마 마스터
  - 도메인 명명 마스터
  - RID (상대 ID) 마스터
  - PDC (주 도메인 컨트롤러) 에뮬레이터 마스터
  - 인프라 마스터

또한 랩 환경에서 정기적으로 AD DS 및 SYSVOL을 백업 하 고 복원 해야 합니다. 자세한 내용은 [시스템 상태 데이터 백업](AD-Forest-Recovery-Procedures.md) 및 [Active Directory Domain Services의 비정식 복원 수행](AD-Forest-Recovery-Procedures.md)을 참조 하세요.

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [AD 포리스트 복구 - 필수 조건](AD-Forest-Recovery-Prerequisties.md)

> [!div class="nextstepaction"]
> [AD 포리스트 복구-사용자 지정 포리스트 복구 계획 고안](AD-Forest-Recovery-Devising-a-Plan.md)

> [!div class="nextstepaction"]
> [AD 포리스트 복구-문제 식별](AD-Forest-Recovery-Identify-the-Problem.md)

> [!div class="nextstepaction"]
> [AD 포리스트 복구-복구 방법을 결정 합니다.](AD-Forest-Recovery-Determine-how-to-Recover.md)

> [!div class="nextstepaction"]
> [AD 포리스트 복구-초기 복구 수행](AD-Forest-Recovery-Perform-initial-recovery.md)

> [!div class="nextstepaction"]
> [AD 포리스트 복구 - 절차](AD-Forest-Recovery-Procedures.md)

> [!div class="nextstepaction"]
> [AD 포리스트 복구-질문과 대답](AD-Forest-Recovery-FAQ.md)

> [!div class="nextstepaction"]
> [AD 포리스트 복구-다중 도메인 포리스트 내에서 단일 도메인 복구](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)

> [!div class="nextstepaction"]
> [AD 포리스트 복구-Windows Server 2003 도메인 컨트롤러를 사용 하 여 포리스트 복구](AD-Forest-Recovery-Windows-Server-2003.md)
