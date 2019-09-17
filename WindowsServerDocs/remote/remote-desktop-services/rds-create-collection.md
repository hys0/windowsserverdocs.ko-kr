---
title: 원격 데스크톱 서비스 컬렉션 만들기
description: RDS 배포에 RDSH 및 RemoteApp 프로그램을 추가하는 방법을 알아봅니다.
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
ms.openlocfilehash: ca43a37bff28a035d9f7292da830a23ca29d23bc
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70871032"
---
# <a name="create-a-remote-desktop-services-collection-for-desktops-and-apps-to-run"></a>데스크톱 및 앱을 실행할 원격 데스크톱 서비스 컬렉션 만들기

>적용 대상: Windows Server(반기 채널), Windows Server 2019, Windows Server 2016

다음 단계를 사용하여 원격 데스크톱 서비스 세션 컬렉션을 만듭니다. 세션 컬렉션은 사용자에게 제공하려는 앱 및 데스크톱이 포함됩니다. 컬렉션을 만든 후 사용자가 액세스할 수 있도록 게시합니다.

컬렉션을 만들기 전에 풀링된 데스크톱 세션과 개인 데스크톱 세션 중에서 필요한 컬렉션 종류를 결정해야 합니다. 

- **세션 기반 가상화를 위해 풀링된 데스크톱 세션 사용**: Windows Server의 컴퓨팅 능력을 활용하여 사용자의 일상적인 워크로드를 구동하기 위한 비용 효율적인 다중 세션 환경을 제공합니다.
- **VDI(가상 데스크톱 인프라)를 만들기 위해 개인 데스크톱 세션 사용**: Windows 클라이언트를 활용하여 사용자들이 Windows 데스크톱 환경에서 기대하게 되는 고성능, 애플리케이션 호환성 및 익숙함을 제공합니다.
 
풀링된 세션을 사용할 경우 여러 명의 사용자가 공유 리소스 풀에 액세스할 수 있지만, 개인 데스크톱 세션을 사용할 경우 풀 내의 고유한 데스크톱이 할당됩니다. 풀링된 세션은 낮아진 전체 비용을 제공하지만, 개인 세션에서는 데스크톱 환경을 사용자 지정할 수 있습니다.

그래픽을 많이 사용하는 호스티드 애플리케이션을 공유해야 하는 경우 개인 세션 데스크톱을 그래픽 가속을 위해 구성된 RemoteFX vGPU와 결합할 수 있습니다. 또는 개인 세션 데스크톱을 새 DDA(개별 디바이스 할당) 기능과 결합하여 가속된 그래픽을 필요로 하는 호스티드 애플리케이션도 지원할 수 있습니다. 자세한 내용은 [나에게 적합한 그래픽 가상화 기술은 무엇일까요?](rds-graphics-virtualization.md)를 참조하세요.


선택한 컬렉션 형식에 관계 없이, 프로그램이 로컬로 실행되더라도 사용자가 지원되는 모든 디바이스에서 액세스하고 작동할 수 있는 RemoteApp - 프로그램 및 리소스로 이러한 컬렉션을 채웁니다.

## <a name="create-a-pooled-desktop-session-collection"></a>풀링된 데스크톱 세션 컬렉션 만들기

1.  서버 관리자에서 클릭 **원격 데스크톱 서비스 > 컬렉션 > 작업 > 세션 컬렉션 만들기**합니다.  
2.  컬렉션의 이름(예: **ContosoApps**)을 입력합니다.  
3.  만든 RD 세션 호스트 서버(예: Contoso-Shr1)를 선택합니다.  
4.  기본값을 적용 **사용자 그룹**합니다.  
5.  이 컬렉션에 대 한 사용자 프로필 디스크에 대해 만든 파일 공유의 위치를 입력 (예를 들어 **\Contoso-Cb1\UserDisksr**).   
6.  **만들기**를 클릭합니다. 에서는 컬렉션을 만든 경우 클릭 **닫기**합니다.  


## <a name="create-a-personal-desktop-session-collection"></a>개인 데스크톱 세션 컬렉션 만들기

New-RDSessionCollection cmdlet을 사용하여 개인 세션 데스크톱 컬렉션을 만듭니다. 다음 세 가지 매개 변수는 개인 세션 데스크톱에 필요한 구성 정보를 제공합니다.

- **-PersonalUnmanaged** - 사용자를 개인 세션 호스트 서버에 할당할 수 있는 세션 컬렉션 유형을 지정합니다. 이 매개 변수를 지정하지 않으면 컬렉션은 사용자가 로그인할 때 사용 가능한 다음 세션 호스트에 할당되는 기존의 RD 세션 호스트 컬렉션으로 만들어집니다.
- **-GrantAdministrativePrivilege** - **-PersonalUnmanaged**를 사용하는 경우 사용자가 세션 호스트에 할당되어 관리 권한이 부여되도록 지정합니다. 이 매개 변수를 사용하지 않는 경우 사용자에게 표준 사용자 권한만 부여됩니다.
- **-AutoAssignUser** - **-PersonalUnmanaged**를 사용하는 경우 RD 연결 브로커를 통해 연결하는 새 사용자가 할당되지 않은 세션 호스트에 자동으로 할당되도록 지정됩니다. 컬렉션에 할당되지 않은 세션 호스트가 없는 경우 오류 메시지가 표시됩니다. 이 매개 변수를 사용하지 않는 경우 로그인하기 전에 [사용자를 세션 호스트에 수동으로 할당](rds-manage-personal-collection.md#manually-assign-a-user-to-a-personal-session-host)해야 합니다.

PowerShell cmdlet을 사용하여 개인 데스크톱 세션 컬렉션을 관리할 수 있습니다. 자세한 내용은 [개인 데스크톱 세션 컬렉션 관리](rds-manage-personal-collection.md)를 참조하세요.

## <a name="publish-remoteapp-programs"></a>RemoteApp 프로그램 게시
다음 단계를 사용하여 컬렉션의 앱 및 리소스를 게시합니다.

1.  새 컬렉션을 선택 하는 서버 관리자에서 (**ContosoApps**).  
2.  RemoteApp 프로그램에서 클릭 **게시할 RemoteApp 프로그램**합니다.  
3. 다음을 클릭 하 고 게시 하려는 프로그램 선택 **게시**합니다.  
