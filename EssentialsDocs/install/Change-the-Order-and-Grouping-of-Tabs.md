---
title: "탭을 그룹화 및 주문 변경"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 79a417fd-1b3e-47ab-ae33-bb1faf95c86d
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 578c5619cfdf076bb2735254494f393d56d35713
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="change-the-order-and-grouping-of-tabs"></a>탭을 그룹화 및 주문 변경

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

탭 하면 탭 행의 왼쪽) (의 첫 번째 대시보드의 탭 순서를 변경할 수 있습니다. 이렇게 하려면 레지스트리에 항목을 추가 합니다. 또한 탭 그룹화 레지스트리에 항목을 추가 하 여 변경할 수 있습니다. 탭의 순서 다음 Microsoft 내장 탭을 된 추가 탭 하 고 제 3 자 탭 하 여 그 다음에 기본 탭 하면 될 수 있습니다.  
  
## <a name="change-the-order-of-the-tabs-in-the-dashboard"></a>탭 대시보드에 순서를 변경  
 레지스트리 순서를 정의 하 여 탭을 표시 하는 추가 기능의 식별자를 추가 해야 합니다.  
  
#### <a name="to-display-your-tab-first-in-the-list-of-tabs"></a>탭을 표시 하려면 사용자 먼저 탭의 목록에서  
  
1.  참조 컴퓨터에서 클릭 **시작**, 입력 **regedit**를 누른 다음 **Enter**합니다.  
  
2.  왼쪽된 창에서 확장 **HKEY_LOCAL_MACHINE**, 확장 **소프트웨어**, 확장 **Microsoft**를 확장 한 다음 **Windows Server**합니다. 하는 경우는 **OEM** 키가 없는, 새로 만드시겠습니까 다음 단계를 완료 해야 합니다.  
  
    1.  마우스 오른쪽 단추로 클릭 **Windows Server**를 가리킨 **새로**을 차례로 클릭 하 고 **키**합니다.  
  
    2.  입력 **OEM** 키의 이름입니다.  
  
3.  마우스 오른쪽 단추로 클릭 **OEM**, 가리킨 **새로**을 차례로 클릭 하 고 **문자열 값**합니다.  
  
4.  입력 **DashboardMainTabID** 문자열 이름을 선택한 다음 키를 눌러 **Enter**합니다.  
  
5.  새 문자열 오른쪽 창에서 마우스 오른쪽 단추로 클릭 하 고 클릭 한 다음 **수정**합니다.  
  
6.  최상위 탭에서 알림 영역에 대해 정의 된 GUID 입력 한 다음 **Enter**합니다.  
  
     만들고 식별 최상위 탭에 대 한 자세한 내용은 참조 [최상위 탭을 만드는](https://msdn.microsoft.com/library/gg513957) Windows Server 솔루션 sdk에서 합니다.  
  
7.  레지스트리에 변경 내용을 저장 합니다.  
  
8.  탭을 그룹화 하는 데 식별자 목록에서 사용자 주 최상위 탭에 대 한 GUID 포함 해야 합니다. 이렇게 하려면에 나열 된 단계를 수행 **대시보드에서 탭을 그룹화 변경**합니다.  
  
## <a name="change-the-grouping-of-tabs-in-the-dashboard"></a>탭 대시보드에 그룹화 변경  
 탭을 레지스트리 식별자를 추가 하 여 기본 제공 된 Microsoft 탭 목록에 포함 되어 그룹화를 확인할 수 있습니다.  
  
#### <a name="to-change-the-grouping-of-tabs"></a>탭 그룹화 변경 하려면  
  
1.  Regedit 열리지 않으면 클릭 **시작**, 입력 **regedit**를 누른 다음 **Enter**합니다.  
  
2.  왼쪽된 창에서 확장 **HKEY_LOCAL_MACHINE**, 확장 **소프트웨어**, 확장 **Microsoft**를 확장 한 다음 **Windows Server**합니다.  
  
3.  마우스 오른쪽 단추로 클릭 **OEM**를 가리킨 **새로**을 차례로 클릭 하 고 **키**합니다.  
  
4.  입력 **DashboardAddins** 키 이름을 선택한 다음 키를 눌러 **Enter**합니다.  
  
5.  마우스 오른쪽 단추로 클릭 **DashboardAddins**, 가리킨 **새로**을 차례로 클릭 하 고 **문자열 값**합니다.  
  
6.  GUID 식별자 탭에 대 한 문자열 이름으로 입력 됩니다. 값 필요 하지 않습니다.  
  
7.  각 탭 및 하위 탭에 대 한 5, 6 단계를 반복 합니다.  
  
8.  레지스트리 변경 내용을 저장 합니다.  
  
## <a name="see-also"></a>참조 하십시오  
 [만들기 및 이미지를 사용자 지정](Creating-and-Customizing-the-Image.md)   
 [추가로 사용자 지정](Additional-Customizations.md)   
 [배포에 대 한 이미지를 준비 중](Preparing-the-Image-for-Deployment.md)   
 [고객 만족도 테스트합니다.](Testing-the-Customer-Experience.md)