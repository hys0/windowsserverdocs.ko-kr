---
title: 원격 액세스 서버에서 기존 부하 모니터링
description: 이 항목은 원격 액세스 모니터링 및 계정 관리에 Windows Server 2016에 대 한 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 62fa2895-62ae-42cf-817c-53e06ac2a26c
ms.author: pashort
author: shortpatti
ms.openlocfilehash: a1f47273ab3be6faa762df2fb90d6486bc0ed2d5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849024"
---
# <a name="monitor-the-existing-load-on-the-remote-access-server"></a>원격 액세스 서버에서 기존 부하 모니터링

>적용 대상: Windows Server (반기 채널), Windows Server 2016

**참고:** Windows Server 2012에는 DirectAccess와 RRAS(Routing and Remote Access Service)가 단일 원격 액세스 역할로 통합되어 있습니다.  
  
용어 **부하** 원격 액세스 서버에서 연결의 수와 관련 된 통계를 의미 합니다. 다음은 원격 액세스 서버에 부하를 추적 하는 데 필요한 단계입니다.  
  
서버에 대 한 부하 통계를 보려면 원격 액세스 서버에서 관리 콘솔에서 사용할 수 있는 모니터링 대시보드를 사용 하려면 또는 성능 모니터 카운터를 사용 하 여 통계를 추적 합니다.  
  
> [!NOTE]  
> 이 항목에 설명 된 작업을 완료 하려면 Domain Admins 그룹의 구성원 또는 각 컴퓨터에서 Administrators 그룹의 구성원으로 로그인 해야 합니다. Administrators 그룹의 구성원 인 계정으로 로그인 하는 동안에 작업을 완료할 수 없는 경우에 Domain Admins 그룹의 구성원 인 계정으로 로그인 하는 동안 작업을 수행해 봅니다.  
  
#### <a name="to-use-the-monitoring-dashboard-to-monitor-the-remote-access-server-load"></a>원격 액세스 서버 로드를 모니터링 하려면 모니터링 대시보드를 사용 하 여  
  
1.  **서버 관리자**, 클릭 **도구**, 를 클릭 하 고 **원격 액세스 관리**합니다.  
  
2.  **대시보드**를 클릭하여 **원격 액세스 관리 콘솔**의 **원격 액세스 대시보드**로 이동합니다.  
  
3.  모니터링 대시보드의 알 수는 **원격 클라이언트 상태** 타일 내는 **서버 상태** 바둑판식으로 배열입니다. 이 타일 연결 되어 있는 원격 클라이언트의 총 수, 연결 된 DirectAccess 클라이언트의 총 수 및 최근 24 시간 동안에서 연결 사용자의 최대 수 등의 통계를 나열 합니다.  
  
4.  클릭할 수 **새로 고침** 아래 **작업** 상태를 다시 로드 하려면 오른쪽 창에 있습니다. 기본 새로 고침 간격을 변경 하려면 **구성 새로 고침 간격** 아래 **작업**합니다.  
  
#### <a name="to-use-the-performance-monitor-tool-to-monitor-performance-counters-on-the-remote-access-server"></a>원격 액세스 서버에서 성능 카운터를 모니터링 하려면 성능 모니터 도구를 사용 하 여  
  
1.  클릭 **시작**, 클릭 **관리 도구**, 를 두 번 클릭 하 고 **성능 모니터**합니다.  
  
2.  아래에서 **성능**, 클릭 **성능 모니터**합니다.  
  
3.  클릭 된 **추가** 단추 (녹색는 십자형 아이콘으로 표시 됨)에 **성능 모니터** 도구 모음.  
  
4.  목록에서 **사용 가능한 카운터**, 선택에 있는 모든 카운터는 **RAS** 및 **RAmgmtsvc** 범주 및 클릭 한 다음 **추가 >>**.  
  
5.  목록에서 다시 **사용 가능한 카운터**, 선택에 있는 모든 카운터는 **IPsec 연결** 범주 및 클릭 한 다음 **추가 >>.**  
  
6.  클릭 **확인** 에서 선택한 카운터를 추가 하는 **성능 모니터** 추적에 대 한 콘솔입니다.  
  
**성능 모니터** 선택한 서버 부하 통계 그래픽으로 표시 됩니다.  
  
![Windows PowerShell](../../../media/Monitor-the-existing-load-on-the-Remote-Access-server/PowerShellLogoSmall.gif)Windows PowerShell 해당 명령을 * * *  
  
다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.  
  
```  
PS> Get-RemoteAccessConnectionStatisticsSummary  
```  
  


