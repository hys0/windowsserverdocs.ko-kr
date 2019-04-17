---
title: Server Core 관리
description: Windows Server의 Server Core 설치를 관리 하는 방법을 알아봅니다
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.author: elizapo
ms.localizationpriority: medium
ms.date: 12/18/2018
ms.openlocfilehash: 39fbb92645d39a46613f2142d0258c78a6ba425b
ms.sourcegitcommit: 4df1bc940338219316627ad03f0525462a05a606
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/19/2018
ms.locfileid: "8978000"
---
# Server Core 서버 관리

>적용 대상: Windows Server(반기 채널) 및 Windows Server 2016

Server Core UI가 때문에 Windows PowerShell cmdlet, 명령줄 도구 또는 원격 도구를 사용 하 여 기본 관리 작업을 수행 해야 합니다. 다음 섹션에서는 PowerShell cmdlet 및 기본 작업에 사용 되는 명령을 간략하게 설명 합니다. 설치를 관리 하도록 [Windows Admin Center](../../manage/windows-admin-center/overview.md)를 공용 미리 보기에서 현재 통합된 관리 포털을 사용할 수도 있습니다. 

## PowerShell cmdlet을 사용 하 여 관리 작업
다음 정보를 사용 하 여 Windows PowerShell cmdlet 사용 하 여 기본 관리 작업을 수행 합니다.

### 고정 IP 주소 설정
Server Core 서버를 설치 하면 기본적으로이 DHCP 주소도가 있습니다. 고정 IP 주소, 필요한 경우 다음 단계를 사용 하 여 설정할 수 있습니다.

현재 네트워크 구성을 보려면 **Get NetIPConfiguration**를 사용 합니다.

이미 사용 중인 IP 주소를 보려면 **Get-netipaddress**를 사용 합니다.

고정 IP 주소를 설정 하려면 다음을 수행 합니다. 

1. **Get NetIPInterface**를 실행 합니다. 
2. Note IP 인터페이스 또는 **InterfaceDescription** 문자열에 대 한 **IfIndex** 열 수 있습니다. 둘 이상의 네트워크 어댑터가 있는 경우 note 해당 인터페이스에 대 한 고정 IP 주소를 설정 하려면 하는 문자열의 수입니다.
3. 고정 IP 주소를 설정 하려면 다음 cmdlet을 실행 합니다.

   ```powershell
   New-NetIPaddress -InterfaceIndex 12 -IPAddress 192.0.2.2 -PrefixLength 24 -DefaultGateway 192.0.2.1
   ```

   각 항목은 다음을 의미합니다.
   - **InterfaceIndex** 2 단계의 **IfIndex** 의 값입니다. (이 예에서는 12)에서
   - **IPAddress** 설정 하려면 정적 IP 주소입니다. (이 예에서는 191.0.2.2)에서
   - **PrefixLength** 접두사 길이 (다른 형태의 서브넷 마스크)를 설정 하는 IP 주소입니다. (예: 우리의 24)
   - **기본 게이트웨이** 기본 게이트웨이 IP 주소입니다. (예: 우리의 192.0.2.1)
4. DNS 클라이언트 서버 주소를 설정 하려면 다음 cmdlet을 실행 합니다. 

   ```powershell
   Set-DNSClientServerAddress –InterfaceIndex 12 -ServerAddresses 192.0.2.4
   ```
   
   각 항목은 다음을 의미합니다.
   - **InterfaceIndex** 2 단계의 IfIndex의 값입니다.
   - **ServerAddresses** DNS 서버의 IP 주소입니다.
5. 여러 DNS 서버를 추가 하려면 다음 cmdlet을 실행 합니다. 

   ```powershell
   Set-DNSClientServerAddress –InterfaceIndex 12 -ServerAddresses 192.0.2.4,192.0.2.5
   ```

   위치,이 예제에서는 **192.0.2.4** 및 **192.0.2.5** 는 DNS 서버의 IP 주소입니다.

실행 DHCP를 사용 하 여 전환할 필요가 **집합 DnsClientServerAddress – InterfaceIndex 12 – ResetServerAddresses**합니다.

### 도메인에 가입
컴퓨터를 도메인에 가입 하려면 다음 cmdlet을 사용 합니다.

1. **추가 컴퓨터**를 실행 합니다. 가입할 도메인 및 도메인 이름을 모두 자격 증명에 대 한 메시지가 표시 됩니다.
2. 로컬 관리자 그룹에 도메인 사용자 계정을 추가 해야 할 경우 (PowerShell 창)에 없는 명령 프롬프트에서 다음 명령을 실행 합니다.

   ```
   net localgroup administrators /add <DomainName>\<UserName>
   ```
3. 컴퓨터를 다시 시작 합니다. **컴퓨터를 다시 시작을**실행 하 여 설정할 수 있습니다.

### 서버 이름 바꾸기
다음 단계를 사용 하 여 서버의 이름을 바꿉니다.

1. **호스트 이름** 또는 **ipconfig** 명령 사용 하 여 서버의 현재 이름을 확인 합니다.
2. 실행 **컴퓨터 이름 바꾸기-ComputerName \<new_name\ >** 합니다.
3. 컴퓨터를 다시 시작 합니다.

### 서버 활성화

실행 **slmgr.vbs – ipk\<productkey\ >** 합니다. **Slmgr.vbs – ato**실행 됩니다. 정품 인증에 성공 하면 메시지를 얻게 되지 않습니다.

> [!NOTE]
> 활성화할 수도 서버 전화로 [키 관리 서비스 (KMS) 서버](../../get-started/server-2016-activation.md)를 사용 하 여 또는 원격으로 합니다. 원격으로 활성화 하려면 원격 컴퓨터에서 다음 cmdlet을 실행 합니다. 

>```powershell
>**cscript windows\system32\slmgr.vbs <ServerName> <UserName> <password>:-ato**
>```
 
### Windows 방화벽 구성

Windows PowerShell cmdlet 및 스크립트를 사용 하 여 Server Core 컴퓨터에서 Windows 방화벽을 로컬로 구성할 수 있습니다. Windows 방화벽을 구성 하는 데 사용할 수 cmdlet에 대 한 [NetSecurity](/powershell/module/netsecurity/?view=win10-ps) 를 참조 하세요.

### Windows PowerShell 원격 기능 사용

명령을 입력 Windows PowerShell의 다른 컴퓨터에서 실행 한 컴퓨터에서 Windows PowerShell 원격 기능을 사용할 수 있습니다. **Enable-psremoting**를 사용 하 여 Windows PowerShell 원격 기능 사용 하도록 설정 합니다.

자세한 내용은 [원격 FAQ](/powershell/module/microsoft.powershell.core/about/about_remote_faq?view=powershell-5.1) 를 참조 하세요.
</br>

## 명령줄에서 관리 작업
다음 참조 정보를 사용 하 여 명령줄에서 관리 작업을 수행 합니다.

### 설치 및 구성
|작업 | 명령 |
|-----|-------|
|로컬 관리자 암호 설정| **순 사용자 관리자** \* |
|컴퓨터를 도메인에 가입| **netdom 조인 %computername%** **/domain:\<domain\ > /userd:\<domain\\username\ > /passwordd:**\* <br> 컴퓨터를 다시 시작 합니다.|
|도메인 변경 된 것을 확인 합니다.| **set** |
|도메인에서 컴퓨터 제거|**netdom 제거 \ < computername\ >**| 
|로컬 관리자 그룹에 사용자 추가|**net localgroup 관리자 / 추가 \ < domain\\username\ >** |
|로컬 관리자 그룹에서 사용자 제거|**net localgroup 관리자 /delete \ < domain\\username\ >** |
|로컬 컴퓨터에 사용자 추가|**총 사용자 \ < domain\username\ > * / 추가** |
|로컬 컴퓨터에 그룹 추가|**net localgroup \ < 그룹 이름 \ > / 추가**|
|도메인에 가입 된 컴퓨터의 이름을 변경합니다|**netdom renamecomputer %computername% /NewName:\<new 컴퓨터 이름 \ > /userd:\<domain\\username\ > /passwordd:** * |
|새 컴퓨터 이름을 확인 합니다.|**set**| 
|작업 그룹에서 컴퓨터의 이름을 변경합니다|**netdom renamecomputer \ < currentcomputername\ > /NewName: \ < newcomputername\ >** <br>컴퓨터를 다시 시작 합니다.|
|페이징 파일 관리를 사용 하지 않도록 설정|**wmic 있음을 이름 = "\ < computername\ >" AutomaticManagedPagefile 설정 = False**| 
|페이징 파일 구성|**wmic pagefileset 이름 = "\ < 경로/filename\ >" InitialSize 설정 = \ < initialsize\ > MaximumSize = \ < maxsize\ >** <br>*경로/파일* 은 경로 *initialsize* 페이징 파일의 이름 시작 크기를 바이트 단위로 페이징 파일의 이며 *maxsize* 바이트에서 페이지 파일의 최대 크기입니다.|
|고정 IP 주소를 변경 합니다.|**ipconfig 모든 /** <br>관련 정보를 기록 또는 텍스트 파일에 리디렉션 (**ipconfig 모든/> ipconfig.txt**).<br>**netsh 인터페이스 ipv4 표시 인터페이스**<br>인터페이스 목록 인지 확인 합니다.<br>**netsh 인터페이스 ipv4 주소 이름을 설정 \ < 인터페이스 list\에서 ID > 소스 고정 주소 = = \ < 선호 IP address\ > 게이트웨이 = \ < 게이트웨이 address\ >**<br>실행 **ipconfig 모든/** DHCP 사용 **No**로 설정 되어 있는 vierfy을 합니다.|
|정적 DNS 주소를 설정 합니다.|**netsh 인터페이스 ipv4 dns 서버 이름을 추가 \<name 또는 네트워크 인터페이스 card\의 ID = > 주소의 주 DNS server\ \<IP 주소 = > 인덱스 = 1 <br> **netsh 인터페이스 ipv4 dns 서버 이름을 추가 보조 DNS server\의 \<name = > 주소 보조 DNS server\의 \<IP 주소 = > 인덱스 2 = * * <br> 추가 서버를 추가 하려면 적절 하 게 반복 합니다.<br>실행 **ipconfig 모든/** 주소가 올바른지 확인 합니다.|
|DHCP에서 제공한 IP 주소를 고정 IP 주소에서 변경|**netsh 인터페이스 ipv4 주소 이름을 설정 = \ < 로컬 system\의 IP 주소 > 소스 DHCP =** <br>실행 **Ipconfig 모든/** DCHP 활성화 **Yes**로 설정 되어 있는지 확인 합니다.|
|제품 키 입력|**slmgr.vbs – 합니다 \ < 제품 k e y >**| 
|로컬에서 서버 활성화|**slmgr.vbs ato**| 
|원격으로 서버 활성화|**cscript slmgr.vbs – 합니다 \ < 제품 k e y > \ < 서버 이름 > \ < username\ > \ < password\ >** <br>**cscript slmgr.vbs ato \ < servername\ > \ < username\ > \ < password\ >** <br>실행 하 여 컴퓨터의 GUID를 가져올 **cscript slmgr.vbs-않은** <br> 실행 **cscript slmgr.vbs-dli \<GUID\ >** <br>라이선스 상태 **라이선스 (활성화)** 으로 설정 되어 있는지 확인 합니다.


### 네트워킹 및 방화벽

|작업|명령| 
|----|-------|
|프록시 서버를 사용 하 여 서버 구성|**netsh Winhttp 프록시 설정 \ < servername\ >: \ < 포트 번호 >** <br>**참고:** Server Core 설치 연결을 허용 하도록 암호가 필요한 프록시를 통해 인터넷에 액세스할 수 없습니다.|
|인터넷 주소에 프록시를 바이패스 하는 데 서버 구성|**netsh winttp 프록시 설정 \ < servername\ >: \ < 포트 번호 > 바이패스 목록 = "< local\ >"**| 
|표시 하거나 IPSEC 구성을 수정합니다|**netsh ipsec**| 
|표시 하거나 NAP 구성을 수정합니다|**netsh nap**| 
|표시 하거나 실제 주소 변환에 IP를 수정|**arp**| 
|표시 하거나 로컬 라우팅 테이블 구성|**경로**| 
|보기 또는 DNS 서버 설정 구성|**nslookup**| 
|디스플레이 프로토콜 통계 및 현재 TCP/IP 네트워크 연결|**netstat**| 
|프로토콜 통계 및 현재 TCP/IP 연결 TCP/IP (NBT) 위로 NetBIOS를 사용 하 여 표시|**nbtstat**| 
|네트워크 연결에 대 한 디스플레이 홉|**pathping**| 
|네트워크 연결에 대 한 추적 홉|**tracert**| 
|멀티 캐스트 라우터 구성을 표시합니다|**mrinfo**| 
|방화벽의 원격 관리를 사용 하도록 설정|**netsh advfirewall 방화벽 규칙 그룹 설정 = "Windows 방화벽 원격 관리" 새 enable = yes**| 
 

### 업데이트, 오류 보고 및 피드백

|작업|명령| 
|----|-------|
|업데이트 설치|**wusa \ < update\ >.msu /quiet**| 
|설치 된 목록 업데이트|**systeminfo**| 
|업데이트를 제거|**/f:\* 확장 \ < update\ >.msu c:\test** <br>이동 하 여 c:\test\ 열기 \ < update\ >.xml 텍스트 편집기에서.<br>**설치** **제거** 바꾸고 파일을 저장 합니다.<br>**하 /n:\ < update\ >.xml**|
|자동 업데이트 구성|현재 설정을 확인 하려면: * * cscript %systemroot%\system32\scregedit.wsf /AU /v * *<br>자동 업데이트를 사용 하도록 설정: **cscript scregedit.wsf /AU 4** <br>자동 업데이트를 사용 하지 않도록 설정: **cscript %systemroot%\system32\scregedit.wsf /AU 1**| 
|오류 보고를 사용 하도록 설정|현재 설정을 확인 하려면: **serverWerOptin /query** <br>자동으로 자세한 보고서를 보내려면: **serverWerOptin 자세한 /** <br>자동으로 요약 보고서를 보내려면: **serverWerOptin /summary** <br>오류 보고를 사용 하지 않도록 설정: **serverWerOptin /disable**|
|사용자 환경 개선 프로그램 (ceip 사용자)에 참여|현재 설정을 확인 하려면: **serverCEIPOptin /query** <br>CEIP 사용 하도록 설정: **serverCEIPOptin 같습니다.** <br>CEIP 사용 하지 않도록 설정: **serverCEIPOptin /disable**|

### 서비스, 프로세스 및 성능

|작업|명령| 
|----|-------|
|실행 중인 서비스 나열|**sc 쿼리** 또는 **순 시작**| 
|서비스 시작|**sc \<service name\ 시작 >** 또는 **net \<service name\ 시작 >**| 
|서비스를 중지 합니다.|**sc 중지 \<service name\ >** 또는 **net 중지 \<service name\ >**| 
|응용 프로그램과 관련 된 프로세스를 실행 중인 목록을 검색합니다|**tasklist**||프로세스를 강제로 중지|**Tasklist** 검색 프로세스 ID (PID)를 실행 한 다음 실행 **taskkill /PID \<process ID\ >**|
|작업 관리자를 시작 합니다.|**taskmgr**| 
|만들기 및 이벤트 추적 세션 및 성능 로그 관리|카운터, 추적, 구성 데이터 수집 또는 API를 만드는: **logman ceate** <br>쿼리 데이터 수집기 속성: **logman 쿼리** <br>시작 하거나 데이터 수집을 중지 하려면: **logman start\ | 중지** <br>수집기는 삭제: **logman delete** <br> 수집기의 속성을 업데이트할: **logman 업데이트** <br>XML 파일에서 데이터 수집기 집합을 가져오거나 XML 파일로 내보낼: **logman import\ | 내보내기**|

### 이벤트 로그

|작업|명령| 
|----|-------|
|이벤트 로그 목록|**wevtutil el**| 
|지정된 된 로그에서 이벤트를 쿼리 합니다.|**wevtutil qe /f:text \ < 이름 \ 로그 >**| 
|이벤트 로그 내보내기|**wevtutil epl \ < 이름 \ 로그 >**| 
|이벤트 로그 지우기|**wevtutil cl \ < 이름 \ 로그 >**| 


### 디스크 및 파일 시스템

|작업|명령|
|----|-------|
|디스크 파티션을 관리합니다|실행 명령의 전체 목록은 **diskpart /?**|  
|RAID 소프트웨어 관리|실행 명령의 전체 목록은 **diskraid /?**|  
|볼륨 탑재 지점을 관리합니다|실행 명령의 전체 목록은 **mountvol /?**| 
|볼륨 조각|실행 명령의 전체 목록은 **defrag /?**|  
|NTFS 파일 시스템 볼륨으로 변환|**변환 \ < 볼륨 letter\ > /fs: ntfs**| 
|파일 압축|실행 명령의 전체 목록은 **compact /?**|  
|열린 파일 관리|실행 명령의 전체 목록은 **openfiles /?**|  
|VSS 폴더 관리|실행 명령의 전체 목록은 **vssadmin /?**| 
|파일 시스템 관리|실행 명령의 전체 목록은 **fsutil /?**||파일 서명 확인|**서명 확인 /?**| 
|파일 또는 폴더의 소유권 가져오기|실행 명령의 전체 목록은 **icacls /?**| 
 
### 하드웨어

|작업|명령| 
|----|-------|
|새 하드웨어 장치용 드라이버 추가|드라이버 폴더 %homedrive%\\\ < 드라이버 folder\ >에 복사 합니다. 실행 **pnputil-i-%homedrive%\\\<driver folder\ > \\\<driver\ >.inf**|
|하드웨어 장치용 드라이버를 제거 합니다.|로드 된 드라이버 목록, 실행 **sc 쿼리 형식 드라이버 =** 합니다. 그러고 나 서 **sc 삭제 \<service_name\ >**|
