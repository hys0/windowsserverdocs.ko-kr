---
title: Windows Server Essentials 설치 및 구성
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.custom: na
ms.date: 06/17/2013
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e95cf219-46a4-4041-bd81-0c4c2a0622cf
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 600aea223ebf48e1370f06070a4c3db7329c6f2f
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80311650"
---
# <a name="install-and-configure-windows-server-essentials"></a>Windows Server Essentials 설치 및 구성

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

##  <a name="BKMK_InstallConfigure"></a>   

 이 문서에서는 Windows Server Essentials를 설치 및 구성 하는 방법에 대 한 단계별 지침을 제공 합니다. 설치를 시작 하기 전에 [Windows Server Essentials를 설치 하기 전에](Before-You-Install-Windows-Server-Essentials.md)에 설명 된 작업을 검토 하 고 완료 합니다.  

 이 문서에서는 Windows Server Essentials를 설치 및 구성 하는 방법에 대 한 단계별 지침을 제공 합니다. 설치를 시작 하기 전에 [Windows Server Essentials를 설치 하기 전에](../install/Before-You-Install-Windows-Server-Essentials.md)에 설명 된 작업을 검토 하 고 완료 합니다.  
  
 Windows Server Essentials는 다음과 같은 두 단계로 설치 하 고 구성 합니다.  
  

1.  [1 단계: Windows Server Essentials 운영 체제 설치](Install-and-Configure-Windows-Server-Essentials.md#BKMK_ManualInstallation) 이 단계에서는 서버에 운영 체제를 설치 합니다.  
  
2.  [2 단계: Windows Server Essentials 운영 체제 구성](Install-and-Configure-Windows-Server-Essentials.md#BKMK_Step2Configure) 이 단계에서는 회사, 도메인 설정 및 네트워크 관리자에 대 한 정보를 제공 하 여 설치를 완료 합니다. 이러한 정보는 서버를 사용할 수 있도록 준비하는 데 사용됩니다.  

1.  [1 단계: Windows Server Essentials 운영 체제 설치](../install/Install-and-Configure-Windows-Server-Essentials.md#BKMK_ManualInstallation) 이 단계에서는 서버에 운영 체제를 설치 합니다.  
  
2.  [2 단계: Windows Server Essentials 운영 체제 구성](../install/Install-and-Configure-Windows-Server-Essentials.md#BKMK_Step2Configure) 이 단계에서는 회사, 도메인 설정 및 네트워크 관리자에 대 한 정보를 제공 하 여 설치를 완료 합니다. 이러한 정보는 서버를 사용할 수 있도록 준비하는 데 사용됩니다.  

  
###  <a name="step-1-install-the-windows-server-essentials-operating-system"></a><a name="BKMK_ManualInstallation"></a>1 단계: Windows Server Essentials 운영 체제 설치  
  
> [!IMPORTANT]
>  운영 체제가 설치 된 후에는 [2 단계: Windows Server Essentials 운영 체제 구성](#BKMK_Step2Configure)을 완료할 때까지 서버를 사용자 지정 하지 마십시오.  
  
 **예상 완료 시간:** 약 30분입니다.  
  
> [!NOTE]
>  이 절차의 예상 완료 시간은 최소 하드웨어 요구 사항을 기준으로 합니다.  
  
##### <a name="to-install-the-operating-system"></a>운영 체제를 설치하려면  
  
1. 네트워크 케이블을 사용하여 컴퓨터를 네트워크에 연결합니다.  
  
   > [!IMPORTANT]
   >  설치 도중에 컴퓨터의 네트워크 연결을 끊지 마세요. 설치가 실패할 수 있습니다.  
  
2. 컴퓨터를 켠 다음 DVD 드라이브에 Windows Server Essentials DVD를 삽입 합니다.  
  
    무인 설치를 수행하는 경우에는 응답 파일이 포함된 플로피 디스크나 USB 플래시 드라이브와 같은 이동식 미디어를 연결하세요. 응답 파일의 내용에 따라 다음 설치 화면 중 전체나 일부가 표시되지 않을 수 있습니다.  
  
3. 컴퓨터를 다시 시작합니다. **CD 또는 DVD에서 부팅하려면 아무 키나 누르세요.** 라는 메시지가 나타나면 아무 키나 누릅니다.  
  
   > [!NOTE]
   >  컴퓨터가 DVD에서 시작되지 않으면 BIOS 부팅 시퀀스에서 CD-ROM 드라이브가 첫 번째로 나열되어 있는지 확인합니다. BIOS 부팅 시퀀스에 대한 자세한 내용은 컴퓨터 제조업체의 설명 문서를 참조하세요.  
  
4. 설치할 **언어**를 선택하고 **시간 및 통화 형식** 및 **키보드 또는 입력 메서드**를 선택한 후 **다음**을 클릭합니다.  
  
5. **지금 설치**를 클릭합니다.  
  
6. **제품 키 입력**에서 제품 키를 입력합니다.  
  
7. **사용 조건**을 읽어 봅니다. 조건에 동의하면 **동의함** 확인란을 선택한 후 **다음**을 클릭합니다.  
  
   > [!NOTE]
   >  사용 조건에 동의하지 않는 경우 설치가 계속 진행되지 않습니다.  
  
8. **설치 유형을 선택하십시오.** 에서 **사용자 지정: Windows만 설치(고급)** 를 클릭합니다.  
  
9. **Windows를 설치할 위치를 지정하세요.** 에서 Windows 운영 체제를 설치할 하드 드라이브를 선택합니다. 모든 내부 하드 드라이브를 설치에 사용할 수 있는지 확인합니다.  
  
    > [!IMPORTANT]
    >   Windows Server Essentials는 C: 볼륨으로 설치 해야 하 고 볼륨 크기는 60 이상 이어야 합니다. 운영 체제 디스크를 두 개의 파티션으로 나누고 C:(시스템 파티션)에는 비즈니스 데이터를 저장하지 않는 것이 좋습니다.  
  
    > [!NOTE]
    >  하드 드라이브가 목록에 표시되지 않으면(예: SATA(Serial Advanced Technology Attachment) 하드 디스크) 해당 하드 디스크의 디바이스 드라이버를 로드해야 합니다. 제조업체에서 디바이스 드라이버를 구하여 플로피 디스크나 USB 플래시 드라이브와 같은 이동식 미디어에 저장합니다. 이동식 미디어를 컴퓨터에 연결한 후 **드라이버 로드**를 클릭합니다.  
  
     파티션을 삭제 및/또는 만들어야 하는 경우 다음 단계를 참조하세요.  
  
    1.  파티션을 삭제하려면 파티션을 선택하고 **드라이브 옵션(고급)** 을 클릭한 후 **삭제**를 클릭합니다. 시스템 파티션을 삭제한 후 **b** 단계 또는 **c** 단계의 지침을 사용하여 새 파티션을 만듭니다.  
  
        > [!NOTE]
        >  **드라이브 옵션(고급)** 을 클릭한 후에는 이 옵션이 다시 나타나지 않습니다. 이런 경우에는 단계에서 드라이브 옵션을 참조하는 부분을 건너뜁니다.  
  
    2.  분할되지 않은 공간에서 파티션을 만들려면 파티션을 분할할 하드 디스크를 클릭한 후 **드라이브 옵션(고급)** 및 **새로 만들기**를 클릭하고 **크기** 텍스트 상자에 만들 파티션 크기를 입력합니다. 예를 들어 권장 파티션 크기인 120GB(기가바이트)를 사용하려면 **122880**을 입력한 후 **적용**을 클릭합니다. 파티션이 만들어지면 **다음**을 클릭합니다. 파티션이 포맷된 후 설치가 계속됩니다.  
  
    3.  분할되지 않은 공간을 모두 사용하는 파티션을 만들려면 파티션을 만들 하드 디스크를 클릭한 후 **드라이브 옵션(고급)** 및 **새로 만들기**를 클릭하고 **적용**을 클릭하여 기본 파티션 크기를 사용합니다. 파티션이 만들어지면 **다음**을 클릭합니다. 파티션이 포맷된 후 설치가 계속됩니다.  
  
        > [!IMPORTANT]
        >  이 단계를 마친 후엔 운영 체제를 다른 파티션으로 이동할 수 없습니다.  
  
   설치하는 동안 컴퓨터의 설치 폴더로 임시 파일이 복사되며 여기에 30분 정도 소요됩니다. Windows Server Essentials 운영 체제가 설치 된 후 컴퓨터가 다시 시작 됩니다. 이제 Windows Server Essentials 운영 체제를 구성할 준비가 되었습니다.  
  
###  <a name="step-2-configure-the-windows-server-essentials-operating-system"></a><a name="BKMK_Step2Configure"></a>2 단계: Windows Server Essentials 운영 체제 구성  
  
> [!IMPORTANT]
>  이전 버전의 Windows Small Business Server에서 Windows Server Essentials로 마이그레이션하려는 경우에는 다른 프로세스를 따라야 합니다. 마이그레이션 설치에 대한 자세한 내용은 다음을 참조하세요.  
> 
> - [Windows SBS 2003에서 마이그레이션](../migrate/Migrate-Windows-Small-Business-Server-2003-to-Windows-Server-Essentials.md)  
>   -   [Windows SBS 2008에서 마이그레이션](../migrate/Migrate-Windows-Small-Business-Server-2008-to-Windows-Server-Essentials.md)  
  
 이 설치 단계에서 조직에 대한 몇 가지 질문에 답해야 하는 메시지가 표시됩니다. 이러한 정보는 운영 체제를 구성하는 데 사용됩니다.  
  
> [!IMPORTANT]
>  이 단계를 시작하기 전에 켜져 있고 제대로 작동하는 라우터 또는 스위치에 로컬 네트워크 어댑터가 연결되어 있는지 확인합니다.  
  
 **예상 완료 시간:** 약 30분입니다.  
  
##### <a name="to-configure-the-operating-system"></a>운영 체제를 구성하려면  
  
1.  **날짜 및 시간 설정 확인** 페이지에서 **시스템 날짜 및 시간 설정 변경**을 클릭하여 서버의 날짜, 시간 및 표준 시간대 설정을 선택합니다. 작업이 완료되면 **다음**을 클릭합니다.  
  
    > [!IMPORTANT]
    >  가상 컴퓨터에 Windows Server Essentials를 설치 하는 경우 호스트 운영 체제에서 사용 되는 것과 동일한 표준 시간대 설정을 선택 해야 합니다. 표준 시간대 설정이 다르면 서버가 설치되지 않을 수도 있습니다.  
  
2.  **서버 설치 모드 선택** 페이지에서 다음 중 하나를 수행합니다.  
  
    1.  Windows Server Essentials 서버 소프트웨어의 전체 새로 설치를 설정 하려면 **새로 설치** 를 선택 합니다.  
  
    2.  **서버 마이그레이션** 을 선택 하 여 Windows server Essentials를 설치 하 고이 서버를 기존 windows 도메인에 연결 합니다.  
  
3.  **서버 개인 설정** 페이지에서 조직 이름, 내부 도메인 이름 및 서버 이름을 입력합니다.  
  
    > [!IMPORTANT]
    >  서버 이름은 네트워크에서 고유한 이름이어야 합니다. 이 단계를 마친 후에는 서버 이름 또는 내부 도메인 이름을 변경할 수 없습니다.  
  
4.  **다음**을 클릭합니다.  
  
5.  **관리자 계정 정보 입력** 페이지에서 새 관리자 계정의 정보를 입력합니다.  
  
    > [!CAUTION]
    >  네트워크 관리자 계정 관리자 또는 네트워크 관리자의 이름을로 하지 마십시오. 이 계정 이름은 시스템에서 사용하도록 예약되어 있습니다.  
  
6.  **표준 사용자 계정 정보 입력** 페이지에서 새 표준 사용자 계정의 정보를 입력한 후 **다음**을 클릭합니다.  
  
7.  **서버를 자동으로 최신 상태로 유지** 페이지에서 서버에 대한 Windows Update를 받을 방법을 선택한 후 **다음**을 클릭합니다.  
  
8.  **서버를 업데이트 및 준비하는 중** 페이지에 최종 설치 프로세스 진행 상황이 표시됩니다. 이 단계는 완료되는 데 시간이 걸리며 컴퓨터가 몇 번 다시 시작됩니다.  
  
9. 마지막 서버가 다시 시작된 후 **서버를 사용할 준비가 되었습니다.** 페이지가 나타납니다. **닫기**를 클릭합니다.  
  
10. **시작** 화면에서 대시보드 타일을 클릭한 후 대시보드에서 **홈** 페이지의 **서버 설정** 작업을 완료합니다. 이러한 작업은 Windows Server Essentials 설치가 완료 된 직후에 완료 해야 합니다.  
  
> [!NOTE]
>  설치를 마치고 나면 설치 도중에 추가한 관리자 계정을 사용하여 자동으로 서버에 로그온됩니다. 기본 제공 관리자 계정 암호는 새 관리자 계정과 동일한 암호로 설정되어 있으며, 기본 제공 관리자 계정은 사용하지 않도록 설정되어 있습니다.  
  
 새로 설치 된 서버는 제품 키를 입력 하지 않고 제한 된 시간 (평가 기간 이라고 함)에 사용할 수 있습니다. 평가 기간 후에는 제품 키를 입력하여 서버를 정품 인증하거나 평가 기간을 연장해야 합니다. 평가 기간은 최대 2회 연장할 수 있습니다. 평가 기간으로 허용되는 최대 날짜 수에 도달하면 제품 키를 사용하여 서버를 정품 인증해야 합니다.  
  
### <a name="customize-windows-server-essentials"></a>Windows Server Essentials 사용자 지정  
 Windows Server Essentials 대시보드의 **홈** 페이지는 서버를 설치한 직후에 완료 해야 하는 **설정** 작업으로 연결 됩니다. 이러한 작업을 수행 하면 서버에 저장 된 정보를 보호 하 고 Windows Server Essentials에서 사용할 수 있는 기능을 사용할 수 있습니다.  
  
 이 작업을 수행하지 않도록 선택하면 사용자는 일부 네트워크 기능에 액세스하지 못할 수 있습니다. 나중에 이러한 작업으로 돌아가려면 Windows Server Essentials 대시보드 **홈** 페이지로 돌아갑니다.  
  
 다음 표는 설정 작업 목록에 나타날 수 있는 항목을 정의합니다.  
  
|작업|설명
|----------|-----------------|  
|다른 Microsoft 제품에 대한 업데이트 가져오기|Microsoft 업데이트를 사용 하 여 Windows Server Essentials 및 기타 Microsoft 제품에 대 한 업데이트를 자동으로 얻도록 지정할 수 있는 도구를 실행 하는 링크에 액세스 하려면이 작업을 클릭 합니다.  
|사용자 계정 추가|사용자 계정 추가에 대한 간략한 정보를 보려면 이 작업을 클릭합니다. **사용자 계정 추가 마법사**를 실행하는 링크가 제공됩니다. 자세한 내용은 [사용자 계정 추가](../manage/Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage1)(영문)를 참조하세요.  
|서버 폴더 추가|서버 폴더 추가에 대한 간략한 정보를 보려면 이 작업을 클릭합니다. **폴더 추가 마법사**를 실행하는 링크가 제공됩니다. 서버 폴더에 대한 온라인 도움말 항목 링크도 제공됩니다. 자세한 내용은 [서버 폴더 추가 또는 이동](../manage/Manage-Server-Folders-in-Windows-Server-Essentials.md#BKMK_5)(영문)을 참조하세요. 
|서버 백업 설정|서버 백업을 사용한 데이터 보호에 대해 간략한 정보를 보려면 이 작업을 클릭합니다. **서버 백업 설정 마법사** 를 실행하는 링크가 제공됩니다. 자세한 내용은 [서버 백업 설정 또는 사용자 지정](../manage/Manage-Server-Backup-in-Windows-Server-Essentials.md#BKMK_1)을 참조하세요. 
|원격 액세스 설정|Windows Server Essentials의 원격 액세스 기능에 대 한 간략 한 정보를 보려면이 작업을 클릭 합니다. **원격 액세스 설정** 페이지 링크가 제공됩니다. 자세한 내용은 [원격 액세스 관리](../manage/Manage-Anywhere-Access-in-Windows-Server-Essentials.md)를 참조 하세요. 
|전자 메일 경고 알림 설정|메일 경고 알림에 대한 간략한 정보를 보려면 이 작업을 클릭합니다. **경고에 대한 전자 메일 알림 설정** 도구를 실행하는 링크가 제공됩니다. 자세한 내용은 [경고에 대한 전자 메일 알림 설정](../manage/Manage-System-Health-in-Windows-Server-Essentials.md#BKMK_Email)(영문)을 참조하세요.  
|미디어 서버 설정|미디어 서버를 사용한 음악, 비디오 및 이미지 파일 공유에 대해 간략한 정보를 보려면 이 작업을 클릭합니다. **미디어 설정** 페이지 링크가 제공됩니다. 미디어 설정에 대한 온라인 도움말 항목 링크도 제공됩니다. 자세한 내용은 [디지털 미디어 관리](../manage/Manage-Digital-Media-in-Windows-Server-Essentials.md)를 참조 하세요. 
|컴퓨터 연결|네트워크 컴퓨터를 서버에 연결하는 방법에 대해 간략한 정보를 보려면 이 작업을 클릭합니다. 자세한 내용은 [서버에 컴퓨터 연결](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_9)을 참조하세요.
  
## <a name="see-also"></a>참고 항목  
  
-   [Windows Server Essentials 설치](Install-Windows-Server-Essentials.md)

