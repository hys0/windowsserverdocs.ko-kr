---
title: 비도메인 구성원 파일 서버에 해시 게시 사용
description: 이 항목은 일부는 BranchCache 배포 가이드에 대 한 Windows Server 2016, 지사에 WAN 대역폭 사용량을 최적화 하기 위해 분산 및 호스트 캐시 모드로 BranchCache를 배포 하는 방법을 보여 주는
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 11584b73-f9e2-4530-afa5-b8df970e6b24
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 223ffd17f1e623f974e97c787fb8b18a806e5d0c
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80319264"
---
# <a name="enable-hash-publication-for-non-domain-member-file-servers"></a>비도메인 구성원 파일 서버에 해시 게시 사용

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 절차를 사용 하 여 Windows Server 2016으로 실행 되는 파일 서버에 로컬 컴퓨터 그룹 정책을 사용 하 여 BranchCache에 대 한 해시 게시를 구성 하는 **네트워크 파일용 BranchCache** 설치 파일 서비스 서버 역할의 역할 서비스입니다.  
  
이 프로시저는 도메인 구성원이 아닌 파일 서버에서 사용을 위한 것입니다. 도메인 구성원 파일 서버에서이 절차를 수행 하는 경우 도메인 그룹 정책을 사용 하 여 BranchCache를 구성할 수도 도메인 그룹 정책 설정은 로컬 그룹 정책 설정을 무시 합니다.  
  
멤버 자격이 **관리자**, 또는 이와 동등한이 절차를 수행 하는 데 필요한 최소값입니다.  
  
> [!NOTE]  
> 하나 이상의 도메인 구성원 파일 서버를 설정한 경우 Active Directory 도메인 서비스에 조직 구성 단위 (OU)에 추가할 수 있으며 다음 그룹 정책을 사용 하 여 해시 게시의 모든 파일 서버에 대 한 한 번에 개별적으로 각 파일 서버를 구성 하는 대신 구성. 자세한 내용은 참조 [도메인 구성원 파일 서버에 대 한 해시 게시 활성화](../../branchcache/deploy/Enable-Hash-Publication-for-Domain-Member-File-Servers.md)합니다.  
  
### <a name="to-enable-hash-publication-for-one-file-server"></a>하나의 파일 서버에 대 한 해시 게시를 사용 하도록 설정 하려면  
  
1.  Windows PowerShell을 열고 **mmc**를 입력한 후 Enter 키를 누릅니다. MMC(Microsoft Management Console)가 열립니다.  
  
2.  MMC의 **파일** 메뉴에서 **스냅인 추가/제거**를 클릭합니다. **추가 / 제거 스냅인** 대화 상자가 열립니다.  
  
3.  **추가 / 제거 스냅인**,  **사용 가능한 스냅인**, 를 두 번 클릭 **그룹 정책 개체 편집기**합니다. 로컬 컴퓨터 개체를 선택 하는 그룹 정책 마법사가 열립니다. **마침**을 클릭한 다음 **확인**을 클릭합니다.  
  
4.  로컬 그룹 정책 편집기 MMC에서 경로 확장: **로컬 컴퓨터 정책**, **컴퓨터 구성**, **관리 템플릿**, **네트워크**, **Lanman Server**합니다. 클릭 **Lanman Server**합니다.  
  
5.  세부 정보 창에서 두 번 클릭 **BranchCache 해시 게시**합니다. **BranchCache 해시 게시** 대화 상자가 열립니다.  
  
6.  에 **BranchCache 해시 게시** 대화 상자를 클릭 하 여 **사용**.  
  
7.  **옵션**, 클릭 **모든 공유 폴더에 대 한 해시 게시 허용**, 다음 중 하나를 클릭 하 고 있습니다.  
  
    1.  이 컴퓨터에 모든 공유 폴더에 대 한 해시 게시를 활성화 하려면 클릭 **모든 공유 폴더에 대 한 해시 게시 허용**합니다.  
  
    2.  BranchCache를 사용할 수 있는 공유 폴더에 대해서만 해시 게시를 활성화 하려면 클릭 **BranchCache 사용 되는 공유 폴더에 대해서만 해시 게시 허용**합니다.  
  
    3.  파일 공유에서 BranchCache를 사용 하는 경우에 컴퓨터의 폴더에 모든 공유에 대 한 해시 게시 금지 하려면 **모든 공유 폴더에 대 한 해시 게시 허용**합니다.  
  
8.  **확인**을 클릭합니다.  
  


