---
title: BranchCache 파일 서버 조직 구성 단위 만들기
description: 이 항목은 일부는 BranchCache 배포 가이드에 대 한 Windows Server 2016, 지사에 WAN 대역폭 사용량을 최적화 하기 위해 분산 및 호스트 캐시 모드로 BranchCache를 배포 하는 방법을 보여 주는
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 2cda192f-6b45-4e6c-88d9-70ca179ddb94
ms.author: pashort
author: shortpatti
ms.openlocfilehash: b7b26ec5808f5b11141e81dc5e738c83c94ef6b8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59874084"
---
# <a name="create-the-branchcache-file-servers-organizational-unit"></a>BranchCache 파일 서버 조직 구성 단위 만들기

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 절차를 사용 하 여 Active Directory 도메인 서비스에 AD DS BranchCache 파일 서버에 대 한 조직 구성 단위 (OU)를 만들려면 수 있습니다.  
  
멤버 자격이 **Domain Admins**, 또는 이와 동등한 최소한이이 절차를 수행 하려면 필요 합니다.  
  
### <a name="to-create-the-branchcache-file-servers-organizational-unit"></a>BranchCache 파일 서버 조직 구성 단위를 만들려면  
  
1.  AD DS 설치 되어 있는, 서버 관리자의 컴퓨터에서 **도구**, 를 클릭 하 고 **Active Directory 사용자 및 컴퓨터**합니다. Active Directory 사용자 및 컴퓨터 콘솔을 엽니다.  
  
2.  Active Directory 사용자 및 컴퓨터 콘솔에서 OU를 만들려는 도메인을 마우스 오른쪽 단추로 클릭 합니다. 도메인 이름이 example.com을 마우스 오른쪽 단추로 클릭 하는 예를 들어 **example.com**합니다. **새로 만들기**를 가리킨 다음 **조직 구성 단위**를 클릭합니다. **새 개체-조직 구성 단위** 대화 상자가 열립니다.  
  
3.  에 **새 개체-조직 구성 단위** 대화 상자의 **이름**, 새 OU에 대 한 이름을 입력 합니다. OU BranchCache 파일 서버 이름을 지정 하려는 경우 예를 들어 입력 **BranchCache 파일 서버**, 를 클릭 하 고 **확인**합니다.  
  


