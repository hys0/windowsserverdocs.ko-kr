---
title: "설치 및 Windows Server Essentials 구성"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 06/17/2013
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e95cf219-46a4-4041-bd81-0c4c2a0622cf
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: cdad118c30fbf303b55ec7ea25bbe3e209c016db
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="install-and-configure-windows-server-essentials"></a>설치 및 Windows Server Essentials 구성

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

##  <a name="BKMK_InstallConfigure"></a>   

 이 문서 설치 및 Windows Server Essentials 구성에 대 한 단계별 지침을 제공 합니다. 설치, 시작 하기 전에 검토 하 고에 대해 설명 하는 작업을 완료 [하기 전에 사용자 설치 Windows Server Essentials](Before-You-Install-Windows-Server-Essentials.md)합니다.  

 이 문서 설치 및 Windows Server Essentials 구성에 대 한 단계별 지침을 제공 합니다. 설치, 시작 하기 전에 검토 하 고에 대해 설명 하는 작업을 완료 [하기 전에 사용자 설치 Windows Server Essentials](../install/Before-You-Install-Windows-Server-Essentials.md)합니다.  
  
 설치 및 Windows Server Essentials 두 단계에서 구성 합니다.  
  

1.  [1 단계: Windows Server Essentials 운영 체제 설치](Install-and-Configure-Windows-Server-Essentials.md#BKMK_ManualInstallation) 이 단계 서버에 운영 체제 설치 합니다.  
  
2.  [2 단계: Windows Server Essentials 운영 체제의 구성](Install-and-Configure-Windows-Server-Essentials.md#BKMK_Step2Configure) 여기서, 회사, 도메인 설정 및 네트워크 관리자에 대 한 정보를 제공 하 여 설치를 완료 합니다. 이 정보를 사용 하는 서버를 사용할 수 있습니다.  

1.  [1 단계: Windows Server Essentials 운영 체제 설치](../install/Install-and-Configure-Windows-Server-Essentials.md#BKMK_ManualInstallation) 이 단계 서버에 운영 체제 설치 합니다.  
  
2.  [2 단계: Windows Server Essentials 운영 체제의 구성](../install/Install-and-Configure-Windows-Server-Essentials.md#BKMK_Step2Configure) 여기서, 회사, 도메인 설정 및 네트워크 관리자에 대 한 정보를 제공 하 여 설치를 완료 합니다. 이 정보를 사용 하는 서버를 사용할 수 있습니다.  

  
###  <a name="BKMK_ManualInstallation"></a>1 단계: Windows Server Essentials 운영 체제 설치  
  
> [!IMPORTANT]
>  운영 체제 설치 되 면 사용자 지정 하지 않은 서버 마칠 때까지 [2 단계: Windows Server Essentials 운영 체제를 구성](#BKMK_Step2Configure)합니다.  
  
 **완성 시간:** 약 30 분 정도입니다.  
  
> [!NOTE]
>  이 절차 전체 예상된 완료 번 최소 하드웨어 요구 사항을 기반으로 합니다.  
  
##### <a name="to-install-the-operating-system"></a>운영 체제 설치 하려면  
  
1.  컴퓨터가 네트워크 케이블을 사용 하 여 네트워크에 연결 합니다.  
  
    > [!IMPORTANT]
    >  설치 중 네트워크에서 컴퓨터를 끊지 마세요. 그렇게 실패 하 여 설치가 될 수 있습니다.  
  
2.  컴퓨터를 켜고 DVD 드라이브에 Windows Server Essentials DVD를 넣습니다.  
  
     자동된 설치를 수행 하는 경우 대답이 파일이 포함 된 이동식 미디어 (예: 플로피 디스크 또는 USB 플래시 드라이브)를 연결 합니다. 대답 파일의 내용에 따라 일부 또는 다음 설치 화면 하지 표시 될 수 있습니다.  
  
3.  컴퓨터를 다시 시작 합니다. 때 메시지 **CD 또는 DVD에서 부팅 하려면 아무 키나 눌러** 나타나면 아무 키나 누릅니다.  
  
    > [!NOTE]
    >  DVD에서 컴퓨터 시작 되지 않는 경우에 BIOS 부팅 순서 CD-ROM 드라이브 먼저 나열 되어 있는지 확인 합니다. BIOS 부팅 순서에 대 한 자세한 내용은 컴퓨터 제조업체에서 설명서를 참조 하세요.  
  
4.  선택는 **언어** 를 설치 하려는 **시간 및 통화 형식**, 및 **키보드 또는 입력된 방법**을 차례로 클릭 하 고 **다음**합니다.  
  
5.  클릭 **지금 설치**합니다.  
  
6.  **제품 키를 입력**, 제품 키를 입력 합니다.  
  
7.  읽기는 **사용권 계약**합니다. 동의 하면 선택는 **사용 약관에 동의** 확인란을 선택한 다음 클릭 **다음**합니다.  
  
    > [!NOTE]
    >  하는 경우 사용 약관에 동의를 선택 하지 않으면, 설치 계속 하지 않습니다.  
  
8.  **설치 유형을 원하는 수행 하나요? **, 클릭 **사용자 지정: Windows 설치만 (고급)**  
  
9. **Windows 설치를 원하는 어디 인가요? **, Windows 운영 체제를 설치 하려면 하드 드라이브를 선택 합니다. 내장 하드 드라이브의 모든를 설치 하기 위해 사용할 수 있는지 확인 합니다.  
  
    > [!IMPORTANT]
    >   Windows Server Essentials로 c: 볼륨을 설치 해야 하 고 볼륨의 크기 60 g B 이상 이어야 합니다. 운영 체제 디스크에 두 가지 파티션을 만드는 하지 비즈니스 데이터를 저장할 c: (시스템 파티션)를 사용 하는 것이 좋습니다.  
  
    > [!NOTE]
    >  하드 드라이브 (예: 직렬 고급 기술 첨부 (SATA) 하드 디스크)에 없는 경우 해당 하드 디스크에 대 한 디바이스 드라이버를 로드 해야 합니다. 제조업체에서 디바이스 드라이버를 획득 하 고 (플로피 디스크 또는 USB 플래시 드라이브와 같은) 이동식 미디어에 저장 합니다. 이동식 미디어를 컴퓨터에 연결 하 고 클릭 한 다음 **드라이버 로드**합니다.  
  
     삭제 하거나 파티션을 만드는 하려는 경우 다음 단계를 참조 하세요.  
  
    1.  파티션을 삭제 하려면을 파티션을 선택 **드라이브 옵션 (고급)**을 차례로 클릭 하 고 **삭제**합니다. 시스템 파티션 삭제 하면 두 단계 지침을 사용 하 여 새 파티션을 만드는 **b** 또는 단계 **c**합니다.  
  
        > [!NOTE]
        >  클릭 한 후 **드라이브 옵션 (고급)**, 옵션 다시 표시 되지 것입니다. 경우에 드라이브 옵션을 참조 하 여 단계 부분을 건너뜁니다.  
  
    2.  파티션을 분할 공간에서을 만들려면 하드 디스크 파티션을 클릭 하려는 클릭 **드라이브 옵션 (고급)**, 클릭 **새로**, 한 다음는 **크기** 텍스트 상자를 만들 파티션 크기를 입력 합니다. 예를 들어 120 g b 권장된 파티션 크기를 사용 하는 경우 입력 **122880**을 차례로 클릭 하 고 **적용**합니다. 파티션을 만든 후에 클릭 **다음**합니다. 설치를 계속 하기 전에 파티션 포맷 됩니다.  
  
    3.  모든 분할된 공간을 사용 하는 파티션에 만들려면 하드 디스크 파티션을 클릭 하려는 클릭 **드라이브 옵션 (고급)**, 클릭 **새로**, 클릭 한 다음 **적용** 기본 파티션 크기를 적용 해야 합니다. 파티션을 만든 후에 클릭 **다음**합니다. 설치를 계속 하기 전에 파티션 포맷 됩니다.  
  
        > [!IMPORTANT]
        >  이 단계를 완료 한 후 다른 파티션 운영 체제 이동할 수 없습니다.  
  
 설치 하는 동안 임시 파일 30 분 정도 걸리며 컴퓨터에 설치 폴더에 복사 됩니다. Windows Server Essentials 운영 체제 설치 되 면 컴퓨터를 다시 시작 합니다. 이제 Windows Server Essentials 운영 체제를 구성 준비가 되었습니다.  
  
###  <a name="BKMK_Step2Configure"></a>2 단계: Windows Server Essentials 운영 체제를 구성 합니다.  
  
> [!IMPORTANT]
>  Windows Server Essentials에는 이전 버전의 Windows Small Business Server에서 마이그레이션하는, 다른 프로세스를 수행 해야 합니다. 마이그레이션 설치에 대 한 정보를 참조 하십시오.  
>   
>  -   [Windows SBS 2003 마이그레이션](../migrate/Migrate-Windows-Small-Business-Server-2003-to-Windows-Server-Essentials.md)  
> -   [마이그레이션 SBS 2008 창에서](../migrate/Migrate-Windows-Small-Business-Server-2008-to-Windows-Server-Essentials.md)  
  
 설치가 단계 조직에 대 한 몇 가지 질문에 대답 하 라는 메시지가 표시 됩니다. 이 정보는 운영 체제를 구성 하는 데 사용 합니다.  
  
> [!IMPORTANT]
>  이 단계를 시작 하기 전에 로컬 네트워크 어댑터에 연결 되었으며 라우터 또는 켜져 스위치를 작동 제대로 있는지 확인 합니다.  
  
 **완성 시간:** 약 30 분  
  
##### <a name="to-configure-the-operating-system"></a>운영 체제의 구성 하려면  
  
1.  에 **확인 날짜 및 시간 설정을** 페이지, 클릭 **시스템 날짜 및 시간 설정을 변경** 날짜, 시간 및 표준 시간대에 대 한 서버 설정을 선택 합니다. 완료 되 면 클릭 **다음**합니다.  
  
    > [!IMPORTANT]
    >  가상 컴퓨터에서 Windows Server Essentials를 설치 하는 경우 호스트 운영 체제에서 사용 하는 동일한 표준 시간대 설정을 선택 하 고 있는지 확인 합니다. 표준 시간대 설정이 다 서버 설치 성공 하지 않을 수 있습니다.  
  
2.  에 **선택 서버 설치 모드** 페이지에서 다음 중 하나를 수행 합니다.  
  
    1.  선택 **새로 설치** Windows Server Essentials 서버 소프트웨어를 설치 하는 새로운 설정 합니다.  
  
    2.  선택 **서버 마이그레이션** 를 Windows Server Essentials를 설치 하 여이 서버 기존 Windows 도메인에 연결 합니다.  
  
3.  에 **개인 설정 하 여 서버** 페이지에서 회사의 이름, 내부 도메인 이름, 서버 이름을 입력 합니다.  
  
    > [!IMPORTANT]
    >  서버 이름 네트워크의 고유한 이름을 이어야 합니다. 이 단계를 완료 한 후 서버 이름 또는 내부 도메인 이름 변경할 수 없습니다.  
  
4.  클릭 **다음**합니다.  
  
5.  에 **관리자 계정 정보를 제공** 페이지에서 새 관리자 계정에 대 한 정보를 입력 합니다.  
  
    > [!CAUTION]
    >  관리자 또는 네트워크 관리자에 게 네트워크 관리자 계정을 이름을 지정 하지 않습니다. 이러한 계정 이름은 사용에 대 한 시스템에 의해 예약 되어 있습니다.  
  
6.  에 **표준 사용자 계정 정보를 제공** 페이지 새로운 표준 사용자 계정에 대 한 정보를 입력 한 다음 클릭 **다음**합니다.  
  
7.  에 **서버를 자동으로 최신 상태로 유지** 페이지에서 선택 하 여 서버에 대 한 Windows 업데이트를 받도록 클릭 한 다음 원하는 **다음**합니다.  
  
8.  **업데이트 서버를 준비 하 고** 페이지를 표시 하는 최종 설치 프로세스 진행 중입니다. 완료 하는 데 시간이 걸립니다이 및 컴퓨터 몇 번 다시 시작 됩니다.  
  
9. 마지막 서버 후 다시 시작, **서버 사용할 준비가 되어** 페이지가 나타납니다. 클릭 **닫기**합니다.  
  
10. 대시보드 타일을 클릭는 **시작** 화면에서 한 후 대시보드에서 완료는 **내 서버 설정** 작업에 **Home** 페이지 합니다. Windows Server Essentials 설치가 완료 된 후에 바로 이러한 작업을 완료 해야 합니다.  
  
> [!NOTE]
>  설치가 완료 되 면 자동으로 로그온 설치 과정에서 추가 하는 새로운 관리자 계정 사용 하 여 서버에 있습니다. 기본 제공 된 관리자 계정 암호 새 관리자 계정으로 동일한 암호를 설정 되 고 기본 관리자 계정 불가능 합니다.  
  
 (평가 기간 라고도 함)를 제한 된 시간에 대 한 제품 키를 입력 하지 않고 새로 설치한 서버를 사용할 수 있습니다. 평가 기간 후 정품 인증 서버 또는 평가 기간 확장 제품 키를 입력 해야 합니다. 평가 기간 최대 두 번 한 확장할 수 있습니다. 평가 기간에 허용 된 일 최대에 도달 하면 서버를 정품 인증 해야 제품 키를 사용 합니다.  
  
### <a name="customize-windows-server-essentials"></a>Windows Server Essentials 사용자 지정  
 **Home** Windows Server Essentials 대시보드의 페이지에 연결 **설치** 후 즉시 완료 되도록 해야 하는 작업 서버를 설치 합니다. 이러한 작업을 수행 하 여 서버에 저장 된 정보를 보호 하 고 Windows Server Essentials에서 사용할 수 있는 기능을 활성화할 수 있습니다.  
  
 작업을 수행 하지 않도록 선택 하면 사용자가 네트워크 일부 기능에 대 한 액세스 되지 않았을 수 있습니다. 나중에 이러한 작업을 반환 하 고 Windows Server Essentials 대시보드도 돌아갈 **Home** 페이지 합니다.  
  
 다음 표에 정의 되어 설정 작업 목록에 표시 될 수 있는 항목 합니다.  
  
|작업|설명
|----------|-----------------|  
|기타 Microsoft 제품에 대 한 업데이트 가져오기|Microsoft 업데이트를 자동으로 Windows Server Essentials 및 Office와 같은 다른 Microsoft 제품에 대 한 업데이트를 가져오는 사용 하려는 경우 지정할 수 있는 도구를 실행 하는 링크를에 액세스 하 여이 작업을 클릭 합니다.  
|사용자 계정 추가|사용자 계정 추가 대 한 간략 한 정보를 보려면이 작업을 클릭 합니다. 링크를 실행 하는 **사용자 계정 마법사 추가** 제공 됩니다. 자세한 내용은 참조 [사용자 계정을 추가](../manage/Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage1)합니다.  
|서버 폴더 추가|서버 폴더 추가 대 한 간략 한 정보를 보려면이 작업을 클릭 합니다. 링크를 실행 하는 **추가 폴더 마법사** 제공 됩니다. 서버 폴더를 사용 하는 온라인 도움말 항목에 대 한 링크는도 제공 합니다. 자세한 내용은 참조 [추가 하거나 서버 폴더 이동](../manage/Manage-Server-Folders-in-Windows-Server-Essentials.md#BKMK_5)합니다. 
|서버 백업 설정|서버 백업을 사용 하 여 데이터를 보호에 대 한 간략 한 정보를 보려면이 작업을 클릭 합니다. 링크를 실행 하 고 **서버 설정 백업 마법사** 제공 됩니다. 자세한 내용은 참조 [설정 또는 사용자 지정 서버 백업](../manage/Manage-Server-Backup-in-Windows-Server-Essentials.md#BKMK_1)합니다. 
|어디서 나 액세스를 설정|Windows Server Essentials에서 액세스 어디서 나 기능에 대 한 간략 한 정보를 보려면이 작업을 클릭 합니다. 에 대 한 링크는 **어디서 나 액세스 설정** 페이지가 제공 됩니다. 자세한 내용은 참조 [관리 어디서 나 액세스](../manage/Manage-Anywhere-Access-in-Windows-Server-Essentials.md)합니다. 
|메일 알림 설정|메일 알림에 대 한 간략 한 정보를 보려면이 작업을 클릭 합니다. 링크를 실행 하는 **알림에 대 한 메일 알림을 설정** 도구가 제공 됩니다. 자세한 내용은 참조 [알림에 대 한 메일 알림을 설정](../manage/Manage-System-Health-in-Windows-Server-Essentials.md#BKMK_Email)합니다.  
|미디어 서버 설정|음악, 동영상 및 이미지 파일 공유 미디어 서버 사용에 대 한 간략 한 정보를 보려면이 작업을 클릭 합니다. 에 대 한 링크는 **미디어 설정** 페이지가 제공 됩니다. 미디어 서버에 대 한 자세한 내용을 보려면 온라인 도움말 항목 프로그램에 대 한 링크는도 제공 합니다. 자세한 내용은 참조 [디지털 미디어 관리](../manage/Manage-Digital-Media-in-Windows-Server-Essentials.md)합니다. 
|컴퓨터에 연결|네트워크 컴퓨터 서버에 연결 하는 방법에 대 한 간략 한 정보를 보려면이 작업을 클릭 합니다. 자세한 내용은 참조 [서버에 컴퓨터를 연결](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_9)합니다.
  
## <a name="see-also"></a>참조 하십시오  
  
-   [Windows Server Essentials 설치](Install-Windows-Server-Essentials.md)

