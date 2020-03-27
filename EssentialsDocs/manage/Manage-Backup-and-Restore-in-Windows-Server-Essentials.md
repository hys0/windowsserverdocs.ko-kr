---
title: Windows Server Essentials에서 백업 및 복원 관리(영문)
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 41000915-f6ff-4dbb-b7be-629ef36386d4
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 37435b8b51bbc6ba4deb09a50f2c85045ecf0536
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80311368"
---
# <a name="manage-backup-and-restore-in-windows-server-essentials"></a>Windows Server Essentials에서 백업 및 복원 관리(영문)

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials
 
 Windows Server Essentials에서는 정기적인 서버 백업 및 네트워크 컴퓨터 백업을 수행하는 안정적인 방법을 제공합니다. 데이터가 손실될 경우 전체 컴퓨터를 복원하지 않고 서버의 성공한 백업에서 데이터를 복원할 수 있습니다. 필요하면 네트워크의 클라이언트 컴퓨터 또는 서버로 전체 시스템을 복원할 수 있습니다. 다음 표에서는 사용할 수 있는 다양한 백업 옵션과 해당 이점을 함께 설명합니다.  
  
|백업 기능|설명|장점|  
|--------------------|-----------------|----------------|  
|서버 백업|Windows Server Essentials를 실행하는 서버를 백업합니다. 데이터가 외부 USB 드라이브로 백업됩니다.<br /><br /> 자세한 내용은 서버 [백업 관리](Manage-Server-Backup-in-Windows-Server-Essentials.md) 및 [서버 복원 또는 복구](Restore-or-repair-your-server-running-Windows-Server-Essentials.md)를 참조 하세요.|-서버에서 파일과 폴더를 복원할 수 있습니다.<br /><br /> -서버의 전체 시스템 복원을 수행할 수 있습니다.|  
|클라이언트 컴퓨터 백업|네트워크에 있는 클라이언트 컴퓨터를 백업합니다. 데이터가 Windows Server Essentials를 실행하는 서버에 백업됩니다.<br /><br /> 자세한 내용은 [클라이언트 백업 관리](Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md) 및 [기존 클라이언트 컴퓨터 백업에서 전체 시스템 복원](Restore-a-full-system-from-an-existing-client-computer-backup.md)을 참조 하세요.|-서버에서 파일과 폴더를 복원할 수 있습니다.<br /><br /> -클라이언트 컴퓨터의 전체 시스템 복원을 수행할 수 있습니다.|  
| Microsoft Azure Backup|서버에서 파일 또는 폴더의 온라인 백업을 수행합니다. Azure Backup를 사용 하 여 서버 데이터를 백업 하는 경우 정보는 암호를 사용 하 여 암호화 된 후 인터넷의 보안 데이터 센터로 업로드 됩니다.<br /><br /> 자세한 내용은 [온라인 백업 관리](Manage-Online-Backup-in-Windows-Server-Essentials.md)를 참조 하세요.|-서버에서 파일과 폴더를 복원할 수 있습니다.<br /><br /> -증분 백업을 사용 하는 경우 파일에 대 한 변경 내용만 클라우드에 전송 됩니다.<br /><br /> -백업은 Microsoft Azure에 저장 되 고 오프 사이트에 있으므로 온사이트 백업 미디어를 보호 하 고 보호할 필요성이 줄어듭니다.|  
  
## <a name="see-also"></a>참고 항목  
  
-   [Windows Server Essentials 관리](Manage-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials 사용](../use/Use-Windows-Server-Essentials.md)
