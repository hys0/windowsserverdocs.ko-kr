---
title: 이전 버전에서 Windows Server Essentials 또는 Windows Server Essentials Experience로 마이그레이션
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.custom: na
ms.date: 10/03/20116
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2974fb3a-5150-43fd-a73f-3e5074eb5d03
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 213ee4304d9d4ebdb7580f7f78fdaca78aa454c9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59883874"
---
# <a name="migrate-from-previous-versions-to-windows-server-essentials-or-windows-server-essentials-experience"></a>이전 버전에서 Windows Server Essentials 또는 Windows Server Essentials Experience로 마이그레이션

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

이 가이드에서는 이전 버전의 Windows Small Business Server 및 Windows Server Essentials (Windows Server Essentials, Windows Small Business Server 2011 Standard, Windows Small Business Server 2011 Essentials, Windows 등에서 마이그레이션하는 방법을 설명 합니다. Small Business Server 2008 및 Windows Small Business Server 2003) Windows Server Essentials 또는 Windows Server Essentials Experience 역할이 설치 된 Windows Server 2012 R2.  
  
 **최대 25 명의 사용자와 50 대의 장치가 있는 환경의**, Windows Server Essentials로 마이그레이션 이전 버전의 Windows SBS이이 가이드의 단계를 수행할 수 있습니다.  
  
 **최대 100 명의 사용자와 200 대의 장치가 있는 환경의**, Windows Server Essentials Experience 역할이 설치 된 Windows Server 2012 r2 Standard 또는 Datacenter 버전으로 마이그레이션할 동일한 지침을 따를 수 있습니다.  
  
> [!NOTE]
>  Windows Server Essentials 제품 개발 팀에서는 마이그레이션하는 동안 문제를 방지하기 위해 마이그레이션을 시작하기 전에 이 문서를 읽을 것을 적극 권장합니다.  
  
## <a name="terms-and-definitions"></a>용어 및 정의  
 **원본 서버** 설정 및 데이터를 마이그레이션하는 기존 서버입니다.  
  
 **대상 서버** 설정 및 데이터를 마이그레이션하는 새 서버입니다.  
  
## <a name="migration-process-summary"></a>마이그레이션 프로세스 요약  
 이 마이그레이션 가이드는 다음 단계로 이루어집니다.  
  
1.  [1단계: Windows Server Essentials의 원본 서버에 대 한 마이그레이션을 준비](Step-1--Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md)합니다.  원본 서버 및 네트워크가 마이그레이션할 준비가 되었는지 확인해야 합니다. 이 섹션에서는 원본 서버를 백업하고, 원본 서버 시스템 상태를 평가하고, 최신 서비스 팩 및 수정 프로그램을 설치하고, 네트워크 구성을 확인하는 과정을 안내합니다.  
  
2.  [2단계: Windows Server Essentials를 새 복제본 도메인 컨트롤러로 설치](Step-2--Install-Windows-Server-Essentials-as-a-new-replica-domain-controller.md)합니다. 이 섹션에서는 도메인 컨트롤러로 설치 하는 방법 Windows Server Essentials 또는 Windows Server 2012 R2 Standard (사용 하도록 설정 하는 Windows Server Essentials Experience 역할)을 설명 합니다.  
  
3.  [3 단계: 새 Windows Server Essentials 서버에 컴퓨터 가입](Step-3--Join-computers-to-the-new-Windows-Server-Essentials-server.md)합니다.  이 섹션에서는 Windows Server Essentials를 실행 하 고 그룹 정책 설정을 업데이트 하는 새 서버에 클라이언트 컴퓨터를 가입 하는 방법에 설명 합니다.  
  
4.  [4 단계: 서버에 대 한 Windows Server Essentials 마이그레이션을 위해 대상 설정 및 데이터 이동](Step-4--Move-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md)합니다.  이 섹션에서는 원본 서버에서 데이터 및 설정을 마이그레이션하는 방법에 대한 정보를 제공합니다.  
  
5.  [5단계: Windows Server Essentials의 대상 서버에 대 한 마이그레이션에 대 한 폴더 리디렉션 사용](Step-5--Enable-folder-redirection-on-the-Destination-Server-for-Windows-Server-Essentials-migration.md)합니다.  원본 서버에서 폴더 리디렉션을 사용하는 경우 대상 서버에서 폴더 리디렉션을 사용하도록 설정한 다음 이전 폴더 리디렉션 그룹 정책 설정을 삭제할 수 있습니다.  
  
6.  [6 단계: 수준 내리기 및 새 Windows Server Essentials 네트워크에서 원본 서버 제거](Step-6--Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md)합니다.  네트워크에서 원본 서버를 제거하기 전에 그룹 정책을 강제로 업데이트하고 원본 서버의 수준을 내려야 합니다.  
  
7.  [7 단계: Windows Server Essentials 마이그레이션을 위한 마이그레이션 후 작업 수행](Step-7--Perform-post-migration-tasks-for-the-Windows-Server-Essentials-migration.md)합니다.  모든 설정 및 데이터를 Windows Server Essentials로 마이그레이션를 마친 후에 사용자 계정에 허용 되는 컴퓨터를 매핑하는 것이 좋습니다.  
  
8.  [8 단계: Windows Server Essentials 모범 사례 분석기 실행](Step-8--Run-the-Windows-Server-Essentials-Best-Practices-Analyzer.md)합니다.  마이그레이션 설정 및 데이터를 Windows Server Essentials를 마친 후 Windows Server Essentials BPA Best Practices Analyzer ()를 실행 해야 합니다.  
  
 일부 마이그레이션 절차에서는 관리자 권한으로 명령 프롬프트 창을 열어야 합니다. 다음 절차에서는 이렇게 하는 방법을 설명합니다.  
  
###  <a name="BKMK_OpenACommandPromptAsAdmin"></a> 관리자로 원본 서버에서 명령 프롬프트 창을 열려면  
  
1.  **시작**을 클릭합니다.  
  
2.  검색 상자에 **cmd**를 입력합니다.  
  
3.  결과 목록에서 **cmd**를 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행**을 클릭합니다.  
  
#### <a name="to-open-a-command-prompt-window-on-the-destination-server-as-an-administrator"></a>대상 서버에서 관리자 권한으로 명령 프롬프트 창을 열려면  
  
1.  **시작** 화면의 검색 상자에 **cmd**를 입력합니다.  
  
2.  결과 목록에서 **cmd**를 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행**을 클릭합니다.  
  
## <a name="see-also"></a>참조  
  
-   [Windows Server Essentials로 서버 데이터 마이그레이션](Migrate-Server-Data-to-Windows-Server-Essentials.md)

-   [Windows Server Essentials로 서버 데이터 마이그레이션](../migrate/Migrate-Server-Data-to-Windows-Server-Essentials.md)

