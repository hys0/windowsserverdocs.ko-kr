---
title: 개인 세션 데스크톱을 사용 하 여 원격 데스크톱 서비스를 사용 하 여
description: 데스크톱을 통해 rds. 할당 된 개인 설정 되 고 공유 하는 방법에 알아봅니다
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
ms.openlocfilehash: 41f6a28c1b754a5277a0966a87dae08a6aa34e08
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59875954"
---
# <a name="use-personal-session-desktops-with-remote-desktop-services"></a>개인 세션 데스크톱을 사용 하 여 원격 데스크톱 서비스를 사용 하 여

>적용 대상: Windows Server (반기 채널), Windows Server 2016

개인 세션 데스크톱을 사용 하 여 클라우드 컴퓨팅 환경에서 서버 기반 개인 데스크톱을 배포할 수 있습니다.  (클라우드 컴퓨팅 환경에 패브릭에서 Hyper-v 서버와 Microsoft Azure 클라우드 또는 Microsoft 클라우드 플랫폼 같은 게스트 가상 컴퓨터를 구분 합니다.) 개인 세션 데스크톱 기능을 각 사용자가 관리자 권한으로 자신의 개인 세션 호스트에 할당 되는 위치를 세션 컬렉션의 새 형식을 만들려면 원격 데스크톱 서비스 세션 기반 데스크톱 배포 시나리오를 확장 합니다. 

다음 정보를 사용 하 여 만들고 개인 세션 데스크톱 컬렉션을 관리 합니다.

## <a name="create-a-personal-session-desktop-collection"></a>개인 세션 데스크톱 컬렉션 만들기

개인 세션 데스크톱 컬렉션을 만들려면 새로 만들기-RDSessionCollection cmdlet을 사용 합니다. 다음 세 매개 변수는 개인 세션 데스크톱에 필요한 구성 정보를 제공 합니다.

- **-PersonalUnmanaged** -개인 세션 호스트 서버에 사용자를 할당 하는 수 있는 세션 컬렉션의 형식을 지정 합니다. 이 매개 변수를 지정 하지 않으면 로그인 할 때 다음 사용 가능한 세션 호스트에 사용자 할당은 기존의 RD 세션 호스트 컬렉션으로 컬렉션이 만들어집니다.
- **-GrantAdministrativePrivilege** 사용 하는 경우- **-PersonalUnmanaged**를 지정 하는 세션 호스트에 할당 된 사용자 수 관리 권한. 이 매개 변수를 사용 하지 않는 경우 사용자는 표준 사용자 권한만 부여 됩니다.
- **-AutoAssignUser** 사용 하는 경우- **-PersonalUnmanaged**, RD 연결 브로커를 통해 연결 하는 새 사용자 지정 하지 않은 세션 호스트에 자동으로 할당 되도록 지정 합니다. 컬렉션에 할당 되지 않은 세션 호스트가 없는 경우 사용자는 오류 메시지가 표시 됩니다. 이 매개 변수를 사용 하지 않는 경우 해야 [세션 호스트에 수동으로 할당](#manually-assign-a-user-to-a-personal-session-host) 로그인 합니다.

## <a name="manually-assign-a-user-to-a-personal-session-host"></a>개인 세션 호스트에 사용자를 수동으로 할당
사용 된 **집합 RDPersonalSessionDesktopAssignment** 개인 세션 호스트 서버 컬렉션에 사용자를 수동으로 할당할 cmdlet. Cmdlet에는 다음 매개 변수를 지원합니다.

-CollectionName \<string\>

-ConnectionBroker \<string\> 

사용자 \<문자열\>

-Name \<string\>

- **– CollectionName** -개인 세션 데스크톱 컬렉션의 이름을 지정 합니다. 이 매개 변수는 필수적 요소입니다.
- **– ConnectionBroker** -원격 데스크톱 배포에 대 한 원격 데스크톱 연결 브로커 (RD 연결 브로커) 서버를 지정 합니다. 값을 제공 하지 않으면 cmdlet은 로컬 컴퓨터의 정규화 된 도메인 이름 (FQDN)을 사용 합니다.
- **– 사용자** -DOMAIN\User 형식으로 개인 세션 데스크톱을 사용 하 여 연결 하려면 사용자 계정을 지정 합니다. 이 매개 변수는 필수적 요소입니다.
- **– 이름** -세션 호스트 서버에서의 이름을 지정 합니다. 이 매개 변수는 필수적 요소입니다. 여기에 식별 되는 세션 호스트 컬렉션의 멤버 여야 합니다.는 **-CollectionName** 매개 변수를 지정 합니다.

합니다 **가져오기-RDPersonalSessionDesktopAssignment** cmdlet은 텍스트 파일에서 사용자 계정 및 개인 세션 데스크톱 간의 연결을 가져옵니다. Cmdlet에는 다음 매개 변수를 지원합니다.

-CollectionName \<string\>

-ConnectionBroker \<string\>

-Path \<string>

**– 경로** 가져올 파일의 경로 및 파일 이름을 지정 합니다.
 
## <a name="removing-a-user-assignment-from-a-personal-session-host"></a>개인 세션 호스트에서 사용자 할당 제거
사용 된 **제거 RDPersonalSessionDesktopAssignment** 개인 세션 데스크톱와 사용자 간의 연결을 제거 하는 cmdlet입니다. Cmdlet에는 다음 매개 변수를 지원합니다.

-CollectionName \<string\>

-ConnectionBroker \<string\>

-Force

-Name \<string\>

사용자 \<문자열\>

**– Force** 실행 사용자에 게 확인을 요청 하지 않고 명령을 강제 합니다.

## <a name="query-user-assignments"></a>쿼리 사용자 할당
사용 된 **Get RDPersonalSessionDesktopAssignment** 개인 세션 데스크톱 및 연결 된 사용자 계정 목록을 가져오려면 cmdlet. Cmdlet에는 다음 매개 변수를 지원합니다.

-CollectionName \<string\>

-ConnectionBroker \<string\>

사용자 \<문자열\>

-Name \<string\>

컬렉션 이름, 사용자 이름 또는 세션 데스크톱 이름별 쿼리에 cmdlet을 실행할 수 있습니다. 만 지정한 경우는 **– CollectionName** 매개 변수를 cmdlet에는 세션 호스트 및 연관 된 사용자의 목록을 반환 합니다. 경우에 **– 사용자** 매개 변수를 사용자와 관련 된 세션 호스트 반환 됩니다. 제공 하는 경우는 **– 이름** 매개 변수를 해당 세션 호스트와 연결 된 사용자가 반환 됩니다. 


합니다 **내보내기 RDPersonalPersonalDesktopAssignment** cmdlet은 현재 사용자 및 개인용 가상 데스크톱 간의 연결을 텍스트 파일에 내보냅니다. Cmdlet에는 다음 매개 변수를 지원합니다.

-CollectionName \<string\>

-ConnectionBroker \<string\>

-Path \<string\>


일반적인 매개 변수를 지원 하는 모든 새 cmdlet:-Verbose,-Debug,-ErrorAction,-ErrorVariable,-OutBuffer 및-outvariable을 지원 합니다. 자세한 내용은 [about_CommonParameters](https://go.microsoft.com/fwlink/p/?LinkID=113216)를 참조하세요.

## <a name="hardware-accelerated-graphics"></a>하드웨어 가속된 그래픽
Windows Server 2016 OpenGL을 지원 하도록 RemoteFX 3D 그래픽 어댑터 (vGPU) 기술을 확장 하 고 단일 사용자 Windows Server 2016 게스트 Vm을 지원 합니다. 가속 된 그래픽을 필요로 하는 호스 티 드 응용 프로그램에 대 한 지원을 제공 하는 새 vGPU 기능을 사용 하 여 개인 세션 데스크톱을 결합할 수 있습니다. 또는 개인 세션 데스크톱도 가속된 그래픽을 필요로 하는 호스 티 드 응용 프로그램에 대 한 지원을 제공 하는 새 불연속 장치 할당 (DDA) 기능과 결합할 수 있습니다.
