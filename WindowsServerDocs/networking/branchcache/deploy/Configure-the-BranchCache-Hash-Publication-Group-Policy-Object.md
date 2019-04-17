---
title: BranchCache 해시 게시 그룹 정책 개체를 구성
description: 이 항목은 Windows Server 2016을 지점에서 WAN 대역폭 사용을 최적화 하 분산 / 호스팅된 캐시 모드로 BranchCache 배포 하는 방법을 보여 주는 BranchCache 배포 가이드
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: da74fea7-52b2-4d6d-9d21-19184eedbe3c
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 6f528c9f0a8a39b286ad7ac4fa728d93c311f779
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="configure-the-branchcache-hash-publication-group-policy-object"></a>BranchCache 해시 게시 그룹 정책 개체를 구성

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 절차 OU에 추가 하는 모든 파일 서버에 적용 동일한 해시 게시 정책 설정을 않아도 BranchCache 해시 게시 그룹 정책 개체 (GPO) 구성 사용할 수 있습니다.  
  
회원 **도메인 관리자**, 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.  
  
> [!NOTE]  
> 이 절차를 수행 하기 전에 파일 서버를 OU로 이동 BranchCache 파일 서버 구성 단위를 만들어야 하 고 BranchCache 해시 게시 GPO 만듭니다. 자세한 내용은 참조 [도메인 구성원 파일 서버에 대 한 사용 해시 게시](../../branchcache/deploy/Enable-Hash-Publication-for-Domain-Member-File-Servers.md)합니다.  
  
### <a name="to-configure-the-branchcache-hash-publication-group-policy-object"></a>그룹 정책 개체 BranchCache 해시 게시 구성 하려면  
  
1.  Windows PowerShell 입력 관리자 권한으로 실행 **mmc**, ENTER 키를 누릅니다. Microsoft Management Console (MMC) 엽니다.  
  
2.  MMC에서에 **파일** 메뉴를 클릭 **스냅인 추가/제거**합니다. **추가 또는 제거 스냅인** 대화 상자를 엽니다.  
  
3.  **추가 또는 제거 스냅인**에서 **사용 가능한 스냅인**, 두 번 클릭 **그룹 정책 관리**, 차례로 클릭 하 고 **확인**합니다.  
  
4.  그룹 정책 관리 mmc에서 BranchCache 해시 게시 이전에 만든 GPO 경로 확장 합니다. 예를 들어, 사용자 숲 example.com, 라는 도메인은 example1.com, GPO 라는 **BranchCache 해시 게시**, 다음 경로 확장: **그룹 정책 관리**, **숲: example.com**, **도메인**, **example1.com**, **그룹 정책 개체**, **BranchCache 해시 게시**합니다.  
  
5.  마우스 오른쪽 단추로 클릭는 **BranchCache 해시 게시** GPO 및 클릭 **편집**합니다. 그룹 정책 편집기 Management console을 엽니다.  
  
6.  그룹 정책 편집기 Management console에서 다음 경로 확장: **컴퓨터 구성**, **정책**, **관리 템플릿**, **네트워크**, **Lanman 서버**합니다.  
  
7.  그룹 정책 편집기 Management console에서 클릭 **Lanman 서버**합니다. 세부 정보 창에서 두 번 클릭 **BranchCache에 대 한 해시 게시**합니다. **BranchCache에 대 한 해시 게시** 대화 상자를 엽니다.  
  
8.  **BranchCache에 대 한 해시 게시** 대화 상자를 클릭 **사용**합니다.  
  
9. **옵션**, 클릭 **해시 게시 모든 공유 폴더를 허용**에서 다음 중 하나를 클릭 하 고 다음과 같습니다.  
  
    1.  해시 게시 모든 공유 폴더를 추가 하는 서버 모든 파일을 사용 하려면 클릭 **해시 게시 모든 공유 폴더를 허용**합니다.  
  
    2.  공유 폴더를 사용할 수에 대해서만 해시 게시를 사용 하도록 설정 하려면 클릭 **해시 게시 공유 폴더를 사용할 수에 허용**합니다.  
  
    3.  모든 컴퓨터의 공유 폴더에서 파일 공유에서 사용할 수 있는 경우에에 대 한 해시 게시 허용 하지 않으려면를 클릭 **해시 게시 모든 공유 폴더에서 허용 하지 않으려면**합니다.  
  
10. 클릭 **확인**합니다.  
  
> [!NOTE]  
> 대부분의 경우 MMC 본체에 저장 하 고 구성 변경 내용을 표시 하는 보기를 새로 고칩니다.  
  


