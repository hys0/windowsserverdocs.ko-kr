---
title: BranchCache 기능을 설치
description: 이 항목은 Windows Server 2016을 지점에서 WAN 대역폭 사용을 최적화 하 분산 / 호스팅된 캐시 모드로 BranchCache 배포 하는 방법을 보여 주는 BranchCache 배포 가이드
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 4f31dc61-2dbe-4c7e-b3f9-85ae49a45049
ms.author: pashort
author: shortpatti
ms.openlocfilehash: a69848536b56521da9b5ef07689aba7f8690e888
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="install-the-branchcache-feature"></a>BranchCache 기능을 설치

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 절차를 사용 하 여 BranchCache 기능을 설치 하 고 Windows Server를 실행 하는 컴퓨터에서 BranchCache 서비스를 시작 하려면&reg; 2016, Windows Server 2012 R2 또는 Windows Server 2012 합니다.  
  
회원 **관리자** 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.  
  
이 절차를 수행 하기 전에 설치 및 구성 비트 기반 응용 프로그램이 나 웹 서버의 하는 것이 좋습니다.  
  
> [!NOTE]  
> Windows PowerShell를 Windows PowerShell을 관리자 권한으로 실행을 사용 하 여이 절차를 수행 하려면 Windows PowerShell 프롬프트에서 다음 명령을 입력 하 고 ENTER 키를 누릅니다.  
>   
> `Install-WindowsFeature BranchCache`  
>   
> `Restart-Computer`  
  
### <a name="to-install-and-enable-the-branchcache-feature"></a>설치 하 고 BranchCache 기능을 사용 하려면  
  
1.  서버 관리자 클릭 **관리**을 차례로 클릭 하 고 **역할 추가 및 기능**합니다. 기능 및 역할 추가 마법사가 열립니다. 클릭 **다음**합니다.  
  
2.  **설치 유형을 선택**, 되도록 **역할 또는 기능 기반 설치** 을 선택한 다음 클릭 **다음**합니다.  
  
3.  **선택 대상 서버**, 올바른 서버를 선택한 다음 클릭 **다음**합니다.  
  
4.  **서버 역할 선택**, 클릭 **다음**합니다.  
  
5.  **기능을 선택**, 클릭 **BranchCache**을 차례로 클릭 하 고 **다음**합니다.  
  
6.  **설치 선택을 확인**, 클릭 **설치**합니다. **설치 진행률**, BranchCache 기능 설치 진행 됩니다. 설치가 완료 되 면 클릭 **닫기**합니다.  
  
BranchCache 기능을 설치한 후 라고도 함 PeerDistSvc--BranchCache 서비스를 사용 하도록 설정 하 고 시작 형식이 자동 합니다.  
  


