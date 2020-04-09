---
title: Windows Server Essentials에서 온라인 백업 관리
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: 95a9f593-fad7-4335-bd4d-c7bb8c033efb
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 5c7db7f2e39ec0f46f2b4d36537a0db94980c108
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80852776"
---
# <a name="manage-online-backup-in-windows-server-essentials"></a>Windows Server Essentials에서 온라인 백업 관리

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials
  
 Microsoft Azure Backup와 통합 하 고 나면 **온라인 백업** 관리 페이지가 Windows Server Essentials 대시보드에 표시 됩니다. **온라인 백업** 페이지를 사용하여 일반적인 관리 작업을 수행할 수 있습니다. 온라인 백업 페이지의 기능은 다음과 같습니다.  
  
- 다음 하위 섹션 페이지:  
  
  -   **온라인 백업** 온라인 백업용 서버를 등록하고 나면 이 섹션에는 현재 백업 상태, 저장소 상태 및 계정 정보가 표시됩니다.  
  
  -   **보호 된 폴더** 이 섹션에는 서버에 있는 모든 공유 폴더 및 모든 파일 히스토리 폴더와 Azure에서 백업 하도록 선택한 기타 폴더가 나열 됩니다. 목록에는 폴더 이름, 폴더 경로 및 각 공유 폴더 상태가 포함됩니다.  
  
  -   **백업 기록** 이 섹션에는 최근 온라인 백업 목록이 표시됩니다. 목록에는 작업 유형과 각 백업의 시간 및 상태가 포함됩니다.  
  
- 선택한 백업 작업이나 복원 작업에 대한 추가 정보가 있는 세부 정보 창.  
  
- 수행할 수 있는 관리 작업 집합을 포함하는 작업 창.  
  
  가장 중요한 비즈니스 및 사용자 데이터는 백업해야 합니다. 예를 들어 중요한 데이터 파일을 포함하는 서버 폴더를 백업해야 합니다. 중요한 정보를 포함하는 네트워크 컴퓨터에 대한 파일 히스토리도 백업해야 합니다.  
  
  온라인으로 백업할 데이터를 결정할 때 구현하려는 백업 빈도와 보존 정책을 고려하세요. 그런 다음 예산을 검토하고 제공할 수 있는 스토리지 공간 크기를 결정합니다. 스토리지 비용 및 볼륨을 요구 사항과 비교하여 계산하고 중요한 데이터를 최대한 많이 보호할 수 있도록 온라인 백업을 구성합니다. 가격 정보를 보려면 [Azure 백업 가격 정보](https://azure.microsoft.com/pricing/details/backup/)를 참조하세요.  
  
  다음 섹션에서는 Windows Server Essentials 대시보드에 표시될 수 있는 다양한 온라인 백업 작업에 대해 설명합니다.  
  
## <a name="online-backup-tasks-in-the-dashboard"></a>대시보드의 온라인 백업 작업  
  
-   [Azure Backup 자격 증명 모음에 인증서 업로드](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_1)  
  
-   [온라인 백업 구성](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_2)  
  
-   [온라인 백업 시작](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_3)  
  
-   [온라인 백업에서 파일 및 폴더 복원](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_4)  
  
-   [백업용으로이 서버 등록](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_5)  
  
-   [서버 등록 취소](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_6)  
  
###  <a name="upload-a-certificate-to-the-azure-backup-vault"></a><a name="BKMK_1"></a>Azure Backup 자격 증명 모음에 인증서 업로드  
 Windows Server Essentials에서 온라인 백업에 대 한 Azure Backup를 사용 하려면 먼저 백업 자격 증명 모음에 등록할 공용 인증서를 업로드 해야 합니다. 인증서는 Microsoft Online Services 구독 소유자를 대신 하 여 구독과 연결 된 리소스를 관리 하는 Azure Backup 배포 (에이전트)를 인증 하는 데 사용 됩니다.  
  
> [!NOTE]
>  인증서를 업로드하기 전에 [Azure Backup 서비스에 등록](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_16)의 절차를 완료해야 합니다.  
  
##### <a name="to-upload-a-certificate-to-use-with-the-azure-backup-service"></a>Azure Backup 서비스에서 사용할 인증서를 업로드하려면  
  
1. 관리자 계정으로 Windows Server Essentials 대시보드에 로그온합니다.  
  
2. 대시보드 **홈** 페이지에서 **온라인 백업**을 클릭합니다.  
  
3. **온라인 백업** 영역에서 **Azure Backup 자격 증명 모음에 인증서 업로드**를 클릭합니다.  
  
    Azure 관리 포털에서 **Recovery Services** 열립니다. Azure에 아직 로그인 하지 않은 경우 Microsoft 계정를 사용 하 여 로그인 해야 합니다.  
  
4. 온라인 백업에 사용할 백업 자격 증명 모음의 이름을 클릭하여 백업 자격 증명 모음에 대한 **빠른 시작** 페이지를 엽니다.  
  
5. **인증서 관리**를 클릭합니다.  
  
6. **인증서 관리** 대화 상자에 Windows Server Essentials에서 생성된 공용 인증서의 경로를 붙여넣습니다. 공용 인증서의 경로를 가져오려면 다음을 수행합니다.  
  
   1.  Windows Server Essentials 대시보드에서 **온라인 백업** 탭을 클릭합니다.  
  
   2.  **온라인 백업** 페이지에서 생성된 인증서의 경로를 복사합니다.  
  
   3.  Azure 관리 포털로 전환한 다음 **인증서 관리** 대화 상자에 생성 된 공용 인증서를 업로드할 경로를 붙여넣습니다.  
  
   > [!NOTE]
   >  고유한 공용 인증서를 사용할 수도 있습니다. 어떤 인증서가 필요한지 알아보려면 **빠른 시작** 페이지에서 **인증서 인식** 링크를 클릭합니다.  
  
   > [!NOTE]
   >   Azure에는 공개 키가 있는 x.509 v2 인증서가 필요 합니다. 자세한 내용은 [자격 증명 모음 인증서 관리](https://msdn.microsoft.com/library/azure/dn169036.aspx)를 참조하세요.  
  
7. 인증서를 선택하고 나서 **확인**(확인 표시)을 클릭합니다.  
  
8. **빠른 시작** 페이지로 돌아갑니다. **대시보드**, 를 클릭하고 인증서가 성공적으로 업로드되었는지 확인합니다. 인증서가 성공적으로 업로드되고 나서 대시보드에는 인증서 지문과 만료 날짜가 표시됩니다.  
  
   이 절차를 완료하고 나서 다음을 수행합니다.  
  
9. Azure Backup 서비스에 서버를 등록 합니다. 자세한 내용은 [백업을 위해 이 서버 등록](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_5)을 참조하세요.  
  
10. 서버의 온라인 백업을 구성합니다. 자세한 내용은 [온라인 백업 구성](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_2)을 참조하세요.  
  
###  <a name="configure-online-backup"></a><a name="BKMK_2"></a>온라인 백업 구성  
 Azure Backup에 서버를 등록 한 후에는 Windows Server Essentials에서 온라인 백업 설정을 구성할 수 있습니다.  
  
##### <a name="to-configure-online-backup"></a>온라인 백업을 구성하려면  
  
1.  Windows Server Essentials 대시보드의 **온라인 백업** 페이지나 서버 등록 마법사에서 **온라인 백업 구성**을 클릭합니다. 온라인 백업 구성 마법사가 나타납니다.  
  
2.  마법사의 **온라인 백업 구성** 페이지에서 Azure Backup에 백업 하려는 각 서버 폴더의 확인란을 선택 합니다. 백업에 포함하지 않을 각 서버 폴더의 확인란을 선택 취소합니다. 목록에 표시되지 않은 폴더를 추가하려면 **폴더 추가**를 클릭합니다. 선택을 완료하면 **다음**을 클릭합니다.  
  
    > [!NOTE]
    >  로컬 서버에 없는 폴더 또는 ReFS 형식으로 지정된 드라이브에 있는 폴더를 선택할 수 없습니다.  
  
3.  마법사의 **파일 히스토리 백업 추가** 페이지에서 파일 히스토리 기능을 지원하는 네트워크 컴퓨터에 대한 파일 히스토리 백업을 포함하도록 선택할 수 있습니다. 그리고 **다음**을 클릭하여 계속합니다.  
  
4.  마법사의 **백업 일정 지정** 페이지에서 다음을 구성하고 **다음**을 클릭하여 계속합니다.  
  
    -   온라인 백업을 실행할 시간을 선택하거나 수락합니다. 기본 시간은 오후 10시입니다. 두 번째 백업을 실행할 시간을 지정할 수도 있습니다.  
  
    -   온라인 백업을 실행할 요일을 선택하거나 수락합니다. 기본적으로 온라인 백업은 월요일부터 금요일까지 실행됩니다.  
  
5.  마법사의 **백업 보존 정책 지정** 페이지에서 온라인 백업을 유지할 일수를 선택하고 **다음**을 클릭합니다. 기본값은 7일입니다. 온라인 백업을 15일 또는 30일 동안 보관하도록 선택할 수도 있습니다.  
  
    > [!NOTE]
    >   Azure Backup는 항상 가장 최근 백업을 보존 합니다. 백업 대상에 백업을 저장할 수 있는 충분한 공간이 없으면 백업 프로세스가 실패합니다. 이 상황을 방지하려면 추가 스토리지 공간을 구입하거나 데이터 보존 기간을 단축합니다. 가격 책정 정보는 Microsoft Azure Backup에 대 한 [가격 정보](https://azure.microsoft.com/pricing/details/backup/) 를 참조 하세요.  
  
6.  온라인 백업에 할당되는 인터넷 대역폭 양을 제한하려면 마법사의 **대역폭 사용량 선택** 페이지에서 **인터넷 대역폭 사용량 사용**을 선택합니다. 페이지에서 옵션을 선택하여 작업 시간 및 비작업 시간 중에 온라인 백업에서 사용할 수 있는 인터넷 대역폭 양을 지정합니다. 그런 다음 비즈니스 시간과 비즈니스 날짜를 지정합니다.  
  
    > [!NOTE]
    >   Azure Backup를 사용 하 여 통합 소프트웨어에서 정보를 백업 하거나 복원할 때 네트워크 대역폭을 활용 하는 방법을 사용자 지정할 수 있습니다. 일반적으로 제한 이라는 기술을 사용 하 여 특정 날짜 및 시간 간격 동안 백업 및 복원 프로세스에서 사용할 수 있는 네트워크 대역폭의 양을 제어할 수 있습니다. 온라인 백업 구성 마법사에서 **인터넷 대역폭 사용량 사용** 확인란을 선택하고 나서 작업 시간 대역폭 제한을 적용할 작업일과 작업 시간을 지정할 수 있습니다. 비 작업 시간 제한은 그 외 다른 시간에 사용됩니다. 유효한 대역폭 범위는 두 제한에 대해 모두 256Kbps에서 무제한까지입니다.  
  
7.  온라인 백업 구성이 완료되면 **닫기**를 클릭합니다.  
  
    > [!TIP]
    >  백업 구성이 성공적으로 완료되면 **온라인 백업** 페이지에는 가장 최근 온라인 백업의 상태와 백업 자격 증명 모음에서 사용되는 저장소 공간 크기가 표시됩니다. 이전 백업의 상태를 확인하려면 **백업 기록**을 클릭합니다.  
  
###  <a name="start-an-online-backup"></a><a name="BKMK_3"></a>온라인 백업 시작  
  
> [!NOTE]
>  온라인 백업을 시작하려면 먼저 [백업을 위해 이 서버를 등록](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_5)하고 [온라인 백업을 구성](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_2)합니다.  
  
##### <a name="to-start-an-online-backup-immediately"></a>온라인 백업을 즉시 시작하려면  
  
1.  대시보드에 관리자로 로그온합니다.  
  
2.  탐색 모음에서 **온라인 백업**을 클릭합니다.  
  
3.  **온라인 백업 작업** 창에서 **지금 백업 시작**을 클릭합니다.  
  
###  <a name="restore-files-and-folders-from-an-online-backup"></a><a name="BKMK_4"></a>온라인 백업에서 파일 및 폴더 복원  
 파일 및 폴더 복원 마법사가 온라인으로 백업되는 파일 및 폴더를 찾고 선택 및 복원하는 프로세스를 안내합니다. 마법사 내에서 이동하면서 다음 작업을 수행합니다.  
  
1.  **파일 및 폴더를 복원할 온라인 백업 선택**  
  
     파일 및 폴더 복원 마법사를 실행하면 우선 현재 로그온된 서버의 온라인 백업 또는 다른 서버의 백업에서 파일을 복원할지를 지정해야 합니다.  
  
2.  **파일과 폴더를 복원할 서버를 선택 하십시오.**  
  
     다른 서버에서 파일과 폴더를 복원하도록 선택했으면 사용할 수 있는 서버 목록에서 복원할 서버를 선택하고 **다음**을 클릭합니다.  
  
3.  **복원할 파일과 폴더가 포함 된 볼륨 선택**  
  
     온라인 백업에는 백업 소스 서버의 볼륨과 일치하는 볼륨이 포함됩니다. 볼륨을 선택하고 나서 복원할 백업의 날짜와 시간을 선택하고 **다음**을 클릭합니다.  
  
4.  **복원할 파일 및 폴더 선택**  
  
     마법사의 **복원할 항목 선택** 페이지에서 다양한 폴더 위치를 열고 복원할 각 파일이나 폴더의 확인란을 선택할 수 있습니다. 파일 선택을 완료하면 **다음**을 클릭합니다.  
  
5.  **복원 된 파일 및 폴더의 대상 위치 지정**  
  
     마법사의 **복원 옵션 지정** 페이지에서 파일과 폴더를 복원할 위치를 지정할 수 있습니다. 두 가지 옵션 중에서 선택할 수 있습니다.  
  
    -   **원래 위치로 복원합니다**. 백업이 시작된 정확한 위치로 파일과 폴더를 복원하려면 이 옵션을 선택합니다.  
  
    -   **다른 위치로 복원합니다**.  파일을 복원할 서버의 다른 위치를 지정하려면 이 옵션을 선택합니다.  
  
         기본 설치에서 복원 파일과 이름이 같은 파일이 대상 위치에 이미 있으면 마법사가 원본 파일의 복사본을 만듭니다. 또한 ACL(액세스 제어 목록)이 현재 파일 사용 권한을 반영하도록 업데이트됩니다. **고급**을 클릭하여 기본 설정을 사용자 지정할 수 있습니다.  
  
6.  **복원 정보를 확인 합니다.**  
  
     **복원 정보 확인** 페이지에서는 지정한 복원 지침의 요약을 제공합니다. 파일 복원을 계속 진행하려면 온라인 백업 계정의 올바른 암호를 입력해야 합니다.  
  
###  <a name="register-this-server-for-backup"></a><a name="BKMK_5"></a>백업용으로이 서버 등록  
 Windows Server Essentials 서버의 파일, 폴더 및 파일 히스토리를 Azure Backup 백업 하거나 복원 하려면 먼저 Microsoft Azure Backup 서비스에 서버를 등록 해야 합니다.  
  
> [!NOTE]
>  서버를 등록하기 전에 온라인 백업을 저장할 백업 자격 증명 모음에서 사용할 인증서를 업로드해야 합니다. 자세한 내용은 [Azure Backup 자격 증명 모음에 인증서 업로드](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_1)를 참조하세요.  
  
##### <a name="to-register-your-server-with-azure-backup"></a>Azure Backup에 서버를 등록하려면  
  
1.  서버에 관리자로 로그온하고 대시보드를 엽니다.  
  
2.  탐색 모음에서 **온라인 백업**을 클릭합니다.  
  
3.  **온라인 백업** 하위 섹션에서 **등록**을 클릭합니다.  
  
4.  온라인 백업에 대해 백업 자격 증명 모음에서 사용할 인증서를 선택합니다. 기본 인증서는 기본적으로 선택됩니다. 다른 인증서를 선택하려면 **찾아보기**를 사용합니다. 그런 다음 **다음**을 클릭합니다.  
  
5.  마법사의 지침에 따라 암호를 만들고 등록을 완료합니다.  
  
###  <a name="unregister-server"></a><a name="BKMK_6"></a>서버 등록 취소  
  
> [!CAUTION]
>  Microsoft Azure Backup 서비스에서 Windows Server Essentials 서버를 등록 취소 하면 더 이상 서버를 백업할 수 Azure Backup. 또한 이전에 업로드된 서버 데이터가 지워집니다. 온라인 백업을 다시 시작하려면 서버를 다시 등록해야 합니다.  
  
##### <a name="to-unregister-your-server-with-azure-backup"></a>Azure Backup에서 서버를 등록 해제하려면  
  
1.  [Azure 관리 포털](https://manage.windowsazure.com)에 로그인합니다.  
  
2.  **Recovery Services**를 클릭합니다.  
  
3.  **복구 서비스**에서 백업 자격 증명 모음의 이름을 클릭합니다.  
  
4.  자격 증명 모음에 대한 **빠른 시작** 페이지에서 **서버**를 클릭합니다.  
  
5.  서버를 선택하고 **삭제**를 클릭한 다음 확인 프롬프트에서 **예**를 클릭합니다.  
  
## <a name="related-tasks"></a>관련 작업  
  
-   [온라인 백업 정책 변경](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_7)  
  
-   [온라인 백업 저장소 사용 보기](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_8)  
  
-   [온라인 백업에 새 폴더 포함](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_9)  
  
-   [온라인 백업 정책에서 파일 히스토리 백업 제거 또는 제외](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_10)  
  
-   [온라인 서버 백업 사용 안 함 또는 다시 사용](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_11)  
  
-   [온라인 서버 백업 중지 진행 중](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_12)  
  
-   [온라인 백업 상태 보기](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_13)  
  
-   [온라인 백업 경고 보기 및 관리](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_14)  
  
-   [온라인 백업을 기본 설정으로 다시 설정](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_15)  
  
-   [Azure Backup 서비스에 등록](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_16)  
  
-   [Windows Server Essentials와 Azure Backup 통합](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_17)  
  
-   [Windows Server Essentials에서 온라인 백업에 대 한 폴더 보호](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_18)  
  
-   [Windows Server Essentials의 온라인 백업 기록](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_19)  
  
###  <a name="change-the-online-backup-policy"></a><a name="BKMK_7"></a>온라인 백업 정책 변경  
 Windows Server Essentials 대시보드를 사용하여 온라인 백업 정책을 간편하게 변경할 수 있습니다.  
  
##### <a name="to-change-the-online-backup-policy"></a>온라인 백업 정책을 변경하려면  
  
1. 대시보드에 관리자로 로그온합니다.  
  
2. 탐색 모음에서 **온라인 백업**을 클릭합니다.  
  
3. **온라인 백업 작업** 창에서 **온라인 백업 구성**을 클릭합니다.  
  
4. 마법사의 지침에 따라 온라인 백업 정책을 사용자 지정합니다.  
  
   사용자 지정할 수 있는 설정에 대한 자세한 내용은 [온라인 백업 구성](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_2)을 참조하세요.  
  
###  <a name="view-online-backup-storage-usage"></a><a name="BKMK_8"></a>온라인 백업 저장소 사용 보기  
  
##### <a name="to-view-the-amount-of-storage-space-that-online-backup-uses"></a>온라인 백업에 사용되는 스토리지 공간 크기를 보려면  
  
1.  대시보드에 관리자로 로그온합니다.  
  
2.  탐색 모음에서 **온라인 백업**을 클릭합니다.  
  
3.  **온라인 백업** 탭의 정보 창에 **저장소 상태** 가 표시됩니다.  
  
###  <a name="include-a-new-folder-in-online-backup"></a><a name="BKMK_9"></a>온라인 백업에 새 폴더 포함  
  
##### <a name="to-include-a-new-folder-in-the-online-backup-policy"></a>온라인 백업 정책에 새 폴더를 포함하려면  
  
1. 대시보드에 관리자로 로그온합니다.  
  
2. 탐색 모음에서 **온라인 백업**을 클릭합니다.  
  
3. **온라인 백업 작업** 창에서 **온라인 백업 구성**을 클릭합니다.  
  
4. **백업 정책 변경 또는 제거** 페이지에서 **온라인 백업 정책 사용자 지정**을 클릭합니다.  
  
5. **온라인 백업 구성** 페이지에서 포함하려는 폴더가 목록에 표시되지 않으면 **폴더 추가**를 클릭합니다.  
  
6. **폴더 추가** 창에서 온라인 백업에 포함할 폴더로 이동하여 선택하고 **확인**을 클릭합니다.  
  
7. **온라인 백업 구성** 페이지에서 포함할 다른 폴더를 원하는 대로 선택하고 **다음**을 클릭합니다.  
  
8. 마법사의 지침에 따라 온라인 백업 정책 사용자 지정을 완료합니다.  
  
   사용자 지정할 수 있는 기타 설정에 대한 자세한 내용은 [온라인 백업 구성](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_2)을 참조하세요.  
  
###  <a name="remove-or-exclude-file-history-backups-from-the-online-backup-policy"></a><a name="BKMK_10"></a>온라인 백업 정책에서 파일 히스토리 백업 제거 또는 제외  
  
##### <a name="to-remove-or-exclude-a-folder-from-the-online-backup-policy"></a>온라인 백업 정책에서 폴더를 제거 또는 제외하려면  
  
1.  대시보드에 관리자로 로그온합니다.  
  
2.  탐색 모음에서 **온라인 백업**을 클릭합니다.  
  
3.  **보호 된 폴더** 탭을 클릭 합니다. 세부 정보 창에는 폴더 목록이 온라인 백업 상태와 함께 표시 됩니다.  
  
4.  온라인 백업 정책에서 제외하려는 폴더를 선택하고 작업 창에서 **온라인 백업에서 폴더 제거**를 클릭합니다.  
  
###  <a name="disable-or-re-enable-online-server-backup"></a><a name="BKMK_11"></a>온라인 서버 백업 사용 안 함 또는 다시 사용  
 Azure Backup를 사용 하 여 서버 데이터를 백업 또는 복원 하는 방법에 대 한 지침은 [이 서버를 백업용으로 등록](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_5)을 참조 하세요.  
  
 Azure Backup 사용을 중지 하 여 서버 데이터를 백업 하거나 복원 하는 방법에 대 한 지침은 [서버 등록 취소](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_6)를 참조 하세요.  
  
###  <a name="stop-an-online-server-backup-in-progress"></a><a name="BKMK_12"></a>온라인 서버 백업 중지 진행 중  
  
##### <a name="to-stop-an-online-server-backup-in-progress"></a>진행 중인 온라인 서버 백업을 중지하려면  
  
1.  대시보드에 관리자로 로그온합니다.  
  
2.  탐색 모음에서 **온라인 백업**을 클릭합니다.  
  
3.  **온라인 백업 작업** 창에서 **백업 중지**를 클릭합니다.  
  
     백업을 중지하고 나면 **백업 기록** 목록에 백업에 대한 **취소됨** 상태가 표시됩니다.  
  
###  <a name="view-online-backup-status"></a><a name="BKMK_13"></a>온라인 백업 상태 보기  
  
##### <a name="to-view-the-backup-status"></a>백업 상태를 보려면  
  
1.  대시보드에 관리자로 로그온합니다.  
  
2.  탐색 모음에서 **온라인 백업**을 클릭합니다.  
  
3.  **백업 기록** 탭을 클릭 합니다. 목록 뷰에 각 백업 작업의 상태가 표시 됩니다. 백업 작업을 선택하여 해당 작업에 대한 추가 세부 정보를 확인합니다.  
  
###  <a name="view-and-manage-online-backup-alerts"></a><a name="BKMK_14"></a>온라인 백업 경고 보기 및 관리  
 다른 많은 경고와 마찬가지로 Azure Backup에 대 한 경고가 경고 뷰어에 표시 됩니다.  
  
##### <a name="to-view-online-backup-alerts-in-the-alert-viewer"></a>경고 뷰어에서 온라인 백업 경고를 보려면  
  
1. 대시보드를 엽니다.  
  
2. 다음 작업 중 하나를 수행합니다.  
  
     Windows Server Essentials: 탐색 창에서 경고 아이콘을 클릭 합니다 \(중요, 경고 또는 정보\)일 수 있습니다. 경고 뷰어가 열립니다.  
  
     Windows Server Essentials: **홈** 페이지에서 **상태 모니터링** 탭을 클릭 합니다.  
  
3. Azure Backup와 관련 된 문제에 대 한 경고 목록을 검토 합니다.  
  
   경고 뷰어 또는 상태 모니터링 탭을 사용 하 여 경고를 관리 하는 방법에 대 한 자세한 내용은 [시스템 상태 관리](Manage-System-Health-in-Windows-Server-Essentials.md)를 참조 하세요.  
  
###  <a name="reset-online-backup-to-default-settings"></a><a name="BKMK_15"></a>온라인 백업을 기본 설정으로 다시 설정  
 Windows Server Essentials에서는 온라인 백업에 대한 설정을 구성하도록 도와주는 마법사를 제공합니다. 기본 설정을 복원하려면 **온라인 백업 구성** 작업을 실행하고 **온라인 백업 정책 제거** 옵션을 선택합니다. 그런 다음 **온라인 백업 구성** 작업을 다시 실행합니다. 이전에 업로드된 데이터는 변경되지 않습니다.  
  
###  <a name="sign-up-for-azure-backup-service"></a><a name="BKMK_16"></a>Azure Backup 서비스에 등록  
 Microsoft Azure Backup Windows Server Essentials와 통합할 준비를 하려면 Microsoft Online Services 계정을 사용 하 여 Azure 관리 포털에 로그온 한 다음 백업 자격 증명 모음을 만들어 Azure에 온라인 백업을 저장 합니다. 그런 다음 Azure Backup 통합 모듈을 다운로드 하 고 다운로드 한 파일을 사용 하 여 Windows Server Essentials 서버에 Azure Backup 추가 기능을 설치 합니다. Microsoft 계정이 없으면 무료 평가판에 등록할 수 있습니다.  
  
 이 설치를 수행하려면 다음 작업을 완료합니다.  
  
1.  Microsoft Online Services 계정 및 백업 미리 보기에 등록합니다.  
  
2.  백업 자격 증명 모음을 만들어 온라인 백업을 저장합니다.  
  
3.  Azure Backup 에이전트를 다운로드 합니다.  
  
4.  서버에 Azure Backup 추가 기능을 설치 합니다.  
  
####  <a name="sign-up-for-a-microsoft-online-services-account-and-the-backup-preview"></a><a name="BKMK_SignupforaMicrosoftOnlineServiceAccount"></a>Microsoft Online Services 계정 및 백업 미리 보기에 등록  
  
1.  Windows Server Essentials 대시보드에 로그온합니다.  
  
2.  대시보드 **홈** 페이지에서 **추가 기능** 범주를 클릭하고 **Azure Backup과 통합**, **Azure Backup에 등록하려면 클릭**을 차례로 클릭합니다.  
  
3.  Azure **Recovery Services** 페이지의 **백업 (미리 보기)** 섹션에서 세부 정보를 검토 합니다.  
  
4.  Azure 구독이 없는 경우 **무료 평가판**을 클릭 하 고 지침에 따라 azure 구독을 가져옵니다.  
  
     Azure 구독이 이미 있는 경우 웹 페이지의 오른쪽 위 모서리에서 **포털** 을 클릭 하 여 azure 관리 포털로 이동 합니다.  
  
5.  Azure 관리 포털 페이지의 왼쪽 창에 **Recovery Services** 표시 됩니다. 여기에서 Windows Server Essentials의 온라인 백업을 저장 하는 백업 자격 증명 모음을 관리할 수 있습니다.  
  
####  <a name="create-a-backup-vault-to-store-online-backups"></a><a name="BKMK_Createabackupvaulttostoreonlinebackups"></a>온라인 백업을 저장할 백업 자격 증명 모음 만들기  
  
1.  Windows Server Essentials 서버의 웹 브라우저에서 [Azure 관리 포털](https://manage.windowsazure.com)에 로그인합니다.  
  
2.  Azure 관리 포털에서 **새로 만들기**, **Data Services**, **Recovery Services**, **백업 자격 증명 모음**, **빠른 생성**을 차례로 클릭 합니다.  
  
3.  백업 자격 증명 모음의 이름을 입력하고 백업을 저장할 영역을 선택한 다음 **빠른 생성**을 클릭합니다.  
  
     **복구 서비스** 영역이 열리고 새 백업 자격 증명 모음이 표시됩니다.  
  
####  <a name="download-the-azure-backup-agent"></a><a name="BKMK_DownloadtheWindowsAzureBackupAgent"></a>Azure Backup 에이전트 다운로드  
  
1.  Windows Server Essentials 대시보드를 엽니다.  
  
2.  대시보드 **홈** 페이지에서 **시작** 탭, **추가 기능** 범주, **Azure Backup과 통합**, **Azure Backup 통합 모듈을 다운로드하려면 클릭**을 차례로 클릭합니다.  
  
####  <a name="install-the-azure-backup-add-in-on-the-server"></a><a name="BKMK_InstalltheWindowsAzureBackupAddIn"></a>서버에 Azure Backup 추가 기능 설치  
  
1. 관리자 계정으로 서버에 로그인하고 이전 단계에서 다운로드한 **OnlineBackupAddin.wssx** 파일을 실행합니다.  
  
2. **소프트웨어 사용 조건**이 표시됩니다. 조건에 동의하면 **동의**를 클릭하여 설치를 계속합니다.  
  
3. **추가 기능 설치** 페이지에서 **추가 기능 설치**를 클릭합니다.  
  
   > [!NOTE]
   >  필수 구성 요소 소프트웨어를 설치하려면 서버를 시작해야 할 수 있습니다.  
  
    **설치** 페이지가 표시됩니다. 설치가 시작되면 진행률 표시기가 표시되어 설치 진행률을 보여 줍니다. 설치가 완료 되 면 Azure Backup 추가 기능이 성공적으로 설치 되었다는 메시지가 표시 됩니다.  
  
4. **마침**을 클릭합니다.  
  
5. 대시보드를 닫았다가 다시 엽니다.  
  
    새 탭 **온라인 백업**이 대시보드에 추가됩니다. 이 탭에서 서버를 등록 하 고 백업 설정을 구성 하 고 Azure 관리 포털에서 **Recovery Services** 를 열어 서버에 대 한 백업 자격 증명 모음을 관리할 수 있습니다.  
  
   이러한 단계를 완료하고 나서 다음을 수행합니다.  
  
6. Windows Server Essentials에서 온라인 백업에 사용할 인증서를 업로드 합니다. 자세한 내용은 [Azure Backup 자격 증명 모음에 인증서 업로드](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_1)를 참조하세요.  
  
7. Azure Backup 자격 증명 모음에 서버를 등록 합니다. 자세한 내용은 [백업을 위해 이 서버 등록](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_5)을 참조하세요.  
  
8. 서버의 온라인 백업을 구성합니다. 자세한 내용은 [온라인 백업 구성](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_2)을 참조하세요.  
  
###  <a name="integrate-azure-backup-with-windows-server-essentials"></a><a name="BKMK_17"></a>Windows Server Essentials와 Azure Backup 통합  
 Microsoft Azure Backup 통합 모듈은 서버의 파일과 폴더를 암호화 하 고 Microsoft에서 제공 하는 Azure 호스팅 저장소 시스템으로 백업할 수 있는 Windows Server Essentials의 새로운 기능입니다. Azure Backup를 사용 하 여 서버에서 데이터를 암호화 하 고 백업 하면 화재, 홍수, 도난 또는 기타 재해로 인 한 중요 한 비즈니스 데이터의 치명적인 손실을 방지할 수 있습니다. Azure Backup를 사용 하 여 서버 데이터를 백업 하는 경우 정보는 암호를 사용 하 여 암호화 된 후 인터넷의 보안 데이터 센터로 업로드 됩니다. 온라인 백업의 데이터에 액세스하려면 인증서로 인증된 서버가 있어야 하고 암호를 제공해야 합니다.  
  
 서버를 통합 하 고 Azure Backup에 등록 한 후에는 정기적으로 예약 된 백업을 수행 하도록 온라인 백업 설정을 구성할 수 있습니다. 온라인 백업 대시보드에서 **지금 백업 시작** 작업을 클릭하여 언제든지 온라인 백업을 시작할 수도 있습니다.  
  
 온라인 백업 설치에는 다음 단계가 포함됩니다.  
  
1.  [Azure Backup 서비스에 등록](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_16) -backup 서비스에 등록 한 후 백업 자격 증명 모음을 만들고 Azure Backup 통합 모듈을 다운로드 및 설치 합니다.  
  
2.  [Azure Backup 자격 증명 모음에 인증서 업로드](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_1)  
  
3.  [백업용으로이 서버 등록](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_5)  
  
4.  [온라인 백업 구성](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_2)  
  
> [!NOTE]
>   Azure Backup는 암호를 사용 하 여 온라인 백업을 위해 파일과 폴더를 암호화 합니다. 암호화 암호를 변경하면 서버를 등록할 때 지정한 암호가 바뀝니다. 암호에는 ASCII로 코딩된 문자만 사용할 수 있습니다.  
  
###  <a name="protect-folders-for-online-backup-in-windows-server-essentials"></a><a name="BKMK_18"></a>Windows Server Essentials에서 온라인 백업에 대 한 폴더 보호  
 대시보드 온라인 백업 섹션의 **보호된 폴더** 하위 섹션에는 서버에 있는 모든 공유 폴더 목록이 표시됩니다. 다음 표에서는 목록에 포함된 정보를 설명합니다.  
  
|열|설명|  
|------------|-----------------|  
|**폴더 이름:**|온라인 백업에 포함된 폴더 이름입니다.<br /><br /> 폴더를 추가하거나 제외하려면 **온라인 백업 구성** 작업을 실행합니다.|  
|**폴더 경로:**|폴더 위치입니다.|  
|**상태:**|상태 **보호**됨, **보호 되지 않음**및 **알 수 없음**의 세 가지 유형이 있습니다.|  
  
###  <a name="online-backup-history-in-windows-server-essentials"></a><a name="BKMK_19"></a>Windows Server Essentials의 온라인 백업 기록  
 대시보드 온라인 백업 섹션의 **백업 기록** 하위 섹션에는 최근 온라인 백업 목록이 표시됩니다. 성공적인 백업을 사용하여 파일과 폴더를 복원합니다. 다음 표에서는 목록에 포함된 정보를 설명합니다.  
  
|열|설명|  
|------------|-----------------|  
|**연산의**|**백업** 및 **복원**의 두 가지 작업 유형이 있습니다.|  
|**런타임**|가장 최근 상태에 대해 기록된 시간입니다.|  
|**상태:**|**성공**, **진행**중, **취소 됨**, **경고**및 **실패**의 5 가지 상태 유형이 있습니다.|  
  
## <a name="see-also"></a>참고 항목  
  
-   [백업 및 복원 관리](Manage-Backup-and-Restore-in-Windows-Server-Essentials.md)  
  
-   [Microsoft Online Services 관리](Manage-Microsoft-Online-Services-in-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials 관리](Manage-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials 사용](../use/Use-Windows-Server-Essentials.md)
