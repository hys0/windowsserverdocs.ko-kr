---
title: DirectAccess 문제 해결
description: 이 항목에서는 Windows Server 2016의 DirectAccess 배포 문제 해결에 대 한 정보를 제공 합니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 61040e19-5960-4eb0-b612-d710627988f7
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 6f969dfdaa2932990619c1e545f77615796e7104
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80314842"
---
# <a name="troubleshooting-directaccess"></a>DirectAccess 문제 해결

>적용 대상: Windows Server(반기 채널), Windows Server 2016

DirectAccess (원격 액세스) 문제를 해결 하려면 다음 단계를 수행 합니다.  
  
|||  
|-|-|  
|**문제**|**해결 방법**|  
|원격 액세스 관리 콘솔에서 DirectAccess 구성을 표시할 수 없습니다.|**누락 된 구성 정보를 복원 하려면**<br />-멀티 사이트 배포 문제를 해결 하는 경우 진입점에 가장 가까운 도메인 컨트롤러를 사용할 수 있는지 확인 합니다.<br />- **Set-daentrypointdc** cmdlet을 사용 하 여 진입점에 가장 가까운 도메인 컨트롤러의 이름을 검색 합니다. 도메인 컨트롤러가 실행 되 고 있지 않은 경우 **set-daentrypointdc** cmdlet을 사용 하 여 다른 도메인 컨트롤러를 가리킵니다.<br />-서버에서 관리자 권한 명령 프롬프트의 **gpresult** 를 실행 하 여 서버가 DirectAccess 그룹 정책 개체를 가져오는지 확인 합니다.<br />-UI (사용자 인터페이스) 로깅을 사용 하도록 설정 합니다.<br />-다음 명령을 사용 하 여 Windows PowerShell 로깅을 시작 합니다.<pre>logman create trace ETWTrace -ow -o c:\ETWTrace.etl -p {AAD4C46D-56DE-4F98-BDA2-B5EAEBDD2B04} 0xffffffffffffffff 0xff -nb 16 16 -bs 1024 -mode 0x2 -max 2048 -ets <br />logman update trace ETWTrace -p {62DFF3DA-7513-4FCA-BC73-25B111FBB1DB} 0xffffffffffffffff 0xff -ets</pre><repro>-사용자 인터페이스를 닫았다가 다시 엽니다.<br />-Windows Powershell 로깅을 사용 하지 않도록 설정 합니다. 이벤트 추적 로그 파일을 수집 합니다. 또한 **% windir%/추적** 폴더의 모든 로그를 수집 합니다.|  
|DirectAccess 구성 적용 실패|**DirectAccess 구성을 새로 고치려면**<br />-멀티 사이트 배포 문제를 해결 하는 경우 진입점에 가장 가까운 도메인 컨트롤러를 사용할 수 있는지 확인 합니다.<br />- **Set-daentrypointdc** cmdlet을 사용 하 여 진입점에 가장 가까운 도메인 컨트롤러의 이름을 검색 합니다. 도메인 컨트롤러가 실행 되 고 있지 않은 경우 **set-daentrypointdc** cmdlet을 사용 하 여 다른 도메인 컨트롤러를 가리킵니다.<br />-다음 명령을 사용 하 여 Windows Powershell 로깅을 시작 합니다.<br /><pre>logman create trace ETWTrace -ow -o c:\ETWTrace.etl -p {AAD4C46D-56DE-4F98-BDA2-B5EAEBDD2B04} 0xffffffffffffffff 0xff -nb 16 16 -bs 1024 -mode 0x2 -max 2048 -ets<br />logman update trace ETWTrace -p {62DFF3DA-7513-4FCA-BC73-25B111FBB1DB} 0xffffffffffffffff 0xff -ets</pre>    <repro><br />- **적용**을 클릭 합니다.<br />-오류가 발생 한 후 Windows Powershell 로깅을 사용 하지 않도록 설정 하 고 이벤트 추적 로그를 수집 합니다.|  
|DirectAccess가 구성 되었지만 클라이언트에서 내부 리소스에 연결할 수 없습니다.|**클라이언트 연결 문제를 해결 하려면**<br />-원격 액세스 관리 콘솔에서 **작업 상태** 탭을 클릭 하 고 모든 구성 요소가 녹색 아이콘을 표시 하는지 확인 합니다. 그렇지 않은 경우 오류 세부 정보를 확인 하 고 해결 단계를 따릅니다.<br />-BPA (원격 액세스 서버 모범 사례 분석기)를 실행 합니다. 경고나 오류가 있는 경우 해결 단계를 수행 하 여 문제를 해결 합니다.|  
|멀티 사이트 구성과 관련 된 문제가 발생 하는 경우 (예: 멀티 사이트를 사용 하도록 설정, 진입점 추가 또는 진입점에 대 한 도메인 컨트롤러 설정)|[멀티 사이트 배포 문제 해결](https://technet.microsoft.com/library/jj554657(v=ws.11).aspx)의 단계를 따릅니다.|  
|대시보드의 구성 상태 타일에 경고 또는 오류가 표시 됩니다.|[원격 액세스 서버의 구성 배포 상태 모니터링](https://technet.microsoft.com/library/jj574221(v=ws.11).aspx)의 단계를 따릅니다.|  
|부하 분산 구성과 관련 된 문제가 발생 합니다. 예를 들어 부하 분산을 사용 하도록 설정 하는 경우 구성이 실패 하거나 클러스터에서 서버를 추가 하거나 제거할 때 문제가 발생 합니다.|부하 분산을 사용 하도록 설정 하거나 노드를 추가 하 고, **적용**을 클릭 했을 때 구성이 새로 고쳐 졌으 나 서버에서 클러스터가 제대로 구성 되지 않은 경우 **cmd.exe/c "reg add HKLM\SYSTEM\CurrentControlSet\Services\RaMgmtSvc\Parameters/F/v debugflag/t REG_DWORD/d" "0xffffffff" ""** 를 실행 하 여 새 서버에서 사용자 인터페이스 로그를 수집 합니다.|  
|작업 상태는 상황을 해결 하기 위해 다음 단계를 수행 하는 동안 오류 또는 경고를 표시 합니다.|작업 상태에 잘못 된 정보가 표시 된 경우 (예: 오류를 수정한 후에도):<br /><br />-레지스트리 키 **cmd.exe/c "reg add HKLM\SYSTEM\CurrentControlSet\Services\RaMgmtSvc\Parameters/f/V EnableTracing/t REG_DWORD/d" "5" ""** 를 사용 하도록 설정 합니다.<br />-작업 상태를 새로 고치고 **% windir%/추적**에서 로그를 수집 합니다.|  
|Windows 8 이상 DirectAccess 클라이언트 컴퓨터는 DirectAccess 연결 상태에 "인터넷 없음"을 보고 하 고, NCSI (네트워크 연결 상태 표시기)는 제한 된 연결을 보고 합니다.|이는 DirectAccess 구성에서 강제 터널링을 사용 하는 경우에 발생할 수 있으며,이로 인해 IPHTTPS만 사용 됩니다. 이 문제를 해결 하기 위해 프록시 서버를 만들고 구성할 수 있습니다. 그러면 NCSI는 프록시 서버를 사용 하 여 인터넷 연결 확인을 수행 합니다. 다음 절차를 사용 하 여 NRPT (이름 확인 정책 테이블)에 정적 프록시를 추가 하는 것이 좋습니다.<br /><br />이 절차의 명령을 실행 하기 전에 모든 도메인 이름, 컴퓨터 이름 및 기타 Windows PowerShell 명령 변수를 배포에 적합 한 값으로 바꾸어야 합니다.<br /><br />**NRPT 규칙에 대 한 정적 프록시 구성**<br />1. "."를 표시 합니다. NRPT 규칙: `Get-DnsClientNrptRule -GpoName "corp.example.com\DirectAccess Client Settings" -Server <DomainControllerNetBIOSName>`<br />2. "."의 이름 (GUID)을 확인 합니다. NRPT 규칙. 이름 (GUID)은 **DA-{..}** 로 시작 해야 합니다.<br />3. "."에 대 한 프록시를 설정 합니다. **Proxy.corp.example.com:8080**에 대 한 NRPT 규칙: `Set-DnsClientNrptRule -Name "DA-{..}" -Server <DomainControllerNetBIOSName> -GPOName "corp.example.com\DirectAccess Client Settings" -DAProxyServerName "proxy.corp.example.com:8080" -DAProxyType "UseProxyName"`<br />4. "."를 표시 합니다. `Get-DnsClientNrptRule`를 실행 하 여 NRPT 규칙을 다시 만들고 **Proxyfqdn: 포트가** 이제 올바르게 구성 되었는지 확인 합니다.<br />5. 클라이언트가 내부적으로 연결 된 경우 DirectAccess 클라이언트에서 `gpupdate /force`를 실행 하 여 그룹 정책를 새로 고친 다음 `Get-DnsClientNrptPolicy`를 사용 하 여 NRPT를 표시 하 고 "." 규칙이 **Proxyfqdn: port**를 표시 하는지 확인 합니다.|  
  


