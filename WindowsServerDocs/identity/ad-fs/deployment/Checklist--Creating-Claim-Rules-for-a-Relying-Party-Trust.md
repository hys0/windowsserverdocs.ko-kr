---
ms.assetid: 44271f44-b50a-4bce-9375-4fcab9618048
title: "목록에 당사자에 대 한 청구 규칙 만들기 신뢰"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 9c75cd4ccbafefdda83cba4551fd6b9af63c4822
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="checklist-creating-claim-rules-for-a-relying-party-trust"></a>검사: 신뢰 파티 보안에 대 한 청구 규칙 만들기

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 검사는 계획, 디자인 및 배포 클레임 규칙 관련 된 Active Directory Federation Services \(AD FS\)에 신뢰 파티 신뢰 하는 데 필요한는 작업이 포함 됩니다.  
  
> [!NOTE]  
> 주문에서이 검사의 작업을 완료 합니다. 이 검사에서 나머지 작업 진행할 수 있도록이 절차의 단계를 완료 한 후이 항목을 참조 링크는 절차로 이동 때 돌아갑니다.  
  
![규칙 주장 만들기](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**검사: 신뢰 파티 보안에 대 한 설정 클레임 규칙 만들기**  
  
||작업|참조|  
|-|--------|-------------|  
|![클레임은 규칙 만들기](media/icon_checkboxo.gif)|클레임 개념을 검토 규칙 주장 규칙 집합 주장 및 규칙 템플릿와 연결 된 신뢰와 관련 된 어떻게 청구 합니다.|![규칙 주장 만들기](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[The 역할 클레임](../../ad-fs/technical-reference/The-Role-of-Claims.md)<br /><br />![규칙 주장 만들기](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[주장 규칙의 역할은](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md)|  
|![클레임은 규칙 만들기](media/icon_checkboxo.gif)|클레임 발급 파이프라인의 모든 단계를 통해 클레임은 어떻게 이동 및 규칙은 클레임 발급 엔진에서 처리 하는 방법에 대 한 개념 검토 합니다.|![규칙 주장 만들기](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[클레임 파이프라인 The 역할](../../ad-fs/technical-reference/The-Role-of-the-Claims-Pipeline.md)<br /><br />![규칙 주장 만들기](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[클레임 엔진 The 역할](../../ad-fs/technical-reference/The-Role-of-the-Claims-Engine.md)|  
|![클레임은 규칙 만들기](media/icon_checkboxo.gif)|효과적으로 계획 하 고 신뢰 파티 신뢰가 실행 되는 출력 클레임 구현, 하나 이상의 클레임 규칙 필요한 지 여부 및 파티 신뢰 의존이 사용 해야 규칙 주장 하는 확인 합니다.|![규칙 주장 만들기](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[종류의 주장 규칙 템플릿을 사용 확인](../../ad-fs/technical-reference/Determine-the-Type-of-Claim-Rule-Template-to-Use.md)|  
|![클레임은 규칙 만들기](media/icon_checkboxo.gif)|다른 규칙과 이상적 출력에서 원하는 결과 제공 하기 위해 표준 규칙 보다 더 복잡 한 논리를 제공 하기 위해 클레임 규칙 언어를 사용 하는 방법을 주장 설정 하나의 클레임을 만들 때 개념에 대 한 검토 합니다.|![규칙 주장 만들기](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[통과 또는 주장 규칙 필터를 사용 하는 경우](../../ad-fs/technical-reference/When-to-Use-a-Pass-Through-or-Filter-Claim-Rule.md)<br /><br />![규칙 주장 만들기](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[변환 주장 규칙을 사용 하는 경우](../../ad-fs/technical-reference/When-to-Use-a-Transform-Claim-Rule.md)<br /><br />![규칙 주장 만들기](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[보내기 LDAP 특성 클레임 일반적으로 사용 하는 경우](../../ad-fs/technical-reference/When-to-Use-a-Send-LDAP-Attributes-as-Claims-Rule.md)<br /><br />![규칙 주장 만들기](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[보내기 그룹 구성원 주장 일반적으로 사용 하는 경우](../../ad-fs/technical-reference/When-to-Use-a-Send-Group-Membership-as-a-Claim-Rule.md)<br /><br />![규칙 주장 만들기](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[승인 주장 규칙을 사용 하는 경우](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)<br /><br />![규칙 주장 만들기](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[사용자 지정 주장 규칙을 사용 하는 경우](../../ad-fs/technical-reference/When-to-Use-a-Custom-Claim-Rule.md)<br /><br />![규칙 주장 만들기](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[주장 규칙 언어의 The 역할](../../ad-fs/technical-reference/The-Role-of-the-Claim-Rule-Language.md)|  
|![클레임은 규칙 만들기](media/icon_checkboxo.gif)|클레임 설명 아직 없는 경우 만들 수 있어야 하는 조직의의 요구를 충족 됩니다. Adfs는 snap\에서 광고 FS 관리에 표시 된 청구 설명의 기본 설정으로 제공 됩니다.|![규칙 주장 만들기](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[주장 설명을 추가](../../ad-fs/operations/Add-a-Claim-Description.md)|  
|![클레임은 규칙 만들기](media/icon_checkboxo.gif)|조직의 필요에 따라 클레임 적절 하 게 발급 한가 신뢰 파티 신뢰가와 관련 된 규칙 집합에 대 한 하나 또는 여러 개의 클레임 규칙을 만듭니다.|![규칙 주장 만들기](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[통과 하는 규칙 만들거나 들어오는 주장 필터링](../../ad-fs/operations/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim.md)<br /><br />![규칙 주장 만들기](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[규칙을 보낼 LDAP 특성 클레임으로 만들기](../../ad-fs/operations/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims.md)<br /><br />![규칙 주장 만들기](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[클레임으로 그룹 구성원 보내기 규칙 만들기](../../ad-fs/operations/Create-a-Rule-to-Send-Group-Membership-as-a-Claim.md)<br /><br />![규칙 주장 만들기](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[들어오는 주장 변환할 규칙 만들기](../../ad-fs/operations/Create-a-Rule-to-Transform-an-Incoming-Claim.md)<br /><br />![규칙 주장 만들기](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[인증 방법을 클레임 보내려면 규칙 만들기](../../ad-fs/operations/Create-a-Rule-to-Send-an-Authentication-Method-Claim.md)<br /><br />![규칙 주장 만들기](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[ADFS 보내려면 규칙 1.x 호환 주장](../../ad-fs/operations/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim.md)<br /><br />![규칙 주장 만들기](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[보내기 클레임 사용 규칙을 사용자 지정 규칙 만들기](../../ad-fs/operations/Create-a-Rule-to-Send-Claims-Using-a-Custom-Rule.md)|  
|![클레임은 규칙 만들기](media/icon_checkboxo.gif)|조직의 필요에 따라 발급 인증 규칙 설정 또는 사용자가 허용 액세스 당사자에 수 있도록이 신뢰 파티 보안와 관련 된 위임 인증 규칙 설정에 대 한 하나 또는 여러 개의 클레임 규칙을 만듭니다.|![규칙 주장 만들기](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[규칙 모든 사용자가 허용 만들기](../../ad-fs/operations/Create-a-Rule-to-Permit-All-Users.md)<br /><br />![규칙 주장 만들기](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[들어오는 주장에 규칙을 허용 하거나 사용자가 기반 거부 만들기](../../ad-fs/operations/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim.md)|  
