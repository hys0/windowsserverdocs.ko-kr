---
title: Windows Admin Center 게이트웨이의 모든 사용자에 대한 공유 연결 구성
description: 관리자가 Windows Admin Center(Project Honolulu) 게이트웨이를 한 번 구성하여 모든 사용자가 단일 연결 목록을 공유하도록 하는 방법을 알아봅니다.
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 03/28/2019
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 943830a2743f7cfd3192a474eb36d57f734d3d34
ms.sourcegitcommit: 20d07170c7f3094c2fb4455f54b13ec4b102f2d7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/13/2020
ms.locfileid: "81269310"
---
# <a name="configure-shared-connections-for-all-users-of-the-windows-admin-center-gateway"></a>Windows Admin Center 게이트웨이의 모든 사용자에 대한 공유 연결 구성

> 적용 대상: Windows Admin Center 미리 보기, Windows Admin Center

게이트웨이 관리자는 공유 연결을 구성하는 기능을 사용하여 지정된 Windows Admin Center 게이트웨이의 모든 사용자에 대한 연결 목록을 한 번 구성할 수 있습니다. 이 기능은 Windows Admin Center 서비스 모드에서만 사용할 수 있습니다.

게이트웨이 관리자는 Windows Admin Center 게이트웨이 설정의 **공유 연결** 탭에서 모든 연결 페이지에서 하던 것처럼 서버, 클러스터 및 PC 연결을 추가할 수 있고 연결 태그를 지정할 수도 있습니다. 공유 연결 목록에 추가된 모든 연결 및 태그는 모든 연결 페이지에서 이 Windows Admin Center 게이트웨이의 모든 사용자에게 표시됩니다.
    ![](../media/shared-cnxns-1.png)

공유 연결이 구성된 후 Windows Admin Center 사용자가 "모든 연결" 페이지에 액세스하면 다음 두 섹션으로 그룹화된 연결이 표시됩니다. 개인 및 공유 연결. 개인 그룹은 특정 사용자의 연결 목록이며 해당 사용자의 브라우저 세션에서 지속됩니다. 공유 연결 그룹은 모든 사용자에 대해 동일하며, 모든 연결 페이지에서 수정할 수 없습니다.
![](../media/shared-cnxns-2.png)