---
title: BranchCache 기능 설치
description: 이 항목은 일부는 BranchCache 배포 가이드에 대 한 Windows Server 2016, 지사에 WAN 대역폭 사용량을 최적화 하기 위해 분산 및 호스트 캐시 모드로 BranchCache를 배포 하는 방법을 보여 주는
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 4f31dc61-2dbe-4c7e-b3f9-85ae49a45049
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 8b4aecd9e9355a6c2d5ac485ac77c76428fe295f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59872194"
---
# <a name="install-the-branchcache-feature"></a>BranchCache 기능 설치

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 절차를 사용 하 여 BranchCache 기능을 설치 하 고 Windows Server를 실행 하는 컴퓨터에서 BranchCache 서비스를 시작 하려면&reg; 2016 년까지 Windows Server 2012 R2 또는 Windows Server 2012.  
  
멤버 자격이 **관리자** 또는 이와 동등한 최소한이이 절차를 수행 하려면 필요 합니다.  
  
이 절차를 수행 하기 전에 설치 하 고 BITS 기반 응용 프로그램 또는 웹 서버를 구성 하는 것이 좋습니다.  
  
> [!NOTE]  
> 관리자는 Windows PowerShell을 실행 하는 Windows PowerShell을 사용 하 여이 절차를 수행 하려면 Windows PowerShell 프롬프트에서 다음 명령을 입력 하 고 ENTER 키를 누릅니다.  
>   
> `Install-WindowsFeature BranchCache`  
>   
> `Restart-Computer`  
  
### <a name="to-install-and-enable-the-branchcache-feature"></a>설치 하 여 BranchCache 기능을 사용 하도록 설정  
  
1.  서버 관리자에서 **관리**, **역할 및 기능 추가**를 차례로 클릭합니다. 역할 및 기능 추가 마법사가 열립니다. **다음**을 클릭합니다.  
  
2.  **설치 유형 선택**, 되도록 **역할 기반 또는 기능 기반 설치** 을 선택한 다음 클릭 **다음**합니다.  
  
3.  **대상 서버 선택**, 반드시 올바른 서버를 선택한 다음 클릭 **다음**합니다.  
  
4.  **서버 역할 선택**에서 **다음**을 클릭합니다.  
  
5.  **기능 선택**, 클릭 **BranchCache**, 를 클릭 하 고 **다음**합니다.  
  
6.  **설치 선택 확인**, 클릭 **설치**합니다. **설치 진행률**, BranchCache 기능 설치를 진행 합니다. 설치가 완료 되 면 클릭 **닫기**합니다.  
  
BranchCache 기능을 설치한 후 라고도 PeerDistSvc-BranchCache 서비스-를 사용 하 고 시작 유형이 자동 인지 합니다.  
  


