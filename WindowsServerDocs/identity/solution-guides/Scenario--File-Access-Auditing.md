---
ms.assetid: 7be1f2cb-02d5-4209-ba79-edf496a88f47
title: 시나리오 파일 액세스 감사
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 37a3b17360112d958b59a7e9c3f64aed5e6f6a5b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406999"
---
# <a name="scenario-file-access-auditing"></a>시나리오: 파일 액세스 감사

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

보안 감사는 회사의 보안을 유지 관리할 수 있는 가장 효율적인 도구 중 하나입니다. 보안 감사의 주요 목표 중 하나는 규정 준수입니다. 예를 들어 Sarbanes Oxley, HIPAA(Health Insurance Portability and Accountability Act), PCI(Payment Card Industry) 등의 업계 표준에서는 기업에서 데이터 보안 및 개인 정보와 관련된 엄격한 규칙 집합을 따르도록 규정하고 있습니다. 보안 감사를 통해 이러한 정책의 유무를 파악하고 해당 표준 준수 여부를 증명할 수 있습니다. 또한 보안 감사를 사용하면 비정상적인 동작을 파악하고, 보안 정책의 결함을 파악 및 완화하며, 법정 분석에 사용할 수 있는 사용자 작업 내역을 만들어 무책임한 행위를 방지할 수 있습니다.  
  
감사 정책 요구 사항은 일반적으로 다음과 같은 수준에서 도출됩니다.  
  
-   **정보 보안.** 파일 액세스 감사 내역은 법정 분석 및 침입 검색에 사용되는 경우가 많습니다. 가치가 높은 정보 액세스에 대해 대상이 지정된 이벤트를 가져옴으로써 조직은 응답 시간 및 조사 정확도를 대폭 개선할 수 있습니다.  
  
-   **조직 구성 정책.** 예를 들어 PCI 표준에 의해 규제를 받는 조직에는 신용 카드 정보 및 PII(개인 식별 정보)를 포함하는 것으로 표시된 모든 파일에 대한 액세스를 모니터링하는 중앙 정책이 있을 수 있습니다.  
  
-   **부서별 정책.** 예를 들어 재무 부서에는 재무 부서에만 권한이 있는 분기별 수익 보고서 등과 같은 특정 금융 문서를 수정할 수 있는 권한이 필요할 수 있으므로 이 부서에서는 이러한 문서를 변경하려는 다른 모든 시도를 모니터링하기를 원할 수 있습니다.  
  
-   **비즈니스 정책.** 예를 들어 회사 경영주는 회사 프로젝트에 속한 데이터를 보려는 모든 무단 시도를 모니터링하기를 원할 수 있습니다.  
  
또한 규정 준수 부서는 사용자, 컴퓨터 및 리소스 특성과 같은 중앙 권한 부여 정책 및 정책 구문에 대한 모든 변경 내용을 모니터링하기를 원할 수 있습니다.  
  
보안 감사에서 가장 중요한 고려 사항 중 하나는 감사 이벤트 수집, 저장 및 분석 비용입니다. 감사 정책의 범위가 너무 넓으면 수집되는 감사 이벤트의 양이 증가하므로 비용도 늘어납니다. 반면 감사 정책의 범위가 너무 좁으면 중요한 이벤트를 놓칠 수 있습니다.  
  
Windows Server 2012와 함께 클레임 및 리소스 속성을 사용 하 여 감사 정책을 작성할 수 있습니다. 이로 인해 보다 구체적인 대상에 맞춰 관리하기 쉬운 감사 정책을 작성할 수 있을 뿐만 아니라 이전에는 수행하기가 어려웠거나 불가능했던 시나리오를 수행할 수 있게 되었습니다. 관리자가 작성할 수 있는 감사 정책 예는 다음과 같습니다.  
  
-   높은 수준의 보안이 허가되지 않은, HBI 문서에 액세스하려는 모든 사람 감사 (예: Audit | Everyone | All-Access | Resource.BusinessImpact=HBI AND User.SecurityClearance!=High)  
  
-   현재 작업 중이지 않은 프로젝트와 관련된 문서에 액세스하려는 모든 공급업체 감사 (예: Audit | Everyone | All-Access | User.EmploymentStatus=Vendor AND User.Project Not_AnyOf Resource.Project)  
  
이와 같은 정책을 사용하면 감사 이벤트의 볼륨을 규정하고 감사 이벤트를 가장 관련성이 높은 데이터나 사용자로 제한할 수 있습니다.  
  
관리자가 감사 정책을 작성 및 적용한 후 고려해야 하는 사항은 수집되는 감사 이벤트에서 의미 있는 정보를 수집하는 것입니다. 식 기반 감사 이벤트를 사용하면 감사 볼륨을 줄일 수 있습니다. 그러나 사용자가 필요한 의미 있는 정보는이 이벤트를 쿼리 및와 같은 질문을 하는 방법을 "액세스 하려는 내 HBI 데이터?" 확인 하려는 중요 한 데이터 액세스 시도? "  
  
 Windows Server 2012 사용자, 컴퓨터 및 리소스 클레임으로 기존 데이터 액세스 이벤트를 개선합니다. 이러한 이벤트는 서버별로 생성됩니다. 조직 전체에서 모든 이벤트를 확인할 수 있도록 하기 위해 Microsoft는 파트너와 협력하여 System Center Operation Manager의 Audit Collection Service 등의 이벤트 수집 및 분석 도구를 제공하고 있습니다.  
  
그림 4는 중앙 감사 정책의 개요를 보여 줍니다.  
  
![솔루션 가이드](media/Scenario--File-Access-Auditing/DynamicAccessControl_RevGuide_4.JPG)  
  
**그림 4** 중앙 감사 환경  
  
보안 감사를 설정하고 사용하는 단계는 일반적으로 다음 단계로 구성됩니다.  
  
1.  모니터링할 정확한 데이터 및 사용자 집합 식별  
  
2.  적합한 감사 정책 만들기 및 적용  
  
3.  감사 이벤트 수집 및 분석  
  
4.  만들어진 정책 관리 및 모니터링  
  
## <a name="in-this-scenario"></a>이 시나리오의 내용  
다음 항목에는 이 시나리오에 대한 추가 지침이 나와 있습니다.  
  
-   [파일 액세스 감사 계획](Plan-for-File-Access-Auditing.md)  
  
-   [중앙 감사 정책을 &#40;사용 하 여 보안 감사 배포 데모 단계&#41;](Deploy-Security-Auditing-with-Central-Audit-Policies--Demonstration-Steps-.md)  
  
## <a name="BKMK_NEW"></a>이 시나리오에 포함 된 역할 및 기능  
다음 표에는 이 시나리오에 포함된 역할 및 기능이 나열되어 있으며, 이러한 역할 및 기능이 시나리오를 지원하는 방법에 대한 설명이 나와 있습니다.  
  
|역할/기능|이 시나리오를 지원하는 방법|  
|-----------------|---------------------------------|  
|Active Directory 도메인 서비스 역할|Windows Server 2012의 AD DS 사용자 클레임 및 장치 클레임, 복합 id, (사용자 + 장치 클레임)를 만드는 새로운 중앙 액세스 정책 (CAP) 모델 및 권한 부여 결정에 파일 분류 정보 사용 수 있도록 하는 클레임 기반 권한 부여 플랫폼을 소개 합니다.|  
|파일 및 저장소 서비스 역할|Windows Server 2012의 파일 서버 관리자 수 확인 파일 또는 폴더에 대 한 사용자에 대 한 유효 사용 권한 및 액세스 문제를 해결 하 고 있는 필요에 따라 액세스 권한을 부여 하는 사용자 인터페이스를 제공 합니다.|  
  


