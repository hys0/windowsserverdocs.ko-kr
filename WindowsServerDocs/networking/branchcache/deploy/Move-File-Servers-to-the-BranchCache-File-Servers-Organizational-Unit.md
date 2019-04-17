---
title: 파일 서버 BranchCache 파일 서버 조직에 이동
description: 이 항목은 Windows Server 2016을 지점에서 WAN 대역폭 사용을 최적화 하 분산 / 호스팅된 캐시 모드로 BranchCache 배포 하는 방법을 보여 주는 BranchCache 배포 가이드
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 56c915ec-edb1-43b0-8ad2-c93841bb566f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 09afb4936545cb1f5bb14573261008ff18badd4d
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="move-file-servers-to-the-branchcache-file-servers-organizational-unit"></a>파일 서버 BranchCache 파일 서버 조직에 이동

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

Active Directory 도메인 서비스 (AD DS)의 BranchCache 파일 서버 조직 (OU)를 추가 하려면이 절차를 사용할 수 있습니다.  
  
회원 **도메인 관리자**, 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.  
  
> [!NOTE]  
> 이 절차를 컴퓨터에 계정 추가 하기 전에 Active Directory 사용자와 컴퓨터 콘솔에는 BranchCache 파일 서버 만들어야 합니다. 자세한 내용은 참조 [BranchCache 파일 서버 조직 단위 만들](../../branchcache/deploy/Create-the-BranchCache-File-Servers-Organizational-Unit.md)합니다.  
  
### <a name="to-move-file-servers-to-the-branchcache-file-servers-organizational-unit"></a>으로 이동 하려면 파일 서버에는 BranchCache 파일 서버 조직  
  
1.  AD DS 설치 되어 있는, 서버 관리자는 컴퓨터에서 클릭 **도구**을 차례로 클릭 하 고 **Active Directory 사용자 및 컴퓨터**합니다. 콘솔 Active Directory 사용자 및 컴퓨터 엽니다.  
  
2.  Active Directory 사용자와 컴퓨터 콘솔에서 계정을 선택 하 고 다음 끌어서 놓기 컴퓨터 계정에는 BranchCache 파일 서버 이전에 만든 왼쪽 클릭 BranchCache 파일 서버에 대 한 계정을 찾습니다. 예를 들어, 라는 OU 이전에 만든 **BranchCache 파일 서버**, 끌어서 컴퓨터 계정에는 **BranchCache 파일 서버** OU 합니다.  
  
3.  도메인에 있는를 이동 하려면 각 BranchCache 파일 서버에 대 한 위의 단계를 반복 합니다.  
  


