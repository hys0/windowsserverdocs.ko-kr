---
ms.assetid: d590c90e-9adf-4305-b226-eb2a5743337b
title: AD DS 디자인 이해
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/07/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: c94f6ddd19e3178243545b0cc71f6f4c7bb4dbec
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59828794"
---
# <a name="understanding-ad-ds-design"></a>AD DS 디자인 이해

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

조직 확장 가능 하 고 안전 하며 관리 하기 쉬운 인프라를 만드는 동안 사용자 및 리소스 관리를 간소화 하기 위해 Windows Server의 Active Directory Domain Services (AD DS)를 사용할 수 있습니다. 분기 office, Microsoft Exchange Server를 다중 포리스트 환경 등 네트워크 인프라를 관리 하려면 AD DS를 사용할 수 있습니다.  
  
AD DS 배포 프로젝트를 포함 세 단계로: 설계 단계, 배포 단계 및 작업 단계는 합니다. 디자인 단계에서 설계 팀의 디렉터리 서비스를 사용 하는 조직 내에서 각 부서의 요구에 가장 부합 하는 AD DS 논리 구조에 대 한 디자인을 만듭니다. 디자인 승인 되 면 배포 팀 환경에서 디자인을 테스트 하 고 프로덕션 환경에서 디자인을 구현 합니다. 배포 팀에서 테스트가 수행 됩니다. 디자인 단계에 잠재적으로 영향을 이므로 디자인 및 배포를 겹치는 중간 작업 합니다. 배포가 완료 되 면 운영 팀은 디렉터리 서비스를 유지 관리를 담당 합니다.  
  
이 가이드에 표시 되는 Windows Server AD DS 디자인 및 배포 전략은 광범위 한 랩 및 파일럿 프로그램 테스트와 고객 환경에서 성공적으로 구현에 따라 하지만 AD DS 디자인을 사용자 지정 해야 할 수 있습니다 및 특정의 복잡 한 환경에 맞게 배포 합니다.
  
- 분기 office 환경에서 AD DS를 배포 하는 방법에 대 한 자세한 내용은 참조는 [읽기 전용 도메인 컨트롤러 (RODC) 분기 Office 계획 가이드](https://go.microsoft.com/fwlink/?LinkId=100207)합니다.  
- Exchange 환경에서 AD DS를 배포 하는 방법에 대 한 자세한 내용은 문서 참조 [Exchange 2007-Active Directory 계획](https://go.microsoft.com/fwlink/?LinkId=88904)합니다.  
- 다중 포리스트 환경에서 AD DS를 배포 하는 방법에 대 한 자세한 내용은 문서 참조 [Windows 2000 및 Windows Server 2003의 여러 포리스트 고려 사항](https://go.microsoft.com/fwlink/?LinkId=88905)합니다.  
