---
title: '3단계: 새 Windows Server Essentials 서버에 컴퓨터 연결'
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a0e07d1a-8409-429b-87d7-0f4a7e14d668
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 1ca1e3a031c95f19fb68aadcf203b13fa39d7558
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80318766"
---
# <a name="step-3-join-computers-to-the-new-windows-server-essentials-server"></a>3단계: 새 Windows Server Essentials 서버에 컴퓨터 연결

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

마이그레이션 프로세스의 다음 단계는 Windows Server Essentials를 실행 하는 새 서버에 클라이언트 컴퓨터를 연결 하는 것입니다.  
  
> [!NOTE]
>  Windows XP 또는 Windows Vista 운영 체제를 실행하는 컴퓨터에서는 이 단계를 건너뛸 수 있습니다. Windows Server Connector 소프트웨어에서는 Windows XP 또는 Windows Vista를 실행 중인 컴퓨터를 지원하지 않습니다.  
  
 클라이언트 컴퓨터를 새 Windows Server Essentials 서버에 연결 하려면 먼저 클라이언트 컴퓨터에서 Windows Server Connector 소프트웨어를 제거 하 여 원본 서버에서 해당 컴퓨터의 연결을 끊어야 합니다.  
  
### <a name="to-uninstall-windows-server-connector-on-a-client-computer"></a>클라이언트 컴퓨터에서 Windows Server Connector를 제거하려면  
  
1.  클라이언트 컴퓨터에서 제어판을 열고 **프로그램 및 기능**을 엽니다.  
  
2.  프로그램 목록에서 컴퓨터에서 실행되고 있는 Connector 애플리케이션을 마우스 오른쪽 단추로 클릭합니다.  
  
    > [!NOTE]
    >  커넥터 응용 프로그램은 클라이언트 컴퓨터가 연결 된 Windows Server Essentials 버전에 따라 **Windows Small Business Server 2011 Essentials connector**또는 **Windows server essentials connector**일 수 있습니다.  
  
3.  **제거**를 클릭합니다.  
  
### <a name="to-reconnect-a-client-computer-to-the-server"></a>서버에 클라이언트 컴퓨터를 다시 연결하려면  
  
1.  서버에 연결하려는 컴퓨터에 로그인합니다.  
  
    > [!NOTE]
    >  이 컴퓨터에 사용자 계정이 여러 개 있는 경우 컴퓨터를 서버에 연결한 후 유지하려는 문서, 사진 및 개인 기본 설정이 있는 사용자 계정을 사용하여 로그인합니다.  
  
2.  Internet Explorer와 같은 인터넷 브라우저를 엽니다.  
  
3.  주소 표시줄에 **http://< servername\>/Connect**를 입력 한 다음 enter 키를 누릅니다.  
  
4.  화면의 지침에 따라 클라이언트 컴퓨터를 새 Windows Server Essentials 서버에 연결 합니다.  
  
## <a name="next-steps"></a>다음 단계  
 클라이언트 컴퓨터를 Windows Server Essentials를 실행 하는 새 서버에 조인 했습니다. 이제 [4 단계: Windows Server Essentials 마이그레이션을 위해 대상 서버로 설정 및 데이터 이동](Step-4--Move-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md)으로 이동 합니다.  
  

모든 단계를 보려면 [Windows Server Essentials로 마이그레이션](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md)을 참조 하세요.

