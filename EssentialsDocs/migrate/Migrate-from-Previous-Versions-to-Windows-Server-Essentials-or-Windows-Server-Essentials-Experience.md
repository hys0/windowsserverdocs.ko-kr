---
title: "이전 버전의 Windows Server Essentials 또는 Windows Server Essentials 경험 마이그레이션을"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
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
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="migrate-from-previous-versions-to-windows-server-essentials-or-windows-server-essentials-experience"></a>이전 버전의 Windows Server Essentials 또는 Windows Server Essentials 경험 마이그레이션을

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

이 가이드에서는 Windows Server Essentials 경험 역할이 설치 된 이전 버전의 Windows Small Business Server 및 Windows Server Essentials (Windows Server Essentials, Windows 작은 Business Server 2011 표준, Windows 작은 Business Server 2011 Essentials, Windows Small Business Server 2008 및 Windows Small Business Server 2003 포함)에서 Windows Server Essentials 또는 Windows Server 2012 r 2 마이그레이션할 하는 방법을 설명 합니다.  
  
 **최대 25 명의 사용자와 장치 50 환경에 대 한**, SBS Windows의 이전 버전의 Windows Server Essentials 하 게 마이그레이션하이 가이드에서 단계를 수행할 수 있습니다.  
  
 **카멜레온 200 디바이스와 사용자가 최대 100 개의 환경에 대 한**, Windows Server Essentials 경험 역할이 설치와 Windows Server 2012 r 2는 표준 또는 Datacenter edition 하 게 마이그레이션하는 동일한 지침을 따를 수 있습니다.  
  
> [!NOTE]
>  마이그레이션 문제를 방지 하려면 Windows Server Essentials 제품 개발 팀은 권장 마이그레이션 시작 하기 전에이 문서를 읽는 합니다.  
  
## <a name="terms-and-definitions"></a>약관 정의  
 **서버 원본** 기존 서버 설정 및 데이터를 마이그레이션하는입니다.  
  
 **대상 서버** 설정 및 데이터를 마이그레이션하는 하는 새 서버 합니다.  
  
## <a name="migration-process-summary"></a>마이그레이션 프로세스 요약  
 이 마이그레이션 가이드 다음 단계에 포함 됩니다.  
  
1.  [1 단계: Windows Server Essentials 소스 서버 마이그레이션 준비](Step-1--Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md)합니다.  원본 서버 및 네트워크 마이그레이션에 대 한 준비가 지 확인 해야 합니다. 이 섹션을 안내 소스 서버 백업, 원본 서버 시스템 상태를 평가 하 고, 최신 서비스 팩 및 수정 사항, 설치 네트워크 구성 확인 합니다.  
  
2.  [새로운 복제 도메인 컨트롤러도 2 단계: Windows Server Essentials를 설치](Step-2--Install-Windows-Server-Essentials-as-a-new-replica-domain-controller.md)합니다. 도메인 컨트롤러를 사용 하도록 설정한 Windows Server Essentials 경험 역할) (와 Windows Server Essentials 또는 Windows Server 2012 r 2 표준 설치 하는 방법을 설명 합니다.  
  
3.  [3 단계: 컴퓨터 새로운 Windows Server Essentials 서버에 가입](Step-3--Join-computers-to-the-new-Windows-Server-Essentials-server.md)합니다.  Windows Server Essentials 실행을 그룹 정책 설정을 업데이트 하는 새 서버 클라이언트 컴퓨터에 참여 하는 방법을 설명이 합니다.  
  
4.  [4 단계: Windows Server Essentials 대상 서버 마이그레이션 설정 및 데이터 이동](Step-4--Move-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md)합니다.  이 섹션 원본 서버에서 데이터 마이그레이션 및 설정에 대 한 정보를 제공합니다.  
  
5.  [5 단계: Windows Server Essentials 대상 서버 마이그레이션에 폴더 리디렉션을 사용](Step-5--Enable-folder-redirection-on-the-Destination-Server-for-Windows-Server-Essentials-migration.md)합니다.  원본 서버의 폴더 리디렉션을 사용 하는 경우 대상 서버의 폴더 리디렉션을 사용 수 있으며 이전 폴더 리디렉션을 그룹 정책 설정 삭제 합니다.  
  
6.  [6 단계: 내리기와 새로운 Windows Server Essentials 네트워크에서 소스 서버 제거](Step-6--Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md)합니다.  네트워크에서 원본 서버를 제거 하기 전에 그룹 정책 업데이트 되도록 하 고 원본 서버 내리기 해야 합니다.  
  
7.  [7 단계: Windows Server Essentials 마이그레이션에 대 한 후 마이그레이션 작업을 수행](Step-7--Perform-post-migration-tasks-for-the-Windows-Server-Essentials-migration.md)합니다.  모든 설정 및 데이터를 Windows Server Essentials 마이그레이션을 완료 하 고 나면 사용자 계정에 허용 된 컴퓨터 매핑하는 것이 좋습니다.  
  
8.  [8 단계: Windows Server Essentials 모범 사례 분석기 실행](Step-8--Run-the-Windows-Server-Essentials-Best-Practices-Analyzer.md)합니다.  설정 마이그레이션 및 Windows Server Essentials에 데이터를 마친 후는 Windows Server Essentials 좋은 방법 분석기 (BPA)를 실행 해야 합니다.  
  
 여러 마이그레이션 절차 관리자 권한으로 명령 프롬프트 창 열면 필요 합니다. 다음 절차에이 작업을 수행 하는 방법을 설명 합니다.  
  
###  <a name="BKMK_OpenACommandPromptAsAdmin"></a>관리자 권한으로 명령 프롬프트 창을 원본 서버의 열려면  
  
1.  클릭 **시작**합니다.  
  
2.  검색 상자에 입력 **cmd**합니다.  
  
3.  결과 목록에서 마우스 오른쪽 단추로 클릭 **cmd**을 차례로 클릭 하 고 **관리자 권한으로 실행**합니다.  
  
#### <a name="to-open-a-command-prompt-window-on-the-destination-server-as-an-administrator"></a>관리자 권한으로 명령 프롬프트 창을 대상 서버의 열려면  
  
1.  에 **시작** 화면에서 검색 상자에 입력 **cmd**합니다.  
  
2.  결과 목록에서 마우스 오른쪽 단추로 클릭 **cmd**을 차례로 클릭 하 고 **관리자 권한으로 실행**합니다.  
  
## <a name="see-also"></a>참조 하십시오  
  
-   [Windows Server essentials 서버 데이터 마이그레이션](Migrate-Server-Data-to-Windows-Server-Essentials.md)

-   [Windows Server essentials 서버 데이터 마이그레이션](../migrate/Migrate-Server-Data-to-Windows-Server-Essentials.md)

