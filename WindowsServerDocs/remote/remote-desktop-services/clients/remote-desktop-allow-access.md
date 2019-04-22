---
title: 원격 데스크톱-PC에 대 한 액세스를 허용 합니다.
description: 원격 PC에 액세스 하기 위한 옵션에 알아봅니다
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0f1557ed-53f7-4333-b023-c8e0f4b58bf4
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 06/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: af41304e08f19ca155f6fd13c9258e9a8f20c163
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59817014"
---
# <a name="remote-desktop---allow-access-to-your-pc"></a>원격 데스크톱-PC에 대 한 액세스를 허용 합니다.

>적용 대상: Windows 10, Windows 8.1, Windows Server 2012 R2, Windows Server 2016

원격 데스크톱을 사용 하 여 연결 하 고 사용 하 여 원격 장치에서 PC를 제어할 수는 [Microsoft 원격 데스크톱 클라이언트](remote-desktop-clients.md) (Windows, iOS, macOS 및 Android에 대 한 사용 가능). 사용자 PC에 대 한 원격 연결을 허용 하는 경우에 사용자 PC에 연결 하 여 책상에 앉아 있는 것 처럼 모든 앱, 파일 및 네트워크 리소스에 액세스할 다른 장치를 사용할 수 있습니다.  

> [!NOTE]
> Windows 10 Pro 및 엔터프라이즈, Windows 8.1 및 Windows Server 2008 보다 최신 버전인 Enterprise 및 Pro, Windows 7 Professional, Enterprise 및 Ultimate 및 Windows Server 버전 8에 연결 하려면 원격 데스크톱을 사용할 수 있습니다. (예: Windows 10 Home) Home edition을 실행 하는 컴퓨터를 연결할 수 없습니다. 

에 연결 하려면 원격 PC에는 컴퓨터 전원을 켜야, 네트워크 연결이 있어야, 원격 데스크톱을 사용할 수 있어야 합니다 (이 인터넷을 통해 사용 가능) 원격 컴퓨터에 대 한 네트워크 액세스 있어야 하며 연결할 권한이 있어야 합니다. 연결 하는 데 필요한 권한, 사용자 목록을 여야 합니다. 연결을 시작 하기 전에 것 연결 하려는 컴퓨터의 이름을 조회 하 고 해당 방화벽을 통해 허용 되는 원격 데스크톱 연결 되었는지 확인 하는 것이 좋습니다.

## <a name="how-to-enable-remote-desktop"></a>원격 데스크톱을 사용 하는 방법

원격 장치에서 사용자 PC에 액세스할 수 있도록 하는 가장 간단한 방법은 설정에서 원격 데스크톱 옵션을 사용 하는 합니다. 이 기능에는 Windows 10 Fall Creators update(1709)를 다운로드할 수 있는 별도 추가 된 앱도 제공 됩니다. 이전 버전의 Windows에 대 한 유사한 기능을 제공 하는 합니다. 하지만이 메서드는 작은 기능 및 유효성 검사를 제공 원격 데스크톱을 사용 하도록 설정 하는 레거시 방식에서는 사용할 수도 있습니다.

### <a name="windows-10-fall-creator-update-1709-or-later"></a>Windows 10 Fall Creator Update (1709) 이상

몇 개의 간편한 단계를 사용 하 여 원격 액세스를 위한 PC를 구성할 수 있습니다.
1. 에 연결 하려는 장치의 선택 **시작** 클릭 합니다 **설정** 왼쪽에서 아이콘입니다.
2. 선택 된 **시스템** 뒤에 그룹을 [ **원격 데스크톱** ](ms-settings:remotedesktop) 항목.
3. 슬라이더를 사용 하 여 원격 데스크톱을 사용 하도록 설정 합니다.
4. 또한 절전 모드 해제 하 고 연결을 용이 하 게 검색 가능한 PC를 유지 하는 것이 좋습니다. 클릭 **설정 표시** 사용 하도록 설정 합니다.
5. 필요에 따라 추가 클릭 하 여 원격으로 연결할 수 있는 사용자 **이 PC를 원격으로 액세스할 수 있는 사용자 선택**합니다.
   1. Administrators 그룹의 멤버는 자동으로 액세스할을 수 있습니다.
6. 이 PC에서의 이름을 기록해 **이 PC에 연결 하는 방법을**합니다. 이 클라이언트를 구성 해야 합니다.

### <a name="windows-7-and-early-version-of-windows-10"></a>Windows 7 및 Windows 10의 초기 버전

원격 액세스를 위한 PC를 구성 하려면 다운로드 하 고 실행 합니다 [Microsoft 원격 데스크톱 도우미](https://www.microsoft.com/download/details.aspx?id=50042)합니다. 이 도우미 원격 액세스할 수 있도록 시스템 설정 업데이트, 컴퓨터 연결에 대 한 절전 모드 해제 되 고 방화벽이 원격 데스크톱 연결을 허용 하는지 확인 합니다. 

### <a name="all-versions-of-windows-legacy-method"></a>Windows (레거시 메서드)의 모든 버전

레거시 시스템 속성을 사용 하 여 원격 데스크톱을 사용 하도록 설정 하려면 지침을 따릅니다 [원격 데스크톱 연결을 사용 하 여 다른 컴퓨터에 연결](https://windows.microsoft.com/windows/remote-desktop-connection-faq)합니다.

## <a name="should-i-enable-remote-desktop"></a>원격 데스크톱을 사용 해야 하나요?

앞에 앉아 물리적으로 하는 경우 PC에 액세스 하려는 경우에 원격 데스크톱을 사용할 필요가 없습니다. 원격 데스크톱을 사용 하도록 설정 하면 로컬 네트워크에 표시 되는 PC에 포트를 엽니다. 집 등 신뢰할 수 있는 네트워크에서 원격 데스크톱에만 사용 해야 합니다. 또한 않으려는 액세스가 엄격 하 게 제어 되는 모든 PC에 원격 데스크톱을 사용 하도록 설정 합니다.

사용 하도록 설정 하면 원격 데스크톱에 대 한 액세스 권한을 부여 하는 Administrators 그룹의 모든 사용자가 추가 사용자와 선택한 원격 컴퓨터에서 해당 계정에 액세스할 수 있도록 주의 합니다.

사용자 PC에 액세스할 수 있는 모든 계정이 강력한 암호를 사용 하 여 구성 되어 있는지 확인 해야 합니다.

## <a name="why-allow-connections-only-with-network-level-authentication"></a>네트워크 수준 인증에만 연결 허용 되는 이유? 
 
PC에 액세스할 수 있는 사용자를 제한 하려는 경우에 사용 하 여 인증 NLA (네트워크 수준) 액세스를 허용 하도록 선택 합니다. 이 옵션을 사용 하도록 설정 하면 사용자는 사용자 PC에 연결 하기 전에 네트워크에 자신을 인증 해야 합니다. 악의적인 사용자와 소프트웨어 로부터 컴퓨터를 보호 하는 데 도움이 되는 보다 안전한 인증 방법을 NLA를 사용 하 여 원격 데스크톱을 실행 하는 컴퓨터 에서만에서 연결을 허용 합니다. NLA 및 원격 데스크톱에 대 한 자세한 내용은 체크 아웃 [RDS 연결에 대 한 구성 NLA](https://technet.microsoft.com/library/cc732713(v=ws.11).aspx)합니다. 

원격으로 연결한 경우 PC에 해당 네트워크 외부에서 홈 네트워크,이 옵션을 선택 하지 마십시오.
