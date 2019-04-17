---
title: "Windows Server Essentials 로그 컬렉터 사용 하 여"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c6985518-b42d-4cfb-9761-eaa75306b6d7
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: d003c6a45159548f7e34d86ca242f74868659d2f
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="use-the-windows-server-essentials-log-collector"></a>Windows Server Essentials 로그 컬렉터 사용 하 여

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

컴퓨터 문제를 해결할 때 Microsoft 고객 서비스 및 지원 담당자 서버, 컴퓨터에는 네트워크에 또는 Windows Server Essentials 로그 수집기를 사용 하 여 둘 다에서 로그를 수집 요청할 수도 있습니다.  
  
 로그 수집기 프로그램 로그, 이벤트 검토자 로그 및 관련된 환경 정보 지정된 위치에 단일 zip 파일에 복사합니다. 컴퓨터에서 원격 연결을 사용 하 여 네트워크를 켜거나 서버 또는 된 컴퓨터에서 직접 로그 수집기를 실행할 수 있습니다.  
  
> [!NOTE]
>  -   로그 수집기 네트워크 문제를 분석 되지 않거나 서버 또는 네트워크에서 컴퓨터를 변경 합니다. 네트워크 문제를 해결 하는 방법에 대 한 정보에 대 한 서버 제품에 대 한 도움말 설명서를 참조 하세요.  
> -   이 가이드에서는 서버에 아닌 네트워크에서 컴퓨터 네트워크 컴퓨터 라고 합니다.  
> -   [Windows Server Essentials 로그 수집기 설치 패키지를 다운로드](https://go.microsoft.com/fwlink/?LinkID=266341)합니다.  
  
 설치 하 고 로그 수집기 실행 하려면 다음 항목의 단계를 수행 합니다.  
  

1.  [로그 수집기 설치](Install-the-Windows-Server-Essentials-Log-Collector.md)  
  
2.  [로그 수집기 실행](Run-the-Windows-Server-Essentials-Log-Collector.md)  

1.  [로그 수집기 설치](../support/Install-the-Windows-Server-Essentials-Log-Collector.md)  
  
2.  [로그 수집기 실행](../support/Run-the-Windows-Server-Essentials-Log-Collector.md)  

  
## <a name="environment-information-collected"></a>환경 정보 수집된  
 각 네트워크 컴퓨터 또는 사용자 지정 하는 서버에 대 한 로그 수집기 다음 환경을 정보를 수집 하 고 로그 컬렉션 파일에 저장 합니다.  
  
-   운영 체제 버전  
  
-   CPU 제조업체 및 설명  
  
-   메모리 양 및 할당  
  
-   TCP/IP에 연결 된 네트워크 어댑터  
  
-   로캘  
  
-   프로세스  
  
-   저장소 구성  
  
-   호스트 파일 정보  
  
-   이벤트 로그 응용 프로그램, 시스템, Windows Server 및 Media Center를 포함 하 여  
  
-   서비스를 제어 관리자 메시지  
  
-   Windows 업데이트 이벤트와 재부팅  
  
-   시스템 오류 및 응용 프로그램 오류  
  
## <a name="services-information-collected"></a>수집 된 정보를 서비스  
  
### <a name="server-services"></a>서버 서비스  
  
-   Windows Server 클라이언트 컴퓨터 백업 서비스  
  
-   Windows Server 클라이언트 컴퓨터 백업 공급자 서비스  
  
-   Windows Server 디바이스 공급자  
  
-   Windows Server 도메인 이름 관리  
  
-   Windows Server 서비스 공급자 레지스트리  
  
-   Windows Server 설정 공급자  
  
-   Windows Server UPnP 디바이스 서비스  
  
-   Windows Server 원격 웹 액세스 관리 공급자  
  
-   Windows Server Health 서비스  
  
-   Windows Server 저장소 서비스  
  
-   Windows Server SQM 서비스  
  
### <a name="network-computer-services"></a>네트워크 컴퓨터 서비스  
  
-   Windows Server 클라이언트 컴퓨터 백업 공급자 서비스  
  
-   Windows Server Health 서비스  
  
-   Windows Server 서비스 공급자 레지스트리  
  
-   Windows Server SQM 서비스  
  
## <a name="logs-and-registry-information-collected"></a>로그 및 레지스트리 정보 수집된  
 각 네트워크 컴퓨터 또는 지정한 서버에 대 한 로그 수집기 정보를 수집 로그 및 레지스트리 서버 및 네트워크 컴퓨터에서 다음과 같이 합니다.  
  
### <a name="server-logs-and-registry-information"></a>서버 로그 및 레지스트리 정보  
  
-   < ProgramData\ > \Microsoft\Windows Server\Logs부터 서버 제품 로그를  
  
-   예약된 작업  
  
-   설치 API 로그  
  
-   Windows 업데이트 기록  
  
-   건강 경고 파일  
  
-   장치 정보 파일  
  
-   서버 백업을 로그 파일  
  
-   표범 로그 파일  
  
-   서비스  
  
-   레지스트리 키에서  
  
    -   \\\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\  
  
    -   \\\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\DevicesProviderSvc  
  
    -   \\\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\DomainManagerProviderSvc  
  
### <a name="network-computer-logs-and-registry-information"></a>네트워크 컴퓨터 로그 및 레지스트리 정보  
  
-   네트워크 컴퓨터 제품 로그 < ProgramData\ > \Microsoft\Windows Server\Logs에서  
  
-   < ProgramData\ > \Microsoft\Windows Server\Data 건강 경고 파일  
  
-   Windows 업데이트 기록  
  
-   설치 API 로그  
  
-   예약 된 작업이 정보  
  
-   \\\HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\Windows Server\ 레지스트리 키  
  
## <a name="logs-for-computers-that-do-not-run-a-version-of-the-windows-operating-system"></a>Windows 운영 체제의 버전을 실행 하지 않는 컴퓨터에 대 한 로그  
 로그 수집기 Windows 운영 체제의 버전을 실행 하지 않는 컴퓨터에서 로그 파일 수집 하지 않습니다. 비 Windows 컴퓨터에 대 한 로그 컬렉터 파일을 저장할 위치를 수동으로 로그 파일을 복사 합니다.  
  
-   System.log  
  
-   라이브러리/로그 Windows Server.log  
  
-   라이브러리/로그/CrashReporter/실행 패드-< nnn\ > (실행 패드-> nnn\ <.crash 파일을 모두 복사)  
  
-   라이브러리/로그/DiagnosticReports/실행 패드-< nnn\ > (실행 패드-> nnn\ <.crash 파일을 모두 복사)  
  
## <a name="see-also"></a>참조 하십시오  
  

-   [로그 수집기 오류 문제 해결](Troubleshoot-Windows-Server-Essentials-Log-Collector-Errors.md)

-   [로그 수집기 오류 문제 해결](../support/Troubleshoot-Windows-Server-Essentials-Log-Collector-Errors.md)

