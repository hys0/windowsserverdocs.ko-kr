---
title: Migration mode1에서 Windows Server Essentials 설치
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: fd7196ac-cfa6-46a5-ba77-6962b47a825e
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 977922d8f2af23afc058162e7455ac5099e4325b
ms.sourcegitcommit: 2f072c0c02e3e0deae331ca64b375d63b89d0522
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2020
ms.locfileid: "83404562"
---
# <a name="install-windows-server-essentials-in-migration-mode1"></a>Migration mode1에서 Windows Server Essentials 설치

>적용 대상: Windows Server 2012 Essentials

네트워크에는 Windows Server Essentials를 실행 하는 서버가 하나만 있을 수 있으며 해당 서버는 네트워크에 대 한 도메인 컨트롤러 여야 합니다.  
  
 마이그레이션 모드에서 Windows Server Essentials를 설치 하면 설치 마법사에서 다음 작업을 수행 합니다.  
  
1.  대상 서버에 Windows Server Essentials 서버 소프트웨어를 설치 하 고 구성 합니다.  
  
2.  도메인 스키마를 최신 버전으로 업데이트합니다.  
  
3.  대상 서버를 기존 도메인에 가입시킵니다. 원본 서버와 대상 서버는 모두 마이그레이션 프로세스가 완료될 때까지 같은 도메인의 구성원이 될 수 있습니다. 마이그레이션이 완료되고 나면 21일 내에 네트워크에서 원본 서버를 제거해야 합니다.  
  
    > [!WARNING]
    >  네트워크에서 원본 서버를 제거할 때까지 21일 유예 기간에 매일 오류 메시지가 이벤트 로그에 추가됩니다. 메시지 텍스트의 내용은 다음과 같습니다. "FSMO 역할 검사 중에 사용자의 환경에서 라이선스 정책을 준수하지 않는 조건을 감지했습니다. 관리 서버는 주 도메인 컨트롤러 및 도메인 명명 마스터 Active Directory 역할을 보유하고 있어야 합니다. 지금 Active Directory 역할을 관리 서버로 이동하세요. 이 조건이 처음 감지된 시간으로부터 21일 내에 문제가 해결되지 않으면 이 서버가 자동으로 종료됩니다." 21일 유예 기간 이후에 원본 서버가 종료됩니다.  
  
4.  작업 마스터(FSMO(Flexible Single Master Operations)라고도 함) 역할을 원본 서버에서 대상 서버로 이전합니다. 작업 마스터 역할은 특수화된 도메인 컨트롤러 작업으로서 표준 데이터 전송 및 업데이트 방법이 적합하지 않을 때 이용됩니다. 대상 서버가 도메인 컨트롤러가 되면 작업 마스터 역할을 가져야 합니다.  
  
5.  대상 서버를 글로벌 카탈로그 서버로 구성합니다. 글로벌 카탈로그 서버는 분산 데이터 리포지토리를 관리하는 도메인 컨트롤러입니다. 여기에는 Active Directory 포리스트의 모든 도메인에서 각 개체에 대한 검색 가능한 부분적 표현이 포함됩니다.  
  
6.  대상 서버를 사이트 라이선스 서버로 구성합니다.  
  
##  <a name="install-windows-server-essentials-on-the-destination-server"></a><a name="BKMK_Install"></a>대상 서버에 Windows Server Essentials 설치  
 마이그레이션 모드에서 대상 서버에 Windows Server Essentials를 설치 및 구성 하려면 다음 절차를 수행 합니다.  
  
#### <a name="to-install-windows-server-essentials-on-the-destination-server"></a>대상 서버에 Windows Server Essentials를 설치 하려면  
  
1. 대상 서버를 설정 하 고 Windows Server Essentials DVD1을 DVD 드라이브에 삽입 합니다. CD 또는 DVD에서 부팅할지 묻는 메시지가 표시되면 아무 키나 눌러 작업을 진행합니다.  
  
   > [!NOTE]
   >  대상 서버에서 USB 플래시 드라이브의 부팅을 지원 하면 **windows 7 USB/DVD 다운로드 도구** 를 사용 하 여 Windows SERVER Essentials ISO 파일에서 부팅 가능한 usb 플래시 드라이브를 만들 수 있습니다. USB 플래시 드라이브를 사용하면 플래시 드라이브가 DVD-ROM 드라이브보다 훨씬 더 빠르게 데이터를 읽으므로 설치 프로세스 속도를 크게 높일 수 있습니다. 부팅 가능 USB 플래시 드라이브를 만들고 나서 플래시 드라이브에 응답 파일을 추가할 수 있습니다. Microsoft Store 웹 사이트에서 [Windows 7 USB/DVD 다운로드 도구를 무료로 다운로드할](https://go.microsoft.com/fwlink/p/?LinkId=248282) 수 있습니다.  
  
   > [!NOTE]
   >  대상 서버가 DVD에서 부팅되지 않으면 컴퓨터를 다시 시작하고 BIOS 설정에서 **DVD-ROM**이 부팅 시퀀스에서 첫 번째로 나열되어 있는지 확인합니다. BIOS 설정 부팅 시퀀스를 변경하는 방법에 대한 자세한 내용은 하드웨어 제조업체의 설명서를 참조하세요.  
  
2. **새로 설치**를 클릭합니다.  
  
3. 목록에 표시되지 않는 내부 하드 드라이브에 있으면 **드라이버 로드**를 클릭하고 계속하기 전에 필요한 드라이버를 설치합니다.  
  
4. 기본 하드 드라이브의 모든 파일과 폴더가 삭제되도록 확인하는 확인란을 선택하고 **설치**를 클릭합니다.  
  
5. **서버 설치 모드 선택** 페이지에서 **서버 마이그레이션**을 클릭하고 필요한 마이그레이션 정보를 제공합니다.  
  
6. **서버를 마이그레이션했습니다.** 메시지가 표시되면 **닫기**를 클릭합니다.  
  
   설치가 완료되고 나면 마이그레이션 응답 파일에 제공한 관리자 사용자 계정 및 암호를 사용하여 자동으로 로그온됩니다.  
  
> [!NOTE]
>  Windows Server Essentials가 설치 되는 동안 데스크톱을 잠금 해제 하려면 기본 제공 관리자 계정을 사용 하 고 암호를 비워 둡니다.  
  
##  <a name="verify-the-health-of-the-domain-controller"></a><a name="BKMK_VerifyTheHealthOfDC"></a>도메인 컨트롤러의 상태를 확인 합니다.  
 마이그레이션을 진행 하기 전에 도메인 컨트롤러 및 Windows Server Essentials 네트워크가 정상 상태 인지 확인 해야 합니다.  
  
 다음 표에는 대상 서버, 네트워크 및 도메인에서 문제를 진단하는 데 사용할 수 있는 도구가 나와 있습니다.  
  
|도구|Description|  
|----------|-----------------|  
|Netdiag|네트워킹 및 연결 문제를 격리하도록 도와줍니다. 자세한 내용을 보고 다운로드하려면 [Netdiag](https://go.microsoft.com/fwlink/?LinkId=217388)를 참조하세요.|  
|Dcdiag.exe|포리스트 또는 엔터프라이즈의 도메인 컨트롤러 상태를 분석하고 문제를 보고하여 문제 해결을 지원합니다. 자세한 내용을 보고 다운로드하려면 [Dcdiag](https://go.microsoft.com/fwlink/?LinkId=217389)를 참조하세요.|  
|Repadmin.exe|도메인 컨트롤러 간의 복제 문제를 진단하도록 도와줍니다. 이 도구를 실행하려면 명령줄 매개 변수가 필요합니다. 자세한 내용을 보고 다운로드하려면 [Repadmin](https://go.microsoft.com/fwlink/?LinkId=217387)을 참조하세요.|  
  
 마이그레이션을 진행하기 전에 이러한 도구에서 보고하는 모든 문제를 해결해야 합니다.  
  
> [!NOTE]
>  다른 온-프레미스 Exchange server로 메일을 마이그레이션하려는 경우 온-프레미스 exchange server를 설정 하는 방법에 대 한 자세한 내용은 온- [프레미스 exchange server와 Windows Server Essentials 통합](../manage/Integrate-an-On-Premises-Exchange-Server-with-Windows-Server-Essentials.md) 을 참조 하세요.
