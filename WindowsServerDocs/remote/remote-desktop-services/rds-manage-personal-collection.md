---
title: RDS에서 개인 데스크톱 세션 컬렉션 관리
description: RDS 배포에 RDSH 및 RemoteApp 프로그램을 추가하는 방법을 알아봅니다.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 11/08/2016
ms.tgt_pltfrm: na
ms.topic: article
author: lizap
manager: dongill
ms.openlocfilehash: 7be6b2bfe1105357811927f5da7092e8c16c3446
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/14/2020
ms.locfileid: "75949845"
---
# <a name="manage-your-personal-desktop-session-collections"></a>개인 데스크톱 세션 컬렉션 관리

다음 정보를 사용하여 원격 데스크톱 서비스에서 개인 데스크톱 세션 컬렉션을 관리합니다.

## <a name="manually-assign-a-user-to-a-personal-session-host"></a>개인 세션 호스트에 사용자를 수동으로 할당
**Set-RDPersonalSessionDesktopAssignment** cmdlet을 사용하여 컬렉션의 개인 세션 호스트 서버에 수동으로 사용자를 할당합니다. 이 cmdlet은 다음 매개 변수를 지원합니다.

-CollectionName \<string\>

-ConnectionBroker \<string\> 

-User \<string\>

-Name \<string\>

- **–CollectionName** - 개인 세션 데스크톱 컬렉션의 이름을 지정합니다. 이 매개 변수는 필수입니다.
- **–ConnectionBroker** - 원격 데스크톱 배포의 RD 연결 브로커(원격 데스크톱 연결 브로커) 서버를 지정합니다. 값을 제공하지 않으면 이 cmdlet은 로컬 컴퓨터의 FQDN(정규화된 도메인 이름)을 사용합니다.
- **–User** - 개인 세션 데스크톱에 연결할 사용자 계정을 DOMAIN\User 형식으로 지정합니다. 이 매개 변수는 필수입니다.
- **–Name** - 세션 호스트 서버의 이름을 지정합니다. 이 매개 변수는 필수입니다. 여기에 식별된 세션 호스트는 **-CollectionName** 매개 변수가 지정하는 컬렉션의 멤버여야 합니다.

**Import-RDPersonalSessionDesktopAssignment** cmdlet은 텍스트 파일에서 사용자 계정 및 개인 세션 데스크톱 간 연결을 가져옵니다. 이 cmdlet은 다음 매개 변수를 지원합니다.

-CollectionName \<string\>

-ConnectionBroker \<string\>

-Path \<string>

**–Path** 가져올 파일의 경로 및 파일 이름을 지정합니다.
 
## <a name="removing-a-user-assignment-from-a-personal-session-host"></a>개인 세션 호스트에서 사용자 할당 제거
**Remove-RDPersonalSessionDesktopAssignment** cmdlet을 사용하여 개인 세션 데스크톱과 사용자 간 연결을 제거합니다. 이 cmdlet은 다음 매개 변수를 지원합니다.

-CollectionName \<string\>

-ConnectionBroker \<string\>

-Force

-Name \<string\>

-User \<string\>

**–Force** 사용자 확인을 요청하지 않고 명령을 강제 실행합니다.

## <a name="query-user-assignments"></a>사용자 할당 쿼리
**Get-RDPersonalSessionDesktopAssignment** cmdlet을 사용하여 개인 세션 데스크톱 및 연결된 사용자 계정 목록을 가져옵니다. 이 cmdlet은 다음 매개 변수를 지원합니다.

-CollectionName \<string\>

-ConnectionBroker \<string\>

-User \<string\>

-Name \<string\>

이 cmdlet을 실행하여 컬렉션 이름, 사용자 이름 또는 세션 데스크톱 이름별로 쿼리할 수 있습니다. **–CollectionName** 매개 변수만 지정하면 이 cmdlet은 세션 호스트 및 연결된 사용자의 목록을 반환합니다. **–User** 매개 변수도 지정하는 경우 해당 사용자와 연결된 세션 호스트가 반환됩니다. **–Name** 매개 변수를 제공하는 경우 해당 세션 호스트와 연결된 사용자가 반환됩니다. 


**Export-RDPersonalPersonalDesktopAssignment** cmdlet을 사용하여 사용자와 개인 가상 데스크톱 간의 현재 연결을 텍스트 파일로 내보냅니다. 이 cmdlet은 다음 매개 변수를 지원합니다.

-CollectionName \<string\>

-ConnectionBroker \<string\>

-Path \<string\>


모든 새 cmdlet은 -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer, -OutVariable 등의 일반 매개 변수를 지원합니다. 자세한 내용은 [about_CommonParameters](https://go.microsoft.com/fwlink/p/?LinkID=113216)를 참조하세요.
