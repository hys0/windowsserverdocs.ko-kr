---
ms.assetid: 503733f8-be0c-429c-81f0-cd4205e8b118
title: 검사 목록-클레임 공급자에 대 한 클레임 규칙 만들기 신뢰
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 708919691f88cc49d1f2bd74d8f4255e1a854353
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192395"
---
# <a name="checklist-creating-claim-rules-for-a-claims-provider-trust"></a>검사 목록: 클레임 공급자에 대 한 클레임 규칙 만들기 신뢰


이 검사 목록을 포함 계획에 대 한 작업을 디자인 및 클레임 공급자와 연결 된 배포 클레임 규칙 Active Directory Federation Services에서 신뢰 \(AD FS\)합니다.  
  
> [!NOTE]  
> 이 검사 목록의 작업을 순서대로 완료하세요. 참조 링크가 절차를 안내하는 경우 이 검사 목록의 나머지 작업을 계속 진행하려면 해당 절차의 단계를 완료한 후 이 항목으로 돌아와야 합니다.  
  
![클레임 규칙을 만드는](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**검사 목록: 클레임 공급자 트러스트에 대 한 클레임 규칙 집합 만들기**  
  
||태스크|참조|  
|-|--------|-------------|  
|![클레임 규칙 만들기](media/icon_checkboxo.gif)|클레임에 대 한 개념을 검토, 클레임 규칙, 클레임 규칙 집합 및 클레임 규칙 템플릿 및 페더레이션된 트러스트와 연관 되는 방식이 있습니다.|![클레임 규칙을 만드는](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[The 역할 클레임](../../ad-fs/technical-reference/The-Role-of-Claims.md)<br /><br />![클레임 규칙을 만드는](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[규칙의 역할 클레임](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md)|  
|![클레임 규칙 만들기](media/icon_checkboxo.gif)|클레임 발급 파이프라인의 모든 단계를 통해 클레임을 전달 하는 방법 및 클레임 발급 엔진에서 규칙은 처리 하는 방법에 대 한 개념을 검토 합니다.|![클레임 규칙을 만드는](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[클레임 파이프라인의 역할](../../ad-fs/technical-reference/The-Role-of-the-Claims-Pipeline.md)<br /><br />![클레임 규칙을 만드는](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[클레임 엔진의 역할](../../ad-fs/technical-reference/The-Role-of-the-Claims-Engine.md)|  
|![클레임 규칙 만들기](media/icon_checkboxo.gif)|효과적으로 계획 하 고이 클레임 공급자 트러스트를 통해 발생 하는 출력 클레임을 구현, 하나 이상의 클레임 규칙이 필요한 여부와이 클레임 공급자 트러스트를 사용 해야 하는 규칙 클레임을 결정 합니다.|![클레임 규칙을 만드는](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[종류의 클레임 규칙 템플릿을 사용 하 여 확인 합니다.](../../ad-fs/technical-reference/Determine-the-Type-of-Claim-Rule-Template-to-Use.md)|  
|![클레임 규칙 만들기](media/icon_checkboxo.gif)|다른 규칙 및 클레임 규칙 언어를 사용 하 여 이상적인 출력에서 원하는 결과 제공 하기 위해 표준 규칙 보다 더 복잡 한 논리를 제공 하는 방법을 클레임 집합을 한 클레임을 만들려는 경우에 대 한 개념을 검토 합니다.|![클레임 규칙을 만드는](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[통과 또는 필터 클레임 규칙을 사용 하는 경우](../../ad-fs/technical-reference/When-to-Use-a-Pass-Through-or-Filter-Claim-Rule.md)<br /><br />![클레임 규칙을 만드는](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[변환 클레임 규칙을 사용 하는 경우](../../ad-fs/technical-reference/When-to-Use-a-Transform-Claim-Rule.md)<br /><br />![클레임 규칙을 만드는](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[a Send LDAP Attributes as Claims Rule 사용 하는 경우](../../ad-fs/technical-reference/When-to-Use-a-Send-LDAP-Attributes-as-Claims-Rule.md)<br /><br />![클레임 규칙을 만드는](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[클레임으로 보내기 그룹 멤버 자격을 사용 하는 경우](../../ad-fs/technical-reference/When-to-Use-a-Send-Group-Membership-as-a-Claim-Rule.md)<br /><br />![클레임 규칙을 만드는](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[사용자 지정 클레임 규칙을 사용 하는 경우](../../ad-fs/technical-reference/When-to-Use-a-Custom-Claim-Rule.md)<br /><br />![클레임 규칙을 만드는](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[클레임 규칙 언어의 역할](../../ad-fs/technical-reference/The-Role-of-the-Claim-Rule-Language.md)|  
|![클레임 규칙 만들기](media/icon_checkboxo.gif)|클레임 설명 아직 없는 경우 만들어야 하는 조직의 요구를 충족 합니다. AD FS 노출 되는 클레임 설명의 기본 집합을 기본 제공 AD FS 관리 스냅인에서\-에 있습니다.|![클레임 규칙을 만드는](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[클레임 설명 추가](../../ad-fs/operations/Add-a-Claim-Description.md)|  
|![클레임 규칙 만들기](media/icon_checkboxo.gif)|조직의 요구에 따라 클레임 적절 하 게 실행 될 수 있도록이 클레임 공급자 트러스트와 연결 되는 수용 변환 규칙 집합에 대 한 하나 이상의 클레임 규칙을 만듭니다.|![클레임 규칙을 만드는](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[통과 하는 규칙을 만들거나 들어오는 클레임 필터링](../../ad-fs/operations/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim.md)<br /><br />![클레임 규칙을 만드는](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[LDAP 특성을 클레임으로 보내기 규칙 만들기](../../ad-fs/operations/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims.md)<br /><br />![클레임 규칙을 만드는](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[클레임으로 보내기 그룹 멤버 자격 규칙 만들기](../../ad-fs/operations/Create-a-Rule-to-Send-Group-Membership-as-a-Claim.md)<br /><br />![클레임 규칙을 만드는](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[들어오는 클레임 변환 규칙 만들기](../../ad-fs/operations/Create-a-Rule-to-Transform-an-Incoming-Claim.md)<br /><br />![클레임 규칙을 만드는](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[인증 방법 클레임을 보내도록 규칙 만들기](../../ad-fs/operations/Create-a-Rule-to-Send-an-Authentication-Method-Claim.md)<br /><br />![클레임 규칙을 만드는](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[AD FS를 보내도록 규칙을 만들 1.x 호환 클레임](../../ad-fs/operations/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim.md)<br /><br />![클레임 규칙을 만드는](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[클레임으로 보내기 규칙을 사용자 지정 규칙 만들기](../../ad-fs/operations/Create-a-Rule-to-Send-Claims-Using-a-Custom-Rule.md)|  
  

