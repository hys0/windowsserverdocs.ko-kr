---
ms.assetid: 39c0126d-af5e-4dcb-88c1-aa38f888e973
title: Active Directory 통합 DNS 영역
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 5e9047fced5c89c1f2c9d5edaf1ff02536c2a709
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80822896"
---
# <a name="active-directory-integrated-dns-zones"></a>Active Directory 통합 DNS 영역

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

도메인 컨트롤러에서 실행 되는 DNS (domain Name System) 서버는 Active Directory Domain Services (AD DS)에 해당 영역을 저장할 수 있습니다. 이러한 방식으로 모든 영역 데이터는 Active Directory 복제를 통해 자동으로 복제 되므로 일반 DNS 영역 전송을 사용 하는 별도의 DNS 복제 토폴로지를 구성할 필요가 없습니다. 이렇게 하면 DNS 배포 프로세스를 간소화 하 고 다음과 같은 이점을 얻을 수가 있습니다.  
  
-   DNS 복제용으로 여러 마스터가 생성 됩니다. 따라서 DNS 서버 서비스를 실행 하는 도메인의 모든 도메인 컨트롤러는 권한이 있는 도메인 이름에 대 한 Active Directory 통합 DNS 영역에 대 한 업데이트를 작성할 수 있습니다. 별도 DNS 영역 전송 토폴로지가 필요 하지 않습니다.  
  
-   보안 동적 업데이트가 지원 됩니다. 보안 동적 업데이트를 통해 관리자는 이름을 업데이트 하는 컴퓨터를 제어 하 고 허가 되지 않은 컴퓨터에서 DNS의 기존 이름을 덮어쓰지 못하게 할 수 있습니다.  
  
Windows Server 2008의 Active Directory 통합 DNS는 응용 프로그램 디렉터리 파티션에 영역 데이터를 저장 합니다. Active Directory와 Windows Server 2003 기반 DNS 통합의 동작이 변경 되지 않습니다. 다음 DNS 관련 응용 프로그램 디렉터리 파티션은 AD DS 설치 하는 동안 만들어집니다.  
  
-   ForestDnsZones 라는 포리스트 전체 응용 프로그램 디렉터리 파티션입니다.  
  
-   DomainDnsZones 라는 포리스트의 각 도메인에 대 한 도메인 전체 응용 프로그램 디렉터리 파티션  
  
AD DS 응용 프로그램 파티션에 DNS 정보를 저장 하는 방법에 대 한 자세한 내용은 [Dns 기술 참조](https://go.microsoft.com/fwlink/?LinkId=106636)를 참조 하세요.  
  
> [!NOTE]  
> Active Directory Domain Services 설치 마법사 (Dcpromo.exe)를 실행할 때 DNS를 설치 하는 것이 좋습니다. 이렇게 하면 마법사에서 DNS 영역 위임을 자동으로 만듭니다. 자세한 내용은 참조 [Windows Server 2008 포리스트 루트 도메인 배포](https://technet.microsoft.com/library/cc731174.aspx)합니다.  
  


