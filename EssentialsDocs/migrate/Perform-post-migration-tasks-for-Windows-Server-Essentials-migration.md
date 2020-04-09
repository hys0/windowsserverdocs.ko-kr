---
title: Windows Server Essentials migration1에 대 한 마이그레이션 후 작업 수행
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: f2d236a4-0d62-4961-9d1f-332054e06f6d
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: b5093772e22fc95a19e800db5c83dec261e7b63a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80852428"
---
# <a name="perform-post-migration-tasks-for-windows-server-essentials-migration1"></a>Windows Server Essentials migration1에 대 한 마이그레이션 후 작업 수행

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

다음 작업을 통해 원본 서버에 있던 일부 동일한 설정을 사용하여 대상 서버 설정을 완료할 수 있습니다. 마이그레이션 프로세스 중에 원본 서버에서 이러한 설정의 일부를 사용하지 않도록 설정했을 수 있으므로 대상 서버에 마이그레이션되지 않았습니다. 또는 선택적 구성 단계를 수행할 수 있습니다.  
  

-   [원본 서버의 DNS 항목 삭제](Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md#BKMK_DeleteDNSEntries)  
  
-   [Lob (기간 업무) 및 기타 응용 프로그램 데이터 폴더 공유](Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md#BKMK_ShareLineOfBusinessAndOtherApplications)  
  
-   [마이그레이션 후 클라이언트 컴퓨터 문제 해결](Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md#BKMK_FixClientComputerIssuesAfterMigrating)  
  
-   [기본 제공 Administrators 그룹에 일괄 작업으로 로그온 할 수 있는 권한을 부여 합니다.](Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md#BKMK_AdminGroup)  

-   [원본 서버의 DNS 항목 삭제](../migrate/Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md#BKMK_DeleteDNSEntries)  
  
-   [Lob (기간 업무) 및 기타 응용 프로그램 데이터 폴더 공유](../migrate/Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md#BKMK_ShareLineOfBusinessAndOtherApplications)  
  
-   [마이그레이션 후 클라이언트 컴퓨터 문제 해결](../migrate/Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md#BKMK_FixClientComputerIssuesAfterMigrating)  
  
-   [기본 제공 Administrators 그룹에 일괄 작업으로 로그온 할 수 있는 권한을 부여 합니다.](../migrate/Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md#BKMK_AdminGroup)  

  
##  <a name="delete-dns-entries-of-the-source-server"></a><a name="BKMK_DeleteDNSEntries"></a>원본 서버의 DNS 항목 삭제  
 원본 서버 서비스를 해제하고 나서 DNS(도메인 이름 서비스) 서버에는 원본 서버를 가리키는 항목이 포함되어 있을 수 있습니다. 이러한 DNS 항목을 삭제합니다.  
  
#### <a name="to-delete-dns-entries-that-point-to-the-source-server"></a>원본 서버를 가리키는 DNS 항목을 삭제하려면  
  
1.  대상 서버에서 **DNS 관리자**를 엽니다.  
  
2.  DNS 관리자에서 서버 이름을 마우스 오른쪽 단추로 클릭하고 **속성**, **전달자** 탭을 차례로 클릭합니다.  
  
3.  원본 서버를 가리키는 전달자 목록에서 항목이 있는지 확인합니다. 항목이 있으면 **편집**을 클릭하고 **전달자 편집** 창에서 해당 항목을 삭제합니다.  
  
4.  **DNS 관리자**에서 서버 이름을 확장하고 **정방향 조회 영역**을 확장합니다.  
  
5.  각 정방향 조회 영역에 대한 영역을 마우스 오른쪽 단추로 클릭하고 **속성**, **이름 서버** 탭을 차례로 클릭합니다.  
  
6.  원본 서버를 가리키는 **이름 서버** 상자의 항목을 클릭하고 **제거**, **확인**을 차례로 클릭합니다.  
  
7.  원본 서버에 대한 모든 포인터가 제거될 때까지 5 - 6단계를 반복합니다.  
  
8.  **확인**을 클릭하여 **속성** 창을 닫습니다.  
  
9. **DNS 관리자** 콘솔에서 **역방향 조회 영역**을 확장합니다.  
  
10. 6~9단계를 반복하여 원본 서버를 가리키는 모든 역방향 조회 영역을 제거합니다.  
  
##  <a name="share-line-of-business-and-other-application-data-folders"></a><a name="BKMK_ShareLineOfBusinessAndOtherApplications"></a>Lob (기간 업무) 및 기타 응용 프로그램 데이터 폴더 공유  
 대상 서버로 복사한 LOB(기간 업무) 및 기타 애플리케이션 데이터 폴더에 대해 공유 폴더 사용 권한 및 NTFS 사용 권한을 설정해야 합니다. 사용 권한을 설정 하면 공유 폴더가 Windows Server Essentials 대시보드의 **저장소** 섹션에 표시 됩니다.  
  
 로그온 스크립트를 사용하여 공유 폴더에 드라이브를 매핑하는 경우 스크립트를 업데이트하여 대상 서버의 드라이브에 매핑해야 합니다.  
  
##  <a name="fix-client-computer-issues-after-migrating"></a><a name="BKMK_FixClientComputerIssuesAfterMigrating"></a>마이그레이션 후 클라이언트 컴퓨터 문제 해결  
 Microsoft ISA (Internet Security and 가속화) 서버가 설치 된 Windows Small Business Server 2003 Premium Edition에서 Windows Server Essentials로 마이그레이션하는 경우 네트워크의 클라이언트 컴퓨터에도 Microsoft 방화벽 클라이언트 및 인터넷이 있습니다. 프록시 서버를 사용 하도록 구성 된 탐색기입니다.  
  
 프록시 서버가 더 이상 없으므로 이 때문에 클라이언트 컴퓨터에서 연결 문제가 발생합니다. 다른 프록시 서버가 구성 되어 있는 경우 클라이언트 컴퓨터는 프록시 서버에 대해 Windows SBS 2003을 실행 하는 서버를 계속 사용 합니다. 이 문제를 해결하려면 프록시 서버를 사용하지 않거나 새 프록시 서버를 사용하도록 Internet Explorer를 다시 구성해야 합니다.  
  
#### <a name="to-reconfigure-internet-explorer"></a>Internet Explorer를 다시 구성하려면  
  
1.  Internet Explorer에서 **도구**, **인터넷 옵션**을 차례로 클릭합니다.  
  
2.  **연결** 탭, **LAN 설정**을 차례로 클릭하고 다음의 하나를 수행합니다.  
  
    -   네트워크에서 프록시 서버를 사용하고 있지 않으면 **LAN 설정** 대화 상자에서 모든 확인란을 선택 취소합니다.  
  
    -   네트워크에서 새 프록시 서버를 사용하려면:  
  
        1.  **LAN 설정** 대화 상자의 **자동 구성** 섹션에서 확인란을 선택 취소합니다.  
  
        2.  **프록시 서버** 섹션에서 확인란이 둘 다 선택되었는지 확인합니다.  
  
        3.  **주소** 상자에 프록시 서버의 FQDN(정규화된 도메인 이름)을 입력합니다.  
  
        4.  **포트** 상자에 **80**을 입력합니다.  
  
3.  **확인** 을 두 번 클릭합니다.  
  
4.  웹 사이트로 이동하여 연결 설정이 올바른지 확인합니다.  
  
##  <a name="give-the-built-in-administrators-group-the-right-to-log-on-as-a-batch-job"></a><a name="BKMK_AdminGroup"></a>기본 제공 Administrators 그룹에 일괄 작업으로 로그온 할 수 있는 권한을 부여 합니다.  
 기존 Windows Small Business Server 2003 도메인을 Windows Server Essentials로 마이그레이션한 후에는 기본 제공 Administrators 그룹에 일괄 작업으로 로그온 할 수 있는 권한을 부여 해야 합니다. 기본 제공 Administrators 그룹에 대상 서버에 대한 일괄 작업으로 로그온 권한이 있는지 확인합니다. 관리자는 로그온하지 않고 대상 서버에서 경고를 실행하려면 이 권한이 필요합니다.  
  
#### <a name="to-give-the-built-in-administrators-group-the-right-to-log-on-as-a-batch-job"></a>기본 제공 Administrators 그룹에 일괄 작업으로 로그온 권한을 부여하려면  
  
1. 대상 서버에서 **그룹 정책 관리** 관리 도구를 엽니다.  
  
2. **그룹 정책 관리** 콘솔 트리에서 **포리스트:** *< ServerName\>* 을 확장 하 고 도메인을 확장 한 다음 서버를 확장 합니다.  
  
3. **도메인 컨트롤러**를 확장하고 **기본 도메인 컨트롤러 정책**을 마우스 오른쪽 단추로 클릭하고 나서 **편집**을 클릭합니다.  
  
4. **그룹 정책 관리 편집기**에서 **기본 도메인 컨트롤러 정책**<em>< ServerName\></em> **policy**를 클릭 한 다음 **컴퓨터 구성**을 확장 합니다.  
  
5. **정책**, **Windows 설정**, **보안 설정**을 차례로 확장합니다.  
  
6. **보안 설정** 트리에서 **로컬 정책**을 확장하고 **사용자 권한 할당**을 클릭합니다.  
  
7. 결과 창에서 **일괄 작업으로 로그온**을 마우스 오른쪽 단추로 클릭하고 속성을 클릭합니다.  
  
8. **일괄 작업으로 로그온 속성** 페이지에서 **사용자 또는 그룹 추가**를 클릭합니다.  
  
9. **사용자 또는 그룹 추가** 대화 상자에서 **찾아보기**를 클릭합니다.  
  
10. **사용자, 컴퓨터 또는 그룹 선택** 대화 상자에서 **Administrators**를 입력합니다.  
  
11. **이름 확인**을 클릭하여 기본 제공 Administrators 그룹이 나타나는지 확인하고 **확인**을 세 번 클릭하여 설정을 저장합니다.  
  
## <a name="see-also"></a>참고 항목  
  

-   [Windows SBS 2003에서 마이그레이션](Migrate-Windows-Small-Business-Server-2003-to-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials로 서버 데이터 마이그레이션](Migrate-Server-Data-to-Windows-Server-Essentials.md)

-   [Windows SBS 2003에서 마이그레이션](../migrate/Migrate-Windows-Small-Business-Server-2003-to-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials로 서버 데이터 마이그레이션](../migrate/Migrate-Server-Data-to-Windows-Server-Essentials.md)

