---
title: "전체 서버 백업-광고 숲 복구"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 398918dc-c8ab-41a6-a377-95681ec0b543
ms.technology: identity-adfs
ms.openlocfilehash: b1af97c2eb23d65c2d106906bc0f5bb1f10b23ec
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="ad-forest-recovery---backing-up-a-full-server"></a>전체 서버 백업-광고 숲 복구  

>Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 r 2에 적용 됩니다.

전체 서버 백업은 다양 한 하드웨어 또는 다른 운영 체제 인스턴스를 복원할 수 있으므로 숲 복구를 위해 준비 것이 좋습니다.  Windows Server 백업을 사용 하 여 서버의 전체 백업을 수행할 수 있습니다. 

## <a name="windows-server-backup"></a>Windows Server 백업
Windows Server 백업 기본적으로 설치 되지 않습니다. Windows Server 2016 및 Windows Server 2012 r 2의 경우 다음 단계를 수행 하 여 설치 합니다.

>[!NOTE]
>단계는 다를 수 있습니다 약간 Windows Server 2016와 Windows Server 2012 r 2 주의 해야 합니다.

Windows Server 2008 및 Windows Server 2008 r 2에 설치 하는 단계를 참조 하세요. [Windows Server 백업 설치](https://technet.microsoft.com/library/cc771232.aspx)합니다.  

### <a name="to-install-windows-server-backup"></a>Windows Server 백업을 설치 하려면
1. 열린 **서버 관리자** 클릭 **역할 및 기능을 추가**합니다.
2. 에 **역할 추가 및 기능 마법사** 클릭 **다음**합니다.
3. 에 **설치 유형을** 화면에서 기본 된 상태로 둡니다 **역할 또는 기능 기반 설치** 클릭 **다음**합니다.
4. 에 **서버 선택** 화면에서 클릭 **다음**합니다.
5. 에 **서버 역할** 화면 클릭 **다음**합니다.
6. 에 **기능** 화면에서 **Windows Server 백업** 클릭 **다음**<ph x="4">
! [</ph> 백업을 설치합니다](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup2.png)
7. 클릭 **설치**합니다.
8. 설치가 완료 되 면 클릭 **닫기**합니다.


### <a name="to-perform-a-backup-with-windows-server-backup"></a>Windows Server 백업 백업

1. 열기 **서버 관리자**, 클릭 **도구**을 차례로 클릭 하 고 **Windows Server 백업**합니다.
    - Windows Server 2008 R2 및 Windows Server 2008 **시작**를 가리킨 **관리 도구**을 차례로 클릭 하 고 **Windows Server 백업**합니다. 
![백업을 설치합니다](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup1.png) 
2. 라는 메시지가 나타나면에 **사용자 계정 컨트롤** 대화 상자에서 백업을 통신사 자격 증명을 제공 하 고 클릭 한 다음 **확인**합니다.
3. 클릭 **로컬 백업**합니다.
4. 에 **알림** 메뉴를 클릭 **번 백업**합니다.
5. 백업 한 번 마법사에서에 **백업 옵션** 페이지, 클릭 **다른 옵션**을 차례로 클릭 하 고 **다음**합니다.
![백업을 설치합니다](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup3.png)
6. 에 **선택 하 고 백업 구성** 페이지, 클릭 **전체 서버 (권장)**을 차례로 클릭 하 고 **다음**합니다.
7. 에 **종류 목적지를 지정** 페이지, 클릭 **로컬 드라이브** 또는 **Remote 공유 폴더**을 차례로 클릭 하 고 **다음**합니다.
8. 에 **백업이 저장 위치 선택** 페이지 백업 위치를 선택 합니다.  로컬 선택한 경우 드라이브 로컬 드라이브를 선택 하거나 공유 원격 선택한 경우 네트워크 공유를 선택 합니다.
9. 확인 화면에서 클릭 **백업**합니다.
![백업을 설치합니다](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup4.png)
10. 이 완료 되 면 클릭 **닫기**합니다.
11. Windows Server 백업을 닫습니다.

>[!NOTE]
>없이 백업 저장 위치를 사용할 수 없다는 오류 메시지가 경우 제외 볼륨 선택 된 중 하나 하거나 원격 공유 또는 새 볼륨 추가 해야 합니다.
>백업할 항목 목록에서 선택한 볼륨도 포함 됩니다 경고 메시지가 표시를 받을 경우 있는지를 확인을 제거 하 고 클릭 **확인**합니다.

## <a name="using-wbadminexe-to-backup-a-windows-server"></a>Wbadmin.exe를 사용 하 여 windows server를 백업 하려면
Wbadmin.exe 백업 및 명령 프롬프트에서 운영 체제, 볼륨, 파일, 폴더 및 응용 프로그램을 복원할 수 있도록 명령줄 유틸리티입니다.

#### <a name="to-perform-a-full-server-backup-using-wbadminexe"></a>전체 서버 백업을 Wbadmin.exe를 사용 하 여 수행 하려면  
  
1.  관리자 명령 프롬프트를 열고, 다음 명령을 입력 하 고 ENTER 키를 누릅니다.  

        wbadmin start backup -backuptarget:<Drive_letter_to store_backup>: -include:<Drive_letter_to_include>:

![백업을 설치합니다](media/AD-Forest-Recovery-Backing-up-a-Full-Server/fullbackup5.png)
## <a name="next-steps"></a>다음 단계

- [광고 포리스트 복구 가이드](AD-Forest-Recovery-Guide.md)
- [광고 숲 복구 절차](AD-Forest-Recovery-Procedures.md)
