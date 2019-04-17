---
ms.assetid: 4981b32f-741e-4afc-8734-26a8533ac530
title: "AD DS 기존 DNS 인프라에 통합"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: ab8d92a237a6d1fb623d9f4bb7dcc88561edf742
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="integrating-ad-ds-into-an-existing-dns-infrastructure"></a>AD DS 기존 DNS 인프라에 통합

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

조직에는 기존 시스템 DNS (도메인 이름) 서버 서비스 있는, Active Directory Domain Services (AD DS) 소유자 DNS AD DS 기존 인프라에 통합 하 고 조직에 대 한 DNS 소유자와 작업 해야 합니다. 이 DNS 서버를 만들고 DNS 클라이언트 구성 포함 됩니다.  
  
## <a name="creating-a-dns-server-configuration"></a>DNS 서버 구성 만들기  
AD DS 기존 DNS 네임 스페이스를 통합 하는 경우 다음을 수행 하는 것이 좋습니다.  
  
-   DNS 서버 서비스는 숲 속의 모든 도메인 컨트롤러에 설치 합니다. DNS 서버가 중 하나를 사용할 수 없는 경우 결함 허용을 제공 합니다. 이런 방법으로 도메인 컨트롤러 이름 확인을 위해 다른 DNS 서버에 의존 필요가 없습니다. 모든 도메인 컨트롤러 uniform 구성 하므로 관리 환경도 간단 합니다.  
  
-   Active Directory 숲 루트 도메인 컨트롤러 개최 된 Active Directory 숲에서 DNS 영역을 구성 합니다.  
  
-   도메인 컨트롤러 각 지역 도메인 개최 된 Active Directory 도메인에 해당 하는 DNS 영역에 대 한 구성 합니다.  
  
-   구성 Active Directory 숲 전체 locator 레코드를 포함 하는 영역 (즉, _msdcs.* forestname* 영역) DNS 응용 프로그램 숲 전체 파티션을 사용 하 여 모든 DNS 서버가 숲 속의 복제할 합니다.  
  
    > [!NOTE]  
    > DNS 서버 서비스 (이 옵션 권장) Active Directory Domain Services 설치 마법사를 통해 설치 된 경우 이전 모든 작업 자동으로 수행 됩니다. 자세한 내용은 참조 [Windows Server 2008 숲 루트 도메인 배포](https://technet.microsoft.com/library/cc731174.aspx)합니다.  
  
    > [!NOTE]  
    > AD DS 숲 전체 locator 레코드를 사용 하 여 복제 파트너 클라이언트가 드 서버를 찾을 수 있도록 하 고 서로 찾을 수 있도록 합니다. AD DS _msdcs 숲 전체 locator 기록을 저장합니다. *forestname* 영역 합니다. 영역에 있는 정보 광범위 하 게 사용할 수 있는 해야을 하기 때문에이 영역 DNS 응용 프로그램 숲 전체 파티션을 사용 하 여 모든 DNS 서버에 숲 복제 됩니다.  
  
기존 DNS 구조 그대로 유지 됩니다. 서버 또는 영역 이동 필요가 없습니다. 간단 하 게 여 기존 DNS 계층에서 DNS Active Directory 통합 영역에 위임 만들기 해야 합니다.  
  
## <a name="creating-the-dns-client-configuration"></a>DNS 클라이언트 구성 만들기  
DNS 클라이언트 컴퓨터에서 구성, AD DS 소유자 DNS 컴퓨터 구성표 및 클라이언트 DNS 서버를 찾는 것은 어떻게 명명 지정 해야 합니다. 다음 표에서 이러한 디자인 요소에 대 한 권장된 구성 합니다.  
  
|디자인 요소|구성|  
|------------------|-----------------|  
|컴퓨터 이름 지정|기본 이름 지정을 사용 합니다. Windows 2000, Windows XP, Windows Server 2003, 경우 Windows Server 2008 또는 Windows Vista 기반 컴퓨터가 도메인에 가입으로 컴퓨터의 호스트 이름을 구성 하는 정식된 도메인 이름 (FQDN) 및 Active Directory 도메인 이름 자체 컴퓨터 지정 됩니다.|  
|클라이언트 이름 확인자 구성|네트워크의 모든 DNS 서버를 가리키도록 클라이언트 컴퓨터를 구성 합니다.|  
  
> [!NOTE]  
> Active Directory 클라이언트 및 도메인 컨트롤러 이름에 대 한 권한이 DNS 서버를 가리키고 하지 않을 경우에 DNS 이름으로 등록 동적으로 수 있습니다.  
  
컴퓨터를 등록 한 경우 조직의 이전에 정적 컴퓨터 DNS 또는 조직 이전에 통합된 DHCP(Dynamic Host Configuration Protocol) (DHCP) 솔루션을 배포 하는 경우 다른 기존 DNS 이름이 있을 수 있습니다. 클라이언트 컴퓨터 이미 등록된 DNS 이름을 가입 된 도메인 Windows Server 2008 AD DS로 업그레이드할 때을 두 가지 이름 갖게 됩니다.  
  
-   기존 DNS 이름  
  
-   새로운 정식된 도메인 이름 (FQDN)  
  
클라이언트 어느 이름으로 여전히 있을 수 있습니다. 모든 기존 DNS, DHCP 또는 통합된 DNS/DHCP 솔루션 그대로 유지 됩니다. 새 주요 이름은 자동으로 생성를 동적 업데이트를 통해 업데이트 됩니다. 이러한은 자동으로 정리 청소를 사용 하 여.  
  
Windows 2000, Windows Server 2003, 또는 Windows Server 2008 실행 하는 서버에 연결할 때 Kerberos 인증 활용 하도록 하려는 경우 기본 이름을 사용 하 여 클라이언트는 서버에 연결 되어 있는지 확인 해야 합니다.  
  


