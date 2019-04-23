---
title: Windows PowerShell을 사용 하 여 비-도메인 구성원 클라이언트 컴퓨터를 구성 하려면
description: 이 항목은 일부는 BranchCache 배포 가이드에 대 한 Windows Server 2016, 지사에 WAN 대역폭 사용량을 최적화 하기 위해 분산 및 호스트 캐시 모드로 BranchCache를 배포 하는 방법을 보여 주는
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 1b511e1a-686d-441f-a1c7-d4d029e1a061
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 9abb77e573d7b3f144ab831c655c81370a4a6af1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59839954"
---
# <a name="use-windows-powershell-to-configure-non-domain-member-client-computers"></a>Windows PowerShell을 사용 하 여 비-도메인 구성원 클라이언트 컴퓨터를 구성 하려면

>적용 대상: Windows Server (반기 채널), Windows Server 2016

호스트 캐시 모드 하거나 수동으로 분산된 캐시 모드로 BranchCache 클라이언트 컴퓨터를 구성 하려면이 절차를 사용할 수 있습니다.  
  
> [!NOTE]  
> 그룹 정책을 사용 하 여 BranchCache 클라이언트 컴퓨터를 구성한 경우 그룹 정책 설정은 정책이 적용 되는 클라이언트 컴퓨터를 수동으로 구성 하는 모든 문서를 무시 합니다.  
  
멤버 자격이 **관리자**, 또는 이와 동등한이 절차를 수행 하는 데 필요한 최소값입니다.  
  
### <a name="to-enable-branchcache-distributed-or-hosted-cache-mode"></a>BranchCache 분산 또는 호스트 캐시 모드를 사용 하도록 설정 하려면  
  
1.  BranchCache 클라이언트 컴퓨터를 구성 하려면에서 관리자는 Windows PowerShell을 실행 하 고 후 다음 중 하나를 수행 합니다.  
  
    -   BranchCache 분산된 캐시 모드 클라이언트 컴퓨터를 구성 하려면 다음 명령을 입력 한 다음 ENTER 키를 누릅니다.  
  
        `Enable-BCDistributed`  
  
    -   BranchCache 호스트 캐시 모드 클라이언트 컴퓨터를 구성 하려면 다음 명령을 입력 한 다음 ENTER 키를 누릅니다.  
  
        `Enable-BCHostedClient`  
  
        > [!TIP]  
        > 사용 가능한 호스트 캐시 서버를 지정 하려는 경우 사용 하 여는 `-ServerNames` 매개 변수를 쉼표로 구분 된 매개 변수 값으로 호스트 캐시 서버 목록이 있습니다. 예를 들어 HCS1 및 HCS2 라는 두 명의 호스트 캐시 서버를 설정한 다음 명령을 사용 하 여 호스트 캐시 모드 클라이언트 컴퓨터를 구성 합니다.  
        >   
        > `Enable-BCHostedClient -ServerNames HCS1,HCS2`  
  


