---
ms.assetid: c87dc32d-ab33-44d2-a46f-f9f878b4e5b4
title: "ADFS 배포를 계획 하"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: ca9e53d7d98f3ae5e6b7b329e52d4979e8c10215
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="planning-to-deploy-ad-fs"></a>ADFS 배포를 계획 하

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012


귀하의 환경에 대 한 정보를 수집 하 고 지침에 따라 결정 Active Directory Federation Services \(AD FS\) 디자인에 대 한 후는 [Windows Server 2012에서 광고 FS 디자인 가이드](https://technet.microsoft.com/library/dd807036.aspx), 조직의 ADFS 디자인 배포를 계획을 시작할 수 있습니다. 완성 된 디자인와이 항목의 정보를 ADFS 조직에서 배포 하기 위해 수행 되는 작업을 확인할 수 있습니다.  
  
## <a name="reviewing-your-ad-fs-design"></a>ADFS 디자인을 검토  
원래 ADFS 생성 하는 디자인 팀 디자인에 대 한 경우 조직의 배포 팀 디자인 팀과 최종 디자인을 검토 하 않도록을 배포 구현 실제로 하는 배포 팀과에서 다릅니다. 디자인에 대 한 다음 포인트 검토 합니다.  
  
-   회사 네트워크 또는 주변 네트워크 federation 서버의 위치에 대 한 최상의 물리적 토폴로지 확인 하려면 디자인 팀의 전략 합니다. 배포 팀 수 AD FS 디자인 가이드에 다음 항목을 검토 하 여이 주제에 대 한 설명서를 참조 하세요.  
  
    -   [AD FS 구성 데이터베이스의 역할](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)  
  
    -   [Federation 서버 배치 계획](https://technet.microsoft.com/library/dd807069.aspx)  
  
    -   [Federation 서버 프록시 배치 계획](https://technet.microsoft.com/library/dd807130.aspx)  
  
    이 디자인 팀 federation 서버 또는 federation 서버 프록시 배치 배포 팀의 주제를 남길 수 있습니다. 배포 팀은 문서화 및 서버 실제 토폴로지에 구현 담당 합니다.  
  
-   비즈니스 이유로 클레임 공급자, 당사자, 또는 문서화 ADFS 디자인 범위 내에서 둘 다로 조직의 지정 합니다. 배포 팀의 구성원을 ADFS 배포 되는 이유는 이유 및 다른 회사 또는 조직의 근황 이해 federation 간 산학 협동에 참여 합니다. 배포 팀의 구성원 다른 회사 또는 조직에 대 한 제한을 이해 하는 \ (제한 된 하드웨어, 없음 익스트라넷 환경 및 니 forth\) 하는 어떤 식으로든에서 디자인 범위 제한 될 수 있습니다. 파트너 조직에 대 한 자세한 내용은 참조 [배포를 계획](https://technet.microsoft.com/library/dd807083.aspx)합니다.  
  
후 디자인 팀과 배포 팀에 동의 이러한 문제를 ADFS 디자인 배포 진행할 수 있습니다. 자세한 내용은 참조 [AD FS 디자인 계획 구현](Implementing-Your-AD-FS-Design-Plan.md)합니다.  
