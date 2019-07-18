---
title: Windows 관리 센터 게이트웨이의 모든 사용자에 대 한 공유 연결 구성
description: 관리자가 Windows 관리 센터 (Project Honolulu) 게이트웨이를 한 번 구성 하 여 모든 사용자가 단일 연결 목록을 공유 하도록 하는 방법을 알아봅니다.
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 03/28/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 46075154a225590376458881768ae86f74a572ad
ms.sourcegitcommit: 286e3181ebd2cb9d7dc7fe651858a4e0d61d153f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/17/2019
ms.locfileid: "68300722"
---
# <a name="configure-shared-connections-for-all-users-of-the-windows-admin-center-gateway"></a>Windows 관리 센터 게이트웨이의 모든 사용자에 대 한 공유 연결 구성

> 적용 대상: Windows 관리 센터 미리 보기, Windows 관리 센터

공유 연결을 구성 하는 기능을 사용 하 여 게이트웨이 관리자는 지정 된 Windows 관리 센터 게이트웨이의 모든 사용자에 대해 연결 목록을 한 번 구성할 수 있습니다. 

Windows 관리 센터 게이트웨이 설정의 **공유 연결** 탭에서 게이트웨이 관리자는 연결 태그를 지정할 수 있는 기능을 비롯 하 여 모든 연결 페이지에서와 같이 서버, 클러스터 및 PC 연결을 추가할 수 있습니다. 공유 연결 목록에 추가 된 모든 연결 및 태그는 모든 연결 페이지에서이 Windows 관리 센터 게이트웨이의 모든 사용자에 게 표시 됩니다.
    ![](../media/shared-cnxns-1.png)

공유 연결이 구성 된 후 Windows 관리 센터 사용자가 "모든 연결" 페이지에 액세스 하는 경우 다음 두 섹션으로 그룹화 된 연결이 표시 됩니다. 개인 및 공유 연결. 개인 그룹은 특정 사용자의 연결 목록이 며 해당 사용자의 브라우저 세션에서 지속 됩니다. 공유 연결 그룹은 모든 사용자에 대해 동일 하며, 모든 연결 페이지에서 수정할 수 없습니다.
![](../media/shared-cnxns-2.png)