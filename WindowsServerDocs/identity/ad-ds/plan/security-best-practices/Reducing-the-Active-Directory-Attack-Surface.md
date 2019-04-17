---
ms.assetid: 864ad4bc-8428-4a8b-8671-cb93b68b0c03
title: "Active Directory 공격 줄이기"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: b2de254076b10a1a75d658f006c2245d523de6b7
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="reducing-the-active-directory-attack-surface"></a>Active Directory 공격 줄이기

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 섹션의 Active Directory 설치 하든지을 구현 하기 기술 컨트롤에 초점을 맞춥니다. 섹션에는 다음과 같은 정보가 포함 되어 있습니다.  
  
-   [최소 권한 관리 모델 구현](../../../ad-ds/plan/security-best-practices/../../../ad-ds/plan/security-best-practices/Implementing-Least-Privilege-Administrative-Models.md) 식별 권한 있는 계정 존재 하는 위험을 완화 하기 구현 하는 추천을 제공할 뿐만 아니라 일상적인 관리에 대해 매우 권한이 있는 계정 사용을 제공 하는 위험에 초점을 맞춥니다.  
  
-   [안전 하 게 관리 호스트 구현](../../../ad-ds/plan/security-best-practices/Implementing-Secure-Administrative-Hosts.md) 원칙 뿐만 아니라 몇 가지 전용, 안전 하 게 관리 시스템 배포 안전 하 게 관리 호스트 배포 추적 방법에 대해 설명 합니다.  
  
-   [도메인 컨트롤러 공격 으로부터 보호할](../../../ad-ds/plan/security-best-practices/Securing-Domain-Controllers-Against-Attack.md) 정책 및 보안 관리 호스트 구현에 대 한 추천 유사 하지만 도메인 컨트롤러 및 관리 하기 위해 사용 되는 시스템은 보안이 보장 하기 위해 일부 도메인 컨트롤러 관련 추천을 포함 하는 설정에 설명 합니다.  
  
## <a name="privileged-accounts-and-groups-in-active-directory"></a>권한 계정과 그룹 Active Directory에  
이 섹션 권한이 있는 계정에 대 한 배경 정보를 제공 하며 Active Directory에 있는 그룹 드 및 Active Directory에 그룹 권한이 있는 계정 간의 차이점을 설명 하는 것입니다. 이러한 차이점을 이해 여부를 구현할의 권장 [구현 최소 권한 관리 모델](../../../ad-ds/plan/security-best-practices/../../../ad-ds/plan/security-best-practices/Implementing-Least-Privilege-Administrative-Models.md) 말한 그대로 옮긴 조직에 대 한 지정 하도록 선택할를 사용 하는 각 그룹 보안을 유지 하 고 계정 적절 하 게 하는 데 필요한 도구 하거나 합니다.  
  
### <a name="built-in-privileged-accounts-and-groups"></a>기본 제공 특권 계정 및 그룹  
Active Directory 관리 위임 용이 하 게 및 최소 권한 원칙 권한과 할당를 지원 합니다. 도메인에 있는 계정이 있는 "일반" 사용자는 기본적으로 디렉터리에 저장 된 많이 읽을 수 있지만 매우 제한 된 집합 디렉터리에 데이터를 변경할 수 있습니다. 사용자는 추가 사용 권한이 필요한의 역할와 관련 된 특정 작업을 수행할 수 있으 해당 관세와 관련 된 작업을 수행할 수 없는 되도록 디렉터리에 기본 제공 되는 다양 한 "권한" 그룹 구성원에에서 부여할 수 있습니다. 조직에서는 특정 업무에 맞게는 세밀 권한 및 IT 직원이 권리와 해당 기능을 위해 필요한 것을 초과 하는 사용 권한을 부여 하지 않고 일상적인 관리 기능을 수행할 수 있도록 사용 권한을 부여 됩니다 그룹을 만들 수도 있습니다.  
  
세 가지 기본 제공 그룹은 디렉터리에 최고 권한 그룹 Active Directory 내: 엔터프라이즈 관리, 도메인 관리자 및 관리자입니다. 이러한 각 그룹의 기능과 기본 구성 다음 섹션에 설명 되어:  
  
#### <a name="highest-privilege-groups-in-active-directory"></a>최고 권한 그룹 Active Directory에  
  
##### <a name="enterprise-admins"></a>엔터프라이즈 관리  
엔터프라이즈 관리자 (EA)만 숲 루트 도메인에에서 있는 그룹 이며 기본적으로 모든 도메인 숲의 관리자가 그룹의 회원은 합니다. 숲 루트 도메인에 기본 제공 된 관리자 계정에만 기본 멤버 EA 그룹입니다. EAs 추가 하거나 제거 하는 도메인, 숲 신뢰 설정 숲 기능 수준 향상 등 권리와 숲 수준 변경 (즉, 변경 되는 숲 속의 모든 도메인에 영향을 주는)를 구현할 수 있도록 하는 사용 권한을 부여 됩니다. 먼저 숲 생성 하거나 아웃 바운드 숲 신뢰 설정와 같은 특정 숲 수준 변경 하는 경우에 제대로 설계 및 구현 위임 모델 EA 멤버십이 해야 합니다. 대부분의 권한 및 EA 그룹에 허용 된 권한 덜 권한이 사용자 및 그룹으로 위임 수 있습니다.  
  
##### <a name="domain-admins"></a>도메인 관리  

한 숲 속의 각 도메인 해당 도메인 관리자가 그룹의 회원 이며 도메인에 가입 하는 모든 컴퓨터에서 로컬 관리자가 그룹의 회원 자체 도메인 관리자 (DA) 그룹을 있습니다. 도메인에 대 한 DA 그룹의만 기본 멤버 해당 도메인에 대 한 기본 제공 된 관리자 계정입니다. 숲 전체 권한이 EAs DAs 되는 도메인 내 "모든 권한을 가집니다" 됩니다. 제대로 설계 및 구현 위임 모델 도메인 관리자 멤버십 "유리창 중단" 경우 (예: 높은 수준의 권한을 통해 계정을 도메인에 있는 모든 컴퓨터에 필요한 경우)에 받아야 합니다. 기본 Active Directory 위임 메커니즘 위임 하는 DA 계정을 긴급 한 경우에만 사용할 수를 허용 하지만 효과적인 위임 모델 구성 시간이 오래 걸릴 수 있으며 프로세스 신속 하 게 하는 제 3 자 도구를 활용 하는 많은 조직 있습니다.  
  
##### <a name="administrators"></a>관리자  
세 번째 그룹에 있는 DAs 및 EAs 중첩 된 기본 도메인 로컬 관리자 (모음) 그룹이입니다. 이 그룹 많은 직접 권한 및 디렉터리에 및 도메인 컨트롤러에서 사용 권한을 부여 됩니다. 그러나 도메인에 대 한 관리자가 그룹 구성원 서버 또는 워크스테이션 권한이 없습니다. 로컬 권한이 부여 된 컴퓨터의 로컬 관리자가 그룹의 회원 통해입니다.  
  
> [!NOTE]  
> 이러한 옵션은 기본 구성 권한이 부여 된 이러한 그룹을 세 그룹의 모든 구성원이 디렉터리의 다른 그룹 구성원을 얻을 수를 조작할 수 있습니다. 경우에 따라 다른 더욱 어렵게 표시 되지만 가능한 권한은 관점 세 그룹 모두 고려해 야 효과적으로 해당 하는 동안 다른 그룹의 회원 가져오는 간단 합니다.  
  
##### <a name="schema-admins"></a>스키마 관리  

4 번째 그룹 특권 스키마 관리자 (SA) 숲 루트 도메인에만 있고에 해당 도메인 기본 관리자 계정이 유사한 Enterprise 관리자 그룹에 기본 멤버와 합니다. 때때로 (AD DS 스키마를 수정 필요한 경우) 및에 일시적으로 채워지지 스키마 관리자 그룹 것입니다.  
  
SA 그룹 Active Directory 스키마 (해당 군도, 디렉터리의 기본 데이터 구조 개체와 특성 등)을 수정할 수 있는 유일한 그룹을 수 있지만 SA 그룹 권한과의 범위 앞에서 설명한 그룹 보다 제한적입니다. 그룹의 회원 일반적으로 필요 자주 때문에 및 짧은 기간 동안에만 조직 SA 그룹의 회원 관리에 대 한 적절 한 관행은 개발 많기 이기도 합니다. 기술적 EA, DA, 및 모음 그룹의 Active Directory에도 마찬가지입니다 하지만 덜까지 일반적으로 찾기 조직 이러한 그룹 SA 그룹 내용에 대 한 유사 사례를 구현 했습니다.  
  
#### <a name="protected-accounts-and-groups-in-active-directory"></a>계정을 보호 하 고 그룹 Active Directory에  
Active Directory 내에서 권한이 있는 계정 및 그룹의 기본 설정 "보호 된" 계정 이라고 및 그룹 디렉터리의 다른 개체 다르게 보호 됩니다. 직접 또는 전이 멤버십 (관계 없이 여부 구성원은 보안 및 배포 그룹에서 파생) 보호 그룹에 있는 모든 계정이 제한 된 보안을 상속 합니다.  

  
예를 들어, 사용자가 메일 그룹의 회원 즉, Active Directory 개체 사용자의에서 보호 그룹의 회원 보호 된 계정으로 표시 됩니다. 계정을 보호 된 계정으로 플래그가, 개체 adminCount 특성 값 1로 설정 됩니다.  
  
> [!NOTE]
> 보호 되는 그룹의 회원 전이적 포함 중첩된 메일 및 그룹 중첩 된 보안, 되지만 중첩된 메일 그룹의 회원 계정 보호 그룹 SID 액세스 토큰에에 받지 않습니다. 그러나, 메일 그룹 보안 그룹 하는 이유 메일 그룹 구성원 열거형 보호 그룹에에서 포함 된 Active Directory에으로 변환 될 수 있습니다. 전자 메일 그룹의 회원 부모 받습니다 이후에 계정 보호 중첩된 메일 그룹 개가 변환 되어야 보안 그룹을 그룹의 SID 다음 로그온 액세스 토큰에를 보호 합니다.  
  
다음 표에서 기본 보호 계정과 Active Directory 운영 체제 버전 및 서비스 팩 수준에서 그룹입니다.  
  
**계정 및 운영 체제 및 서비스 팩을 버전 Active Directory에 그룹 기본 보호**  
  
|||||  
|-|-|-|-|  
|**Windows 2000 < s p 4**|**Windows 2000 s p 4-Windows Server 2003**|**Windows Server 2003 s p 1 +**|**Windows Server 2008-Windows Server 2012**|  
|관리자|계정에서|계정에서|계정에서|  
||관리자|관리자|관리자|  
||관리자|관리자|관리자|  
|도메인 관리|백업 관리자|백업 관리자|백업 관리자|  
||인증 게시자|||  
||도메인 관리|도메인 관리|도메인 관리|  
|엔터프라이즈 관리|도메인 컨트롤러|도메인 컨트롤러|도메인 컨트롤러|  
||엔터프라이즈 관리|엔터프라이즈 관리|엔터프라이즈 관리|  
||Krbtgt|Krbtgt|Krbtgt|  
||연산자 인쇄|연산자 인쇄|연산자 인쇄|  
||||읽기 도메인 컨트롤러|  
||복제|복제|복제|  
|스키마 관리|스키마 관리||스키마 관리|  
  
##### <a name="adminsdholder-and-sdprop"></a>AdminSDHolder 및 SDProp  
모든 Active Directory 도메인의 시스템 컨테이너 AdminSDHolder 라는 개체 자동으로 만들어집니다. AdminSDHolder 개체의 목적은 보호 계정과 그룹에 대 한 권한을 일관 되 게 적용 되도록, 보호 그룹과 계정을 도메인에 있는에 관계 없이 하는 것입니다.  

기본적으로, 60 분 마다 보안 설명자 전파 (SDProp)로 알려진 프로세스는 도메인 PDC 에뮬레이터 역할 도메인 컨트롤러에서 실행 됩니다. SDProp 보호 계정과 도메인에 있는 그룹에 대 한 권한 된 도메인의 AdminSDHolder 개체에 대 한 권한을 비교합니다. 보호 된 계정 및 그룹 중 하나에 대 한 권한을 AdminSDHolder 개체에 대 한 권한을 일치 하지 않는 경우 도메인의 AdminSDHolder 개체 일치 하도록 보호 계정과 그룹에 대 한 권한은 다시 설정 됩니다.  
  
계정 또는 그룹을 디렉터리의 다른 위치로 이동 하는 경우에 자녀가 권한을 상속 하지 않는 새로운 상위 개체의 의미 보호 그룹과 계정에서 사용 권한을 상속 비활성화 되었습니다. AdminSDHolder 개체 부모 개체 사용 권한 변경 AdminSDHolder의 사용 권한 변경 되지 않는 상속도는 사용할 수 없습니다.  
  
> [!NOTE]
> 보호 되는 그룹에서 계정이 제거 되 면 더 이상으로 간주 됩니다 보호 계정 되지만 해당 adminCount 특성 수동으로 변경 되지 않는 경우 1로 설정 합니다. 이 구성 결과 개체의 Acl SDProp,으로 업데이트 되어 더 이상 있지만 아직 개체 부모 개체에서 사용 권한을 상속 되지 않습니다. 따라서 개체 조직 (OU) 권한이 위임 된 있지만 이전 보호 개체 위임된 사용 권한을 상속 하지는에 있을 수 있습니다. 스크립트를 찾아 이전의 보호 되는 도메인의 개체 다시 설정에 있습니다는 [Microsoft 지원 문서 817433](https://support.microsoft.com/?id=817433)합니다.  
  
###### <a name="adminsdholder-ownership"></a>AdminSDHolder 절감  
대부분의 Active Directory 개체는 도메인의 모음 그룹 담당 합니다. 그러나 AdminSDHolder 개체, 기본적으로 소유한 도메인의 DA 그룹입니다. (없는 DAs 파생 되지 않은 도메인에 대 한 관리자가 그룹의 회원 통해 권한과 상황입니다.)  
  
Windows Server 2008 이전 버전의 Windows에서 개체의 소유자 사용 권한을 자체 원래 되어 있지 않은 사용 권한을 부여 개체를 변경할 수 있습니다. 따라서 도메인의 AdminSDHolder 개체에 기본 사용 권한 변경 도메인의 AdminSDHolder 개체에 대 한 권한을 모음 또는 EA 그룹의 회원 사용자가 방지 합니다. 그러나 도메인에 대 한 관리자가 그룹의 회원 개체의 소유권을 하 고 직접 추가 권한을 부여,이 보호 기본적인 이며만 개체 실수로 변경 하지 사용자가 도메인에 있는 DA 그룹의 회원 되지 않도록 보호 의미 하는 수 있습니다. 또한 모음 및 EA (있는 경우) AdminSDHolder 로컬 도메인 (루트 EA 도메인)의 개체의 특성을 변경할 수 있는 권한이 그룹입니다.  
  
> [!NOTE]  
> AdminSDHolder 개체 dSHeuristics에 특성 제한 된 사용자 지정할 수 있습니다 (제거) 보호 그룹 정보로 간주 되어 있는 AdminSDHolder 및 SDProp 영향을 받는 그룹입니다. 이러한 사용자 지정 신중 하 게 고려해 야 구현 않은 경우 유효한 상황이 수정 dSHeuristics AdminSDHolder에는 유용 하지만 합니다. AdminSDHolder 개체 dSHeuristics 특성 수정에 대 한 자세한 내용은 Microsoft 지원 문서에서 찾을 수 있습니다 [817433](https://support.microsoft.com/?id=817433) 및 [973840](https://support.microsoft.com/kb/973840)의 [부록 c: 보호 계정 및 Active Directory에 그룹](Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory.md)합니다.  
  
다른 여러 가지 Active Directory에 가장 권한이 있는 그룹 여기 설명 하지만 그룹 허용 된 권한 레벨 높은 합니다. 기본 및 Active Directory 및 각 할당 사용자 권한을에 기본 제공 그룹의 모든에 대 한 자세한 내용은 참조 [부록 b: 권한이 있는 계정 및 Active Directory에 그룹](../../../ad-ds/plan/security-best-practices/Appendix-B--Privileged-Accounts-and-Groups-in-Active-Directory.md)합니다.  
  


