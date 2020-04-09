---
ms.assetid: 7d957ebb-3476-49d8-b00b-6e93b4a94778
title: 포리스트 디자인 요구 사항 파악
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/07/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 33025dc2e08185744ffd0dee7eac4d0c020a0691
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80822406"
---
# <a name="identifying-forest-design-requirements"></a>포리스트 디자인 요구 사항 파악

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

조직에 대 한 포리스트 디자인을 만들려면 디렉터리 구조에서 충족 해야 하는 비즈니스 요구 사항을 파악 해야 합니다. 여기에는 조직의 그룹에서 네트워크 리소스를 관리 하는 데 필요한 자율성을 결정 하 고, 각 그룹이 다른 그룹의 네트워크에서 리소스를 격리 해야 하는지 여부를 결정 하는 작업이 포함 됩니다.  
  
Active Directory Domain Services (AD DS)를 사용 하면 고유한 관리 요구 사항을 갖는 조직 내의 여러 그룹을 수용 하는 디렉터리 인프라를 디자인 하 고 필요에 따라 그룹 간에 구조적 및 운영 독립성을 달성할 수 있습니다.  
  
조직의 그룹에는 다음과 같은 유형의 요구 사항이 있을 수 있습니다.  
  
-   **조직 구조 요구 사항**. 조직의 일부는 비용 절감을 위해 공유 인프라에 참여할 수 있지만 조직의 나머지 부분과 독립적으로 작동 하는 기능이 필요 합니다. 예를 들어 대기업 내의 연구 그룹은 모든 자체 연구 데이터에 대 한 제어를 유지 해야 할 수 있습니다.  
  
-   **운영 요구 사항**. 조직의 한 부분은 디렉터리 서비스 구성, 가용성 또는 보안에 대 한 unique 제약 조건을 설정 하거나 디렉터리에 unique 제약 조건을 적용 하는 응용 프로그램을 사용할 수 있습니다. 예를 들어 조직 내의 개별 비즈니스 단위는 다른 사업부에서 배포 되지 않은 디렉터리 스키마를 수정 하는 디렉터리 사용 응용 프로그램을 배포할 수 있습니다. 디렉터리 스키마는 포리스트의 모든 도메인 간에 공유 되므로 여러 포리스트를 만드는 것은 이러한 시나리오에 적합 한 솔루션입니다. 다른 예제는 다음 조직 및 시나리오에 있습니다.  
  
    -   군사 조직  
  
    -   호스팅 시나리오  
  
    -   내부적 및 외부적으로 모두 사용할 수 있는 디렉터리를 유지 관리 하는 조직 (예: 인터넷 사용자가 공개적으로 액세스할 수 있는 디렉터리)  
  
-   **법적 요구 사항**. 일부 조직에는 특정 방식으로 작동 하기 위한 법적 요구 사항이 있습니다. 예를 들어 비즈니스 계약에 지정 된 특정 정보에 대 한 액세스를 제한할 수 있습니다. 일부 조직에는 격리 된 내부 네트워크에서 작동 하는 보안 요구 사항이 있습니다. 이러한 요구 사항을 충족 하지 못하면 계약과 법적 조치를 손실할 수 있습니다.  
  
포리스트 설계 요구 사항을 식별 하는 과정에는 조직의 그룹이 잠재적 포리스트 소유자 및 해당 서비스 관리자를 신뢰 하 고 조직의 각 그룹에 대 한 자율성 및 격리 요구 사항을 식별할 수 있는 정도를 식별 하는 작업이 포함 됩니다.  
  
디자인 팀은 AD DS를 사용 하려는 조직의 각 그룹에 대 한 서비스 및 데이터 관리에 대 한 격리 및 자율성 요구 사항을 문서화 해야 합니다. 또한 팀은 AD DS 배포에 영향을 줄 수 있는 제한 된 연결 영역을 기록해 야 합니다.  
  
디자인 팀은 AD DS를 사용 하려는 조직의 각 그룹에 대 한 서비스 및 데이터 관리에 대 한 격리 및 자율성 요구 사항을 문서화 해야 합니다. 또한 팀은 AD DS 배포에 영향을 줄 수 있는 제한 된 연결 영역을 기록해 야 합니다. 찾은 지역을 문서화 하는 데 도움이 되는 워크시트의 경우 [Windows Server 2003 배포 키트의 작업 지원](https://go.microsoft.com/fwlink/?LinkID=102558) 에서 Job_Aids_Designing_and_Deploying_Directory_and_Security_Services .zip을 다운로드 하 고 "포리스트 디자인 요구 사항" (DSSLOGI_2)을 엽니다.  
  
## <a name="in-this-section"></a>단원 내용  
  
-   [서비스 관리자 권한 범위](../../ad-ds/plan/Service-Administrator-Scope-of-Authority.md)  
  
-   [자율성 및 격리](../../ad-ds/plan/Autonomy-vs.-Isolation.md)  
