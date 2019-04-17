---
ms.assetid: d590c90e-9adf-4305-b226-eb2a5743337b
title: "이해 AD DS 디자인"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 09afe3d19add87327d05bfafba6e0492a278b968
ms.sourcegitcommit: 1c3e6375b2e8eb01cfd299d0e9478fee46905c99
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/27/2018
---
# <a name="understanding-ad-ds-design"></a>이해 AD DS 디자인

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

조직에서는 관리를 간소화 사용자 및 리소스 만드는 동안 Windows Server의 Active Directory Domain Services (AD DS)를 사용할 수 있습니다. 인프라 확장 안전 하 고 관리할 수 있습니다. AD DS 지점, Microsoft Exchange Server 여러 숲 환경 등 네트워크 인프라를 관리 하려면 사용할 수 있습니다.  
  
AD DS 배포 프로젝트 과정은: 디자인 단계는, 한 배포 및 작업 단계가 합니다. 디자인 단계 중 디자인 팀의 각 나누기 디렉터리 서비스를 사용 하는 조직에서 요구에 가장 잘 맞는 AD DS 논리 구조 디자인을 만듭니다. 디자인 승인 되 면 배포 팀 환경에서 디자인을 테스트 하 고 프로덕션 환경에서 디자인을 구현 합니다. 테스트는 수행 배포 팀에서 잠재적으로 설계 단계에 영향을 하기 때문에 겹치는 디자인 및 배포 되는 중간 활동 합니다. 배포 완료 되 면 운영 팀은 디렉터리 서비스를 유지 해야 합니다.  
  
이 가이드에 표시 되는 Windows Server AD DS 디자인 및 배포 전략은 광범위 한 랩 및 시험 프로그램을 테스트 성공적인 구현 고객이 환경에 따라 달라, 있지만 해야 할 수 있습니다. AD DS 디자인 및 배포 복잡 하 고 특정 환경에 맞게 사용자 지정 합니다.  
  
-   AD DS 지점 환경에 배포에 대 한 자세한 내용은 참조는 Read-Only 도메인 컨트롤러 (RODC) 지점 계획 가이드 ([https://go.microsoft.com/fwlink/?LinkId=100207](https://go.microsoft.com/fwlink/?LinkId=100207)).  
  
-   Exchange 환경에서 AD DS 배포에 대 한 자세한 내용은 참조 Exchange 2007-계획 Active Directory ([https://go.microsoft.com/fwlink/?LinkId=88904](https://go.microsoft.com/fwlink/?LinkId=88904)).  
  
-   AD DS 여러 숲 환경에 배포에 대 한 자세한 내용은 참조 Windows 2000 및 Windows Server 2003 여러 숲 고려 ([https://go.microsoft.com/fwlink/?LinkId=88905](https://go.microsoft.com/fwlink/?LinkId=88905)).  
  


