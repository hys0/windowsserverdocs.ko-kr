---
title: 원격 데스크톱에서 수신 대기 포트 변경
description: 원격 데스크톱 클라이언트에 대 한 수신 대기 포트를 변경 하는 방법을 알아봅니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
author: lizap
ms.author: elizapo
ms.date: 07/19/2018
ms.localizationpriority: medium
ms.openlocfilehash: b70479b644f4984c93136d6493483c372703244d
ms.sourcegitcommit: d3f73936160505a40633ad8dd5931ac5fe3eccdb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/12/2019
ms.locfileid: "9297323"
---
# 컴퓨터에서 원격 데스크톱에 대 한 수신 대기 포트 변경

>적용 대상: Windows 10, Windows 8.1, Windows 8, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2008 R2

원격 데스크톱 클라이언트를 통해 컴퓨터 (Windows 클라이언트 또는 Windows Server)에 연결 하는 경우 컴퓨터에서 원격 데스크톱 기능 "듣게" 정의 된 수신 대기 포트를 통해 연결 요청 (기본적으로 3389). 레지스트리를 수정 하 여 Windows 컴퓨터에서 수신 대기 포트를 변경할 수 있습니다.

1. 레지스트리 편집기를 시작 합니다. (검색 상자에 regedit를 입력 합니다.)
2. 다음 레지스트리 하위 키로 이동: HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP Tcp\PortNumber
3. **Gt_ 수정 편집**을 클릭 하 고 **10 진수**를 클릭 합니다.
4. 새 포트 번호를 입력 한 후 **확인**을 클릭 합니다. 
5. 레지스트리 편집기를 닫고 컴퓨터를 다시 시작 합니다.

원격 데스크톱 연결을 사용 하 여이 컴퓨터에 연결한 다음에 새 포트를 입력 해야 합니다. 방화벽을 사용 하는 경우 새 포트 번호에 연결을 허용 하도록 방화벽을 구성 해야 합니다.
