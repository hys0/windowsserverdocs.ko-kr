---
title: "부팅 가능한 USB 플래시 드라이브를 만들기"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2fe8e35c-69f9-40b3-a270-22e2402510d8
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 9d587329e1141040b2511e1574649f1844dcec90
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="create-a-bootable-usb-flash-drive"></a>부팅 가능한 USB 플래시 드라이브를 만들기

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

Windows Server Essentials 배포 하는 데 부팅 가능한 USB 플래시 드라이브를 만들 수 있습니다. 첫 번째 단계 USB 플래시 드라이브를 사용 하 여 DiskPart, 명령줄 유틸리티 준비 하는 것입니다. DiskPart에 대 한 내용은 [DiskPart 명령줄 옵션](https://go.microsoft.com/fwlink/?LinkId=207073)합니다.  
  
 만들거나 부팅 가능한 USB를 사용 하 않도록 할 수 있는 추가 시나리오 플래시 드라이브를 다음 항목을 참조 하십시오.  
  
-   [전체 시스템 기존 클라이언트 컴퓨터 백업에서 복원](https://technet.microsoft.com/library/jj713539.aspx#BKMK_CreateBootable)  
  
-   [복원 하거나 복구 Windows Server Essentials 실행 하는 서버](https://technet.microsoft.com/library/jj593197.aspx#BKMK_Restore_2)  
  
### <a name="to-create-a-bootable-usb-flash-drive"></a>부팅 가능한 USB 플래시 드라이브를 만들려면  
  
1.  실행 중인 컴퓨터에 USB 플래시 드라이브를 삽입 합니다.  
  
2.  관리자 권한으로 명령 프롬프트 창을 엽니다.  
  
3.  입력 `diskpart`합니다.  
  
4.  열리는 명령줄 새 창에서 확인 하려면 명령 프롬프트에서 USB 플래시 드라이브 번호 또는 드라이브 문자를 입력 `list disk`, 한 다음 enter 키를 누릅니다. `list disk`명령 컴퓨터의 모든 디스크를 표시 합니다. Note 숫자 드라이브 또는 USB 플래시 드라이브의 드라이브 문자가 합니다.  
  
5.  명령 프롬프트에 입력 `select disk <X>`여기서 X 드라이브 번호 또는 드라이브 문자가 있는 usb 플래시 드라이브를 하 고 다음 enter 키를 누릅니다.  
  
6.  입력 `clean`을 ENTER 누릅니다. USB 플래시 드라이브에서 모든 데이터를 삭제 합니다.  
  
7.  새 주요 파티션을 USB 플래시 드라이브에를 만들려면 입력 `create part pri`, 한 다음 enter 키를 누릅니다.  
  
8.  입력을 선택 하려면 파티션의 방금 만든 `select part 1`, 한 다음 enter 키를 누릅니다.  
  
9. 파티션 포맷, 입력 `format fs=ntfs quick`, 한 다음 enter 키를 누릅니다.  
  
    > [!IMPORTANT]
    >  서버 플랫폼 UEFI Unified Extensible Firmware Interface ()를 지 원하는 경우 NTFS가 아닌 f a t 32로 USB 플래시 드라이브를 포맷 해야 합니다. 입력 파티션을 f a t 32로 포맷 `format fs=fat32 quick`, 한 다음 enter 키를 누릅니다.  
  
10. 입력 `active`, 한 다음 enter 키를 누릅니다.  
  
11. 입력 `exit`, 한 다음 enter 키를 누릅니다.  
  
12. 사용자 지정 이미지 준비 완료 되 면 루트 USB 플래시 드라이브에 저장 합니다.  
  
## <a name="see-also"></a>참조 하십시오  

 [Windows Server Essentials ADK 시작](Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [만들기 및 이미지를 사용자 지정](Creating-and-Customizing-the-Image.md)   
 [추가로 사용자 지정](Additional-Customizations.md)   
 [배포에 대 한 이미지를 준비 중](Preparing-the-Image-for-Deployment.md)   
 [고객 만족도 테스트합니다.](Testing-the-Customer-Experience.md)   

 [Windows Server Essentials ADK 시작](../install/Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [만들기 및 이미지를 사용자 지정](../install/Creating-and-Customizing-the-Image.md)   
 [추가로 사용자 지정](../install/Additional-Customizations.md)   
 [배포에 대 한 이미지를 준비 중](../install/Preparing-the-Image-for-Deployment.md)   
 [고객 만족도 테스트합니다.](../install/Testing-the-Customer-Experience.md)   

 [어떻게 도움이 필요 하신가요?](https://windows.microsoft.com/windows/support)
