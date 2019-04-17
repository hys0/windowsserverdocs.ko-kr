---
title: Windows Server Update Services (WSUS) 콘텐츠 서버 구성
description: 이 항목 대 한 Windows Server 2016을 지점에서 WAN 대역폭 사용을 최적화 하 분산 / 호스팅된 캐시 모드로 BranchCache 배포 하는 방법을 보여 주는 BranchCache 배포 가이드의 일부입니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 9724aa8d-e4ae-404c-bee6-cef1534cd3ca
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 8200a0905f7bc5c403288a22faece5f84eac8af9
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="configure-windows-server-update-services-wsus-content-servers"></a>Windows Server Update Services (WSUS) 콘텐츠 서버 구성

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

후 BranchCache 기능을 설치 BranchCache 서비스를 시작 하 고, 로컬 컴퓨터에 업데이트 파일을 저장할 WSUS 서버를 구성 합니다. 

로컬 컴퓨터에 업데이트 파일을 저장할 WSUS 서버를 구성할 때 업데이트 메타 데이터 및 업데이트 파일 다운로드 하 여 되며 직접 WSUS 서버에 저장 합니다. 이렇게 하면 BranchCache 클라이언트 컴퓨터 Microsoft 업데이트 웹 사이트에서 직접 대신 WSUS 서버에서 파일 Microsoft 제품 업데이트를 받을 수 있습니다.  
  
WSUS 동기화에 대 한 자세한 내용은 참조 [업데이트 동기화 설정](https://technet.microsoft.com/en-us/library/mt612311.aspx)  