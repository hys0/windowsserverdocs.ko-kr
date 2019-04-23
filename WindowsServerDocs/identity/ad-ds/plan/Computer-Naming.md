---
ms.assetid: f7002265-60fa-40b8-9dd7-4bf131d9320a
title: 컴퓨터 이름 지정
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: ae2483571d67b4cdb32c2a547b924b1315573da0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59842164"
---
# <a name="computer-naming"></a>컴퓨터 이름 지정

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Windows 2000, Windows XP, Windows Server 2003, Windows Server 2008 또는 Windows Vista 운영 체제를 실행 하는 컴퓨터를 조인 하는 경우 도메인에 컴퓨터 기본적으로 자체 이름을 할당 합니다. 자체 할당 이름 구성 (즉, 시스템 속성의 컴퓨터 이름) 컴퓨터의 호스트 이름 및 컴퓨터에 가입 된 Active Directory 도메인의 도메인 이름 시스템 (DNS) 이름 (즉, 주 DNS 접미사 시스템 속성에서). 호스트 이름 및 도메인의 DNS 이름을 연결 하 여 정규화 된 도메인 이름 (FQDN) 라고 합니다. 예를 들어, Server1 조인 corp.contoso.com 도메인 이름이 하는 호스트 된 컴퓨터, 컴퓨터의 FQDN server1.corp.contoso.com입니다.  
  
컴퓨터의 FQDN은 등록 된 이름과 구분 하는 컴퓨터에 정적으로 DNS 영역에 입력 되었거나 DNS/동적 호스트 구성 프로토콜 (DHCP) 서버 서비스를 통합된 하 여 등록 된 다른 DNS 도메인 이름을 이미 있으면 이전에 있습니다. 컴퓨터 이름 중 하나를 참조할 수 있습니다.  
  
Active Directory Domain Services (AD DS)에서 명명 규칙에 대 한 자세한 내용은 컴퓨터, 도메인, 사이트 및 조직 구성 단위에 대 한 Active Directory의 명명 규칙 참조 ([https://go.microsoft.com/fwlink/?LinkID=106629](https://go.microsoft.com/fwlink/?LinkID=106629)).  
  


