---
title: 새 파일 서버 콘텐츠 서버로 설치
description: 이 항목은 Windows Server 2016을 지점에서 WAN 대역폭 사용을 최적화 하 분산 / 호스팅된 캐시 모드로 BranchCache 배포 하는 방법을 보여 주는 BranchCache 배포 가이드
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 1f49fc3c-28a6-4d3d-b787-1be9e61e792f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 53937cfc139efc6df5facfa872e63609229a548c
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="install-a-new-file-server-as-a-content-server"></a>새 파일 서버 콘텐츠 서버로 설치

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 절차를 사용 하 여 설치 파일 서비스 거부 하려면 및 **네트워크 파일에 대 한 BranchCache** Windows Server 2016을 실행 하는 컴퓨터에서 역할 서비스입니다.  
  
회원 **관리자**, 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.  
  
> [!NOTE]  
> Windows PowerShell를 Windows PowerShell을 관리자 권한으로 실행을 사용 하 여이 절차를 수행 하려면 Windows PowerShell 프롬프트에서 다음 명령을 입력 하 고 ENTER 키를 누릅니다.  
>   
> `Install-WindowsFeature FS-BranchCache -IncludeManagementTools`  
>   
> `Restart-Computer`  
>   
> 데이터 중복 제거 역할 서비스를 설치 하려면 다음 명령을 입력 하 고 ENTER 키를 누릅니다.  
>   
> `Install-WindowsFeature FS-Data-Deduplication -IncludeManagementTools`  
  
### <a name="to-install-file-services-and-the-branchcache-for-network-files-role-service"></a>파일 서비스 및 네트워크 파일 역할 서비스에 대 한 BranchCache 설치 하려면  
  
1.  서버 관리자 클릭 **관리**을 차례로 클릭 하 고 **역할 추가 및 기능**합니다. 역할 추가 및 기능 마법사가 열립니다. **시작 하기 전에**, 클릭 **다음**합니다.  
  
2.  **설치 유형을 선택**, 되도록 **역할 또는 기능 기반 설치** 을 선택한 다음 클릭 **다음**합니다.  
  
3.  **선택 대상 서버**, 올바른 서버를 선택한 다음 클릭 **다음**합니다.  
  
4.  **서버 역할 선택**에 **역할**, 사항에 유의 **, 파일 저장소 서비스** 역할이 이미 설치 되어 있습니다. 확장 역할 서비스 선택을 역할 이름의 왼쪽에 있는 화살표를 클릭 하 고의 왼쪽에 있는 화살표를 클릭 한 다음 **파일과 iSCSI 서비스**합니다.  
  
5.  확인란을 선택 **파일 서버** 및 **네트워크 파일에 대 한 BranchCache**합니다.  
  
    > [!TIP]  
    > 또한의 확인란을 선택 하는 것이 좋습니다 **데이터 중복 제거**합니다.
  
    클릭 **다음**합니다.  
  
6.  **기능 선택**, 클릭 **다음**합니다.  
  
7.  **설치 선택을 확인**선택 항목을 검토 하 고 클릭 한 다음 **설치**합니다. **설치 진행률** 창이 설치 시 표시 됩니다. 설치가 완료 되 면 클릭 **닫기**합니다.
