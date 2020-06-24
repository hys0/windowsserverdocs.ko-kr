---
title: 부팅 가능 USB 플래시 드라이브 만들기
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.date: 05/04/2018
ms.prod: windows-server
ms.topic: article
ms.assetid: 2fe8e35c-69f9-40b3-a270-22e2402510d8
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 69a57333990a225663d2cd3cc61c75947d07cdab
ms.sourcegitcommit: 6d6a0225b1f83b71fcb494b94d666cd5e54c7566
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85267374"
---
# <a name="create-a-bootable-usb-flash-drive"></a>부팅 가능 USB 플래시 드라이브 만들기

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Windows Server Essentials를 배포 하는 데 사용할 부팅 가능 USB 플래시 드라이브를 만들 수 있습니다. 첫 번째 단계는 명령줄 유틸리티인 DiskPart를 사용하여 USB 플래시 드라이브를 준비하는 것입니다. DiskPart에 관한 자세한 내용은 [DiskPart 명령줄 옵션](https://go.microsoft.com/fwlink/?LinkId=207073)을 참조하세요.  


> [!TIP]
> 서버 대신 PC에서 Windows를 복구 하거나 다시 설치 하는 데 사용할 부팅 가능 USB 플래시 드라이브를 만들려면 [복구 드라이브 만들기](https://support.microsoft.com/help/4026852/windows-create-a-recovery-drive)를 참조 하세요.
  
 부팅 가능 USB 플래시 드라이브를 만들거나 사용할 수 있는 추가적인 시나리오는 다음 항목을 참조하세요.  
  
-   [기존 클라이언트 컴퓨터 백업으로 전체 시스템 복원](../manage/restore-a-full-system-from-an-existing-client-computer-backup.md)  
  
-   [Windows Server Essentials를 실행하는 서버 복원 또는 복구](../manage/restore-or-repair-your-server-running-windows-server-essentials.md)  

  
### <a name="to-create-a-bootable-usb-flash-drive"></a>부팅 가능 USB 플래시 드라이브를 만들려면  
  
1.  실행 중인 컴퓨터에 USB 플래시 드라이브를 삽입합니다.  
  
2.  관리자로 명령 프롬프트 창을 엽니다.  
  
3.  `diskpart`.  
  
4.  새 명령줄 창이 열리면 USB 플래시 드라이브 숫자 또는 드라이브 문자를 결정하고 명령 프롬프트에 `list disk`을(를) 입력한 후 ENTER를 클릭합니다. `list disk` 명령이 컴퓨터에 있는 모든 디스크를 표시합니다. USB 플래시 드라이브의 드라이브 번호 또는 드라이브 문자를 확인합니다.  
  
5.  명령 프롬프트에 `select disk <X>`를 입력합니다. 여기서 X는 USB 플래시 드라이브의 드라이브 번호 또는 드라이브 문자입니다. 그런 다음 Enter 키를 누릅니다.  
  
6.  `clean`을(를) 입력한 다음 ENTER 키를 누릅니다. 이 명령은 USB 플래시 드라이브에서 모든 데이터를 삭제합니다.  
  
7.  USB 플래시 드라이브에서 새 주 파티션을 만들려면 `create partition primary`를 입력한 다음 Enter 키를 누릅니다.  
  
8.  방금 만든 파티션을 선택하려면 `select partition 1`을 입력한 다음 Enter 키를 누릅니다.  
  
9. 파티션을 포맷하려면 `format fs=ntfs quick`을(를) 입력한 다음 ENTER 키를 누릅니다.  
  
    > [!IMPORTANT]
    >  서버 플랫폼에서 UEFI(Unified Extensible Firmware Interface)를 지원하는 경우 USB 플래시 드라이브를 NTFS가 아니라 FAT32로 포맷해야 합니다. 파티션을 FAT32로 포맷하려면 `format fs=fat32 quick`을 입력한 다음 Enter 키를 누릅니다.  
  
10. `active`을(를) 입력한 다음 Enter 키를 누릅니다.  
  
11. `exit`을(를) 입력한 다음 Enter 키를 누릅니다.  
  
12. 사용자 지정 이미지 준비가 완료되면 해당 이미지를 USB 플래시 드라이브 루트에 저장합니다.  
  
## <a name="see-also"></a>참고 항목  

 [Windows Server Essentials ADK 시작 하기](Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [이미지 만들기 및 사용자 지정](Creating-and-Customizing-the-Image.md)   
 [추가 사용자 지정](Additional-Customizations.md)   
 [배포를 위한 이미지 준비](Preparing-the-Image-for-Deployment.md)   
 [사용자 환경 테스트](Testing-the-Customer-Experience.md)     

 [도움 요청하기](https://windows.microsoft.com/windows/support)
