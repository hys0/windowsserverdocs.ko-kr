---
title: 도메인 구성원 파일 서버에 해시 게시 사용
description: 이 항목은 일부는 BranchCache 배포 가이드에 대 한 Windows Server 2016, 지사에 WAN 대역폭 사용량을 최적화 하기 위해 분산 및 호스트 캐시 모드로 BranchCache를 배포 하는 방법을 보여 주는
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: a3f1f7c4-d9b2-43e6-8bfa-fac707bbd4d3
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 1e450b9a2282cb4820b8802aa6d36e822f56ca12
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71356586"
---
# <a name="enable-hash-publication-for-domain-member-file-servers"></a>도메인 구성원 파일 서버에 해시 게시 사용

>적용 대상: Windows Server(반기 채널), Windows Server 2016

Active Directory 도메인 서비스 (AD DS)를 사용 하는 경우에 여러 파일 서버에 대 한 BranchCache 해시 게시를 사용 하도록 설정 하려면 도메인 그룹 정책을 사용할 수 있습니다. 이렇게 조직 구성 단위 (OU)를 만들어야 합니다를 추가 하려면 파일 서버 OU에 그룹 정책 개체 (GPO) BranchCache 해시 게시를 만들고 GPO를 구성 합니다.  
  
여러 파일 서버에 대 한 해시 게시를 사용 하도록 설정 하려면 다음 항목을 참조 하십시오.  
  
-   [BranchCache 파일 서버 조직 구성 단위 만들기](../../branchcache/deploy/Create-the-BranchCache-File-Servers-Organizational-Unit.md)  
  
-   [파일 서버를 BranchCache 파일 서버 조직 구성 단위로 이동 합니다.](../../branchcache/deploy/Move-File-Servers-to-the-BranchCache-File-Servers-Organizational-Unit.md)  
  
-   [BranchCache 해시 게시 그룹 정책 개체 만들기](../../branchcache/deploy/Create-the-BranchCache-Hash-Publication-Group-Policy-Object.md)  
  
-   [BranchCache 해시 게시 그룹 정책 개체 구성](../../branchcache/deploy/Configure-the-BranchCache-Hash-Publication-Group-Policy-Object.md)  
  


