---
title: 원격 데스크톱 서비스 컬렉션 만들기
description: RDS 배포에 RDSH 및 RemoteApp 프로그램 및 추가 하는 방법에 알아봅니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 11/08/2016
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ae9767e3-864a-4eb2-96c0-626759ce6d60
author: lizap
manager: dongill
ms.openlocfilehash: 52806e28c4ef87453995728623efe2954a76dfd9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59839244"
---
# <a name="create-a-remote-desktop-services-collection-for-desktops-and-apps-to-run"></a>데스크톱 및 실행 하는 앱에 대 한 원격 데스크톱 서비스 컬렉션 만들기

>적용 대상: Windows Server (반기 채널), Windows Server 2016

원격 데스크톱 서비스 세션 컬렉션을 만들려면 다음 단계를 사용 합니다. 세션 컬렉션에는 앱 및 데스크톱 사용자에 게 제공 하려는 보유 합니다. 컬렉션을 만든 후 게시 사용자가 액세스할 수 있도록 합니다.

필요한 컬렉션의 종류를 결정 해야 하는 컬렉션을 만들기 전에: 데스크톱 세션 또는 개인 데스크톱 세션을 풀링됩니다. 

- **풀링된 데스크톱 세션을 사용 하 여 세션 기반 가상화를 위한**: 사용자의 일상적인 작업을 구동 하는 비용 효율적인 다중 세션 환경을 제공 하기 위해 Windows Server의 계산 능력을 활용 합니다.
- **에 대 한 개인 데스크톱 세션을 사용 하 여 가상 데스크톱 인프라 (VDI)를 만들려면**: 높은 성능, 응용 프로그램 호환성 및 사용자가 해당 Windows 데스크톱 환경 기대 하는 경험을 제공 하기 위해 Windows 클라이언트를 활용 합니다.
 
풀링된 세션을 사용 하 여 여러 사용자가 액세스할 공유 풀 리소스의 개인 데스크톱 세션을 사용 하는 동안 사용자가 할당 된 풀 내에서 자신의 데스크톱입니다. 풀링된 세션 개인 세션 데스크톱 경험을 사용자 지정할 수 있도록 하는 동안 낮은 전체 비용을 제공 합니다.

공유 호스팅 응용 프로그램에 그래픽을 많이 해야 하는 경우에 그래픽 가속에 대해 구성 된 RemoteFX vGPU를 사용한 개인 세션 데스크톱을 결합할 수 있습니다. 또는 개인 세션 데스크톱도 가속된 그래픽을 필요로 하는 호스 티 드 응용 프로그램에 대 한 지원을 제공 하는 새 불연속 장치 할당 (DDA) 기능과 결합할 수 있습니다. 체크 아웃 [그래픽 가상화 기술을 적합 한](rds-graphics-virtualization.md) 자세한 내용은 합니다.


선택한 컬렉션의 형식에 관계 없이-Remoteapp 프로그램 및 사용자 지원 되는 모든 장치에서 액세스 하 고 프로그램을 로컬로 실행 된 것 처럼 작업할 수 있는 리소스를 사용 하 여 해당 컬렉션을 채울 수 있습니다.

## <a name="create-a-pooled-desktop-session-collection"></a>풀링된 데스크톱 세션 컬렉션 만들기

1.  서버 관리자에서 클릭 **원격 데스크톱 서비스 > 컬렉션 > 작업 > 세션 컬렉션 만들기**합니다.  
2.  예를 들어 컬렉션에 대 한 이름을 입력 **ContosoAps**합니다.  
3.  (예: Contoso Shr1) 만든 RD 세션 호스트 서버를 선택 합니다.  
4.  기본값을 적용 **사용자 그룹**합니다.  
5.  이 컬렉션에 대 한 사용자 프로필 디스크에 대해 만든 파일 공유의 위치를 입력 (예를 들어 **\Contoso-Cb1\UserDisksr**).   
6.  **만들기**를 클릭합니다. 에서는 컬렉션을 만든 경우 클릭 **닫기**합니다.  


## <a name="create-a-personal-desktop-session-collection"></a>개인 데스크톱 세션 컬렉션 만들기

개인 세션 데스크톱 컬렉션을 만들려면 새로 만들기-RDSessionCollection cmdlet을 사용 합니다. 다음 세 매개 변수는 개인 세션 데스크톱에 필요한 구성 정보를 제공 합니다.

- **-PersonalUnmanaged** -개인 세션 호스트 서버에 사용자를 할당 하는 수 있는 세션 컬렉션의 형식을 지정 합니다. 이 매개 변수를 지정 하지 않으면 로그인 할 때 다음 사용 가능한 세션 호스트에 사용자 할당은 기존의 RD 세션 호스트 컬렉션으로 컬렉션이 만들어집니다.
- **-GrantAdministrativePrivilege** 사용 하는 경우- **-PersonalUnmanaged**를 지정 하는 세션 호스트에 할당 된 사용자 수 관리 권한. 이 매개 변수를 사용 하지 않는 경우 사용자는 표준 사용자 권한만 부여 됩니다.
- **-AutoAssignUser** 사용 하는 경우- **-PersonalUnmanaged**, RD 연결 브로커를 통해 연결 하는 새 사용자 지정 하지 않은 세션 호스트에 자동으로 할당 되도록 지정 합니다. 컬렉션에 할당 되지 않은 세션 호스트가 없는 경우 사용자는 오류 메시지가 표시 됩니다. 이 매개 변수를 사용 하지 않는 경우 해야 [세션 호스트에 수동으로 할당](rds-manage-personal-collection.md#manually-assign-a-user-to-a-personal-session-host) 로그인 합니다.

개인 데스크톱 세션 컬렉션을 관리 하려면 PowerShell cmdlet을 사용할 수 있습니다. 참조 [개인 데스크톱 세션 컬렉션을 관리](rds-manage-personal-collection.md) 자세한 내용은 합니다.

## <a name="publish-remoteapp-programs"></a>RemoteApp 프로그램 게시
컬렉션에는 앱 및 리소스를 게시 하려면 다음 단계를 사용 합니다.

1.  새 컬렉션을 선택 하는 서버 관리자에서 (**ContosoApps**).  
2.  RemoteApp 프로그램에서 클릭 **게시할 RemoteApp 프로그램**합니다.  
3. 다음을 클릭 하 고 게시 하려는 프로그램 선택 **게시**합니다.  
