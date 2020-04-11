---
title: 원격 데스크톱 - PC 액세스 허용
description: PC에 원격으로 액세스하기 위한 옵션에 대해 알아보기
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.topic: article
ms.assetid: 0f1557ed-53f7-4333-b023-c8e0f4b58bf4
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 06/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0596dbd847ae8e64e1f4c780f142f28e34656ae8
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855906"
---
# <a name="remote-desktop---allow-access-to-your-pc"></a>원격 데스크톱 - PC 액세스 허용

>적용 대상: Windows 10, Windows 8.1, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2

[Microsoft 원격 데스크톱 클라이언트](remote-desktop-clients.md)(Windows, iOS, macOS 맟 Android에서 사용 가능)를 사용하면 원격 디바이스에서 원격 데스크톱을 통해 PC에 연결하고 제어할 수 있습니다. PC에 대한 원격 연결을 허용하면 다른 디바이스를 사용하여 PC에 연결하고, 책상에 앉아 있는 것처럼 모든 앱, 파일 및 네트워크 리소스에 액세스할 수 있습니다.  

> [!NOTE]
> 원격 데스크톱을 사용하여 Windows 10 Pro/Enterprise, Windows 8.1 및 8 Enterprise/Pro, Windows 7 Professional/Enterprise/Ultimate, Windows Server 2008 이후 버전의 Windows Server에 연결할 수 있습니다. Home 버전(예: Windows 10 Home)을 실행 중인 컴퓨터에는 연결할 수 없습니다. 

원격 PC에 연결하려면 컴퓨터가 켜져 있고, 네트워크에 연결되어 있어야 하며, 원격 데스크톱이 사용 설정되어 있고, 사용자에게 원격 컴퓨터에 대한 네트워크(인터넷) 액세스 권한과 연결 권한이 있어야 합니다. 사용자 목록에 있는 사용자에게 연결 권한이 있습니다. 연결을 시작하기 전에 연결할 컴퓨터의 이름을 조회하고 방화벽을 통해 원격 데스크톱 연결이 허용되는지 확인하는 것이 좋습니다.

## <a name="how-to-enable-remote-desktop"></a>원격 데스크톱을 사용 설정하는 방법

원격 디바이스에서 PC에 대한 액세스를 허용하는 가장 간단한 방법은 설정에서 원격 데스크톱 옵션을 사용하는 것입니다. 이 기능은 Windows 10 Fall Creators Update(1709)에 추가되었으므로 이전 버전의 Windows에 유사한 기능을 제공하는 별도의 다운로드 가능한 앱도 사용할 수 있습니다. 또한 원격 데스크톱을 사용 설정하는 기존 방법을 사용할 수도 있지만 이 방법은 더 적은 기능과 유효성 검사를 제공합니다.

### <a name="windows-10-fall-creator-update-1709-or-later"></a>Windows 10 Fall Creator Update(1709) 이상

몇 가지 간단한 단계를 통해 PC의 원격 액세스를 구성할 수 있습니다.
1. 연결하려는 디바이스에서 **시작**을 선택한 다음, 왼쪽에서 **설정** 아이콘을 클릭합니다.
2. **시스템** 그룹, [**원격 데스크톱**](ms-settings:remotedesktop) 항목을 차례로 선택합니다.
3. 원격 데스크톱을 사용하도록 설정하려면 슬라이더를 사용하세요.
4. 또한 원활한 연결을 위해 PC의 절전 모드를 해제하고 검색 가능하게 유지하는 것이 좋습니다. **설정 표시**를 클릭하여 활성화합니다.
5. 필요에 따라 **이 PC에 원격으로 액세스할 수 있는 사용자 선택**을 클릭하여 원격으로 연결할 수 있는 사용자를 추가합니다.
   1. 관리자 그룹의 구성원에게는 자동으로 액세스 권한이 부여됩니다.
6. **이 PC에 연결하는 방법** 아래에 나오는 이 PC의 이름을 기록해 둡니다. 클라이언트를 구성하려면 이 정보가 필요합니다.

### <a name="windows-7-and-early-version-of-windows-10"></a>Windows 7 및 Windows 10의 초기 버전

PC의 원격 액세스를 구성하려면 [Microsoft 원격 데스크톱 도우미](https://www.microsoft.com/download/details.aspx?id=50042)를 다운로드하고 실행합니다. 이 도우미는 원격 액세스를 사용하도록 시스템 설정을 업데이트하고, 컴퓨터가 절전 모드에서 해제된 상태로 연결을 기다리도록 하며, 방화벽이 원격 데스크톱 연결을 허용하는지 확인합니다. 

### <a name="all-versions-of-windows-legacy-method"></a>모든 버전의 Windows(기존 방법)

레거시 시스템 속성을 사용하여 원격 데스크톱을 사용 설정하려면 [원격 데스크톱 연결을 사용하여 다른 컴퓨터에 연결](https://windows.microsoft.com/windows/remote-desktop-connection-faq) 지침을 따르세요.

## <a name="should-i-enable-remote-desktop"></a>원격 데스크톱을 사용하도록 설정해야 하나요?

PC를 실제로 사용할 때만 PC에 액세스하려는 경우에는 원격 데스크톱을 사용하도록 설정할 필요가 없습니다. 원격 데스크톱을 사용하도록 설정하면 로컬 네트워크에 표시되는 PC의 포트가 열립니다. 신뢰할 수 있는 네트워크(예: 집)의 원격 데스크톱만 사용하도록 설정해야 합니다. 또한 액세스가 엄격하게 제어되는 PC에서는 원격 데스크톱을 사용하도록 설정하지 않는 것이 좋습니다.

원격 데스크톱에 대한 액세스를 사용하도록 설정할 때는 관리자 그룹의 모든 사용자와 선택된 추가 사용자에게 컴퓨터의 계정에 원격으로 액세스할 수 있는 권한을 부여해야 합니다.

PC에 액세스할 수 있는 모든 계정에 강력한 암호를 구성해야 합니다.

## <a name="why-allow-connections-only-with-network-level-authentication"></a>네트워크 수준 인증을 통한 연결만 허용되는 이유는 무엇인가요? 

PC에 액세스할 수 있는 사용자를 제한하려는 경우 NLA(네트워크 수준 인증)를 통한 액세스만 허용하도록 선택합니다. 이 옵션을 사용하도록 설정하면 다른 사용자가 네트워크에 인증해야만 PC에 연결할 수 있습니다. NLA를 사용하는 원격 데스크톱을 실행하는 컴퓨터에서만 연결을 허용하는 것은 악의적인 사용자와 소프트웨어로부터 컴퓨터를 보호하는 데 도움이 되는 보다 안전한 인증 방법입니다. NLA 및 원격 데스크톱에 대해 자세히 알아보려면 [RDS 연결용 NLA 구성](https://technet.microsoft.com/library/cc732713(v=ws.11).aspx)을 확인하세요.

홈 네트워크 외부에서 해당 네트워크의 PC에 원격으로 연결하는 경우에는 이 옵션을 선택하지 마세요.
