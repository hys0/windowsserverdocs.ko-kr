---
ms.assetid: 84754c23-f039-4de4-a378-853942e662df
title: 소개
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: ab21cca727342f6dc69ceecfb0c8991b30b0f227
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71389885"
---
# <a name="introduction"></a>소개

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

컴퓨터에 있는 한, 단순 또는 복잡 한 컴퓨팅 인프라에 대 한 공격은 존재 하지 않습니다. 그러나 지난 10년 동안 전세계 모든 규모, 모든 분야에서 기존의 위협 환경을 크게 변경한 방법으로 공격 및 피해를 당하는 기업들이 점점 늘어나고 있습니다. 사이버 전쟁과 사이버 범죄는 유례없는 속도로 증가해 왔습니다. 공격이 activist 위치에 의해 결정 되는 "Hacktivism"는 조직의 비밀 정보를 노출 하 고, 서비스 거부를 만들거나, 인프라를 제거 하는 데 사용할 수 있는 많은 위반에 대 한 동기으로 청구 됩니다. 조직의 지적 재산권 (빼내기 위해 공공)을 목표로 하는 공용 및 개인 기관에 대 한 공격을 목표로 하 게 됩니다.  
  
IT (정보 기술) 인프라를 갖춘 조직이 공격 으로부터 면역 되지 않지만 조직의 컴퓨팅 인프라에 대 한 주요 세그먼트를 보호 하기 위해 적절 한 정책, 프로세스 및 컨트롤을 구현 하는 경우의 공격 에스컬레이션 완전 한 손상에 대 한 침투가 안전할 수 있습니다. 조직 외부에서 발생 하는 공격의 수와 소수 자릿수는 최근 몇 년 동안 eclipsed 된 insider threat가 있기 때문에이 문서에서는 권한이 있는 사용자가 환경을 오용 하지 않고 외부 공격자에 대해 설명 하는 경우가 많습니다. 그럼에도 불구 하 고이 문서에서 제공 하는 원칙과 권장 사항은 외부 공격자와 잘못 또는 악의적인 참가자 로부터 환경을 보호 하는 데 도움이 됩니다.  
  
이 문서에 제공 된 정보 및 권장 사항은 다양 한 소스에서 가져온 것 이며 Active Directory 설치를 손상 으로부터 보호 하기 위해 설계 된 사례에서 파생 됩니다. 공격을 방지할 수 있는 것은 아니지만 Active Directory 공격 노출 영역을 줄이고, 공격자가 디렉터리의 손상을 더욱 어렵게 만드는 컨트롤을 구현할 수 있습니다. 이 문서에서는 손상 된 환경에서 관찰 된 가장 일반적인 취약성 유형과 고객이 Active Directory 설치의 보안을 향상 시키기 위해 수행한 가장 일반적인 권장 사항을 제공 합니다.  
  
## <a name="account-and-group-naming-conventions"></a>계정 및 그룹 명명 규칙  
다음 표에서는 문서 전체에서 참조 되는 그룹 및 계정에 대해이 문서에서 사용 되는 명명 규칙에 대 한 지침을 제공 합니다. 테이블에는 각 계정/그룹의 위치, 이름 및 이러한 계정/그룹이이 문서에서 참조 되는 방식이 포함 되어 있습니다.  
  


|**계정/그룹 위치**|**계정/그룹의 이름**|**이 문서에서 참조 되는 방법**|
| --- | --- | --- |   
|Active Directory-각 도메인|관리자|기본 제공 관리자 계정|  
|Active Directory-각 도메인|Administrators|기본 제공 관리자 (BA) 그룹|  
|Active Directory-각 도메인|Domain Admins|도메인 관리자 (DA) 그룹|  
|Active Directory-포리스트 루트 도메인|Enterprise Admins|EA (Enterprise Admins) 그룹|  
|도메인 컨트롤러가 아닌 Windows Server 및 워크스테이션을 실행 하는 컴퓨터의 로컬 컴퓨터 보안 계정 관리자 (SAM) 데이터베이스|관리자|로컬 관리자 계정|  
|도메인 컨트롤러가 아닌 Windows Server 및 워크스테이션을 실행 하는 컴퓨터의 로컬 컴퓨터 보안 계정 관리자 (SAM) 데이터베이스|Administrators|로컬 관리자 그룹|  
  
## <a name="about-this-document"></a>이 문서 정보  
Microsoft 정보 기술 (MSIT)의 일부인 Microsoft 정보 보안 및 위험 관리 (ISRM) 조직은 내부 사업부, 외부 고객 및 업계 동료와 협력 하 여 정책을 수집, 배포 및 정의 합니다. 사례 및 컨트롤입니다. Microsoft와 고객은이 정보를 사용 하 여 보안을 강화 하 고 IT 인프라의 공격 노출 영역을 줄일 수 있습니다. 이 문서에서 제공 하는 권장 사항은 MSIT 및 ISRM 내에서 사용 되는 다양 한 정보 소스 및 사례를 기반으로 합니다. 다음 섹션에서는이 문서의 원본에 대 한 자세한 정보를 제공 합니다.  
  
### <a name="microsoft-it-and-isrm"></a>Microsoft IT 및 ISRM  
Microsoft AD DS 포리스트와 도메인에 보안을 설정 하기 위해 MSIT 및 ISRM 내에서 다양 한 사례 및 컨트롤이 개발 되었습니다. 이러한 컨트롤이 광범위 하 게 적용 되는 경우이 문서에 통합 되었습니다. SAFE-T (새로운 기술용 솔루션 가속기)는 새로운 기술을 식별 하 고 보안 요구 사항 및 컨트롤을 정의 하 여 채택을 가속화 하는 ISRM 내의 팀입니다.  
  
### <a name="active-directory-security-assessments"></a>Active Directory 보안 평가  
Microsoft ISRM 내에서 평가, 컨설팅 및 엔지니어링 (ACE) 팀은 내부 Microsoft 비즈니스 단위 및 외부 고객과 협력 하 여 응용 프로그램 및 인프라 보안을 평가 하 고 조직의 보안 상태. 하나의 ACE 서비스 제품은 ADSA (Active Directory 보안 평가) 이며,이는 사람, 프로세스 및 기술을 평가 하 고 고객 관련 권장 사항을 생성 하는 조직의 AD DS 환경을 전체적으로 평가한 것입니다. 고객은 조직의 고유한 특성, 관행 및 위험 성향 지을 기반으로 하는 권장 사항을 제공 합니다. Microsoft의 고객 외에도 Active Directory 설치를 위해 ADSAs가 수행 되었습니다. 시간이 지남에 따라 다양 한 크기와 산업의 고객에 게 적용할 수 있는 다양 한 권장 사항이 있습니다.  
  
### <a name="content-origin-and-organization"></a>내용 출처 및 구성  
이 문서의 내용 대부분은 손상 된 고객에 대해 수행 된 ADSA 및 기타 ACE 팀 평가와 심각한 손상을 경험 하지 않은 고객에 게 서 파생 됩니다. 개별 고객 데이터는이 문서를 만드는 데 사용 되지 않았지만 평가에서 확인 한 가장 일반적으로 악용 된 취약성 및 고객 AD DS의 보안을 개선 하기 위해 고객에 게 적용 한 권장 사항을 수집 했습니다. 사전. 모든 취약성이 모든 환경에 적용되는 것은 아니며 마찬가지로 모든 권장 사항이 모든 조직에서 구현하기에 적합한 것은 아닙니다.  
  
이 문서는 다음과 같이 구성 됩니다.  
  
## <a name="executive-summary"></a>요약  
독립형 문서로 읽거나 전체 문서와 함께 읽을 수 있는 임원 요약은이 문서에 대 한 개략적인 요약을 제공 합니다. 임원 요약에는 고객 환경을 손상 시키는 데 사용 되는 가장 일반적인 공격 벡터, Active Directory 설치 보안을 위한 요약 권장 사항 및 새 AD DS를 배포 하려는 고객을 위한 기본 목표가 포함 되어 있습니다. 지금 또는 나중에 포리스트를 실행 합니다.  
  
### <a name="introduction"></a>소개  
지금 읽고 있는 섹션입니다.  
  
### <a name="avenues-to-compromise"></a>손상될 작업 환경  
이 섹션에서는 공격자가 고객의 인프라를 손상 시키는 데 사용할 수 있는 가장 일반적으로 활용 되는 취약성에 대 한 정보를 제공 합니다. 이 섹션에서는 일반적인 취약성 범주와이를 활용 하 여 처음에 고객의 인프라를 관통 하 고, 추가 시스템 간에 손상을 전파 하 고, 궁극적으로 AD DS 및 도메인 컨트롤러를 대상으로 하 여 완전 하 게 유지 합니다. 조직의 포리스트를 제어 합니다.  
  
이 섹션에서는 특히 취약점을 사용 하 여 Active Directory를 직접 대상으로 지정 하는 영역에서 각 취약점 유형 해결에 대 한 자세한 권장 사항을 제공 하지 않습니다. 그러나 각 취약점 유형에 대해 대책을 개발 하 고 조직의 공격 노출 영역을 줄이는 데 사용할 수 있는 추가 정보에 대 한 링크를 제공 합니다.  
  
### <a name="reducing-the-active-directory-attack-surface"></a>Active Directory 공격에 대한 취약성 줄이기  
이 섹션에서는 권한 있는 그룹을 보호 하 고 관리 하기 위한 후속 권장 사항을 설명 하는 이유를 설명 하는 데 도움이 되는 정보를 제공 하기 위해 Active Directory 권한 있는 계정 및 그룹에 대 한 배경 정보를 제공 계좌. 그런 다음 일상적인 관리에 대해 매우 권한 있는 계정을 사용 해야 하는 필요성을 줄이는 방법에 대해 설명 합니다 .이 경우 EA (Enterprise Admins), DA (Domain Admins) 및 기본 제공 되는 그룹에 부여 되는 권한 수준이 필요 하지 않습니다. Active Directory의 관리자 (BA) 그룹. 다음으로, 권한 있는 그룹 및 계정을 보호 하 고 보안 관리 방법 및 시스템을 구현 하기 위한 지침을 제공 합니다.  
  
이 섹션에서는 이러한 구성 설정에 대 한 자세한 정보를 제공 하지만, "있는 그대로" 사용 하거나 수정할 수 있는 단계별 구성 지침을 제공 하는 각 권장 사항에 대 한 부록도 포함 했습니다. 조직의 요구 사항 이 섹션에서는 인프라에서 가장 보안이 엄격 보안 시스템 사이에 있어야 하는 도메인 컨트롤러를 안전 하 게 배포 하 고 관리 하기 위한 정보를 제공 합니다.  
  
### <a name="monitoring-active-directory-for-signs-of-compromise"></a>손상 징후에 대한 Active Directory 모니터링  
사용자 환경에서 강력한 SIEM (보안 정보 및 이벤트 모니터링)을 구현 하거나 인프라의 보안을 모니터링 하는 다른 메커니즘을 사용 하 고 있는지 여부에 관계 없이이 섹션에서는 Windows에서 이벤트를 식별 하는 데 사용할 수 있는 정보를 제공 합니다. 조직이 공격 받고 있음을 나타낼 수 있는 시스템입니다. Windows 7 및 Windows Vista 운영 체제에서 감사 하위 범주의 효과적인 구성을 비롯 하 여 기존 및 고급 감사 정책에 대해 설명 합니다. 이 섹션에는 감사할 개체 및 시스템의 포괄적인 목록이 포함 되어 있으며, 관련 부록에는 손상이 손상 된 시도를 감지 하는 경우 모니터링 해야 하는 이벤트가 나열 되어 있습니다.  
  
### <a name="planning-for-compromise"></a>손상 계획  
이 섹션은 기술 세부 정보에서 "다시 실행" 하 여 시작 하 고, IT 인프라 뿐만 아니라 비즈니스에 가장 중요 한 사용자, 응용 프로그램 및 시스템을 식별 하기 위해 구현할 수 있는 원칙 및 프로세스를 중심으로 합니다. 조직의 안정성 및 운영에 가장 중요 한 것을 확인 한 후에는 지적 재산, 사람 또는 시스템 인지 여부에 관계 없이 이러한 자산을 분리 하 고 보호 하는 데 집중할 수 있습니다. 경우에 따라 기존 AD DS 환경에서 자산을 분리 하 고 보안을 설정 하는 것이 가능 하지만, 중요 한 자산에 대 한 보안 경계를 설정 하 고 모니터링 하는 데 사용할 수 있는 작은 개별 "셀"을 구현 하는 것이 좋습니다. 자산이 중요 한 구성 요소 보다 더 보안이 엄격. 새 솔루션을 만들어 레거시 응용 프로그램 및 시스템을 제거 하는 데 사용 되는 메커니즘인 "creative 소멸" 이라는 개념을 설명 하 고 섹션은 다음을 통해 보다 안전한 환경을 유지 관리 하는 데 도움이 되는 권장 사항으로 끝납니다. 비즈니스 및 IT 정보를 결합 하 여 정상 작동 상태에 대 한 자세한 그림을 생성 합니다. 조직의 표준에 대해 알고 비정상적인 상태 공격 및 손상을 보다 쉽게 식별할 수 있음을 나타낼 수 있습니다.  
  
### <a name="summary-of-best-practice-recommendations"></a>모범 사례 권장 사항 요약  
이 섹션에서는이 문서에서 만든 권장 사항을 요약 하 고, 각 권장 사항에 대 한 자세한 정보를 문서와 부록에서 확인할 수 있는 링크를 제공 하는 것 외에도이 문서에 설명 된 권장 사항을 요약 하는 표를 제공 합니다.  
  
### <a name="appendices"></a>부록  
부록은 문서 본문에 포함 된 정보를 보강 하기 위해이 문서에 포함 되어 있습니다. 부록 목록과 각각에 대 한 간략 한 설명이 다음 표에 나와 있습니다.  
  
 
|**부록**|**설명**|
| --- | --- | 
|[부록 B: Active Directory의 권한 있는 계정 및 그룹](../../../ad-ds/plan/security-best-practices/Appendix-B--Privileged-Accounts-and-Groups-in-Active-Directory.md)|공격자가 Active Directory 설치를 손상 하 고 제거 하는 데 활용할 수 있으므로 보안에 집중할 수 있는 사용자 및 그룹을 식별 하는 데 도움이 되는 배경 정보를 제공 합니다.|  
|[부록 C: Active Directory의 보호된 계정 및 그룹](../../../ad-ds/plan/security-best-practices/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory.md)|Active Directory의 보호 된 그룹에 대 한 정보를 포함 합니다. 또한 보호 된 그룹으로 간주 되며 AdminSDHolder 및 SDProp의 영향을 받는 그룹의 제한 된 사용자 지정 (제거)에 대 한 정보도 포함 되어 있습니다.|  
|[부록 D: Active Directory의 기본 제공 관리자 계정 보안](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md)|포리스트의 각 도메인에서 관리자 계정을 보호 하는 데 도움이 되는 지침을 포함 합니다.|  
|[부록 E: Active Directory의 Enterprise Admins 그룹 보안](../../../ad-ds/plan/security-best-practices/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory.md)|포리스트의 Enterprise Admins 그룹을 보호 하는 데 도움이 되는 지침을 포함 합니다.|  
|[부록 F: Active Directory의 Domain Admins 그룹 보안](../../../ad-ds/plan/security-best-practices/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory.md)|포리스트의 각 도메인에서 Domain Admins 그룹의 보안을 유지 하는 데 도움이 되는 지침을 포함 합니다.|  
|[부록 G: Active Directory에서 관리자 그룹의 보안 설정](../../../ad-ds/plan/security-best-practices/Appendix-G--Securing-Administrators-Groups-in-Active-Directory.md)|포리스트의 각 도메인에서 기본 제공 관리자 그룹의 보안을 유지 하는 데 도움이 되는 지침을 제공 합니다.|  
|[부록 H: 로컬 관리자 계정 및 그룹 보안](../../../ad-ds/plan/security-best-practices/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups.md)|도메인에 가입 된 서버 및 워크스테이션에서 로컬 관리자 계정 및 관리자 그룹을 보호 하는 데 도움이 되는 지침을 포함 합니다.|  
|[부록 I: Active Directory의 보호된 계정 및 그룹에 대한 관리 계정 만들기](../../../ad-ds/manage/component-updates/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory.md)|제한 된 권한을 가진 계정을 만드는 데 사용할 수 있는 정보를 제공 하 고, 보안이 엄격 제어 될 수 있지만, 임시 권한 상승이 필요한 경우 Active Directory에서 권한 있는 그룹을 채우는 데 사용할 수 있습니다.|  
|[부록 L: 모니터링할 이벤트](../../../ad-ds/plan/Appendix-L--Events-to-Monitor.md)|사용자 환경에서 모니터링 해야 하는 이벤트를 나열 합니다.|  
|[부록 M: 문서 링크 및 권장 자료](../../../ad-ds/manage/Appendix-M--Document-Links-and-Recommended-Reading.md)|권장 되는 읽기 목록을 포함 합니다. 또한이 문서의 하드 카피 판독기에서이 정보에 액세스할 수 있도록 외부 문서와 해당 Url에 대 한 링크 목록이 포함 되어 있습니다.|  
  


