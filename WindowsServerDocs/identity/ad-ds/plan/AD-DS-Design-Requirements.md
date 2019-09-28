---
ms.assetid: f6e76ef0-2217-4cdb-980f-22a780a85ebb
title: AD DS 디자인 요구 사항
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: cb9d4c04bc3fc7bb534e75b80f0947bd225b7b85
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71368963"
---
# <a name="ad-ds-design-requirements"></a>AD DS 디자인 요구 사항

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

  
## <a name="designing-the-active-directory-logical-structure"></a>Active Directory 논리 구조 디자인  
Windows Server 2008 Active Directory 도메인 서비스 (AD DS)를 배포 하기 전에 계획 하 고 사용자 환경에 AD DS 논리 구조를 디자인 해야 합니다. 네트워크 계정 및 공유 리소스를 관리 하는 효율적인 방법을 제공 및 AD DS 논리 구조의 디렉터리 개체 구성 방법을 결정 합니다. AD DS 논리 구조를 디자인 하는 경우 조직의 네트워크 인프라의 중요 한 부분을 정의 합니다.  
  
AD DS 논리 구조를 디자인 하려면 조직에 필요한 포리스트 수를 확인 하 고 도메인, 도메인 이름 시스템 (DNS) 인프라 및 조직 구성 단위 (Ou)에 대 한 디자인을 만듭니다. 다음 그림에서는 논리 구조를 디자인 하기 위한 프로세스를 보여 줍니다.  
  
![AD DS 디자인 요구 사항](media/AD-DS-Design-Requirements/d5cebae6-a752-4063-a98f-473799c251bd.gif)  
  
자세한 내용은 참조 [는 논리적 구조에 대 한 Windows Server 2008 AD DS 디자인](Designing-the-Logical-Structure.md)합니다.  
  
## <a name="designing-the-site-topology"></a>사이트 토폴로지 디자인  
AD DS 인프라에 대 한 논리 구조를 디자인 한 후에 네트워크에 대 한 사이트 토폴로지를 디자인 해야 합니다. 사이트 토폴로지는 실제 네트워크의 논리적 표현입니다. AD DS 사이트의 경우 각 사이트 및 사이트 링크 및 사이트 간 AD DS 복제를 지 원하는 사이트 링크 브리지 내에서 AD DS 도메인 컨트롤러의 위치에 대 한 정보를 포함 합니다. 다음 그림에서는 사이트 토폴로지 디자인 프로세스를 보여 줍니다.  
  
![AD DS 디자인 요구 사항](media/AD-DS-Design-Requirements/d34d43c0-437f-47cb-9b64-09c0f9ce6479.gif)  
  
자세한 내용은 참조 [는 사이트 토폴로지에 대 한 Windows Server 2008 AD DS 디자인](Designing-the-Site-Topology.md)합니다.  
  
## <a name="planning-domain-controller-capacity"></a>도메인 컨트롤러 용량 계획  
효율적인 AD DS 성능을 보장 하기 위해 각 사이트에 대 한 도메인 컨트롤러의 적절 한 수를 확인 하 고 Windows Server 2008에 대 한 하드웨어 요구 사항을 맞는지 확인 해야 합니다. 신중 하 게 용량 도메인 컨트롤러에 대 한 계획 하면 인해 도메인 컨트롤러 성능 및 응용 프로그램 응답 시간을 일으킬 수 있는 하드웨어 요구 사항의 과소 평가 하지 마십시오. 다음 그림에서는 도메인 컨트롤러 용량 계획 프로세스를 보여 줍니다.  
  
![AD DS 디자인 요구 사항](media/AD-DS-Design-Requirements/fff6ef22-5c7b-4478-ad76-42b296dcf769.gif)  
  
## <a name="enabling-windows-server-2008-advanced-ad-ds-features"></a>Windows Server 2008을 사용 하도록 설정 하는 것 고급 AD DS 기능  
Windows Server 2008 AD DS 도메인 또는 포리스트 기능 수준을 올리는 하 여 환경에 고급 기능을 도입을 사용할 수 있습니다. 도메인 또는 포리스트의 모든 도메인 컨트롤러는 Windows Server 2008을 실행 하는 경우에 기능 수준을 Windows Server 2008을 발생 시킬 수 있습니다.  
  
자세한 내용은 참조 [AD DS에 대 한 고급 기능을 사용 하도록 설정](../../ad-ds/plan/Enabling-Advanced-Features-for-AD-DS.md)합니다.  
  


