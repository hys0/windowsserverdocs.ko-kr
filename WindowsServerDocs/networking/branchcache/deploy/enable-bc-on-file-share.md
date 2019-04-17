---
title: (옵션) 파일 공유에서 BranchCache 사용 하도록 설정
description: 이 항목은 Windows Server 2016을 지점에서 WAN 대역폭 사용을 최적화 하 분산 / 호스팅된 캐시 모드로 BranchCache 배포 하는 방법을 보여 주는 BranchCache 배포 가이드
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-bc
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9c465a9e-c504-44ec-9ebc-4e06ba54db30
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 33ed40ef91d9389bb7940dcf928cba43f0c9dbd2
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="enable-branchcache-on-a-file-share-optional"></a>(옵션) 파일 공유에서 BranchCache 사용 하도록 설정

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

파일 공유에서 BranchCache 수 있도록이 절차를 사용할 수 있습니다.  
  
> [!IMPORTANT]  
> 해시 게시 설정 값으로 구성 하는 경우이 절차를 수행 해야 **해시 게시 모든 공유 폴더를 허용**합니다.  
  
회원 **관리자**, 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.  
  
### <a name="to-enable-branchcache-on-a-file-share"></a>파일 공유에서 BranchCache 사용 하도록 설정 하려면  
  
1.  열기 Windows PowerShell 입력 **mmc**, ENTER 키를 누릅니다. Microsoft Management Console (MMC) 엽니다.  
  
2.  MMC에서에 **파일** 메뉴를 클릭 **스냅인 추가/제거**합니다. **추가 또는 제거 스냅인** 대화 상자를 엽니다.  
  
3.  **추가 또는 제거 스냅인**에서 **사용 가능한 스냅인**, 두 번 클릭 **공유 폴더**합니다. 선택 되어 있는 로컬 컴퓨터 개체와 공유 폴더 마법사가 열립니다. 사용자가 선호 하는 보기 구성 클릭 **완료**을 차례로 클릭 하 고 **확인**합니다.  
  
4.  두 번 클릭 **공유 된 폴더 (로컬)**을 차례로 클릭 하 고 **공유**합니다.  
  
5.  세부 정보 창에서 공유를 마우스 오른쪽 단추로 클릭 한 다음 **속성**합니다. 공유의 **속성** 대화 상자를 엽니다.  
  
6.  에 **속성** 대화 상자의 **일반** 탭을 클릭 **오프 라인 설정**합니다. **오프 라인 설정** 대화 상자를 엽니다.  
  
7.  되도록 **파일 및 사용자 지정 프로그램은 사용 가능한 오프 라인만** 을 선택한 다음 클릭 **BranchCache**합니다.  
  
8.  클릭 **확인** 두 번 합니다.  
  

