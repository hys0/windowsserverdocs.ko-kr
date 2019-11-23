---
title: Active Directory 관리 센터 탐색 창 사용자 지정
ms.prod: windows-server
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
ms.openlocfilehash: 63038014207acd3846cb8db20c7836718615df51
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403759"
---
# <a name="customize-the-active-directory-administrative-center-navigation-pane"></a>Active Directory 관리 센터 탐색 창 사용자 지정

>적용 대상: Windows Server(반기 채널), Windows Server 2016

  Active Directory 사용자 및 컴퓨터 콘솔 트리와 비슷한 트리 뷰를 사용 하거나 목록 뷰를 사용 하 여 Active Directory 관리 센터 탐색 창을 탐색할 수 있습니다.

 트리 보기 또는 목록 보기를 사용 하는 경우에는 로컬 도메인 또는 외부 도메인 \(의 다양 한 컨테이너를 추가 하 여 언제 든 지 Active Directory 관리 센터 탐색 창을 사용자 지정할 수 있습니다. 즉, 로컬 도메인과 함께 트러스트 관계가 설정 된 로컬 도메인과 다른 도메인\) 탐색 창에 별도의 노드로 추가 합니다. Active Directory 관리 센터 탐색 창을 사용자 지정 하면 Active Directory 개체에 보다 빠르게 액세스할 수 있습니다. 자세한 내용은 [Active Directory 관리 센터에서 다른 도메인 관리](manage-different-domains-in-active-directory-administrative-center.md)를 참조 하세요.

 또한 탐색 창을 보다 세부적으로 사용자 지정하려면 수동으로 추가한 탐색 창 노드의 이름을 바꾸거나, 해당 노드를 제거하거나, 해당 노드의 복제본을 만들거나, 해당 노드를 탐색 창에서 위 또는 아래로 이동합니다.

> [!NOTE]
>  기본 로컬 도메인 노드는 사용자 지정할 수 없습니다.

### <a name="to-customize-the-active-directory-administrative-center-navigation-pane"></a>Active Directory 관리 센터 탐색 창을 사용자 지정 하려면

1. Active Directory 관리 센터 탐색 창에서 수정할 노드를 마우스 오른쪽 단추로\-클릭 합니다. 노드의 위치 또는 이름을 수정하거나 노드의 복제본을 만들 수 있습니다.

2. 다음 명령 중 하나를 클릭 합니다.

   -   **바꾸면**

   -   **중복 노드 만들기**

   -   **제거**

   -   **위로 이동**

   -   **아래로 이동**

   목록 뷰를 사용 하 여 가장 최근에 사용한 \(MRU\) 목록을 활용할 수 있습니다. 이 탐색 노드에서 하나 이상의 컨테이너를 방문할 때 MRU 목록이 탐색 노드 아래에 자동으로 나타납니다. Active Directory 관리 센터 창 위쪽의 이동 경로 탐색 막대를 확장 하 여 현재 MRU 목록을 볼 수도 있습니다. MRU 목록에는 항상 특정 탐색 노드에서 방문한 마지막 3 개의 컨테이너가 포함 됩니다. 특정 컨테이너를 선택할 때마다 이 컨테이너가 MRU 목록의 맨 위에 추가되고 MRU 목록의 마지막 컨테이너는 제거됩니다.

  

