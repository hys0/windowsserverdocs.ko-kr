---
title: WSUS(Windows Server Update Services) 콘텐츠 서버 구성
description: 이 항목은 BranchCache 배포 가이드에 대 한 Windows Server 2016, 지사에 WAN 대역폭 사용량을 최적화 하기 위해 분산 및 호스트 캐시 모드로 BranchCache를 배포 하는 방법에 설명 하는 부분입니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 9724aa8d-e4ae-404c-bee6-cef1534cd3ca
ms.author: pashort
author: shortpatti
ms.openlocfilehash: e8576282be92f02daf716da82ea75eddc755ee5c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59873844"
---
# <a name="configure-windows-server-update-services-wsus-content-servers"></a>WSUS(Windows Server Update Services) 콘텐츠 서버 구성

>적용 대상: Windows Server (반기 채널), Windows Server 2016

BranchCache 기능을 설치 하 고 BranchCache 서비스를 시작, 후 WSUS 서버를 구성 하는 로컬 컴퓨터에 업데이트 파일을 저장 되어야 합니다. 

로컬 컴퓨터에서 업데이트 파일을 저장할 WSUS 서버를 구성할 때 업데이트 메타 데이터와 업데이트 파일을 모두 다운로드 하 여 되며 WSUS 서버에 직접 저장 합니다. 이렇게 하면 Microsoft Update 웹 사이트에서 직접 읽지 못하고 WSUS 서버에서 BranchCache 클라이언트 컴퓨터 수신 Microsoft 제품 업데이트 파일입니다.  
  
WSUS 동기화에 대 한 자세한 내용은 참조 [업데이트 동기화를 설정](https://technet.microsoft.com/library/mt612311.aspx)  