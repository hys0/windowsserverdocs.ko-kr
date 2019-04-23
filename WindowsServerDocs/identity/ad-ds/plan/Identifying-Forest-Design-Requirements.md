---
ms.assetid: 7d957ebb-3476-49d8-b00b-6e93b4a94778
title: 포리스트 디자인 요구 사항 파악
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/07/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: bf8d9d164bf07151572785cda906be911f97b53e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59835334"
---
# <a name="identifying-forest-design-requirements"></a>포리스트 디자인 요구 사항 파악

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

조직에 대 한 포리스트 디자인을 만들려면 디렉터리 구조를 수용 해야 하는 비즈니스 요구 사항을 식별 해야 합니다. 이 결정 하는 것 얼마나 많은 자율성 조직 요구에 해당 네트워크 리소스 및 다른 그룹에서 네트워크에 해당 리소스를 격리할 필요 여부를 각 그룹을 관리 하에 있는 그룹입니다.  
  
Active Directory Domain Services (AD DS)를 사용 하면 조직 내에서 고유한 관리 요구 사항이 있는 여러 그룹을 수용 하는 디렉터리 인프라를 디자인 하 고 그룹 간에 구조 및 운영 독립성을 달성 하기 위해 반복 합니다.  
  
조직의 그룹에 속한 일부는 다음과 같은 유형의 요구 사항이 있을 수 있습니다.  
  
-   **조직 구조 요구 사항**합니다. 조직의 부분 비용을 절감 조직의 나머지 부분에서 독립적으로 작동할 수 있어야 하는 공유 인프라에 참여할 수 있습니다. 예를 들어, 대규모 조직 내에서 연구 그룹을 모든 연구 데이터를 지속적으로 제어 해야 합니다.  
  
-   **운영 요구 사항**합니다. 조직의 일부인 하나 디렉터리 서비스 구성, 가용성 또는 보안에 고유한 제약 조건을 적용 하거나 unique 제약 조건 디렉터리에 배치 하는 응용 프로그램을 사용할 수 있습니다. 예를 들어, 조직 내에서 각 비즈니스 부서 디렉터리 사용 응용 프로그램 디렉터리 스키마를 수정 하는 다른 비즈니스 단위에서 배포 되지 않은 배포 될 수 있습니다. 디렉터리 스키마에서 포리스트의 모든 도메인 간에 공유 되므로 여러 포리스트 만들기는 이러한 시나리오에 대 한 솔루션입니다. 다른 예제는 다음 조직 및 시나리오를 참조 하십시오.  
  
    -   군사 조직  
  
    -   호스팅 시나리오  
  
    -   사용할 수 있는 내부 및 외부에서 (예: 사용자가 인터넷에서 공개적으로 액세스할 수 있는) 디렉터리를 관리 하는 조직  
  
-   **법적 요구 사항**합니다. 일부 조직에서는 법적 요구 사항이 특정 방식으로 작동 합니다. 예를 들어, 비즈니스 계약에 지정 된 대로 특정 정보에 대 한 액세스를 제한 합니다. 일부 조직에는 격리 된 내부 네트워크에 적용할 보안 요구 사항이 있습니다. 이러한 요구 사항을 충족 하는 오류 계약 및 가능한 경우 법적 조치 손실 될 수 있습니다.  
  
포리스트 디자인 요구 사항을 식별 하는 부분에서는 잠재적인 포리스트 소유자 및 서비스 관리자가 조직의 그룹에서에서 신뢰할 수 있는 정도 확인 하 고 각각에 대 한 자율성 및 격리 요구 사항 식별 조직에서 그룹입니다.  
  
디자인 팀은 AD DS를 사용 하는 조직 내에서 각 그룹에 대 한 서비스 및 데이터 관리에 대 한 격리 및 자율성 요구 사항을 문서화 해야 합니다. 팀의 AD DS 배포에 영향을 줄 수는 제한 된 연결의 모든 영역을 참고 해야 합니다.  
  
디자인 팀은 AD DS를 사용 하는 조직 내에서 각 그룹에 대 한 서비스 및 데이터 관리에 대 한 격리 및 자율성 요구 사항을 문서화 해야 합니다. 팀의 AD DS 배포에 영향을 줄 수는 제한 된 연결의 모든 영역을 참고 해야 합니다. 식별 지역 문서화에 도움을 주는 워크시트에 대 한 다운로드에서 Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip [작업 보조 기능에 대 한 Windows Server 2003 Deployment Kit](https://go.microsoft.com/fwlink/?LinkID=102558) 연 "포리스트 디자인 요구 사항"(DSSLOGI_2.doc).  
  
## <a name="in-this-section"></a>단원 내용  
  
-   [서비스 관리자 권한 범위](../../ad-ds/plan/Service-Administrator-Scope-of-Authority.md)  
  
-   [자율성 및 격리](../../ad-ds/plan/Autonomy-vs.-Isolation.md)  
