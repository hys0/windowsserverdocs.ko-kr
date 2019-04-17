---
ms.assetid: f6e76ef0-2217-4cdb-980f-22a780a85ebb
title: "AD DS 디자인 요구 사항"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 17338cd00fecec098865095dd9613f62beb3a457
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="ad-ds-design-requirements"></a>AD DS 디자인 요구 사항

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

  
## <a name="designing-the-active-directory-logical-structure"></a>디자인 Active Directory 논리 구조  
Windows Server 2008 Active Directory Domain Services (AD DS)를 배포 하기 전에 대 한 계획 하 고 귀하의 환경에 대 한 논리 AD DS 구조 디자인 해야 합니다. AD DS 논리 구조 directory 개체 구성 되는 방식에 따라 결정 하 고 네트워크 계정과 공유 리소스를 관리 하는 데 효과적인 방법 제공 합니다. AD DS 논리 구조 디자인할 때 조직의 네트워크 인프라의 큰 부분을 정의 됩니다.  
  
AD DS 논리 구조 디자인을 조직 필요한 숲 수를 확인 하 고 디자인 도메인, 시스템 DNS (도메인 이름) infrastructure 및 조직 (Ou)을 만듭니다. 다음 그림에서는 논리 구조 디자인 프로세스를 보여 줍니다.  
  
![AD DS 디자인 요구 사항](media/AD-DS-Design-Requirements/d5cebae6-a752-4063-a98f-473799c251bd.gif)  
  
자세한 내용은 참조 [논리 구조 Windows Server 2008 AD DS 디자인](Designing-the-Logical-Structure.md)합니다.  
  
## <a name="designing-the-site-topology"></a>사이트 토폴로지 디자인  
AD DS 인프라에 대 한 논리 구조 디자인한 후 네트워크에 대 한 사이트 토폴로지를 디자인 해야 합니다. 사이트 토폴로지는 실제 네트워크 논리를 표시 합니다. 사이트 AD DS 각 사이트 사이트 링크와 지원 사이트 간 AD DS 복제 하는 사이트 링크 다리 내 AD DS 도메인 컨트롤러의 위치에 대 한 정보를 포함 합니다. 다음 그림에서는 사이트 토폴로지 디자인 프로세스를 보여 줍니다.  
  
![AD DS 디자인 요구 사항](media/AD-DS-Design-Requirements/d34d43c0-437f-47cb-9b64-09c0f9ce6479.gif)  
  
자세한 내용은 참조 [Windows Server 2008 사이트 토폴로지 AD DS 디자인](Designing-the-Site-Topology.md)합니다.  
  
## <a name="planning-domain-controller-capacity"></a>도메인 컨트롤러 용량 계획  
효율적인 AD DS 성능을 보장 하기 위해 도메인 컨트롤러 각 사이트에 대 한 적절 한 수를 확인 하 고 Windows Server 2008 위한 하드웨어 요구 사항에 맞는지 확인 해야 합니다. 주의 용량 도메인 컨트롤러에 대 한 계획 저하 도메인 컨트롤러 성능 및 응용 프로그램 응답 시간 발생할 수 있는 하드웨어 요구 사항을 간과 해서는 하지 않으면 설치할 수 있도록 보장 합니다. 다음은 도메인 컨트롤러 용량 계획 하는 과정입니다.  
  
![AD DS 디자인 요구 사항](media/AD-DS-Design-Requirements/fff6ef22-5c7b-4478-ad76-42b296dcf769.gif)  
  
## <a name="enabling-windows-server-2008-advanced-ad-ds-features"></a>Windows Server 2008 활성화 고급 AD DS 기능  
Windows Server 2008 AD DS 귀하의 환경에 도메인 또는 숲 기능 수준 발생 시켜 고급 기능을 소개 하기 사용할 수 있습니다. 도메인 또는 숲 속의 모든 도메인 컨트롤러 Windows Server 2008 실행 중인 경우 Windows Server 2008 기능 수준을 발생 시킬 수 있습니다.  
  
자세한 내용은 참조 [AD DS 하기 위한 고급 기능을 활성화](../../ad-ds/plan/Enabling-Advanced-Features-for-AD-DS.md)합니다.  
  


