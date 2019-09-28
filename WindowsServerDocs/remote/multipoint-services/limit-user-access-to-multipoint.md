---
title: 서버에 대 한 사용자 액세스 제한
description: 사용자 및 그룹에 대 한 MultiPoint 서비스에 대 한 액세스 권한을 부여 하거나 거부 하는 방법 알아보기
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4cabd4f1-a764-4be6-bc6e-0a5f5566390c
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 62f2a3f9b94ac3f0474636c34e8ec1f81c568cad
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71389061"
---
# <a name="limit-users-access-to-the-multipoint-server"></a>Multipoint server에 대 한 사용자 액세스 제한
MultiPoint server를 Active Directory 도메인에 가입 시키거나 로컬 사용자 계정을 사용 하 든 상관 없이 모든 사용자는 기본적으로 MultiPoint server에 액세스할 수 있습니다. 사용자가 MultiPoint 서비스 환경의 스테이션에 로그온 하도록 허용 하기 전에 서버에 대 한 액세스를 제한 해야 합니다.  
  
Remote Desktop Users 그룹의 모든 사용자는 MultiPoint server에 로그온 할 수 있습니다. 기본적으로 사용자 그룹 Everyone은 Remote Desktop Users 그룹의 구성원 이므로 모든 로컬 사용자 및 도메인 사용자는 MultiPoint Server에 로그온 할 수 있습니다. MultiPoint Server에 대 한 액세스를 제한 하려면 원격 데스크톱 사용자 그룹에서 Everyone 사용자 그룹을 제거 하 고 원격 데스크톱 사용자 그룹에 특정 사용자 또는 그룹을 추가 합니다.  
  
## <a name="add-or-remove-users-or-groups-to-the-remote-desktop-users-group"></a>원격 데스크톱 사용자 그룹에 사용자 또는 그룹 추가 또는 제거  
  
1.  **시작** 화면에서 **컴퓨터 관리**를 엽니다.  
  
2.  콘솔 트리의 **로컬 사용자 및 그룹**에서 **그룹**을 클릭 합니다.  
  
3.  **원격 데스크톱 사용자**를 두 번 클릭 하 고 지침에 따라 사용자를 추가 하거나 제거 합니다.  
  
    -   서버에 대 한 일반 액세스를 제한 하려면 Everyone 그룹을 제거 합니다.  
  
    -   MultiPoint server 사용자에 게 스테이션에 대 한 액세스 권한을 부여 하려면 각 로컬 계정이 나 각 도메인 사용자 또는 그룹 계정을 원격 데스크톱 사용자 그룹에 추가 합니다.  