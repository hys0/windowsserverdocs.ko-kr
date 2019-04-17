---
ms.assetid: 41b56704-c6f9-4d29-af97-62123e300565
title: "OU 디자인 개념을 검토"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 0e832d068a4d03316853d8b59e3f2ac4a6ebc816
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="reviewing-ou-design-concepts"></a>OU 디자인 개념을 검토

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

도메인에 대 한 조직 단위 구조 다음과 같습니다.  
  
-   OU 계층 다이어그램  
  
-   Ou 목록  
  
-   각 OU 다음과 같습니다.  
  
    -   Ou 목적  
  
    -   사용자 또는 그룹 OU의 개체 또는 OU 제어할 수 있는의 목록  
  
    -   사용자 및 그룹 개체 OU에 대 한 컨트롤 유형  
  
조직 또는 그룹의 부서 계층을 반영 하기 위해 OU 계층 필요가 없습니다. Ou 그룹 정책 또는 개체 가시성을 제한 하는 응용 프로그램 관리, 위임와 같은 특정 목적을 위해 생성 됩니다.  
  
개인 또는 자체 리소스와 데이터를 관리 하려면 자유롭게 해야 하는 그룹 조직에서 관리 위임 OU 구조를 만들 수 있습니다. Ou 관리 경계 나타내고 한 데이터 관리자 권한 범위를 제어할 수 있습니다.  
  
예를 들어, 라는 ResourceOU OU 만들 하 고 사용 하 여 파일 및 인쇄 서버 관리 하는 그룹에 속해 있는 모든 컴퓨터 계정 저장할 수 있습니다. 그런 다음를 액세스할 수 있는 그룹에 데이터 관리자만 보안 OU에 구성할 수 있습니다. 이렇게 하면 무단 파일 및 인쇄 서버 계정으로 다른 그룹에 대 한 데이터 관리자를 않습니다.  
  
그룹 정책 또는 특정 사용자가 볼 수 없도록 보호 개체 가시성을 제한 하는 응용 프로그램 처럼 특정 목적에의 Ou 하위 만들어 OU 구조를 조정할 수 있습니다. 예를 들어, 사용자 또는 리소스를 선택 하 고 그룹 그룹 정책을 적용 해야 하는 경우 해당 사용자 또는 리소스 OU을을 추가한 다음 해당 OU 그룹 정책을 적용 합니다. 또한 위임 관리 제어의 더욱 사용 하도록 OU 계층을 사용할 수 있습니다.  
  
수준 OU 구조의 수에 제한이 기술 이지만, 관리에 대 한 것이 좋습니다 10 수준 보다 더 깊이 OU 구조를 제한 합니다. 각 수준을 Ou 수에 제한이 기술 있습니다. 참고 Active Directory Domain Services (AD DS) 해당-사용된 응용 프로그램 (즉, 전체 LDAP(Lightweight Directory Access Protocol) (LDAP) 경로를 디렉터리의 개체) 고유 이름에 사용 되는 문자의 수에 제한이 있을 수 있습니다 또는 계층 내 OU 깊이 합니다.  
  
AD DS OU 구조 최종 사용자가 볼 수 없습니다. OU 구조 관리 하는 도구 및 관리자 데이터를 서비스 관리자에 대 한 이며 쉽게 변경할 수 있습니다. 계속 검토 및 지원 정책 기반 관리 하 고 관리 구조의 변경 사항을 반영 하기 위해 OU 구조 디자인을 업데이트 합니다.  
  


