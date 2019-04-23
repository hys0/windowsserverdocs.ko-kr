---
title: 서버에 대 한 사용자 액세스를 제한 합니다.
description: 권한을 부여 하거나 MultiPoint 서비스 사용자 및 그룹에 대 한 액세스를 거부 하는 방법을 알아봅니다
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4cabd4f1-a764-4be6-bc6e-0a5f5566390c
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 1466e19152847a6c7d88f77162c50ec73a5a7d27
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59830814"
---
# <a name="limit-users-access-to-the-multipoint-server"></a>Multipoint 서버에 대 한 사용자 액세스를 제한 합니다.
Active Directory 도메인에 MultiPoint 서버를 가입 또는 로컬 사용자 계정을 사용 하는지 여부를 모든 사용자는 기본적으로 MultiPoint 서버에 대 한 액세스를 갖습니다. MultiPoint 서비스 환경에서 스테이션에 로그온 하는 사용자를 허용 하기 전에 서버에 액세스를 제한 해야 합니다.  
  
Remote Desktop Users 그룹의 모든 사용자가 MultiPoint 서버에 로그온 수 있습니다. Everyone 사용자 그룹을 기본적으로 Remote Desktop Users 그룹의 구성원이 며 따라서 모든 로컬 사용자 및 도메인 사용자에 로그온 할 수는 MultiPoint Server. MultiPoint 서버에 액세스를 제한 하는 모든 사용자가 Remote Desktop Users 그룹에서 그룹화 하 고 다음 Remote Desktop Users 그룹에 특정 사용자 또는 그룹을 추가 하는 사용자를 제거 합니다.  
  
## <a name="add-or-remove-users-or-groups-to-the-remote-desktop-users-group"></a>사용자 또는 그룹의 원격 데스크톱 사용자 그룹을 추가 또는 제거  
  
1.  **시작** 화면이 열리면서 **컴퓨터 관리**합니다.  
  
2.  콘솔 트리에서 아래 **로컬 사용자 및 그룹**, 클릭 **그룹**합니다.  
  
3.  두 번 클릭 **Remote Desktop Users**, 사용자를 추가 하거나 제거 지침을 따릅니다.  
  
    -   서버에 대 한 일반 액세스를 제한 하려면 Everyone 그룹를 제거 합니다.  
  
    -   액세스 권한을 부여 하려면 MultiPoint 서버 사용자 스테이션에서 Remote Desktop Users 그룹에 각 로컬 계정 또는 각 도메인 사용자 또는 그룹 계정을 추가 합니다.  