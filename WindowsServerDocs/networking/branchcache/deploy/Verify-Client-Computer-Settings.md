---
title: 클라이언트 컴퓨터 설정 확인
description: 이 항목은 일부는 BranchCache 배포 가이드에 대 한 Windows Server 2016, 지사에 WAN 대역폭 사용량을 최적화 하기 위해 분산 및 호스트 캐시 모드로 BranchCache를 배포 하는 방법을 보여 주는
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 31ea58b0-d407-4f62-8ec6-6a1b19174042
ms.author: lizross
author: eross-msft
ms.openlocfilehash: e4bd3c4d4b2998f5c4faea22887bdef8663587cb
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80319174"
---
# <a name="verify-client-computer-settings"></a>클라이언트 컴퓨터 설정 확인

>적용 대상: Windows Server(반기 채널), Windows Server 2016

BranchCache에 대 한 클라이언트 컴퓨터가 올바르게 구성 되었는지 확인 하려면이 절차를 사용할 수 있습니다.  
  
> [!NOTE]  
> 이 절차는 수동으로 업데이트 하는 그룹 정책에 대 한 BranchCache 서비스를 다시 시작 하는 단계를 포함 합니다. 이 경우에 자동으로 수행 됩니다 컴퓨터를 다시 부팅 해야 하는 경우 이러한 작업을 수행할 필요가 없습니다.  
  
멤버 여야 **관리자**, 하거나이 절차를 수행 하려면 해당 합니다.  
  
### <a name="to-verify-branchcache-client-computer-settings"></a>BranchCache 클라이언트 컴퓨터 설정을 확인 하려면  
  
1.  BranchCache 구성을 확인 하려면 클라이언트 컴퓨터에서 그룹 정책을 새로 고치려면, 관리자 권한으로 Windows PowerShell을 실행 하 고 다음 명령을 입력 한 다음 ENTER 키를 누릅니다.  
  
    `gpupdate /force`  
  
2.  호스트 캐시 모드로 구성 되어 있고 구성 하는 클라이언트 컴퓨터를 자동으로 검색할 호스트 캐시 서버를 중지 하 고 BranchCache 서비스를 다시 시작 하려면 다음 명령을 실행 하는 서비스 연결 지점에 합니다.  
  
    `net stop peerdistsvc`  
  
    `net start peerdistsvc`  
  
3.  다음 명령을 실행 하 여 현재 BranchCache 운영 모드를 검사 합니다.  
  
    `Get-BCStatus`  
  
4.  Windows PowerShell에서의 출력을 검토는 **Get BCStatus** 명령입니다.  
  
    에 대 한 값 **BranchCacheIsEnabled** 해야 **True**합니다.  
  
    **ClientSettings**, 에 대 한 값 **CurrentClientMode** 해야 **DistributedClient** 또는 **HostedCacheClient**, 이 가이드를 사용 하 여을 구성 하는 모드에 따라 합니다.  
  
    **ClientSettings**, 호스트 캐시 모드를 구성 하 고 구성 하는 동안 호스트 캐시 서버의 이름을 제공 하거나 클라이언트에 자동으로 배치 된 경우 호스트 캐시 서버 서비스 연결 지점을 사용 하는 경우, **HostedCacheServerList** 이름 또는 호스트 캐시 서버 이름이 동일 하는 값이 있어야 합니다. 예를 들어, 호스트 캐시 서버 HCS1 및 사용자의 도메인 이름이 corp.contoso.com 인 경우에 대 한 값 **HostedCacheServerList** 는 **HCS1.corp.contoso.com**합니다.  
  
5.  올바른 값으로 그룹 정책 또는 로컬 컴퓨터 정책 설정, 구성 된 방화벽 예외를 확인 하려면이 가이드의 단계를 사용 하 고 있는지 확인 하지 않은 설정은 위에 나열 된 BranchCache의 정확한 수 있습니다. 또한 컴퓨터를 다시 시작 하거나 그룹 정책을 새로 고치려면 BranchCache 서비스를 다시 시작 하는이 절차의 단계를 수행 합니다.  
  


