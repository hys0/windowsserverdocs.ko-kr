---
ms.assetid: 4163cf03-3bff-426c-9844-4cc2d7897d52
title: AD DS 소유자 역할에 DNS 할당
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: dde9ed6035b30ba5b5b96b7132d25a1f8a1c0b8c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59884024"
---
# <a name="assigning-the-dns-for-ad-ds-owner-role"></a>AD DS 소유자 역할에 DNS 할당

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

포리스트 소유자 포리스트의 Active Directory Domain Services (AD DS) 소유자에 대 한 도메인 이름 시스템 (DNS)를 할당합니다. 포리스트의 AD DS 소유자에 대 한 DNS 사람 (또는 사용자 그룹)는 DNS의 배포를 감독 하는 일을 담당 하는 것 (필요한 경우) 및 AD DS 인프라에 대 한 도메인 이름에 등록 된 적절 한 인터넷 기관.  
  
AD DS 소유자에 대 한 DNS 포리스트에 대 한 AD DS 디자인에 대 한 DNS 담당합니다. 조직의 현재 DNS 서버 서비스를 작동 하는 경우 AD DS 소유자 대리자 도메인 컨트롤러에서 실행 되는 DNS 서버로 포리스트 루트 DNS 이름에 대 한 DNS를 사용 하 여 기존 DNS 서버 서비스의 DNS designer 작동 합니다.  
  
포리스트에 대 한 AD DS 소유자에 대 한 DNS 동적 호스트 구성 프로토콜 (DHCP) 그룹 및 조직의 DNS 그룹을 사용 하 여 연락처를 유지 관리 하며 이러한 그룹을 사용 하 여 (있는 경우) 포리스트의 각 도메인의 개별 DNS 소유자 계획을 조정 합니다. 포리스트에 대 한 DNS 소유자 DHCP 및 DNS 그룹 AD DS 디자인 프로세스에 대 한 DNS에 관련 된 각 그룹은 DNS 디자인 계획을 알고 있으며 초기 입력을 제공할 수 있도록 보장 합니다.  
  


