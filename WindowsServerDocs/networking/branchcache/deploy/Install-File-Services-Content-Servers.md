---
title: 파일 서비스 콘텐츠 서버의 설치
description: 이 항목은 Windows Server 2016을 지점에서 WAN 대역폭 사용을 최적화 하 분산 / 호스팅된 캐시 모드로 BranchCache 배포 하는 방법을 보여 주는 BranchCache 배포 가이드
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 74b0a5ed-dc20-4974-9d4b-2426987a01a1
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 7036323e7cc31bd14be8025b6064a806fb45ef19
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="install-file-services-content-servers"></a>파일 서비스 콘텐츠 서버의 설치

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

파일 서비스 서버 역할을 실행 하는 콘텐츠 서버를 배포 하는, 서비스 파일 서버 역할의 네트워크 파일 역할 서비스에 대 한 BranchCache 설치 해야 합니다. 또한, 요구 사항에 따라 파일 공유에서 BranchCache를 사용 해야 합니다.  
  
콘텐츠 서버 구성 하는 동안 모든 파일 공유에 대 한 콘텐츠를 게시 BranchCache 허용할 수 있습니다 하거나 파일 공유 게시할 중 일부를 선택할 수 있습니다.  
  
> [!NOTE]  
> BranchCache 활성화 된 파일 서버 또는 콘텐츠 서버로 웹 서버를 배포한 BranchCache 클라이언트가 파일 요청 하기 전에 콘텐츠 정보 오프 라인으로 계산 이제 됩니다. 이 개선 사항을 때문 하지 필요가 해시 게시 콘텐츠 서버에 대 한 구성에서 이전 버전의 BranchCache와 같이 합니다.  
>   
> 계산 이미 수행 된 및 콘텐츠 정보 콘텐츠를 요청 하는 첫 번째 클라이언트에 대 한 준비를 하기 때문에 더욱 빠른 성능을 하 고 더 많은 대역폭 자동 해시 세대가 제공 합니다.  
  
콘텐츠 서버 배포 하려면 다음 항목을 참조 하십시오.  
  
-   [파일 서비스 서버 역할을 구성 합니다.](../../branchcache/deploy/Configure-the-File-Services-server-role.md)  
  
-   [해시 게시 파일 서버에 대 한 사용 하도록 설정](../../branchcache/deploy/Enable-Hash-Publication-for-File-Servers.md)  
  
-   [파일 공유 및 #40; BranchCache 사용 옵션 & #41;](../../branchcache/deploy/enable-bc-on-file-share.md)  
  


