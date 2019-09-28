---
title: 서버 그룹 만들기 및 관리
description: 서버 관리자
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-server-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9d5b1be8-49fd-4ff7-9580-e4ff21fe4b17
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 74075f091cd707f6faf73567c1dce6f22a2f6753
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71383223"
---
# <a name="create-and-manage-server-groups"></a>서버 그룹 만들기 및 관리

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 Windows 서버에서 서버 관리자의 사용자 지정, 사용자 정의 서버 그룹을 만드는 방법에 설명 합니다.

## <a name="BKMK_groups"></a>서버 그룹
서버 풀에 추가 하는 서버에 표시 되는 **모든 서버** 서버 관리자의 페이지입니다. 추가한 서버의 사용자 지정 그룹을 만들 수 있습니다. 서버 그룹을 사용 하면 보고를 논리 단위로 서버 풀의 작은 하위 집합을 관리 하려면 예를 들어 라는 그룹을 만들 수 있습니다 **Accounting Servers** 조직에서 모든 서버에 대 한의 회계 부서 또는 그룹 이라는 **시카고** 시카고에 위치한 모든 서버에 대 한 합니다. 서버 그룹을 만든 후 그룹의 서버 관리자의 홈 페이지 이벤트, 서비스, 성능 카운터, 모범 사례 분석기 결과 대 한 정보를 표시 하 고 전체적으로 역할 및 그룹에 대 한 기능을 설치 합니다.

서버는 둘 이상의 그룹에 속할 수 있습니다.

#### <a name="to-create-a-new-server-group"></a>새 서버 그룹을 만들려면

1.  **관리** 메뉴에서 **서버 그룹 만들기**를 클릭 합니다.

2.  **서버 그룹 이름** 텍스트 상자에 **Accounting Servers**와 같이 친숙한 서버 그룹의 이름을 입력합니다.

3.  서버 풀에서 **선택** 된 목록에 서버를 추가 하거나 **active directory**, **DNS**또는 **가져오기** 탭을 사용 하 여 다른 서버를 그룹에 추가 합니다. 이러한 탭을 사용 하는 방법에 대 한 자세한 내용은이 가이드의 [서버 관리자에 서버 추가](add-servers-to-server-manager.md) 를 참조 하세요.

4.  그룹에 서버 추가를 마쳤으면 **확인**을 클릭합니다. 새 그룹의 서버 관리자 탐색 창에 표시 됩니다는 **모든 서버** 그룹입니다.

#### <a name="to-edit-an-existing-server-group"></a>기존 서버 그룹을 편집하려면

1.  다음 중 하나를 수행합니다.

    -   서버 관리자 탐색 창에서 서버 그룹을 마우스 오른쪽 단추로 클릭 한 다음 **서버 그룹 편집**을 클릭 합니다.

    -   서버 그룹에 대 한 홈 페이지의 **서버** 타일에서 **작업** 메뉴를 연 다음 **서버 그룹 편집**을 클릭 합니다.

2.  그룹 이름을 변경 하거나 그룹에서 서버를 추가 또는 제거 합니다.

    > [!NOTE]
    > 서버 그룹에서 서버를 제거 해도 서버 관리자에서 서버가 제거 되지는 않습니다. 그룹에서 제거된 서버는 **모든 서버** 그룹의 서버 풀에 유지됩니다.

3.  그룹 변경을 마쳤으면 **확인**을 클릭합니다.

#### <a name="to-delete-an-existing-server-group"></a>기존 서버 그룹을 삭제하려면

1.  다음 중 하나를 수행합니다.

    -   서버 관리자 탐색 창에서 서버 그룹을 마우스 오른쪽 단추로 클릭 한 다음 **서버 그룹 삭제**를 클릭 합니다.

    -   서버 그룹에 대 한 홈 페이지의 **서버** 타일에서 **작업** 메뉴를 연 다음 **서버 그룹 삭제**를 클릭 합니다.

2.  서버 그룹을 삭제할 것인지 묻는 메시지가 표시되면 **예**를 클릭합니다.

    > [!NOTE]
    > 서버 그룹을 삭제 해도 서버 관리자에서 서버가 제거 되지 않습니다. 삭제된 그룹에 있던 서버는 **모든 서버** 그룹의 서버 풀에 유지됩니다.

3.  그룹 변경을 마쳤으면 **확인**을 클릭합니다.

## <a name="see-also"></a>관련 항목
[서버 관리자 @no__t에 서버 추가](add-servers-to-server-manager.md)-1[서버 관리자](server-manager.md)



