---
title: 그룹 새로 고침 정책
description: 이 항목은 서버 배포 인증서 802.1 X 유선 및 무선 배포 가이드의 일부
manager: brianlic
ms.topic: article
ms.assetid: 65b36794-bb09-4c1b-a2e7-8fc780893d97
ms.prod: windows-server
ms.technology: networking
ms.author: lizross
author: eross-msft
ms.openlocfilehash: b9522909960470d9f5f3e183afbd97ab1b919019
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80318254"
---
# <a name="refresh-group-policy"></a>그룹 새로 고침 정책

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 절차는 수동으로 로컬 컴퓨터에서 그룹 정책을 새로 사용할 수 있습니다. 그룹 정책은 새로 고칠 때, 인증서 자동 등록 구성 되어 있고 제대로 작동 로컬 컴퓨터가 인증 기관 (CA)에서 인증서 자동 등록 된 경우.  
  
> [!NOTE]  
> 그룹 정책은 도메인 구성원 컴퓨터를 다시 시작 하거나 사용자가 도메인 구성원 컴퓨터에 로그온 할 때 자동으로 새로 고쳐집니다. 또한 그룹 정책 정기적으로 새로 고쳐집니다. 기본적으로이 정기적 새로 고침에는 최대 30 분의 임의 오프셋 90 분 마다 수행 됩니다.  
  
멤버 자격이 **관리자**, 또는 이와 동등한 최소한이이 절차를 완료 합니다.  
  
### <a name="to-refresh-group-policy-on-the-local-computer"></a>로컬 컴퓨터에서 그룹 정책을 새로 고치려면  
  
1.  NPS를 설치한 컴퓨터에서 Windows PowerShell을 열고&reg; 작업 표시줄에서 아이콘을 사용 하 여 합니다.  
  
2.  Windows PowerShell 프롬프트에서 입력 **gpupdate**, 한 다음 ENTER를 누릅니다.  
  


