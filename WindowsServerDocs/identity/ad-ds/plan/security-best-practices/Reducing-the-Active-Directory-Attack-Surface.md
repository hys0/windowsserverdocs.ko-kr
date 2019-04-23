---
ms.assetid: 864ad4bc-8428-4a8b-8671-cb93b68b0c03
title: Active Directory 공격에 대한 취약성 줄이기
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: d692641d316b5fe7206cc3f413bdcfc9b74675b9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59874154"
---
# <a name="reducing-the-active-directory-attack-surface"></a>Active Directory 공격에 대한 취약성 줄이기

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 섹션에서는 Active Directory 설치의 공격 표면을 줄이기 위해 구현 하는 기술 컨트롤에 중점을 둡니다. 섹션에는 다음 정보가 들어 있습니다.  
  
-   [최소 권한 관리 모델 구현](../../../ad-ds/plan/security-best-practices/../../../ad-ds/plan/security-best-practices/Implementing-Least-Privilege-Administrative-Models.md) 사용 높은 권한이 있지만 위험 식별에 초점을 맞춥니다 위험을 줄이려면 구현 되는 권장 사항을 제공 하는 것 외에도 일상적인 관리를 제공에 대 한 계정 해당 권한이 있는 계정입니다.  
  
-   [보안 관리 호스트 구현](../../../ad-ds/plan/security-best-practices/Implementing-Secure-Administrative-Hosts.md) 몇 가지 샘플 외에도 전용, 보안 관리 시스템의 배포 보안 관리 호스트를 배포 하는 방법에 대 한 원칙을 설명 합니다.  
  
-   [공격에 대 한 도메인 컨트롤러 보안](../../../ad-ds/plan/security-best-practices/Securing-Domain-Controllers-Against-Attack.md) 정책 및 보안 관리 호스트의 구현에 대 한 권장 사항을 유사 하지만 일부 도메인 컨트롤러 관련 하기 위한 권장 사항을 포함 하는 설정을 설명 합니다. 도메인 컨트롤러 및 관리 하는 데 시스템 보안이 되는지 확인 합니다.  
  
## <a name="privileged-accounts-and-groups-in-active-directory"></a>권한 있는 계정 및 Active Directory의 그룹  
이 섹션에서는 권한 있는 계정에 대 한 배경 정보를 제공 하며 Active Directory에서 그룹 공통점 및 Active Directory의 권한 있는 계정 및 그룹 간 차이점에 설명. 이러한 차이 이해 하면 여부 구현 권장 사항을 [최소 권한 관리 모델 구현](../../../ad-ds/plan/security-best-practices/../../../ad-ds/plan/security-best-practices/Implementing-Least-Privilege-Administrative-Models.md) 축 자 또는 조직에 맞게 선택, 해야 할 도구가 있는 각 그룹 및 계정을 적절 하 게 보호 합니다.  
  
### <a name="built-in-privileged-accounts-and-groups"></a>기본 제공 계정 및 그룹 권한  
Active Directory 위임 관리를 용이 하 게 하 고 권한 및 사용 권한 할당에 최소 권한의 원칙을 지원 합니다. 도메인에 계정이 있는 "일반" 사용자는 기본적으로 대부분의 디렉터리에 저장 된 것을 읽을 수는 있지만 디렉터리에는 데이터의 매우 제한 된 집합만 변경할 수 있습니다. 추가 권한이 필요한 사용자 역할에 관련 된 특정 작업을 수행할 수 있지만 업무와 관련 되지 않은 작업을 수행할 수 없습니다 있도록 디렉터리에 기본 제공 되는 다양 한 "권한 있는" 그룹의 멤버 자격을 부여할 수 있습니다. 조직에서는 특정 직무에 맞는 및 세분화 된 권한 및 IT 직원이 작업을 초과 하는 사용 권한과 권한 부여 하지 않고 일상적인 관리 기능을 수행할 수 있도록 권한을 부여 하는 그룹을 만들 수도 이러한 함수에 필요 합니다.  
  
Active Directory 내에서 세 가지 기본 제공 그룹 다음과 같습니다. 디렉터리에 가장 높은 권한 그룹 Enterprise Admins, Domain Admins 및 관리자를 선택 합니다. 기본 구성 및 기능 이러한 각 그룹의 다음 섹션에 설명 되어 있습니다.  
  
#### <a name="highest-privilege-groups-in-active-directory"></a>Active Directory에서 가장 높은 권한 그룹  
  
##### <a name="enterprise-admins"></a>Enterprise Admins  
Enterprise Admins (EA) 그룹 포리스트 루트 도메인에만 존재 하는 이며 기본적으로 포리스트의 모든 도메인의 관리자 그룹의 구성원입니다. 포리스트 루트 도메인에 내장 된 Administrator 계정을 EA 그룹의 유일한 기본 멤버는 합니다. EAs는 추가 또는 제거 하는 도메인, 포리스트 트러스트를 설정 또는 포리스트 기능 수준 올리기 등 권한 및 포리스트 차원의 변경 (즉, 포리스트의 모든 도메인에 영향을 주는)를 구현할 수 있는 권한이 부여 됩니다. 제대로 설계 및 구현 된 위임 모델에서는 먼저 포리스트를 구성 하는 경우에 또는 아웃 바운드 포리스트 트러스트를 구축 하는 등 특정 포리스트 차원의 변경을 수행할 때 EA 멤버 자격이 필요 합니다. EA 그룹에 부여 된 권한과의 가장 낮은 사용자 및 그룹에 위임할 수 있습니다.  
  
##### <a name="domain-admins"></a>Domain Admins  

포리스트의 각 도메인에 도메인에 가입 된 모든 컴퓨터에서 로컬 Administrators 그룹의 멤버인 해당 도메인의 관리자 그룹의 구성원 인 자체 도메인 관리자 (DA) 그룹을 있습니다. 도메인에 대 한 DA 그룹의 유일한 기본 멤버는 해당 도메인에 대 한 기본 제공 관리자 계정. DAs는 EAs 포리스트 전체 권한을 있지만 자신의 도메인 내에서 "모음"입니다. 제대로 설계 및 구현 된 위임 모델에서 Domain Admins의 구성원 이어야 "비상" 시나리오 (예: 상황에는 모든 컴퓨터를 도메인에 대 한 높은 수준의 권한 있는 계정 필요)에 받아야 합니다. 네이티브 Active Directory 위임 메커니즘 위임 정도로 DA 계정을 응급 시나리오에만 사용할 수 있기를 허용 하지만 효과적인 위임 모델 생성 시간이 오래 걸릴 수 있으며 많은 조직에서 활용 타사 도구 신속 하 게 처리 합니다.  
  
##### <a name="administrators"></a>Administrators  
세 번째 그룹에 넣을 DAs과 EAs 중첩 기본 제공 도메인 로컬 관리자 (BA) 그룹이입니다. 이 그룹에는 대부분의 직접 권한 및 도메인 컨트롤러와 디렉터리에 대 한 권한이 부여 됩니다. 그러나 도메인에 대 한 관리자 그룹 구성원 서버 또는 워크스테이션에 권한이 없습니다. 로컬 권한 부여 되는 컴퓨터의 로컬 Administrators 그룹의 멤버 자격을 통해 것입니다.  
  
> [!NOTE]  
> 이러한 옵션은 이러한 권한 있는 그룹의 기본 구성의 3 개 그룹의 멤버인 다른 그룹의 구성원을 얻으려고 디렉터리를 조작할 수 있습니다. 일부 경우에는 더 어렵게 하지만 잠재적인 문제점 관점에서 세 그룹 고려해 야과 동등 다른 그룹의 멤버 자격을 얻으려면 간단 합니다.  
  
##### <a name="schema-admins"></a>Schema Admins  

네 번째 그룹, 권한 있는 포리스트 루트 도메인에만 존재 하 고 Enterprise Admins 그룹 비슷합니다 기본 멤버로 해당 도메인의 기본 제공 관리자 계정에 스키마 관리자 (SA). Schema Admins 그룹 일시적 으로만 및 경우에 따라 (AD DS 스키마의 수정이 필요한 경우)를 채울 수 것입니다.  
  
SA 그룹의 권한 및 사용 권한 범위는 앞에서 설명한 보다 제한적 이라는 것 SA 그룹의 유일한 그룹 (즉, 개체 및 특성과 같은 디렉터리의 기본 데이터 구조)에 Active Directory 스키마를 수정할 수 있는 경우에 그룹입니다. 일반적으로 그룹의 멤버 자격이 필요 자주 고 짧은 시간 동안만 조직 SA 그룹의 멤버 자격 관리에 대 한 적절 한 사례를 개발 했습니다 하는 경우가 일반적 이기도 합니다. EA, DA 및 BA 그룹의 Active Directory에도 기술적으로 마찬가지 이지만 훨씬 더 일반적인 조직 SA 그룹의 경우 이러한 그룹에 대 한 비슷한 사례에 구현 되어 있는지를 찾으려고 합니다.  
  
#### <a name="protected-accounts-and-groups-in-active-directory"></a>보호 된 계정 및 Active Directory의 그룹  
Active Directory 내에서 권한 있는 계정 및 그룹의 기본 집합이 "보호 된" 계정 이라는 및 그룹 디렉터리에 다른 개체와 다르게 보호 됩니다. 이 제한 된 보안을 상속 하는 모든 보호 된 그룹 (에 관계 없이 여부 구성원은 보안 또는 메일 그룹에서 파생 됨)에 직접 또는 전이적 멤버 자격이 있는 모든 계정.  

  
예를 들어 사용자가 메일 그룹의 멤버 즉, Active Directory 사용자 개체에서에서 보호 그룹의 구성원은 보호 된 계정으로 표시 됩니다. 계정이 보호 된 계정으로 플래그가 지정 되 면 개체에 대 한 adminCount 특성의 값을 1로 설정 됩니다.  
  
> [!NOTE]
> 보호 그룹의 전이적 멤버 자격이 중첩 된 배포 및 중첩 된 보안 그룹에 있지만 중첩 된 배포 그룹의 구성원 인 계정을 보호 그룹의 SID 액세스 토큰에에 받지 못합니다. 그러나 배포 그룹 보호 되는 그룹 멤버가 열거형에 포함 된 이유는 Active Directory 보안 그룹에는 배포 그룹을 변환할 수 있습니다. 이전 배포 그룹의 구성원은 부모 받습니다 이후에 계정을 다음 로그온 할 때 해당 액세스 토큰에서 그룹의 SID를 보호 해야 보호 된 메일 그룹이 중첩된 된 적이 변환할 수는 보안 그룹.  
  
다음 표에서 기본 보호 된 계정 및 운영 체제 버전 및 서비스 팩 수준에 따라 Active Directory에서 그룹을 나열합니다.  
  
**기본 운영 체제 및 서비스 팩 (SP) 버전에서 Active Directory의 보호 된 계정 및 그룹**  
  
|||||  
|-|-|-|-|  
|**Windows 2000 <SP4**|**Windows 2000 SP4 -Windows Server 2003**|**Windows Server 2003 SP1+**|**Windows Server 2008 -Windows Server 2012**|  
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
모든 Active Directory 도메인의 시스템 컨테이너의 AdminSDHolder 라는 개체가 자동으로 만들어집니다. AdminSDHolder 개체의 목적은 보호 된 계정 및 그룹에 대 한 권한을 일관 되 게 적용 하는 도메인에서 보호 그룹 및 계정 위치에 관계 없이 되도록 합니다.  

기본적으로, 60 분 마다 보안 설명자 전파자 (SDProp) 이라는 프로세스는 도메인의 PDC 에뮬레이터 역할을 보유 하는 도메인 컨트롤러에서 실행 됩니다. SDProp 보호 된 계정 및 도메인에서 그룹에 대 한 권한 사용 하 여 도메인의 AdminSDHolder 개체에 대 한 권한을 비교합니다. 보호 된 계정 및 그룹에 대 한 권한을 AdminSDHolder 개체에 대 한 권한을 일치 하지 않으면, 보호 된 계정 및 그룹에 대 한 권한은 도메인의 AdminSDHolder 개체의과 일치 하도록 다시 설정 됩니다.  
  
계정 또는 그룹은 디렉터리에서 다른 위치로 이동, 경우에 해당 권한을 상속 하지 않는 새 부모 개체로에서 의미 있는 보호 된 그룹 및 계정에서 사용 권한 상속이 비활성화 됩니다. 부모 개체에 사용 권한 변경 내용을 AdminSDHolder의 권한은 변경 되지 않습니다 있도록 AdminSDHolder 개체에 상속도 비활성화 됩니다.  
  
> [!NOTE]
> 계정이 보호 된 그룹에서 제거 되 면 해당 adminCount 특성은 계속 수동으로 변경 되지 않으면 1로 설정 하지만 보호 된 계정에 더 이상 간주 됩니다. SDProp를 하 여 개체의 Acl은 더 이상 업데이트 되지만 여전히 개체 부모 개체에서 권한을 상속 하지 않습니다는이 구성 됩니다. 따라서 개체는 조직 구성 단위 (OU) 권한이 위임 된, 하지만 이전의 보호 된 개체는 이러한 위임 된 권한을 상속 하지에 있을 수 있습니다. 찾은 도메인에서 이전의 보호 된 개체를 다시 설정 하는 스크립트를 찾을 수 있습니다 합니다 [Microsoft 지원 문서 817433](https://support.microsoft.com/?id=817433)합니다.  
  
###### <a name="adminsdholder-ownership"></a>AdminSDHolder 소유권  
Active Directory에서 대부분의 개체는 도메인의 BA 그룹에 의해 소유 됩니다. 그러나 AdminSDHolder 개체를 기본적으로 소유한 도메인의 DA 그룹입니다. (이는 DAs 파생 되지 않은 도메인에 대 한 관리자 그룹의 멤버 자격을 통해 권한과 해당 상황이 발생 합니다.)  
  
Windows Server 2008 보다 이전 버전 Windows의 소유자 개체의 원래 되어 있지 않은 사용 권한 직접 부여를 포함 하 여 개체의 권한을 변경할 수 있습니다. 따라서 도메인의 AdminSDHolder 개체에 대 한 기본 권한을 도메인의 AdminSDHolder 개체에 대 한 사용 권한 변경 BA 또는 EA 그룹의 구성원 인 사용자를 방지 합니다. 그러나 도메인에 대 한 관리자 그룹의 멤버 개체의 소유권을 자체 추가 권한을 부여, 즉,이 보호 기본적인 이며 사용자가 실수로 변경 하지 않도록 개체 보호 도메인의 DA 그룹의 멤버가 아닌 합니다. 또한 EA 고 BA (있는 경우) 그룹 (EA에 대 한 루트 도메인) 로컬 도메인의 AdminSDHolder 개체의 특성을 변경 하는 권한을 가집니다.  
  
> [!NOTE]  
> DSHeuristics, AdminSDHolder 개체에 대 한 특성 보호 되는 그룹 라고 하며 AdminSDHolder 및 SDProp 영향을 받지는 그룹의 제한 된 사용자 지정 (제거)을 허용 합니다. 이 사용자 지정 신중 하 게 고려해 야 구현 되는 경우 유효한 경우가 수정 dSHeuristics AdminSDHolder에 유용 하지만 합니다. AdminSDHolder 개체에 dSHeuristics 특성의 수정에 대 한 자세한 내용은 Microsoft 지원 문서에서 찾을 수 있습니다 [817433](https://support.microsoft.com/?id=817433) 하 고 [973840](https://support.microsoft.com/kb/973840), 및 [부록 c: 보호 된 계정 및 Active Directory에서 그룹](Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory.md)합니다.  
  
다른 여러 가지 있지만 Active Directory에서 가장 권한이 있는 그룹은 여기에 설명 된, 권한이 부여 된 그룹 수준의 권한 상승 합니다. 모든 기본 및 Active Directory 및 각각에 할당 된 사용자 권한에서 기본 제공 그룹에 대 한 자세한 내용은 참조 하세요. [부록 b: 권한 있는 계정 및 Active Directory에서 그룹](../../../ad-ds/plan/security-best-practices/Appendix-B--Privileged-Accounts-and-Groups-in-Active-Directory.md)합니다.  
  


