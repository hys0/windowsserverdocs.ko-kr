---
ms.assetid: b8df1828-5ead-4c90-b0fe-95c675116b7c
title: 조직 구성 단위 디자인 만들기
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 9ecd0228b50a4e597c3fa1dbd3fdaf1f84ca1d3f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59830404"
---
# <a name="creating-an-organizational-unit-design"></a>조직 구성 단위 디자인 만들기

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

포리스트 소유자는 해당 도메인에 대 한 조직 구성 단위 (OU) 디자인을 담당 합니다. OU 디자인을 만들려면 OU 소유자 역할을 하 고 만드는 계정 및 리소스 Ou 할당 OU 구조를 디자인 하는 작업을 해야 합니다.  
  
처음에 위임 된 관리를 사용 하도록 설정 하려면 OU 구조를 디자인 합니다. OU 디자인 완료 되 면 사용자 및 컴퓨터 및 개체의 표시를 제한 하려면 그룹 정책 적용에 대 한 추가 OU 구조를 만들 수 있습니다. 자세한 내용은 그룹 정책 인프라 디자인을 참조 ([https://go.microsoft.com/fwlink/?LinkId=106655](https://go.microsoft.com/fwlink/?LinkId=106655)).  
  
## <a name="ou-owner-role"></a>OU 소유자 역할  
도메인에 대 한 디자인 하는 각 OU에 대 한 OU 소유자를 지정 하는 포리스트 소유자입니다. OU 소유자는 Active Directory Domain Services (AD DS)에 있는 개체의 하위 트리를 제어 하는 데이터 관리자입니다. OU 소유자 관리를 위임 하는 방법 및 정책을 해당 OU 내에서 개체에 적용 되는 방식을 제어할 수 있습니다. 또한 새 하위 트리를 만들 수 있으며 해당 하위 트리 내에서 ou 관리 위임.  
  
있으므로 OU 소유자 소유 하지 않거나 디렉터리 서비스의 작업을 제어을 분리할 수 있습니다 소유권 및 디렉터리 서비스의 관리에서 소유권 및 관리 개체의 서비스 관리자에 게 높은 수준의 수를 줄이면 액세스 합니다.  
  
Ou는 독립적인 관리 및 디렉터리에 있는 개체의 표시 유형을 제어 하는 방법을 제공 합니다. Ou는 다른 데이터 관리자에서 격리를 제공 하지만 격리 서비스 관리자에 게에서 제공 하지 않습니다. OU 소유자 개체의 하위 트리에 대 한 제어를 갖지만 포리스트 소유자는 모든 하위 트리에 대 한 모든 권한을 유지 합니다. 이 통해 포리스트 소유자를 액세스 제어 목록 (ACL), 오류 등의 실수를 수정 하 고 데이터 관리자가 종료 되는 경우 위임 된 하위 트리를 회수를 수 있습니다.  
  
## <a name="account-ous-and-resource-ous"></a>계정 Ou 및 리소스 Ou  
계정 Ou 사용자, 그룹 및 컴퓨터 개체를 포함 합니다. 포리스트 소유자는 이러한 개체를 관리 하 고 다음 구조 제어 OU 소유자에 게 위임 하는 OU 구조를 만들어야 합니다. 새 AD DS 도메인을 배포 하는 경우 도메인의 계정 제어를 위임할 수 있도록 도메인에 대 한 계정을 OU를 만듭니다.  
  
리소스 Ou 리소스 및 해당 리소스를 관리 하는 일을 담당 하는 계정을 포함 합니다. 포리스트 소유자 해당 구조 제어 OU 소유자에 게 위임 하 고 이러한 리소스를 관리 하는 OU 구조를 만들기 위한 이기도 합니다. 리소스 Ou 필요에 따라 만들 데이터 및 장치 관리에는 자치를 위해 조직 내에서 각 그룹의 요구 사항을 기반으로 합니다.  
  
## <a name="documenting-the-ou-design-for-each-domain"></a>각 도메인에 대 한 OU 설계를 문서화  
포리스트 내에서 리소스에 대 한 제어를 위임 하는 데 사용 하는 OU 구조를 디자인 하려면 팀을 구성 합니다. 포리스트 소유자 디자인 프로세스에 포함 될 수 있습니다 및 OU 디자인을 승인 해야 합니다. 또한 디자인 올바른지 확인 하려면 하나 이상의 서비스 관리자를 포함할 수 있습니다. 다른 디자인 팀 참가자가 관리 하는 일을 담당 하는 소유자 Ou 및 OU에서 작동 하는 데이터 관리자를 포함할 수 있습니다.  
  
OU 디자인을 문서화 하는 것이 반드시 합니다. 만들려는 Ou의 이름을 나열 합니다. 및 각 OU에 대 한 OU, OU 소유자, 상위 OU (있는 경우) 및 해당 OU의 원본 형식을 문서화 합니다.  
  
OU 디자인을 문서화에 도움을 주는 워크시트에 대 한 작업 보조 기능에 대 한 Windows Server 2003 Deployment Kit에서 Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip 다운로드 ([https://go.microsoft.com/fwlink/?LinkID=102558](https://go.microsoft.com/fwlink/?LinkID=102558)) 연 " 각 도메인에 대 한 Ou 식별"(DSSLOGI_9.doc).  
  
## <a name="in-this-section"></a>단원 내용  
  
-   [OU 디자인 개념 검토](../../ad-ds/plan/Reviewing-OU-Design-Concepts.md)  
  
-   [OU 개체를 사용 하 여 관리 위임](../../ad-ds/plan/Delegating-Administration-by-Using-OU-Objects.md)  
  


