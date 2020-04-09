---
ms.assetid: d8e61aa4-8e4b-4097-83ca-70cf61366b75
title: OU 개체를 사용하여 관리 위임
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: af13896c07c10710be6e087be5d31dbd4aec698f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80822716"
---
# <a name="delegating-administration-by-using-ou-objects"></a>OU 개체를 사용하여 관리 위임

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ou (조직 구성 단위)를 사용 하 여 OU 내에서 사용자 또는 컴퓨터와 같은 개체 관리를 지정 된 개인 또는 그룹에 위임할 수 있습니다. OU를 사용 하 여 관리를 위임 하려면 그룹에 관리 권한을 위임할 개인 또는 그룹을 저장 하 고, 개체 집합을 OU에 배치한 후 OU의 관리 태스크를 해당 그룹에 위임 합니다.  
  
Active Directory Domain Services (AD DS)를 사용 하면 매우 세부적인 수준에서 위임할 수 있는 관리 작업을 제어할 수 있습니다. 예를 들어 OU의 모든 개체에 대 한 모든 권한을 가진 그룹 하나를 할당할 수 있습니다. 다른 그룹에 OU의 사용자 계정을 만들고, 삭제 하 고, 관리 하는 권한만 할당 합니다. 그런 다음 사용자 계정 암호를 다시 설정할 수 있는 권한을 세 번째 그룹에 할당 합니다. 원본 OU의 하위 트리에 배치 된 모든 Ou에 적용 되도록 이러한 사용 권한을 상속 가능 하 게 만들 수 있습니다.  
  
기본 Ou와 컨테이너는 AD DS 설치 하는 동안 만들어지고 서비스 관리자가 제어 합니다. 서비스 관리자가 이러한 컨테이너를 계속 제어 하는 것이 가장 좋습니다. 디렉터리의 개체에 대 한 제어를 위임 해야 하는 경우 Ou를 추가 하 고 이러한 Ou에 개체를 저장 합니다. 해당 Ou에 대 한 제어를 적절 한 데이터 관리자에 게 위임 합니다. 이렇게 하면 서비스 관리자에 게 제공 되는 기본 컨트롤을 변경 하지 않고 디렉터리의 개체에 대 한 제어를 위임할 수 있습니다.  
  
포리스트 소유자는 OU 소유자에 게 위임 된 권한 수준을 결정 합니다. 이 경우 ou 내에서 개체를 만들고 조작 하는 기능을 통해 OU에 있는 단일 형식의 개체에 대 한 단일 특성만 제어할 수 있습니다. 사용자에 게 OU에서 개체를 만들 수 있는 기능을 부여 하면 사용자가 만드는 모든 개체의 특성을 조작할 수 있는 권한이 해당 사용자에 게 암시적으로 부여 됩니다. 또한 만든 개체가 컨테이너인 경우에는 사용자에 게 컨테이너에 배치 된 개체를 만들고 조작 하는 기능이 암시적으로 제공 됩니다.  
  
## <a name="in-this-section"></a>단원 내용  
  
-   [기본 컨테이너 및 OU 관리 위임](../../ad-ds/plan/Delegating-Administration-of-Default-Containers-and-OUs.md)  
  
-   [계정 OU 및 리소스 OU 관리 위임](../../ad-ds/plan/Delegating-Administration-of-Account-OUs-and-Resource-OUs.md)  
  


