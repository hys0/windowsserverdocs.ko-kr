---
ms.assetid: 4f835b82-67b9-428c-b634-ce133cca5113
title: "AD DS 배포 전략 예 평가"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 4cac1e344cfed078927f2945048807d686deebd1
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="evaluating-ad-ds-deployment-strategy-examples"></a>AD DS 배포 전략 예 평가

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

가상 회사, Active Directory Domain Services (AD DS)의 환경에 배포 되는 금강의 다음 예를 것이 좋습니다. 도메인 4 개 Contoso 환경은 구성 됩니다. 숲 기능 수준 Windows Server 2003입니다. 다음 그림 Contoso 조직 현재 도메인 구조를 보여 줍니다.  
  
![AD DS 배포 전략](media/Evaluating-AD-DS-Deployment-Strategy-Examples/3dd79e00-48f8-4927-989c-c55a79caf1be.gif)  
  
기존 환경을 검토 한 후는 하 고 해당 배포 목표를 확인 Contoso 설정 다음 AD DS 배포 전략:  
  
-   Windows Server 2003 도메인 Windows Server 2008 도메인으로 업그레이드 합니다.  
  
-   Windows Server 2008로 도메인 및 숲 기능 수준 발생 시켜 고급 AD DS 기능을 사용 합니다.  
  
-   재구성 emea.concorp.contoso.con 도메인와 해당 도메인 통합 숲 내 africa.concorp.contoso.com 도메인.  
  
Windows Server 2008 숲 기능 수준을 발생 AD DS 새로운 기능을 최대한 활용 하는 Contoso 수 있게 합니다. 다음 그림에서는 같이 숲, 내 도메인 재구성 도메인 관리 하는 데 필요한 관리 양을 줄이는 됩니다.  
  
![AD DS 배포 전략](media/Evaluating-AD-DS-Deployment-Strategy-Examples/1c061755-413d-452d-b121-6910f8555327.gif)  
  


