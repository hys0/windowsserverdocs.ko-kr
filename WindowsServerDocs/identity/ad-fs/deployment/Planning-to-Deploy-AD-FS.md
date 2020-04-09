---
ms.assetid: c87dc32d-ab33-44d2-a46f-f9f878b4e5b4
title: AD FS 배포 계획
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 3cc26807d43f8a041647045af0074fd538c395a4
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855326"
---
# <a name="planning-to-deploy-ad-fs"></a>AD FS 배포 계획


사용자 환경에 대 한 정보를 수집 하 고 [Windows Server 2012의 AD FS 디자인 가이드](https://technet.microsoft.com/library/dd807036.aspx)에 있는 지침에 따라\) 디자인을 AD FS \(Active Directory Federation Services을 결정 한 후에는 조직의 AD FS 디자인 배포 계획을 시작할 수 있습니다. 이 항목의 완료 된 디자인과 정보를 사용 하 여 조직에 AD FS를 배포 하기 위해 수행할 작업을 결정할 수 있습니다.  
  
## <a name="reviewing-your-ad-fs-design"></a>AD FS 디자인 검토  
조직에 대해 원래 AD FS 디자인을 생성 한 디자인 팀이 배포를 실제로 구현할 배포 팀과 다른 경우 배포 팀은 디자인 팀과 함께 최종 디자인을 검토 해야 합니다. 디자인에 대해 검토할 사항은 다음과 같습니다.  
  
-   회사 네트워크 또는 경계 네트워크에 페더레이션 서버를 배치할 최상의 실제 토폴로지를 결정하기 위한 디자인 팀의 전략. 배포 팀은 AD FS 디자인 가이드에서 다음 항목을 검토 하 여이 주제에 대 한 설명서를 참조할 수 있습니다.  
  
    -   [AD FS 구성 데이터베이스의 역할](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)  
  
    -   [페더레이션 서버 배치 계획](https://technet.microsoft.com/library/dd807069.aspx)  
  
    -   [페더레이션 서버 프록시 배치 계획](https://technet.microsoft.com/library/dd807130.aspx)  
  
    디자인 팀은 페더레이션 서버 또는 페더레이션 프록시 배치를 배포 팀에 맡길 수 있습니다. 이 경우 배포 팀은 서버의 실제 토폴로지를 문서화하고 구현하는 역할을 담당합니다.  
  
-   문서화된 AD FS 디자인 범위 내에서 조직이 클레임 공급자, 신뢰 당사자 또는 둘 다로 지정된 비즈니스 이유. 배포 팀의 구성원이 AD FS를 배포 하는 이유와 페더레이션 파트너 관계에 참여 하는 다른 회사나 조직을 이해 해야 합니다. 또한 배포 팀의 구성원은 다른 회사 또는 조직에 존재 하는 제약 조건 (제한 된 하드웨어 \(, 엑스트라넷 환경 없음 등)을 이해 하\) 고 다른 방식으로 디자인 범위를 제한할 수 있습니다. 파트너 조직에 대한 자세한 내용은 [배포 계획](https://technet.microsoft.com/library/dd807083.aspx)을 참조하세요.  
  
디자인 팀과 배포 팀이 이러한 문제에 동의 하면 AD FS 설계 배포를 진행할 수 있습니다. 자세한 내용은 [AD FS 디자인 계획 구현](Implementing-Your-AD-FS-Design-Plan.md)을 참조하세요.  
