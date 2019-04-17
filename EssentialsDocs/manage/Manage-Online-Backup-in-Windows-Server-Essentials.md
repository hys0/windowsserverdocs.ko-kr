---
title: "Online Backup-Windows Server Essentials의 관리"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 95a9f593-fad7-4335-bd4d-c7bb8c033efb
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 37d59d500a2de1e2b98c848e7484ae13639d09b7
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="manage-online-backup-in-windows-server-essentials"></a>Online Backup-Windows Server Essentials의 관리

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.
  
 Microsoft Azure Backup 통합는 **Online Backup-** 관리 페이지가 Windows Server Essentials 대시보드에 나타납니다. **Online Backup-** 페이지 일반적인 관리 작업을 수행할 수 있습니다. Online Backup-페이지에서 기능은 다음과 같습니다.  
  
-   다음과 같은 하위 섹션 페이지:  
  
    -   **Online Backup-** 서버 online backup-에 등록 한 후 백업 현재 상태, 저장소 상태 및 계정 정보가이 섹션에 표시 됩니다.  
  
    -   **보호 된 폴더가** 모든 공유 폴더 하 고 서버에 모든 파일 히스토리 폴더 및 Azure에서 백업할 하고자 하는 다른 모든 폴더가이 섹션을 나열 합니다. 목록 폴더 이름, 폴더 경로 및 각 공유 폴더에 대 한 상태를 포함 합니다.  
  
    -   **기록 백업** 이 여기서 최근 온라인 백업 목록이 표시 됩니다. 목록 종류의 작업을 하 고 시간과 각 백업에 대 한 상태를 포함합니다.  
  
-   선택한 백업 작업 또는 복원 작업에 대 한 추가 정보가 포함 된 세부 정보 창 합니다.  
  
-   관리 작업을 수행할 수 있는의 집합을 포함 하는 작업 창 합니다.  
  
 모범 사례로 가장 중요 한 비즈니스 및 사용자 데이터를 백업 해야 합니다. 예를 들어, 데이터 중요 한 파일을 포함 하는 서버 폴더를 백업 해야 합니다. 또한 중요 한 정보가 포함 된 네트워크 컴퓨터에 대 한 파일 히스토리를 백업 해야 합니다.  
  
 온라인를 백업 하는 데이터를 결정할 때 구현 하려는 백업 빈도 및 보유 정책을 것이 좋습니다. 다음에 budget 검토 하 고 수는 저장소 공간의 크기 확인 합니다. 균형 비용과 스토리지 요구 사항에 대 한 볼륨을 맞추고 online backup-중요 한 데이터를 가능한 한 많은 보호 하기 위해 다음 구성 합니다. 가격 정보를 참조 [세부 정보를 백업 Azure에 대 한 가격](https://azure.microsoft.com/pricing/details/backup/)합니다.  
  
 다음 섹션에는 Windows Server Essentials 대시보드 나타날 수 있는 다양 한 온라인 백업 작업에 설명 합니다.  
  
## <a name="online-backup-tasks-in-the-dashboard"></a>대시보드에 온라인 백업 작업  
  
-   [Azure 백업 모음에 인증서를 업로드](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_1)  
  
-   [Online backup-구성](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_2)  
  
-   [온라인 백업을 시작합니다](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_3)  
  
-   [온라인 백업에서 파일 및 폴더를 복원](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_4)  
  
-   [백업에 대 한이 서버 등록](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_5)  
  
-   [서버 등록을 취소합니다](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_6)  
  
###  <a name="BKMK_1"></a>Azure 백업 모음에 인증서를 업로드  
 백업을 사용 하 여 Azure에 대 한 온라인 백업은 Windows Server Essentials의, 전에 모음 백업으로 등록 인증서를 공개 업로드 해야 합니다. 인증서를 인증 구독와 관련 된 리소스를 관리 하려면 Microsoft 온라인 서비스 가입 소유자 대신 활동 Azure 백업 배포 (에이전트) 사용 됩니다.  
  
> [!NOTE]
>  절차를 수행 해야 인증서 업로드 하기 전에 [Azure 백업 서비스에 대 한 등록할](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_16)합니다.  
  
##### <a name="to-upload-a-certificate-to-use-with-the-azure-backup-service"></a>Azure 백업 서비스를 사용 하는 인증서 업로드  
  
1.  Windows Server Essentials 대시보드 관리자 계정으로 로그온 합니다.  
  
2.  대시보드에서 **Home** 페이지, 클릭 **ONLINE BACKUP-**합니다.  
  
3.  에 **ONLINE BACKUP-** 영역 클릭 **업로드 인증서를 Azure 백업 보관소**합니다.  
  
     열립니다 **복구 서비스** Azure 관리 포털에 있습니다. 로그인 한 경우 않았지만 t 이미 azure, Microsoft 계정을 사용 하 여 로그인 해야 합니다.  
  
4.  온라인 백업을 대해 열고를 사용 합니다 백업 모음의 이름을 클릭는 **빠른 시작** 페이지가 백업을 모음에 대 한 합니다.  
  
5.  클릭 **인증서 관리**합니다.  
  
6.  에 **관리 인증서** 공개 인증서의 경로 Windows Server Essentials에서 생성 된 대화 상자의 붙여넣기. 공개 인증서 경로 가져오려면 다음을 수행 합니다.  
  
    1.  Windows Server Essentials 대시보드에서 클릭 하 고 **Online Backup-** 탭 합니다.  
  
    2.  에 **Online Backup-** 페이지에서 생성 된 인증서의 경로 복사 합니다.  
  
    3.  스위치 Azure 관리 포털,으로 이동한 다음에 **관리 인증서** 대화 상자에서 생성 된 공개 인증서 업로드 경로 붙여 합니다.  
  
    > [!NOTE]
    >  공용 인증서를 사용할 수 있습니다. 에 어떤 인증서가 필요한 경우를 알아야는 **빠른 시작** 페이지, 클릭는 **획득 인증서** 링크입니다.  
  
    > [!NOTE]
    >   Azure 공개 키 x.509 v2 인증서가 필요합니다. 자세한 내용은 참조 [관리 보관소 인증서](https://msdn.microsoft.com/library/azure/dn169036.aspx)합니다.  
  
7.  인증서를 선택한 후 클릭 **확인** (확인 표시) 합니다.  
  
8.  돌아갑니다는 **빠른 시작** 페이지 합니다. 클릭 **대시보드**, 인증서 업로드 했습니다 있는지 확인 합니다. 인증서를 업로드 대시보드 인증서 지문 및 만료 날짜가 표시 됩니다.  
  
 이 절차를 완료 한 후 다음을 수행 합니다.  
  
1.  Azure 백업 서비스와 함께 서버를 등록 합니다. 자세한 내용은 참조 [백업이 서버 등록](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_5)합니다.  
  
2.  서버 online backup-구성 합니다. 자세한 내용은 참조 [online backup-구성](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_2)합니다.  
  
###  <a name="BKMK_2"></a>Online backup-구성  
 서버를 Azure 백업으로 등록 한 후 Windows Server Essentials의 온라인 백업 설정을 구성할 수 있습니다.  
  
##### <a name="to-configure-online-backup"></a>Online backup-구성 하려면  
  
1.  또는 서버 등록 마법사에서 중 하나는 **온라인 백업** 페이지 Windows Server Essentials 대시보드의 클릭 **online backup-구성**합니다. 온라인 백업 구성 마법사가 나타납니다.  
  
2.  에 **Online Backup-구성** 마법사의 페이지를 선택 하 고 Azure 백업을 백업 하려는 각 서버 폴더에 대 한 확인란. 백업에 포함 하지 않을 각 서버 폴더에 대 한 확인란의 선택을 취소 합니다. 목록에 표시 되지 않는 폴더를 추가 하려면 클릭 **폴더 추가**합니다. 선택 했으면 클릭 **다음**합니다.  
  
    > [!NOTE]
    >  로컬 서버에 있지 않으면 된 폴더 또는 ReFS 하이퍼링크로 서식이 드라이브에 있는 폴더를 선택할 수 없습니다.  
  
3.  에 **파일 히스토리 백업을 추가** 페이지 마법사의 파일 히스토리 기능을 지 원하는 네트워크 컴퓨터에 대 한 파일 히스토리를 백업을 포함 하도록 선택할 수 있습니다. 클릭 한 다음 **다음** 을 계속 합니다.  
  
4.  에 **백업 일정 지정** 페이지 마법사 다음 구성 하 고 클릭 한 다음 **다음** 계속 하려면:  
  
    -   선택 하거나 실행 하는 online backup-시간 있습니다. 기본 시간이 오후 10 시입니다. 두 번째 백업을 실행할 시간을 지정할 수도 있습니다.  
  
    -   선택 하거나 실행 하는 online backup-일 합니다. 기본적으로 online backup-월요일부터 금요일에서 실행 됩니다.  
  
5.  에 **백업 보존 정책 지정** 페이지 선택 온라인 백업의을 클릭 한 다음 원하는 일 수 마법사의 **다음**합니다. 기본값은 7 일 합니다. 또한 온라인 백업을 15 또는 30 일 동안 보관 수 있습니다.  
  
    > [!NOTE]
    >   항상 백업 azure 최근 백업을 그대로 유지 됩니다. 백업 목적지에 백업을 저장할 수 있는 충분 한 공간이 없는 경우 백업 프로세스 실패 합니다. 이런이 경우를 방지 하려면 추가 저장소 공간을 구입 하거나에서 데이터 보존 시간을 줄일 합니다. 가격 정보를 참조 [세부 정보 가격](https://azure.microsoft.com/pricing/details/backup/) Microsoft Azure Backup에 대 한 합니다.  
  
6.  에 **대역폭 사용량이 선택** online backup-선택에 할당 인터넷 대역폭의 양을 제한 하려면 마법사 페이지 **사용 인터넷 대역폭 사용량이**합니다. 페이지에서 옵션을 사용 하 여 작업 하는 동안 시간과 시간 동안 사용 하 여 online backup-수 있도록 인터넷 대역폭의 양을 지정할 수 있습니다. 업무 시간 및 비즈니스용 일 정하십시오.  
  
    > [!NOTE]
    >   Azure 백업 통합 소프트웨어를 백업 정보를 복원 하거나 때 네트워크 대역폭을 이용 하는 방식을 사용자 지정할 수 있습니다. 일반적으로 제한 이라고 기술을 사용 백업에서 사용할 수 있는 네트워크 대역폭의 양을 제어할 하 고 프로세스 중 특정 날짜 및 시간 간격으로 복원할 수 있습니다. 선택한 후는 **사용 인터넷 대역폭 사용량이** 확인란 Online Backup-구성 마법사에서 근무 한 작업 시간 대역폭 제한이 적용 하는 동안 작업 시간 지정할 수 있습니다. 업무 외 시간 제한 0x80070643 전혀 사용 됩니다. 유효한 대역폭 범위 256 높일에서 모두 제한에 대 한 Unlimited입니다.  
  
7.  온라인 백업 구성을 완료 되 면 클릭 **닫기**합니다.  
  
    > [!TIP]
    >  백업 구성을 완료 한 후는 **온라인 백업** 페이지에서 최근 online backup-및 백업 모음에서 사용 하는 저장소 공간의 크기의 상태를 표시 합니다. 이전 백업의 상태를 확인 하려면 클릭 **백업 기록**합니다.  
  
###  <a name="BKMK_3"></a>온라인 백업을 시작합니다  
  
> [!NOTE]
>  먼저 온라인 백업을, 시작 하기 전에 [이 서버 백업에 등록](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_5), 다음 [구성 online backup-](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_2)합니다.  
  
##### <a name="to-start-an-online-backup-immediately"></a>Online backup-는 바로 시작 하려면  
  
1.  대시보드 관리자 권한으로 로그온 합니다.  
  
2.  탐색 모음에서 클릭 **ONLINE BACKUP-**합니다.  
  
3.  에 **온라인 백업 작업** 창 클릭 **지금 백업 시작**합니다.  
  
###  <a name="BKMK_4"></a>온라인 백업에서 파일 및 폴더를 복원  
 복원할 파일 및 폴더 마법사 찾고을 선택 하 고 온라인 백업 되는 파일 및 폴더를 복원 하는 과정 안내 합니다. 마법사를 통해 발전 처럼 다음과 같은 작업을 수행 합니다.  
  
1.  **파일 및 폴더를 복원 하는 온라인 백업 선택**  
  
     복원할 파일 및 폴더 마법사를 실행할 때 가장 먼저 작업을 수행 해야 하는 온라인 백업을 현재에 로그인 한 서버 또는 다른 서버 백업에서 파일을 복원 하려면 지정입니다.  
  
2.  **서버에서 파일 및 폴더를 복원 하는 데 선택**  
  
     다른 서버에서 파일 및 폴더를 복원 하도록 선택 하면 선택 서버를 사용할 수 있는 서버의 목록에서 복원 클릭 한 다음 원하는 **다음**합니다.  
  
3.  **파일 및 폴더를 복원 포함 된 볼륨 선택**  
  
     온라인 백업을 백업 원본 서버의 볼륨에 해당 하는 볼륨을 포함 합니다. 볼륨을 선택한 후 날짜 및 시간 백업에서 복원을 클릭 한 다음 선택 **다음**합니다.  
  
4.  **파일 및 폴더를 복원 하려면 선택**  
  
     에 **복원 항목 선택** 페이지 마법사의 수 있는 다양 한 폴더 위치를 열고 각 파일 또는 폴더를 복원 하려면에 대 한 확인란을 선택 합니다. 파일 선택 했으면 클릭 **다음**합니다.  
  
5.  **복원 된 파일 및 폴더의 위치를 지정**  
  
     **복원 옵션을 지정** 페이지 마법사의 파일과 폴더를 복원 하는 위치를 지정할 수 있습니다. 두 가지 옵션이 있습니다.  
  
    -   **원래 위치로 복원**합니다. 파일 및 폴더는에서 백업을 수행한 정확한 위치를 복원 하려면이 옵션을 선택 합니다.  
  
    -   **다른 위치에 복원**합니다.  서버에서 파일을 복원 하는 다른 위치를 지정 하려면이 옵션을 선택 합니다.  
  
         마법사 대상 위치에 파일이 복원 파일로 동일한 이름의 이미의 기본 설치 원래 파일의 복사본을 만듭니다. 또한 현재 파일 권한 반영 하기 위해 액세스 제어 목록 (ACL) 업데이트 됩니다. 클릭 하면 **고급** 기본 설정을 사용자 지정 합니다.  
  
6.  **복원 정보 확인**  
  
     **복원 정보 확인** 페이지에 지정 된 복원 지시에 대 한 요약 제공 합니다. 파일 복원 진행할 수 있도록 백업 온라인 계정에 대해 올바른 암호를 입력 해야 합니다.  
  
###  <a name="BKMK_5"></a>백업에 대 한이 서버 등록  
 백업 또는 파일, 폴더 및 Windows Server Essentials 서버에서 파일 히스토리 Azure 백업을 복원 하려면 먼저 Microsoft Azure Backup 서비스와 함께 서버를 등록 해야 합니다.  
  
> [!NOTE]
>  서버를 등록 하기 전에 온라인 백업이 저장 된 자격 증명 백업 모음을 사용 하는 인증서를 업로드 해야 합니다. 자세한 내용은 참조 [인증서 Azure 백업 모음에 업로드](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_1)합니다.  
  
##### <a name="to-register-your-server-with-azure-backup"></a>서버 Azure 백업으로 등록 하려면  
  
1.  관리자 권한으로 서버에에 로그인 하 고 대시보드 엽니다.  
  
2.  탐색 모음에서 클릭 **ONLINE BACKUP-**합니다.  
  
3.  에 **Online Backup-** 하위, 클릭 **등록**합니다.  
  
4.  백업 모음 온라인 백업에 사용 하려는 인증서를 선택 합니다. 기본적으로 기본 인증서가 선택 사용 하 여 다른 인증서를 선택 하려고 할 경우 **찾아보기**합니다. 클릭 한 다음 **다음**합니다.  
  
5.  암호를 만들고 등록을 완료 하 고 마법사의 지침을 따릅니다.  
  
###  <a name="BKMK_6"></a>서버 등록을 취소합니다  
  
> [!CAUTION]
>  Microsoft Azure Backup 서비스에서 Windows Server Essentials 서버 등록을 취소할 경우 Azure 백업 서버를 더 이상 백업할 수 없습니다. 또한 이전에 업로드 된 서버 데이터가 지워집니다. 온라인 백업을, 다시 시작 하려면 다시 서버를 등록 해야 합니다.  
  
##### <a name="to-unregister-your-server-with-azure-backup"></a>서버 Azure 백업으로 등록을 취소 하려면  
  
1.  에 로그인 하 여 [Azure 관리 포털](https://manage.windowsazure.com)합니다.  
  
2.  클릭 **복구 서비스**합니다.  
  
3.  **복구 서비스**, 백업 모음의 이름을 클릭 합니다.  
  
4.  **빠른 시작** 모음에 대 한 페이지, 클릭 **서버**합니다.  
  
5.  서버를 클릭 **삭제**을 차례로 클릭 하 고 **예** 명령 프롬프트에 있습니다.  
  
## <a name="related-tasks"></a>관련된 작업  
  
-   [변경 백업 온라인 정책](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_7)  
  
-   [보기 백업 온라인 저장소 사용](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_8)  
  
-   [Online backup-에 새 폴더를 포함 합니다.](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_9)  
  
-   [온라인 정책 백업에서 파일 히스토리를 백업 제외를 제거 하거나](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_10)  
  
-   [또는 온라인 서버 백업 다시 사용 안 함](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_11)  
  
-   [진행 중인 온라인 서버 백업 중지](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_12)  
  
-   [온라인 백업 상태 보기](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_13)  
  
-   [보기 및 관리 온라인 백업 알림](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_14)  
  
-   [기본 설정으로 online backup-초기화](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_15)  
  
-   [Azure 백업 서비스에 가입](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_16)  
  
-   [Windows Server Essentials Azure 백업을 통합합니다](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_17)  
  
-   [폴더 online backup-Windows Server Essentials의에 대 한 보호](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_18)  
  
-   [Windows Server Essentials의 온라인 백업 기록](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_19)  
  
###  <a name="BKMK_7"></a>변경 백업 온라인 정책  
 Windows Server Essentials 대시보드 사용 하 여 백업 온라인 정책을 변경 하려면 쉽습니다.  
  
##### <a name="to-change-the-online-backup-policy"></a>온라인 정책 백업를 변경 하려면  
  
1.  대시보드 관리자 권한으로 로그온 합니다.  
  
2.  탐색 모음에서 클릭 **Online Backup-**합니다.  
  
3.  에 **온라인 백업 작업** 창 클릭 **online backup-구성**합니다.  
  
4.  온라인 정책 백업 사용자 지정 하 고 마법사의 지침을 따릅니다.  
  
 자세한 내용은 사용자 지정할 수 있는 설정에 대 한 참고 [online backup-구성](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_2)합니다.  
  
###  <a name="BKMK_8"></a>보기 백업 온라인 저장소 사용  
  
##### <a name="to-view-the-amount-of-storage-space-that-online-backup-uses"></a>Online Backup-사용 하는 저장소 공간의 크기를 보려면  
  
1.  대시보드 관리자 권한으로 로그온 합니다.  
  
2.  탐색 모음에서 클릭 **ONLINE BACKUP-**합니다.  
  
3.  에 **Online Backup-** 탭에서 **저장소 상태** 정보 창에 표시 합니다.  
  
###  <a name="BKMK_9"></a>Online backup-에 새 폴더를 포함 합니다.  
  
##### <a name="to-include-a-new-folder-in-the-online-backup-policy"></a>새 폴더를 백업 온라인 정책에 포함  
  
1.  대시보드 관리자 권한으로 로그온 합니다.  
  
2.  탐색 모음에서 클릭 **Online Backup-**합니다.  
  
3.  에 **온라인 백업 작업** 창 클릭 **online backup-구성**합니다.  
  
4.  에 **변경 하거나 주식 백업 정책 제거할** 페이지, 클릭 **온라인 백업 정책을 사용자 지정**합니다.  
  
5.  에 **Online Backup-구성** 페이지에서 해당 폴더 포함 하도록 하려는 경우 목록에 나타나지 않으면를 클릭 **폴더 추가**합니다.  
  
6.  에 **폴더 추가** 창을를 찾아 online backup-에 포함할를 클릭 한 다음 원하는 폴더 선택 **확인**합니다.  
  
7.  에 **Online Backup-구성** 페이지에서 다른 폴더 포함 원하는 대로 클릭 한 다음 선택 **다음**합니다.  
  
8.  백업 온라인 정책 마치게 하 고 마법사의 지침을 따릅니다.  
  
 자세한 내용은 사용자 지정할 수 있는 다른 설정에 대 한 참고 [online backup-구성](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_2)합니다.  
  
###  <a name="BKMK_10"></a>온라인 정책 백업에서 파일 히스토리를 백업 제외를 제거 하거나  
  
##### <a name="to-remove-or-exclude-a-folder-from-the-online-backup-policy"></a>제거 하거나 폴더를 백업 온라인 정책에서 제외 하려면  
  
1.  대시보드 관리자 권한으로 로그온 합니다.  
  
2.  탐색 모음에서 클릭 **Online Backup-**합니다.  
  
3.  클릭 하 고 **보호 폴더** 탭 합니다. 세부 정보 창 백업 온라인 상태 있는 폴더를 목록이 표시 됩니다.  
  
4.  온라인 백업 정책에서 제외 하 고 작업 창의 클릭 한 다음 원하는 폴더 선택 **online backup-에서 폴더를 제거**합니다.  
  
###  <a name="BKMK_11"></a>또는 온라인 서버 백업 다시 사용 안 함  
 백업 서버 데이터를 복원 하거나 Azure 백업을 사용 하는 방법에 대 한 지침을 참조 하세요. [백업이 서버 등록](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_5)합니다.  
  
 Azure 백업을 사용 하 여 백업 서버 데이터를 복원 하거나 중지 하는 방법에 대 한 지침을 참조 하세요. [등록을 취소 서버](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_6)합니다.  
  
###  <a name="BKMK_12"></a>진행 중인 온라인 서버 백업 중지  
  
##### <a name="to-stop-an-online-server-backup-in-progress"></a>진행 중인 온라인 서버 백업의 중지 하려면  
  
1.  대시보드 관리자 권한으로 로그온 합니다.  
  
2.  탐색 모음에서 클릭 **ONLINE BACKUP-**합니다.  
  
3.  에 **온라인 백업 작업** 창 클릭 **백업 중지**합니다.  
  
     백업의 상태 중지 한 후 **취소 됨** 에 백업에 표시 되는 **백업 기록** 목록입니다.  
  
###  <a name="BKMK_13"></a>온라인 백업 상태 보기  
  
##### <a name="to-view-the-backup-status"></a>백업 상태를 확인 하려면  
  
1.  대시보드 관리자 권한으로 로그온 합니다.  
  
2.  탐색 모음에서 클릭 **ONLINE BACKUP-**합니다.  
  
3.  클릭 하 고 **백업 기록** 탭 합니다. 목록 보기 각 백업 작업에 대 한 상태를 표시합니다. 해당 작업에 대 한 추가 세부 정보를 보려면 백업 작업을 선택 합니다.  
  
###  <a name="BKMK_14"></a>보기 및 관리 온라인 백업 알림  
 다른 여러 경고 같은 Azure 백업에 대 한 알림도 Alert 뷰어에 표시 됩니다.  
  
##### <a name="to-view-online-backup-alerts-in-the-alert-viewer"></a>알림 뷰어에서 온라인 백업 알림을 보려면  
  
1.  대시보드를 엽니다.  
  
2.  다음 중 하나를 수행 합니다.  
  
      Windows Server Essentials: 탐색 창에서 알림 아이콘을 클릭 \ (중요, 경고 또는 Informational\ 수 있음). 알림 뷰어를 엽니다.  
  
      Windows Server Essentials:에 **Home** 페이지, 클릭는 **상태를 모니터링** 탭 합니다.  
  
3.  Azure 백업으로 관련 된 문제에 대 한 알림도 목록을 검토 합니다.  
  
 알림을 관리 하려면 Alert 뷰어 또는 상태를 모니터링 탭 사용에 대 한 자세한 내용은 참조 [시스템 의료 관리](Manage-System-Health-in-Windows-Server-Essentials.md)합니다.  
  
###  <a name="BKMK_15"></a>기본 설정으로 online backup-초기화  
 Windows Server Essentials online backup-에 대 한 설정을 구성 하는 데 도움이 되는 마법사를 제공 합니다. 기본 설정으로 복원 하려는 경우 실행는 **online backup-구성** 의 작업을 하 고 선택는 **온라인 백업 정책을 제거** 옵션입니다. 실행 하는 **online backup-구성** 다시 작업입니다. 이전에 업로드 데이터 그대로 유지 됩니다.  
  
###  <a name="BKMK_16"></a>Azure 백업 서비스에 가입  
 Windows Server Essentials와 Microsoft Azure Backup 통합를 준비 하 Microsoft Online Services 계정과 Azure 관리 포털을에 로그인 하 고 온라인 백업을 Azure에서 저장 하도록 백업 저장소 만듭니다 됩니다. 다음 백업 통합 Azure 모듈 다운로드 및 설치 하 여 Azure 백업 Add-In Windows Server Essentials 서버에 다운로드 한 파일을 사용 하 여 됩니다. Microsoft 계정이 없는 경우 무료 평가판에 등록할 수 있습니다.  
  
 이 설정을 수행 하려면 다음 작업을 수행 합니다.  
  
1.  Microsoft Online Services 계정과 백업 미리 보기 로그인 합니다.  
  
2.  온라인 백업을 저장할 백업 저장소를 만듭니다.  
  
3.  Azure 백업 에이전트를 다운로드 합니다.  
  
4.  서버에는 Azure 백업에서 Add-In 설치 합니다.  
  
####  <a name="BKMK_SignupforaMicrosoftOnlineServiceAccount"></a>Microsoft Online Services 계정과 백업 미리 보기에 등록  
  
1.  Windows Server Essentials 대시보드 로그온 합니다.  
  
2.  대시보드에서 **홈** 페이지, 클릭는 **추가 기능** 범주를 확 징 클릭 **Azure 백업으로 통합**을 차례로 클릭 하 고 **Azure 백업 등록할 클릭**합니다.  
  
3.  Azure에서 **복구 서비스** 페이지에 **(미리 보기) 백업** 섹션에서 세부 정보를 확인 합니다.  
  
4.  Azure 구독이 없는 경우 클릭 **무료 평가판**, Azure 구독을 지침을 따릅니다.  
  
     이미 Azure 구독 클릭 **포털** Azure 관리 포털으로 이동 하 여 웹 페이지의 오른쪽 위 모서리에서 합니다.  
  
5.  Azure 관리 포털 페이지에서 확인할 수 있습니다 **복구 서비스** 왼쪽된 창에서 합니다. 사용자 자 백업의 관리 s 해당 스토어 온라인 백업을 Windows Server Essentials의 보관소 합니다.  
  
####  <a name="BKMK_Createabackupvaulttostoreonlinebackups"></a>온라인 백업을 저장할 백업 저장소 만들기  
  
1.  에 로그인 하 여 [Azure 관리 포털](https://manage.windowsazure.com)Windows Server Essentials 서버의 웹 브라우저에서 합니다.  
  
2.  Azure 관리 포털, 클릭 **새로**, 클릭 **데이터 서비스**, 클릭 **복구 서비스**, 클릭 **백업 보관소**을 차례로 클릭 하 고 **빨리 만들기**합니다.  
  
3.  백업 저장실 이름을 입력, 백업에 저장을 클릭 한 다음 원하는 지역을 선택 **빨리 만들기**합니다.  
  
     **복구 서비스** 함께 표시 하 여 새 백업 보관소 영역을 엽니다.  
  
####  <a name="BKMK_DownloadtheWindowsAzureBackupAgent"></a>Azure 백업 에이전트 다운로드  
  
1.  Windows Server Essentials 대시보드를 엽니다.  
  
2.  대시보드에서 **홈** 페이지, 클릭는 **시작** 탭을 클릭는 **추가 기능** 범주를 확 징 클릭 **Azure 백업으로 통합**를 차례로 클릭 하 고 **Azure 백업 통합 모듈 다운로드 하려면 클릭**합니다.  
  
####  <a name="BKMK_InstalltheWindowsAzureBackupAddIn"></a>서버에는 Azure 백업에서 Add-In 설치  
  
1.  관리자 계정을 사용 하 여 서버에 로그인 한 다음 실행는 **OnlineBackupAddin.wssx** 이전 단계에서 다운로드 한 파일.  
  
2.  **소프트웨어 사용 조건** 표시 됩니다. 이용 약관에 동의 하면 클릭 **수락** 설치를 계속 합니다.  
  
3.  에 **에서 추가 기능 설치** 페이지, 클릭 **에서 추가 기능 설치**합니다.  
  
    > [!NOTE]
    >  서버 필수 소프트웨어를 설치 하려면 다시 시작 해야 합니다.  
  
     **설치** 페이지가 표시 됩니다. 진행률 표시기 설치가 시작 되 고 진행률이 설치 시 표시 됩니다. 설치가 완료 되 면 하 여 Azure 백업에서 Add-in 성공적으로 설치 하는 메시지를 받게 됩니다.  
  
4.  클릭 **완료**합니다.  
  
5.  대시보드 닫았다가 다시 합니다.  
  
     새 탭을 **Online Backup-**, 대시보드에 추가 됩니다. 이 탭에서 서버에 등록할 백업 설정을 구성 하 고 열 수 **복구 서비스** 서버에 대 한 백업 저장소 관리를 Azure 관리 포털에 있습니다.  
  
 다음이 단계를 완료 한 후 다음을 수행 합니다.  
  
1.  Windows Server Essentials 온라인 백업에 사용 하는 인증서를 업로드 합니다. 자세한 내용은 참조 [인증서 Azure 백업 모음에 업로드](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_1)합니다.  
  
2.  Azure 백업 모음 서버를 등록 합니다. 자세한 내용은 참조 [백업이 서버 등록](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_5)합니다.  
  
3.  서버 online backup-구성 합니다. 자세한 내용은 참조 [online backup-구성](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_2)합니다.  
  
###  <a name="BKMK_17"></a>Windows Server Essentials Azure 백업을 통합합니다  
 Microsoft Azure Backup 통합 모듈 하면 암호화 하 고 Microsoft에서 제공 하는 Azure 호스트 저장 시스템을 서버에서 파일 및 폴더를 백업 하는 Windows Server Essentials의 새로운 기능입니다. Azure 백업 암호화 하 고 서버에 데이터를 백업를 사용 하 여 불, 초과와 도난당 또는 기타 장애 중요 한 비즈니스 데이터 심각한 손실 되지 않도록 할 수 있습니다. Azure 백업을 사용 하 여 서버에 데이터를 백업 하는 정보 인터넷 보안 데이터 센터에 업로드 되기 전에 하면 암호를 사용 하 여 암호화 됩니다. 온라인에서 데이터에 액세스할 수 백업, 인증서를 인증 된 서버 있고 있어야는 암호를 제공 해야 합니다.  
  
 통합 하 고 서버 Azure 백업으로 등록을 정기적으로 예약 된 백업이 수행 하려면 온라인 백업 설정을 구성할 수 있습니다. 클릭 하 여 언제 든 지 온라인 백업 시작할 수도 있습니다는 **지금 백업 시작** 백업 대시보드에 온라인 작업입니다.  
  
 온라인 백업 설정 이러한 단계를 따릅니다.  
  
1.  [Azure 백업 서비스에 대 한 등록할](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_16) 로그인 한 후-백업 서비스 백업 저장소, 다운로드 만들고 Azure 백업 통합 모듈 설치 합니다.  
  
2.  [Azure 백업 모음에 인증서를 업로드](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_1)  
  
3.  [백업에 대 한이 서버 등록](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_5)  
  
4.  [Online backup-구성](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_2)  
  
> [!NOTE]
>   Azure 백업 파일 및 폴더는 online backup-에 대 한 암호화 하는 암호를 사용 합니다. 암호화 암호 변경 서버에 등록할 때 지정 된 암호를 대체 합니다. 암호가는 ASCII 코딩 문자만 수락 하도록 합니다.  
  
###  <a name="BKMK_18"></a>폴더 online backup-Windows Server Essentials의에 대 한 보호  
 **보호 폴더** 대시보드의 Online Backup-섹션의 하위 섹션 서버에 모든 공유 폴더 목록이 표시 됩니다. 다음 표에서 목록에 포함 된 정보에 설명 합니다.  
  
|열|설명|  
|------------|-----------------|  
|**폴더 이름:**|온라인 백업에 포함 된 폴더의 이름입니다.<br /><br /> 추가 하거나 폴더 제외를 실행 하는 **online backup-구성** 작업입니다.|  
|**폴더 경로 다음과 같습니다.**|폴더의 위치입니다.|  
|**상태:**|세 가지 유형이 상태 **보호**, **보호 되지 않는**, 및 **알 수 없는**합니다.|  
  
###  <a name="BKMK_19"></a>Windows Server Essentials의 온라인 백업 기록  
 **백업 기록** 대시보드의 Online Backup-섹션의 하위 섹션 최근 온라인 백업 목록이 표시 됩니다. 파일 및 폴더를 복원 하려면 백업이 실패를 사용할 수 있습니다. 다음 표에서 목록에 포함 된 정보에 설명 합니다.  
  
|열|설명|  
|------------|-----------------|  
|**작업:**|두 가지 유형의 작업-가지 **백업** 및 **복원**합니다.|  
|**시간:**|최신 상태에 대 한 로그인 한 시간입니다.|  
|**상태:**|상태 5 가지 유형이 **성공**, **진행에서**, **취소**, **경고**, 및 **실패**합니다.|  
  
## <a name="see-also"></a>참조 하십시오  
  
-   [관리 백업 및 복원](Manage-Backup-and-Restore-in-Windows-Server-Essentials.md)  
  
-   [Microsoft Online Services 관리](Manage-Microsoft-Online-Services-in-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials 관리](Manage-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials을 사용 하 여](../use/Use-Windows-Server-Essentials.md)
