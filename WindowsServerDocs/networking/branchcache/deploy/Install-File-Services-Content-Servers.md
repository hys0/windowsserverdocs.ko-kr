---
title: 파일 서비스 콘텐츠 서버 설치
description: 이 항목은 일부는 BranchCache 배포 가이드에 대 한 Windows Server 2016, 지사에 WAN 대역폭 사용량을 최적화 하기 위해 분산 및 호스트 캐시 모드로 BranchCache를 배포 하는 방법을 보여 주는
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 74b0a5ed-dc20-4974-9d4b-2426987a01a1
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 4fb9e40ce34a82a8797db1bf6d61c739f742c2d3
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80319248"
---
# <a name="install-file-services-content-servers"></a>파일 서비스 콘텐츠 서버 설치

>적용 대상: Windows Server(반기 채널), Windows Server 2016

파일 서비스 서버 역할을 실행 하는 콘텐츠 서버를 배포 하려면 파일 서비스 서버 역할의 네트워크 파일 역할 서비스용 BranchCache를 설치 해야 합니다. 또한 요구 사항에 따라 파일 공유에서 BranchCache를 활성화 해야 합니다.  
  
콘텐츠 서버에 구성 하는 동안 BranchCache 게시의 모든 파일 공유에 대 한 콘텐츠를 허용할 수 있습니다 또는 게시 하는 파일 공유의 하위 집합을 선택할 수 있습니다.  
  
> [!NOTE]  
> BranchCache 사용 가능된 파일 서버 또는 콘텐츠 서버와 웹 서버를 배포 하면 BranchCache 클라이언트가 파일을 요청 하기 전에 콘텐츠 정보를 오프 라인으로 계산 이제 됩니다. 이러한 향상으로 인해 필요가 없습니다 콘텐츠 서버에 대 한 해시 게시를 구성 하는 이전 버전의 BranchCache에서와 같이 합니다.  
>   
> 이미 수행 된 계산 및 콘텐츠 정보 콘텐츠를 요청 하는 첫 번째 클라이언트에 대 한 준비 않았기 때문에 성능이 향상 되 고 대역폭이 더욱 절약이 자동 해시 생성 제공 합니다.  
  
콘텐츠 서버를 배포 하려면 다음 항목을 참조 하십시오.  
  
-   [파일 서비스 서버 역할 구성](../../branchcache/deploy/Configure-the-File-Services-server-role.md)  
  
-   [파일 서버에 대 한 해시 게시 사용](../../branchcache/deploy/Enable-Hash-Publication-for-File-Servers.md)  
  
-   [파일 공유 &#40;에 BranchCache 사용 (선택 사항)&#41;](../../branchcache/deploy/enable-bc-on-file-share.md)  
  


