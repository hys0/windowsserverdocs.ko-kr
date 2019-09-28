---
ms.assetid: 864ad4bc-8428-4a8b-8671-cb93b68b0c03
title: Active Directory 공격에 대한 취약성 줄이기
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 94bc65d42fa90dd7c93ba759a41d34edec10de09
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71367650"
---
# <a name="reducing-the-active-directory-attack-surface"></a>Active Directory 공격에 대한 취약성 줄이기

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 섹션에서는 Active Directory 설치의 공격 노출 영역을 줄이기 위해 구현 하는 기술 컨트롤에 대해 집중적으로 설명 합니다. 섹션에는 다음 정보가 포함 되어 있습니다.  
  
-   [최소 권한 관리 모델을 구현](../../../ad-ds/plan/security-best-practices/../../../ad-ds/plan/security-best-practices/Implementing-Least-Privilege-Administrative-Models.md) 하는 것은 일상적인 관리를 위해 매우 특권 수준의 계정을 사용 하는 경우의 위험을 줄이기 위해 구현 하는 권장 사항을 제공 하는 것 외에도 중요 합니다. 권한 있는 계정이 있습니다.  
  
-   보안 [관리 호스트를 구현](../../../ad-ds/plan/security-best-practices/Implementing-Secure-Administrative-Hosts.md) 하면 보안 관리 호스트 배포에 대 한 몇 가지 샘플 방법 뿐만 아니라 전용 보안 관리 시스템의 배포에 대 한 원칙을 설명 합니다.  
  
-   [도메인 컨트롤러를 공격 으로부터 보호](../../../ad-ds/plan/security-best-practices/Securing-Domain-Controllers-Against-Attack.md) 하는 것은 보안 관리 호스트의 구현에 대 한 권장 사항과 유사 하지만 몇 가지 도메인 컨트롤러 관련 권장 사항을 포함 하는 정책 및 설정을 설명 합니다. 도메인 컨트롤러와 이러한 컨트롤러를 관리 하는 데 사용 되는 시스템은 잘 보호 되어야 합니다.  
  
## <a name="privileged-accounts-and-groups-in-active-directory"></a>Active Directory의 권한 있는 계정 및 그룹  
이 섹션에서는 Active Directory의 권한 있는 계정 및 그룹 간의 차이점을 설명 하기 위해 Active Directory의 권한 있는 계정 및 그룹에 대 한 배경 정보를 제공 합니다. 이러한 차이점을 이해 하면 [최소 권한 관리 모델을 구현](../../../ad-ds/plan/security-best-practices/../../../ad-ds/plan/security-best-practices/Implementing-Least-Privilege-Administrative-Models.md) 하는 데 권장 사항을 구현 하거나 조직에 맞게 사용자 지정 하도록 선택 하는 등의 방법으로 각 그룹을 보호 하는 데 필요한 도구를 사용할 수 있습니다. 계정을 적절 하 게 합니다.  
  
### <a name="built-in-privileged-accounts-and-groups"></a>기본 제공 계정 및 그룹 권한  
Active Directory는 관리 위임을 용이 하 게 하 고 권한 및 사용 권한을 할당 하는 최소 권한 원칙을 지원 합니다. 도메인에 계정이 있는 "일반" 사용자는 기본적으로 디렉터리에 저장 된 항목의 대부분을 읽을 수 있지만 디렉터리에 있는 데이터의 매우 제한 된 집합만 변경할 수 있습니다. 추가 권한이 필요한 사용자는 해당 역할과 관련 된 특정 작업을 수행할 수 있지만 해당 의무와 관련이 없는 작업을 수행할 수 없도록 디렉터리에 기본 제공 되는 다양 한 "권한 있는" 그룹의 멤버 자격을 부여할 수 있습니다. 또한 조직에서는 특정 업무 담당 업무에 맞게 조정 된 그룹을 만들 수 있으며, IT 직원이이를 초과 하는 권한 및 사용 권한을 부여 하지 않고도 일상적인 관리 기능을 수행할 수 있도록 하는 세분화 된 권한 및 사용 권한이 부여 됩니다. 는 이러한 함수에 필요 합니다.  
  
Active Directory 내에서 세 개의 기본 제공 그룹은 디렉터리의 가장 높은 권한 그룹입니다. Enterprise Admins, Domain Admins 및 Administrators. 다음 섹션에서는 이러한 각 그룹의 기본 구성 및 기능에 대해 설명 합니다.  
  
#### <a name="highest-privilege-groups-in-active-directory"></a>Active Directory의 가장 높은 권한 그룹  
  
##### <a name="enterprise-admins"></a>Enterprise Admins  
EA (Enterprise Admins)는 포리스트 루트 도메인에만 존재 하는 그룹 이며, 기본적으로 포리스트의 모든 도메인에서 Administrators 그룹의 구성원입니다. 포리스트 루트 도메인의 기본 제공 관리자 계정은 EA 그룹의 유일한 기본 멤버입니다. EAs에는 도메인 추가 또는 제거, 포리스트 트러스트 설정 또는 포리스트 기능 수준 올리기와 같이 포리스트 전체 변경 내용 (포리스트의 모든 도메인에 영향을 주는 변경 내용)을 구현할 수 있는 권한 및 사용 권한이 부여 됩니다. 제대로 설계 및 구현 된 위임 모델에서는 먼저 포리스트를 구성 하는 경우에 또는 아웃 바운드 포리스트 트러스트를 구축 하는 등 특정 포리스트 차원의 변경을 수행할 때 EA 멤버 자격이 필요 합니다. EA 그룹에 부여 된 권한 및 사용 권한은 대부분 권한이 낮은 사용자 및 그룹에 위임할 수 있습니다.  
  
##### <a name="domain-admins"></a>Domain Admins  

포리스트의 각 도메인에는 해당 도메인의 관리자 그룹의 구성원이 고 도메인에 가입 된 모든 컴퓨터에서 로컬 Administrators 그룹의 구성원 인 자체 도메인 관리자 (DA) 그룹이 있습니다. 도메인에 대 한 DA 그룹의 유일한 기본 멤버는 해당 도메인에 대 한 기본 제공 관리자 계정입니다. DAs는 도메인 내에서 "모두 강력한" 반면, EAs에는 포리스트 차원의 권한이 있습니다. 제대로 설계 되 고 구현 된 위임 모델에서는 도메인 관리자 멤버 자격이 "중단" 시나리오 (도메인의 모든 컴퓨터에 대 한 높은 수준의 권한이 있는 계정을 필요로 하는 경우)에만 필요 합니다. 네이티브 Active Directory 위임 메커니즘으로는 응급 시나리오 에서만 DA 계정을 사용할 수 있는 범위를 위임할 수 있지만 효과적인 위임 모델을 구성 하는 데는 많은 시간이 소요 될 수 있으며 많은 조직에서 프로세스를 신속 하 게 진행 하기 위한 타사 도구입니다.  
  
##### <a name="administrators"></a>Administrators  
세 번째 그룹은 DAs 및 EAs가 중첩 된 기본 제공 도메인 로컬 관리자 (BA) 그룹입니다. 이 그룹에는 디렉터리 및 도메인 컨트롤러에서 많은 직접 권한 및 사용 권한이 부여 됩니다. 그러나 도메인의 관리자 그룹은 구성원 서버 또는 워크스테이션에 대 한 권한이 없습니다. 로컬 권한이 부여 된 컴퓨터의 로컬 관리자 그룹의 멤버 자격을 통해입니다.  
  
> [!NOTE]  
> 이러한 권한 있는 그룹의 기본 구성 이지만 세 그룹 중 하나의 멤버가 다른 그룹의 멤버 자격을 얻기 위해 디렉터리를 조작할 수 있습니다. 경우에 따라 다른 그룹의 멤버 자격을 얻을 수는 있지만 다른 그룹의 멤버 자격을 얻는 것은 어려울 수 있습니다. 하지만 잠재적 권한 측면에서 볼 때 세 그룹 모두 효과적으로 동일한 것으로 간주 되어야 합니다.  
  
##### <a name="schema-admins"></a>Schema Admins  

네 번째 권한 있는 그룹인 스키마 관리자 (SA)는 포리스트 루트 도메인에만 존재 하며 Enterprise Admins 그룹과 마찬가지로 기본 구성원으로 해당 도메인의 기본 제공 관리자 계정만 갖습니다. Schema Admins 그룹은 일시적이 고 가끔씩만 채워질 수 있습니다 (AD DS 스키마를 수정 해야 하는 경우).  
  
SA 그룹은 Active Directory 스키마를 수정할 수 있는 유일한 그룹 이지만 (즉, 디렉터리의 기본 데이터 구조 (예: 개체 및 특성), SA 그룹의 권한 및 사용 권한 범위는 앞에서 설명한 것 보다 제한 됩니다. 그룹과. 또한 그룹의 멤버 자격은 일반적으로 자주 필요 하지 않으며 짧은 기간 동안만 SA 그룹의 멤버 자격 관리에 대 한 적절 한 방법을 개발 하는 것을 발견 하는 것이 일반적입니다. 이는 Active Directory의 EA, DA 및 BA 그룹에 기술적으로 적용 되지만, 조직에서 이러한 그룹에 대 한 유사한 방법을 SA 그룹에 구현 하는 것을 확인 하는 것은 일반적이 지 않습니다.  
  
#### <a name="protected-accounts-and-groups-in-active-directory"></a>Active Directory의 보호 된 계정 및 그룹  
Active Directory 내에서 "protected" 계정 및 그룹 이라는 기본 권한 있는 계정 집합과 그룹은 디렉터리의 다른 개체와 다르게 보호 됩니다. 보호 되는 그룹에 직접 또는 전이적 멤버 자격이 있는 모든 계정 (멤버 자격이 보안 또는 배포 그룹에서 파생 되었는지 여부에 관계 없이)은이 제한 된 보안을 상속 합니다.  

  
예를 들어 사용자가 메일 그룹의 멤버인 경우에는 Active Directory에서 보호 되는 그룹의 구성원 인 경우 해당 사용자 개체는 보호 된 계정으로 플래그가 지정 됩니다. 계정이 보호 된 계정으로 플래그가 지정 되 면 개체의 adminCount 특성 값이 1로 설정 됩니다.  
  
> [!NOTE]
> 보호 된 그룹의 전이적 구성원은 중첩 된 배포 및 중첩 된 보안 그룹을 포함 하지만 중첩 된 메일 그룹의 멤버인 계정은 해당 액세스 토큰에서 보호 되는 그룹의 SID를 받지 않습니다. 그러나 Active Directory에서 메일 그룹을 보안 그룹으로 변환할 수 있습니다 .이는 배포 그룹이 보호 된 그룹 구성원 열거에 포함 되는 이유입니다. 보호 된 중첩 된 메일 그룹을 보안 그룹으로 변환 해야 하는 경우에는 다음에 로그온 할 때 이전 메일 그룹의 멤버인 계정이 액세스 토큰에서 부모 보호 그룹의 SID를 받게 됩니다.  
  
다음 표에서는 운영 체제 버전 및 Service Pack 수준에서 Active Directory의 기본 보호 된 계정 및 그룹을 나열 합니다.  
  
**운영 체제 및 SP (서비스 팩) 버전에 의해 Active Directory의 기본 보호 된 계정 및 그룹**  
  
|||||  
|-|-|-|-|  
|**Windows 2000 < SP4**|**Windows 2000 SP4-Windows Server 2003**|**Windows Server 2003 SP1 이상**|**Windows Server 2008-Windows Server 2012**|  
|Administrators|Account Operators|Account Operators|Account Operators|  
||관리자|관리자|관리자|  
||Administrators|Administrators|Administrators|  
|Domain Admins|Backup Operators|Backup Operators|Backup Operators|  
||Cert Publishers|||  
||Domain Admins|Domain Admins|Domain Admins|  
|Enterprise Admins|도메인 컨트롤러 하나 이상|도메인 컨트롤러 하나 이상|도메인 컨트롤러 하나 이상|  
||Enterprise Admins|Enterprise Admins|Enterprise Admins|  
||Krbtgt|Krbtgt|Krbtgt|  
||Print Operators|Print Operators|Print Operators|  
||||Read-only Domain Controllers|  
||Replicator|Replicator|Replicator|  
|Schema Admins|Schema Admins||Schema Admins|  
  
##### <a name="adminsdholder-and-sdprop"></a>AdminSDHolder 및 SDProp  
모든 Active Directory 도메인의 시스템 컨테이너에서 AdminSDHolder 라는 개체가 자동으로 생성 됩니다. AdminSDHolder 개체의 목적은 보호 된 그룹과 계정이 도메인에 있는 위치에 관계 없이 보호 된 계정 및 그룹에 대 한 사용 권한이 일관 되 게 적용 되도록 하는 것입니다.  

60 분 마다 (기본적으로), 보안 설명자 전파자 (SDProp) 라는 프로세스는 도메인의 PDC 에뮬레이터 역할을 보유 하는 도메인 컨트롤러에서 실행 됩니다. SDProp는 도메인의 AdminSDHolder 개체에 대 한 사용 권한을 보호 된 계정 및 도메인의 그룹에 대 한 권한과 비교 합니다. 보호 된 계정 및 그룹에 대 한 사용 권한이 AdminSDHolder 개체에 대 한 사용 권한과 일치 하지 않으면 보호 된 계정 및 그룹에 대 한 사용 권한이 도메인의 AdminSDHolder 개체와 일치 하도록 다시 설정 됩니다.  
  
보호 된 그룹 및 계정에 대 한 사용 권한 상속이 사용 하지 않도록 설정 되어 있습니다. 즉, 계정이 나 그룹이 디렉터리의 다른 위치로 이동 하더라도 새 부모 개체에서 사용 권한을 상속 하지 않습니다. 부모 개체에 대 한 사용 권한이 AdminSDHolder의 사용 권한을 변경 하지 않도록 AdminSDHolder 개체에 대 한 상속도 사용 하지 않도록 설정 됩니다.  
  
> [!NOTE]
> 보호 된 그룹에서 계정이 제거 되 면 더 이상 보호 된 계정으로 간주 되지 않지만, 수동으로 변경 되지 않은 경우 해당 adminCount 특성은 1로 설정 된 상태로 유지 됩니다. 이 구성의 결과로 개체의 Acl이 SDProp에 의해 더 이상 업데이트 되지 않지만 개체는 여전히 부모 개체에서 사용 권한을 상속 하지 않습니다. 따라서 개체는 권한이 위임 된 OU (조직 구성 단위)에 상주할 수 있지만 이전에 보호 된 개체는 이러한 위임 된 권한을 상속 하지 않습니다. 도메인에서 이전에 보호 된 개체를 찾아 다시 설정 하는 스크립트는 [Microsoft 지원 문서 817433](https://support.microsoft.com/?id=817433)에서 찾을 수 있습니다.  
  
###### <a name="adminsdholder-ownership"></a>AdminSDHolder 소유권  
Active Directory의 대부분 개체는 도메인의 BA 그룹이 소유 합니다. 그러나 AdminSDHolder 개체는 기본적으로 도메인의 DA 그룹에서 소유 합니다. (이 경우 DAs는 도메인에 대 한 관리자 그룹의 멤버 자격을 통해 권한 및 사용 권한을 파생 하지 않습니다.)  
  
Windows Server 2008 이전 버전의 Windows에서는 개체 소유자가 원래 권한이 없는 권한을 부여 하는 것을 포함 하 여 개체의 사용 권한을 변경할 수 있습니다. 따라서 도메인의 AdminSDHolder 개체에 대 한 기본 권한을 사용 하면 BA 또는 EA 그룹의 멤버인 사용자가 도메인의 AdminSDHolder 개체에 대 한 사용 권한을 변경할 수 없습니다. 그러나 도메인에 대 한 관리자 그룹의 멤버는 개체의 소유권을 가지 며 자신에 게 추가 권한을 부여할 수 있습니다. 즉,이 보호는 기초적인 기능이 며, 도메인에 있는 DA 그룹의 구성원이 아닙니다. 또한 BA 및 EA (해당 하는 경우) 그룹에는 로컬 도메인 (EA에 대 한 루트 도메인)에 있는 AdminSDHolder 개체의 특성을 변경할 수 있는 권한이 있습니다.  
  
> [!NOTE]  
> AdminSDHolder 개체 dSHeuristics의 특성은 보호 된 그룹으로 간주 되며 AdminSDHolder 및 SDProp의 영향을 받는 그룹의 제한 된 사용자 지정 (제거)을 허용 합니다. 이 사용자 지정은 AdminSDHolder에서 dSHeuristics을 수정 하는 데 유용한 유효한 상황이 있기는 하지만 구현 된 경우 신중 하 게 고려해 야 합니다. AdminSDHolder 개체에서 dSHeuristics 특성을 수정 하는 방법에 대 한 자세한 내용은 Microsoft 지원 문서 [817433](https://support.microsoft.com/?id=817433) 및 [973840](https://support.microsoft.com/kb/973840)및 [appendix C에서 찾을 수 있습니다. Active Directory @ no__t의 보호 된 계정 및 그룹-0.  
  
Active Directory에서 가장 권한 있는 그룹은 여기에 설명 되어 있지만 상승 된 권한 수준이 부여 된 여러 다른 그룹이 있습니다. Active Directory의 모든 기본 및 기본 제공 그룹과 각 그룹에 할당 된 사용자 권한에 대 한 자세한 내용은 [Appendix B: Active Directory @ no__t의 권한 있는 계정 및 그룹  
  


