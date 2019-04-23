---
ms.assetid: ac6604b0-7459-4ff3-af1c-4936897f5d14
title: 기본 컨테이너 및 OU의 관리 위임
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 9d482854fd82b4bf0d0e61315d36e6222470ca55
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59830894"
---
# <a name="delegating-administration-of-default-containers-and-ous"></a>기본 컨테이너 및 OU의 관리 위임

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

모든 Active Directory 도메인에는 컨테이너 및 Active Directory Domain Services (AD DS)를 설치 하는 동안 만든 조직 구성 단위 (Ou)의 표준 집합을 포함 합니다. 여기에는 다음과 같은 옵션이 포함됩니다.  
  
-   계층에 루트 컨테이너 역할을 하는 도메인 컨테이너를  
  
-   기본 서비스 관리자 계정을 보유 하는 기본 제공 컨테이너  
  
-   도메인에서 만든 새 사용자 계정 및 그룹에 대 한 기본 위치는 사용자 컨테이너  
  
-   도메인에는 새 컴퓨터 계정에 대 한 기본 위치는 컴퓨터 컨테이너 생성  
  
-   도메인 컨트롤러 컴퓨터 계정에 대 한 컴퓨터 계정에 대 한 기본 위치는 도메인 컨트롤러 OU  
  
포리스트 소유자는 이러한 기본 컨테이너 및 Ou를 제어합니다.  
  
## <a name="domain-container"></a>도메인 컨테이너  
도메인 컨테이너는 루트 컨테이너는 도메인의 계층 구조입니다. 정책 또는이 컨테이너에서 액세스 제어 목록 (ACL)을 변경할 도메인 전체에 영향을 미칠 수 있습니다. 이 컨테이너의 제어를 위임 하지 않는 서비스 관리자에 의해 제어 해야 합니다.  
  
## <a name="users-and-computers-containers"></a>사용자 및 컴퓨터 컨테이너  
Windows Server 2003에서 Windows Server 2008 전체 도메인 업그레이드를 수행한 경우 기존 사용자 및 컴퓨터 사용자 및 컴퓨터 컨테이너에 자동으로 배치 됩니다. 새 Active Directory 도메인, 사용자 및 컴퓨터 컨테이너 만드는 경우 모든 새 사용자 계정 및 도메인의 도메인 컨트롤러가 아닌 컴퓨터 계정에 대 한 기본 위치입니다.  
  
> [!IMPORTANT]  
> 사용자 또는 컴퓨터에 대 한 제어를 위임 해야 하는 경우 사용자 및 컴퓨터에서 기본 설정을 수정 하지 마십시오 컨테이너입니다. 대신 필요에 따라 새 Ou를 만들 및 해당 기본 컨테이너에서 새 Ou에 사용자 및 컴퓨터 개체를 이동 합니다. 필요에 따라 새 Ou에 대 한 제어를 위임 합니다. 수정 하지 않는 기본 컨테이너를 제어 하는 것이 좋습니다.  
  
기본 사용자 및 컴퓨터에 그룹 정책 설정을 적용할 수 없습니다는 또한 컨테이너입니다. 그룹에 정책을 적용할 사용자 및 컴퓨터를 새 Ou를 만들고 해당 Ou에 사용자 및 컴퓨터 개체를 이동 합니다. 새 Ou에 그룹 정책 설정을 적용 합니다.  
  
필요에 따라 선택한 컨테이너에 배치 하는 기본 컨테이너에 있는 개체의 생성을 리디렉션할 수 있습니다.  
  
## <a name="well-known-users-and-groups-and-built-in-accounts"></a>잘 알려진 사용자와 그룹 및 기본 제공 계정  
기본적으로 새 도메인에서 몇 가지 잘 알려진 사용자와 그룹 및 기본 제공 계정이 생성 됩니다. 이러한 계정 관리를 서비스 관리자의 제어 아래로 유지 되는 것이 좋습니다. 서비스 관리자가 아닌 사용자 에게만 이러한 계정의 관리를 위임 하지 않는 합니다. 다음 표에서 잘 알려진 사용자와 그룹 및 서비스 관리자의 제어 권한이 유지 해야 하는 기본 제공 계정입니다.  
  
|잘 알려진 사용자 및 그룹|기본 제공 계정|  
|--------------------------------|----------------------|  
|Cert Publishers<br /><br />도메인 컨트롤러 하나 이상<br /><br />Group Policy Creator Owners<br /><br />KRBTGT<br /><br />도메인 게스트<br /><br />관리자<br /><br />Domain Admins<br /><br />스키마 Admins (포리스트 루트 도메인에만 해당)<br /><br />Enterprise Admins (포리스트 루트 도메인에만 해당)<br /><br />도메인 사용자|관리자<br /><br />게스트<br /><br />Guests<br /><br />Account Operators<br /><br />Administrators<br /><br />Backup Operators<br /><br />들어오는 포리스트 트러스트 작성기<br /><br />Print Operators<br /><br />Pre-Windows 2000 Compatible Access<br /><br />Server Operators<br /><br />사용자|  
  
## <a name="domain-controller-ou"></a>도메인 컨트롤러 OU  
도메인 컨트롤러는 도메인에 추가 되 면 해당 컴퓨터 개체에 도메인 컨트롤러 OU에 자동으로 추가 됩니다. 이 OU 집합이 기본 정책이 적용 됩니다. 이러한 정책은 모든 도메인 컨트롤러에 균일 하 게 적용 됩니다 있도록이 OU에서 도메인 컨트롤러의 컴퓨터 개체를 이동 하지는 것이 좋습니다. 기본 정책을 적용 하려면 도메인 컨트롤러를 제대로 작동 하지 않을 수 있습니다.  
  
기본적으로 서비스 관리자는이 OU를 제어합니다. 서비스 관리자가 아닌 개인에 게 해당이 OU의 제어를 위임 하지 않는 합니다.  
  


