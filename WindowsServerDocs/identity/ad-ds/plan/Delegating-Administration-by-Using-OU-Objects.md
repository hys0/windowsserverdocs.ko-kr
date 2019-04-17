---
ms.assetid: d8e61aa4-8e4b-4097-83ca-70cf61366b75
title: "관리 OU 개체를 사용 하 여 위임"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 8d0b4765304d8b302fc174c191af2c8e87a25304
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="delegating-administration-by-using-ou-objects"></a>관리 OU 개체를 사용 하 여 위임

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

지정 된 개인 또는 그룹 OU 내의 관리 등 사용자 또는 컴퓨터의 개체 위임 하 조직 (Ou)을 사용할 수 있습니다. 관리를 OU을 사용 하 여 위임 하려면 장소 개인 또는 그룹을 위임 관리자 권한 그룹으로 개체 ou을 제어할 수를 설정 놓고 관리 작업 그룹에 ou 위임.  
  
Active Directory 도메인 서비스 (AD DS) 매우 자세한 수준 위임 될 수 있는 관리 작업을 제어할 수 있습니다. 예를 들어, 한 그룹에; 모든 개체의 모든 권한이를 지정할 수 있습니다. 다른 그룹 만드는, 삭제 및 관리 OU;의 사용자 계정에만 권한이 지정 한 다음 지정 제 3 그룹화만 사용자 계정 암호 다시 설정 수행할 수 있습니다. 원래의 하위에 있는 모든 Ou 적용 되도록 이러한 권한은 상속 할 수 있습니다.  
  
기본 Ou 및 컨테이너 광고 DS 설치 시 생성 되 고 서비스 관리자에서 제어 됩니다. 서비스 관리자 계속 이러한 컨테이너 제어 하는 것이 좋습니다. 위임 개체 디렉터리에 대 한 제어 하려는 경우 추가 Ou 만들고 개체 이러한 Ou에 배치 합니다. 적절 한 데이터 관리자에 게 이러한 Ou 제어할을 위임 합니다. 이 서비스 관리자에 게 부여 기본 제어를 변경 하지 않고 디렉터리의 개체 제어할 위임 수 있습니다.  
  
숲 소유자 OU 소유자에 위임 하는 기관의 결정 합니다. 이 만들고 OU 한 가지 형식의 OU에서 개체의 단일 특성을 제어할 수만 내의 개체를 조작 하는 기능에서 까지입니다. 부여 사용자 암시적 OU 개체를 만들 수 있는 사용자가 작성 개체의 특성을 조작 하는 기능 해당 사용자 부여 합니다. 또한 만든 개체 컨테이너 경우, 사용자를 만들고 컨테이너에 추가 하는 모든 개체를 조작할 수 암시적 있습니다.  
  
## <a name="in-this-section"></a>이 섹션에서  
  
-   [기본 컨테이너 및 Ou 관리 위임](../../ad-ds/plan/Delegating-Administration-of-Default-Containers-and-OUs.md)  
  
-   [계정 Ou 및 리소스 Ou 관리 위임](../../ad-ds/plan/Delegating-Administration-of-Account-OUs-and-Resource-OUs.md)  
  


