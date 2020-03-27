---
title: BranchCache 디자인 선택
description: 이 항목은 일부는 BranchCache 배포 가이드에 대 한 Windows Server 2016, 지사에 WAN 대역폭 사용량을 최적화 하기 위해 분산 및 호스트 캐시 모드로 BranchCache를 배포 하는 방법을 보여 주는
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 86c1ccad-2aa4-40fe-84c1-f77c49eb1216
ms.author: lizross
author: eross-msft
ms.openlocfilehash: ca605589d28811f96296f2ff865e8ae6923304c3
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80319111"
---
# <a name="choosing-a-branchcache-design"></a>BranchCache 디자인 선택

>적용 대상: Windows Server(반기 채널), Windows Server 2016

BranchCache 모드에 대해 자세히 알아보려면 및 배포에 대 한 가장 모드를 선택 하려면이 항목을 사용할 수 있습니다.  
  
다음과 같은 모드 및 모드 조합에서 BranchCache를 배포 하려면이 가이드를 사용할 수 있습니다.  
  
-   모든 지사의 분산된 캐시 모드로 구성 됩니다.  
  
-   모든 지사의 호스트 캐시 모드로 구성 되어 있고 사이트에서 호스트 캐시 서버.  
  
-   분산된 캐시 모드로 구성 된 일부 지점 및 일부 지점 호스트 캐시 서버 사이트에 있으며 해당 호스트 캐시 모드로 구성 됩니다.  
  
다음 그림은 분산된 캐시 모드로 구성 된 하나의 지사와 호스트 캐시 모드로 구성 된 하나의 지점으로는 이중 모드 설치를 보여 줍니다.  
  
![BranchCache 디자인 선택](../../media/Choosing-a-BranchCache-Design/bc_new_modes.jpg)  
  
BranchCache를 배포 하기 전에 조직에서 각 지사에 대해 선호 하는 모드를 선택 합니다.  
  


