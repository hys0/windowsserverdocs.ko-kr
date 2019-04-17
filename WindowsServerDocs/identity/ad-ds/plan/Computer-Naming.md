---
ms.assetid: f7002265-60fa-40b8-9dd7-4bf131d9320a
title: "컴퓨터 이름 지정"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: d0dbe2da76a1cf3d1a4dd74183b5dd7106ef17b9
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="computer-naming"></a>컴퓨터 이름 지정

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Windows 2000, Windows XP, Windows Server 2003, Windows Server 2008 또는 Windows Vista 운영 체제를 실행 하는 컴퓨터가 도메인에 기본적으로 컴퓨터 자체 이름이 지정 합니다. 자신을 지정 이름 구성 (즉, 시스템 속성의 컴퓨터 이름을)는 컴퓨터의 호스트 이름과 Active Directory 도메인 가입 컴퓨터의 시스템 DNS (도메인 이름) 이름 (즉, 기본 DNS 접미사 시스템 속성의). 연결 된 도메인의 DNS 이름과 호스트 이름을 (FQDN) 정식된 도메인 이름으로 알려져 있습니다. 예를 들어 서버 1 호스트 이름의 컴퓨터가 corp.contoso.com 도메인에 가입 하는 경우 컴퓨터의 FQDN server1.corp.contoso.com는 합니다.  
  
컴퓨터에 이미 DNS 영역에 입력 하거나 등록 통합된 DNS 정적 다른 DNS 도메인 이름 경우 / DHCP(Dynamic Host Configuration Protocol) (DHCP) 서버 서비스는 컴퓨터의 FQDN는 이전에 등록 된 이름 다릅니다. 컴퓨터 이름 중 하나에서 참조할 수 있습니다.  
  
용어가 Active Directory Domain Services (AD DS)에 대 한 자세한 내용은 Active Directory에 명명 규칙을 참조 하세요. 컴퓨터에서 도메인, 사이트 및 조직에 대 한 ([https://go.microsoft.com/fwlink/?LinkID=106629](https://go.microsoft.com/fwlink/?LinkID=106629)).  
  


