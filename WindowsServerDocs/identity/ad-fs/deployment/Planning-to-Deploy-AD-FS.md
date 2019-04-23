---
ms.assetid: c87dc32d-ab33-44d2-a46f-f9f878b4e5b4
title: AD FS 배포 계획
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: ca9e53d7d98f3ae5e6b7b329e52d4979e8c10215
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59831694"
---
# <a name="planning-to-deploy-ad-fs"></a>AD FS 배포 계획

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012


사용자 환경에 대 한 정보를 수집 하 고 Active Directory Federation Services를 사용 하도록 결정 한 후 \(AD FS\) 의 지침에 따라 디자인 된 [Windows Server 2012의 AD FS 디자인 가이드](https://technet.microsoft.com/library/dd807036.aspx), 조직의 AD FS 디자인 배포 계획을 시작할 수 있습니다. 완료 된 디자인 및이 항목의 정보를 사용 하 여 조직에서 AD FS를 배포 하는 데는 작업을 확인할 수 있습니다.  
  
## <a name="reviewing-your-ad-fs-design"></a>AD FS 디자인 검토  
원래 AD FS를 생성 하는 디자인 팀에 대 한 디자인 조직을 실제로 구현할 배포 배포 팀은 디자인 팀과 함께 최종 디자인을 검토 하 고 있는지 확인 하는 배포 팀에서 다릅니다. 디자인에 대해 검토할 사항은 다음과 같습니다.  
  
-   회사 네트워크 또는 경계 네트워크에 페더레이션 서버를 배치할 최상의 실제 토폴로지를 결정하기 위한 디자인 팀의 전략. 배포 팀은 AD FS 디자인 가이드의 다음 항목을 검토 하 여이 주제에 대 한 설명서를 참조할 수 있습니다.  
  
    -   [AD FS 구성 데이터베이스의 역할](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)  
  
    -   [페더레이션 서버 배치 계획](https://technet.microsoft.com/library/dd807069.aspx)  
  
    -   [페더레이션 서버 프록시 배치 계획](https://technet.microsoft.com/library/dd807130.aspx)  
  
    디자인 팀은 페더레이션 서버 또는 페더레이션 프록시 배치를 배포 팀에 맡길 수 있습니다. 이 경우 배포 팀은 서버의 실제 토폴로지를 문서화하고 구현하는 역할을 담당합니다.  
  
-   문서화된 AD FS 디자인 범위 내에서 조직이 클레임 공급자, 신뢰 당사자 또는 둘 다로 지정된 비즈니스 이유. 배포 팀의 구성원을 AD FS를 배포 하는 이유는 이유 및 다른 회사 또는 조직을 이해 해야 페더레이션 파트너 관계에 참여 합니다. 배포 팀의 멤버에도 다른 회사 또는 조직에 대 한 존재 하는 제약 조건을 이해 \(하드웨어, 엑스트라넷 환경 없음 등 제한\) 는 어떤 방식으로든에서 디자인의 범위를 제한할 수 있습니다. 파트너 조직에 대한 자세한 내용은 [배포 계획](https://technet.microsoft.com/library/dd807083.aspx)을 참조하세요.  
  
디자인 한 후 팀과 배포 팀은 이러한 사안에 동의한, AD FS 디자인 배포를 진행할 수 있습니다. 자세한 내용은 [AD FS 디자인 계획 구현](Implementing-Your-AD-FS-Design-Plan.md)을 참조하세요.  
