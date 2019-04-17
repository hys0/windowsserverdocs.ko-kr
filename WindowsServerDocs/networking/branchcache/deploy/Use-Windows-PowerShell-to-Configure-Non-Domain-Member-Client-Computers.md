---
title: Windows PowerShell 구성 비 도메인 구성원 클라이언트 컴퓨터를 사용 하 여
description: 이 항목은 Windows Server 2016을 지점에서 WAN 대역폭 사용을 최적화 하 분산 / 호스팅된 캐시 모드로 BranchCache 배포 하는 방법을 보여 주는 BranchCache 배포 가이드
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 1b511e1a-686d-441f-a1c7-d4d029e1a061
ms.author: pashort
author: shortpatti
ms.openlocfilehash: a5415d9fa5a4af806f23a1af9c907b1f02e9627b
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="use-windows-powershell-to-configure-non-domain-member-client-computers"></a>Windows PowerShell 구성 비 도메인 구성원 클라이언트 컴퓨터를 사용 하 여

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

캐시 모드 호스트 또는 수동으로 분산된 캐시 모드에 대 한 클라이언트 BranchCache 컴퓨터 구성 하려면이 절차를 사용할 수 있습니다.  
  
> [!NOTE]  
> 그룹 정책을 사용 하 여 BranchCache 클라이언트 컴퓨터 구성한 경우 그룹 정책 설정을 재정의 정책이 적용 되는 클라이언트 컴퓨터의 모든 수동으로 구성 합니다.  
  
회원 **관리자**, 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.  
  
### <a name="to-enable-branchcache-distributed-or-hosted-cache-mode"></a>BranchCache 분산 또는 호스트 된 캐시 모드를 사용 하도록 설정 하려면  
  
1.  BranchCache 클라이언트 컴퓨터 구성 하려면에서 Windows PowerShell을 관리자 권한으로 실행 한 후 다음 중 하나를 수행 합니다.  
  
    -   BranchCache 분산된 캐시 모드에 대 한 클라이언트 컴퓨터를 구성 하려면 다음 명령을 입력 하 고 ENTER 키를 누릅니다.  
  
        `Enable-BCDistributed`  
  
    -   호스트 BranchCache 캐시 모드에 대 한 클라이언트 컴퓨터를 구성 하려면 다음 명령을 입력 하 고 ENTER 키를 누릅니다.  
  
        `Enable-BCHostedClient`  
  
        > [!TIP]  
        > 사용 하 여 호스팅된 사용할 수 있는 캐시 서버 지정 하려는 경우는 `-ServerNames` 매개 쉼표로 구분 하 여 호스팅된 캐시 서버 매개 값 목록이 합니다. 예를 들어, 라는 HCS1 HCS2 두 호스트 캐시 서버를 사용 하는 경우 다음 명령을 사용 하 여 호스팅된 캐시 모드에 대 한 클라이언트 컴퓨터를 구성 합니다.  
        >   
        > `Enable-BCHostedClient -ServerNames HCS1,HCS2`  
  


