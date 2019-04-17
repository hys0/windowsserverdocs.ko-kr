---
title: "Windows Server Essentials의 방화벽 문제 해결"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 51d94b67-8b9b-4159-80dd-f652d73a43cb
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 3c48d2abb7fd8431f40f76f8eece5c4142be4c75
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="troubleshoot-your-firewall-in-windows-server-essentials"></a>Windows Server Essentials의 방화벽 문제 해결
 
>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.
  
 원격 액세스할 수 있는 문제가 있는 경우 복구 어디서 나 액세스 마법사를 실행 합니다.  
  
### <a name="to-run-the-repair-anywhere-access-wizard"></a>마법사를 실행 하는 복구 어디서 나 액세스  
  
1.  대시보드를 엽니다.  
  
2.  클릭 **설정**를 클릭는 **어디서 나 액세스** 탭을 클릭 한 다음 **복구**합니다.  
  
3.  복구 어디서 나 액세스 마법사의 지침을 따릅니다.  
  
 고급 네트워크 설정 사용 하거나 Microsoft 이외의 방화벽을 사용 하는 경우 방화벽에서 추가 포트를 열어야 해야 할 수 있습니다. 다음 표에서 포트도 인터넷 할당 숫자 기관 (IANA) 등록 되어 있습니다.  
  
|포트 번호|설명|  
|-----------------|-----------------|  
|65500|인증서 웹 서비스|  
|65510 및 65515|클라이언트 컴퓨터 배포 웹 사이트|  
|65520|Mac 클라이언트 컴퓨터에 대 한 웹 서비스|  
|65532|서버 루프백 통신을 위해 프레임 워크 공급자|  
|6602|클라이언트 컴퓨터와 통신을 위해 프레임 워크 공급자|  
  
## <a name="see-also"></a>참조 하십시오  
  
-   [사용 하 여 원격 웹 액세스](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md)  
  
-   [원격 Web Access 관리](../manage/Manage-Remote-Web-Access-in-Windows-Server-Essentials.md)  
  
-   [액세스를 어디서 나 관리](../manage/Manage-Anywhere-Access-in-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials 관리](../manage/Manage-Windows-Server-Essentials.md)  
  

-   [Windows Server Essentials 지원](Support-Windows-Server-Essentials.md)

-   [Windows Server Essentials 지원](../support/Support-Windows-Server-Essentials.md)

