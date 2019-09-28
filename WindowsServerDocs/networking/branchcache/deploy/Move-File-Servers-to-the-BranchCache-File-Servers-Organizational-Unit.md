---
title: BranchCache 파일 서버 조직 구성 단위로 파일 서버 이동
description: 이 항목은 일부는 BranchCache 배포 가이드에 대 한 Windows Server 2016, 지사에 WAN 대역폭 사용량을 최적화 하기 위해 분산 및 호스트 캐시 모드로 BranchCache를 배포 하는 방법을 보여 주는
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 56c915ec-edb1-43b0-8ad2-c93841bb566f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: ad297e25f258140fce4af3f825e362f62748c77d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71356526"
---
# <a name="move-file-servers-to-the-branchcache-file-servers-organizational-unit"></a>BranchCache 파일 서버 조직 구성 단위로 파일 서버 이동

>적용 대상: Windows Server(반기 채널), Windows Server 2016

Active Directory 도메인 서비스 (AD DS)에서 BranchCache 파일 서버에 조직 구성 단위 (OU)를 추가 하려면이 절차를 사용할 수 있습니다.  
  
멤버 자격이 **Domain Admins**, 또는 이와 동등한 최소한이이 절차를 수행 하려면 필요 합니다.  
  
> [!NOTE]  
> 이 절차를 OU에 컴퓨터 계정을 추가 하기 전에 Active Directory 사용자 및 컴퓨터 콘솔에서 BranchCache 파일 서버 OU을 만들어야 합니다. 자세한 내용은 참조 [BranchCache 파일 서버 조직 구성 단위 만들기](../../branchcache/deploy/Create-the-BranchCache-File-Servers-Organizational-Unit.md)합니다.  
  
### <a name="to-move-file-servers-to-the-branchcache-file-servers-organizational-unit"></a>이동 하는 파일 서버에서 BranchCache 파일 서버 조직 구성 단위  
  
1.  AD DS 설치 되어 있는, 서버 관리자의 컴퓨터에서 **도구**, 를 클릭 하 고 **Active Directory 사용자 및 컴퓨터**합니다. Active Directory 사용자 및 컴퓨터 콘솔을 엽니다.  
  
2.  Active Directory 사용자 및 컴퓨터 콘솔에서 BranchCache 파일 서버를 마우스 왼쪽 단추 클릭을에서 계정을 선택 하 고 다음 끌어 이전에 만든 OU의 BranchCache 파일 서버에 컴퓨터 계정에 대 한 컴퓨터 계정을 찾습니다. 예를 들어 명명 된 OU를 이전에 만든 **BranchCache 파일 서버**, 끌어다 놓고 컴퓨터 계정에는 **BranchCache 파일 서버** OU입니다.  
  
3.  각 BranchCache 파일 서버 OU로 이동 하려는 도메인에 대해 이전 단계를 반복 합니다.  
  


