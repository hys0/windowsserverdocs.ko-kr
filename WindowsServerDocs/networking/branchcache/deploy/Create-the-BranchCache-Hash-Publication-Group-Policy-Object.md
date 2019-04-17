---
title: BranchCache 해시 게시 그룹 정책 개체 만들기
description: 이 항목은 Windows Server 2016을 지점에서 WAN 대역폭 사용을 최적화 하 분산 / 호스팅된 캐시 모드로 BranchCache 배포 하는 방법을 보여 주는 BranchCache 배포 가이드
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: c3d33bed-83ef-4eb8-acf9-0719ecb4a931
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 4510d13c806adc2db46dfccce02a5a1b2814a2c4
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="create-the-branchcache-hash-publication-group-policy-object"></a>BranchCache 해시 게시 그룹 정책 개체 만들기

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 절차 BranchCache 해시 게시 그룹 정책 개체 (GPO)을 사용할 수 있습니다.  
  
회원 **도메인 관리자**, 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.  
  
> [!NOTE]  
> 이 절차를 수행 하기 전에 BranchCache 파일 서버 조직 단위를 만들고 파일 서버 OU로 이동 합니다. 자세한 내용은 참조 [도메인 구성원 파일 서버에 대 한 사용 해시 게시](../../branchcache/deploy/Enable-Hash-Publication-for-Domain-Member-File-Servers.md)합니다.  
  
### <a name="to-create-the-branchcache-hash-publication-group-policy-object"></a>BranchCache 해시 게시 그룹 정책 개체를 만들려면  
  
1.  열기 Windows PowerShell 입력 **mmc**, ENTER 키를 누릅니다. Microsoft Management Console (MMC) 엽니다.  
  
2.  MMC에서에 **파일** 메뉴를 클릭 **스냅인 추가/제거**합니다. **추가 또는 제거 스냅인** 대화 상자를 엽니다.  
  
3.  **추가 또는 제거 스냅인**에서 **사용 가능한 스냅인**, 두 번 클릭 **그룹 정책 관리**, 차례로 클릭 하 고 **확인**합니다.  
  
4.  그룹 정책 관리 MMC 경로 BranchCache 파일 서버 이전에 만든를 확장 합니다. 예를 들어, 사용자 숲은 example.com, 도메인 example1.com, 라는, OU은 이름 BranchCache 파일 서버, 확장 다음 경로: **그룹 정책 관리**, **숲: example.com**, **도메인**, **example1.com**, **BranchCache 파일 서버**합니다.  
  
5.  마우스 오른쪽 단추로 클릭 **BranchCache 파일 서버**을 차례로 클릭 하 고 **GPO이이 도메인에 있는 만들고 여기에 링크**합니다. **새 GPO** 대화 상자를 엽니다. **이름**, GPO 새 이름을 입력 합니다. 예를 들어, BranchCache 해시 게시 개체 이름을 지정 하려면 입력 **BranchCache 해시 게시**합니다. 클릭 **확인**합니다.  
  


