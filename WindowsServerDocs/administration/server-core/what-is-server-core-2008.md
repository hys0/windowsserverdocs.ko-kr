---
title: Server Core 2008 란?
description: Windows Server 2008의 Server Core 설치 옵션에 알아봅니다
ms.prod: windows-server-threshold
ms.author: helohr
ms.date: 11/01/2017
ms.topic: article
author: Heidilohr
ms.openlocfilehash: c1ef71dbc589cfdeac63b46d720c4bdd0a44dbaa
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59815404"
---
#<a name="what-is-server-core-2008"></a>Server Core 2008 란?
>적용 대상: Windows Server 2008

>[!NOTE]
>이 정보는 Windows Server 2008에 적용 됩니다. Windows Server의 Server Core에 대 한 정보를 참조 하세요 [Windows Server의 Server Core 설치를 란](https://docs.microsoft.com/windows-server/administration/server-core/what-is-server-core)합니다. 

Server Core 옵션에는 Windows Server 2008 Standard, Enterprise 또는 Datacenter edition을 배포 하는 경우 사용할 수 있는 새로운 최소한의 설치 옵션이입니다. Server Core이이 장의 뒷부분에 설명 된 대로 하면 특정 서버 역할 설치를 지 원하는 Windows Server 2008의 최소 설치를 사용 하 여 제공 합니다. 모든 사용 가능한 서버 역할 및 다른 Microsoft 또는 타사 서버 응용 프로그램을 Microsoft Exchange Server 또는 SAP 설치를 지 원하는 Windows Server 2008 전체 설치 옵션을 사용 하 여이 대조해 보세요. 

본론으로 들어가기 전에 모든, "설치 옵션" 라는 문구를 설명 해야 합니다. 일반적으로 Windows Server 2008의 복사본을 구매 하면 특정 버전 또는 재고 관리 단위 (Sku)를 사용할 라이선스를 구입 합니다. 표 1-1 사용할 수 있는 다양 한 Windows Server 2008 버전을 나열 합니다. 또한 표에서 각 버전에 사용할 수 있는 설치 옵션 (전체, Server Core 또는 둘 다).

**표 1-1** Windows Server 2008 버전 및 설치 옵션에 대 한 지원을
| 버전       | 전체          | Server Core  |
| ------------- | :-------------: | :------------: |
| Windows Server 2008 Standard (x86 및 x64)       | X | X        |
| Windows Server 2008 Enterprise (x86 및 x64)       | X | X        |
| Windows Server 2008 Datacenter (x86 및 x64)        | X | X       |
| Windows Web Server 2008 (x86 및 x64)       | X | X  |
| Windows Server 2008 For itanium-based systems       | X |     |
| Windows HPC Server 2008 (x64만 해당)       | X |   |
| Windows Server 2008 Standard 하이퍼-V 불포함 (x86 및 x64) | X | X |
| Windows Server 2008 Enterprise 하이퍼-V 불포함 (x86 및 x64)  | X | X |
| Windows Server 2008 Standard 하이퍼-V 불포함 (x86 및 x64) | X | X |

작업을 이해 하려면 "설치 옵션" 인 Windows Server 2008 Enterprise Edition의 복사본을 설치할 수 있는 볼륨 라이선스를 구입한를 가정해 보겠습니다. 시스템에 볼륨 라이선스 미디어를 삽입 하 고 그림 1-1에 나와 있는 것 처럼 보게 되겠지만 화면 중 하나로 설치 프로세스를 시작 하는 경우 다양 한 버전 및 설치 옵션을 사용 하 여 제공 합니다.

![설치 하는 Server Core 설치 옵션 선택](../media/what-is-server-core-2008/FIg1-1.png)

**그림 1-1** 설치 하는 Server Core 설치 옵션 선택

그림 1-1, 볼륨 라이선스 (또는 일반 정품 미디어에 대 한 제품 키) 사용 하면 두 가지 설치 옵션 중에서 선택할 수 있습니다: 두 번째 옵션 (을 전체 설치의 Windows Server 2008 Enterprise) 및 다섯 번째 옵션 (한 Server Core 설치의 Windows Server 2008 Enterprise의 경우)이이 예제에서 선택한 후자를 사용 하 여 합니다. 

##<a name="full-vs-server-core"></a>완전 트랜잭션 내구성과 Server Core 
Microsoft Windows 플랫폼의 초기 시절 Windows 서버 된 기본적으로 "모든" 기능을 일부는 사용할 수 있습니다 실제로 네트워킹 환경에서 모든 종류를 포함 하는 서버입니다. 예를 들어 시스템에서 Windows Server 2003을 설치할 때 라우팅 및 원격 액세스 서비스 (RRAS)에 대 한 이진 파일 설치 된 서버에서이 서비스에 대 한 필요가 없습니다 (하지만 여전히 구성 하 고 작동 하는 전에 RRAS를 사용 하도록 설정 해야) 해야 하는 경우에 합니다. Windows Server 2008 서버에서 해당 역할을 설치 하도록 선택한 경우에 서버 역할에 따라 필요한 이진 파일을 설치 하 여 이전 버전을 개선 합니다. 그러나 Windows Server 2008 전체 설치 옵션을 여러 서비스 및 기타 구성 요소를 특정 사용 시나리오에 필요한 수 없는 경우가 많습니다 계속 설치 합니다. 

Microsoft는 두 번째 설치 옵션을 생성 하는 이유는-Server Core-Windows Server 2008: 일반적으로 사용 되는 서버 역할의 특정 지원이 반드시 필요 하지 않은 다른 기능과 서비스를 제거 하려면. 예를 들어, 도메인 이름 시스템 (DNS) 서버를 실제로 필요 하지 않습니다 보안상의 이유로 DNS 서버에서 웹 사이트를 탐색 하려고 하기 때문에 설치 된 Windows Internet Explorer. DNS 서버를 그래픽 사용자 인터페이스 (GUI)도 필요 하지 않습니다, 그리고 DNS의 거의 모든 측면을 관리할 수 때문에 강력한 Dnscmd.exe 명령을 사용 하거나 DNS Microsoft Management Console (MMC)를 사용 하 여 명령줄에서 스냅인.

이 방지 하려면 Microsoft Active Directory Domain Services (AD DS), DNS, 동적 호스트 구성 프로토콜 (DHCP), 파일 및 인쇄와 같은 핵심 네트워크 서비스를 실행 하는 데 반드시 필요 하지는 Windows Server 2008의 모든 항목을 제거 하기로 및 다른 몇 가지 서버 역할입니다. 결과 새로운 Server Core 설치 옵션을 제한 된 수의 역할 및 기능을 지 원하는 서버를 만드는 데 사용할 수 있습니다. 

##<a name="the-server-core-gui"></a>Server Core GUI
처음에 대 한 시스템 및 로그온에 Server Core 설치를 완료 하면 관심이 다소의 외에 대 한 합니다. 그림 1-2 첫 번째 로그온 후 Server Core 사용자 인터페이스를 보여 줍니다.

![Server Core 사용자 인터페이스](../media/what-is-server-core-2008/Fig1-2.png)

**그림 1-2** Server Core 사용자 인터페이스

바탕 화면이 나타나지 않았습니다! 즉, 해당 시작 메뉴, 작업 표시줄 및 보는 데 사용할 수 있습니다 다른 기능을 사용 하 여 Windows 탐색기 셸이 없기 있습니다. 사용자 구성 단순화 및 속도 하나를 사용 하거나 스크립트와 도움이 되는 배치 파일을 사용 하 여 느린가 한 번에 명령을 입력 하 여 하나 대부분의 Server Core 설치를 구성 하는 작업을 수행 해야 한다는 것을 의미 하는 명령 프롬프트 됩니다. 이러한 자동화 하 여 작업 합니다. 또한 Server Core의 무인된 설치를 수행 하면 응답 파일을 사용 하 여 일부 초기 구성 작업을 수행할 수 있습니다. 

Netsh.exe, Dfscmd.exe, 등 Dnscmd.exe 명령줄 도구를 사용 하 여 전문가 인 관리자를 구성 하 고 Server Core 설치 관리 편리 하 고 재미도 될 수 있습니다. 그러나 사용자에 게는 전문가가, 모든 손실 되지 않습니다. Server Core 설치 관리에 대 한 표준 Windows Server 2008 MMC 도구를 계속 사용할 수 있습니다. 서비스 팩 1을 사용 하 여 Windows Server 2008 전체 설치 또는 Windows Vista를 실행 하는 다른 시스템에서이 크레딧을 사용 하기만 하면 됩니다. 

구성 하 고 나머지 장에서 특정 서버 역할 및 기타 구성 요소를 관리 하는 방법으로 처리 하는 동안에 장 3 ~ 6이이 책의 Server Core 설치를 관리 하는 방법에 대 한 자세히 알아봅니다. 다양 한 Windows 명령줄 도구 및 사용 하는 방법에 대 한 자세한 내용은 두 가지 좋은 리소스가 있습니다을 참조 하십시오.
* Windows Server 2008 기술 라이브러리 () 명령 참조 섹션 
* *Windows 명령줄 Administrator's Pocket Consultant* William R. Stanek (Microsoft Press, 2008)에서 

표 1-2는 Server Core 설치에서 사용할 수 있는 해당 실행 개체와 함께 기본 GUI 응용 프로그램을 나열 합니다.

**표 1-2** Server Core 설치에서 사용할 수 있는 GUI 응용 프로그램
| GUI 응용 프로그램 | 경로 사용 하 여 실행 파일 |
| -------------   | -------------       | 
| 명령 프롬프트 | %WINDIR%\System32\Cmd.exe |
| Microsoft 지원 진단 도구 | %WINDIR%\System32\MSdt.exe |
| Windows 메모장 | %WINDIR%\System32\Notepad.exe |
| 레지스트리 편집기 | %WINDIR%\System32\Regedt32.exe |
| 시스템 정보 | %WINDIR%\System32\MSinfo32.exe |
| 작업 관리자 | %WINDIR%\System32\Taskmgr.exe |
| Windows Installer | %WINDIR%\System32\MSiexec.exe |

매우 간단한 목록입니다. 이제 다음과 같습니다. Server Core에 포함 되지 않은 사용자 인터페이스 요소 목록
* Windows 탐색기 데스크톱 셸 (Explorer.exe) 및 테마와 같은 지원 기능 
* 모든 MMC 콘솔 
* 국가 및 언어 옵션 (Intl.cpl) 및 날짜 및 시간 (Timedate.cpl)를 제외 하 고 모든 Control Panel 유틸리티 
* Internet Explorer 및 HTML 도움말을 비롯 한 모든 (HTML) 렌더링 엔진 
* Windows Mail 
* Windows Media Player 
* 그리기, 계산기 및 워드 패드와 같은 대부분의 accessories

.NET Framework는 또한 즉, Server Core 설치에서 실행 중인 관리 코드에 대 한 지원은 Server Core에 없습니다. 네이티브 코드-Windows Api (응용 프로그래밍 인터페이스)를 사용 하 여 작성 된 코드-Server Core에서 실행할 수 있습니다. 요약 하자면,.NET Framework에 종속 된 모든 GUI 응용 프로그램 또는 Explorer.exe는 셸 Server Core에서 실행 되지 않습니다. 

>[!NOTE]
>Windows PowerShell에서.NET Framework를 필요로 하므로 Server Core에 Windows PowerShell을 설치할 수 없습니다. 그러나으로 PowerShell WMI 명령을 사용 하 여 Windows PowerShell을 사용 하 여 원격으로 Server Core 설치를 관리할 수 있습니다.

##<a name="supported-server-roles"></a>지원 되는 서버 역할 
Server Core 설치에는 제한 된 수의 Windows Server 2008 전체 설치와 비교 하는 서버 역할의 포함 됩니다. 표 1-3는 Windows Server 2008 Enterprise Edition의 전체 및 Server Core 설치에 사용 가능한 역할을 비교합니다. 

**표 1-3** Windows Server 2008 Enterprise Edition의 전체 및 Server Core 설치에 대 한 서버 역할의 비교
| 서버 역할  | 전체 설치에서 사용 가능  | Server Core에서 사용할 수 있습니다.  |
| ------------- | :-------------: | :------------: |
| AD CS(Active Directory 인증서 서비스)  | X |  |
| AD DS(Active Directory 도메인 서비스)  | X  | X |
| AD FS(Active Directory Federation Services)  | X  |  |
| AD LDS(Active Directory Lightweight Directory Services)  | X  | X |
| AD RMS(Active Directory Rights Management Services)  | X  |  |
| 응용 프로그램 서버  | X  |  |
| DHCP 서버  | X  | X |
| DNS 서버  | X  | X |
| 팩스 서버  | X  |  |
| 파일 서비스  | X  | X |
| Hyper-V  | X | X |
| 네트워크 정책 및 액세스 서비스  | X  |  |
| 인쇄 서비스  | X  | X |
| 스트리밍 미디어 서비스  | X  | X |
| 터미널 서비스  | X  |  |
| UDDI 서비스  | X  |  |
| 웹 서버(IIS) | X | X |
| Windows 배포 서비스  | X |  |

Server Core에 대 한 사용 가능한 역할은 일반적으로 아키텍처 (예: x86 또는 x64) 및 제품 버전에 관계 없이 동일한 이지만는 몇 가지 예외가 있습니다.
* Hyper-v (가상화) 역할은 Hyper-v 제품 미디어를 사용 하 여 Windows Server 2008을 구매 하는 경우에 사용할 수 있습니다 (Hyper-v는 x64에만 사용할 수 있는 버전). 이 역할에 필요 하지 않은 경우 대신 Windows Server 2008 Hyper-v 제품 미디어 없이 구입할 수 있습니다. 
* Standard Edition에 대 한 파일 서비스 역할을 하나의 독립 실행형 파일 시스템 (DFS (분산) 루트 제한 되며 Cross-File 복제 (Dfs-r) 지원 하지 않습니다. 
* Server Core에서 스트리밍 미디어 서비스 역할을 설치할 수 있습니다, 전에 해야 패키지 다운로드 및 설치는 적절 한 Microsoft 업데이트 독립 실행형 (.msu 파일) (x86 또는 x64) 서버의 아키텍처에 대 한 Microsoft 다운로드 센터에서 합니다.
* 웹 서버 (IIS) 역할에서 ASP.NET을 지원 하지 않습니다. 즉,.NET Framework는 Server Core 웹 서버를 사용 하 여 수행할 수 있는 작업을 제한 하는 Server core에서 지원 되지 않습니다. 

##<a name="supported-optional-features"></a>지원 되는 선택적 기능
Server Core 설치는 또한 Windows Server 2008 전체 설치에 사용할 수 있는 기능의 제한 된 하위 집합만 지원합니다. 표 1-4는 Windows Server 2008 Enterprise Edition의 전체 및 Server Core 설치에 사용할 수 있는 기능을 비교합니다.

**표 1-4** Windows Server 2008 Enterprise Edition의 전체 및 Server Core 설치에 대 한 기능 비교

| 기능  | 전체 설치에서 사용 가능  | Server Core에서 사용할 수 있습니다.  |
| ------------- | :-------------: | :------------: |
| .NET Framework 3.0 기능  | X  |  |
| BitLocker 드라이브 암호화  | X  | X |
| BITS 서버 확장  | X  |  |
| 연결 관리자 관리 키트  | X |  |
| 데스크톱 환경  | X |  |
| 장애 조치(failover) 클러스터링  | X  | X |
| 그룹 정책 관리  | X  |  |
| 인터넷 인쇄 클라이언트  | X  |  |
| 인터넷 저장소 이름 서버  | X  |  |
| LPR 포트 모니터  | X  |  |
| 메시지 큐  | X  |  |
| 다중 경로 IO  | X  | X |
| 네트워크 부하 분산  | X  | X |
| 피어 이름 확인 프로토콜  | X  |  |
| qWave(Quality Windows Audio Video Experience)  | X |  |
| 원격 지원  | X  |  |
| 원격 차등 압축 | X  |  |
| 원격 서버 관리 도구  | X  |  |
| 이동식 저장소 관리자 | X  | X |
| RPC Over HTTP 프록시 | X  |  |
| 단순 TCP/IP 서비스  | X  |  |
| SMTP 서버  | X  |  |
| SMNP 서비스  | X  | X  |
| 저장소 관리자에 대 한 San  | X  |  |
| UNIX 기반 응용 프로그램용 하위 시스템 | X | X  |
| 텔넷 클라이언트  | X | X  |
| 텔넷 서버  | X   |  |
| TFTP 클라이언트  | X   |  |
| Windows 내부 데이터베이스  | X  |  |
| Windows PowerShell  | X  |  |
| Windows 제품 정품 인증 서비스  | X   |  |
| Windows Server 백업 기능  | X  | X  |
| Windows 시스템 리소스 관리자  | X  |  |
| WINS 서버  | X | X |
| 무선 LAN 서비스 | X  |  |

다시 Server Core에 사용할 수 있는 기능에 관한 알아야 할 사항이 몇 가지:
* 일부 기능은 Server Core에 제대로 (또는 모든) 함수를 특수 한 하드웨어가 필요할 수 있습니다. 이러한 기능에는 BitLocker 드라이브 암호화, 장애 조치 클러스터링, 다중 경로 IO, 네트워크 부하 분산 및 이동식 저장소 포함 됩니다. 
* 장애 조치 클러스터링은 Standard Edition에서 사용할 수 없습니다.

##<a name="server-core-architecture"></a>Server Core 아키텍처
자세히 살펴보기 Server Core를 간단히 살펴보겠습니다 Windows Server 2008의 Server Core 설치의 아키텍처는 전체 설치와 비교 하 여 합니다. 먼저 Server Core 설치 옵션을 시스템에 Windows Server 2008을 설치할 때 선택할 수 있는 단순히 Windows Server 2008의 다른 버전이 아닙니다 해야 합니다. 이것은 다음을 의미합니다.
* Server Core 설치에서 커널 같은 동일한 하드웨어 아키텍처 (예: x86 또는 x64) 및 버전의 전체 설치에서 찾을 수입니다. 
* 이진 파일을 Server Core 설치에 있는 경우 동일한 하드웨어 아키텍처 (예: x86 또는 x64) 및 버전의 전체 설치에는 특정 이진 파일의 동일한 버전 (뒷부분에서 설명 하는 두 개의 예외) 포함 
* 해당 설정이 동일한 전체 설치에서 동일한 방식으로 정확 하 게 구성 되어 있으면 (예, 특정 방화벽 예외 또는 특정 서비스의 시작 유형)에 특정 설정을 특정 기본 구성을 Server Core 설치에서 (x86 또는 x64) 하드웨어 아키텍처 및 버전입니다.

그림 1-3에서는 전체 설치와 Windows Server 2008의 Server Core 설치의 아키텍처의 단순화 된 보기를 보여 줍니다. 점선 전체 다이어그램이 전체 설치의 아키텍처를 표시 하는 동안 Server Core의 아키텍처를 나타냅니다. 

다이어그램에서는 핵심 운영 체제 기능의 하위 집합으로 생성 되는 Server Core를 사용 하 여 Windows Server 2008의 모듈식 아키텍처를 보여 줍니다. 동일한 하드웨어 아키텍처 및 버전에 대 한 Server Core를 새로 설치할 때 모든 파일이 없는 전체 설치에서 Server Core에만 있는 두 개의 특수 파일 (Scregedit.wsf 및 Oclist.exe)를 제외 하 고 있는 이기도 합니다. 이러한 특수 한 파일은 Server Core 설치 및 추가의 초기 구성 또는 역할 및 선택적 구성 요소 제거를 간소화 하기 위해 Server Core에 포함 되었습니다. 

![Server Core 및 전체 설치의 아키텍처](../media/what-is-server-core-2008/Fig1-3.png)

**그림 1-3** Server Core 및 전체 설치의 아키텍처

##<a name="driver-support"></a>드라이버 지원
그림 1-3에서 표시 하는 Server Core의 아키텍처 다이어그램 분명히 간단 합니다. 표시 되지 않지만 것의 차이점은 장치 드라이버 지원에 Server Core 및 전체 설치 합니다. Windows Server 2008 전체 설치에는 수천 개의 다른 종류의 다양 한 다른 하드웨어 구성에 제품을 설치할 수 있도록 하는 장치에 대 한 기본 드라이버 포함 되어 있습니다. (Windows Vista 클라이언트 운영 체제는 디지털 카메라 및 서버를 사용 하 여 일반적으로 사용 되는 스캐너와 같은 장치를 지원 하기 위해 더 많은 드라이버를 포함 합니다.) 

새 장치에 연결 (인지에 설치 된)의 Windows Server 2008 전체 설치를 플러그 앤 플레이 (PnP) 하위 시스템은 먼저 있는지 여부를 장치에 대 한 기본 드라이버를가 있는지 확인 합니다. 호환 되는 기본 드라이버 있으면 PnP 하위 시스템은 자동으로 장치와 드라이버를 설치한 다음이 작동 합니다. Windows Server 2008 전체 설치에서 풍선 팝업 알림이 표시 될 수 있습니다, 드라이버 설치가 완료 된 후 장치가 사용할 준비가 되 고 나타내는입니다. 

Server Core 설치에서 드라이버 설치 프로세스 (PnP 하위 시스템은 Server Core에 있는)와 동일 두 한정자가 있는 합니다. 먼저 Server Core에만 최소한 기본 드라이버 및 다음과 같은 유형의 장치에 대해서만 포함 됩니다.
* 표준 비디오 그래픽 배열 (VGA) 비디오 드라이버 
* 저장소 장치에 대 한 드라이버 
* 네트워크 어댑터에 대 한 드라이버

여기에 표시 된 세 가지 장치 범주 각각에 대 한 Server Core 포함 (동일한 하드웨어 아키텍처)에 대 한 해당 전체 설치에 있는 동일한 기본 드라이버 note 합니다. 

또한 PnP 하위 시스템에서 새 장치에 대 한 드라이버를 자동으로 설치할 때는 자동으로-풍선 팝업 알림이 표시 되지 않습니다. 왜 안 돼요? 없기 때문에 GUI는 없습니다 Server Core에 없는 작업 표시줄을 작업 표시줄의 알림 영역이 죠! 

따라서 어떻게 해야 하나요 Server Core 설치에 인쇄 서비스 역할을 추가 하 고 프린터를 설치 하 시겠습니까? 프린터 드라이버를 수동으로 추가 하면 서버에, Server Core에 상자에서 인쇄 드라이버가 없습니다.

##<a name="service-footprint"></a>서비스 공간
Server Core 최소 설치 되므로, 동일한 하드웨어 아키텍처 및 버전을 해당 전체 설치 보다 적은 시스템 서비스 사용을 있습니다. 예를 들어, 약 75 대의 시스템 서비스는 약 50 자동으로 시작 되도록 구성 되는 Windows Server 2008 전체 설치에 기본적으로 설치 됩니다. 반면, Server Core에 자동으로 이러한 시작 40 개 미만의 기본적으로 설치 하는 약 70만 서비스가 있습니다. 

표 1-5의 시작 모드를 사용 하 여 Server Core 설치에서 기본적으로 설치 되는 서비스를 나열 하 고 각 서비스에서 사용 하는 계정 키를 누릅니다.

**표 1-5** 기본적으로 Server Core에 설치 하는 시스템 서비스

| 서비스 이름  | 표시 이름  | 시작 모드  | 계정  |
| ------------- | ------------- | ------------ | ------------ |
| AeLookupSvc  | 응용 프로그램 환경  | 자동 | LocalSystem |
| AppMgmt  | 응용 프로그램 관리  | 수동 | LocalSystem |
| BFE | 기본 필터링 엔진  | 자동 | LocalService |
| BITS | BITS(Background Intelligent Transfer Service)  | 자동 | LocalSystem |
| 브라우저 | 컴퓨터 브라우저  | 수동 | LocalSystem |
| CertPropSvc | 인증서 전파  | 수동 | LocalSystem |
| COMSysApp  | COM+ 시스템 응용 프로그램  | 수동 | LocalSystem |
| CryptSvc  | 암호화 서비스  | 자동 | Network-Service |
| DcomLaunch  | DCOM Server 프로세스 시작 관리자  | 자동 | LocalSystem |
| Dhcp  | DHCP 클라이언트  | 자동 | LocalService |
| 누릅니다 | DNS 클라이언트  | 자동 | Network-Service |
| DPS  | 진단 정책 서비스  | 자동 | LocalService |
| 이벤트 로그 | Windows 이벤트 로그  | 자동 | LocalService |
| EventSystem  | COM + 이벤트 시스템  | 자동 | LocalService |
| FCRegSvc  | Microsoft 파이버 채널 플랫폼 등록 서비스  | 수동 | LocalService |
| gpsvc  | 그룹 정책 클라이언트  | 자동 | LocalSystem |
| hidserv | 휴먼 인터페이스 장치 액세스  | 수동 | LocalSystem |
| hkmsvc  | 상태 키 및 인증서 관리  | 수동 | LocalSystem |
| IKEEXT  | IKE 및 AuthIP IPsec 키 지정 모듈  | 자동 | LocalSystem |
| iphlpsvc  | IP 도우미  | 자동 | LocalSystem |
| KeyIso | CNG 키 격리  | 수동 | LocalSystem |
| KtmRm  | DTC(Distributed Transaction Coordinator)용 KtmRm  | 자동 | Network-Service |
| LanmanServer  | 서버  | 자동 | LocalSystem |
| LanmanWorkstation  | Workstatione  | 자동 | LocalService |
| lltdsvc  | 연결 계층 토폴로지 검색 매퍼  | 수동 | LocalService |
| lmhosts  | TCP/IP NetBIOS Helper  | 자동 | LocalService |
| MpsSvc  | Windows 방화벽  | 자동 | LocalService |
| MSDTC  | DTC(Microsoft Distributed Transaction Coordinator)  | 자동 | Network-Service |
| MSiSCSI  | Microsoft iSCSI 초기자 서비스  | 수동 | LocalSystem |
| msiserver  | Windows Installer  | 수동 | LocalSystem |
| napagent  | 네트워크 액세스 보호 에이전트  | 수동 | Network-Service |
| Netlogon  | Netlogon  | 수동 | LocalSystem |
| netprofm  | 네트워크 목록 서비스  | 자동 | LocalService |
| NlaSvc  | 네트워크 위치 인식  | 자동 | Network-Service |
| nsi  | 네트워크 저장소 인터페이스 서비스  | 자동 | LocalService |
| pla  | 성능 로그 및 경고  | 수동 | LocalService |
| PlugPlay  | 플러그 앤 플레이  | 자동 | LocalSystem |
| PolicyAgent  | IPSec 정책 에이전트  | 자동 | Network-Service |
| ProfSvc  | 사용자 프로필 서비스  | 자동 | LocalSystem |
| ProtectedStorage  | 보호 된 저장소  | 수동 | LocalSystem |
| RemoteRegistry  | 원격 레지스트리  | 자동 | LocalService |
| RpcSs  | RPC(원격 프로시저 호출)  | 자동 | Network-Service |
| RSoPProv | 공급자 정책 결과 집합  | 수동 | LocalSystem |
| sacsvr  | 특수 관리 콘솔 도우미  | 수동 | LocalSystem |
| SamSs  | 보안 계정 관리자  | 자동 | LocalSystem |
| SCardSvr | 스마트 카드  | 수동 | LocalService |
| 일정 | 작업 스케줄러  | 자동 | LocalSystem |
| SCPolicySvc | 스마트 카드 제거 정책  | 수동 | LocalSystem |
| seclogon | 보조 로그온  | 자동 | LocalSystem |
| SENS | 시스템 이벤트 알림 서비스  | 자동 | LocalSystem |
| SessionEnv | 터미널 서비스 구성  | 수동 | LocalSystem |
| slsvc  | 소프트웨어 라이선스 | 자동 | Network-Service |
| SNMPTRAP  | SNMP 트랩  | 수동 | LocalService |
| swprv  | Microsoft 소프트웨어 섀도 복사본 공급자 | 수동 | LocalSystem |
| TBS | TPM 기본 서비스  | 수동 | LocalService |
| TermService  | 터미널 서비스 | 자동 | Network-Service |
| TrustedInstaller | Windows 모듈 설치 관리자  | 자동 | LocalSystem |
| UmRdpService | 터미널 서비스 UserMode 포트 리디렉터  | 수동 | LocalSystem |
| vds | 가상 디스크  | 수동 | LocalSystem |
| VSS | 볼륨 섀도 복사본  | 수동 | LocalSystem |
| W32Time | Windows 시간  | 자동 | LocalService |
| WcsPlugInService  | Windows 색 시스템  | 수동 | LocalService |
| WdiServiceHost  | 진단 서비스 호스트  | 수동 | LocalService |
| WdiSystemHost  | 진단 시스템 호스트  | 수동 | LocalSystem |
| Wecsvc | Windows 이벤트 수집기  | 수동 | Network-Service |
| WinHttpAuto-ProxySvc  | WinHTTP 웹 프록시 자동 검색 서비스  | 자동 | LocalService |
| Winmgmt | Windows Management Instrumentation | 자동 | LocalSystem |
| WinRM  | Windows Remote Management (Ws-management) | 자동 | Network-Service |
| wmiApSrv  | WMI Performance Adapter  | 수동 | LocalSystem |
| wuauserv | Windows 업데이트 | 자동 | LocalSystem |