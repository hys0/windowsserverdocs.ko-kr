---
ms.assetid: 39c0126d-af5e-4dcb-88c1-aa38f888e973
title: Active Directory 통합 DNS 영역
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 5e0830944ec5d91dace52db337e89211ee362b98
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59873254"
---
# <a name="active-directory-integrated-dns-zones"></a>Active Directory 통합 DNS 영역

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

도메인 컨트롤러에서 실행 되는 도메인 이름 시스템 (DNS) 서버는 Active Directory Domain Services (AD DS)에서 해당 영역을 저장할 수 있습니다. 따라서에서 모든 영역 데이터는 Active Directory 복제를 사용 하 여 자동으로 복제 되므로 일반 DNS 영역 전송을 사용 하는 별도 DNS 복제 토폴로지를 구성 하는 데 필요한 아닙니다. 이 DNS를 배포 하는 과정을 간소화 하 고 다음과 같은 이점을 제공 합니다.  
  
-   여러 마스터가 DNS 복제에 대해 만들어집니다. 따라서 DNS 서버 서비스를 실행 하는 도메인의 모든 도메인 컨트롤러는 신뢰할 수 있는 도메인 이름에 대 한 Active Directory 통합 DNS 영역에 업데이트를 쓸 수 있습니다. 별도 DNS 영역 전송 토폴로지 필요 하지 않습니다.  
  
-   보안 동적 업데이트만 지원 됩니다. 보안 동적 업데이트 사용 하면 관리자가 컴퓨터에 있는 이름 업데이트를 제어 하 고 허가 되지 않은 컴퓨터에서 DNS의 기존 이름과 덮어쓰지 방지 합니다.  
  
Windows Server 2008의 active Directory 통합 DNS 응용 프로그램 디렉터리 파티션에 영역 데이터를 저장합니다. (Windows Server 2003 기반 DNS와 Active Directory 통합에서 동작 내용이 있습니다.) 다음과 같은 DNS 별 응용 프로그램 디렉터리 파티션이 AD DS 설치 중 생성 됩니다.  
  
-   포리스트 전체 응용 프로그램 디렉터리 파티션에, ForestDnsZones 호출  
  
-   포리스트의 각 도메인에 대해 도메인 수준의 응용 프로그램 디렉터리 파티션을 DomainDnsZones 라는  
  
AD DS 응용 프로그램 파티션의 DNS 정보를 저장 하는 방법에 대 한 자세한 내용은 참조는 [DNS 기술 참조](https://go.microsoft.com/fwlink/?LinkId=106636)합니다.  
  
> [!NOTE]  
> Active Directory 도메인 서비스 설치 마법사 (Dcpromo.exe)를 실행 하는 경우 DNS를 설치 하는 것이 좋습니다. 이 작업을 수행 하는 경우 마법사를 자동으로 DNS 영역 위임을 만듭니다. 자세한 내용은 참조 [Windows Server 2008 포리스트 루트 도메인 배포](https://technet.microsoft.com/library/cc731174.aspx)합니다.  
  


