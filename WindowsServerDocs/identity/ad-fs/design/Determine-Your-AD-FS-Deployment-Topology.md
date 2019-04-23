---
ms.assetid: f67b0bc9-e5af-4891-9da0-d9be539af42d
title: AD FS 배포 토폴로지 결정
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 3300c16be6d516d7ec0bf4d0c3a025e59e6126b6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59834524"
---
# <a name="determine-your-ad-fs-deployment-topology"></a>AD FS 배포 토폴로지 결정

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Active Directory Federation Services의 배포 계획의 첫 번째 단계 \(AD FS\) single sign에 맞게 올바른 배포 토폴로지를 결정 하는 것\-온 \(SSO\) 요구에 조직입니다. 이 섹션의에서 항목에서는 AD FS와 함께 사용할 수 있는 여러 가지 배포 토폴로지를 설명 합니다. 또한 특정 비즈니스 요구 사항에 가장 적합한 토폴로지를 선택할 수 있도록 각 배포 토폴로지와 연관된 이점 및 제한 사항을 설명합니다.  
  
이 배포 토폴로지 항목을 계속 읽기 전에 먼저 다음 표에 나와 있는 작업을 순서대로 완료하는 것이 좋습니다.  
  
|권장 작업|설명|참조|  
|--------------------|---------------|-------------|  
|AD FS 데이터가 저장 되 고 페더레이션 서버 팜의 다른 페더레이션 서버에 복제 되는 방법을 검토 합니다.|AD FS 구성 데이터베이스에 저장되는 기본 데이터의 용도 및 이러한 데이터에 사용할 수 있는 복제 방법을 이해합니다. 이 항목에서는 구성 데이터베이스의 개념을 소개하고 두 가지 데이터베이스 유형, 즉 Windows 내부 데이터베이스 \(WID\) 및 Microsoft SQL Server입니다.|[AD FS 구성 데이터베이스의 역할](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)|  
|조직에 배포할 AD FS 구성 데이터베이스의 유형 선택|WID 또는 SQL Server를 AD FS 구성 데이터베이스로 사용하는 것과 연관된 여러 가지 이점 및 제한 사항을 지원되는 다양한 응용 프로그램 시나리오와 함께 검토합니다.|[AD FS 배포 토폴로지 고려 사항](AD-FS-Deployment-Topology-Considerations.md)|  
  
> [!NOTE]  
> 기본 중복성, 부하 분산 및 페더레이션 서비스의 크기를 조정 하는 옵션을 구현 하 \(필요한 경우\), 모든 프로덕션 환경에 페더레이션 서버 팜 당 두 개 이상의 페더레이션 서버를 배포 하는 것이 좋습니다 에 관계 없이 사용 하 여 데이터베이스의 형식입니다.  
  
위 표를 검토했으면 이 섹션의 다음 항목을 계속 검토합니다.  
  
-   [WID를 사용 하 여 독립 실행형 페더레이션 서버](Stand-Alone-Federation-Server-Using-WID.md)  
  
-   [WID를 사용 하 여 페더레이션 서버 팜](Federation-Server-Farm-Using-WID-2012.md)  
  
-   [WID와 프록시를 사용 하 여 페더레이션 서버 팜](Federation-Server-Farm-Using-WID-and-Proxies-2012.md)  
  
-   [SQL Server를 사용 하 여 페더레이션 서버 팜](Federation-Server-Farm-Using-SQL-Server-2012.md)  
  
AD FS 배포 토폴로지를 선택 하면를 마친 후 항목을 검토 하는 것이 좋습니다 [AD FS 서버 용량 계획](Planning-for-AD-FS-Server-Capacity.md) 이 토폴로지를 지원 하기 위해 배포 해야 하는 서버의 권장 되는 수를 결정 합니다.  
  
## <a name="see-also"></a>관련 항목
[Windows Server 2012의에서 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012.md)

