---
ms.assetid: 84754c23-f039-4de4-a378-853942e662df
title: "소개"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: dc89afc47eb78a388238e8edf5059b0bec3006ad
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="introduction"></a>소개

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

으로 컴퓨터에는 컴퓨팅 인프라를 간단한 또는 복잡 공격이 오래전부터 합니다. 그러나 내에서 지난 10 전 세계의 모든 부분에 있는 모든 규모의 수가 증가 공격 되어 위협 환경 크게 변경 하는 방법에 손상 합니다. 기록 속도로 사이버 전쟁과 사이버 증가 했습니다. 서비스 거부 만드는 조직의 비밀 정보를 제공 하기 위한 다양 한 위반에 대 한 변경한 이유가 무엇 인지도 주장 또는 삭제 인프라에도 "Hacktivism," activist positions 하 여 공격이 동기은 부여 했습니다. Exfiltrating 공개 하 게 비밀로 기관에 대 한 공격 조직의 지식 (IP) 되 고 어디에서 나 있습니다.  
  
정보 it 인프라와 없음 조직 공격에 영향을 받지 이지만 적절 한 정책을, 프로세스를 및 컨트롤 구현 핵심 부분의 조직 컴퓨팅 인프라를 보호 하기 위해의 전체 손상에 침투 공격이 에스컬레이션 예방 수 있습니다. 번호와 규모의 공격 조직 외부에서 발생 한 최근 몇 년 동안에서 참가자 위협 은폐가, 하기 때문에이 문서의 권한이 있는 사용자 환경의 오용 보다는 외장 공격자 자주 설명 합니다. 그러나 원칙 및이 문서에 제공 되는 권장은 귀하의 환경 외부 공격자 및 실수로 또는 악성 참가자 로부터 보호 하는 것입니다.  
  
정보와 권장 사항을이 여기서 제공 다양 한 소스에서에서 가져온 및 Active Directory를 설치 하려면 손상 으로부터 보호 하기 위한 관행에서 파생 되었습니다. Active Directory 하든지 하 고 확인 하는 컨트롤을 구현 하는 공격을 방지 하려면 수는 없지만 어려운 훨씬 더 디렉터리의 공격자가 손상 될 합니다. 이 문서에 관찰된 손상 된 환경 및 Active Directory를 설치 하려면 자녀의의 보안을 개선 하기 위해 고객에 게 하였습니다 가장 일반적인 추천 가장 일반적인 유형의의 취약성을 제공 합니다.  
  
## <a name="account-and-group-naming-conventions"></a>계정 하 고 그룹 이름 지정 규칙  
다음 표에서 명명이 문서에 그룹과 전체 문서에서 참조 계정에 대 한 사용 규칙에 대 한 지침을 제공 합니다. 각 계정/그룹, 이름, 이러한 계정을/그룹이이 문서에서 참조 되는 방식을의 위치를 테이블에 포함 되어 있습니다.  
  


|**그룹 계정 위치**|**계정/그룹의 이름**|**이 문서에서 참조 되는 방식**|
| --- | --- | --- |   
|각 도메인 active Directory-|관리자|기본 제공 관리자 계정|  
|각 도메인 active Directory-|관리자|기본 제공 (모음) 관리자가 그룹|  
|각 도메인 active Directory-|도메인 관리|도메인 관리자 (DA) 그룹|  
|이렇게 active Directory-|엔터프라이즈 관리|그룹 Enterprise 관리자 (EA)|  
|로컬 컴퓨터 보안 계정 (삼로) 관리자 데이터베이스 워크스테이션 및 Windows Server을 실행 하는 컴퓨터에서 도메인 컨트롤러 되지 않습니다.|관리자|로컬 관리자 계정|  
|로컬 컴퓨터 보안 계정 (삼로) 관리자 데이터베이스 워크스테이션 및 Windows Server을 실행 하는 컴퓨터에서 도메인 컨트롤러 되지 않습니다.|관리자|로컬 관리자가 그룹|  
  
## <a name="about-this-document"></a>이 문서에 대 한  
Microsoft 보안 정보 및 참가의 Microsoft 정보 기술을 (MSIT), 내부 비즈니스 장치, 외부 고객의 경우 및 수집, 산업 파트너와 작동 하는 위험 관리 (ISRM) 조직, 배포 및 정책, 방법 및 컨트롤 정의 합니다. 이 정보는 하 고 보안 강화 및 IT 인프라의 공격을 줄일 Microsoft와 고객에서 사용할 수 있습니다. 이 문서에 제공 되는 추천 다양 한 소스와 관행 MSIT 및 ISRM 내 사용 기반으로 합니다. 다음 섹션에서는이 문서의 기원에 대 한 자세한 정보를 제공합니다.  
  
### <a name="microsoft-it-and-isrm"></a>Microsoft IT 및 ISRM  
다양 한 관행 및 컨트롤 MSIT 및 ISRM Microsoft AD DS 숲 및 도메인 안전 하 게 내 개발 되었습니다. 이러한 컨트롤이 광범위 하 게 적용 되는 경우 여기서이 문서에 통합 되어 있습니다. 안전 T (신흥 기술에 대 한 해결 방법 바로)는 내 ISRM 소유자 기본 새로운 기술을 식별 하 고 보안 요구 사항 및 컨트롤의 채택 보다 빠르게를 정의 하는 팀이 합니다.  
  
### <a name="active-directory-security-assessments"></a>보안 평가 active Directory  
내 Microsoft 비즈니스 단위 내부 및 외부 고객 응용 프로그램 및 infrastructure 보안 평가 하 고 전략적 및 전략적 지침을 제공 하 조직의 보안 환경을 강화 하기 위해 Microsoft ISRM, 평가, 컨설팅, 및 엔지니어링 에이스가 팀 작동 합니다. ACE 서비스를 제공 하나는 Active Directory 보안 Assessment (ADSA), 피플, 프로세스를 및 기술 평가 하 고 고객 관련 추천을 생성 하는 조직의 AD DS 환경을 전체론적인 assessment는입니다. 추천 회사의 고유한 특징, 방법 및 위험 욕구가 기반으로 하는 고객 제공 됩니다. Microsoft에서 고객의 뿐 아니라 Active Directory 설치 ADSAs 수행한 후 합니다. 시간이 지남에 따라 다양 한 추천 여러 다양 한 크기와 산업 고객 적용 하기 위해 발견 되었습니다.  
  
### <a name="content-origin-and-organization"></a>콘텐츠 출처 및 조직  
대부분의이 문서의 콘텐츠는 ADSA 및 기타 ACE 팀 평가 손상된 고객 및 중요 한 손상 되지 경험한 고객을 위해 수행에서 파생 되었습니다. 하지만이 문서를 만드는 개별 고객 데이터를 사용 하지 않았습니다를 확인 했으며 가장 일반적으로 발생된 하는 문제점 수집 했습니다 우리의 평가 및 추천 하였습니다 고객에 게 자신의 AD DS 설치의 보안을 개선 합니다. 모든 환경에 적용할 수 있는 모든 취약성을 받지 않으며 모든 권장 모든 조직에서를 구현할 수 있습니다.  
  
이 문서는 다음과 같은 구성 되어 있습니다.  
  
## <a name="executive-summary"></a>요약  
고급 간략하게 설명이 문서는 집행 요약, 독립 실행형 문서로 또는 전체 문서와 함께에서 읽을 수를 제공 합니다. 가장 일반적인 공격 손상 고객 환경, 이제 또는 나중에 새로운 AD DS 숲 배포할 계획 하는 고객에 대 한 Active Directory 설치 및 기본 목적을 보호 하기 위한 요약 추천을 제공 하는 데 사용 되는 집행 요약에 포함 됩니다.  
  
### <a name="introduction"></a>소개  
현재 읽고 구역입니다.  
  
### <a name="avenues-to-compromise"></a>손상 수단  
이 섹션 취약성 하는 데 사용할 공격자가 고객의 인프라 손상 발견 했습니다 일반적으로 활용 하는 가장 중 일부에 대 한 정보를 제공 합니다. 이 섹션의 문제와 처음 고객의 인프라를 관통, 추가 시스템 손상 전파 및 결국 AD DS 및 도메인 컨트롤러를 완전히 제어할 조직의 숲 가져오는 대상으로 지정 활용는 어떻게 일반적인 범주도 시작 합니다.  
  
이 섹션 각 유형의의 없는 취약성 직접 Active Directory를 대상으로 사용 되지 않는 문제를 해결 하기 위해에 대 한 자세한 내용은 제공 되지 않습니다. 그러나 각 형식의 취약성에 대 한 추가 정보를 대책을 개발 하 고 공격 조직의 줄이기 위해 사용할 수 있는 링크를 제공 했습니다 했습니다.  
  
### <a name="reducing-the-active-directory-attack-surface"></a>Active Directory 공격 줄이기  
이 섹션 권한이 있는 계정 보안 및 권한이 있는 그룹 및 계정 관리에 대 한 후속 추천을 제공 하는 이유를 설명 하는 데 도움이 되는 정보를 제공 하기 위해 Active Directory에 있는 그룹에 대 한 배경 정보를 제공 하 여 시작 합니다. Enterprise 관리자 (EA), 도메인 관리자 (DA) 및 기본 관리자 (모음) 그룹 Active directory에서 등 그룹으로 허가 된 권한 레벨 필요 하지 않은 일상적인 관리에 대 한 권한이 높은 계정을 사용 하 여 필요 줄이기 하는 방법을 설명 합니다. 다음으로 권한이 있는 그룹 및 계정 보안에 대 한 및 안전 하 게 관리 사례와 시스템이 구현에 대 한 지침을 제공 했습니다.  
  
이 섹션 구성 이러한 설정에 대 한 자세한 정보를 제공 하며, 회사의 요구 사항에 대 한 사용 하는 "" 있는 그대로 될 수 있습니다 하거나 수정할 수 있는 구성 단계별 지침을 제공 하는 각 권장 부록도 포함 되어 있습니다. 이 섹션 정보를 안전 하 게 배포 및 관리할 엄격 가장 보안된 시스템 인프라에 포함 되어 있는 도메인 컨트롤러를 제공 하 여 완료 됩니다.  
  
### <a name="monitoring-active-directory-for-signs-of-compromise"></a>침입 Active Directory를 모니터링합니다.  
강력한 보안 정보 및 모니터링 (SIEM) 귀하의 환경에 이벤트 구현 있거나 인프라의 보안 상태를 모니터링 하 여 다른 메커니즘을 사용 하는 이벤트를 조직 공격을 나타낼 수 있는 Windows 시스템에서 파악 하는 데 사용 될 수 있는 정보를 제공이 합니다. 일반 및 고급 감사 정책, Windows 7 및 Windows Vista 운영 체제에 적용 구성을 감사 하위 범주를 포함 하 여 설명할입니다. 연결 된 부록을 모니터링 하 여 해야 손상 시도 감지 하는 경우 이벤트를 표시 및이 섹션 개체와 감사할 시스템의 전체 목록을 포함 됩니다.  
  
### <a name="planning-for-compromise"></a>손상에 대 한 계획  
이 여기서 기술 세부 정보 원칙 및 사용자가, 응용 프로그램 및 IT 인프라에 뿐만 아니라 가장 중요 한 시스템을 식별 구현할 수 있는 프로세스에 초점을 맞추는에서 "다시 단계별로" 시작 있지만 비즈니스에 있습니다. 안정성과 조직의 운영에 가장 중요 한 항목을 확인 한 후 지적, 피플 또는 시스템은 있는지 여부를 분리 하 고 이러한 자산 보호에 집중할 수 있습니다. 경우에 따라 분리 하 고 보안 하기 주기 자산 수행할 수 기존 AD DS 환경을 사용자의 다른 경우 고려해 야 작은, 별도 "셀" 구현 중요 한 자산 주위 안전한 경계를 설정 하 고 보다 덜 중요 한 구성 요소 엄격 자산 모니터링할 수 있도록 합니다. 섹션 비즈니스 및 IT 정보 정상적인 작동 상태는 자세한 그림을 만드는 데 결합 하 여 더 많은 보안 환경을 유지 하는 데 도움이 되는 추천 여 마무리 하 고는 레거시 응용 프로그램 및 시스템 제거할 수 있습니다 새로운 솔루션 만들어 장치는 "창의적인 소멸" 이라는 개념이 설명 되어 있습니다. 조직에 대 한 정상를 파악 하 여 비정상적인 공격 하 고 손상 나타낼 수 있는 더 쉽게 확인할 수 있습니다.  
  
### <a name="summary-of-best-practice-recommendations"></a>가장 좋은 방법은 요약  
이 섹션을 요약이 문서에서 추천 표를 제공 하 고 각 권장에 대 한 자세한 내용은 해당 부록 문서에서 찾을 수 있는 링크를 제공할 뿐만 아니라 상대 우선 순위 부여 하 여 정렬 합니다.  
  
### <a name="appendices"></a>부록  
부록 정보 본문 문서에 포함 된 추가이 문서에 포함 됩니다. 부록과 각각의 간략 한 설명을 목록이 포함 되어 다음 표에서 합니다.  
  
 
|**부록**|**설명**|
| --- | --- | 
|[부록 b: 권한이 있는 계정 및 그룹 Active Directory에](../../../ad-ds/plan/security-best-practices/Appendix-B--Privileged-Accounts-and-Groups-in-Active-Directory.md)|식별 사용자 및 그룹을 손상 Active Directory 설치도 삭제 공격자에서 사용할 수 있으므로 보안에 초점 해야 하는 데 도움이 되는 배경 정보를 제공 합니다.|  
|[부록 c: 보호 계정과 그룹 Active Directory에](../../../ad-ds/plan/security-best-practices/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory.md)|보호 된 그룹 Active Directory에 대 한 정보를 포함 합니다. 또한 보호 그룹 정보로 간주 되어 있는 AdminSDHolder 및 SDProp 영향을 받는 그룹의 (제거) 사용자를 제한 된 정보가 들어 있습니다.|  
|[부록 d: Active Directory에 기본 제공 관리자 계정 보안](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md)|각 도메인 숲에서 관리자 계정을 보호 하기 위한 지침을 포함 합니다.|  
|[부록 e: Active Directory에 관리자 그룹 엔터프라이즈 보안](../../../ad-ds/plan/security-best-practices/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory.md)|엔터프라이즈 관리자 그룹에서 숲 속의 보안을 유지 하기 위한 지침을 포함 합니다.|  
|[부록 f: 도메인 관리자 그룹 Active Directory에 고정](../../../ad-ds/plan/security-best-practices/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory.md)|각 도메인 숲에서 도메인 관리자 그룹 보안을 유지 하기 위한 지침을 포함 합니다.|  
|[부록 g: 관리자가 그룹 Active Directory에 고정](../../../ad-ds/plan/security-best-practices/Appendix-G--Securing-Administrators-Groups-in-Active-Directory.md)|관리자가 기본 제공 그룹 각 도메인 숲에서 보안을 유지 하기 위한 지침을 포함 합니다.|  
|[로컬 관리자 계정 및 그룹 부록 h: 보안](../../../ad-ds/plan/security-best-practices/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups.md)|되는 지침을 로컬 관리자 계정을 안전 하 고 관리자가 그룹 워크스테이션과 도메인에 가입 서버에 포함 되어 있습니다.|  
|[부록 i: 보호 계정과 Active Directory에 있는 그룹에 대 한 계정을 만들 관리](../../../ad-ds/manage/component-updates/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory.md)|제한 된 권한 및 엄격 제어할 수 있습니다 하지만 임시 상승 필요할 때 권한이 있는 그룹 Active Directory에 채우려면 사용할 수 있는 계정을 만드는 데 필요한 정보를 제공 합니다.|  
|[모니터에 부록 l: 이벤트](../../../ad-ds/plan/Appendix-L--Events-to-Monitor.md)|귀하의 환경에 모니터 해야 하는 대 한 이벤트를 표시 합니다.|  
|[부록 m: 링크 문서 및 권장 읽기](../../../ad-ds/manage/Appendix-M--Document-Links-and-Recommended-Reading.md)|권장된 읽기 목록이 포함 되어 있습니다. 외부 문서 링크는 목록과 사이트의 Url 판독기 하드 카피가 문서의이 정보에 액세스할 수 있도록도 포함 됩니다.|  
  


