---
ms.assetid: 28ecaf5c-9131-406c-b211-a230162e462e
title: 일정 결정
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: dee63ce0fb687b2b722ce64614c54388fc544433
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59839004"
---
# <a name="determining-the-schedule"></a>일정 결정

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

사이트 링크 일정을 설정 하 여 사이트 링크의 가용성을 제어할 수 있습니다. 여러 개의 사이트 링크를 통과 하는 두 사이트 간의 복제를 하는 경우 모든 관련 링크의 복제 일정의 교집합 두 사이트 간 연결 일정을 결정 합니다.  
  
사이트 링크 일정을 설정 하는 것에 대 한 계획을 직접 상호 복제 하는 도메인 컨트롤러를 포함 하는 사이트 링크 간의 두 개의 겹치는 일정을 만듭니다. 복제 트래픽 사용량이 적은 시간 동안 차단 하려는 경우가 아니면 이러한 링크에서 기본값 (100% 사용 가능한) 일정을 사용 합니다. 차단 복제를 다른 트래픽 우선 순위를 부여 하지만 복제 대기 시간을 늘릴 수도 있습니다.  
  
도메인 컨트롤러 시간을 utc (협정 세계시)로 저장 합니다. 사이트 및 일정을 설정 하는 컴퓨터의 현지 시간으로 사이트 링크 개체 일정에서 시간 설정을 준수 합니다. 도메인 컨트롤러는 다른 사이트와 표준 시간대에 있는 컴퓨터에 연결 하는 경우 도메인 컨트롤러에서 일정을 컴퓨터의 사이트에 대 한 현지 시간에 따라 시간 설정이 표시 됩니다.  
  


