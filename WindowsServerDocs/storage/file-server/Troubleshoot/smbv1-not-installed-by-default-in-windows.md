---
title: SMBv1는 Windows 10 버전 1709, Windows Server 버전 1709 이상 버전에서 기본적으로 설치 되지 않습니다.
description: Windows 10의 SMBv1 프로토콜의 동작에 대해 설명 합니다 .이 업데이트 및 Windows Server 버전 1709 이상 버전
author: Deland-Han
manager: dcscontentpm
audience: ITPro
ms.topic: article
ms.author: delhan
ms.date: 12/25/2019
ms.openlocfilehash: 27869820e49257d059d124bac3f515ac91fef7b0
ms.sourcegitcommit: 30afd51d74cb6472720fb13ec47d80cf42b20c27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/25/2020
ms.locfileid: "80272319"
---
# <a name="smbv1-is-not-installed-by-default-in-windows-10-version-1709-windows-server-version-1709-and-later-versions"></a>SMBv1는 Windows 10 버전 1709, Windows Server 버전 1709 이상 버전에서 기본적으로 설치 되지 않습니다.

## <a name="summary"></a>요약

Windows 10의 작성자 업데이트 및 Windows Server, 버전 1709 (RS3) 이상 버전에서 서버 메시지 블록 버전 1 (SMBv1) 네트워크 프로토콜은 더 이상 기본적으로 설치 되지 않습니다. 2007 년부터 시작 하 여 SMBv2 이상 프로토콜에 의해 대체 되었습니다. Microsoft는 2014에서 SMBv1 프로토콜을 공개적으로 사용 하지 않습니다. 

SMBv1는 Windows 10의 Windows 10 크리에이터 업데이트 및 Windows Server 버전 1709 (RS3)에서 다음과 같은 동작을 수행 합니다. 
 
- 이제 SMBv1에는 클라이언트 및 서버 하위 기능이 따로 제거 될 수 있습니다.    
- Windows 10 Enterprise 및 Windows 10 교육에는 새로 설치한 후 기본적으로 SMBv1 클라이언트 또는 서버가 더 이상 포함 되지 않습니다.    
- Windows Server 2016에는 새로 설치한 후 기본적으로 SMBv1 클라이언트 또는 서버가 더 이상 포함 되지 않습니다.    
- Windows 10 Home 및 Windows 10 Professional은 새로 설치한 후 기본적으로 SMBv1 서버를 더 이상 포함 하지 않습니다.    
- Windows 10 Home 및 Windows 10 Professional은 새로 설치한 후에도 기본적으로 SMBv1 클라이언트를 포함 합니다. SMBv1 클라이언트가 전체 15 일 동안 사용 되지 않는 경우 (컴퓨터를 해제 하는 경우 제외) 자동으로 자동으로 제거 됩니다.    
- Windows 10 Home 및 Windows 10 Professional의 전체 업그레이드 및 Insider 항공편은 처음에 SMBv1를 자동으로 제거 하지 않습니다. SMBv1 클라이언트나 서버를 총 15 일 동안 사용 하지 않으면 (컴퓨터가 꺼진 시간 제외) 각각 자동으로 제거 됩니다.     
- Windows 10 Enterprise 및 Windows 10 교육용 버전의 전체 업그레이드 및 Insider 항공편은 SMBv1을 자동으로 제거 하지 않습니다. 관리자는 이러한 관리 되는 환경에서 SMBv1 제거를 결정 해야 합니다. Windows 10 버전 1809 (RS5) 이상 버전에서 관리자는 "SMB 1.0/CIFS 자동 제거" 기능을 설정 하 여 SMBv1 자동 제거를 활성화할 수 있습니다.    
- 15 일 후 SMBv1 자동 제거는 일회성 작업입니다. 관리자가 SMBv1를 다시 설치 하는 경우 추가 시도는 제거 되지 않습니다.
- SMB 버전 2.02, 2.1, 3.0, 3.02 및 3.1.1 기능은 기본적으로 SMBv2 이진 파일의 일부로 완전히 지원 되 고 포함 되어 있습니다.    
- 컴퓨터 브라우저 서비스는 SMBv1를 사용 하므로 SMBv1 클라이언트나 서버가 제거 되 면 서비스가 제거 됩니다. 즉, Explorer Networkcan 레거시 NetBIOS 데이터 그램 검색 방법을 통해 Windows 컴퓨터를 더 이상 표시할 수 없습니다.    
- SMBv1는 Windows 10 및 Windows Server 2016의 모든 버전에서 계속 다시 설치할 수 있습니다.    
 
  > [!NOTE]
  > Windows 10, 버전 1803 (RS4) Professional은 Windows 10, 버전 1703 (RS2) 및 Windows 10 버전 1607 (RS1)와 동일한 방식으로 SMBv1를 처리 합니다. 이 문제는 Windows 10 버전 1809 (RS5)에서 해결 되었습니다. 여전히 SMBv1를 수동으로 제거할 수 있습니다. 그러나 다음 시나리오에서는 15 일 후 Windows가 자동으로 SMBv1를 제거 하지 않습니다. 
 
-  Windows 10 버전 1803을 새로 설치 합니다.     
-  Windows 10, 버전 1709로 먼저 업그레이드 하지 않고 windows 10, 버전 1607 또는 Windows 10, 버전 1703을 Windows 10, 버전 1803로 직접 업그레이드할 수 있습니다.     
 
SMBv1만 지 원하는 장치에 연결 하려고 하거나 이러한 장치가 사용자에 게 연결 하려고 하면 다음 오류 메시지 중 하나가 표시 될 수 있습니다.     

```
You can't connect to the file share because it's not secure. This share requires the obsolete SMB1 protocol, which is unsafe and could expose your system to attack.
Your system requires SMB2 or higher. For more info on resolving this issue, see: https://go.microsoft.com/fwlink/?linkid=852747  
```

```
The specified network name is no longer available.
```

```
Unspecified error 0x80004005
```

```
System Error 64
```

```
The specified server cannot perform the requested operation.
```

```
Error 58
```    

다음 이벤트는 원격 서버에이 클라이언트의 SMBv1 연결이 필요 하지만 클라이언트에서 SMBv1가 제거 되거나 사용 하지 않도록 설정 된 경우에 나타납니다.

```
Log Name:      Microsoft-Windows-SmbClient/Security
 Source:        Microsoft-Windows-SMBClient
 Date:          Date/Time
 Event ID:      32002
 Task Category: None
 Level:         Info
 Keywords:      (128)
 User:          NETWORK SERVICE
 Computer:      junkle.contoso.com
 Description:
 The local computer received an SMB1 negotiate response. 

Dialect: 
SecurityMode 
Server name: 

Guidance: 
SMB1 is deprecated and should not be installed nor enabled. For more information, see https://go.microsoft.com/fwlink/?linkid=852747.
```

```
Log Name:      Microsoft-Windows-SmbClient/Security
 Source:        Microsoft-Windows-SMBClient
 Date:          Date/Time
 Event ID:      32000
 Task Category: None
 Level:         Info
 Keywords:      (128)
 User:          NETWORK SERVICE
 Computer:      junkle.contoso.com
 Description: 
SMB1 negotiate response received from remote device when SMB1 cannot be negotiated by the local computer. 
Dialect: 
Server name: 

Guidance: 
The client has SMB1 disabled or uninstalled. For more information: https://go.microsoft.com/fwlink/?linkid=852747.     
```

이러한 장치는 Windows를 실행할 가능성이 없습니다. 이전 버전의 Linux, Samba 또는 기타 타사 소프트웨어를 실행 하 여 SMB 서비스를 제공할 가능성이 높습니다. 이러한 버전의 Linux와 Samba는 더 이상 지원 되지 않는 경우가 많습니다. 

> [!NOTE]
> Windows 10, 버전 1709을 "가를 크리에이터 업데이트" 라고도 합니다.   

## <a name="more-information"></a>자세한 내용

이 문제를 해결 하려면 SMBv1만 지 원하는 제품의 제조업체에 문의 하 고 SMBv 2.02 이상 버전을 지 원하는 소프트웨어 또는 펌웨어 업데이트를 요청 하십시오. 알려진 공급 업체의 최신 목록과 SMBv1 요구 사항은 다음 Windows 및 Windows Server Storage 엔지니어링 팀 블로그 문서를 참조 하세요. 

[SMBv1 제품 클리어 링](https://techcommunity.microsoft.com/t5/Storage-at-Microsoft/SMB1-Product-Clearinghouse/ba-p/426008) 
#### <a name="leasing-mode"></a>임대 모드

Oplock를 사용 하지 않도록 설정 하는 요구 사항과 같이 레거시 소프트웨어 동작에 대 한 응용 프로그램 호환성을 제공 하기 위해 SMBv1가 필요한 경우 Windows에서는 임대 모드 라고 하는 새 SMB 공유 플래그를 제공 합니다. 이 플래그는 공유에서 임대 및 oplock와 같은 최신 SMB 의미 체계를 사용 하지 않도록 설정할지 여부를 지정 합니다.

Oplock 또는 임대를 사용 하지 않고 공유를 지정 하 여 레거시 응용 프로그램이 SMBv2 이상 버전에서 작동 하도록 할 수 있습니다. 이렇게 하려면 **new-smbshare** 또는 **new-smbshare** PowerShell Cmdlet을 **-LeasingMode None** 매개 변수와 함께 사용 합니다.

> [!NOTE]
> 이 옵션은 공급 업체에 필요한 경우 타사 응용 프로그램에서 레거시 지원을 위해 필요한 공유 에서만 사용 해야 합니다. 스케일 아웃 파일 서버에서 사용 되는 사용자 데이터 공유 또는 CA 공유에 대해 임대 모드를 지정 하지 마십시오. 이는 oplock 및 임대 제거로 인해 대부분의 응용 프로그램에서 불안정 및 데이터가 손상 되기 때문입니다. 임대 모드는 공유 모드 에서만 작동 합니다. 모든 클라이언트 운영 체제에서 사용할 수 있습니다.

#### <a name="explorer-network-browsing"></a>탐색기 네트워크 검색

컴퓨터 브라우저 서비스는 SMBv1 프로토콜을 사용 하 여 Windows 탐색기 네트워크 노드 ("네트워크 환경"이 라고도 함)를 채웁니다. 이 레거시 프로토콜은 더 이상 사용 되지 않으며, 라우팅되지 않으며, 보안이 제한 됩니다. SMBv1 없이 서비스를 사용할 수 없으므로 동시에 제거 됩니다.

그러나 여전히 탐색기 네트워크 입력 home 및 small business workgroup environment를 사용 하 여 Windows 기반 컴퓨터를 찾아야 하는 경우 더 이상 SMBv1를 사용 하지 않는 Windows 기반 컴퓨터에서 다음 단계를 따를 수 있습니다. 
 
1. "함수 검색 공급자 호스트" 및 "함수 검색 리소스 게시" 서비스를 시작한 다음 **자동 (지연 된 시작)** 으로 설정 합니다.

2. 탐색기 네트워크를 열면 메시지가 표시 되 면 네트워크 검색을 사용 하도록 설정 합니다.    
 
이러한 설정이 있는 서브넷 내의 모든 Windows 장치가 검색을 위해 네트워크에 표시 됩니다. 이는 WS 검색 프로토콜을 사용 합니다. Windows 장치가 표시 된 후에도이 찾아보기 목록에 해당 장치가 표시 되지 않으면 다른 공급 업체 및 제조업체에 문의 하십시오. 이 프로토콜을 사용 하지 않도록 설정 하거나 SMBv1만 지원할 수 있습니다.

> [!NOTE]
> 장치를 검색 하 고 검색 해야 하는이 기능을 사용 하도록 설정 하는 대신 드라이브와 프린터를 매핑하는 것이 좋습니다. 매핑된 리소스를 쉽게 찾을 수 있고, 교육을 줄이고, 사용 하기 더 안전 합니다. 이러한 리소스는 그룹 정책를 통해 자동으로 제공 되는 경우에 특히 그렇습니다. 관리자는 IP 주소, Active Directory Domain Services (AD DS), Bonjour, Mdn, uPnP 등을 사용 하 여 레거시 컴퓨터 브라우저 서비스가 아닌 방법으로 위치에 대 한 프린터를 구성할 수 있습니다.

이러한 해결 방법을 사용할 수 없거나 응용 프로그램 제조업체에서 지원 되는 버전의 SMB를 제공할 수 없는 경우 [Windows에서 SMBv1, SMBv2 및 SMBv3를 검색, 사용 및 사용 하지 않도록 설정 하는 방법](detect-enable-and-disable-smbv1-v2-v3.md)의 단계에 따라 SMBv1을 수동으로 다시 사용 하도록 설정할 수 있습니다.

> [!IMPORTANT]
> SMBv1를 다시 설치 하지 않는 것이 좋습니다. 이는 이전 프로토콜에 랜 섬 웨어 및 기타 맬웨어에 대 한 알려진 보안 문제가 있기 때문입니다.  

#### <a name="windows-server-best-practices-analyzer-messaging"></a>Windows Server 모범 사례 분석기 메시징

Windows Server 2012 이상 서버 운영 체제에는 파일 서버용 BPA (모범 사례 분석기)가 포함 되어 있습니다. SMB1을 제거 하기 위한 올바른 온라인 지침을 수행한 경우이 BPA를 실행 하면 모순 되는 경고 메시지가 반환 됩니다.

    Title: The SMB 1.0 file sharing protocol should be enabled
    Severity: Warning
    Date: 3/25/2020 12:38:47 PM
    Category: Configuration
    Problem: The Server Message Block 1.0 (SMB 1.0) file sharing protocol is disabled on this file server.
    Impact: SMB not in a default configuration, which could lead to less than optimal behavior.
    Resolution: Use Registry Editor to enable the SMB 1.0 protocol.

이 특정 BPA 규칙의 지침을 무시 해야 합니다. 사용 되지 않습니다. 반복: SMB 1.0을 사용 하지 않습니다.

## <a name="references"></a>참조

[SMB1 사용 중지](https://aka.ms/stopusingsmb1)
