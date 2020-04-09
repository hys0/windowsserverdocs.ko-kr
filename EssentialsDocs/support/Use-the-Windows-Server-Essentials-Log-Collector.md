---
title: Windows Server Essentials 로그 수집기 사용
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: c6985518-b42d-4cfb-9761-eaa75306b6d7
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: fa7ad24eec7c2732ee1c840aae678e3b0bff768c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80852166"
---
# <a name="use-the-windows-server-essentials-log-collector"></a>Windows Server Essentials 로그 수집기 사용

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

컴퓨터 문제를 해결할 때 Microsoft 고객 서비스 및 지원 담당자의 담당자가 Windows Server Essentials 로그 수집기를 사용 하 여 서버, 네트워크의 컴퓨터 또는 둘 다에서 로그를 수집 하도록 요청할 수 있습니다.  
  
 로그 수집기에서는 프로그램 로그, 이벤트 검토자 로그 및 관련된 환경 정보를 지정된 위치의 단일 zip 파일로 복사합니다. 컴퓨터에 대한 원격 연결을 사용하거나 서버 또는 네트워크의 컴퓨터에서 직접 로그 수집기를 실행할 수 있습니다.  
  
> [!NOTE]
>로그 수집기에서는 네트워크 문제를 분석하거나 서버 또는 네트워크의 컴퓨터를 변경하지 않습니다. 네트워크 문제를 해결하는 방법에 대한 자세한 내용은 서버 제품에 대한 도움말 문서를 참조하세요.  
>이 가이드에서는 서버가 아닌 네트워크의 컴퓨터를 네트워크 컴퓨터 라고 합니다.  
>
>[Windows Server Essentials 로그 수집기 설치 패키지를 다운로드](https://www.microsoft.com/download/details.aspx?id=34821)합니다.  
  
 로그 수집기를 설치 및 실행하려면 다음 항목의 단계를 수행합니다.  
  

1. [로그 수집기 설치](Install-the-Windows-Server-Essentials-Log-Collector.md)  
  
2. [로그 수집기 실행](Run-the-Windows-Server-Essentials-Log-Collector.md)  

3. [로그 수집기 설치](../support/Install-the-Windows-Server-Essentials-Log-Collector.md)  
  
4. [로그 수집기 실행](../support/Run-the-Windows-Server-Essentials-Log-Collector.md)  


## <a name="environment-information-collected"></a>수집된 환경 정보  
 로그 수집기에서는 지정되는 각 네트워크 컴퓨터 또는 서버에 대해 다음 환경 정보를 수집하고 로그 컬렉션 파일에 저장합니다.  
  
-   운영 체제 버전  
  
-   CPU 제조업체 및 설명  
  
-   메모리 양 및 할당  
  
-   TCP/IP에 바인딩되어 있는 네트워크 어댑터  
  
-   로캘  
  
-   프로세스  
  
-   저장소 구성  
  
-   호스트 파일 정보  
  
-   응용 프로그램, 시스템, Windows Server 및 미디어 센터를 포함한 이벤트 로그  
  
-   서비스 제어 관리자 메시지  
  
-   다시 부팅 이벤트 및 Windows 업데이트 이벤트  
  
-   시스템 오류 및 응용 프로그램 오류  
  
## <a name="services-information-collected"></a>수집된 서비스 정보  
  
### <a name="server-services"></a>서버 서비스  
  
-   Windows Server Client Computer Backup Service  
  
-   Windows Server Client Computer Backup Provider Service  
  
-   Windows Server 장치 공급자  
  
-   Windows Server 도메인 이름 관리  
  
-   Windows Server 서비스 공급자 레지스트리  
  
-   Windows Server 설정 공급자  
  
-   Windows Server UPnP 장치 서비스  
  
-   Windows Server 원격 웹 액세스 관리 공급자  
  
-   Windows Server 상태 관리 서비스  
  
-   Windows Server Storage Service  
  
-   Windows Server SQM 서비스  
  
### <a name="network-computer-services"></a>네트워크 컴퓨터 서비스  
  
-   Windows Server Client Computer Backup Provider Service  
  
-   Windows Server 상태 관리 서비스  
  
-   Windows Server 서비스 공급자 레지스트리  
  
-   Windows Server SQM 서비스  
  
## <a name="logs-and-registry-information-collected"></a>수집된 로그 및 레지스트리 정보  
 로그 수집기에서는 다음과 같이 지정된 각 네트워크 컴퓨터 또는 서버에 대한 로그 및 레지스트리 정보를 서버 및 네트워크 컴퓨터에서 수집합니다.  
  
### <a name="server-logs-and-registry-information"></a>서버 로그 및 레지스트리 정보  
  
-   서버 제품 로그, < ProgramData\>\Microsoft\Windows Server\Logs  
  
-   예약형 작업  
  
-   설치 API 로그  
  
-   Windows 업데이트 로그  
  
-   상태 경고 파일  
  
-   장치 정보 파일  
  
-   서버 백업 로그 파일  
  
-   Panther 로그 파일  
  
-   서비스  
  
-   레지스트리 키, 위치:  
  
    -   \\\ HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\Windows Server \  
  
    -   \\\ HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Services\DevicesProviderSvc  
  
    -   \\\ HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Services\DomainManagerProviderSvc  
  
### <a name="network-computer-logs-and-registry-information"></a>네트워크 컴퓨터 로그 및 레지스트리 정보  
  
-   < ProgramData\>\Microsoft\Windows Server\Logs에서 네트워크 컴퓨터 제품 로그  
  
-   상태 경고 파일 < ProgramData\>\Microsoft\Windows Server\Data  
  
-   Windows 업데이트 로그  
  
-   설치 API 로그  
  
-   예약형 작업 정보  
  
-   \\\ HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\Windows Server의 레지스트리 키 \  
  
## <a name="logs-for-computers-that-do-not-run-a-version-of-the-windows-operating-system"></a>Windows 운영 체제 버전을 실행하지 않는 컴퓨터에 대한 로그  
 로그 수집기에서는 Windows 운영 체제 버전을 실행하지 않는 컴퓨터에서 로그 파일을 수집하지 않습니다. 비 Windows 컴퓨터의 경우 로그 수집기 파일을 저장하는 동일한 위치에 다음 로그 파일을 복사합니다.  
  
-   System.log  
  
-   Library/Logs/Windows Server.log  
  
-   Library/Logs/CrashReporter/실행 패드-< nnn\> (모든 실행 패드-< nnn\>파일)를 복사 합니다.  
  
-   Library/Logs/DiagnosticReports/실행 패드-< nnn\> (모든 실행 패드-< nnn\>파일)를 복사 합니다.  
  
## <a name="see-also"></a>참고 항목  
  

-   [로그 수집기 오류 문제 해결](Troubleshoot-Windows-Server-Essentials-Log-Collector-Errors.md)

-   [로그 수집기 오류 문제 해결](../support/Troubleshoot-Windows-Server-Essentials-Log-Collector-Errors.md)

