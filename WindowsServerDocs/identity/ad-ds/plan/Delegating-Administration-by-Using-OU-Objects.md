---
ms.assetid: d8e61aa4-8e4b-4097-83ca-70cf61366b75
title: OU 개체를 사용하여 관리 위임
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 39c4278270e4ab4fba9ff1062d2aa043d203a74b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886944"
---
# <a name="delegating-administration-by-using-ou-objects"></a>OU 개체를 사용하여 관리 위임

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

지정 된 개인 또는 그룹에 OU에 사용자 또는 컴퓨터 같은 개체의 관리를 위임할 수 조직 구성 단위 (Ou)를 사용할 수 있습니다. OU를 사용 하 여 관리를 위임 하려면 개인 또는 그룹을 그룹에 관리 권한을 위임는 배치에 대 한 OU를 제어 하는 개체 집합 놓고 해당 그룹에 OU에 대 한 관리 작업을 위임 합니다.  
  
Active Directory Domain Services (AD DS)를 사용 하면 매우 세부적인된 수준에서 위임할 수 있는 관리 작업을 제어할 수 있습니다. 예를 들어; OU의 모든 개체의 전체 제어를 하나의 그룹에 할당할 수 있습니다. 다른 그룹 만들기, 삭제 및; OU에서 사용자 계정 관리에 권한을 할당합니다 및 다음 할당 세 번째 그룹에 권한을 사용자 계정 암호 재설정에 합니다. 원래 OU의 하위 트리에 있는 모든 Ou에 적용 되도록 이러한 권한을 상속할 수 만들 수 있습니다.  
  
기본 Ou와 컨테이너에는 AD DS 설치 중 생성 되 고 서비스 관리자에 의해 제어 됩니다. 서비스 관리자는 계속 이러한 컨테이너를 제어 하는 것이 좋습니다. 디렉터리 개체에에서 대 한 제어를 위임 하는 경우 추가 Ou 만들고 이러한 Ou의 개체를 배치 합니다. 적절 한 데이터 관리자에 게 이러한 Ou에 대 한 제어를 위임 합니다. 이 서비스 관리자에 지정 된 기본 컨트롤을 변경 하지 않고도 디렉터리 개체에에서 대 한 제어를 위임할 수 있습니다.  
  
포리스트 소유자 OU 소유자에 위임 된 권한 수준을 결정 합니다. 만들기 및 OU에 있는 개체의 단일 형식의 단일 특성 제어만 허용 하는 OU 내에서 개체를 조작 하는 기능에서 지정할 수 있습니다. OU에 암시적으로 개체를 만들 수는 사용자에 게 부여 부여 사용자 사용자가 만드는 모든 개체의 모든 특성을 조작할 수 있습니다. 또한 만든 개체가 컨테이너 이면 사용자를 만들고 컨테이너에 있는 모든 개체를 조작할 수 암시적으로 있습니다.  
  
## <a name="in-this-section"></a>단원 내용  
  
-   [기본 컨테이너 및 Ou 관리 위임](../../ad-ds/plan/Delegating-Administration-of-Default-Containers-and-OUs.md)  
  
-   [계정 Ou 및 리소스 Ou 관리 위임](../../ad-ds/plan/Delegating-Administration-of-Account-OUs-and-Resource-OUs.md)  
  


