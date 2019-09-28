---
ms.assetid: 44271f44-b50a-4bce-9375-4fcab9618048
title: 검사 목록-신뢰 당사자 트러스트에 대 한 클레임 규칙 만들기
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: e070e21e6cc4a8cd11a70e3b5c1d994e0dfb8629
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408507"
---
# <a name="checklist-creating-claim-rules-for-a-relying-party-trust"></a>검사 목록: 신뢰 당사자 트러스트에 대 한 클레임 규칙 만들기


이 검사 목록에는 Active Directory Federation Services \(AD FS @ no__t-1에서 신뢰 당사자 트러스트와 관련 된 클레임 규칙을 계획, 설계 및 배포 하는 데 필요한 작업이 포함 되어 있습니다.  
  
> [!NOTE]  
> 이 검사 목록의 작업을 순서대로 완료하세요. 참조 링크가 절차를 안내하는 경우 이 검사 목록의 나머지 작업을 계속 진행하려면 해당 절차의 단계를 완료한 후 이 항목으로 돌아와야 합니다.  
  
![ 클레임 규칙 만들기 @ no__t-1 검사 목록: 신뢰 당사자 트러스트에 대 한 클레임 규칙 집합 만들기 @ no__t-0  
  
||태스크|참조|  
|-|--------|-------------|  
|![클레임 규칙 만들기](media/icon_checkboxo.gif)|클레임에 대 한 개념을 검토, 클레임 규칙, 클레임 규칙 집합 및 클레임 규칙 템플릿 및 페더레이션된 트러스트와 연관 되는 방식이 있습니다.|![creating 규칙 만들기](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[클레임의 역할](../../ad-fs/technical-reference/The-Role-of-Claims.md)<br /><br />![ 클레임 규칙 만들기](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[클레임 규칙의 역할](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md)|  
|![클레임 규칙 만들기](media/icon_checkboxo.gif)|클레임 발급 파이프라인의 모든 단계를 통해 클레임을 전달 하는 방법 및 클레임 발급 엔진에서 규칙은 처리 하는 방법에 대 한 개념을 검토 합니다.|![ 클레임 규칙 만들기](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[클레임 파이프라인의 역할](../../ad-fs/technical-reference/The-Role-of-the-Claims-Pipeline.md)<br /><br />![ 클레임 규칙을 만드는](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[클레임 엔진의 역할](../../ad-fs/technical-reference/The-Role-of-the-Claims-Engine.md)|  
|![클레임 규칙 만들기](media/icon_checkboxo.gif)|효과적으로 계획 하 고이 신뢰 당사자 트러스트를 통해 발생 하는 출력 클레임을 구현, 하나 이상의 클레임 규칙이 필요한 여부와 규칙을 사용할지이 신뢰 당사자 트러스트 클레임을 결정 합니다.|![ 클레임 규칙을 만드는](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[데 사용할 클레임 규칙 템플릿 유형을 결정 합니다](../../ad-fs/technical-reference/Determine-the-Type-of-Claim-Rule-Template-to-Use.md) .|  
|![클레임 규칙 만들기](media/icon_checkboxo.gif)|다른 규칙 및 클레임 규칙 언어를 사용 하 여 이상적인 출력에서 원하는 결과 제공 하기 위해 표준 규칙 보다 더 복잡 한 논리를 제공 하는 방법을 클레임 집합을 한 클레임을 만들려는 경우에 대 한 개념을 검토 합니다.|@no__t-](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[통과 또는 필터 클레임 규칙을 사용 하는 경우](../../ad-fs/technical-reference/When-to-Use-a-Pass-Through-or-Filter-Claim-Rule.md) 클레임 규칙 만들기<br /><br />![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[변환 클레임 규칙을 사용 하는 경우](../../ad-fs/technical-reference/When-to-Use-a-Transform-Claim-Rule.md) 클레임 규칙 만들기<br /><br />![ 클레임 규칙을](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[사용 하](../../ad-fs/technical-reference/When-to-Use-a-Send-LDAP-Attributes-as-Claims-Rule.md) 여 클레임 규칙을 만듭니다.<br /><br />![ 클레임 규칙](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[으로 송신 그룹 구성원을 사용 하는 경우 클레임 규칙](../../ad-fs/technical-reference/When-to-Use-a-Send-Group-Membership-as-a-Claim-Rule.md) 을 만듭니다.<br /><br />![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[권한 부여 클레임 규칙을 사용 하는 경우](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md) 클레임 규칙 만들기<br /><br />![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[사용자 지정 클레임 규칙을 사용 하는 경우](../../ad-fs/technical-reference/When-to-Use-a-Custom-Claim-Rule.md) 클레임 규칙 만들기<br /><br />![ 클레임 규칙을 만드는](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[클레임 규칙 언어의 역할](../../ad-fs/technical-reference/The-Role-of-the-Claim-Rule-Language.md)|  
|![클레임 규칙 만들기](media/icon_checkboxo.gif)|클레임 설명 아직 없는 경우 만들어야 하는 조직의 요구를 충족 합니다. AD FS 노출 되는 클레임 설명의 기본 집합을 기본 제공 AD FS 관리 스냅인에서\-에 있습니다.|![ 클레임 규칙 만들기](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[클레임 설명 추가](../../ad-fs/operations/Add-a-Claim-Description.md)|  
|![클레임 규칙 만들기](media/icon_checkboxo.gif)|조직의 요구에 따라 클레임 적절 하 게 실행 될 수 있도록이 신뢰 당사자 트러스트와 연결 된 규칙 집합에 대 한 하나 이상의 클레임 규칙을 만듭니다.|![ 클레임 규칙](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[을 만들어 들어오는 클레임을 통과 또는 필터링 하는 규칙을 만듭니다](../../ad-fs/operations/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim.md) .<br /><br />![ 클레임 규칙](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[을 만드는 규칙을 만들어 LDAP 특성을 클레임으로 보내기](../../ad-fs/operations/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims.md)<br /><br />![ 클레임 규칙 만들기](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[그룹 구성원을 클레임으로 전송 하는 규칙을 만듭니다](../../ad-fs/operations/Create-a-Rule-to-Send-Group-Membership-as-a-Claim.md) .<br /><br />![ 클레임 규칙 만들기](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[들어오는 클레임을 변환 하는 규칙을 만듭니다](../../ad-fs/operations/Create-a-Rule-to-Transform-an-Incoming-Claim.md) .<br /><br />![ 클레임 규칙 만들기](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[인증 방법 클레임을 보내는 규칙을 만듭니다](../../ad-fs/operations/Create-a-Rule-to-Send-an-Authentication-Method-Claim.md) .<br /><br />![ 클레임 규칙 만들기](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[AD FS 1.X 호환 클레임을 보내는 규칙을 만듭니다.](../../ad-fs/operations/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim.md)<br /><br />![ 클레임 규칙 만들기](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[사용자 지정 규칙을 사용 하 여 클레임을 보내는 규칙을 만듭니다](../../ad-fs/operations/Create-a-Rule-to-Send-Claims-Using-a-Custom-Rule.md) .|  
|![클레임 규칙 만들기](media/icon_checkboxo.gif)|조직의 요구에 따라 발급 권한 부여 규칙 집합 또는 사용자가 액세스 하도록 허가할 신뢰 당사자 있도록이 신뢰 당사자 트러스트와 연결 되는 위임 권한 부여 규칙 집합에 대 한 하나 이상의 클레임 규칙을 만듭니다.|![ 클레임 규칙 만들기](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[모든 사용자를 허용 하는 규칙을 만듭니다](../../ad-fs/operations/Create-a-Rule-to-Permit-All-Users.md) .<br /><br />![ 클레임 규칙 만들기](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[들어오는 클레임을 기준으로 사용자를 허용 하거나 거부 하는 규칙을 만듭니다](../../ad-fs/operations/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim.md) .|  
