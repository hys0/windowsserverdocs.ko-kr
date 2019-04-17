---
title: "5 단계: Windows Server Essentials 대상 서버 마이그레이션에 폴더 리디렉션을 사용합니다"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d3925f80-552d-431f-b2a6-2af202e50ca4
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 613ff4c80a80ed4f3207cb0c1ead6db12c723e85
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="step-5-enable-folder-redirection-on-the-destination-server-for-windows-server-essentials-migration"></a>5 단계: Windows Server Essentials 대상 서버 마이그레이션에 폴더 리디렉션을 사용합니다

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

원본 서버의 폴더 리디렉션을 사용 하는 경우 대상 서버의 폴더 리디렉션을 사용 수 있으며 이전 폴더 리디렉션을 그룹 정책 설정 삭제 합니다.  
  
 Windows Server Essentials 대시보드 대상 서버의 폴더 리디렉션을 사용 하려면 먼저를 사용 합니다. 그리고 이전 폴더 리디렉션을 그룹 정책 설정을 삭제 합니다.  
  
### <a name="to-enable-folder-redirection-on-the-destination-server"></a>폴더 리디렉션을 대상 서버에 사용 하려면  
  
1.  대상 서버, Windows Server Essentials 대시보드를 엽니다.  
  
2.  탐색 모음에서 클릭 **디바이스**합니다.  
  
3.  에 **디바이스 작업** 창 클릭 **구현 그룹 정책**합니다.  
  
4.  에 **폴더 리디렉션을 그룹 정책을 사용 하도록 설정** 페이지에서 이동를 클릭 한 다음 폴더 선택 **다음**합니다.  
  
5.  에 **보안 정책 설정 사용** 페이지, 클릭 **완료**합니다.  
  
### <a name="to-delete-the-old-folder-redirection-group-policy-setting"></a>오래 된 폴더 리디렉션을 그룹 정책 설정 삭제 하려면  
  
1.  대상 서버에서 엽니다는 **그룹 정책 관리** 관리 도구입니다.  
  
2.  **그룹 정책 관리**, 확장 **숲:***YourNetworkDomainName*, 확장 **도메인**, 확장 *YourNetworkDomainName*를 확장 한 다음 **그룹 정책 개체**합니다.  
  
3.  삭제 및 클릭 한 다음 원하는 정책을 마우스 오른쪽 단추로 클릭 **삭제**합니다.  
  
4.  경고를 읽고 클릭 한 다음 **예**합니다.  
  
5.  닫기 **그룹 정책 관리**합니다.  
  
 네트워크 사용자에 게 폴더 리디렉션에 대 한 변경을 적용 하려면 로그 자신의 컴퓨터 오프 한 다음 다시 로그온 해야 합니다. 이렇게 하면 모든 리디렉션된 폴더 대상 서버에 전송 합니다.  
  
## <a name="next-steps"></a>다음 단계  
 폴더 리디렉션을 대상 서버의 설정. 지금 이동 [6 단계: 내리기 하 고 원본 서버 새로운 Windows Server Essentials 네트워크에서 제거](Step-6--Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md)합니다.  
  

모든 단계를 참조 [Windows Server essentials 마이그레이션](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md)합니다.

