---
ms.assetid: 84754c23-f039-4de4-a378-853942e662df
title: 소개
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 8e2717af6183944b26a71e55b36f31cef51cf2e7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59831874"
---
# <a name="introduction"></a>소개

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

컴퓨터와 간단 하거나 복잡 하 든 컴퓨팅 인프라에 대 한 공격 있었을 수 있습니다. 그러나 지난 10년 동안 전세계 모든 규모, 모든 분야에서 기존의 위협 환경을 크게 변경한 방법으로 공격 및 피해를 당하는 기업들이 점점 늘어나고 있습니다. 사이버 전쟁과 사이버 범죄는 유례없는 속도로 증가해 왔습니다. "핵,"는 공격 activist 위치로 동기 부여는 동기 위반 횟수에 대 한 서비스 거부를 만들려면 조직 비밀 정보를 노출 하도록 의도 한 대로 클레임 또는 인프라 파괴 되었습니다. 빼내기를 사용 하 여 공용 및 사설 기관 공격 조직의 IP (지적재산권) 되 고 유비쿼터스 있습니다.  
  
정보 기술 (IT) 인프라를 사용 하 여 조직이 없습니다 적절 한 정책, 프로세스 및 컨트롤의 공격 으로부터 조직의 컴퓨팅 인프라의 주요 부문을 보호 하기 위해 구현 됩니다 있지만 공격 으로부터 무효 임 손상 완료 침투 안전할 수 있습니다. 조직 외부에서 발생 하는 공격의 규모와 수는 최근 몇 년 동안에서 내부자 위협 은폐에, 때문에 권한 있는 사용자 환경의 오용 보다는 외부 공격자가 자주이 문서에 설명 합니다. 그럼에도 불구 하 고 원리와이 문서의 권장 사항은 외부 공격자와 참가자 실수 또는 고의적 공격 으로부터 환경을 보호를 돕기 위해 고안 되었습니다.  
  
정보 및이 문서의 권장 사항은 다양 한 원본에서에서 가져온 되며 손상에 대 한 Active Directory 설치 보호 하도록 디자인 된 사례에서 파생 됩니다. 가능한 Active Directory 공격 표면을 줄이기 위해 하는 컨트롤을 구현 하는 공격을 방지 하려면 가능한 경우에 공격자가 훨씬 더 어렵습니다 디렉터리의 손상 됩니다. 이 문서에서 관찰 된 손상 된 환경 및 해당 Active Directory 설치의 보안을 개선 하기 위해 고객에 게 만들었습니다 가장 일반적인 권장 사항이 있다고 하는 취약점의 가장 일반적인 종류를 표시 합니다.  
  
## <a name="account-and-group-naming-conventions"></a>계정 및 그룹 이름 지정 규칙  
다음 표에서 그룹 및 문서 전체에서 참조 하는 계정에 대 한이 문서에 사용 된 명명 규칙에 대 한 지침을 제공 합니다. 테이블에 포함 된 각 계정/그룹, 해당 이름 및이 문서에서는 이러한 계정/그룹 참조 하는 방법을의 위치가입니다.  
  


|**그룹 계정 위치**|**계정/그룹의 이름**|**이 문서에서 참조 되는 방식**|
| --- | --- | --- |   
|Active Directory-각 도메인|관리자|기본 제공 관리자 계정|  
|Active Directory-각 도메인|Administrators|기본 제공 관리자 (BA) 그룹|  
|Active Directory-각 도메인|Domain Admins|도메인 관리자 (DA) 그룹|  
|Active Directory 포리스트 루트 도메인|Enterprise Admins|Enterprise Admins (EA) 그룹|  
|도메인 컨트롤러가 아닌 Windows 서버 및 워크스테이션을 실행 하는 컴퓨터에서 로컬 컴퓨터 보안 계정 관리자 (SAM) 데이터베이스|관리자|로컬 관리자 계정|  
|도메인 컨트롤러가 아닌 Windows 서버 및 워크스테이션을 실행 하는 컴퓨터에서 로컬 컴퓨터 보안 계정 관리자 (SAM) 데이터베이스|Administrators|로컬 관리자 그룹|  
  
## <a name="about-this-document"></a>이 문서에 대 한  
Microsoft Information Technology (MSIT)의 구성 요소인 Microsoft 정보 보안 및 위험 관리 (ISRM) 조직의 내부 비즈니스 단위, 외부 고객 및 업계 동료를 수집 하 고 배포 하 고, 정책을 정의 사용 하 여 작동 사례 및 컨트롤입니다. 이 정보를 보안을 높이고 IT 인프라의 공격 표면을 줄이기 Microsoft 및 고객에서 사용할 수 있습니다. 이 문서에는 권장 사항은 다양 한 정보 소스 및 MSIT 및 ISRM 내에서 사용 사례를 기반으로 합니다. 다음 섹션에서는이 문서의 원본에 대 한 자세한 정보를 제공합니다.  
  
### <a name="microsoft-it-and-isrm"></a>Microsoft IT 및 ISRM  
다양 한 방법과 컨트롤 내에서 MSIT ISRM Microsoft AD DS 포리스트 및 도메인 보호를 위해 개발 되었습니다. 이러한 컨트롤을 광범위 하 게 적용 하는 경우는이 문서에 통합 되었습니다. 안전한-T (새로운 기술에 대 한 Solution Accelerator)는 ISRM 인 기본 문서는 새로운 기술을 식별 하 고 해당 도입을 가속화 하는 컨트롤 및 보안 요구 사항 정의 내에서 팀이 합니다.  
  
### <a name="active-directory-security-assessments"></a>Active Directory 보안 평가  
내의 내부 Microsoft 사업부와 외부 고객은 응용 프로그램 및 인프라 보안을 평가 하 고 전략 지침을 제공 하기를 늘리려면 Microsoft ISRM, 평가, 컨설팅, 및 엔지니어링 (ACE) 팀에서 작동 합니다 조직의 보안 상태입니다. 한 ACE 서비스 제공에는 Active Directory 보안 평가 (ADSA), 사람, 프로세스 및 기술을 평가 하 고 고객에 따라 권장 구성을 생성 하는 조직의 AD DS 환경의 전체적인 평가입니다. 고객은 조직의 고유한 특성, 방법 및 위험 성향 지를 기반으로 하는 권장 사항 제공 됩니다. Microsoft에서 고객 외에도 Active Directory 설치에 대 한 ADSAs 수행 되었습니다. 시간에 따른 권장 사항 수가 다양 한 크기 및 업계의 고객 간에 적용할 발견 되었습니다.  
  
### <a name="content-origin-and-organization"></a>내용 출처 및 구성  
이 문서의 대부분은 ADSA 및 손상 된 고객 및 중요 한 손상을 경험 하지 않았기 하는 고객에 대해 수행 하는 다른 ACE 팀 평가에서 파생 됩니다. 개별 고객 데이터를이 문서를 만드는 사용 하지 않은 하지만 수집 되는 가장 일반적으로 악용된 된 취약성 당사의 평가 및 권장 사항을 만들었습니다 고객에 게 해당 AD DS의 보안을 개선 하기 위해 설치 합니다. 모든 취약성이 모든 환경에 적용되는 것은 아니며 마찬가지로 모든 권장 사항이 모든 조직에서 구현하기에 적합한 것은 아닙니다.  
  
이 문서는 다음과 같이 구성 됩니다.  
  
## <a name="executive-summary"></a>요약  
Executive 요약, 독립 실행형 문서 또는 전체 문서와 함께에서 읽을 수에이 문서의 요약을 제공 합니다. 새 AD DS를 배포 하려는 고객에 대 한 Active Directory 설치의 경우와 기본 목표를 보호 하기 위한 요약 권장 사항, 고객 환경을 손상 시키는 데 사용 되는 사실이 관찰 되었습니다 가장 일반적인 공격 벡터는 Executive 요약에 포함 지금 또는 나중에 포리스트.  
  
### <a name="introduction"></a>소개  
지금 읽고 있는 섹션입니다.  
  
### <a name="avenues-to-compromise"></a>손상될 작업 환경  
이 섹션에서는 고객의 인프라를 손상 시키는 공격자가 사용할 수 있는 취약점으로 인 한 일반적으로 활용 하는 몇 가지에 대 한 정보를 제공 합니다. 이 섹션에서는 처음에 고객의 인프라를 침투, 추가 시스템 손상 전파 및 결국 전체 가져오려면 AD DS와 도메인 컨트롤러를 대상를 활용 하는 방법 및 취약점으로 인 한 일반 범주를 사용 하 여 시작 조직 포리스트 컨트롤입니다.  
  
이 섹션에서는 각 유형의는 취약성 Active Directory를 직접 대상에 사용 되지 않는 영역에서 특히 취약점을 해결 하는 방법에 대 한 자세한 권장 사항을 제공 하지 않습니다. 그러나 각 유형의 취약점으로 인 한 조직의 공격 노출 영역을 줄이고 대책을 개발 하는 데 사용할 수 있는 추가 정보 링크를 제공 했습니다.  
  
### <a name="reducing-the-active-directory-attack-surface"></a>Active Directory 공격에 대한 취약성 줄이기  
이 섹션에서는 권한 있는 계정 및 보안 설정 및 관리 권한 있는 그룹에 대 한 후속 권장 사항에 대 한 이유 분명히는 정보를 제공 하는 Active Directory에서 그룹에 대 한 배경 정보를 제공 하 여 시작 하 고 계정입니다. 매우 강력한 권한의 계정을 사용 하 여 Enterprise Admins (EA)와 도메인 관리자 (DA) 기본 제공 그룹에 부여 되는 권한 수준이 필요 하지 않은 일상적인 관리에 대 한 필요를 줄여 방법 설명 Active Directory에서 관리자 (BA) 그룹입니다. 다음으로 권한 있는 그룹 및 계정 보호 및 보안 관리 방식 및 시스템을 구현 하기 위한 지침을 제공 했습니다.  
  
이 섹션에서는 이러한 구성 설정에 대 한 자세한 정보를 제공 하지만 사용 되는 "는" 일 수 있습니다 하거나 수정할 수 있습니다 하는 단계별 구성 지침을 제공 하는 각 권장 사항에 대 한 부록도 포함 되어 있습니다를 조직의 요구 사항입니다. 이 섹션에서는 안전 하 게 배포 하 고 인프라에서 가장 엄격 하 게 보안된 시스템 간에 해야 하는 도메인 컨트롤러를 관리 하는 정보를 제공 하 여 완료 합니다.  
  
### <a name="monitoring-active-directory-for-signs-of-compromise"></a>손상 징후에 대한 Active Directory 모니터링  
이 섹션에서는 Windows에서 이벤트를 식별 하는 설명에서는 강력한 보안 정보 및 이벤트 (SIEM) 환경에서 모니터링 구현 또는 다른 메커니즘을 사용 하 여 인프라의 보안을 모니터링 하는 조직은 공격을 나타낼 수 있는 시스템. 기존 및 고급 감사 정책, Windows 7 및 Windows Vista 운영 체제에서 얼마나 효과적으로 구성 감사 하위 범주를 포함 하 여 설명 합니다. 이 섹션에서는 개체 및를 감사 하려면 시스템의 포괄적인 목록을 포함 하 고 관련된 부록은 목적은 손상 시도 감지 하는 경우를 모니터링 해야 하는 이벤트를 나열 합니다.  
  
### <a name="planning-for-compromise"></a>손상 계획  
이 섹션에서는 단계별"뒤로" 원칙 및 프로세스 사용자, 응용 프로그램 및 IT 인프라에 뿐만 아니라 가장 중요 한 시스템을 식별 하도록 구현할 수 있습니다를 중점적으로 기술 세부 정보에서 시작 하지만 비즈니스입니다. 안정성 및 조직 업무에 가장 중요 한를 식별 한 후이 든 상관 없이 지적 재산권, 사람 또는 시스템을 분리 하 여 이러한 자산을 보호에 집중할 수 있습니다. 경우에 따라 분리 및 자산 보안 유지 수행 될 수 있습니다, 기존 AD DS 환경의 다른 경우에서 구현을 고려해 작은, 별도 "셀" 중요 한 자산 주위에 보안 경계를 설정 하 고 해당 모니터링 할 수 있도록 자산 덜 중요 한 구성 요소 보다 더 엄격 하 게 합니다. 레거시 응용 프로그램 및 시스템을 제거할 수 있습니다 새 솔루션을 만들어는 메커니즘인 "creative 소멸" 이라는 개념에 대해 끝나며 섹션에서 더 안전한 환경 유지 관리 하는 데 도움이 되는 권장 사항 비즈니스 및 IT 정상적인 작동 상태는 새로운 자세한 그림을 생성 하는 정보를 결합 합니다. 조직에 대 한 정상를 알고 있으면 공격 및 손상을 나타낼 수 있는 비정상적인 상태 보다 쉽게 식별할 수 있습니다.  
  
### <a name="summary-of-best-practice-recommendations"></a>모범 사례 권장 사항이 요약  
이 섹션에서는이 문서의 권장 사항을 요약 하는 테이블을 제공 하 고 각 권장 사항에 대 한 자세한 문서 및 해당 부록에서 찾을 수 있는 링크를 제공 하는 것 외에도 상대적 우선 순위를 기준으로 정렬 합니다.  
  
### <a name="appendices"></a>부록  
문서 본문에 포함 된 정보를 보강 하는이 문서의 부록 포함 됩니다. 각 대 한 간략 한 설명과 부록 목록이 포함 되어 다음 표에서 합니다.  
  
 
|**부록**|**설명**|
| --- | --- | 
|[부록 b: 권한 있는 계정 및 Active Directory의 그룹](../../../ad-ds/plan/security-best-practices/Appendix-B--Privileged-Accounts-and-Groups-in-Active-Directory.md)|사용자 및 보안을 손상 하 고 Active Directory 설치를 파괴도 공격자가 활용할 수 있으므로 때문에 중점을 두어야 하는 그룹을 식별 하는 데 도움이 되는 배경 정보를 제공 합니다.|  
|[부록 c: 보호 된 계정 및 Active Directory의 그룹](../../../ad-ds/plan/security-best-practices/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory.md)|Active Directory의 보호 된 그룹에 대 한 정보를 포함합니다. 또한 보호 되는 그룹 라고 하며 AdminSDHolder 및 SDProp 영향을 받지는 그룹의 제한 된 사용자 지정 (제거)에 대 한 정보를 포함 합니다.|  
|[부록 d: Active Directory에서 기본 제공 관리자 계정 보안](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md)|포리스트의 각 도메인의 관리자 계정을 보호 하기 위한 지침을 포함 합니다.|  
|[부록 e: Active Directory의 Enterprise Admins 그룹 보안](../../../ad-ds/plan/security-best-practices/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory.md)|포리스트의 Enterprise Admins 그룹 보안을 유지 하기 위한 지침을 포함 합니다.|  
|[부록 f: Active Directory에서 Domain Admins 그룹 보안](../../../ad-ds/plan/security-best-practices/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory.md)|포리스트의 각 도메인의 Domain Admins 그룹 보안을 유지 하기 위한 지침을 포함 합니다.|  
|[부록 g: Active Directory에서 관리자 그룹의 보안 설정](../../../ad-ds/plan/security-best-practices/Appendix-G--Securing-Administrators-Groups-in-Active-Directory.md)|포리스트의 각 도메인에 기본 제공 Administrators 그룹을 보호 하기 위한 지침을 포함 합니다.|  
|[부록 h: 로컬 관리자 계정 및 그룹 보안](../../../ad-ds/plan/security-best-practices/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups.md)|보안 로컬 관리자 계정 및 도메인에 가입 된 서버 및 워크스테이션에서 관리자 그룹을 하기 위한 지침을 포함 합니다.|  
|[부록 i: 보호 된 계정 및 Active Directory에서 그룹에 대 한 계정 관리](../../../ad-ds/manage/component-updates/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory.md)|권한을 제한 및 엄격 하 게 제어할 수 있지만 임시 권한 상승이 필요한 경우 Active Directory에서 권한 있는 그룹을 채우는 데 사용할 수 있는 계정을 만드는 정보를 제공 합니다.|  
|[부록 l: 모니터링할 이벤트](../../../ad-ds/plan/Appendix-L--Events-to-Monitor.md)|사용자 환경에서 모니터링 해야 하는 대 한 이벤트를 나열 합니다.|  
|[부록 m: 문서 링크 및 읽어보면 좋은 자료](../../../ad-ds/manage/Appendix-M--Document-Links-and-Recommended-Reading.md)|읽어보면 좋은 자료의 목록을 포함합니다. 외부 문서에 대 한 링크 목록 및 해당 Url 하드 카피를이 문서의 독자가이 정보에 액세스할 수 있도록도 포함 합니다.|  
  


