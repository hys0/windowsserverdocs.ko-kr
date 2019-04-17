---
title: "Windows Server Essentials migration1에 대 한 후 마이그레이션 작업 수행"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f2d236a4-0d62-4961-9d1f-332054e06f6d
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 535a547ded55cb4afc0942259eadf5222a815274
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="perform-post-migration-tasks-for-windows-server-essentials-migration1"></a>Windows Server Essentials migration1에 대 한 후 마이그레이션 작업 수행

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

다음 작업 일부 원본 서버에 동일한 설정 사용 하 여 목적지 서버 설정을 완료 하는 데 도움이 됩니다. 수 비활성화 되었습니다 이러한 설정 중 일부 원본 서버에 마이그레이션 과정 하므로 대상 서버도 이동 되지 않았습니다. 또는 자녀가 선택적 구성 단계를 수행 해야 할 수도 있습니다.  
  

-   [원본 서버 DNS 항목 삭제](Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md#BKMK_DeleteDNSEntries)  
  
-   [업무-및 기타 응용 프로그램 데이터 폴더 공유](Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md#BKMK_ShareLineOfBusinessAndOtherApplications)  
  
-   [후 마이그레이션 클라이언트 컴퓨터 문제 해결](Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md#BKMK_FixClientComputerIssuesAfterMigrating)  
  
-   [기본 제공 된 관리자가 그룹 일괄 작업으로 로그온 할 수 있는 권한을 제공합니다](Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md#BKMK_AdminGroup)  

-   [원본 서버 DNS 항목 삭제](../migrate/Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md#BKMK_DeleteDNSEntries)  
  
-   [업무-및 기타 응용 프로그램 데이터 폴더 공유](../migrate/Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md#BKMK_ShareLineOfBusinessAndOtherApplications)  
  
-   [후 마이그레이션 클라이언트 컴퓨터 문제 해결](../migrate/Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md#BKMK_FixClientComputerIssuesAfterMigrating)  
  
-   [기본 제공 된 관리자가 그룹 일괄 작업으로 로그온 할 수 있는 권한을 제공합니다](../migrate/Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md#BKMK_AdminGroup)  

  
##  <a name="BKMK_DeleteDNSEntries"></a>원본 서버 DNS 항목 삭제  
 원본 서버를 제거한 후 서비스 DNS (도메인 이름) 서버 원본 서버를 가리키는 항목 여전히 포함 될 수 있습니다. 이러한 DNS 항목이 삭제 됩니다.  
  
#### <a name="to-delete-dns-entries-that-point-to-the-source-server"></a>원본 서버를 가리키는 DNS 항목을 삭제 하려면  
  
1.  대상 서버에서 엽니다 **DNS 관리자**합니다.  
  
2.  DNS 관리자 서버 이름을 마우스 오른쪽 단추로 클릭 **속성**을 차례로 클릭 하 고는 **전달자** 탭 합니다.  
  
3.  원본 서버를 가리키는 전달자 목록에서 항목이 있는지 확인 합니다. 없는 경우, 클릭 **편집**, 다음에서 해당 항목을 삭제 하 고 있는 **전달자 편집** 창 합니다.  
  
4.  **DNS 관리자**서버 이름 확장 한 다음 확장 **앞 조회 영역이**합니다.  
  
5.  각 앞 조회 영역에 대 한 영역을 마우스 오른쪽 단추로 클릭, **속성**을 차례로 클릭 하 고 있는 **이름 서버** 탭 합니다.  
  
6.  항목을 클릭는 **이름 서버** 소스 서버에 포인트를 클릭 하는 상자 **제거**을 차례로 클릭 하 고 **확인**합니다.  
  
7.  원본 서버에 대 한 모든 포인터를 제거할 때까지 5, 6 단계를 반복 합니다.  
  
8.  클릭 **확인** 닫을 수 있는 **속성** 창 합니다.  
  
9. 에 **DNS 관리자** 콘솔, 확장 **역방향 조회 영역이**합니다.  
  
10. 원본 서버를 가리키는 모든 역방향 조회 영역 제거 9 6 단계를 반복 합니다.  
  
##  <a name="BKMK_ShareLineOfBusinessAndOtherApplications"></a>업무-및 기타 응용 프로그램 데이터 폴더 공유  
 공유 폴더 권한 및 비즈니스 선 및 기타 응용 프로그램 데이터 폴더 대상 서버에 복사한 NTFS 권한이 설정 해야 합니다. 공유 폴더에서 Windows Server Essentials 대시보드에 표시 되는 사용 권한의 설정한 후는 **저장소** 섹션.  
  
 로그온 스크립트 공유 폴더를 드라이브 매핑를 사용 하는 경우 스크립트 대상 서버의 드라이브에 매핑됩니다를 업데이트 해야 합니다.  
  
##  <a name="BKMK_FixClientComputerIssuesAfterMigrating"></a>후 마이그레이션 클라이언트 컴퓨터 문제 해결  
 Windows Server essentials Windows 작은 Business Server 2003 프리미엄 Edition Microsoft 인터넷 보안 및 라우터 서버가 설치 마이그레이션할 경우 네트워크에서 컴퓨터 클라이언트 아직 Microsoft 방화벽 클라이언트 및 Internet Explorer 프록시 서버를 사용 하도록 구성 합니다.  
  
 이 인해 연결 문제가 클라이언트에서 컴퓨터를 프록시 서버 더 이상 존재 하기 때문입니다. 다른 프록시 서버 구성 된 경우 컴퓨터 프록시 서버에 대 한 Windows SBS 2003을 실행 하는 서버를 사용 하 여 계속 합니다. 이 문제를 해결 하려면 Internet Explorer 프록시 서버를 사용 하지 않도록 또는 새 프록시 서버를 사용 하 여를 다시 구성 해야 합니다.  
  
#### <a name="to-reconfigure-internet-explorer"></a>Internet Explorer를 다시 구성 하려면  
  
1.  Internet Explorer 클릭 **도구**을 차례로 클릭 하 고 **인터넷 옵션**합니다.  
  
2.  클릭는 **연결** 탭을 클릭 **LAN 설정**, 하 고 다음 중 하나를 수행 합니다.  
  
    -   프록시 서버에서 네트워크를 사용 하지 않는 경우에 모든 확인란의 선택을 취소는 **(LAN) 설정** 대화 상자가 합니다.  
  
    -   네트워크에서 새 프록시 서버를 사용 하려면:  
  
        1.  **(LAN) 설정** 확인란의 선택을 취소 합니다 대화 상자에서 **자동 구성** 섹션.  
  
        2.  에 **프록시 서버** 섹션, 확인란을 모두 선택 되어 있는지 확인 합니다.  
  
        3.  에 **주소** 상자에 프록시 서버 (FQDN) 정식된 도메인 이름 입력 합니다.  
  
        4.  에 **포트** 상자에 입력 **80**합니다.  
  
3.  클릭 **확인** 두 번 합니다.  
  
4.  연결 설정이 올바른지 확인 하기 위해 웹 사이트로 이동 합니다.  
  
##  <a name="BKMK_AdminGroup"></a>기본 제공 된 관리자가 그룹 일괄 작업으로 로그온 할 수 있는 권한을 제공합니다  
 Windows Server essentials 기존 Windows Small Business Server 2003 도메인 마이그레이션할 권리를 배치 작업으로 로그온 기본 관리자가 그룹 제공 해야 있습니다. 기본 관리자가 그룹 아직 대상 서버에 배치 작업으로 로그온 수 있는 권한이 있는지 확인 합니다. 관리자가이 권리를 알림을 대상 서버에 로그인 하지 않고도 실행 해야 합니다.  
  
#### <a name="to-give-the-built-in-administrators-group-the-right-to-log-on-as-a-batch-job"></a>관리자가 그룹 일괄 작업으로 로그온 권한을 제공 기본 제공  
  
1.  대상 서버에서 엽니다는 **그룹 정책 관리** 관리 도구입니다.  
  
2.  에 **그룹 정책 관리** 콘솔 트리에서, 확장 **숲:***< ServerName\ >*도메인 확장 한 다음 서버를 확장 합니다.  
  
3.  확장 **도메인 컨트롤러**를 마우스 오른쪽 단추로 클릭 **기본 도메인 컨트롤러 정책**을 차례로 클릭 하 고 **편집**합니다.  
  
4.  **그룹 정책 편집기 관리**, 클릭 **기본 도메인 컨트롤러 정책***< ServerName\ >***정책**를 확장 한 다음 **컴퓨터 구성**합니다.  
  
5.  확장 **정책**, 확장 **Windows 설정**를 확장 한 다음 **보안 설정**합니다.  
  
6.  **보안 설정** 트리를 확장 **로컬 정책**을 차례로 클릭 하 고 **사용자 권한 할당**합니다.  
  
7.  결과 창에서 마우스 오른쪽 단추로 클릭 **일괄 작업으로 로그온**, 마우스 속성을 클릭 합니다.  
  
8.  에 **일괄 작업 속성으로 로그온** 페이지, 클릭 **사용자 또는 그룹 추가**합니다.  
  
9. 에 **사용자 또는 그룹 추가** 대화 상자를 클릭 **찾아보기**합니다.  
  
10. 에 **사용자를 컴퓨터 또는 그룹 선택** 대화 상자에서 유형 **관리자**합니다.  
  
11. 클릭 **이름 확인** 기본 관리자가 그룹 나타나면 및 클릭 한 다음 확인 하려면 **확인** 세 번 설정을 저장 합니다.  
  
## <a name="see-also"></a>참조 하십시오  
  

-   [Windows SBS 2003 마이그레이션](Migrate-Windows-Small-Business-Server-2003-to-Windows-Server-Essentials.md)  
  
-   [Windows Server essentials 서버 데이터 마이그레이션](Migrate-Server-Data-to-Windows-Server-Essentials.md)

-   [Windows SBS 2003 마이그레이션](../migrate/Migrate-Windows-Small-Business-Server-2003-to-Windows-Server-Essentials.md)  
  
-   [Windows Server essentials 서버 데이터 마이그레이션](../migrate/Migrate-Server-Data-to-Windows-Server-Essentials.md)

