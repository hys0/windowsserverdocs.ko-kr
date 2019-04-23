---
title: '3단계: 새 Windows Server Essentials 서버에 컴퓨터 연결'
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a0e07d1a-8409-429b-87d7-0f4a7e14d668
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: f71ac280e2de0b7d945f2d979fe52d173f7c3323
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59861874"
---
# <a name="step-3-join-computers-to-the-new-windows-server-essentials-server"></a>3단계: 새 Windows Server Essentials 서버에 컴퓨터 연결

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

마이그레이션 프로세스의 다음 단계는 Windows Server Essentials를 실행 하는 새 서버에 클라이언트 컴퓨터를 연결 하는 것입니다.  
  
> [!NOTE]
>  Windows XP 또는 Windows Vista 운영 체제를 실행하는 컴퓨터에서는 이 단계를 건너뛸 수 있습니다. Windows Server Connector 소프트웨어에서는 Windows XP 또는 Windows Vista를 실행 중인 컴퓨터를 지원하지 않습니다.  
  
 새 Windows Server Essentials 서버에는 클라이언트 컴퓨터를 조인할 수 있습니다, 전에 클라이언트 컴퓨터의 Windows Server Connector 소프트웨어를 제거 하 여 원본 서버에서 분리 해야 합니다.  
  
### <a name="to-uninstall-windows-server-connector-on-a-client-computer"></a>클라이언트 컴퓨터에서 Windows Server Connector를 제거하려면  
  
1.  클라이언트 컴퓨터에서 제어판을 열고 **프로그램 및 기능**을 엽니다.  
  
2.  프로그램 목록에서 컴퓨터에서 실행되고 있는 Connector 응용 프로그램을 마우스 오른쪽 단추로 클릭합니다.  
  
    > [!NOTE]
    >  커넥터 응용 프로그램 일 수 있습니다 **Windows Small Business Server 2011 Essentials Connector**, 또는 **Windows Server Essentials Connector**Windows Server Essentials 버전에 따라는 클라이언트 컴퓨터에 연결 되었습니다.  
  
3.  **제거**를 클릭합니다.  
  
### <a name="to-reconnect-a-client-computer-to-the-server"></a>서버에 클라이언트 컴퓨터를 다시 연결하려면  
  
1.  서버에 연결하려는 컴퓨터에 로그인합니다.  
  
    > [!NOTE]
    >  이 컴퓨터에 사용자 계정이 여러 개 있는 경우 컴퓨터를 서버에 연결한 후 유지하려는 문서, 사진 및 개인 기본 설정이 있는 사용자 계정을 사용하여 로그인합니다.  
  
2.  Internet Explorer와 같은 인터넷 브라우저를 엽니다.  
  
3.  주소 표시줄에 입력 **http://<servername\>/connect**, 한 다음 ENTER를 누릅니다.  
  
4.  새 Windows Server Essentials 서버에 클라이언트 컴퓨터를 가입 하려면 화면의 지침을 따릅니다.  
  
## <a name="next-steps"></a>다음 단계  
 클라이언트 컴퓨터에서 Windows Server Essentials를 실행 하는 새 서버에 가입한 합니다. 이제 [4 단계: 서버에 대 한 Windows Server Essentials 마이그레이션을 위해 대상 설정 및 데이터 이동](Step-4--Move-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md)합니다.  
  

모든 단계를 보려면 [Windows Server Essentials로 마이그레이션](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md)합니다.

