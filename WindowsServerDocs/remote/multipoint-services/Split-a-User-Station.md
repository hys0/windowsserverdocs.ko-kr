---
title: 사용자 스테이션 분할
description: 두 명의 사용자가 동일한 스테이션을 사용할 수 있도록 MultiPoint 서비스에서 디스플레이를 분할 하는 방법을 알아봅니다.
ms.custom: na
ms.date: 07/08/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f0d1fc9c-f5ea-45bc-a8da-623c5d081cdf
author: lizap
manager: dongill
ms.author: elizapo
ms.openlocfilehash: 5067df3f5902570d56ee130264c751d66b5b0d3f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71394954"
---
# <a name="split-a-user-station"></a>사용자 스테이션 분할
해상도가 1024x768 이상인 모든 MultiPoint 서비스 스테이션 모니터는 **스테이션** 탭의 **스테이션 분할** 작업을 사용하여 두 스테이션으로 분할할 수 있습니다. 분할이 이루어질 때 모니터에 표시되어 있던 데스크톱은 모니터의 왼쪽 반으로 이동되고 새로운 스테이션이 동일한 모니터의 오른쪽 반에 생성됩니다. 이러한 분할 생성을 완료하려면 새로운 스테이션을 키보드, 마우스 및 USB 허브에 매핑해야 합니다. 스테이션이 분할되면 한 사용자가 왼쪽 스테이션에 로그온한 상태에서 다른 사용자가 오른쪽 스테이션에 로그온할 수 있습니다.  
  
화면 분할 스테이션 사용의 이점 포함 될 수 있습니다.  
  
-   MultiPoint 서비스 시스템에서 더 많은 학생을 수용하여 비용 절감 및 공간 절약  
  
-   두 학생 함께 나란히 프로젝트에서 공동 작업을 허용 합니다.  
  
-   교사는 한 스테이션에서 절차를 보여 주고 동시에 학생은 다른 스테이션에서 이를 따라 수행할 수 있음  
   
> [!NOTE]  
> 스테이션을 분할할 때 스테이션의 활성 세션이 일시 중단됩니다. 따라서 사용자는 분할이 완료된 후 스테이션에 다시 로그온하여 작업을 다시 시작해야 합니다.  
  
**스테이션을 분할 하려면:**  
  
1.  다중 포인트 관리자에서 클릭에 스테이션 모드에는 **스테이션** 탭 합니다.  
  
2.  **스테이션** 열에서 분할하려는 스테이션 이름을 클릭합니다.  
  
3.  **스테이션 작업**에서 **스테이션 분할**을 클릭합니다.  
  
**분할 스테이션을 단일 스테이션으로 반환 하려면:**  
  
1.  다중 포인트 관리자에서 클릭에 스테이션 모드에는 **스테이션** 탭 합니다.  
  
2.  **스테이션** 열에서 분할을 끝내려는 스테이션 이름을 클릭합니다.  
  
3.  **스테이션 작업**에서 **스테이션 분할 해제**를 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
[사용자 스테이션 관리](Manage-User-Stations.md)