---
ms.assetid: 28ecaf5c-9131-406c-b211-a230162e462e
title: "일정을 확인"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 0ec953b34475c50e62553a9ba95e4d45d9904bf3
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="determining-the-schedule"></a>일정을 확인

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

사이트 연결에 대 한 일정을 설정 하 여 사이트 링크 사용 가능 여부를 제어할 수 있습니다. 두 개의 사이트 간의 복제 통과 여러 사이트 링크, 모든 관련 된 링크에서 복제 일정 교차로 두 사이트 간의 연결이 일정을 결정 합니다.  
  
사이트 링크 일정을 설정에 대 한 계획을 서로 바로 복제 하는 도메인 컨트롤러 포함 된 사이트 링크 간의 겹치는 두 가지 일정을 만듭니다. 최대 사용 시간에 용량이 복제 교통량을 차단 하지 않는 경우에 해당 링크 기본 (100% 사용 가능) 일정을 사용 합니다. 차단 복제 하 여 다른 교통에 우선 순위 부여 했는데 복제 대기 시간을 늘릴 수도 있습니다.  
  
도메인 컨트롤러 시간을 표준시 (협정)에 저장합니다. 로컬 시간 사이트 및 일정 설정 되어 컴퓨터의 사이트 링크 개체 일정에서 시간 설정이 준수 합니다. 다른 사이트 및 표준 시간대에는 된 컴퓨터에 연결 하는 도메인 컨트롤러를 도메인 컨트롤러에서 일정 컴퓨터의 사이트에 대 한 현지 시간에 따라 시간 설정이 표시 됩니다.  
  


