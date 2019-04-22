---
title: 콘텐츠 서버로 새 파일 서버 설치
description: 이 항목은 일부는 BranchCache 배포 가이드에 대 한 Windows Server 2016, 지사에 WAN 대역폭 사용량을 최적화 하기 위해 분산 및 호스트 캐시 모드로 BranchCache를 배포 하는 방법을 보여 주는
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 1f49fc3c-28a6-4d3d-b787-1be9e61e792f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: e3a4dbe5339685b385b0157756379e9e545f1964
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59812024"
---
# <a name="install-a-new-file-server-as-a-content-server"></a>콘텐츠 서버로 새 파일 서버 설치

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 절차를 사용 하 여 파일 서비스 서버 역할을 설치 하 고 **네트워크 파일용 BranchCache** Windows Server 2016를 실행 하는 컴퓨터에서 역할 서비스입니다.  
  
멤버 자격이 **관리자**, 또는 이와 동등한이 절차를 수행 하는 데 필요한 최소값입니다.  
  
> [!NOTE]  
> 관리자는 Windows PowerShell을 실행 하는 Windows PowerShell을 사용 하 여이 절차를 수행 하려면 Windows PowerShell 프롬프트에서 다음 명령을 입력 하 고 ENTER 키를 누릅니다.  
>   
> `Install-WindowsFeature FS-BranchCache -IncludeManagementTools`  
>   
> `Restart-Computer`  
>   
> 데이터 중복 제거 역할 서비스를 설치 하려면 다음 명령을 입력 한 다음 ENTER 키를 누릅니다.  
>   
> `Install-WindowsFeature FS-Data-Deduplication -IncludeManagementTools`  
  
### <a name="to-install-file-services-and-the-branchcache-for-network-files-role-service"></a>파일 서비스 및 네트워크 파일 역할 서비스용 BranchCache를 설치 하려면  
  
1.  서버 관리자에서 **관리**, **역할 및 기능 추가**를 차례로 클릭합니다. 역할 및 기능 추가 마법사가 열립니다. **시작 하기 전에**, 를 클릭 하 여 **다음**합니다.  
  
2.  **설치 유형 선택**, 되도록 **역할 기반 또는 기능 기반 설치** 을 선택한 다음 클릭 **다음**합니다.  
  
3.  **대상 서버 선택**, 반드시 올바른 서버를 선택한 다음 클릭 **다음**합니다.  
  
4.  **서버 역할 선택**,  **역할**, 유의 **파일 및 저장소 서비스** 역할이 이미 설치 되어; 역할 서비스 선택 항목을 확장 역할 이름의 왼쪽에 있는 화살표를 클릭 한 다음 왼쪽의 화살표를 클릭 **파일 및 iSCSI 서비스**합니다.  
  
5.  에 대 한 확인란을 선택 **파일 서버** 및 **네트워크 파일용 BranchCache**합니다.  
  
    > [!TIP]  
    > 또한에 대 한 확인란을 선택 하는 것이 좋습니다 **데이터 중복 제거**합니다.
  
    **다음**을 클릭합니다.  
  
6.  **기능 선택**, 클릭 **다음**합니다.  
  
7.  **설치 선택 확인**, 선택 항목을 검토 하 고 클릭 한 다음 **설치**합니다. **설치 진행률** 설치 하는 동안 창이 표시 됩니다. 설치가 완료 되 면 클릭 **닫기**합니다.
