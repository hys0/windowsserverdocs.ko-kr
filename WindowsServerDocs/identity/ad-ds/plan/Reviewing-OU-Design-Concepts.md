---
ms.assetid: 41b56704-c6f9-4d29-af97-62123e300565
title: OU 디자인 개념 검토
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 67f8ef3ec37146002f3e099caa459fc209fcf5b7
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80821977"
---
# <a name="reviewing-ou-design-concepts"></a>OU 디자인 개념 검토

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

도메인의 OU (조직 구성 단위) 구조에는 다음이 포함 됩니다.  
  
-   OU 계층 구조 다이어그램  
  
-   Ou 목록  
  
-   각 OU:  
  
    -   OU의 용도  
  
    -   Ou 또는 OU의 개체에 대 한 제어 권한이 있는 사용자 또는 그룹 목록  
  
    -   사용자 및 그룹이 OU의 개체에 대해 보유 하 고 있는 컨트롤의 형식입니다.  
  
OU 계층 구조는 조직 또는 그룹의 부서별 계층 구조를 반영 하지 않아도 됩니다. Ou는 관리 위임, 그룹 정책 응용 프로그램 등의 특정 용도에 대해 만들어지며 개체의 표시 여부를 제한 합니다.  
  
조직의 개인 또는 그룹에 대 한 관리를 위임 하 여 자신의 리소스와 데이터를 관리 해야 하는 조직의 개인 또는 그룹에 대 한 관리를 위임 하도록 OU 구조를 설계할 수 있습니다. Ou는 관리 경계를 나타내며 데이터 관리자의 권한 범위를 제어할 수 있습니다.  
  
예를 들어 ResourceOU 라는 OU를 만들고이를 사용 하 여 그룹에서 관리 하는 파일 및 인쇄 서버에 속하는 모든 컴퓨터 계정을 저장할 수 있습니다. 그런 다음 그룹의 데이터 관리자만이 OU에 액세스할 수 있도록 OU에 보안을 구성할 수 있습니다. 이렇게 하면 다른 그룹의 데이터 관리자가 파일 및 인쇄 서버 계정을 변경할 수 없습니다.  
  
그룹 정책 응용 프로그램과 같은 특정 용도의 Ou 하위 트리를 만들어 특정 사용자만 볼 수 있도록 보호 된 개체의 표시 여부를 제한 하 여 OU 구조를 더 구체화할 수 있습니다. 예를 들어 사용자 또는 리소스의 선택 그룹에 그룹 정책를 적용 해야 하는 경우 해당 사용자 또는 리소스를 OU에 추가 하 고 해당 OU에 그룹 정책을 적용할 수 있습니다. 또한 OU 계층 구조를 사용 하 여 관리 제어를 추가로 위임할 수 있습니다.  
  
OU 구조의 수준 수에 대 한 기술적인 제한은 없지만 관리 효율성을 위해 OU 구조를 10 개 수준 이하로 제한 하는 것이 좋습니다. 각 수준의 Ou 수에 대 한 기술적인 제한은 없습니다. Active Directory Domain Services (AD DS) 사용 응용 프로그램은 고유 이름 (즉, 디렉터리에 있는 개체에 대 한 전체 LDAP (Lightweight Directory Access Protocol) 경로) 또는 계층 내 OU 깊이에서 사용 되는 문자 수에 제한이 있을 수 있습니다.  
  
AD DS의 OU 구조는 최종 사용자에 게 표시 되지 않습니다. OU 구조는 서비스 관리자와 데이터 관리자를 위한 관리 도구로, 쉽게 변경할 수 있습니다. 계속 해 서 OU 구조 디자인을 검토 하 고 업데이트 하 여 관리 구조의 변경 사항을 반영 하 고 정책 기반 관리를 지원 합니다.  
  


