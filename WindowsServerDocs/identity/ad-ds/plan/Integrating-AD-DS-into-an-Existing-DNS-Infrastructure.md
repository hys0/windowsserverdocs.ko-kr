---
ms.assetid: 4981b32f-741e-4afc-8734-26a8533ac530
title: 기존 DNS 인프라에 AD DS 통합
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 62405ea9ee38bb3fa457b7731e26fbffb2594797
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59891044"
---
# <a name="integrating-ad-ds-into-an-existing-dns-infrastructure"></a>기존 DNS 인프라에 AD DS 통합

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

기존 도메인 이름 시스템 (DNS) 서버 서비스 조직에 이미 있으면 기존 인프라에 AD DS를 통합 하 여 조직에 대 한 DNS 소유자를 사용 하 여 Active Directory Domain Services (AD DS) 소유자에 대 한 DNS 작동 해야 합니다. DNS 서버 및 DNS 클라이언트 구성을 생성이 포함 됩니다.  
  
## <a name="creating-a-dns-server-configuration"></a>DNS 서버 구성 만들기  
기존 DNS 네임 스페이스를 사용 하 여 AD DS와 통합 하는 경우에 다음을 수행 하는 것이 좋습니다.  
  
-   포리스트의 모든 도메인 컨트롤러에 DNS 서버 서비스를 설치 합니다. 이 DNS 서버 중 하나를 사용할 수 없는 경우 내결함성을 제공 합니다. 이 이렇게 하면 도메인 컨트롤러는 이름 확인에 대 한 다른 DNS 서버에 의존할 필요가 없습니다. 모든 도메인 컨트롤러 구성이 uniform 때문에 관리 환경도 간단 합니다.  
  
-   Active Directory 포리스트에 대 한 DNS 영역을 호스트 하는 Active Directory 포리스트 루트 도메인 컨트롤러를 구성 합니다.  
  
-   Active Directory 도메인에 해당 하는 DNS 영역을 호스트 하려면 각 지역 도메인에 대 한 도메인 컨트롤러를 구성 합니다.  
  
-   Active Directory 포리스트 로케이터 레코드를 포함 하는 영역을 구성 (즉, _msdcs. *forestname* 영역) 포리스트 DNS 응용 프로그램 디렉터리 파티션을 사용 하 여 포리스트에 있는 모든 DNS 서버를 복제 합니다.  
  
    > [!NOTE]  
    > DNS 서버 서비스가 Active Directory 도메인 서비스 설치 마법사 (이 옵션을 권장)를 사용 하 여 설치 된 이전 작업을 모두 자동으로 수행 됩니다. 자세한 내용은 참조 [Windows Server 2008 포리스트 루트 도메인 배포](https://technet.microsoft.com/library/cc731174.aspx)합니다.  
  
    > [!NOTE]  
    > AD DS 포리스트 로케이터 레코드를 사용 하 여 서로 찾 및 클라이언트가 글로벌 카탈로그 서버를 찾을 수 있도록 하려면 복제 파트너 수 있도록 합니다. AD DS는 _msdcs에서 포리스트 로케이터 레코드를 저장합니다. *forestname* 영역입니다. 영역에 정보를 광범위 하 게 사용할 수 있어야 합니다, 때문에이 영역 포리스트 DNS 응용 프로그램 디렉터리 파티션을 사용 하 여 포리스트에 있는 모든 DNS 서버에 복제 됩니다.  
  
기존 DNS 구조는 그대로 남아 있습니다. 모든 서버 또는 영역을 이동할 필요가 없습니다. 기존 DNS 계층 구조에서 위임을 Active Directory 통합 DNS 영역을 만들려면 하기만 합니다.  
  
## <a name="creating-the-dns-client-configuration"></a>DNS 클라이언트 구성 만들기  
DNS 클라이언트 컴퓨터를 구성 하려면 AD DS 소유자에 대 한 DNS 클라이언트는 DNS 서버를 찾는 방법 및 구성표의 이름을 지정 하는 컴퓨터를 지정 해야 합니다. 다음 표에서 이러한 디자인 요소에 대 한 권장된 구성 하세요.  
  
|디자인 요소|Configuration|  
|------------------|-----------------|  
|컴퓨터 이름 지정|기본 명명 규칙을 사용 합니다. Windows 2000, Windows XP, Windows Server 2003, Windows Server 2008 또는 Windows Vista 기반 컴퓨터를 도메인에 가입 되 면 활성 이름과 정규화 된 도메인 이름 (FQDN) 컴퓨터의 호스트 이름을 구성 하는 자체 컴퓨터 할당 디렉터리 도메인입니다.|  
|클라이언트 확인자 구성|네트워크의 모든 DNS 서버를 가리키도록 클라이언트 컴퓨터를 구성 합니다.|  
  
> [!NOTE]  
> Active Directory 클라이언트와 도메인 컨트롤러는 하지 해당 이름에 대 한 권한이 있는 DNS 서버를 가리키는 경우에 해당 DNS 이름을 등록할 동적으로 수 있습니다.  
  
컴퓨터는 조직은 이전에 정적으로 등록 된 경우 컴퓨터 DNS 또는 조직에서 이전에 통합된 하는 동적 호스트 구성 프로토콜 (DHCP) 솔루션을를 배포 하는 경우에 다른 기존 DNS 이름이 있을 수 있습니다. 클라이언트 컴퓨터에 이미 등록된 된 DNS 이름이 도메인 가입 된 Windows Server 2008 AD DS로 업그레이드 되 면, 두 개의 서로 다른 이름을 갖게 됩니다.  
  
-   기존 DNS 이름  
  
-   새 정규화 된 도메인 이름 (FQDN)  
  
클라이언트 이름 중 하나에서 여전히 있을 수 있습니다. 모든 기존 DNS, DHCP 또는 DNS/DHCP 솔루션 통합된 그대로 유지 됩니다. 새 기본 이름은 자동으로 생성 되며 동적 업데이트를 사용 하 여 업데이트 됩니다. 이러한 자동으로 정리 됩니다 청소를 통해.  
  
Windows 2000, Windows Server 2003 또는 Windows Server 2008을 실행 하는 서버에 연결할 때 Kerberos 인증을 활용 하려는 경우 기본 이름을 사용 하 여 클라이언트 서버에 연결 되는지 확인 해야 합니다.  
  


