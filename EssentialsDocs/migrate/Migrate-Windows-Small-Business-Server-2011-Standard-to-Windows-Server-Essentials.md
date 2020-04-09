---
title: Windows Small Business Server 2011 Standard에서 Windows Server Essentials로 마이그레이션
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: c8325f87-fd79-471b-bf70-3f052692c383
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: d4f4dbb7063428aee7728071b8e62c5cc019b2af
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80852496"
---
# <a name="migrate-windows-small-business-server-2011-standard-to-windows-server-essentials"></a>Windows Small Business Server 2011 Standard에서 Windows Server Essentials로 마이그레이션

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

이 가이드에서는 기존 Windows Small Business Server 2011 Standard 도메인을 새 하드웨어의 Windows Server&reg; 2012 Essentials로 마이그레이션한 다음 설정 및 데이터를 마이그레이션하는 방법에 대해 설명 합니다. 또한 마이그레이션을 완료 한 후에 Windows Server Essentials 네트워크에서 기존 서버를 제거 하는 방법을 설명 합니다.  
  
> [!NOTE]
>  마이그레이션 중에 문제를 방지 하기 위해 Windows Server Essentials 제품 개발 팀에서는 마이그레이션을 시작 하기 전에이 문서를 읽을 것을 적극 권장 합니다.  
> 
> [!NOTE]
> 
>  최신 버전의 Windows Server Essentials로 서버 데이터를 마이그레이션하려면 [Windows Server essentials로 마이그레이션](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md)을 참조 하세요.  
> 
>  최신 버전의 Windows Server Essentials로 서버 데이터를 마이그레이션하려면 [Windows Server essentials로 마이그레이션](../migrate/Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md)을 참조 하세요.  

  
## <a name="additional-resources"></a>추가 리소스  
 마이그레이션 프로세스에 도움이 되는 추가 정보, 도구 및 커뮤니티 리소스에 대한 링크는 [Windows Small Business Server 마이그레이션](https://go.microsoft.com/fwlink/?LinkId=217520)을 참조하세요.  
  
## <a name="terms-and-definitions"></a>용어 및 정의  
 **원본 서버:** 설정 및 데이터를 마이그레이션하는 기존 서버입니다.  
  
 **대상 서버:** 설정 및 데이터를 마이그레이션하는 새 서버입니다.  
  
## <a name="migration-process-summary"></a>마이그레이션 프로세스 요약  
 이 마이그레이션 가이드는 다음 단계로 이루어집니다.  
  

1.  [Windows Server Essentials 마이그레이션을 위해 원본 서버를 준비](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md)합니다.  원본 서버 및 네트워크가 마이그레이션할 준비가 되었는지 확인해야 합니다. 이 섹션에서는 원본 서버를 백업하고, 원본 서버 시스템 상태를 평가하고, 최신 서비스 팩 및 수정 프로그램을 설치하고, 네트워크 구성을 확인하는 과정을 안내합니다.  
  
2.  [마이그레이션 모드에서 Windows Server Essentials를 설치](Install-Windows-Server-Essentials-in-migration-mode.md)합니다.  이 섹션에서는 마이그레이션 모드에서 대상 서버에 Windows Server Essentials를 설치 하기 위해 수행 해야 하는 단계에 대해 설명 합니다.  
  
3.  [새 Windows Server Essentials 서버에 컴퓨터를 연결](Join-computers-to-the-new-Windows-Server-Essentials-server.md)합니다.  이 섹션에서는 새 Windows Server Essentials 네트워크에 클라이언트 컴퓨터를 가입 하 고 그룹 정책 설정을 업데이트 하는 방법을 설명 합니다.  
  
4.  [SBS 2011 설정 및 데이터를 대상 서버로 이동](Move-Windows-SBS-2011-Standard-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md)합니다.  이 섹션에서는 원본 서버에서 데이터 및 설정을 마이그레이션하는 방법에 대한 정보를 제공합니다.  
  
5.  [Windows Server Essentials 대상 서버에서 폴더 리디렉션을 사용 하도록 설정](Enable-folder-redirection-on-the-Windows-Server-Essentials-Destination-Server.md)합니다.  원본 서버에서 폴더 리디렉션을 사용하는 경우 대상 서버에서 폴더 리디렉션을 사용하도록 설정한 다음 이전 폴더 리디렉션 그룹 정책 설정을 삭제할 수 있습니다.  
  
6.  [새 Windows Server Essentials 네트워크에서 원본 서버 수준 내리기 및 제거](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md)  네트워크에서 원본 서버를 제거하기 전에 그룹 정책을 강제로 업데이트하고 원본 서버의 수준을 내려야 합니다.  
  
7.  [Windows Server Essentials 마이그레이션을 위한 마이그레이션 후 작업을 수행](Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md)합니다.  모든 설정 및 데이터를 Windows Server Essentials로 마이그레이션한 후에는 허용 된 컴퓨터를 사용자 계정에 매핑할 수 있습니다.  
  
8.  [Windows Server Essentials 모범 사례 분석기를 실행](Run-the-Windows-Server-Essentials-Best-Practices-Analyzer.md)합니다.  설정 및 데이터를 Windows Server Essentials로 마이그레이션한 후에는 Windows Server Essentials BPA를 실행 해야 합니다.  
 
 일부 마이그레이션 절차에서는 관리자 권한으로 명령 프롬프트 창을 열어야 합니다.  
  
###  <a name="to-open-a-command-prompt-window-on-the-source-server-as-an-administrator"></a><a name="BKMK_OpenACommandPromptAsAdmin"></a>원본 서버에서 관리자 권한으로 명령 프롬프트 창을 열려면  
  
1.  **시작**을 클릭합니다.  
  
2.  검색 상자에 **cmd**를 입력합니다.  
  
3.  결과 목록에서 **cmd**를 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행**을 클릭합니다.  
  
#### <a name="to-open-a-command-prompt-window-on-the-destination-server-as-an-administrator"></a>대상 서버에서 관리자 권한으로 명령 프롬프트 창을 열려면  
  
1.  **시작** 화면의 검색 상자에 **cmd**를 입력합니다.  
  
2.  결과 목록에서 **cmd**를 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행**을 클릭합니다.
