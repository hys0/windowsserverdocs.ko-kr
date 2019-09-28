---
title: 원격 액세스 서버 및 해당 구성 요소의 작동 상태 모니터링
description: 이 항목은 Windows Server 2016의 원격 액세스 모니터링 및 계정에 대 한 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 077a3a64-2fa3-4994-9711-ec1fbdc081ba
ms.author: pashort
author: shortpatti
ms.openlocfilehash: d0ad63ec88a428239a174a0217db94c44ab799bc
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404548"
---
# <a name="monitor-the-operations-status-of-the-remote-access-server-and-its-components"></a>원격 액세스 서버 및 해당 구성 요소의 작동 상태 모니터링

>적용 대상: Windows Server(반기 채널), Windows Server 2016

**참고:** Windows Server 2012에는 DirectAccess와 RRAS(Routing and Remote Access Service)가 단일 원격 액세스 역할로 통합되어 있습니다.  
  
원격 액세스 서버에서 관리 콘솔의 작업 상태를 모니터링 데 사용할 수 있습니다.  
  
> [!NOTE]  
> 이 항목에 설명 된 작업을 완료 하려면 Domain Admins 그룹의 구성원 또는 각 컴퓨터에서 Administrators 그룹의 구성원으로 로그인 해야 합니다. Administrators 그룹의 구성원 인 계정으로 로그인 하는 동안에 작업을 완료할 수 없는 경우에 Domain Admins 그룹의 구성원 인 계정으로 로그인 하는 동안 작업을 수행해 봅니다.  
  
#### <a name="to-monitor-the-remote-access-server-operations-status"></a>원격 액세스 서버 작업 상태를 모니터링 하려면  
  
1.  **서버 관리자**, 클릭 **도구**, 를 클릭 하 고 **원격 액세스 관리**합니다.  
  
2.  클릭 **대시보드** 탐색할 **원격 액세스 보고** 에 **원격 액세스 관리 콘솔**합니다.  
  
3.  모니터링 대시보드의 알 수는 **작동 상태** 타일 내는 **서버 상태** 바둑판식으로 배열입니다. 이 타일 서버 작동 상태 및 모든 서버 구성 요소의 상태를 나열합니다.  
  
4.  클릭 **새로 고침** 아래 **작업** 작동 상태를 다시 로드 하려면 오른쪽 창에 있습니다. 작업 상태는 자동으로 새로 고쳐집니다 5 분 마다 되는 기본 새로 고침 간격. 기본 새로 고침 간격을 변경 하려면 **구성 새로 고침 간격**합니다.  
  
![Windows PowerShell](../../../media/Monitor-the-operations-status-of-the-Remote-Access-server-and-its-components/PowerShellLogoSmall.gif)***<em>windows powershell 해당 명령</em>***  
  
다음 Windows PowerShell cmdlet은 이전 절차와 같은 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.  
  
> [!NOTE]  
> 클러스터의 작업 상태에 대 한 명령 참조에 대 한 포함 되어 있습니다.  
  
```  
PS> Get-RemoteAccessHealth  
PS> Get-RemoteAccessHealth -Cluster  
```  
  


