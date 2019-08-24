---
title: 원격 데스크톱 서비스에서 개인 세션 데스크톱 사용
description: RDS를 통해 할당된 맞춤형 데스크톱을 공유하는 방법을 알아봅니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
author: lizap
ms.author: elizapo
ms.date: 09/16/2016
manager: dongill
ms.openlocfilehash: 723e68bad79e7723aaa0690c312e20ccf47c47b0
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2019
ms.locfileid: "63743508"
---
# <a name="use-personal-session-desktops-with-remote-desktop-services"></a>원격 데스크톱 서비스에서 개인 세션 데스크톱 사용

>적용 대상: Windows Server(반기 채널), Windows Server 2019, Windows Server 2016

개인 세션 데스크톱을 사용하여 클라우드 컴퓨팅 환경에서 서버 기반 개인 데스크톱을 배포할 수 있습니다.  (클라우드 컴퓨팅 환경에서는 패브릭 Hyper-V 서버와 Microsoft Azure 클라우드 또는 Microsoft 클라우드 플랫폼 같은 게스트 가상 머신이 구분되어 있습니다.) 개인 세션 데스크톱 기능은 각 사용자가 관리자 권한으로 자신의 개인 세션 호스트에 할당되는 새로운 유형의 세션 컬렉션을 만들기 위해 원격 데스크톱 서비스에서 세션 기반 데스크톱 배포 시나리오를 확장합니다. 

다음 정보를 사용하여 개인 세션 데스크톱 컬렉션을 만들고 관리합니다.

## <a name="create-a-personal-session-desktop-collection"></a>개인 세션 데스크톱 컬렉션 만들기

New-RDSessionCollection cmdlet을 사용하여 개인 세션 데스크톱 컬렉션을 만듭니다. 다음 세 가지 매개 변수는 개인 세션 데스크톱에 필요한 구성 정보를 제공합니다.

- **-PersonalUnmanaged** - 사용자를 개인 세션 호스트 서버에 할당할 수 있는 세션 컬렉션 유형을 지정합니다. 이 매개 변수를 지정하지 않으면 컬렉션은 사용자가 로그인할 때 사용 가능한 다음 세션 호스트에 할당되는 기존의 RD 세션 호스트 컬렉션으로 만들어집니다.
- **-GrantAdministrativePrivilege** - **-PersonalUnmanaged**를 사용하는 경우 사용자가 세션 호스트에 할당되어 관리 권한이 부여되도록 지정합니다. 이 매개 변수를 사용하지 않는 경우 사용자에게 표준 사용자 권한만 부여됩니다.
- **-AutoAssignUser** - **-PersonalUnmanaged**를 사용하는 경우 RD 연결 브로커를 통해 연결하는 새 사용자가 할당되지 않은 세션 호스트에 자동으로 할당되도록 지정됩니다. 컬렉션에 할당되지 않은 세션 호스트가 없는 경우 오류 메시지가 표시됩니다. 이 매개 변수를 사용하지 않는 경우 로그인하기 전에 [사용자를 세션 호스트에 수동으로 할당](#manually-assign-a-user-to-a-personal-session-host)해야 합니다.

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

## <a name="hardware-accelerated-graphics"></a>하드웨어 가속 그래픽
Windows Server 2016은 RemoteFX 3D vGPU(그래픽 어댑터) 기술을 확장하여 OpenGL을 지원하고 단일 사용자 Windows Server 2016 게스트 VM을 지원합니다. 개인 세션 데스크톱을 새 vGPU 기능과 결합하여 가속된 그래픽을 필요로 하는 호스티드 애플리케이션을 지원할 수 있습니다. 또는 개인 세션 데스크톱을 새 DDA(개별 디바이스 할당) 기능과 결합하여 가속된 그래픽을 필요로 하는 호스티드 애플리케이션도 지원할 수 있습니다.
