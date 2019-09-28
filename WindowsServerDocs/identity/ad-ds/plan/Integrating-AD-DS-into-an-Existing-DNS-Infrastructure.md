---
ms.assetid: 4981b32f-741e-4afc-8734-26a8533ac530
title: 기존 DNS 인프라에 AD DS 통합
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: f4bb480be4696f15f0a63c20ab47042264584d2c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402555"
---
# <a name="integrating-ad-ds-into-an-existing-dns-infrastructure"></a>기존 DNS 인프라에 AD DS 통합

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

조직에 기존 DNS (Domain Name System) 서버 서비스가 이미 있는 경우 AD DS를 기존 인프라에 통합 하려면 AD DS (Active Directory Domain Services DNS) 소유자가 조직에 대 한 DNS 소유자와 작업 해야 합니다. 여기에는 DNS 서버 및 DNS 클라이언트 구성이 생성 됩니다.  
  
## <a name="creating-a-dns-server-configuration"></a>DNS 서버 구성 만들기  
기존 DNS 네임 스페이스와 AD DS를 통합 하는 경우 다음을 수행 하는 것이 좋습니다.  
  
-   포리스트의 모든 도메인 컨트롤러에 DNS 서버 서비스를 설치 합니다. DNS 서버 중 하나를 사용할 수 없는 경우 내결함성을 제공 합니다. 이러한 방식으로 도메인 컨트롤러는 이름 확인을 위해 다른 DNS 서버에 의존할 필요가 없습니다. 또한 모든 도메인 컨트롤러에 균일 한 구성이 있으므로 관리 환경을 단순화 합니다.  
  
-   Active Directory 포리스트에 대 한 DNS 영역을 호스팅하도록 Active Directory 포리스트 루트 도메인 컨트롤러를 구성 합니다.  
  
-   각 지역 도메인에 대 한 도메인 컨트롤러를 구성 하 여 해당 Active Directory 도메인에 해당 하는 DNS 영역을 호스트 합니다.  
  
-   Active Directory 포리스트 차원의 로케이터 레코드 (즉, _msdcs)가 포함 된 영역을 구성 합니다. *forestname* 영역)을 사용 하 여 포리스트의 모든 dns 서버에 복제할 수 있습니다.  
  
    > [!NOTE]  
    > Active Directory Domain Services 설치 마법사를 사용 하 여 DNS 서버 서비스를 설치 하는 경우 (이 옵션을 사용 하는 것이 좋습니다.) 이전 태스크가 모두 자동으로 수행 됩니다. 자세한 내용은 참조 [Windows Server 2008 포리스트 루트 도메인 배포](https://technet.microsoft.com/library/cc731174.aspx)합니다.  
  
    > [!NOTE]  
    > AD DS는 포리스트 차원의 로케이터 레코드를 사용 하 여 복제 파트너가 서로를 찾고 클라이언트에서 글로벌 카탈로그 서버를 찾을 수 있도록 합니다. AD DS은 포리스트 차원의 로케이터 레코드를 _msdcs에 저장 합니다. *forestname* 영역. 영역의 정보는 광범위 하 게 사용할 수 있어야 하므로이 영역은 포리스트 전체 DNS 응용 프로그램 디렉터리 파티션을 통해 포리스트의 모든 DNS 서버에 복제 됩니다.  
  
기존 DNS 구조는 그대로 유지 됩니다. 서버 또는 영역을 이동할 필요는 없습니다. 기존 DNS 계층에서 Active Directory 통합 DNS 영역에 대 한 위임을 만들어야 합니다.  
  
## <a name="creating-the-dns-client-configuration"></a>DNS 클라이언트 구성 만들기  
클라이언트 컴퓨터에서 DNS를 구성 하려면 AD DS 소유자의 DNS에서 컴퓨터 명명 체계와 클라이언트에서 DNS 서버를 찾는 방법을 지정 해야 합니다. 다음 표에서는 이러한 디자인 요소에 권장 되는 구성을 보여 줍니다.  
  
|디자인 요소|Configuration|  
|------------------|-----------------|  
|컴퓨터 이름 지정|기본 이름 지정을 사용 합니다. Windows 2000, Windows XP, Windows Server 2003, Windows Server 2008 또는 Windows Vista 기반 컴퓨터가 도메인에 가입 하면 컴퓨터에서 컴퓨터의 호스트 이름과 활성 이름을 구성 하는 FQDN (정규화 된 도메인 이름)을 할당 합니다. 디렉터리 도메인입니다.|  
|클라이언트 확인자 구성|네트워크의 모든 DNS 서버를 가리키도록 클라이언트 컴퓨터를 구성 합니다.|  
  
> [!NOTE]  
> Active Directory 클라이언트와 도메인 컨트롤러는 해당 이름에 대 한 권한이 있는 DNS 서버를 가리키지 않는 경우에도 해당 DNS 이름을 동적으로 등록할 수 있습니다.  
  
이전에 조직에서 DNS에 컴퓨터를 정적으로 등록 했거나 조직에서 이전에 통합 된 DHCP (Dynamic Host Configuration Protocol) 솔루션을 배포한 경우 컴퓨터에 다른 기존 DNS 이름이 있을 수 있습니다. 클라이언트 컴퓨터에 이미 등록 된 DNS 이름이 있는 경우 해당 DNS가 가입 된 도메인은 Windows Server 2008 AD DS로 업그레이드 되 고 두 가지 다른 이름을 갖게 됩니다.  
  
-   기존 DNS 이름  
  
-   새 FQDN (정규화 된 도메인 이름)  
  
클라이언트는 어떤 이름으로도 찾을 수 있습니다. 모든 기존 DNS, DHCP 또는 통합 된 DNS/DHCP 솔루션은 그대로 유지 됩니다. 새 기본 이름은 동적 업데이트를 통해 자동으로 생성 되 고 업데이트 됩니다. 청소를 통해 자동으로 정리 됩니다.  
  
Windows 2000, Windows Server 2003 또는 Windows Server 2008를 실행 하는 서버에 연결할 때 Kerberos 인증을 사용 하려면 클라이언트에서 기본 이름을 사용 하 여 서버에 연결 하도록 해야 합니다.  
  


