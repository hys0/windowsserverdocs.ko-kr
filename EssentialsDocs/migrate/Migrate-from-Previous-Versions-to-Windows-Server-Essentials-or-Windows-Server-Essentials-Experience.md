---
title: 이전 버전에서 Windows Server Essentials 또는 Windows Server Essentials Experience로 마이그레이션
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: 2974fb3a-5150-43fd-a73f-3e5074eb5d03
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 5c73714dff2d89201ac93704105038c604f12e06
ms.sourcegitcommit: 2f072c0c02e3e0deae331ca64b375d63b89d0522
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2020
ms.locfileid: "83404578"
---
# <a name="migrate-from-previous-versions-to-windows-server-essentials-or-windows-server-essentials-experience"></a>이전 버전에서 Windows Server Essentials 또는 Windows Server Essentials Experience로 마이그레이션

>적용 대상: Windows Server 2012 R2 Essentials

이 가이드에서는 이전 버전의 Windows Small Business Server 및 Windows Server Essentials (Windows Server Essentials, Windows Small Business Server 2011 Standard, Windows Small Business Server 2011 Essentials, Windows Small business Server 2008 및 Windows Small business server 2003 포함)에서 windows server essentials로 또는 windows server Essentials Experience 역할이 설치 된 Windows Server 2012 r 2로 마이그레이션하는 방법에 대해 설명 합니다.  
  
 **최대 25 명의 사용자와 50 장치가 있는 환경의 경우**이 가이드의 단계를 수행 하 여 이전 버전의 windows SBS에서 Windows Server Essentials로 마이그레이션할 수 있습니다.  
  
 **최대 100 명의 사용자 및 200 장치가 있는 환경의 경우**동일한 지침에 따라 Windows Server Essentials Experience 역할이 설치 된 windows Server 2012 R2 Standard 또는 Datacenter 버전으로 마이그레이션할 수 있습니다.  
  
> [!NOTE]
>  Windows Server Essentials 제품 개발 팀에서는 마이그레이션하는 동안 문제를 방지하기 위해 마이그레이션을 시작하기 전에 이 문서를 읽을 것을 적극 권장합니다.  
  
## <a name="terms-and-definitions"></a>용어 및 정의  
 **원본 서버** 설정 및 데이터를 마이그레이션하는 기존 서버입니다.  
  
 **대상 서버** 설정 및 데이터를 마이그레이션하는 새 서버입니다.  
  
## <a name="migration-process-summary"></a>마이그레이션 프로세스 요약  
 이 마이그레이션 가이드는 다음 단계로 이루어집니다.  
  
1. [1 단계: Windows Server Essentials 마이그레이션을 위한 원본 서버 준비](Step-1--Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md)  원본 서버 및 네트워크가 마이그레이션할 준비가 되었는지 확인해야 합니다. 이 섹션에서는 원본 서버를 백업하고, 원본 서버 시스템 상태를 평가하고, 최신 서비스 팩 및 수정 프로그램을 설치하고, 네트워크 구성을 확인하는 과정을 안내합니다.  
  
2. [2 단계: Windows Server Essentials를 새 복제본 도메인 컨트롤러로 설치](Step-2--Install-Windows-Server-Essentials-as-a-new-replica-domain-controller.md)합니다. 이 섹션에서는 windows server Essentials 또는 windows server Essentials Experience 역할을 사용 하도록 설정 된 windows server 2012 R2 Standard를 도메인 컨트롤러로 설치 하는 방법을 설명 합니다.  
  
3. [3 단계: 새 Windows Server Essentials 서버에 컴퓨터를 연결](Step-3--Join-computers-to-the-new-Windows-Server-Essentials-server.md)합니다.  이 섹션에서는 Windows Server Essentials를 실행 하는 새 서버에 클라이언트 컴퓨터를 연결 하 고 그룹 정책 설정을 업데이트 하는 방법을 설명 합니다.  
  
4. [4 단계: Windows Server Essentials 마이그레이션을 위해 대상 서버에 설정 및 데이터를 이동](Step-4--Move-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md)합니다.  이 섹션에서는 원본 서버에서 데이터 및 설정을 마이그레이션하는 방법에 대한 정보를 제공합니다.  
  
5. [5 단계: Windows Server Essentials 마이그레이션을 위해 대상 서버에서 폴더 리디렉션을 사용 하도록 설정](Step-5--Enable-folder-redirection-on-the-Destination-Server-for-Windows-Server-Essentials-migration.md)합니다.  원본 서버에서 폴더 리디렉션을 사용하는 경우 대상 서버에서 폴더 리디렉션을 사용하도록 설정한 다음 이전 폴더 리디렉션 그룹 정책 설정을 삭제할 수 있습니다.  
  
6. [6 단계: 새 Windows Server Essentials 네트워크에서 원본 서버 수준 내리기 및 제거](Step-6--Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md)  네트워크에서 원본 서버를 제거하기 전에 그룹 정책을 강제로 업데이트하고 원본 서버의 수준을 내려야 합니다.  
  
7. [7 단계: Windows Server Essentials 마이그레이션을 위한 마이그레이션 후 작업을 수행](Step-7--Perform-post-migration-tasks-for-the-Windows-Server-Essentials-migration.md)합니다.  모든 설정 및 데이터를 Windows Server Essentials로 마이그레이션한 후에는 허용 된 컴퓨터를 사용자 계정에 매핑할 수 있습니다.  
  
8. [8 단계: Windows Server Essentials 모범 사례 분석기를 실행](Step-8--Run-the-Windows-Server-Essentials-Best-Practices-Analyzer.md)합니다.  Windows Server Essentials에 대 한 설정 및 데이터 마이그레이션을 완료 한 후에는 Windows Server Essentials 모범 사례 분석기 (BPA)를 실행 해야 합니다.  
  
   일부 마이그레이션 절차에서는 관리자 권한으로 명령 프롬프트 창을 열어야 합니다. 다음 절차에서는 이렇게 하는 방법을 설명합니다.  
  
###  <a name="to-open-a-command-prompt-window-on-the-source-server-as-an-administrator"></a><a name="BKMK_OpenACommandPromptAsAdmin"></a>원본 서버에서 관리자 권한으로 명령 프롬프트 창을 열려면  
  
1.  **시작**을 클릭합니다.  
  
2.  검색 상자에 **cmd**를 입력합니다.  
  
3.  결과 목록에서 **cmd**를 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행**을 클릭합니다.  
  
#### <a name="to-open-a-command-prompt-window-on-the-destination-server-as-an-administrator"></a>대상 서버에서 관리자 권한으로 명령 프롬프트 창을 열려면  
  
1.  **시작** 화면의 검색 상자에 **cmd**를 입력합니다.  
  
2.  결과 목록에서 **cmd**를 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행**을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
  
-   [Windows Server Essentials로 서버 데이터 마이그레이션](Migrate-Server-Data-to-Windows-Server-Essentials.md)

-   [Windows Server Essentials로 서버 데이터 마이그레이션](../migrate/Migrate-Server-Data-to-Windows-Server-Essentials.md)

