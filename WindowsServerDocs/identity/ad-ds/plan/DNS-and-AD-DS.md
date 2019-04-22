---
ms.assetid: c32606b4-2ee2-4df3-a704-8ac6723e188f
title: DNS 및 AD DS
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/08/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: f6d75a78119d76a0f8380967292b1d0abc720597
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59813144"
---
# <a name="dns-and-ad-ds"></a>DNS 및 AD DS

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Active Directory Domain Services (AD DS)를 사용 하 여 도메인 이름 시스템 (DNS) 이름 확인 서비스 수 있도록 도메인 컨트롤러 및 도메인 컨트롤러를 찾는 클라이언트에 대해 호스트 하는 디렉터리 서비스가 서로 통신할 수 있습니다.  
  
AD DS에 기존 DNS 네임 스페이스에 Active Directory 네임 스페이스의 쉽게 통합할 수 있습니다. 기능와 같은 Active Directory 통합 DNS 영역 쉽게 보조 영역을 설정 하는 필요성을 제거 하 여 DNS를 배포 하 고 영역 전송을 구성 합니다.  
  
DNS에서 AD DS를 지 원하는 방법에 대 한 자세한 내용은 [Active Directory 기술 참조에 대 한 DNS 지원](https://go.microsoft.com/fwlink/?LinkID=48147)합니다.  
  
> [!NOTE]  
> AD DS 도메인 이름을 클라이언트를 사용 하는 주 DNS 접미사에서와 다른 비연속 네임 스페이스를 구현 하는 경우 DNS 사용 하 여 AD DS 통합은 복잡 합니다. 자세한 내용은 [비연속 Namespace](../../ad-ds/plan/../../ad-ds/plan/Disjoint-Namespace.md)합니다.  
  
## <a name="in-this-section"></a>단원 내용  
  
- [도메인 컨트롤러 위치](../../ad-ds/plan/Domain-Controller-Location.md)  
- [Active Directory 통합 DNS 영역](../../ad-ds/plan/Active-Directory-Integrated-DNS-Zones.md)  
- [컴퓨터 이름 지정](../../ad-ds/plan/Computer-Naming.md)  
- [비연속 Namespace](../../ad-ds/plan/../../ad-ds/plan/Disjoint-Namespace.md)  
