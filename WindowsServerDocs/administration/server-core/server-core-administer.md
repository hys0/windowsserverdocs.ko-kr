---
title: 서버 코어 관리
description: Windows Server의 Server Core 설치를 관리 하는 방법 알아보기
ms.prod: windows-server
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.author: elizapo
ms.localizationpriority: medium
ms.date: 12/18/2018
ms.openlocfilehash: 577014f6fd7e3a3eb58567b1a644d44360f9e498
ms.sourcegitcommit: 51e0b575ef43cd16b2dab2db31c1d416e66eebe8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/17/2020
ms.locfileid: "76259051"
---
# <a name="administer-a-server-core-server"></a>Server Core 서버 관리

>적용 대상: Windows Server 2019, Windows Server 2016 및 Windows Server (반기 채널)

Server Core에는 UI가 없으므로 Windows PowerShell cmdlet, 명령줄 도구 또는 원격 도구를 사용 하 여 기본 관리 작업을 수행 해야 합니다. 다음 섹션에서는 기본 작업에 사용 되는 PowerShell cmdlet 및 명령을 간략하게 설명 합니다. 현재 공개 미리 보기로 제공 되는 통합 된 관리 포털의 [Windows 관리 센터](../../manage/windows-admin-center/overview.md)를 사용 하 여 설치를 관리할 수도 있습니다. 

## <a name="administrative-tasks-using-powershell-cmdlets"></a>PowerShell cmdlet을 사용 하는 관리 작업
Windows PowerShell cmdlet을 사용 하 여 기본 관리 작업을 수행 하려면 다음 정보를 사용 합니다.

### <a name="set-a-static-ip-address"></a>고정 IP 주소 설정
Server Core 서버를 설치 하는 경우 기본적으로 DHCP 주소가 포함 됩니다. 고정 IP 주소가 필요한 경우 다음 단계를 사용 하 여 설정할 수 있습니다.

현재 네트워크 구성을 보려면 **NetIPConfiguration**를 사용 합니다.

이미 사용 하 고 있는 IP 주소를 보려면 **new-netipaddress**를 사용 합니다.

고정 IP 주소를 설정 하려면 다음을 수행 합니다. 

1. **Get-netipinterface**를 실행 합니다. 
2. IP 인터페이스 또는 IfIndex **description** 문자열에 대 한 열의 숫자를 확인 합니다. 네트워크 어댑터가 둘 이상인 경우에는 고정 IP 주소를 설정 하려는 인터페이스에 해당 하는 숫자 또는 문자열을 확인 합니다.
3. 다음 cmdlet을 실행 하 여 고정 IP 주소를 설정 합니다.

   ```powershell
   New-NetIPaddress -InterfaceIndex 12 -IPAddress 192.0.2.2 -PrefixLength 24 -DefaultGateway 192.0.2.1
   ```

   각 항목은 다음을 의미합니다.
   - **InterfaceIndex** 는 2 단계의 **IfIndex** 값입니다. (이 예제에서는 12)
   - **IPAddress** 는 설정 하려는 고정 IP 주소입니다. (이 예제에서는 191.0.2.2)
   - **PrefixLength** 는 설정 중인 IP 주소에 대 한 접두사 길이 (서브넷 마스크의 또 다른 형태)입니다. (이 예제에서는 24)
   - **DefaultGateway** 는 기본 게이트웨이의 IP 주소입니다. (이 예제에서는 192.0.2.1)
4. 다음 cmdlet을 실행 하 여 DNS 클라이언트 서버 주소를 설정 합니다. 

   ```powershell
   Set-DNSClientServerAddress –InterfaceIndex 12 -ServerAddresses 192.0.2.4
   ```
   
   각 항목은 다음을 의미합니다.
   - **InterfaceIndex** 는 2 단계의 IfIndex 값입니다.
   - **ServerAddresses** 는 DNS 서버의 IP 주소입니다.
5. 여러 DNS 서버를 추가 하려면 다음 cmdlet을 실행 합니다. 

   ```powershell
   Set-DNSClientServerAddress –InterfaceIndex 12 -ServerAddresses 192.0.2.4,192.0.2.5
   ```

   여기서,이 예제에서 **예에서 192.0.2.4** 및 **192.0.2.5** 는 둘 다 DNS 서버의 IP 주소입니다.

DHCP를 사용 하도록 전환 해야 하는 경우 **Set DnsClientServerAddress – InterfaceIndex 12 – ResetServerAddresses**를 실행 합니다.

### <a name="join-a-domain"></a>도메인 가입
다음 cmdlet을 사용 하 여 컴퓨터를 도메인에 가입 시킵니다.

1. **컴퓨터 추가**를 실행 합니다. 도메인 및 도메인 이름에 가입 하기 위해 두 자격 증명을 모두 입력 하 라는 메시지가 표시 됩니다.
2. 로컬 관리자 그룹에 도메인 사용자 계정을 추가 해야 하는 경우 명령 프롬프트 (PowerShell 창이 아님)에서 다음 명령을 실행 합니다.

   ```
   net localgroup administrators /add <DomainName>\<UserName>
   ```
3. 컴퓨터를 다시 시작합니다. **컴퓨터 다시 시작**을 실행 하 여이 작업을 수행할 수 있습니다.

### <a name="rename-the-server"></a>서버 이름 바꾸기
서버 이름을 바꾸려면 다음 단계를 사용 합니다.

1. **hostname** 또는 **ipconfig** 명령으로 현재 서버 이름을 확인합니다.
2. **이름 바꾸기-컴퓨터-ComputerName \<new_name\>** 를 실행 합니다.
3. 컴퓨터를 다시 시작합니다.

### <a name="activate-the-server"></a>서버 정품 인증

**Slmgr.vbs – ipk\<productkey\>** 를 실행 합니다. 그런 다음 **slmgr.vbs – ato**를 실행 합니다. 활성화가 성공 하면 메시지가 표시 되지 않습니다.

> [!NOTE]
> 전화, [KMS (키 관리 서비스) 서버](../../get-started/server-2016-activation.md)를 사용 하 여 또는 원격으로 서버를 정품 인증할 수도 있습니다. 원격으로 정품 인증 하려면 원격 컴퓨터에서 다음 cmdlet을 실행 합니다. 
> 
> ```
> cscript windows\system32\slmgr.vbs <ServerName> <UserName> <password>:-ato
> ```
 
### <a name="configure-windows-firewall"></a>Windows 방화벽 구성

Windows PowerShell cmdlet 및 스크립트를 사용하여 Server Core 컴퓨터에서 로컬로 Windows 방화벽을 구성할 수 있습니다. Windows 방화벽을 구성 하는 데 사용할 수 있는 cmdlet에 대 한 [Netsecurity](/powershell/module/netsecurity/?view=win10-ps) 를 참조 하세요.

### <a name="enable-windows-powershell-remoting"></a>Windows PowerShell 원격 기능 사용

특정 컴퓨터의 Windows PowerShell에 입력된 명령을 또 다른 컴퓨터에서 실행하는 Windows PowerShell 원격 기능을 사용할 수 있습니다. **Enable-psremoting**를 사용 하 여 Windows PowerShell 원격을 사용 하도록 설정 합니다.

자세한 내용은 [원격 FAQ 정보](/powershell/module/microsoft.powershell.core/about/about_remote_faq?view=powershell-5.1)를 참조 하세요.

## <a name="administrative-tasks-from-the-command-line"></a>명령줄에서 관리 태스크
다음 참조 정보를 사용 하 여 명령줄에서 관리 작업을 수행할 수 있습니다.

### <a name="configuration-and-installation"></a>구성 및 설치

|                             작업                              |                                                                                                                                                                                                                 명령                                                                                                                                                                                                                 |
|---------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|             로컬 관리자 암호 설정             |                                                                                                                                                                                                      **net 사용자 관리자** \*                                                                                                                                                                                                      |
|                  도메인에 컴퓨터를 가입                  |                                                                                                                                                       **netdom join% computername%** **/domain:\<domain\>/userd:\<domain\\username\>/passwordd:** \* <br> 컴퓨터를 다시 시작합니다.                                                                                                                                                        |
|              도메인 변경 여부 확인              |                                                                                                                                                                                                                 **set**                                                                                                                                                                                                                 |
|                도메인에서 컴퓨터 제거                |                                                                                                                                                                                                   **netdom \<computername\> 제거**                                                                                                                                                                                                    |
|         로컬 관리자 그룹에 사용자 추가          |                                                                                                                                                                                       **net localgroup Administrators/add \<도메인\\사용자 이름\>**                                                                                                                                                                                       |
|       로컬 관리자 그룹에서 사용자 제거       |                                                                                                                                                                                     **net localgroup Administrators/delete \<도메인\\사용자 이름\>**                                                                                                                                                                                      |
|               로컬 컴퓨터에 사용자 추가                |                                                                                                                                                                                                **net user \<domain\username\> \*/add**                                                                                                                                                                                                 |
|               로컬 컴퓨터에 그룹 추가               |                                                                                                                                                                                                 **net localgroup \<그룹 이름\>/add**                                                                                                                                                                                                  |
|          도메인 가입 컴퓨터 이름 변경          |                                                                                                                                                           **netdom renamecomputer% computername%/newname:\<새 컴퓨터 이름\>/userd:\<domain\\username\>/passwordd:** \*                                                                                                                                                            |
|                 새 컴퓨터 이름 확인                 |                                                                                                                                                                                                                 **set**                                                                                                                                                                                                                 |
|         작업 그룹의 컴퓨터 이름 변경         |                                                                                                                                                                **netdom renamecomputer \<currentcomputername\>/NewName:\<newcomputername\>** <br>컴퓨터를 다시 시작합니다.                                                                                                                                                                 |
|                페이징 파일 관리 사용 안 함                 |                                                                                                                                                                        **wmic computersystem 이름 = "\<computername\>" set 자동 Managed파일 이름 = False**                                                                                                                                                                         |
|                   페이징 파일 구성                   |                                                            **wmic pagefileset where name = "\<경로/파일 이름\>" set InitialSize =\<InitialSize\>, MaximumSize =\<maxsize\>** <br>여기서 *path/filename* 은 페이징 파일의 경로 및 이름입니다. *initialsize* 는 페이징 파일의 시작 크기 (바이트)이 고 *maxsize* 는 페이지 파일의 최대 크기 (바이트)입니다.                                                             |
|                 고정 IP 주소로 변경                 | **ipconfig/all** <br>관련 정보를 기록 하거나 텍스트 파일로 리디렉션합니다 (**ipconfig/all > ipconfig .txt**).<br>**netsh 인터페이스 ipv4 표시 인터페이스**<br>인터페이스 목록이 있는지 확인 합니다.<br>**netsh interface ipv4 set address \<Name ID from interface list\> source = 고정 address =\<기본 설정 IP 주소\> 게이트웨이 =\<게이트웨이 주소\>**<br>**Ipconfig/all** 을 실행 하 여 DHCP Enabled가 **No**로 설정 되어 있는지 확인 합니다. |
|                   정적 DNS 주소를 설정 합니다.                   |   <strong>netsh interface ipv4 add dnsserver name = 네트워크 인터페이스 카드의\<이름 또는 ID\> 주소 =\<주 DNS 서버의 IP 주소\> 인덱스 = 1 <br></strong>netsh interface ipv4 add dnsserver name =\<name of 보조 DNS 서버\> address =\<보조 DNS 서버의 IP 주소\> 인덱스 = 2\*\* <br> 서버를 더 추가 하려면 적절 하 게 반복 합니다.<br>**Ipconfig/all** 을 실행 하 여 주소가 올바른지 확인 합니다.   |
| 고정 IP 주소에서 DHCP 제공 IP 주소로 변경 |                                                                                                                                      **netsh interface ipv4 set address name = local system\> source = DHCP의\<IP 주소** <br>**Ipconfig/all** 을 실행 하 여 DCHP Enabled가 **Yes**로 설정 되었는지 확인 합니다.                                                                                                                                      |
|                      제품 키 입력                      |                                                                                                                                                                                                   **slmgr.vbs – ipk \<제품 키\>**                                                                                                                                                                                                    |
|                  로컬로 서버 정품 인증                  |                                                                                                                                                                                                           **slmgr.vbs-ato**                                                                                                                                                                                                            |
|                 원격으로 서버 정품 인증                  |                                            **cscript slmgr.vbs – ipk \<제품 키\>\<서버 이름\>\<사용자 이름\>\<암호\>** <br>**cscript ato \<servername\> \<사용자 이름\> \<암호\>** <br>**Cscript slmgr.vbs** 를 실행 하 여 컴퓨터의 GUID를 가져옵니다. <br> **Dli \<GUID\>를** 실행 합니다. <br>라이선스 상태가 라이선스 **(활성화 됨)** 로 설정 되어 있는지 확인 합니다.                                             |

### <a name="networking-and-firewall"></a>네트워킹 및 방화벽

|작업|명령| 
|----|-------|
|프록시 서버를 사용 하도록 서버 구성|**netsh Winhttp set proxy \<servername\>:\<포트 번호\>** <br>**참고:** Server Core 설치는 연결을 허용 하기 위해 암호가 필요한 프록시를 통해 인터넷에 액세스할 수 없습니다.|
|인터넷 주소에 프록시를 사용 하지 않도록 서버 구성|**netsh winhttp set proxy \<servername\>:\<포트 번호\> 바이패스 목록 = "\<local\>"**| 
|IPSEC 구성 표시 또는 수정|**netsh ipsec**| 
|NAP 구성 표시 또는 수정|**netsh nap**| 
|IP를 실제 주소 변환에 표시 하거나 수정 합니다.|**arp**| 
|로컬 라우팅 테이블을 표시 하거나 구성 합니다.|**route**| 
|DNS 서버 설정 보기 또는 구성|**nslookup**| 
|프로토콜 통계 및 현재 TCP/IP 네트워크 연결 표시|**netstat**| 
|NBT (NetBIOS over TCP/IP)를 사용 하 여 프로토콜 통계 및 현재 TCP/IP 연결을 표시 합니다.|**nbtstat**| 
|네트워크 연결에 대 한 홉 표시|**pathping**| 
|네트워크 연결에 대 한 추적 홉|**tracert**| 
|멀티캐스트 라우터 구성 표시|**mrinfo**| 
|방화벽의 원격 관리 사용|**netsh advfirewall firewall set rule group = "Windows Defender Firewall Remote Management" new enable = yes**| 
 

### <a name="updates-error-reporting-and-feedback"></a>업데이트, 오류 보고 및 피드백

|                               작업                                |                                                                                                                               명령                                                                                                                                |
|-------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                         업데이트 설치                         |                                                                                                                    **wusa \<업데이트\>.msu/quiet**                                                                                                                    |
|                      설치된 업데이트 나열                       |                                                                                                                            **systeminfo**                                                                                                                            |
|                         업데이트 제거                          |                                 **/f:\* \<업데이트\>.msu c:\test를 확장 합니다.** <br>C:\test\으로 이동 하 여 텍스트 편집기에서\>.xml \<업데이트를 엽니다.<br>**Install** 을 **Remove** 로 바꾸고 파일을 저장 합니다.<br>**pkgmgr.exe/n:\<업데이트\>.xml**                                 |
|                    자동 업데이트 구성                    |          현재 설정인 **cscript%SYSTEMROOT%\SYSTEM32\SCREGEDIT.WSF/AU/v \*\*<br>자동 업데이트를 사용 하도록 설정 하려면 다음을 수행 합니다. \*\*cscript scregedit.exe. .WSF/AU 4** <br>자동 업데이트를 사용 하지 않도록 설정 하려면: **cscript%SYSTEMROOT%\SYSTEM32\SCREGEDIT.WSF/AU 1**          |
|                      오류 보고 사용                       | 현재 설정을 확인 하려면: **serverWerOptin/query** <br>상세 보고서를 자동으로 보내려면: **serverWerOptin 자세한/** <br>요약 보고서를 자동으로 보내려면: **serverWerOptin/summary** <br>오류 보고를 사용 하지 않도록 설정 하려면: **serverWerOptin/disable** |
| CEIP(사용자 환경 개선 프로그램) 참여 |                                                     현재 설정을 확인 하려면: **serverCEIPOptin/query** <br>CEIP를 사용 하도록 설정 하려면: **serverCEIPOptin/enable** <br>CEIP를 사용 하지 않도록 설정 하려면: **serverCEIPOptin/disable**                                                      |

### <a name="services-processes-and-performance"></a>서비스, 프로세스 및 성능

|                               작업                               |                                                                                                                                                                                                             명령                                                                                                                                                                                                              |
|------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                    실행 중인 서비스 나열                     |                                                                                                                                                                                                  **sc 쿼리** 또는 **net start**                                                                                                                                                                                                   |
|                         서비스 시작                          |                                                                                                                                                                                 **sc start \<서비스 이름\>** 또는 **net start \<서비스 이름\>**                                                                                                                                                                                  |
|                          서비스 중지                          |                                                                                                                                                                                  **sc stop \<서비스 이름\>** 또는 **net stop \<서비스 이름\>**                                                                                                                                                                                   |
| 실행 중인 애플리케이션 목록 및 관련 프로세스 검색 |                                                                                                                                                                                                           **tasklist**                                                                                                                                                                                                           |
|                        작업 관리자 시작                        |                                                                                                                                                                                                           **taskmgr->networking**                                                                                                                                                                                                            |
|    이벤트 추적 세션 및 성능 로그 만들기 및 관리    | 카운터, 추적, 구성 데이터 컬렉션 또는 API를 만들려면: **logman 만들기** <br>데이터 수집기 속성을 쿼리하려면: **logman query** <br>데이터 수집을 시작 하거나 중지 하려면: **logman start\|stop** <br>수집기를 삭제 하려면: **logman delete** <br> 수집기의 속성을 업데이트 하려면: **logman update** <br>XML 파일에서 데이터 수집기 집합을 가져오거나 XML 파일로 내보내려면: **logman 가져오기\|내보내기** |

### <a name="event-logs"></a>이벤트 로그

|작업|명령| 
|----|-------|
|이벤트 로그 나열|**wevtutil el**| 
|지정 된 로그의 쿼리 이벤트|**wevtutil qe/f: 텍스트 \<로그 이름\>**| 
|이벤트 로그 내보내기|**wevtutil epl \<로그 이름\>**| 
|이벤트 로그 지우기|**wevtutil cl \<로그 이름\>**| 


### <a name="disk-and-file-system"></a>디스크 및 파일 시스템

|                   작업                   |                        명령                        |
|------------------------------------------|-------------------------------------------------------|
|          디스크 파티션 관리          | 전체 명령 목록을 보려면 **diskpart/?** 를 실행 하십시오.  |
|           소프트웨어 RAID 관리           | 명령의 전체 목록을 보려면 **diskraid/?** 를 실행 하십시오.  |
|        볼륨 탑재 지점 관리        | 전체 명령 목록은 **mountvol/?** 를 실행 합니다.  |
|           볼륨 조각 모음            |  전체 명령 목록을 보려면 **defrag/?** 를 실행 하십시오.   |
| NTFS 파일 시스템으로 볼륨 변환 |        **\<볼륨 문자\>/FS: NTFS로 변환 합니다.**         |
|              파일 압축              |  전체 명령 목록을 보려면 **compact/?** 를 실행 하십시오.  |
|          열린 파일 관리           | 전체 명령 목록을 보려면 **openfiles/?** 를 실행 하십시오. |
|          VSS 폴더 관리          | 전체 명령 목록을 보려면 **vssadmin/?** 를 실행 하십시오.  |
|        파일 시스템 관리        |  전체 명령 목록을 보려면 **fsutil/?** 를 실행 하십시오.   |
|    파일 또는 폴더의 소유권 가져오기    |  전체 명령 목록을 보려면 **icacls/?** 를 실행 하십시오.   |
 
### <a name="hardware"></a>하드웨어

|작업|명령| 
|----|-------|
|새 하드웨어 디바이스의 드라이버 추가|% Homedrive%\\\<드라이버 폴더\>폴더에 드라이버를 복사 합니다. **Pnputil-i-a% homedrive%\\\<driver 폴더\>\\\<드라이버\>.inf를 실행 합니다.**|
|하드웨어 디바이스의 드라이버 제거|로드 된 드라이버 목록을 보려면 **sc query type = driver**를 실행 합니다. 그런 다음 **sc delete \<service_name** 를 실행\>|
