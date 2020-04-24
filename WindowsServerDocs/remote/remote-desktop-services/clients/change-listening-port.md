---
title: 원격 데스크톱에서 수신 대기 포트 변경
description: 원격 데스크톱 클라이언트에 대한 수신 대기 포트를 변경하는 방법을 알아봅니다.
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.topic: article
author: lizap
ms.author: elizapo
ms.date: 07/19/2018
ms.localizationpriority: medium
ms.openlocfilehash: 818ae5217d0144b2a4ec6e45f3a7757455cfabf1
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2020
ms.locfileid: "80854666"
---
# <a name="change-the-listening-port-for-remote-desktop-on-your-computer"></a>컴퓨터에서 원격 데스크톱의 수신 대기 포트 변경

>적용 대상: Windows 10, Windows 8.1, Windows 8, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2008 R2

원격 데스크톱 클라이언트를 통해 컴퓨터(Windows 클라이언트 또는 Windows Server)에 연결할 때 컴퓨터의 원격 데스크톱 기능이 정의된 수신 포트(기본적으로 3389)를 통해 연결 요청을 "수신"합니다. 레지스트리를 수정하여 Windows 컴퓨터에서 해당 수신 포트를 변경할 수 있습니다.

1. 레지스트리 편집기를 시작합니다. (검색 상자에 regedit을 입력합니다.)
2. 다음 레지스트리 하위 키로 이동합니다. HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp\PortNumber
3. **편집 > 수정**을 클릭하고 **Decimal**을 클릭합니다.
4. 새 포트 번호를 입력하고 **확인**을 클릭합니다. 
5. 레지스트리 편집기를 닫고 컴퓨터를 다시 시작합니다.

다음번에 원격 데스크톱 연결을 사용하여 이 컴퓨터에 연결할 때 새 포트를 입력해야 합니다. 방화벽을 사용하는 경우 새 포트 번호로의 연결을 허용하도록 방화벽을 구성해야 합니다.
