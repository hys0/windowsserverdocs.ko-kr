---
ms.assetid: 696a29b2-d627-4c9a-a384-9c8aaf50bd23
title: 사용할 클레임 규칙 템플릿 유형 결정
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f1d38e23d7f1671f729b03b7e6f8000471d2e9f9
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66188652"
---
# <a name="determine-the-type-of-claim-rule-template-to-use"></a>사용할 클레임 규칙 템플릿 유형 결정


Active Directory 페더레이션 서비스를 디자인 하는 중요 한 부분은 \(AD FS\) 인프라 전체 클레임 규칙 집합을 결정 하는-는 해당 클레임 규칙 템플릿을 만드는 데 사용 해야 하 고, 각 파트너에 대 한 사용자의 조직과 페더레이션에 참여 합니다. AD FS 관리 스냅인에서 클레임 규칙 템플릿을 사용 하 여 규칙을 만들면\-에서 합니다.  
  
구성한 각 클레임 규칙 집합은 하나의 페더레이션된 트러스트에만 연결될 수 있습니다. 즉, 하나의 트러스트에 규칙 집합을 만든 후 페더레이션 서비스의 다른 트러스트에 사용할 수 없습니다. 대신, 각 페더레이션된 파트너와 조직 간에 합의된 원하는 클레임 집합을 보다 신속하게 생성하기 위해 클레임 규칙 템플릿에서 쉽게 규칙을 만들 수 있습니다.  
  
규칙 및 규칙 템플릿에 대한 자세한 내용은 [The Role of Claim Rules](The-Role-of-Claim-Rules.md)을 참조하세요.  
  
사용해야 하는 클레임 규칙 템플릿 유형을 결정하기 전에 다음 질문을 고려해 보세요.  
  
-   신뢰할 수 있는 클레임 공급자가 어떤 클레임을 제공하나요?  
  
-   각 클레임 공급자의 어떤 클레임을 신뢰하나요?  
  
-   이 페더레이션 서비스를 신뢰하는 신뢰 당사자가 어떤 클레임을 요구하나요?  
  
-   각 신뢰 당사자에게 어떤 클레임을 공개하실 것인가요?  
  
-   어떤 사용자가 각 신뢰 당사자에 액세스할 수 있어야 하나요?  
  
이러한 질문에 대답하면 견고한 클레임 규칙 디자인을 계획하는 데 도움이 됩니다. 또한 매끄러운 권한 부여 및 액세스 제어 전략을 만들고 배포 팀이 롤아웃 중에 보다 효율적으로 작업하는 데 도움이 됩니다.  
  
이 다음 섹션에서는 비즈니스 요구에 따라 해당 환경에 대해 선택할 규칙 템플릿 유형에 대해 알아볼 수 있습니다.  
  
## <a name="claim-rule-template-types"></a>클레임 규칙 템플릿 유형  
다음 표에 AD FS 관리 스냅인을 사용 하 여 규칙을 만드는 데 사용할 수 있는 클레임 규칙 템플릿의 유형의 모든\-에서 각 템플릿 유형의 사용 하 여 다른 경우의 이점과 합니다.  
  
|규칙 템플릿 유형|설명|장점|단점|  
|----------------------|---------------|--------------|-----------------|  
|들어오는 클레임 통과 또는 필터링|선택한 클레임 유형에 대한 모든 클레임 값을 통과하거나 선택한 클레임 유형에 대한 특정 클레임 값만 통과하도록 클레임 값에 따라 클레임을 필터링하는 규칙을 만드는 데 사용됩니다.<br /><br />자세한 내용은 [When to Use a Pass Through or Filter Claim Rule](When-to-Use-a-Pass-Through-or-Filter-Claim-Rule.md)를 참조하세요.|-특정 클레임을 수락 하거나 발급을 선택 하는데 사용할 수 변경|클레임 형식 및 값을 변경할 수 없습니다|  
|들어오는 클레임 변환|들어오는 클레임을 선택하고 다른 클레임 유형에 매핑하거나 해당 클레임 값을 새 클레임 값에 매핑할 수 있는 규칙을 만드는 데 사용됩니다.<br /><br />자세한 내용은 [When to Use a Transform Claim Rule](When-to-Use-a-Transform-Claim-Rule.md)를 참조하세요.|-클레임 유형 또는 값을 정규화 할 수 있습니다.<br />-바꾸면 e\-들어오는 클레임의 메일 접미사|-더 복잡 한 대체 문자열을 사용자 지정 규칙이 필요|  
|LDAP 특성을 클레임으로 보내기|LDAP 특성 저장소에서 신뢰 당사자에게 클레임으로 보낼 특성을 선택하는 규칙을 만드는 데 사용됩니다.<br /><br />자세한 내용은 [When to Use a Send LDAP Attributes as Claims Rule](When-to-Use-a-Send-LDAP-Attributes-as-Claims-Rule.md)를 참조하세요.|-모든 AD DS에서 클레임을 소싱할 수\/AD LDS 특성 저장소<br />-단일 규칙을 사용 하 여 여러 클레임을 발급할 수 있습니다.|성능 – 계정 조회의 결과로 느립니다.<br />-사용자 지정 LDAP 필터를 사용 하 여 쿼리용 수 없습니다.|  
|그룹 구성원을 클레임으로 보내기|사용자가 Active Directory 보안 그룹의 구성원인 경우 지정된 클레임 유형 및 값을 보낼 수 있는 규칙을 만드는 데 사용됩니다. 선택한 그룹에 따라 하나의 클레임만 이 규칙을 사용하여 전송됩니다.<br /><br />자세한 내용은 [When to Use a Send Group Membership as a Claim Rule](When-to-Use-a-Send-Group-Membership-as-a-Claim-Rule.md)를 참조하세요.|-계정 조회가 없습니다. 그룹 클레임을 발급 하는 것에 대 한 빠른 성능|사용자는 로컬 Active Directory 그룹의 구성원 이어야 합니다.|  
|사용자 지정 규칙을 사용하여 클레임 보내기|표준 규칙 템플릿보다 많은 고급 옵션을 제공하는 사용자 지정 규칙을 만드는 데 사용됩니다. AD FS 사용 하 여 사용자 지정 규칙 클레임 규칙 언어 작성 합니다.<br /><br />자세한 내용은 [When to Use a Custom Claim Rule](When-to-Use-a-Custom-Claim-Rule.md)를 참조하세요.|-SQL 특성 저장소에서 클레임을 소싱 하 사용할 수<br />-사용자 지정 LDAP 필터를 지정 하려면 사용할 수 있습니다.<br />-PPID를 실행 하는 데 사용 될 수 있습니다.<br />-사용 하 여 사용자 지정 특성 저장소<br />-입력된 클레임 집합에만 클레임을 추가 하려면 사용할 수 있습니다.<br />-둘 이상의 들어오는 클레임을 기반으로 하는 클레임을 보내도록 사용할 수 있습니다.|-구성 하기가 어렵습니다 \- 시간이를 초기에 클레임 규칙 언어에 대 한 지식이 필요할 수 있습니다|  
|들어오는 클레임에 따라 사용자 허용 또는 거부|들어오는 클레임의 유형 및 값에 따라 사용자가 신뢰 당사자에 대해 액세스를 허용하거나 거부하는 규칙을 만드는 데 사용됩니다.<br /><br />자세한 내용은 [When to Use an Authorization Claim Rule](When-to-Use-an-Authorization-Claim-Rule.md)를 참조하세요.|--권한 부여 프로세스를 간소화 하는 중|-필요 하나 및 하나만 클레임 유형을 클레임 값 지정<br />-클레임 값에 대해 패턴 일치를 지원 하지 않습니다.|  
|모든 사용자 허용|모든 사용자가 신뢰 당사자에 액세스할 수 있도록 하는 규칙을 만드는 데 사용됩니다.<br /><br />자세한 내용은 [When to Use an Authorization Claim Rule](When-to-Use-an-Authorization-Claim-Rule.md)를 참조하세요.|-간단 하 게 구성|들어오는 클레임 서식 파일에 허용 또는 거부 사용자 기반을 사용 하 여 보다 안전한 작음|  
  

