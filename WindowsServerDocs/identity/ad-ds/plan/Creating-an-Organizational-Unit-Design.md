---
ms.assetid: b8df1828-5ead-4c90-b0fe-95c675116b7c
title: 조직 구성 단위 디자인 만들기
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 718cb4ed8efebbd92f13db67cc4b8f86ac9feb56
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80822736"
---
# <a name="creating-an-organizational-unit-design"></a>조직 구성 단위 디자인 만들기

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

포리스트 소유자는 도메인에 대 한 OU (조직 구성 단위) 디자인을 만듭니다. Ou 디자인을 만들려면 ou 구조를 디자인 하 고 OU 소유자 역할을 할당 하 고 계정 및 리소스 Ou를 만들어야 합니다.  
  
처음에는 관리를 위임할 수 있도록 OU 구조를 디자인 합니다. OU 디자인이 완료 되 면 사용자 및 컴퓨터에 대 한 그룹 정책의 응용 프로그램에 대 한 추가 OU 구조를 만들고 개체의 표시 여부를 제한할 수 있습니다. 자세한 내용은 그룹 정책 인프라 디자인 ([https://go.microsoft.com/fwlink/?LinkId=106655](https://go.microsoft.com/fwlink/?LinkId=106655))을 참조 하세요.  
  
## <a name="ou-owner-role"></a>OU 소유자 역할  
포리스트 소유자는 도메인에 대해 디자인 하는 각 OU의 OU 소유자를 지정 합니다. OU 소유자는 Active Directory Domain Services (AD DS)에서 개체의 하위 트리를 제어 하는 데이터 관리자입니다. OU 소유자는 관리를 위임 하는 방법과 정책을 OU 내의 개체에 적용 하는 방법을 제어할 수 있습니다. 또한 새 하위 트리를 만들고 Ou의 관리를 위임할 수 있습니다.  
  
OU 소유자는 디렉터리 서비스의 작업을 소유 하거나 제어 하지 않으므로 디렉터리 서비스의 소유권 및 관리를 개체의 소유권 및 관리에서 분리 하 여 높은 수준의 액세스 권한이 있는 서비스 관리자 수를 줄일 수 있습니다.  
  
Ou는 디렉터리에서 개체의 표시 여부를 제어 하는 관리 자율성 및 수단을 제공 합니다. Ou는 다른 데이터 관리자와의 격리를 제공 하지만 서비스 관리자와의 격리는 제공 하지 않습니다. OU 소유자는 개체의 하위 트리를 제어할 수 있지만 포리스트 소유자는 모든 하위 트리에 대 한 모든 권한을 보유 합니다. 이를 통해 포리스트 소유자는 ACL (액세스 제어 목록)의 오류와 같은 실수를 수정 하 고 데이터 관리자가 종료 될 때 위임 된 하위 트리를 회수할 수 있습니다.  
  
## <a name="account-ous-and-resource-ous"></a>계정 Ou 및 리소스 Ou  
계정 Ou에는 사용자, 그룹 및 컴퓨터 개체가 포함 됩니다. 포리스트 소유자는 이러한 개체를 관리 하는 OU 구조를 만든 다음이 구조에 대 한 제어를 OU 소유자에 게 위임 해야 합니다. 새 AD DS 도메인을 배포 하는 경우 도메인의 계정에 대 한 제어를 위임할 수 있도록 도메인의 계정 OU를 만듭니다.  
  
리소스 Ou 리소스 및 해당 리소스를 관리 하는 일을 담당 하는 계정을 포함 합니다. 또한 포리스트 소유자는 이러한 리소스를 관리 하 고 해당 구조의 제어를 OU 소유자에 게 위임 하는 OU 구조를 만듭니다. 조직 내의 각 그룹에 대 한 요구 사항에 따라 필요한 만큼 리소스 Ou를 만들어 데이터 및 장비 관리의 자율성을 확인 합니다.  
  
## <a name="documenting-the-ou-design-for-each-domain"></a>각 도메인에 대 한 OU 디자인 문서화  
팀을 조합 하 여 포리스트 내의 리소스에 대 한 제어를 위임 하는 데 사용 하는 OU 구조를 설계 합니다. 포리스트 소유자는 디자인 프로세스에 포함 될 수 있으며 OU 디자인을 승인 해야 합니다. 설계가 올바른지 확인 하기 위해 서비스 관리자가 하나 이상 포함 될 수도 있습니다. 다른 디자인 팀 참가자에 게는 Ou를 담당 하는 데이터 관리자와 해당 Ou를 관리할 OU 소유자가 포함 될 수 있습니다.  
  
OU 디자인을 문서화 하는 것이 중요 합니다. 만들려는 Ou의 이름을 나열 합니다. 그리고 각 OU에 대해 OU의 유형, OU 소유자, 부모 OU (해당 하는 경우) 및 해당 OU의 원본을 문서화 합니다.  
  
OU 디자인을 문서화 하는 데 도움이 되는 워크시트의 경우 Windows Server 2003 배포 키트 ([https://go.microsoft.com/fwlink/?LinkID=102558](https://go.microsoft.com/fwlink/?LinkID=102558))의 작업 지원에서 Job_Aids_Designing_and_Deploying_Directory_and_Security_Services .zip을 다운로드 하 고 "각 도메인에 대 한 ou 식별" (DSSLOGI_9 .doc)을 엽니다.  
  
## <a name="in-this-section"></a>단원 내용  
  
-   [OU 디자인 개념 검토](../../ad-ds/plan/Reviewing-OU-Design-Concepts.md)  
  
-   [OU 개체를 사용하여 관리 위임](../../ad-ds/plan/Delegating-Administration-by-Using-OU-Objects.md)  
  


