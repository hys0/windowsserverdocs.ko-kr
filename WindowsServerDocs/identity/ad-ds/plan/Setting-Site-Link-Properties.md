---
ms.assetid: de054ac2-a386-43ec-a537-c0de21549741
title: 사이트 링크 속성 설정
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: c9a9b25aa56948e3116ebfef67a6af73917b76c2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402479"
---
# <a name="setting-site-link-properties"></a>사이트 링크 속성 설정

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

사이트 간 복제는 연결 개체의 속성에 따라 발생 합니다. 지식 일관성 검사기 (KCC)가 연결 개체를 만들 때 사이트 링크 개체의 속성에서 복제 일정을 파생 시킵니다. 각 사이트 링크 개체는 둘 이상의 사이트 간 WAN (광역 네트워크) 연결을 나타냅니다.  
  
사이트 링크 개체 속성을 설정 하는 단계는 다음과 같습니다.  
  
-   해당 복제 경로와 관련 된 비용을 확인 하는 중입니다. KCC는 동일한 디렉터리 파티션을 복제 하는 두 사이트 간의 복제를 위해 비용을 사용 하 여 가장 저렴 한 경로를 결정 합니다.  
  
-   사이트 간 복제가 발생할 수 있는 시간을 정의 하는 일정을 결정 합니다.  
  
-   일정에 정의 된 대로 복제가 허용 되는 시간 동안 복제를 수행 하는 빈도를 정의 하는 복제 간격을 결정 합니다.  
  
## <a name="in-this-guide"></a>이 가이드의 내용  
  
-   [비용 결정](../../ad-ds/plan/Determining-the-Cost.md)  
  
-   [일정 결정](../../ad-ds/plan/Determining-the-Schedule.md)  
  
-   [간격 결정](../../ad-ds/plan/Determining-the-Interval.md)  
  


