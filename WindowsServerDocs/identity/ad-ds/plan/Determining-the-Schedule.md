---
ms.assetid: 28ecaf5c-9131-406c-b211-a230162e462e
title: 일정 결정
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: d5c1c7c77304317bab2e80223dd745c88bc79efd
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80822546"
---
# <a name="determining-the-schedule"></a>일정 결정

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

사이트 링크에 대 한 일정을 설정 하 여 사이트 링크 가용성을 제어할 수 있습니다. 두 사이트 간의 복제가 여러 사이트 링크를 통과 하는 경우 모든 관련 링크에 대 한 복제 일정의 교집합에 따라 두 사이트 간의 연결 일정이 결정 됩니다.  
  
사이트 링크 일정을 설정 하는 계획을 수립 하려면 서로 직접 복제 하는 도메인 컨트롤러가 포함 된 사이트 링크 사이에 두 개의 겹치는 일정을 만듭니다. 사용량이 많은 시간에 복제 트래픽을 차단 하려는 경우를 제외 하 고 해당 링크에 대 한 기본 (100-% 사용 가능) 일정을 사용 합니다. 복제를 차단 하 여 다른 트래픽에 우선 순위를 부여 하지만 복제 대기 시간도 증가 합니다.  
  
도메인 컨트롤러는 UTC (협정 세계시)로 시간을 저장 합니다. 사이트 링크 개체 일정의 시간 설정은 일정이 설정 된 사이트 및 컴퓨터의 현지 시간을 따릅니다. 도메인 컨트롤러가 다른 사이트 및 표준 시간대에 있는 컴퓨터에 연결 하면 도메인 컨트롤러의 일정에 따라 컴퓨터 사이트의 현지 시간에 따라 시간 설정이 표시 됩니다.  
  


