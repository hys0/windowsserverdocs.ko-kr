---
title: "Windows Server Essentials 마이그레이션 모드 1에 설치"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fd7196ac-cfa6-46a5-ba77-6962b47a825e
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 808a4b1e120fa559d603b34ad006b18de6b94378
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="install-windows-server-essentials-in-migration-mode1"></a>Windows Server Essentials 마이그레이션 모드 1에 설치

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

Windows Server Essentials 실행 하는 네트워크에만 한 서버 수 있고 해당 서버 네트워크 도메인 컨트롤러 해야 합니다.  
  
 마이그레이션 모드로 Windows Server Essentials를 설치할 때 설치 마법사는 다음과 같은 작업을 수행 합니다.  
  
1.  설치 하 고 대상 서버에는 Windows Server Essentials 서버 소프트웨어를 구성 합니다.  
  
2.  도메인 스키마 가장 최신 버전으로 업데이트 됩니다.  
  
3.  대상 서버 기존 도메인에 연결 합니다. 원본 서버와 대상 서버는 모두 같은 도메인 마이그레이션 프로세스가 끝날 때까지 합니다. 마이그레이션을 완료 되 면 21 일 내 네트워크에서 소스 서버를 제거 해야 합니다.  
  
    > [!WARNING]
    >  오류 메시지가 소스 서버 네트워크에서 제거 될 때까지 21 일 유예 기간 동안 매일 이벤트 로그에 추가 됩니다. 텍스트의 메시지 읽기 "FSMO 역할 검사 상태 감지 중단 라이선스 정책 준수 하는 사용자 환경의 합니다. 주 도메인 컨트롤러 및 도메인 마스터 Active Directory 역할 명명 관리 서버 누르고 있어야 합니다. 이제 관리 서버에 Active Directory 역할 이동 하세요. 이 서버는 자동으로 종료 때가이 상태를 찾았습니다 처음부터 21 일에 문제가 해결 되지 않으면. " 21 일 유예 기간이 지나면 원본 서버 종료 됩니다.  
  
4.  원본 서버에서 작업 마스터 (단일 유연한 마스터 작업 나 FSMO 라고도 함) 역할을 대상 서버에 전송합니다. 작업 마스터 역할은 표준 데이터를 전송 하 고 업데이트 방법이 적합 하지 않은 경우에 사용 되는 도메인 컨트롤러 특별 한 작업을 합니다. 대상 서버 도메인 컨트롤러 차면 마스터 역할을 작업은 보유 해야 것입니다.  
  
5.  대상 서버 드 서버도 구성 됩니다. 드 서버는 분산된 데이터 저장소를 관리 하는 도메인 컨트롤러 합니다. 검색 및 일부 표현 Active Directory 숲 속의 모든 도메인에 있는 모든 개체의 포함 됩니다.  
  
6.  대상 서버 사이트 라이선스 서버도 구성 됩니다.  
  
##  <a name="BKMK_Install"></a>Windows Server Essentials 대상 서버의 설치  
 설치 하 고 구성 Windows Server Essentials 마이그레이션 모드로 대상 서버의 다음 절차를 수행 합니다.  
  
#### <a name="to-install-windows-server-essentials-on-the-destination-server"></a>Windows Server Essentials 대상 서버에 설치 하려면  
  
1.  대상 서버 설정 하 고 Windows Server Essentials DVD1 DVD 드라이브에 삽입 합니다. CD 또는 DVD에서 부팅 것인지 묻는 메시지가 표시 아무 키나지 않습니다.  
  
    > [!NOTE]
    >  사용할 수 있는 대상 서버 USB 플래시 드라이브에서 부팅를 지 원하는 경우는 **Windows 7/USB DVD 다운로드 도구** Windows Server Essentials ISO 파일에서 부팅 가능한 USB 플래시 드라이브를 만들 수 있습니다. USB 플래시 드라이브를 사용 하 여 크게 속도를 높일 수 설치 프로세스 플래시 드라이브 데이터 DVD-ROM 드라이브 보다 훨씬 신속 읽습니다 하기 때문입니다. 부팅 가능한 USB 플래시 드라이브를 만든 후 응답 파일 플래시 드라이브를 추가할 수 있습니다. 하면 [Windows 7/USB DVD 다운로드 도구를 다운로드](https://go.microsoft.com/fwlink/p/?LinkId=248282) Microsoft 스토어 웹 사이트에서 무료입니다.  
  
    > [!NOTE]
    >  대상 서버 DVD에서 부팅 되지 않고 컴퓨터를 다시 시작 하 고 되도록 BIOS 설정 확인 **DVD-ROM** 먼저 부팅 순서 대로 나열 됩니다. BIOS 설정 부팅 순서를 변경 하는 방법에 대 한 자세한 내용은 하드웨어 제조업체의 설명서를 참조 합니다.  
  
2.  클릭 **새로 설치**합니다.  
  
3.  목록에 표시 되지 않는 한 내장 하드 드라이브를 사용 하는 경우 클릭 **드라이버 로드** 계속 하기 전에 필요한 드라이버를 설치 하 고 있습니다.  
  
4.  파일을 모두 확인 하는 확인란을 선택 하 고 기본 하드 드라이브에는 폴더를 삭제 되 고 클릭 한 다음 **설치**합니다.  
  
5.  에 **선택 서버 설치 모드** 페이지, 클릭 **서버 마이그레이션**, 마이그레이션 필요한 정보를 제공 합니다.  
  
6.  때는 **서버 성공적으로 마이그레이션** 클릭 메시지가 나타나면 **닫기**합니다.  
  
 설치가 완료 된 후 자동으로 로그온 관리자가 사용자 계정 및 암호 마이그레이션 응답 파일에 제공 합니다.  
  
> [!NOTE]
>  Windows Server Essentials를 설치 하는 동안 바탕 화면 잠금 해제를 기본 관리자 계정을 사용 하 고 암호를 비워 두고 있습니다.  
  
##  <a name="BKMK_VerifyTheHealthOfDC"></a>도메인 컨트롤러의 상태를 확인  
 마이그레이션을 계속 하기 전에 도메인 컨트롤러 및 Windows Server Essentials 네트워크 건강 지 확인 해야 합니다.  
  
 다음 표에서 대상 서버 및 네트워크에 및 도메인에 있는 문제를 진단 하는 데 사용할 수 있는 도구:  
  
|도구|설명|  
|----------|-----------------|  
|Netdiag|도움이는 네트워킹 및 연결 문제를 분리합니다. 표시 되는 자세한 정보 및 다운로드를 [Netdiag](https://go.microsoft.com/fwlink/?LinkId=217388)합니다.|  
|Dcdiag.exe|엔터프라이즈에 도메인 컨트롤러의 상태를 분석 하 고 문제 해결에 도움이 되는 문제를 보고 합니다. 표시 되는 자세한 정보 및 다운로드를 [Dcdiag](https://go.microsoft.com/fwlink/?LinkId=217389)합니다.|  
|Repadmin.exe|사용자 도메인 컨트롤러 간의 복제 문제 진단에 도움이 됩니다. 이 도구를 실행 하려면 명령줄 매개 변수 필요 합니다. 표시 되는 자세한 정보 및 다운로드를 [Repadmin](https://go.microsoft.com/fwlink/?LinkId=217387)합니다.|  
  
 마이그레이션 하기 전에 이러한 도구 보고서를 진행 하는 모든 문제를 해결 해야 합니다.  
  
> [!NOTE]
>  메일 다른 온-프레미스 Exchange server를 마이그레이션해야 하려는 경우 [Windows Server Essentials 온-프레미스 Exchange Server 부합](../manage/Integrate-an-On-Premises-Exchange-Server-with-Windows-Server-Essentials.md) 온-프레미스 Exchange server를 설정 하는 방법에 대 한 내용은 합니다.
