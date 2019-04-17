---
title: 새로 고침 그룹 정책
description: 이 항목은 802.1 X 유선 및 무선 배포에 대 한 배포 서버 인증서 가이드
manager: brianlic
ms.topic: article
ms.assetid: 65b36794-bb09-4c1b-a2e7-8fc780893d97
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 4d9f5d38199f8cf3c0ffe46df4cd975cd9c56ff6
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="refresh-group-policy"></a>새로 고침 그룹 정책

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 절차 그룹 정책을 새로 고칩니다 수동으로 로컬 컴퓨터에 사용할 수 있습니다. 그룹 정책, 새로 때 인증서 등록이 구성 되어 있고 제대로 작동 로컬 컴퓨터가 자동 등록 인증서를 인증 기관 (캐나다)에서 합니다.  
  
> [!NOTE]  
> 그룹 정책 또는 사용자가 도메인 회원 컴퓨터에 로그온 할 때 도메인 회원 컴퓨터를 다시 시작 하면 자동으로 새로 고쳐집니다. 또한, 그룹 정책 주기적으로 새로 고쳐집니다. 기본적으로 정기적으로이 새로 90 분 마다 최대 30 분 임의 오프셋으로 수행 됩니다.  
  
회원 **관리자**, 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.  
  
### <a name="to-refresh-group-policy-on-the-local-computer"></a>로컬 컴퓨터에서 그룹 정책을 복구 하려면  
  
1.  NPS 설치 된 컴퓨터에서 Windows PowerShell 열고&reg; 작업 표시줄의 아이콘을 사용 하 여 합니다.  
  
2.  Windows PowerShell 프롬프트에 입력 **gpupdate**, ENTER 키를 누릅니다.  
  


