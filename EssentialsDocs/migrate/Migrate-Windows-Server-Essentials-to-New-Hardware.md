---
title: "Windows Server Essentials 새 하드웨어로 마이그레이션합니다"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f695ae90-3160-407b-bebf-9e460f22c86d
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 61106439a63a75143a9cca0989c70370adfedd38
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="migrate-windows-server-essentials-to-new-hardware"></a>Windows Server Essentials 새 하드웨어로 마이그레이션합니다

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

이 가이드에서는 새로운 하드웨어에서 Windows Server Essentials의 기존® 2012 Windows Server Essentials 도메인 마이그레이션을 하는 방법을 설명 하 고 다음 마이그레이션하는 설정 및 데이터를 합니다. 이 가이드 마이그레이션을 완료 한 후 Windows Server Essentials 네트워크에서 기존 서버를 제거 하는 방법도 설명 합니다.  
  
> [!NOTE]
>  마이그레이션 문제를 방지 하려면 Windows Server Essentials 제품 개발 팀은 권장 마이그레이션 시작 하기 전에이 문서를 읽는 합니다.  
  
> [!NOTE]

>  최신 버전의 Windows Server Essentials 서버 데이터 마이그레이션할 참조 [Windows Server essentials 마이그레이션](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md)합니다.  

  
## <a name="additional-resources"></a>추가 리소스  
 추가 정보, 도구 및 마이그레이션 과정을 안내 하는 데 커뮤니티 리소스에 대 한 링크를 방문는 [Windows 소규모 기업 서버 마이그레이션](https://go.microsoft.com/fwlink/?LinkId=217520) 웹 합니다.  
  
## <a name="terms-and-definitions"></a>약관 정의  
 **원본 서버:** 기존 서버 설정 및 데이터를 마이그레이션하는입니다.  
  
 **대상 서버:** 설정 및 데이터를 마이그레이션하는 하는 새 서버 합니다.  
  
## <a name="migration-process-summary"></a>마이그레이션 프로세스 요약  
 이 마이그레이션 가이드 다음 단계에 포함 됩니다.  
  

1.  [Windows Server Essentials 소스 서버 마이그레이션 준비](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md)합니다.  원본 서버 및 네트워크 마이그레이션에 대 한 준비가 지 확인 해야 합니다. 이 섹션을 안내 소스 서버 백업, 원본 서버 시스템 상태를 평가 하 고, 최신 서비스 팩 및 수정 사항, 설치 네트워크 구성 확인 합니다.  
  
2.  [Windows Server Essentials 마이그레이션 모드로 설치](Install-Windows-Server-Essentials-in-migration-mode.md)합니다.  이 섹션 마이그레이션 모드로 대상 서버에 Windows Server Essentials 설치를 위해 수행 해야 하는 단계에 설명 합니다.  
  
3.  [컴퓨터를 새 Windows Server Essentials 서버에 가입](Join-computers-to-the-new-Windows-Server-Essentials-server.md)합니다.  이 섹션 그룹 정책 설정을 업데이트와 새로운 Windows Server Essentials 서버에 참가 클라이언트 컴퓨터에 설명 합니다.  
  
4.  [Windows Server Essentials 대상 서버 마이그레이션 설정 및 데이터 이동](Move-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md)합니다.  이 섹션 원본 서버에서 데이터 마이그레이션 및 설정에 대 한 정보를 제공합니다.  
  
5.  [폴더 리디렉션을 Windows Server Essentials 대상 서버의 구성](Configure-folder-redirection-on-the-Windows-Server-Essentials-Destination-Server.md)합니다.  원본 서버의 폴더 리디렉션을 사용 하는 경우 대상 서버의 폴더 리디렉션을 사용 수 있으며 이전 폴더 리디렉션을 그룹 정책 설정 삭제 합니다.  
  
6.  [원본 서버 새로운 Windows Server Essentials 네트워크에서 제거 하 고 내리기](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md)합니다.  네트워크에서 원본 서버를 제거 하기 전에 그룹 정책 업데이트 되도록 하 고 원본 서버 내리기 해야 합니다.  
  
7.  [Windows Server Essentials 마이그레이션에 대 한 후 마이그레이션 작업을 수행](Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md)합니다.  모든 설정 및 데이터를 Windows Server Essentials 마이그레이션을 완료 하 고 나면 사용자 계정에 허용 된 컴퓨터 매핑하는 것이 좋습니다.  
  
8.  [Windows Server Essentials 모범 사례 분석기 실행](Run-the-Windows-Server-Essentials-Best-Practices-Analyzer.md)합니다.  설정 마이그레이션 및 Windows Server Essentials에 데이터를 완료 한 후 다운로드 하 고 Windows Server Essentials BPA 실행 해야 합니다.  
  
 여러 마이그레이션 절차 관리자 권한으로 명령 프롬프트 창 열면 필요 합니다.  
  
#### <a name="to-open-a-command-prompt-window-as-an-administrator"></a>관리자 권한으로 명령 프롬프트 창을 열려면  
  
1.  에 **시작** 화면에서 검색 상자에 입력 **cmd**합니다.  
  
2.  결과 목록에서 마우스 오른쪽 단추로 클릭 **cmd**을 차례로 클릭 하 고 **관리자 권한으로 실행**합니다.
