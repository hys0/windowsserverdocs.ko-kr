---
ms.assetid: 4163cf03-3bff-426c-9844-4cc2d7897d52
title: AD DS 소유자 역할에 DNS 할당
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 8ef63fd9e53d20c812ff84e601e73d4276b304be
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80825266"
---
# <a name="assigning-the-dns-for-ad-ds-owner-role"></a>AD DS 소유자 역할에 DNS 할당

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

포리스트 소유자는 포리스트에 대 한 Active Directory Domain Services (AD DS) 소유자의 DNS (Domain Name System)를 할당 합니다. 포리스트의 AD DS 소유자에 대 한 DNS는 AD DS 인프라의 DNS 배포를 감독 하 고 필요한 경우 도메인 이름이 적절 한 인터넷 기관에 등록 되었는지 확인 하는 사람 (또는 사용자 그룹)입니다.  
  
AD DS 소유자에 대 한 DNS는 포리스트에 대 한 AD DS 디자인의 DNS를 담당 합니다. 조직에서 현재 DNS 서버 서비스를 운영 하 고 있는 경우 기존 DNS 서버 서비스에 대 한 DNS 디자이너는 AD DS 소유자의 DNS를 사용 하 여 포리스트 루트 DNS 이름을 도메인 컨트롤러에서 실행 되는 DNS 서버에 위임 합니다.  
  
포리스트의 AD DS 소유자에 대 한 DNS는 또한 DHCP (Dynamic Host Configuration Protocol) 그룹 및 조직의 DNS 그룹과의 연결을 유지 하 고 이러한 그룹을 사용 하 여 포리스트의 각 도메인에 대 한 개별 DNS 소유자 계획을 조정 합니다. 포리스트에 대 한 DNS 소유자는 각 그룹이 DNS 디자인 계획을 인식 하 고 입력을 조기에 제공할 수 있도록 DHCP 및 DNS 그룹이 DNS (AD DS) 디자인 프로세스에 대 한 DNS에 포함 되도록 합니다.  
  


