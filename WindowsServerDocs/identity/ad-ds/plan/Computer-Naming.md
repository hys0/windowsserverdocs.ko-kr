---
ms.assetid: f7002265-60fa-40b8-9dd7-4bf131d9320a
title: 컴퓨터 이름 지정
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 2b396778b458976604e527fad0c4649d03239fa6
ms.sourcegitcommit: 11421f4005f9f3a3f6c0db95b1836d0f765a9fa3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81624381"
---
# <a name="computer-naming"></a>컴퓨터 이름 지정

> 적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Windows 2000, Windows XP, Windows Server 2003, Windows Server 2008 또는 Windows Vista 운영 체제를 실행 하는 컴퓨터가 도메인에 가입 하면 기본적으로 컴퓨터에서 자체 이름을 할당 합니다. 자신을 할당 하는 이름은 컴퓨터의 호스트 이름 (시스템 속성의 컴퓨터 이름)과 컴퓨터가 조인한 Active Directory 도메인의 DNS (Domain Name System) 이름 (시스템 속성의 주 DNS 접미사)으로 구성 됩니다. 도메인의 호스트 이름과 DNS 이름을 연결 하는 것을 FQDN (정규화 된 도메인 이름) 이라고 합니다. 예를 들어 호스트 이름이 Server1 인 컴퓨터가 도메인 corp.contoso.com에 가입 하면 컴퓨터의 FQDN은 server1.corp.contoso.com입니다.

컴퓨터에 이미 DNS 영역에 정적으로 입력 되었거나 통합 된 DNS/동적 호스트 구성 프로토콜 (DHCP) 서버 서비스에서 등록 된 다른 DNS 도메인 이름이 있는 경우 컴퓨터의 FQDN은 이전에 등록 된 이름과는 다릅니다. 두 이름 중 하나를 통해 컴퓨터를 참조할 수 있습니다.

Active Directory Domain Services (AD DS)의 명명 규칙에 대 한 자세한 내용은 [컴퓨터, 도메인, 사이트 및 ou에 대 한 Active Directory의 명명 규칙](https://support.microsoft.com/help/909264/)을 참조 하세요.
