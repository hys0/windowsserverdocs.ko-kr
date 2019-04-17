---
title: 클라이언트 컴퓨터 설정 확인
description: 이 항목은 Windows Server 2016을 지점에서 WAN 대역폭 사용을 최적화 하 분산 / 호스팅된 캐시 모드로 BranchCache 배포 하는 방법을 보여 주는 BranchCache 배포 가이드
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 31ea58b0-d407-4f62-8ec6-6a1b19174042
ms.author: pashort
author: shortpatti
ms.openlocfilehash: d507f2097a9349cbefba520ad0dc143e0dd7452e
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="verify-client-computer-settings"></a>클라이언트 컴퓨터 설정 확인

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 절차 클라이언트 컴퓨터 BranchCache에 대해 올바르게 구성 되어 있는지 확인 하기 위해 사용할 수 있습니다.  
  
> [!NOTE]  
> 이 절차 그룹 정책 수동으로 업데이트 하 고 BranchCache 서비스를 다시 시작 단계 포함 되어 있습니다. 이 경우 자동으로 수행 됩니다와 컴퓨터를 다시 부팅 하는 경우 이러한 작업을 수행할 필요가 없습니다.  
  
소속 있어야 **관리자**, 나이 절차를 수행 하는 것과 같습니다.  
  
### <a name="to-verify-branchcache-client-computer-settings"></a>BranchCache 클라이언트 컴퓨터 설정을 확인 하려면  
  
1.  그룹 정책을 가지의 BranchCache 구성을 확인 새로 Windows PowerShell을 관리자 권한으로 실행 다음 명령을 입력 하 고 enter 합니다.  
  
    `gpupdate /force`  
  
2.  호스트 캐시 모드로 구성 하 고 구성 하는 컴퓨터에 자동으로 검색 하는 데 주관 캐시 서버 서비스 연결 지점에 중지 되 고 BranchCache 서비스를 다시 시작 뒤 다음 명령을 실행 합니다.  
  
    `net stop peerdistsvc`  
  
    `net start peerdistsvc`  
  
3.  다음 명령을 실행 하 여 현재 BranchCache 작동 모드를 검사 합니다.  
  
    `Get-BCStatus`  
  
4.  Windows PowerShell 출력을 검토 하 고 **Get BCStatus** 명령을 합니다.  
  
    에 대 한 값 **BranchCacheIsEnabled** 있어야 **진정한**합니다.  
  
    **ClientSettings**에 대 한 값 **CurrentClientMode** 있어야 **DistributedClient** 또는 **HostedCacheClient**모드가이 가이드를 사용 하 여 구성에 따라 합니다.  
  
    **ClientSettings**구성 호스트 캐시 모드를 구성 하는 동안 여 호스팅된 캐시 서버 이름 제공 하거나 클라이언트는 자동으로 있는 경우 캐시 서버 서비스 연결 포인트를 사용 하 여 호스팅된, **HostedCacheServerList** 이름 또는 호스트 캐시 서버 이름이 같은 않은 있어야 합니다. 예를 들어 HCS1 및 도메인 여 호스팅된 캐시 서버 라는에 대 한 값 corp.contoso.com **HostedCacheServerList** 는 **HCS1.corp.contoso.com**합니다.  
  
5.  위에 나열 된 설정을 BranchCache 중 하나로 올바르지 값이이 가이드의 단계를 사용 하 여 그룹 정책 또는 컴퓨터 정책을 로컬 설정을 구성한, 방화벽 예외를 확인 하 고 있는지 없는 경우 올바른 됩니다. 또한 컴퓨터를 다시 시작 하거나이 절차 그룹 정책 복구 BranchCache 서비스를 다시 시작 하는 단계를 수행 합니다.  
  


