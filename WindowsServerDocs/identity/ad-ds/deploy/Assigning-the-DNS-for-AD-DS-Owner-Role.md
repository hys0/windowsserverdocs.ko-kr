---
ms.assetid: 4163cf03-3bff-426c-9844-4cc2d7897d52
title: "DNS AD DS 소유자 역할 지정 하는 방법"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: e393cbf32aa5a13ff22044eabb8c575508baaf79
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="assigning-the-dns-for-ad-ds-owner-role"></a>DNS AD DS 소유자 역할 지정 하는 방법

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

숲 소유자는 시스템 DNS (도메인 이름)은 숲에 대 한 Active Directory 도메인 서비스 AD DS 소유자에 대 한 할당합니다. AD DS 소유자는 숲 속의 DNS 사용자 (또는 사람들)는 누구 일까요을 DNS 배포 감독 도메인 이름 적절 한 인터넷 기관으로 등록 된 광고 DS 인프라 하 고 있는지 확인 (필요한 경우).  
  
DNS AD DS 소유자에는 DNS 숲 AD DS 디자인에 대 한 담당 합니다. 조직에는 DNS 서버 서비스 현재 작동을 DNS 도메인 컨트롤러에서 실행 중인 DNS 서버를 숲 루트 DNS 이름을 위임 AD DS 소유자에 대 한 기존 DNS 서버 서비스에 대 한 DNS 디자이너 작동 합니다.  
  
숲에 대 한 소유자 AD DS DNS 연락처 DHCP Dynamic Host Configuration Protocol () 그룹과 조직의 DNS 그룹으로 유지 관리 하며 된 이러한 그룹 (있는 경우)는 숲 속의 각 도메인의 개별 DNS 소유자의 계획을 조정 합니다. 숲 DNS 소유자 DHCP 및 DNS 그룹 AD DS 디자인 프로세스에 대 한 DNS에 관련 된 각 그룹 DNS 디자인 계획의 인식 및 초기 입력을 제공할 수 있도록 보장 합니다.  
  


