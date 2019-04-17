---
ms.assetid: b8df1828-5ead-4c90-b0fe-95c675116b7c
title: "조직 디자인"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 3a74770a4558c79d1f9250f37181562e1d235d34
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="creating-an-organizational-unit-design"></a>조직 디자인

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

숲 소유자는 도메인 조직 단위 디자인 만드는 담당 합니다. OU 디자인 OU 소유자 역할을 하 고 만드는 계정 및 리소스 Ou 할당 OU 구조 디자인 포함 됩니다.  
  
처음에 디자인 OU 구조 관리 위임 수 있도록 합니다. OU 디자인이 완료 되 면 개체 가시성을 제한 하 고 사용자와 컴퓨터에 그룹 정책을 적용에 대 한 추가 OU 구조 만들 수 있습니다. 자세한 내용은 참조 그룹 정책 인프라 디자인 ([https://go.microsoft.com/fwlink/?LinkId=106655](https://go.microsoft.com/fwlink/?LinkId=106655)).  
  
## <a name="ou-owner-role"></a>OU 소유자 역할  
숲 소유자 OU 소유자 도메인에 대 한 디자인 각 OU 지정 합니다. OU 소유자는 Active Directory Domain Services (AD DS)의 개체 하위를 제어 하는 데이터 관리자입니다. OU 소유자 관리 위임 하는 방법 및 내에서 자녀가 OU 개체 정책이 적용 되는 방식을 제어할 수 있습니다. 또한 새로운 하위 만들 고 이러한 하위 내 Ou 관리 수도 있습니다.  
  
OU 소유자 소유 하지 않거나 제어 디렉터리 서비스의 작동을 하기 때문에 구분할 수 있습니다 소유 하 고 관리 디렉터리 서비스의 소유권 및 물체, 관리를 줄이며 수가 높은 수준의 액세스 권한 가진 서비스 관리자.  
  
Ou는 독립적인 관리 및 디렉터리의 개체 표시 여부를 제어 하는 방법을 제공 합니다. 다른 데이터 관리자에서 Ou 격리 하지만 격리 관리자 서비스의에서 제공 하지 않습니다. OU 소유자의 개체 하위 제어할 있지만, 숲 소유자 모든 하위를 완전히 제어할을 유지 됩니다. 숲 소유자가 (ACL)는 액세스 제어 목록에 오류가 등 실수를 수정 하 고 데이터 관리자 종료 되 면 위임된 하위 확보할 수 있습니다.  
  
## <a name="account-ous-and-resource-ous"></a>계정 Ou 및 리소스 Ou  
계정 Ou 사용자, 그룹과 컴퓨터 개체를 포함 합니다. 숲 소유자 이러한 개체 관리 하 고 다음 구조 제어 OU 소유자에 위임 하는 OU 구조를 만들어야 합니다. 새 AD DS 도메인을 배포 하는 경우 도메인에 있는 계정 제어 위임 수 있도록 OU 도메인 계정을 만듭니다.  
  
리소스 Ou 리소스 및 리소스를 관리 하는 계정 포함 됩니다. 숲 소유자 OU 소유자에 게 해당 구조 제어 위임 및 다음이 리소스를 관리 하는 OU 구조 만드는 대 한 책임 이기도 합니다. 만들기 리소스 Ou 필요에 따라 자율성 관리에서에 대 한 데이터와 장비 조직 내에서 각 그룹의 요구 사항에 따라 합니다.  
  
## <a name="documenting-the-ou-design-for-each-domain"></a>각 도메인에 대 한 OU 디자인 기록  
팀 OU 구조 위임 리소스 숲 내 제어를 사용 하는 디자인을 구성 합니다. 숲 소유자 디자인 프로세스에 참여 수 있으며 OU 디자인 승인 해야 합니다. 하나 이상의 서비스 관리자에 디자인 올바른지 확인 포함 될 수도 있습니다. 다른 디자인 팀 참가자 관리 하는 소유자는 Ou 및 OU에서 작동 하는 데이터 관리자 포함 될 수 있습니다.  
  
문서 OU 디자인을 고려해 야 합니다. 만들려는 Ou의 이름을 표시 합니다. 및 각 OU에 대 한 문서 OU, OU 소유자, 부모 OU (가능한 경우), 그 OU 출처의 형식 있습니다.  
  
다운로드 Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip).  
  
## <a name="in-this-section"></a>이 섹션에서  
  
-   [OU 디자인 개념을 검토](../../ad-ds/plan/Reviewing-OU-Design-Concepts.md)  
  
-   [관리 OU 개체를 사용 하 여 위임](../../ad-ds/plan/Delegating-Administration-by-Using-OU-Objects.md)  
  


