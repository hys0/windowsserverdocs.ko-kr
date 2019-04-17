---
title: BranchCache 파일 서버 조직 만들기
description: 이 항목은 Windows Server 2016을 지점에서 WAN 대역폭 사용을 최적화 하 분산 / 호스팅된 캐시 모드로 BranchCache 배포 하는 방법을 보여 주는 BranchCache 배포 가이드
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 2cda192f-6b45-4e6c-88d9-70ca179ddb94
ms.author: pashort
author: shortpatti
ms.openlocfilehash: a92cb3110e4aecb1ef09a45ed14173305722c655
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="create-the-branchcache-file-servers-organizational-unit"></a>BranchCache 파일 서버 조직 만들기

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

BranchCache 파일 서버에 대 한 Active Directory Domain Services (AD DS)에 조직 (OU)을 만들려면이 절차를 사용할 수 있습니다.  
  
회원 **도메인 관리자**, 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.  
  
### <a name="to-create-the-branchcache-file-servers-organizational-unit"></a>BranchCache 파일 서버 조직 단위를 만들려면  
  
1.  AD DS 설치 되어 있는, 서버 관리자는 컴퓨터에서 클릭 **도구**을 차례로 클릭 하 고 **Active Directory 사용자 및 컴퓨터**합니다. 콘솔 Active Directory 사용자 및 컴퓨터 엽니다.  
  
2.  콘솔 Active Directory 사용자 및 컴퓨터에서 OU 추가할 도메인을 마우스 오른쪽 단추로 클릭 합니다. 예를 들어 도메인 example.com 이름이 마우스 오른쪽 단추로 클릭 **example.com**합니다. 가리킨 **새로**을 차례로 클릭 하 고 **조직**합니다. **새 개체-조직** 대화 상자를 엽니다.  
  
3.  에 **새 개체-조직** 대화 상자의 **이름**, 새 OU 이름을 입력 합니다. 예를 들어, OU BranchCache 파일 서버의 이름을 지정 하려면 입력 **BranchCache 파일 서버**을 차례로 클릭 하 고 **확인**합니다.  
  


