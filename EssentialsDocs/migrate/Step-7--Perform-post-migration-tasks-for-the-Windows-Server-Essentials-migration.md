---
title: '7단계: Windows Server Essentials 마이그레이션을 위한 마이그레이션 후 작업 수행'
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d382e3fd-d393-4bd0-883f-db50104a969f
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 6a61d28f29097bcb6993a471587f4cc1ae0bcc3f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59819164"
---
# <a name="step-7-perform-post-migration-tasks-for-the-windows-server-essentials-migration"></a>7단계: Windows Server Essentials 마이그레이션을 위한 마이그레이션 후 작업 수행

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

다음 작업을 통해 원본 서버에 있던 일부 동일한 설정을 사용하여 대상 서버 설정을 완료할 수 있습니다. 마이그레이션 프로세스 중에 원본 서버에서 이러한 설정의 일부를 사용하지 않도록 설정했을 수 있으므로 대상 서버에 마이그레이션되지 않았습니다.  
  
1.  [원본 서버에 대 한 DNS 항목 삭제](Step-7--Perform-post-migration-tasks-for-the-Windows-Server-Essentials-migration.md#BKMK_DeleteDNSEntries)  
  
2.  [기간 업무 및 기타 응용 프로그램 데이터 폴더 공유](Step-7--Perform-post-migration-tasks-for-the-Windows-Server-Essentials-migration.md#BKMK_ShareLineOfBusinessAndOtherApplications)  
  
##  <a name="BKMK_DeleteDNSEntries"></a> 원본 서버에 대 한 DNS 항목 삭제  
 원본 서버 서비스를 해제하고 나서 DNS(도메인 이름 서비스) 서버에는 원본 서버를 가리키는 항목이 포함되어 있을 수 있습니다. 이러한 DNS 항목을 삭제합니다.  
  
#### <a name="to-delete-dns-entries-that-point-to-the-source-server"></a>원본 서버를 가리키는 DNS 항목을 삭제하려면  
  
1.  대상 서버에서 **DNS 관리자**를 엽니다.  
  
2.  DNS 관리자에서 서버 이름을 마우스 오른쪽 단추로 클릭하고 **속성**, **전달자** 탭을 차례로 클릭합니다.  
  
3.  원본 서버를 가리키는 전달자 목록에서 항목이 있는지 확인합니다. 항목이 있으면 **편집**을 클릭하고 **전달자 편집** 창에서 해당 항목을 삭제합니다.  
  
4.  **DNS 관리자**에서 서버 이름을 확장하고 **정방향 조회 영역**을 확장합니다.  
  
5.  각 정방향 조회 영역에 대한 영역을 마우스 오른쪽 단추로 클릭하고 **속성**, **이름 서버** 탭을 차례로 클릭합니다.  
  
6.  **이름 서버** 텍스트 상자에서 원본 서버를 가리키는 항목을 선택하고 **제거**를 클릭한 후 **확인**을 클릭합니다.  
  
7.  원본 서버에 대한 모든 포인터가 제거될 때까지 5 - 6단계를 반복합니다.  
  
8.  **확인**을 클릭하여 **속성** 창을 닫습니다.  
  
9. **DNS 관리자**에서 **역방향 조회 영역**을 확장합니다.  
  
10. 6~9단계를 반복하여 원본 서버를 가리키는 모든 역방향 조회 영역을 제거합니다.  
  
##  <a name="BKMK_ShareLineOfBusinessAndOtherApplications"></a> 기간 업무 및 기타 응용 프로그램 데이터 폴더 공유  
 대상 서버로 복사한 LOB(기간 업무) 및 기타 응용 프로그램 데이터 폴더에 대해 공유 폴더 사용 권한 및 NTFS 사용 권한을 설정해야 합니다. 사용 권한을 설정하고 나서 공유 폴더가 대시보드의 **저장소** 탭에 표시됩니다.  
  
 로그온 스크립트를 사용하여 공유 폴더에 드라이브를 매핑하는 경우 스크립트를 업데이트하여 대상 서버의 드라이브에 매핑해야 합니다.  
  
## <a name="next-steps"></a>다음 단계  
 Windows Server Essentials 마이그레이션을 위한 마이그레이션 후 작업을 수행 했습니다. 이제 [단계 8-Windows Server Essentials 모범 사례 분석기 실행](Step-8--Run-the-Windows-Server-Essentials-Best-Practices-Analyzer.md)합니다.  
  

모든 단계를 보려면 [Windows Server Essentials로 마이그레이션](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md)합니다.

