---
title: "7 단계: Windows Server Essentials 마이그레이션에 대 한 후 마이그레이션 작업 수행"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
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
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="step-7-perform-post-migration-tasks-for-the-windows-server-essentials-migration"></a>7 단계: Windows Server Essentials 마이그레이션에 대 한 후 마이그레이션 작업 수행

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

다음 작업 일부 원본 서버에 동일한 설정 사용 하 여 목적지 서버 설정을 완료 하는 데 도움이 됩니다. 수 비활성화 되었습니다 이러한 설정 중 일부 원본 서버에 마이그레이션 과정 하므로 대상 서버도 이동 되지 않았습니다.  
  
1.  [원본 서버에 대 한 DNS 항목을 삭제](Step-7--Perform-post-migration-tasks-for-the-Windows-Server-Essentials-migration.md#BKMK_DeleteDNSEntries)  
  
2.  [업무-및 기타 응용 프로그램 데이터 폴더 공유](Step-7--Perform-post-migration-tasks-for-the-Windows-Server-Essentials-migration.md#BKMK_ShareLineOfBusinessAndOtherApplications)  
  
##  <a name="BKMK_DeleteDNSEntries"></a>원본 서버에 대 한 DNS 항목을 삭제  
 원본 서버를 제거한 후 서비스 DNS (도메인 이름) 서버 원본 서버를 가리키는 항목 여전히 포함 될 수 있습니다. 이러한 DNS 항목이 삭제 됩니다.  
  
#### <a name="to-delete-dns-entries-that-point-to-the-source-server"></a>원본 서버를 가리키는 DNS 항목을 삭제 하려면  
  
1.  대상 서버에서 엽니다 **DNS 관리자**합니다.  
  
2.  DNS 관리자 서버 이름을 마우스 오른쪽 단추로 클릭 **속성**을 차례로 클릭 하 고는 **전달자** 탭 합니다.  
  
3.  원본 서버를 가리키는 전달자 목록에서 항목이 있는지 확인 합니다. 없는 경우, 클릭 **편집**, 다음에서 해당 항목을 삭제 하 고 있는 **전달자 편집** 창 합니다.  
  
4.  **DNS 관리자**서버 이름 확장 한 다음 확장 **앞 조회 영역이**합니다.  
  
5.  각 앞 조회 영역에 대 한 영역을 마우스 오른쪽 단추로 클릭, **속성**을 차례로 클릭 하 고 있는 **이름 서버** 탭 합니다.  
  
6.  항목을 선택 하는 **이름 서버** 소스 서버에 포인트를 클릭 하는 텍스트 상자 **제거**를 차례로 클릭 하 고 **확인**합니다.  
  
7.  원본 서버에 대 한 모든 포인터를 제거할 때까지 5, 6 단계를 반복 합니다.  
  
8.  클릭 **확인** 닫을 수 있는 **속성** 창 합니다.  
  
9. **DNS 관리자**, 확장 **역방향 조회 영역이**합니다.  
  
10. 원본 서버를 가리키는 모든 역방향 조회 영역 제거 9 6 단계를 반복 합니다.  
  
##  <a name="BKMK_ShareLineOfBusinessAndOtherApplications"></a>업무-및 기타 응용 프로그램 데이터 폴더 공유  
 공유 폴더 권한 및 비즈니스 선 및 기타 응용 프로그램 데이터 폴더 대상 서버에 복사한 NTFS 권한이 설정 해야 합니다. 공유 폴더에서 사용 권한의 설정한 후에 대시보드에 표시 됩니다는 **저장소** 탭 합니다.  
  
 로그온 스크립트 공유 폴더를 드라이브 매핑를 사용 하는 경우 스크립트 대상 서버의 드라이브에 매핑됩니다를 업데이트 해야 합니다.  
  
## <a name="next-steps"></a>다음 단계  
 Windows Server Essentials 마이그레이션에 대 한 후 마이그레이션 작업을 수행 했습니다. 지금 이동 [단계 8-Windows Server Essentials 모범 사례 분석기 실행](Step-8--Run-the-Windows-Server-Essentials-Best-Practices-Analyzer.md)합니다.  
  

모든 단계를 참조 [Windows Server essentials 마이그레이션](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md)합니다.

