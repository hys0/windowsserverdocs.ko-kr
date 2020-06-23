---
title: Windows Server Essentials에서 원격 액세스 문제 해결
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: 68f2b05c-09eb-4cba-8db4-a91353b513c6
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 313b4fae48a5b70cb16cae0cfb3a7bc048ef97a3
ms.sourcegitcommit: 56ac7cf3f4bbcc5175f140d2df5f37cc42ba76d1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85217563"
---
# <a name="troubleshoot-anywhere-access-in-windows-server-essentials"></a>Windows Server Essentials에서 원격 액세스 문제 해결

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

이 항목에서는 Windows Server Essentials에서 원격 액세스 복구 마법사를 사용 하 여 네트워크 사용자가 서버 리소스에 액세스 하지 못하는 문제를 해결 하는 방법에 대 한 일반적인 지침을 제공 합니다. 원격 액세스 기능-원격 웹 액세스, VPN (가상 사설망) 및 DirectAccess-네트워크 사용자가 언제 어디서 든 인터넷에 연결 된 모든 장치에서 서버 리소스에 액세스할 수 있습니다.  
  
 원격 액세스 복구 마법사는 네트워크 사용자가 원격으로 서버 리소스에 액세스하지 못하게 하는 라우터, 도메인 이름 또는 방화벽 문제를 식별하여 해결하려고 시도합니다.  
  
> [!NOTE]
>  Windows Server Essentials 커뮤니티에서 제공 하는 최신 문제 해결 정보는 [Windows Server Essentials 포럼](https://social.technet.microsoft.com/Forums/winserveressentials/threads)을 참조 하는 것이 좋습니다. Windows Server Essentials 포럼은 도움말을 검색하거나 질문하기 좋은 곳입니다.  
  
### <a name="to-repair-anywhere-access"></a>원격 액세스를 복구하려면  
  
1.  서버에 로그온하여 대시보드를 엽니다.  
  
2.  **설정**을 클릭한 다음 **원격 액세스** 탭을 클릭합니다.  
  
3.  **복구**를 클릭합니다. 원격 액세스 복구 마법사가 시작됩니다.  
  
4.  **다음**을 클릭합니다. 마법사가 원격 액세스를 분석하여 문제를 식별한 후 문제를 해결하려고 합니다.  
  
5.  마법사가 완료될 때 경고가 표시되면 **다시 시도**를 클릭하여 문제를 다시 복구해 봅니다. 경고가 계속 표시되는 경우 경고에서 문제 및 문제 해결 단계에 대한 추가 정보를 확인하세요.  
  
### <a name="to-get-more-information-about-an-alert"></a>경고에 대한 추가 정보를 확인하려면  
  
1.  대시보드 오른쪽 위에서 오류 또는 경고 아이콘을 클릭하여 경고 뷰어를 엽니다.  
  
2.  경고 뷰어에서 오류 또는 경고를 클릭하여 추가 정보를 봅니다.  
  
## <a name="additional-troubleshooting-for-anywhere-access"></a>원격 액세스의 추가 문제 해결  
 원격 액세스 복구 마법사에서 원격 액세스를 복구할 수 없는 경우 원격 웹 액세스, VPN 및 DirectAccess와 관련된 문제에 대한 다음 문제 해결 리소스를 확인하세요.  
  

-   [원격 웹 액세스 연결 문제 해결](Troubleshoot-Remote-Web-Access-connectivity-in-Windows-Server-Essentials.md)  
  
-   [방화벽 문제 해결](Troubleshoot-your-firewall-in-Windows-Server-Essentials.md)
  
-   Windows server essentials 커뮤니티에서 보고 한 최신 문제는 [Windows Server Essentials 포럼](https://social.technet.microsoft.com/Forums/winserveressentials/threads) 을 참조 하세요.
