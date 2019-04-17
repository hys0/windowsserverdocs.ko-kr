---
ms.assetid: 39c0126d-af5e-4dcb-88c1-aa38f888e973
title: "Active Directory 통합 DNS 영역"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 11940ddda320ea36bf8439afed91fcf6803f2fee
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="active-directory-integrated-dns-zones"></a>Active Directory 통합 DNS 영역

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

도메인 컨트롤러에서 실행 하는 도메인 DNS Name System () 서버 해당 영역 Active Directory Domain Services (AD DS)에 저장할 수 있습니다. 이런 방법으로 필요는 없습니다 복제 Active Directory를 사용 하 여 모든 영역 데이터를 자동으로 복제 일반 DNS 영역 전송을 사용 하는 별도 DNS 복제 토폴로지 구성할 수 있습니다. 이 DNS 배포 하는 과정을 간소화 하 고 다음과 같은 이점을 제공 합니다.  
  
-   여러 명의 마스터 DNS 복제 만들어집니다. 따라서 모든 도메인 컨트롤러 DNS 서버 서비스가 실행 되는 도메인의 업데이트 된 신뢰할 수 있는 도메인 이름에 대 한 Active Directory 통합 DNS 영역 기록할 수 있습니다. 별도 DNS 영역 전송 토폴로지 필요 하지 않습니다.  
  
-   동적 보안 업데이트는 지원 합니다. 보안 동적 업데이트 어떤 이름을 업데이트 하는 어떤 컴퓨터를 제어 하 고 기존 이름을 dns에서 덮어쓰지 무단으로 컴퓨터를 방지 하는 관리자를 허용 합니다.  
  
Windows Server 2008에서 active Directory 통합 DNS 응용 프로그램 파티션 영역 데이터를 저장합니다. (Active Directory와 Windows Server 2003 기반 DNS 통합에서 행동 변경 사항이 합니다.) 다음 DNS 특정 응용 프로그램 파티션 AD DS 설치 시 만들어집니다.  
  
-   라는 ForestDnsZones 숲 전체의 응용 디렉터리 파티션  
  
-   전체 도메인 응용 프로그램은 숲 속의 각 도메인에 대 한 파티션 DomainDnsZones 이라는  
  
AD DS 파티션을 응용 프로그램에서 DNS 정보를 저장 하는 방법에 대 한 자세한 내용은 참조는 [DNS 기술 참조](https://go.microsoft.com/fwlink/?LinkId=106636)합니다.  
  
> [!NOTE]  
> DNS Active Directory Domain Services 설치 마법사 (Dcpromo.exe) 실행 하는 경우 설치 하는 것이 좋습니다. 이 작업을 수행 하는 경우 마법사는 자동으로 DNS 영역 위임을 만듭니다. 자세한 내용은 참조 [Windows Server 2008 숲 루트 도메인 배포](https://technet.microsoft.com/library/cc731174.aspx)합니다.  
  


