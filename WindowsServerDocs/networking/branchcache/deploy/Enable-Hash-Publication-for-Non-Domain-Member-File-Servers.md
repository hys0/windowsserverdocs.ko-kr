---
title: 해시 게시 비 도메인 구성원 파일 서버에 대 한 사용 하도록 설정
description: 이 항목은 Windows Server 2016을 지점에서 WAN 대역폭 사용을 최적화 하 분산 / 호스팅된 캐시 모드로 BranchCache 배포 하는 방법을 보여 주는 BranchCache 배포 가이드
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 11584b73-f9e2-4530-afa5-b8df970e6b24
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 4cb3d217115cff3a9b30ee11acb7ba0de6672b24
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="enable-hash-publication-for-non-domain-member-file-servers"></a>해시 게시 비 도메인 구성원 파일 서버에 대 한 사용 하도록 설정

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 절차를 사용 하 여 해시 게시 BranchCache와 Windows Server 2016 실행 하는 파일 서버에 로컬 그룹 정책 컴퓨터 사용에 대 한 구성 하 고 **BranchCache 네트워크 파일에 대 한** 설치 파일 서비스 거부의 역할 서비스 합니다.  
  
이 절차 비 도메인 회원 파일 서버에 사용 하 여 위한 것입니다. 도메인 회원 파일 서버에이 절차를 수행 하는 경우 도메인 그룹 정책을 사용 하 여 BranchCache 구성할 수도 도메인 그룹 정책 설정을 로컬 그룹 정책 설정을 재정의 합니다.  
  
회원 **관리자**, 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.  
  
> [!NOTE]  
> 하나 이상의 도메인 구성원 파일 서버를 사용 하는 경우에 조직에 (OU) Active Directory Domain Services에서 추가 하 고 그룹 정책을 사용 하 여 각 파일 서버 개별적으로 구성 아니라 해시 게시 모든 파일 서버에 대해 한 번에 구성 수 있습니다. 자세한 내용은 참조 [도메인 구성원 파일 서버에 대 한 사용 해시 게시](../../branchcache/deploy/Enable-Hash-Publication-for-Domain-Member-File-Servers.md)합니다.  
  
### <a name="to-enable-hash-publication-for-one-file-server"></a>하나의 파일 서버에 대 한 해시 게시 사용 하도록 설정 하려면  
  
1.  열기 Windows PowerShell 입력 **mmc**, ENTER 키를 누릅니다. Microsoft Management Console (MMC) 엽니다.  
  
2.  MMC에서에 **파일** 메뉴를 클릭 **스냅인 추가/제거**합니다. **추가 또는 제거 스냅인** 대화 상자를 엽니다.  
  
3.  **추가 또는 제거 스냅인**에서 **사용 가능한 스냅인**, 두 번 클릭 **그룹 정책 개체 편집기**합니다. 그룹 정책 개체 로컬 컴퓨터를 선택 열립니다. 클릭 **완료**을 차례로 클릭 하 고 **확인**합니다.  
  
4.  로컬 그룹 정책 편집기 MMC 다음 경로 확장: **로컬 컴퓨터 정책**, **컴퓨터 구성**, **관리 템플릿**, **네트워크**, **Lanman 서버**합니다. 클릭 **Lanman 서버**합니다.  
  
5.  세부 정보 창에서 두 번 클릭 **BranchCache에 대 한 해시 게시**합니다. **BranchCache에 대 한 해시 게시** 대화 상자를 엽니다.  
  
6.  **BranchCache에 대 한 해시 게시** 대화 상자를 클릭 **사용**합니다.  
  
7.  **옵션**, 클릭 **해시 게시 모든 공유 폴더를 허용**에서 다음 중 하나를 클릭 하 고 다음과 같습니다.  
  
    1.  이 컴퓨터의 모든 공유 폴더에 대 한 해시 게시를 사용 하도록 설정 하려면 클릭 **해시 게시 모든 공유 폴더를 허용**합니다.  
  
    2.  공유 폴더를 사용할 수에 대해서만 해시 게시를 사용 하도록 설정 하려면 클릭 **해시 게시 공유 폴더를 사용할 수에 허용**합니다.  
  
    3.  모든 컴퓨터의 공유 폴더에서 파일 공유에서 사용할 수 있는 경우에에 대 한 해시 게시 허용 하지 않으려면를 클릭 **해시 게시 모든 공유 폴더에서 허용 하지 않으려면**합니다.  
  
8.  클릭 **확인**합니다.  
  


