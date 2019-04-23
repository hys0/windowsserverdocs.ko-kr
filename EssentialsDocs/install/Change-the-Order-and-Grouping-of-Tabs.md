---
title: 탭 순서 및 그룹화 변경
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59887764"
---
# <a name="change-the-order-and-grouping-of-tabs"></a>탭 순서 및 그룹화 변경

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

탭 행에서 사용자 탭이 왼쪽에서 첫 번째 탭이 되도록 대시보드에서 탭의 순서를 변경할 수 있습니다. 이를 위해 레지스트리에 항목을 추가합니다. 레지스트리에 항목을 추가하여 탭의 그룹에 영향을 줄 수도 있습니다. 탭 순서는 사용자의 주 탭, Microsoft 기본 제공 탭, 사용자의 추가 탭, 타사 탭 순서대로 나타날 수 있습니다.  
  
## <a name="change-the-order-of-the-tabs-in-the-dashboard"></a>대시보드에서 탭 순서 변경  
 순서를 정의하려면 레지스트리에 사용자 탭을 표시하는 추가 기능인 식별자를 추가해야 합니다.  
  
#### <a name="to-display-your-tab-first-in-the-list-of-tabs"></a>탭 목록에 사용자 탭을 제일 먼저 표시하려면  
  
1.  참조 컴퓨터에서 **시작**을 클릭하고 **regedit**를 입력한 다음 **Enter**키를 누릅니다.  
  
2.  왼쪽 창에서 **HKEY_LOCAL_MACHINE**, **소프트웨어**, **Microsoft**, **Windows Server**를 차례로 확장합니다. **OEM** 키가 없으면 다음 단계를 수행하여 만들어야 합니다.  
  
    1.  **Windows Server**를 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 가리킨 다음 **키**를 클릭합니다.  
  
    2.  키 이름에 **OEM**을 입력합니다.  
  
3.  **OEM**을 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 가리킨 다음 **문자열 값**을 클릭합니다.  
  
4.  문자열 이름에 **DashboardMainTabID**를 입력한 다음 **Enter** 키를 누릅니다.  
  
5.  오른쪽 창에서 새 문자열을 마우스 오른쪽 단추로 클릭한 다음 **수정**을 클릭합니다.  
  
6.  최상위 탭에 대해 정의된 GUID를 입력한 다음 **Enter**키를 누릅니다.  
  
     최상위 탭을 만들고 식별하는 방법에 대한 자세한 내용은 Windows Server Solutions SDK에서 [최상위 탭 만들기](https://msdn.microsoft.com/library/gg513957) 를 참조하세요.  
  
7.  레지스트리에 변경 사항을 저장합니다.  
  
8.  탭을 그룹화하려면 식별자 목록에 사용자의 최상위 수준의 주 탭에 대한 GUID를 포함해야 합니다. 이렇게 하려면 **대시보드에서 탭의 그룹화 변경**에 나열된 단계를 수행합니다.  
  
## <a name="change-the-grouping-of-tabs-in-the-dashboard"></a>대시보드에서 탭의 그룹화 변경  
 레지스트리에 식별자를 추가하여 사용자 탭이 함께 그룹화되고 Microsoft 기본 제공 탭 목록에 포함되었는지 확인할 수 있습니다.  
  
#### <a name="to-change-the-grouping-of-tabs"></a>탭 그룹화를 변경하려면  
  
1.  regedit가 열려 있지 않으면 **시작**을 클릭하고 **regedit**를 입력한 다음 **Enter** 키를 누릅니다.  
  
2.  왼쪽 창에서 **HKEY_LOCAL_MACHINE**, **소프트웨어**, **Microsoft**, **Windows Server**를 차례로 확장합니다.  
  
3.  **OEM**을 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 가리킨 다음 **키**를 클릭합니다.  
  
4.  키 이름에 **DashboardAddins**를 입력한 다음 **Enter** 키를 누릅니다.  
  
5.  **DashboardAddins**를 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 가리킨 다음 **문자열 값**을 클릭합니다.  
  
6.  문자열 이름으로 사용자 탭의 GUID 식별자를 입력합니다. 값은 필요하지 않습니다.  
  
7.  사용자 탭 및 하위 탭 각각에 대해 5단계와 6단계를 반복합니다.  
  
8.  레지스트리 변경 사항을 저장합니다.  
  
## <a name="see-also"></a>관련 항목  
 [만들기 및 이미지를 사용자 지정](Creating-and-Customizing-the-Image.md)   
 [추가 사용자 지정](Additional-Customizations.md)   
 [배포용 이미지 준비](Preparing-the-Image-for-Deployment.md)   
 [사용자 환경 테스트](Testing-the-Customer-Experience.md)