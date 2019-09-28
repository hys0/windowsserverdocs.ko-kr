---
ms.assetid: ac6604b0-7459-4ff3-af1c-4936897f5d14
title: 기본 컨테이너 및 OU의 관리 위임
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 15c6688e32a7ebefbb2dd0fa1e53a4d72baef267
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408931"
---
# <a name="delegating-administration-of-default-containers-and-ous"></a>기본 컨테이너 및 OU의 관리 위임

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

모든 Active Directory 도메인에는 Active Directory Domain Services (AD DS) 설치 중에 생성 되는 컨테이너 및 Ou (조직 구성 단위)의 표준 집합이 포함 되어 있습니다. 여기에는 다음과 같은 옵션이 포함됩니다.  
  
-   계층 구조에 대 한 루트 컨테이너 역할을 하는 도메인 컨테이너  
  
-   기본 제공 컨테이너-기본 서비스 관리자 계정을 보유 합니다.  
  
-   새 사용자 계정 및 도메인에서 만든 그룹의 기본 위치인 사용자 컨테이너  
  
-   컴퓨터 컨테이너는 도메인에서 만든 새 컴퓨터 계정의 기본 위치입니다.  
  
-   도메인 컨트롤러의 컴퓨터 계정에 대 한 기본 위치인 도메인 컨트롤러 OU  
  
포리스트 소유자는 이러한 기본 컨테이너와 Ou를 제어 합니다.  
  
## <a name="domain-container"></a>도메인 컨테이너  
도메인 컨테이너는 도메인 계층 구조의 루트 컨테이너입니다. 이 컨테이너의 정책 또는 ACL (액세스 제어 목록)을 변경 하면 도메인 전체에 영향을 줄 수 있습니다. 이 컨테이너의 제어를 위임 하지 마십시오. 서비스 관리자가 제어 해야 합니다.  
  
## <a name="users-and-computers-containers"></a>사용자 및 컴퓨터 컨테이너  
Windows Server 2003에서 Windows Server 2008로 전체 도메인 업그레이드를 수행 하면 기존 사용자 및 컴퓨터가 자동으로 사용자 및 컴퓨터 컨테이너에 배치 됩니다. 새 Active Directory 도메인을 만드는 경우 사용자 및 컴퓨터 컨테이너는 도메인에 있는 모든 새 사용자 계정 및 도메인 컨트롤러가 아닌 컴퓨터 계정에 대 한 기본 위치입니다.  
  
> [!IMPORTANT]  
> 사용자 또는 컴퓨터에 대 한 제어를 위임 해야 하는 경우에는 사용자 및 컴퓨터 컨테이너에서 기본 설정을 수정 하지 마십시오. 대신, 필요에 따라 새 Ou를 만들고 사용자 및 컴퓨터 개체를 기본 컨테이너와 새 Ou로 이동 합니다. 필요에 따라 새 Ou에 대 한 제어를 위임 합니다. 기본 컨테이너를 제어 하는 사용자를 수정 하지 않는 것이 좋습니다.  
  
또한 기본 사용자 및 컴퓨터 컨테이너에 그룹 정책 설정을 적용할 수 없습니다. 사용자 및 컴퓨터에 그룹 정책를 적용 하려면 새 Ou를 만들고 사용자 및 컴퓨터 개체를 해당 Ou로 이동 합니다. 새 Ou에 그룹 정책 설정을 적용 합니다.  
  
필요에 따라 기본 컨테이너에 배치 되는 개체 생성을 사용자가 선택한 컨테이너에 배치 하도록 리디렉션할 수 있습니다.  
  
## <a name="well-known-users-and-groups-and-built-in-accounts"></a>잘 알려진 사용자 및 그룹 및 기본 제공 계정  
기본적으로 잘 알려진 여러 사용자 및 그룹과 기본 제공 계정이 새 도메인에 만들어집니다. 이러한 계정에 대 한 관리는 서비스 관리자의 제어로 유지 하는 것이 좋습니다. 이러한 계정의 관리를 서비스 관리자가 아닌 개인에 게 위임 하지 마십시오. 다음 표에는 잘 알려진 사용자 및 그룹과 서비스 관리자의 제어를 유지 해야 하는 기본 제공 계정이 나와 있습니다.  
  
|잘 알려진 사용자 및 그룹|기본 제공 계정|  
|--------------------------------|----------------------|  
|Cert Publishers<br /><br />도메인 컨트롤러 하나 이상<br /><br />Group Policy Creator Owners<br /><br />KRBTGT<br /><br />도메인 게스트<br /><br />관리자<br /><br />Domain Admins<br /><br />스키마 관리자 (포리스트 루트 도메인에만 해당)<br /><br />Enterprise Admins (포리스트 루트 도메인에만 해당)<br /><br />도메인 사용자|관리자<br /><br />게스트<br /><br />Guests<br /><br />Account Operators<br /><br />Administrators<br /><br />Backup Operators<br /><br />들어오는 포리스트 트러스트 빌더<br /><br />Print Operators<br /><br />Windows 2000 이전 버전과 호환 되는 액세스<br /><br />Server Operators<br /><br />사용자|  
  
## <a name="domain-controller-ou"></a>도메인 컨트롤러 OU  
도메인 컨트롤러를 도메인에 추가 하면 해당 컴퓨터 개체가 도메인 컨트롤러 OU에 자동으로 추가 됩니다. 이 OU에는 기본 정책 집합이 적용 됩니다. 이러한 정책이 모든 도메인 컨트롤러에 균일 하 게 적용 되도록 하려면 도메인 컨트롤러의 컴퓨터 개체를이 OU 외부로 이동 하지 않는 것이 좋습니다. 기본 정책을 적용 하지 않으면 도메인 컨트롤러가 제대로 작동 하지 않을 수 있습니다.  
  
기본적으로 서비스 관리자는이 OU를 제어 합니다. 서비스 관리자가 아닌 사용자에 게이 OU 제어를 위임 하지 마십시오.  
  


