---
title: Server Core 관리
description: Windows Server의 Server Core 설치를 관리 하는 방법에 알아봅니다.
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.author: elizapo
ms.localizationpriority: medium
ms.date: 12/18/2018
ms.openlocfilehash: 50fa737db5862132c1dde5cb6eb6b83674b3f02e
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66811390"
---
# <a name="administer-a-server-core-server"></a>Server Core 서버를 관리 합니다.

>적용 대상: Windows Server (반기 채널) 및 Windows Server 2016

Server Core UI가 때문에 기본 관리 작업을 수행 하려면 Windows PowerShell cmdlet, 명령줄 도구 또는 원격 도구를 사용 해야 합니다. 다음 섹션에서는 PowerShell cmdlet 및 기본 작업에 사용 되는 명령을 간략하게 설명 합니다. 사용할 수도 있습니다 [Windows Admin Center](../../manage/windows-admin-center/overview.md), 현재 공개 미리 보기로 제공, 설치를 관리 하는 통합된 관리 포털. 

## <a name="administrative-tasks-using-powershell-cmdlets"></a>PowerShell cmdlet을 사용 하 여 관리 작업
다음 정보를 사용 하 여 Windows PowerShell cmdlet 사용 하 여 기본 관리 작업을 수행 합니다.

### <a name="set-a-static-ip-address"></a>고정 IP 주소 설정
Server Core 서버를 설치할 때 기본적으로 것에 DHCP 주소가 있습니다. 고정 IP 주소를 해야 하는 경우 다음 단계를 사용 하 여 설정할 수 있습니다.

현재 네트워크 구성을 보려면 사용 하 여 **Get NetIPConfiguration**합니다.

이미 사용 중인 IP 주소를 보려면 사용 하 여 **Get NetIPAddress**합니다.

고정 IP 주소를 설정 하려면 다음을 수행 합니다. 

1. 실행할 **Get-netipinterface**합니다. 
2. 번호를 적어둡니다 합니다 **IfIndex** IP 인터페이스에 대 한 열 또는 **InterfaceDescription** 문자열입니다. 네트워크 어댑터가 둘 이상인 경우에 대 한 고정 IP 주소를 설정 하려면 인터페이스에 해당 하는 문자열의 수를 note 합니다.
3. 고정 IP 주소를 설정 하려면 다음 cmdlet을 실행 합니다.

   ```powershell
   New-NetIPaddress -InterfaceIndex 12 -IPAddress 192.0.2.2 -PrefixLength 24 -DefaultGateway 192.0.2.1
   ```

   각 항목이 나타내는 의미는 다음과 같습니다.
   - **InterfaceIndex** 값인 **IfIndex** 에서 2 단계. (이 예제에서는 12)의
   - **IPAddress** 설정 하려는 고정 IP 주소입니다. (예제의 191.0.2.2)
   - **PrefixLength** 접두사 길이 (서브넷 마스크의 또 다른 형태)을 설정 하 여 IP 주소입니다. (이 예에서는 24)에 대 한
   - **기본 게이트웨이** 기본 게이트웨이 IP 주소입니다. (이 예에서는 192.0.2.1)에 대 한
4. DNS 클라이언트 서버 주소를 설정 하려면 다음 cmdlet을 실행 합니다. 

   ```powershell
   Set-DNSClientServerAddress –InterfaceIndex 12 -ServerAddresses 192.0.2.4
   ```
   
   각 항목이 나타내는 의미는 다음과 같습니다.
   - **InterfaceIndex** 2 단계의 IfIndex의 값입니다.
   - **ServerAddresses** DNS 서버의 IP 주소입니다.
5. 여러 DNS 서버를 추가 하려면 다음 cmdlet을 실행 합니다. 

   ```powershell
   Set-DNSClientServerAddress –InterfaceIndex 12 -ServerAddresses 192.0.2.4,192.0.2.5
   ```

   이 예제에서는 where **192.0.2.4** 하 고 **192.0.2.5** 는 DNS 서버의 두 IP 주소입니다.

DHCP를 실행을 사용 하도록 전환 해야 하는 경우 **Set-dnsclientserveraddress – InterfaceIndex 12 – ResetServerAddresses**합니다.

### <a name="join-a-domain"></a>도메인 가입
컴퓨터를 도메인에 가입 하려면 다음 cmdlet을 사용 합니다.

1. 실행할 **Add-computer**합니다. 도메인 이름과 도메인에 조인할 두 자격 증명에 대 한 라는 메시지가 표시 됩니다.
2. 로컬 관리자 그룹에 도메인 사용자 계정을 추가 해야 할 경우 (PowerShell 창)에 없는 명령 프롬프트에서 다음 명령을 실행 합니다.

   ```
   net localgroup administrators /add <DomainName>\<UserName>
   ```
3. 컴퓨터를 다시 시작합니다. 실행 하 여 이렇게 **Restart-computer**합니다.

### <a name="rename-the-server"></a>서버 이름 바꾸기
서버 이름을 바꾸려면 다음 단계를 사용 합니다.

1. **hostname** 또는 **ipconfig** 명령으로 현재 서버 이름을 확인합니다.
2. 실행할 **Rename-computer-ComputerName \<new_name\>** 합니다.
3. 컴퓨터를 다시 시작합니다.

### <a name="activate-the-server"></a>서버 정품 인증

실행할 **slmgr.vbs – ipk\<productkey\>** 합니다. 그런 다음 실행 **slmgr.vbs – ato**합니다. 정품 인증에 성공 메시지가 표시 되지 않습니다.

> [!NOTE]
> 하 여 서버를 활성화할 수도 있습니다 전화를 사용 하는 [서비스 KMS (키 관리) 서버](../../get-started/server-2016-activation.md), 또는 원격으로 합니다. 원격으로 활성화 하려면 원격 컴퓨터에서 다음 cmdlet을 실행 합니다. 
> 
> ```powershell
> **cscript windows\system32\slmgr.vbs <ServerName> <UserName> <password>:-ato**
> ```
 
### <a name="configure-windows-firewall"></a>Windows 방화벽 구성

Windows PowerShell cmdlet 및 스크립트를 사용하여 Server Core 컴퓨터에서 로컬로 Windows 방화벽을 구성할 수 있습니다. 참조 [NetSecurity](/powershell/module/netsecurity/?view=win10-ps) Windows 방화벽을 구성 하 여 cmdlet에 대 한 합니다.

### <a name="enable-windows-powershell-remoting"></a>Windows PowerShell 원격 기능 사용

특정 컴퓨터의 Windows PowerShell에 입력된 명령을 또 다른 컴퓨터에서 실행하는 Windows PowerShell 원격 기능을 사용할 수 있습니다. Windows PowerShell 원격 기능을 사용 하도록 설정 **Enable-psremoting**합니다.

자세한 내용은 [원격 FAQ 정보](/powershell/module/microsoft.powershell.core/about/about_remote_faq?view=powershell-5.1)합니다.

## <a name="administrative-tasks-from-the-command-line"></a>명령줄에서 관리 작업
다음 참조 정보를 사용 하 여 명령줄에서 관리 작업을 수행 합니다.

### <a name="configuration-and-installation"></a>구성 및 설치

|                             태스크                              |                                                                                                                                                                                                                 명령                                                                                                                                                                                                                 |
|---------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|             로컬 관리자 암호 설정             |                                                                                                                                                                                                      **net user administrator** \*                                                                                                                                                                                                      |
|                  도메인에 컴퓨터 가입                  |                                                                                                                                                       **netdom join %computername%** **/domain:\<도메인\> /userd:\<도메인\\username\> /passwordd:** \* <br> 컴퓨터를 다시 시작합니다.                                                                                                                                                        |
|              도메인 변경 여부 확인              |                                                                                                                                                                                                                 **set**                                                                                                                                                                                                                 |
|                도메인에서 컴퓨터 제거                |                                                                                                                                                                                                   **netdom remove \<computername\>**                                                                                                                                                                                                    |
|         로컬 관리자 그룹에 사용자 추가          |                                                                                                                                                                                       **net localgroup 관리자 /add \<도메인\\사용자 이름\>**                                                                                                                                                                                       |
|       로컬 관리자 그룹에서 사용자 제거       |                                                                                                                                                                                     **net localgroup 관리자 /delete \<도메인\\사용자 이름\>**                                                                                                                                                                                      |
|               로컬 컴퓨터에 사용자 추가                |                                                                                                                                                                                                **net user \<domain\username\> \* /add**                                                                                                                                                                                                 |
|               로컬 컴퓨터에 그룹 추가               |                                                                                                                                                                                                 **net localgroup \<그룹 이름\> 추가**                                                                                                                                                                                                  |
|          도메인 가입 컴퓨터 이름 변경          |                                                                                                                                                           **netdom renamecomputer %computername% /NewName:\<new computer name\> /userd:\<domain\\username\> /passwordd:** \*                                                                                                                                                            |
|                 새 컴퓨터 이름 확인                 |                                                                                                                                                                                                                 **set**                                                                                                                                                                                                                 |
|         작업 그룹의 컴퓨터 이름 변경         |                                                                                                                                                                **netdom renamecomputer \<currentcomputername\> /NewName:\<newcomputername\>** <br>컴퓨터를 다시 시작합니다.                                                                                                                                                                 |
|                페이징 파일 관리 사용 안 함                 |                                                                                                                                                                        **wmic computersystem 이름을 여기서 = "\<computername\>" AutomaticManagedPagefile 설정 = False**                                                                                                                                                                         |
|                   페이징 파일 구성                   |                                                            **wmic pagefileset 이름을 여기서 = "\<path/filename\>" InitialSize 설정 =\<initialsize\>, MaximumSize =\<maxsize\>** <br>여기서 *path/filename* 페이징 파일의 이름과 경로에 *initialsize* 시작 크기입니다 (바이트)를 사용 하는 페이징 파일을 및 *maxsize* 의 최대 크기는 페이지 파일 (바이트)에서입니다.                                                             |
|                 고정 IP 주소로 변경                 | **ipconfig /all** <br>관련 정보를 기록 하거나 텍스트 파일에 리디렉션 (**ipconfig /all > ipconfig.txt**).<br>**netsh 인터페이스 ipv4 표시 인터페이스**<br>인터페이스 목록 인지 확인 합니다.<br>**netsh interface ipv4 주소 이름 설정 \<인터페이스 목록에서 ID\> 소스 정적 주소 = =\<IP 주소를 기본 설정\> 게이트웨이 =\<게이트웨이 주소\>**<br>실행 **ipconfig /all** DHCP 사용으로 설정 되어 있는지 확인 하려면 **No**합니다. |
|                   고정 DNS 주소를 설정 합니다.                   |   <strong>netsh interface ipv4 dns 서버 이름을 추가 =\<네트워크 인터페이스 카드의 이름 또는 ID\> 주소 =\<주 DNS 서버의 IP 주소\> 인덱스 = 1 <br></strong>netsh interface ipv4 dns 서버 이름을 추가 =\<보조 DNS 서버 이름\> 주소 =\<보조 DNS 서버 IP 주소의\> 인덱스 = 2\*\* <br> 추가 서버를 추가 하려면 적절 하 게 반복 합니다.<br>실행 **ipconfig /all** 주소가 올바른지 확인 합니다.   |
| 고정 IP 주소에서 DHCP 제공 IP 주소로 변경 |                                                                                                                                      **netsh interface ipv4 주소 이름 설정 =\<로컬 시스템의 IP 주소\> 원본 DHCP =** <br>실행할 **ipconfig /all** DCHP를 사용 하도록 설정으로 설정 되어 있는지 확인 하려면 **예**합니다.                                                                                                                                      |
|                      제품 키 입력                      |                                                                                                                                                                                                   **slmgr.vbs – ipk \<제품 키\>**                                                                                                                                                                                                    |
|                  로컬로 서버 정품 인증                  |                                                                                                                                                                                                           **slmgr.vbs -ato**                                                                                                                                                                                                            |
|                 원격으로 서버 정품 인증                  |                                            **cscript slmgr.vbs – ipk \<제품 키\>\<서버 이름\>\<username\>\<암호\>** <br>**cscript slmgr.vbs-ato \<servername\> \<username\> \<암호\>** <br>실행 하 여 컴퓨터의 GUID를 가져오려면 **cscript slmgr.vbs-않았습니다** <br> Run **cscript slmgr.vbs -dli \<GUID\>** <br>라이선스 상태로 설정 되어 있는지 확인 하십시오 **(활성화) 하는 사용이 허가 된**합니다.                                             |

### <a name="networking-and-firewall"></a>네트워킹 및 방화벽

|태스크|명령| 
|----|-------|
|프록시 서버를 사용 하도록 서버 구성|**netsh Winhttp 프록시 설정 \<servername\>:\<포트 번호\>** <br>**참고:** Server Core 설치는 프록시 연결을 허용 하는 데 암호 필요를 통해 인터넷에 액세스할 수 없습니다.|
|인터넷 주소에 대 한 프록시를 무시 하도록 서버 구성|**netsh winttp set proxy \<servername\>:\<port number\> bypass-list="\<local\>"**| 
|IPSEC 구성 표시 또는 수정|**netsh ipsec**| 
|NAP 구성 표시 또는 수정|**netsh nap**| 
|표시 하거나 IP-물리적 주소 변환이 수정|**arp**| 
|표시 하거나 로컬 라우팅 테이블 구성|**route**| 
|보기 또는 DNS 서버 설정을 구성 합니다.|**nslookup**| 
|프로토콜 통계 및 현재 TCP/IP 네트워크 연결 표시|**netstat**| 
|프로토콜 통계 및 TCP/IP (NBT)를 통해 NetBIOS를 사용 하 여 현재 TCP/IP 연결 표시|**nbtstat**| 
|네트워크 연결의 홉 표시|**pathping**| 
|네트워크 연결의 홉 추적|**tracert**| 
|멀티캐스트 라우터 구성 표시|**mrinfo**| 
|방화벽의 원격 관리를 사용 하도록 설정|**netsh advfirewall 방화벽 규칙 그룹 설정 = "Windows 방화벽 원격 관리" 새 enable = yes**| 
 

### <a name="updates-error-reporting-and-feedback"></a>업데이트, 오류 보고 및 피드백

|                               태스크                                |                                                                                                                               명령                                                                                                                                |
|-------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                         업데이트 설치                         |                                                                                                                    **wusa \<update\>.msu /quiet**                                                                                                                    |
|                      설치된 업데이트 나열                       |                                                                                                                            **systeminfo**                                                                                                                            |
|                         업데이트 제거                          |                                 **expand /f:\* \<update\>.msu c:\test** <br>연 c:\test\ 이동할 \<업데이트\>텍스트 편집기에서.xml입니다.<br>바꿉니다 **설치** 사용 하 여 **제거** 파일을 저장 합니다.<br>**pkgmgr /n:\<update\>.xml**                                 |
|                    자동 업데이트 구성                    |          현재 설정을 확인 하려면: **cscript %systemroot%\system32\scregedit.wsf /AU /v \* \* <br>자동 업데이트를 사용 하도록 설정 하려면: \* \*cscript scregedit.wsf /AU 4** <br>자동 업데이트를 사용 하지 않도록 설정: **cscript %systemroot%\system32\scregedit.wsf /AU 1**          |
|                      오류 보고 사용                       | 현재 설정을 확인 하려면: **serverWerOptin /query** <br>자세한 보고서를 자동으로 보내도록: **serverWerOptin 자세한 /** <br>요약 보고서를 자동으로 보내도록: **serverWerOptin 했습니다** <br>오류 보고를 해제 하려면: **serverWerOptin /disable** |
| CEIP(사용자 환경 개선 프로그램) 참여 |                                                     현재 설정을 확인 하려면: **serverCEIPOptin /query** <br>CEIP를 사용 하도록 설정 하려면: **serverCEIPOptin 같습니다.** <br>CEIP를 사용 하지 않도록 설정: **serverCEIPOptin /disable**                                                      |

### <a name="services-processes-and-performance"></a>서비스, 프로세스 및 성능

|                               태스크                               |                                                                                                                                                                                                             명령                                                                                                                                                                                                              |
|------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                    실행 중인 서비스 나열                     |                                                                                                                                                                                                  **sc 쿼리** 또는 **net 시작**                                                                                                                                                                                                   |
|                         서비스 시작                          |                                                                                                                                                                                 **sc 시작 \<서비스 이름을\>**  하거나 **시작 net \<서비스 이름\>**                                                                                                                                                                                  |
|                          서비스 중지                          |                                                                                                                                                                                  **sc stop \<서비스 이름을\>**  하거나 **net stop \<서비스 이름\>**                                                                                                                                                                                   |
| 실행 중인 응용 프로그램 목록 및 관련 프로세스 검색 |                                                                                                                                                                                                           **tasklist**                                                                                                                                                                                                           |
|                        작업 관리자 시작                        |                                                                                                                                                                                                           **taskmgr**                                                                                                                                                                                                            |
|    이벤트 추적 세션과 성능 로그를 만들고 설정 합니다.    | 카운터, 추적, 구성 데이터 수집 또는 API를 만들려면: **logman 서로** <br>쿼리 데이터 수집기 속성: **logman 쿼리** <br>시작 하거나 데이터 수집을 중지 하려면: **logman 시작\|중지** <br>수집기를 삭제 하려면: **logman 삭제** <br> 수집기의 속성을 업데이트 하려면: **logman 업데이트** <br>데이터 수집기 집합 XML 파일에서 가져오거나 XML 파일로 내보내기: **logman 가져오기\|내보내기** |

### <a name="event-logs"></a>이벤트 로그

|태스크|명령| 
|----|-------|
|이벤트 로그 나열|**wevtutil el**| 
|지정된 된 로그에서 이벤트를 쿼리|**wevtutil qe /f:text \<log name\>**| 
|이벤트 로그 내보내기|**wevtutil epl \<로그 이름\>**| 
|이벤트 로그 지우기|**wevtutil cl \<log name\>**| 


### <a name="disk-and-file-system"></a>디스크 및 파일 시스템

|                   태스크                   |                        명령                        |
|------------------------------------------|-------------------------------------------------------|
|          디스크 파티션 관리          | 실행할 명령의 전체 목록은, **diskpart /?**  |
|           소프트웨어 RAID 관리           | 실행할 명령의 전체 목록은, **diskraid /?**  |
|        볼륨 탑재 지점 관리        | 실행할 명령의 전체 목록은, **mountvol /?**  |
|           볼륨 조각 모음            |  실행할 명령의 전체 목록은, **조각 모음 /?**   |
| NTFS 파일 시스템으로 볼륨 변환 |        **변환할 \<볼륨 문자\> /fs: ntfs**         |
|              파일 압축              |  실행할 명령의 전체 목록은, **압축 /?**  |
|          열린 파일 관리           | 실행할 명령의 전체 목록은, **openfiles /?** |
|          VSS 폴더 관리          | 실행할 명령의 전체 목록은, **vssadmin /?**  |
|        파일 시스템 관리        |  실행할 명령의 전체 목록은, **fsutil /?**   |
|    파일 또는 폴더의 소유권 가져오기    |  실행할 명령의 전체 목록은, **icacls /?**   |
 
### <a name="hardware"></a>하드웨어

|태스크|명령| 
|----|-------|
|새 하드웨어 장치의 드라이버 추가|드라이버 %homedrive% 폴더로 복사\\\<드라이버 폴더\>합니다. 실행할 **pnputil-i-a %homedrive%\\\<드라이버 폴더\>\\\<드라이버\>.inf**|
|하드웨어 장치의 드라이버 제거|목록을 로드 된 드라이버에 대 한 실행 **sc 쿼리 유형 = 드라이버**합니다. 그런 다음 실행 **sc delete \<service_name\>**|
