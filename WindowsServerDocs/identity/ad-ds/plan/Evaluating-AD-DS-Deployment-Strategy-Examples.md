---
ms.assetid: 4f835b82-67b9-428c-b634-ce133cca5113
title: AD DS 배포 전략 예제 평가
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 169d0a55f9fb167390c13ac1c89f8d68427f318d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59842114"
---
# <a name="evaluating-ad-ds-deployment-strategy-examples"></a>AD DS 배포 전략 예제 평가

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

다음 예제에서는 가상의 회사 Active Directory 도메인 서비스 (AD DS) 해당 환경에 배포 되는 Contoso Pharmaceuticals의 것이 좋습니다. Contoso 환경 네 개의 도메인으로 구성 됩니다. 포리스트 기능 수준을 Windows Server 2003 됩니다. 다음 그림은 Contoso 조직에 대 한 현재 도메인 구조를 보여줍니다.  
  
![AD DS 배포 전략](media/Evaluating-AD-DS-Deployment-Strategy-Examples/3dd79e00-48f8-4927-989c-c55a79caf1be.gif)  
  
기존 환경을 검토 하는 이러한 배포 목표 식별 후 Contoso 다음 AD DS 배포 전략을 설정 합니다.  
  
-   Windows Server 2008 도메인에 Windows Server 2003 도메인을 업그레이드 합니다.  
  
-   Windows Server 2008 도메인 및 포리스트 기능 수준 올리기 하 여 고급 AD DS 기능을 사용 합니다.  
  
-   Emea.concorp.contoso.con 도메인과 해당 도메인을 통합 하기 위해 포리스트 내에서 africa.concorp.contoso.com 도메인을 재구성 합니다.  
  
Windows Server 2008 포리스트 기능 수준을 올리는 하면 Contoso의 새로운 AD DS 기능을 활용할 수 있습니다. 다음 그림에 나와 있는 것 처럼 포리스트 내의 도메인 구조 변경 도메인을 관리 하기 위해 필요한 관리 양이 줄어듭니다.  
  
![AD DS 배포 전략](media/Evaluating-AD-DS-Deployment-Strategy-Examples/1c061755-413d-452d-b121-6910f8555327.gif)  
  


