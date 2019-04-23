---
title: Active Directory 관리 센터 탐색 창 사용자 지정
ms.prod: windows-server-threshold
description: Windows Server 보안
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.assetid: c9933d16-e153-435a-b5b7-3e594db42d5c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: e7b1128d93912f724225905bedd38131f8aab0b2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59854844"
---
# <a name="customize-the-active-directory-administrative-center-navigation-pane"></a>Active Directory 관리 센터 탐색 창 사용자 지정

>적용 대상: Windows Server (반기 채널), Windows Server 2016

  인 Active Directory 사용자 및 컴퓨터 콘솔 트리와 비슷한 트리 뷰를 사용 하 여 또는 목록 보기를 사용 하 여 Active Directory 관리 센터 탐색 창을 통해 찾아볼 수 있습니다.

 트리 뷰 또는 목록 보기를 사용 하는지 여부를 사용자 지정할 수 있습니다 Active Directory 관리 센터 탐색 창에 언제 든 지 로컬 도메인 또는 외부 도메인에서 다양 한 컨테이너를 추가 하 여 \(즉, 로컬 도메인 이외의 도메인 로컬 도메인과 트러스트 관계가 설정된 된\) 별도 노드로 탐색 창에 있습니다. Active Directory 관리 센터 탐색 창 사용자 지정 Active Directory 개체에 대 한 빠른 액세스를 제공할 수 있습니다. 자세한 내용은 [Active Directory 관리 센터에서 다른 도메인 관리](manage-different-domains-in-active-directory-administrative-center.md)합니다.

 또한 탐색 창을 보다 세부적으로 사용자 지정하려면 수동으로 추가한 탐색 창 노드의 이름을 바꾸거나, 해당 노드를 제거하거나, 해당 노드의 복제본을 만들거나, 해당 노드를 탐색 창에서 위 또는 아래로 이동합니다.

> [!NOTE]
>  기본 로컬 도메인 노드는 사용자 지정할 수 없습니다.

### <a name="to-customize-the-active-directory-administrative-center-navigation-pane"></a>Active Directory 관리 센터 탐색 창을 사용자 지정 하려면

1.  Active Directory 관리 센터 탐색 창에서 마우스 오른쪽\-수정 하려는 노드를 클릭 합니다. 노드의 위치 또는 이름을 수정하거나 노드의 복제본을 만들 수 있습니다.

2.  다음 명령 중 하나를 클릭 합니다.

    -   **이름 바꾸기**

    -   **중복 노드 만들기**

    -   **제거**

    -   **위로 이동**

    -   **아래로 이동**

 목록 보기를 사용 하 여 가장 최근에 사용한 활용을 걸릴 수 있습니다 \(MRU\) 목록입니다. 이 탐색 노드의 하나 이상의 컨테이너를 방문 하면 MRU 목록은 탐색 노드 아래 자동으로 나타납니다. 또한 Active Directory 관리 센터 창의 맨 위에 있는 이동 경로 탐색 막대를 확장 하 여 현재 MRU 목록을 볼 수 있습니다. MRU 목록에는 항상 특정 탐색 노드를 방문 하는 마지막 세 개의 컨테이너를 포함 합니다. 특정 컨테이너를 선택할 때마다 이 컨테이너가 MRU 목록의 맨 위에 추가되고 MRU 목록의 마지막 컨테이너는 제거됩니다.

  

