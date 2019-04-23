---
ms.assetid: 41b56704-c6f9-4d29-af97-62123e300565
title: OU 디자인 개념 검토
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: f05104466c1cedcfbc8d94060ffa8fbfd9d18033
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59832174"
---
# <a name="reviewing-ou-design-concepts"></a>OU 디자인 개념 검토

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

도메인의 OU (조직 단위) 구조는 다음과 같습니다.  
  
-   OU 계층 구조 다이어그램  
  
-   Ou의 목록  
  
-   각 OU:  
  
    -   OU에 대 한 용도  
  
    -   OU의 OU 또는 개체를 통해 권한이 있는 사용자 또는 그룹의 목록  
  
    -   OU의 개체에 대 한 사용자 및 그룹 컨트롤의 형식  
  
OU 계층 구조 부서별 조직 또는 그룹의 계층 구조를 반영 하지 않아도 됩니다. Ou의 그룹 정책 또는 개체의 표시를 제한 하려면 응용 프로그램 관리를 위임 같은 특정 목적을 위해 생성 됩니다.  
  
개인 또는 조직 내에서 고유한 리소스 및 데이터 관리에 자율성을 필요로 하는 그룹 관리를 위임할 OU 구조를 디자인할 수 있습니다. Ou 관리 경계를 나타내고 데이터 관리자의 인증 범위를 제어할 수 있습니다.  
  
예를 들어 ResourceOU 호출 된 OU를 만들고 파일 그룹에 의해 관리 되는 인쇄 서버에 속하는 모든 컴퓨터 계정을 저장 하는 데 사용할 수 있습니다. 그런 다음 그룹에서 데이터 관리자만 OU에 액세스할 수 있도록 OU에서 보안을 구성할 수 있습니다. 이 데이터 관리자가 다른 그룹의 파일 및 인쇄 서버 계정을 사용 하 여 변조를 방지 합니다.  
  
그룹 정책 또는 특정 사용자만 볼 수 있도록 보호 되는 개체의 표시 여부를 제한 하는 응용 프로그램 등 특정 용도 대 한 Ou의 하위 트리를 만들어 OU 구조를 더욱 구체화할 수 있습니다. 예를 들어, 사용자 또는 리소스 선택 그룹에 그룹 정책을 적용 해야 할 경우 해당 사용자 또는 리소스를 OU을 추가한 다음 그룹 정책을 해당 OU에 적용 합니다. 위임을 사용 하도록 추가로 관리 제어의 OU 계층 구조를 사용할 수도 있습니다.  
  
OU 구조에는 수준 수에 제한이 없음을 기술 이지만, 관리 효율성에 대 한 것이 좋습니다 OU 구조 수가 10 개 수준 깊이 제한 하는 것입니다. 각 수준에서 Ou의 수는 기술적인 제한은 없습니다. 참고 해당 Active Directory Domain Services (AD DS)-응용 프로그램의 고유 이름 (즉, 전체 LDAP Lightweight Directory Access Protocol () 경로 디렉터리에서 개체)에 사용 되는 또는 문자 수에 제한이 있을 수 있습니다는 계층 내에서 OU 깊이입니다.  
  
최종 사용자에 게 표시 되도록 AD DS의 OU 구조를 사용 하는 것이 없습니다. OU 구조는 서비스 관리자와 데이터 관리자에 대 한 관리 도구 및 변경 하는 것이 쉽습니다. 검토 및 사용자 관리 구조에 대 한 변경 내용을 반영 하 고 정책 기반 관리를 지원 하도록 OU 구조 디자인 업데이트를 계속 합니다.  
  


