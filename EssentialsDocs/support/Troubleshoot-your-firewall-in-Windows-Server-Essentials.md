---
title: Windows Server Essentials에서 방화벽 문제 해결
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: 51d94b67-8b9b-4159-80dd-f652d73a43cb
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 1ff27915f3d6c92416ed22b7e143bdc1cf3b385f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80853186"
---
# <a name="troubleshoot-your-firewall-in-windows-server-essentials"></a>Windows Server Essentials에서 방화벽 문제 해결
 
>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials
  
 원격 액세스에서 문제가 발생하는 경우 원격 액세스 복구 마법사를 실행합니다.  
  
### <a name="to-run-the-repair-anywhere-access-wizard"></a>원격 액세스 복구 마법사를 실행하려면  
  
1. 대시보드를 엽니다.  
  
2. **설정**, **원격 액세스** 탭, **복구**를 차례로 클릭합니다.  
  
3. 원격 액세스 복구 마법사의 지침에 따릅니다.  
  
   고급 네트워크 설정을 사용하거나 타사 방화벽을 사용하는 경우 방화벽에서 추가 포트를 열어야 할 수도 있습니다. 다음 표의 포트는 IANA(Internet Assigned Numbers Authority)에 등록되어 있습니다.  
  
|포트 번호|설명|  
|-----------------|-----------------|  
|65500|인증서 웹 서비스|  
|65510 및 65515|클라이언트 컴퓨터 배포 웹 사이트|  
|65520|Mac 클라이언트 컴퓨터용 웹 서비스|  
|65532|서버 루프백 통신용 공급자 프레임워크|  
|6602|서버와 클라이언트 컴퓨터 간의 통신용 공급자 프레임워크|  
  
## <a name="see-also"></a>참고 항목  
  
-   [원격 웹 액세스 사용](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md)  
  
-   [원격 웹 액세스 관리](../manage/Manage-Remote-Web-Access-in-Windows-Server-Essentials.md)  
  
-   [원격 액세스 관리](../manage/Manage-Anywhere-Access-in-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials 관리](../manage/Manage-Windows-Server-Essentials.md)  
  

-   [Windows Server Essentials 지원](Support-Windows-Server-Essentials.md)

-   [Windows Server Essentials 지원](../support/Support-Windows-Server-Essentials.md)

