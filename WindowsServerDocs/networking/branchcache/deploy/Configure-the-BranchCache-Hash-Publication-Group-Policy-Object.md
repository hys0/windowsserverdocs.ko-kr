---
title: BranchCache 해시 게시 그룹 정책 개체 구성
description: 이 항목은 일부는 BranchCache 배포 가이드에 대 한 Windows Server 2016, 지사에 WAN 대역폭 사용량을 최적화 하기 위해 분산 및 호스트 캐시 모드로 BranchCache를 배포 하는 방법을 보여 주는
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: da74fea7-52b2-4d6d-9d21-19184eedbe3c
ms.author: pashort
author: shortpatti
ms.openlocfilehash: bae0d3dff22205f3311020e233a26835527186f5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406497"
---
# <a name="configure-the-branchcache-hash-publication-group-policy-object"></a>BranchCache 해시 게시 그룹 정책 개체 구성

>적용 대상: Windows Server(반기 채널), Windows Server 2016

OU에 추가 하는 모든 파일 서버에 적용 된 동일한 해시 게시 정책 설정을 갖도록 BranchCache 해시 게시 그룹 정책 개체 (GPO)를 구성 하려면이 절차를 사용할 수 있습니다.  
  
멤버 자격이 **Domain Admins**, 또는 이와 동등한 최소한이이 절차를 수행 하려면 필요 합니다.  
  
> [!NOTE]  
> 이 절차를 수행 하기 전에 BranchCache 파일 서버 조직 구성 단위를 만들어야 합니다. 파일 서버를 OU로 이동한 BranchCache 해시 게시 GPO를 만듭니다. 자세한 내용은 참조 [도메인 구성원 파일 서버에 대 한 해시 게시 활성화](../../branchcache/deploy/Enable-Hash-Publication-for-Domain-Member-File-Servers.md)합니다.  
  
### <a name="to-configure-the-branchcache-hash-publication-group-policy-object"></a>그룹 정책 개체의 BranchCache 해시 게시를 구성 하려면  
  
1.  관리자 유형으로 Windows PowerShell 실행 **mmc**, 한 다음 ENTER를 누릅니다. MMC(Microsoft Management Console)가 열립니다.  
  
2.  Mmc에서에 **파일** 메뉴를 클릭 하 여 **스냅인 추가/제거**합니다. **추가 / 제거 스냅인** 대화 상자가 열립니다.  
  
3.  **추가 / 제거 스냅인**,  **사용 가능한 스냅인**, 두 번 클릭 **그룹 정책 관리**, 를 클릭 하 고 **확인**합니다.  
  
4.  그룹 정책 관리 MMC에서 BranchCache 해시 게시 이전에 만든 GPO에 경로 확장 합니다. 예를 들어 포리스트의 이름이 example.com이 고, 도메인 이름이 example1.com이 고, GPO가 **BranchCache 해시 게시**인 경우 다음 경로를 확장 합니다. **그룹 정책 관리**, **포리스트: example.com**, **도메인**, **Example1.com**, **그룹 정책 개체**, **BranchCache 해시 게시**.  
  
5.  마우스 오른쪽 단추로 클릭는 **BranchCache 해시 게시** GPO 및 클릭 **편집**합니다. 그룹 정책 관리 편집기 콘솔이 열립니다.  
  
6.  그룹 정책 관리 편집기 콘솔에서 다음 경로를 확장 합니다. **컴퓨터 구성**, **정책**, **관리 템플릿**, **네트워크**, **Lanman Server**.  
  
7.  그룹 정책 관리 편집기 콘솔에서 클릭 **Lanman Server**합니다. 세부 정보 창에서 두 번 클릭 **BranchCache 해시 게시**합니다. **BranchCache 해시 게시** 대화 상자가 열립니다.  
  
8.  에 **BranchCache 해시 게시** 대화 상자를 클릭 하 여 **사용**.  
  
9. **옵션**, 클릭 **모든 공유 폴더에 대 한 해시 게시 허용**, 다음 중 하나를 클릭 하 고 있습니다.  
  
    1.  모든 파일 서버 OU에 추가 된 모든 공유 폴더에 대 한 해시 게시를 사용 하려면 **모든 공유 폴더에 대 한 해시 게시 허용**합니다.  
  
    2.  BranchCache를 사용할 수 있는 공유 폴더에 대해서만 해시 게시를 활성화 하려면 클릭 **BranchCache 사용 되는 공유 폴더에 대해서만 해시 게시 허용**합니다.  
  
    3.  파일 공유에서 BranchCache를 사용 하는 경우에 컴퓨터의 폴더에 모든 공유에 대 한 해시 게시 금지 하려면 **모든 공유 폴더에 대 한 해시 게시 허용**합니다.  
  
10. **확인**을 클릭합니다.  
  
> [!NOTE]  
> 대부분의 경우에서 MMC 콘솔을 저장 하 고 구성 변경 내용을 표시 하려면 보기를 새로 고칩니다.  
  


