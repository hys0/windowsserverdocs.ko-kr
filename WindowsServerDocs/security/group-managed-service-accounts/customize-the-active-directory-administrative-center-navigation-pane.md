---
title: "관리 센터 Active Directory 탐색 창 사용자 지정"
ms.prod: windows-server-threshold
description: "Windows Server 보안"
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
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="customize-the-active-directory-administrative-center-navigation-pane"></a>관리 센터 Active Directory 탐색 창 사용자 지정

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

  You can browse through the Active Directory Administrative Center navigation pane by using the tree view, which is similar to the Active Directory Users and Computers console tree, or by using the list view.

 Whether you use the tree view or the list view, you can customize your Active Directory Administrative Center navigation pane anytime by adding various containers from the local domain or any foreign domain \(that is, a domain other than the local domain that has an established trust with the local domain\) to the navigation pane as separate nodes. Customizing the Active Directory Administrative Center navigation pane can provide quicker access to Active Directory objects. 자세한 내용은 참조 [Active Directory 관리 센터에서 다른 도메인 관리](manage-different-domains-in-active-directory-administrative-center.md)합니다.

 또한, 탐색 창을 추가로 사용자 지정 하려면 이름 바꾸기 또는 이러한 수동으로 추가 탐색 창 노드 제거, 이러한 노드 복제 만들기 하거나 이동할 수 위나 아래로 탐색 창에서 합니다.

> [!NOTE]
>  기본 로컬 도메인 노드 사용자 지정할 수 없습니다.

### <a name="to-customize-the-active-directory-administrative-center-navigation-pane"></a>To customize the Active Directory Administrative Center navigation pane

1.  In the Active Directory Administrative Center navigation pane, right\-click the node that you want to modify. 위치나 노드를 수정할 수 또는 그의 복사본을 만들 수 있습니다.

2.  다음 명령을 중 하나를 클릭 합니다.

    -   **이름 바꾸기**

    -   **중복 노드 만들기**

    -   **제거**

    -   **위로 이동**

    -   **아래로 이동**

 목록 보기를 사용 하 여 최근에 사용한 \(MRU\) 목록 이용할 수 있습니다. 최근에 사용한 목록 자동으로 사용자가 방문이 탐색 노드에서 하나 이상의 컨테이너 탐색 노드 아래에 나타납니다. You can also view the current MRU list by expanding the breadcrumb bar at the top of the Active Directory Administrative Center window. 최근에 사용한 목록에 특정 탐색 노드에서 방문 마지막 사진 3 컨테이너 항상 포함 되어 있습니다. 특정 컨테이너 선택 해야 할 때마다가이 컨테이너 최근에 사용한 목록의 맨 위로에 추가 되 고 마지막 컨테이너 최근에 사용한 목록에서 제거 됩니다.

  

