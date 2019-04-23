---
title: DirectAccess 문제 해결
description: 이 항목에서는 Windows Server 2016에서 DirectAccess 배포 문제 해결에 대 한 정보를 제공 합니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 61040e19-5960-4eb0-b612-d710627988f7
ms.author: pashort
author: shortpatti
ms.openlocfilehash: ec725eea286c359461b0f4a7b8763b97464e7067
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59867094"
---
# <a name="troubleshooting-directaccess"></a>DirectAccess 문제 해결

>적용 대상: Windows Server (반기 채널), Windows Server 2016

원격 액세스 (DirectAccess) 문제를 해결 하려면 다음이 단계를 수행 합니다.  
  
|||  
|-|-|  
|**문제점**|**해결 방법**|  
|원격 액세스 관리 콘솔의 DirectAccess 구성이 표시 수 없는 경우|**누락 된 구성 정보를 복원 하려면**<br />-멀티 사이트 배포를 해결 하는 경우에 진입점으로 가장 가까운 도메인 컨트롤러를 사용할 수 있는지를 확인 합니다.<br />-을 사용 합니다 **Get DAEntrypointDC** 진입점으로 가장 가까운 도메인 컨트롤러의 이름을 검색 하기 위한 cmdlet입니다. 도메인 컨트롤러를 실행 하지 않는 경우 사용 합니다 **Set-daentrypointdc** cmdlet은 다른 도메인 컨트롤러를 가리키도록 합니다.<br />-Run **gpresult** DirectAccess 그룹 정책 개체를 가져오는 서버는 서버에서 관리자 권한 명령 프롬프트에서.<br />-사용자 인터페이스 (UI) 로깅을 사용 하도록 설정 합니다.<br />-Windows PowerShell 로깅 시작 하려면 다음 명령을 사용 합니다.<pre>logman create trace ETWTrace -ow -o c:\ETWTrace.etl -p {AAD4C46D-56DE-4F98-BDA2-B5EAEBDD2B04} 0xffffffffffffffff 0xff -nb 16 16 -bs 1024 -mode 0x2 -max 2048 -ets <br />logman update trace ETWTrace -p {62DFF3DA-7513-4FCA-BC73-25B111FBB1DB} 0xffffffffffffffff 0xff -ets</pre><repro>-사용자 인터페이스를 닫고 닫습니다.<br />-Windows Powershell 로깅 사용 하지 않도록 설정 합니다. 이벤트 추적 로그 파일을 수집 합니다. 또한에서 모든 로그를 수집 합니다 **%windir%/tracing** 폴더입니다.|  
|DirectAccess 구성이 적용 실패|**DirectAccess 구성을 새로 고치려면**<br />-멀티 사이트 배포를 해결 하는 경우에 진입점으로 가장 가까운 도메인 컨트롤러를 사용할 수 있는지를 확인 합니다.<br />-을 사용 합니다 **Get DAEntrypointDC** 진입점으로 가장 가까운 도메인 컨트롤러의 이름을 검색 하기 위한 cmdlet입니다. 도메인 컨트롤러를 실행 하지 않는 경우 사용 합니다 **Set-daentrypointdc** cmdlet은 다른 도메인 컨트롤러를 가리키도록 합니다.<br />-Windows Powershell 로깅 시작 하려면 다음 명령을 사용 합니다.<br /><pre>logman create trace ETWTrace -ow -o c:\ETWTrace.etl -p {AAD4C46D-56DE-4F98-BDA2-B5EAEBDD2B04} 0xffffffffffffffff 0xff -nb 16 16 -bs 1024 -mode 0x2 -max 2048 -ets<br />logman update trace ETWTrace -p {62DFF3DA-7513-4FCA-BC73-25B111FBB1DB} 0xffffffffffffffff 0xff -ets</pre>    <repro><br />-클릭 **적용**합니다.<br />-오류 발생 후 Windows Powershell 로깅 사용 하지 않도록 설정 하 고 이벤트 추적 로그를 수집 합니다.|  
|DirectAccess가 구성 되어 있지만 클라이언트는 내부 리소스에 연결할 수 없습니다.|**클라이언트 연결 문제를 해결 하려면**<br />-을 클릭 합니다 **작업 상태** 원격 액세스 관리 콘솔에서 탭 및 모든 구성 요소가 녹색 아이콘 표시 되는지 확인 합니다. 그렇지 않은 경우 오류 세부 정보를 확인 하 고 해결 단계를 수행 합니다.<br />-원격 액세스 서버 Best Practices Analyzer (BPA)를 실행 합니다. 모든 경고 또는 오류가 있는 경우 문제를 해결 하려면 해결 단계를 따릅니다.|  
|멀티 사이트 구성 (예를 들어,를 추가, 멀티 사이트 진입점을 사용 하도록 설정 또는 진입점에 대 한 도메인 컨트롤러 설정)와 관련 된 문제를 발생 합니다.|단계를 따릅니다 [멀티 사이트 배포 문제 해결](https://technet.microsoft.com/library/jj554657(v=ws.11).aspx)합니다.|  
|구성 상태 타일을 대시보드에 경고 또는 오류를 보여 줍니다.|단계를 따릅니다 [원격 액세스 서버의 구성 배포 상태를 모니터링할](https://technet.microsoft.com/library/jj574221(v=ws.11).aspx)합니다.|  
|부하 분산 (예: 구성 실패 하면 부하 분산을 사용 하도록 설정 하거나 추가 하거나 클러스터에서 서버를 제거 하는 경우 문제가 있는 경우)를 구성 하는 데 관련 된 발생 문제|부하 분산 또는 추가 노드를 사용 하도록 설정 된 경우 구성을 클릭 했을 때 새로 고칠 **적용**, 클러스터 서버에서 다음 명령을 올바르게 구성 하지 않은 하지만: **cmd.exe /c "reg add HKLM\ SYSTEM\CurrentControlSet\Services\RaMgmtSvc\Parameters /f /v DebugFlag /t REG_DWORD /d "" 0xffffffff"" "** 수집할 사용자 인터페이스 새 서버에 기록 합니다.|  
|작업 상태가 오류 또는 경고는 상황을 해결 하려면 다음 단계 후|작업 상태 (예: 오류도 후 수정) 잘못 된 정보가 표시 됩니다.<br /><br />-   Enable the registry key **cmd.exe /c "reg add HKLM\SYSTEM\CurrentControlSet\Services\RaMgmtSvc\Parameters /f /v EnableTracing /t REG_DWORD /d ""5"" "**.<br />-작업 상태를 새로 고치고에서 로그 수집 **%windir%/tracing**합니다.|  
|Windows 8 및 이후 버전의 DirectAccess 클라이언트 컴퓨터 "No Internet" DirectAccess 연결에 대 한 상태 보고 및 네트워크 연결 상태 표시기 (NCSI) 제한 된 연결을 보고 합니다.|DirectAccess 구성에서 강제 터널링을 사용 하 고이 인해 IPHTTPS만 사용 되는 경우 발생할 수 있습니다. 이 문제를 해결 하려면 수 만들고 프록시 서버를 구성 합니다. NCSI 다음 프록시 서버를 사용 하 여 인터넷 연결 검사를 수행 합니다. 추가한 정적 프록시에는 NRPT 이름 확인 정책 테이블 () 다음 절차를 사용 하는 것이 좋습니다.<br /><br />이 절차의 명령은 실행 하기 전에 배포에 대 한 적절 한 값을 사용 하 여 모든 도메인 이름, 컴퓨터 이름 및 다른 Windows PowerShell 명령 변수를 대체를 확인 합니다.<br /><br />**정적 프록시는 NRPT 규칙에 대 한 구성**<br />1.  표시 된 "." NRPT 규칙: `Get-DnsClientNrptRule -GpoName "corp.example.com\DirectAccess Client Settings" -Server <DomainControllerNetBIOSName>`<br />2.  이름 (GUID)를 참고 합니다 "." NRPT 규칙입니다. 이름 (GUID)로 시작 해야 **DA-{0}.}**<br />3.  에 대 한 프록시를 설정 합니다 "." 에 대 한 NRPT 규칙이 **proxy.corp.example.com:8080**:  `Set-DnsClientNrptRule -Name "DA-{..}" -Server <DomainControllerNetBIOSName> -GPOName "corp.example.com\DirectAccess Client Settings" -DAProxyServerName "proxy.corp.example.com:8080" -DAProxyType "UseProxyName"`<br />4.  표시 된 "." 다시 실행 하 여 NRPT 규칙이 `Get-DnsClientNrptRule`를 확인 **ProxyFQDN:port** 올바르게 구성 되었습니다.<br />5.  실행 하 여 그룹 정책 새로 고침 `gpupdate /force` DirectAccess 클라이언트에서 클라이언트는 내부적으로 연결 되 면 다음 표시는 NRPT를 사용 하 여 `Get-DnsClientNrptPolicy` 하 고 있는지 확인 합니다 "." 표시 규칙 **ProxyFQDN:port**합니다.|  
  


