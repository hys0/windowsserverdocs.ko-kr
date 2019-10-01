---
title: Windows Server Essentials에서 연결
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.custom: na
ms.date: 05/07/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 149a5d34-43b7-4b9e-99e7-9f2294ab9ddb
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 04d09574046474da5bee4437628ade9646cf58ca
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70866939"
---
# <a name="get-connected-in-windows-server-essentials"></a>Windows Server Essentials에서 연결

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

 Connector 소프트웨어를 사용하여 컴퓨터를 Windows Server Essentials에 연결할 수 있습니다. Connector 소프트웨어는 서버에 컴퓨터 연결 마법사를 사용하여 서버에 컴퓨터를 연결할 때 설치됩니다. **Http:/\>/< servername/connect**를 입력 하 여이 마법사를 시작할 수 있습니다. 여기서 **< servername\>**  은 서버 이름입니다.  

 항목 내용  


-   [서버에 컴퓨터 연결 준비](Get-Connected-in-Windows-Server-Essentials.md#BKMK_A)  

-   [Connector 소프트웨어를 사용 하 여 서버에 컴퓨터 연결](Get-Connected-in-Windows-Server-Essentials.md#BKMK_B)  

-   [실행 패드 사용](Get-Connected-in-Windows-Server-Essentials.md#BKMK_C)  

-   [서버에 컴퓨터 연결 준비](Get-Connected-in-Windows-Server-Essentials.md#BKMK_A)  

-   [Connector 소프트웨어를 사용 하 여 서버에 컴퓨터 연결](Get-Connected-in-Windows-Server-Essentials.md#BKMK_B)  

-   [실행 패드 사용](Get-Connected-in-Windows-Server-Essentials.md#BKMK_C)  


##  <a name="BKMK_A"></a>서버에 컴퓨터 연결 준비  
 이 섹션에서는 Connector 소프트웨어, Windows Server Essentials에서 지원되는 운영 체제, 서버에 컴퓨터를 연결하기 전에 완료해야 하는 필수 구성 요소 작업, Connector 소프트웨어를 실행할 때 서버에서 컴퓨터에 적용하는 변경 사항에 대해 설명합니다.  


-   [커넥터 소프트웨어 개요](Get-Connected-in-Windows-Server-Essentials.md#BKMK_1)  

-   [서버에 컴퓨터를 연결 하기 위한 필수 구성 요소](Get-Connected-in-Windows-Server-Essentials.md#BKMK_2)  

-   [Mac 컴퓨터를 네트워크에 연결 하기 위한 필수 구성 요소](Get-Connected-in-Windows-Server-Essentials.md#BKMK_3)  

-   [클라이언트 컴퓨터에 대해 지원 되는 운영 체제](Get-Connected-in-Windows-Server-Essentials.md#BKMK_4)  

-   [서버에서 클라이언트 컴퓨터에 대해 수행 하는 변경 내용](Get-Connected-in-Windows-Server-Essentials.md#BKMK_5)  

-   [네트워크 사용자 이름 및 암호 정보](Get-Connected-in-Windows-Server-Essentials.md#BKMK_6)  

-   [서버 관리자 계정](Get-Connected-in-Windows-Server-Essentials.md#BKMK_7)  

-   [Windows 도메인에서 컴퓨터 제거](Get-Connected-in-Windows-Server-Essentials.md#BKMK_8)  

###  <a name="BKMK_1"></a>커넥터 소프트웨어 개요  
 Windows Server Essentials 운영 체제용 Connector 소프트웨어는 네트워크에 있는 컴퓨터를 Windows Server Essentials 서버에 연결합니다. 컴퓨터를 서버에 연결할 때 Connector 소프트웨어를 사용하여 컴퓨터를 자동으로 백업하고 상태를 모니터링할 수 있습니다. Connector 소프트웨어를 사용하여 Windows Server Essentials 서버를 구성하고 원격으로 관리할 수도 있습니다. Connector 소프트웨어는 클라이언트 컴퓨터를 서버에 연결할 때 설치됩니다. 클라이언트 컴퓨터를 Windows Server Essentials 서버에 연결하는 방법에 대한 자세한 내용은 이 항목의 뒷부분에 있는 [서버에 컴퓨터 연결](Get-Connected-in-Windows-Server-Essentials.md#BKMK_9)을 참조하세요.  

-   [커넥터 소프트웨어 개요](Get-Connected-in-Windows-Server-Essentials.md#BKMK_1)  

-   [서버에 컴퓨터를 연결 하기 위한 필수 구성 요소](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_2)  

-   [Mac 컴퓨터를 네트워크에 연결 하기 위한 필수 구성 요소](Get-Connected-in-Windows-Server-Essentials.md#BKMK_3)  

-   [클라이언트 컴퓨터에 대해 지원 되는 운영 체제](Get-Connected-in-Windows-Server-Essentials.md#BKMK_4)  

-   [서버에서 클라이언트 컴퓨터에 대해 수행 하는 변경 내용](Get-Connected-in-Windows-Server-Essentials.md#BKMK_5)  

-   [네트워크 사용자 이름 및 암호 정보](Get-Connected-in-Windows-Server-Essentials.md#BKMK_6)  

-   [서버 관리자 계정](Get-Connected-in-Windows-Server-Essentials.md#BKMK_7)  

-   [Windows 도메인에서 컴퓨터 제거](Get-Connected-in-Windows-Server-Essentials.md#BKMK_8)  

###  <a name="BKMK_1"></a>커넥터 소프트웨어 개요  
 Windows Server Essentials 운영 체제용 Connector 소프트웨어는 네트워크에 있는 컴퓨터를 Windows Server Essentials 서버에 연결합니다. 컴퓨터를 서버에 연결할 때 Connector 소프트웨어를 사용하여 컴퓨터를 자동으로 백업하고 상태를 모니터링할 수 있습니다. Connector 소프트웨어를 사용하여 Windows Server Essentials 서버를 구성하고 원격으로 관리할 수도 있습니다. Connector 소프트웨어는 클라이언트 컴퓨터를 서버에 연결할 때 설치됩니다. 클라이언트 컴퓨터를 Windows Server Essentials 서버에 연결하는 방법에 대한 자세한 내용은 이 항목의 뒷부분에 있는 [서버에 컴퓨터 연결](Get-Connected-in-Windows-Server-Essentials.md#BKMK_9)을 참조하세요.  


###  <a name="BKMK_2"></a>서버에 컴퓨터를 연결 하기 위한 필수 구성 요소  
 네트워크에 컴퓨터를 연결하기 전에 다음 요구 사항을 충족해야 합니다.  

-   Windows Server Essentials 설치가 완료되고 서버가 실행 중입니다. Connector 소프트웨어에서는 서버와 통신할 수 없으면 설치를 종료합니다.  


-   클라이언트 컴퓨터에서 지원되는 운영 체제를 실행 중입니다. 자세한 내용은 [클라이언트 컴퓨터에 대해 지원 되는 운영 체제](Get-Connected-in-Windows-Server-Essentials.md#BKMK_4)를 참조하세요.


-   클라이언트 컴퓨터는 인터넷에 올바르게 연결되어 있어야 합니다.  

-   Windows Server Essentials를 실행하는 서버와 같은 네트워크에 있는 클라이언트 컴퓨터가 해당 서버와 같은 IP 서브넷에 있습니다.  

-   클라이언트 컴퓨터에 .NET Framework 4.5가 설치되어 있습니다. Connector 소프트웨어에서 이 프로그램을 컴퓨터에 자동으로 설치합니다.  

-   클라이언트 컴퓨터가 다음 최소 시스템 요구 사항을 충족합니다.  

    -   1.4GHz 이상 프로세서  

    -   RAM 1GB 이상  

    -   사용 가능한 하드 드라이브 공간 1GB(설치 후에는 이 공간 부분이 사용 가능하게 됨)  

-   부팅 파티션(Windows 운영 체제를 설치한 디스크 파티션)은 NTFS 파일 시스템으로 포맷됩니다.  

-   컴퓨터 이름은 15자 이하여야 합니다.  

-   컴퓨터 이름은 밑줄(_)을 포함하지 않습니다.  

-   컴퓨터의 날짜 및 시간 설정이 서버의 설정에 맞춰집니다.  

-   클라이언트 컴퓨터는 항상 단일 Windows Server Essentials 서버에만 연결할 수 있습니다.  

-   이미 다른 Active Directory 도메인에 가입된 클라이언트 컴퓨터는 Windows Server Essentials 도메인에 가입할 수 없습니다.  

> [!NOTE]
> 
>  Windows server essentials 또는 Windows Server Essentials에 대 한 온-프레미스 클라이언트 배포에서는 컴퓨터를 Windows Server Essentials 도메인에 추가 하지 않고 서버에 연결할 수 있습니다. 이 방법은 모든 지원되는 클라이언트 운영 체제에서 사용할 수 있는 것은 아니며 그룹 정책 및 VPN(가상 사설망)과 같이 컴퓨터를 도메인에 연결해야 하는 기능은 사용할 수 없습니다. 요구 사항 및 지침은 [도메인에 가입 하지 않고 Windows Server Essentials 서버에 컴퓨터 연결](Get-Connected-in-Windows-Server-Essentials.md#BKMK_10)을 참조하세요.  

 Windows Server Essentials를 실행하는 서버에 컴퓨터를 연결하기 위한 단계별 지침은 [Connect computers to the server](Get-Connected-in-Windows-Server-Essentials.md#BKMK_9)을 참조하세요.  

>  Windows server essentials 또는 Windows Server Essentials에 대 한 온-프레미스 클라이언트 배포에서는 컴퓨터를 Windows Server Essentials 도메인에 추가 하지 않고 서버에 연결할 수 있습니다. 이 방법은 모든 지원되는 클라이언트 운영 체제에서 사용할 수 있는 것은 아니며 그룹 정책 및 VPN(가상 사설망)과 같이 컴퓨터를 도메인에 연결해야 하는 기능은 사용할 수 없습니다. 요구 사항 및 지침은 [도메인에 가입 하지 않고 Windows Server Essentials 서버에 컴퓨터 연결](Get-Connected-in-Windows-Server-Essentials.md#BKMK_10)을 참조하세요.  

 Windows Server Essentials를 실행하는 서버에 컴퓨터를 연결하기 위한 단계별 지침은 [Connect computers to the server](Get-Connected-in-Windows-Server-Essentials.md#BKMK_9)을 참조하세요.  


###  <a name="BKMK_3"></a>Mac 컴퓨터를 네트워크에 연결 하기 위한 필수 구성 요소  
 네트워크에 Mac 컴퓨터를 연결하기 전에 다음 요구 사항을 충족해야 합니다.  

-   서버 운영 체제 설치가 완료되고 서버가 실행 중입니다. Connector 소프트웨어에서는 서버와 통신할 수 없으면 설치하지 않습니다.  

-   컴퓨터에서 Mac OS X 10.5(Leopard) 이상을 실행하고 있습니다.  

-   컴퓨터가 서버와 같은 IP 서브넷에 있습니다.  

-   컴퓨터는 인터넷에 올바르게 연결되어 있어야 합니다.  

-   컴퓨터가 다음 최소 시스템 요구 사항을 충족하는지 확인합니다.  

    -   1.4GHz 이상 프로세서  

    -   RAM 1GB 이상  

    -   사용 가능한 하드 드라이브 공간 1GB(설치 후에는 이 공간 부분이 사용 가능하게 됨)  

-   클라이언트 컴퓨터는 항상 단일 서버에만 연결할 수 있습니다.  

###  <a name="BKMK_4"></a>클라이언트 컴퓨터에 대해 지원 되는 운영 체제  
 Windows Server Essentials에서는 모든 지원되는 클라이언트 컴퓨터에 대해 같은 기능 집합을 제공합니다. 이러한 기능에는 도메인 가입, 실행 패드 및 클라이언트 쪽 상태 알림이 포함됩니다.  

> [!IMPORTANT]
>  Windows Server Essentials에서는 Windows Home, Starter 또는 Media Center 버전을 실행하는 컴퓨터의 도메인 가입을 지원하지 않습니다. 또한 원격 웹 액세스를 사용하여 이러한 컴퓨터에 연결할 수 없습니다.  

#### <a name="windows-server-essentials"></a>Windows Server Essentials  
  이 섹션은 windows server essentials를 실행 하는 서버 또는 windows server Essentials Experience 역할이 설치 된 windows Server 2012 R2 Standard 또는 Windows Server 2012 R2 Datacenter를 실행 하는 서버에 적용 됩니다. 다음 컴퓨터 운영 체제가 지원됩니다.  

 **Windows 7 운영 체제**  

- Windows 7 Home Basic SP1 (x86 및 x64)  

- Windows 7 Home Premium SP1 (x86 및 x64)  

- Windows 7 Professional SP1 (x86 및 x64)  

- Windows 7 Ultimate SP1 (x86 및 x64)  

- Windows 7 Enterprise SP1 (x86 및 x64)  

- Windows 7 Starter SP1 (x86)  

  **Windows 8 운영 체제**  

- Windows 8  

- Windows 8 Pro  

- Windows 8 Enterprise  

  **운영 체제 Windows 8.1**  

- Windows 8.1  

- Windows 8.1 Pro  

- Windows 8.1 Enterprise  

  **Windows 10 운영 체제**  

- Windows 10  

- Windows 10 Pro  

- Windows 10 Enterprise  

- Windows 10 Education  

  **Mac 클라이언트 컴퓨터**  

- Mac OS X v10.5 Leopard  

- Mac OS X v10.6 Snow Leopard  

- Mac OS X v10.7 Lion  

- Mac OS X v10.8 Mountain Lion  

> [!NOTE]
>  Windows Server Essentials 대시보드에서 Mac 컴퓨터의 상태 및 백업 상태를 볼 수 있습니다. 그러나 대시보드에서 컴퓨터 백업을 구성하거나 백업을 시작할 수 없습니다. 또한 원격 웹 액세스를 사용하여 Mac 컴퓨터에 연결할 수 없습니다.  

#### <a name="windows-server-essentials"></a>Windows Server Essentials  
  이 섹션은 Windows Server Essentials를 실행 하는 서버에 적용 됩니다. 다음 컴퓨터 운영 체제가 지원됩니다.  

 **Windows 7 운영 체제**  

- Windows 7 Home Basic (x86 및 x64)  

- Windows 7 Home Premium (x86 및 x64)  

- Windows 7 Professional (x86 및 x64)  

- Windows 7 Ultimate (x86 및 x64)  

- Windows 7 Enterprise (x86 및 x64)  

- Windows 7 스타터 (x86)  

  **Windows 8 운영 체제**  

- Windows 8  

- Windows 8 Pro  

- Windows 8 Enterprise  

  **Windows 10 운영 체제**  

- Windows 10  

- Windows 10 Pro  

- Windows 10 Enterprise  

- Windows 10 Education  

  **Mac 클라이언트 컴퓨터**  

- Mac OS X v10.5 Leopard  

- Mac OS X v10.6 Snow Leopard  

- Mac OS X v10.7 Lion  

> [!NOTE]
>  Windows Server Essentials 대시보드에서 Mac 컴퓨터에 대한 상태 및 백업 상태를 볼 수 있습니다. 그러나 대시보드에서 컴퓨터 백업을 구성하거나 백업을 시작할 수 없습니다. 또한 원격 웹 액세스를 사용하여 Mac 컴퓨터에 연결할 수 없습니다.  

###  <a name="BKMK_5"></a>서버에서 클라이언트 컴퓨터에 대해 수행 하는 변경 내용  
 컴퓨터에 서버에 연결하면 Windows Server Essentials 소프트웨어에서는 컴퓨터와 서버가 함께 작동할 수 있도록 컴퓨터에 많은 변경 사항을 적용합니다.  

 소프트웨어에서는 다음을 수행합니다.  

-   컴퓨터에 Connector 소프트웨어를 설치합니다.  

-   컴퓨터에 Microsoft .NET Framework 4.5를 설치합니다(설치되어 있지 않은 경우).  

-   컴퓨터의 바탕 화면에 대시보드 및 실행 패드에 대 한 바로 가기를 만듭니다.  

-   다음 기능이 작동할 수 있도록 컴퓨터에서 Windows 방화벽 포트를 구성합니다.  

    -   핵심 네트워킹  

    -   원격 데스크톱 서비스  

-   원활한 백업을 위해 컴퓨터를 다음과 같이 변경합니다.  

    -   자동 백업을 실행하는 예약 작업을 만듭니다.  

    -   서버를 통해 백업 작업을 관리하는 서비스를 설치합니다.  

    -   파일 및 폴더를 복원하는 동안 사용되는 가상 장치 드라이버를 설치합니다.  

-   상태 에이전트를 설치하여 문제를 감지하고 해당하는 경고 알림을 만듭니다.  

-   컴퓨터에서 상태 평가를 되풀이하고 상태 경고 알림을 동기화하기 위한 예약 작업을 만듭니다.  

-   컴퓨터에서 서버 및 기타 Windows Server Essentials 기능과의 통신에 사용할 서비스를 컴퓨터에 추가합니다.  

-   원격 데스크톱 서비스가 실행될 수 있도록 Windows 클라이언트를 실행하는 클라이언트 컴퓨터에서 TCP 포트 3389를 엽니다.  

-   클라이언트 컴퓨터에 VPN을 배포 하 고 Windows Server Essentials에서 vpn 기능을 사용 하는 경우 단일 클릭 환경을 제공 하거나, Windows Server Essentials에서 VPN 기능을 사용 하는 경우 자동 연결 환경을 제공 합니다.  


 서버에 컴퓨터를 연결하는 방법에 대한 자세한 내용은 [Connect computers to the server](Get-Connected-in-Windows-Server-Essentials.md#BKMK_9)을 참조하세요.  

###  <a name="BKMK_6"></a>네트워크 사용자 이름 및 암호 정보  
 서버를 관리하는 사용자로부터 네트워크 사용자 이름 및 암호 정보를 얻을 수 있습니다. 이 자격 증명을 사용하여 컴퓨터를 서버에 연결하고 서버에서 정보에 액세스할 수 있습니다.  

###  <a name="BKMK_6"></a>네트워크 사용자 이름 및 암호 정보  
 서버를 관리하는 사용자로부터 네트워크 사용자 이름 및 암호 정보를 얻을 수 있습니다. 이 자격 증명을 사용하여 컴퓨터를 서버에 연결하고 서버에서 정보에 액세스할 수 있습니다. 


 서버 관리자는 대시보드의 **사용자** 탭에서 사용자 계정을 추가하여 네트워크 자격 증명을 만들 수 있습니다. 사용자 계정에 대한 자세한 내용은 [대시보드를 사용하여 사용자 계정 관리](../manage/Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage8)를 참조하세요.  

###  <a name="BKMK_7"></a>서버 관리자 계정  
 Connector 소프트웨어를 설치하려면 네트워크 관리자 계정 이름 및 암호를 제공할 수 있어야 합니다. 네트워크 관리자 계정을 사용하면 사용자가 조직에 대한 LAN을 관리하고 스위치 및 라우터와 같은 네트워크 장치를 관리 및 유지 관리할 수 있습니다.  

 네트워크 관리자 계정을 사용하여 수행할 수 있는 작업은 다음과 같습니다.  

- 네트워크로 연결된 응용 프로그램 및 기타 소프트웨어 설치  

- 서버에서 저장소 관리  

- 소프트웨어 업데이트 배포  

- 일상적인 백업 수행  

- 네트워크에서 일상적인 작업 모니터링  

  Windows server essentials Experience 역할이 설치 된 windows Server Essentials, Windows Server Essentials 및 Windows Server 2012 r 2에서 사용자 계정에 네트워크 관리자 액세스 수준을 할당할 수 있습니다. 네트워크 관리자 작업을 수행하는 데 필요한 사용 권한이 부여됩니다. 사용자에게 네트워크 관리자 액세스 수준이 할당되면 관리자 사용 권한이 필요한 작업에 대한 **사용자 액세스 제어** 프롬프트가 열립니다.  

###  <a name="BKMK_8"></a>Windows 도메인에서 컴퓨터 제거  
 도메인에서 컴퓨터를 제거하려고 하면 도메인 계정의 사용자 이름과 암호를 입력하라는 메시지가 표시됩니다.  

##### <a name="to-remove-a-computer-from-a-windows-domain"></a>Windows 도메인에서 컴퓨터를 제거하려면  

1.  **시작**을 클릭하고 **컴퓨터**를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  

2.  **컴퓨터 이름, 도메인 및 작업 그룹 설정**에서 **설정 변경**을 클릭합니다.  

    > [!NOTE]
    >  관리자 암호 또는 확인을 입력하라는 메시지가 표시되면 도메인 암호를 입력하거나 확인을 제공합니다.  

3.  **시스템 속성** 대화 상자에서 **컴퓨터 이름** 탭, **변경**을 차례로 클릭합니다.  

4.  **컴퓨터 이름/도메인 변경** 대화 상자의 **소속 그룹**에서 **작업 그룹**을 클릭하고 다음의 하나를 수행합니다.  

    1.  기존 작업 그룹에 가입하려면 가입하려는 작업 그룹의 이름을 입력하고 **확인**을 클릭합니다.  

    2.  작업 그룹을 만들려면 만들려는 작업 그룹의 이름을 입력하고 **확인**을 클릭합니다.  

        > [!NOTE]
        >  컴퓨터가 도메인에서 제거되고 해당 도메인의 컴퓨터 계정이 사용하지 않도록 설정됩니다.  

##  <a name="BKMK_B"></a>Connector 소프트웨어를 사용 하 여 서버에 컴퓨터 연결  
 이 섹션에서는 Connector 소프트웨어를 설치하고 컴퓨터를 서버에 연결하고 서버에 컴퓨터를 연결할 때 발생하는 문제를 해결하는 데 도움이 되는 절차와 정보에 액세스할 수 있습니다.  


-   [서버에 컴퓨터 연결](Get-Connected-in-Windows-Server-Essentials.md#BKMK_9)  

-   [도메인에 가입 하지 않고 Windows Server Essentials 서버에 컴퓨터 연결](Get-Connected-in-Windows-Server-Essentials.md#BKMK_10)  

-   [Connector 소프트웨어 설치](Get-Connected-in-Windows-Server-Essentials.md#BKMK_11)  

-   [수동으로 컴퓨터 데이터 및 설정 이동](Get-Connected-in-Windows-Server-Essentials.md#BKMK_12)  

-   [컴퓨터 배포 중에 여러 사용자 프로필 전송](Get-Connected-in-Windows-Server-Essentials.md#BKMK_Transfer)  

-   [Connector 소프트웨어 제거](Get-Connected-in-Windows-Server-Essentials.md#BKMK_13)  

-   [서버에서 컴퓨터 연결 끊기 또는 서버에 컴퓨터 다시 연결](Get-Connected-in-Windows-Server-Essentials.md#BKMK_14)  

-   [백업이 절전 모드 및 최대 절전 모드에서 작동 하는 방식](Get-Connected-in-Windows-Server-Essentials.md#BKMK_Sleep)  

-   [서버에 컴퓨터 연결](Get-Connected-in-Windows-Server-Essentials.md#BKMK_9)  

-   [도메인에 가입 하지 않고 Windows Server Essentials 서버에 컴퓨터 연결](Get-Connected-in-Windows-Server-Essentials.md#BKMK_10)  

-   [Connector 소프트웨어 설치](Get-Connected-in-Windows-Server-Essentials.md#BKMK_11)  

-   [수동으로 컴퓨터 데이터 및 설정 이동](Get-Connected-in-Windows-Server-Essentials.md#BKMK_12)  

-   [컴퓨터 배포 중에 여러 사용자 프로필 전송](Get-Connected-in-Windows-Server-Essentials.md#BKMK_Transfer)  

-   [Connector 소프트웨어 제거](Get-Connected-in-Windows-Server-Essentials.md#BKMK_13)  

-   [서버에서 컴퓨터 연결 끊기 또는 서버에 컴퓨터 다시 연결](Get-Connected-in-Windows-Server-Essentials.md#BKMK_14)  

-   [백업이 절전 모드 및 최대 절전 모드에서 작동 하는 방식](Get-Connected-in-Windows-Server-Essentials.md#BKMK_Sleep)  


###  <a name="BKMK_9"></a>서버에 컴퓨터 연결  
 Windows server essentials Experience 역할이 설치 된 windows server Essentials 또는 Windows Server 2012 r 2를 실행 하는 서버에 컴퓨터를 연결 하는 경우 클라이언트 컴퓨터가 인터넷에 올바르게 연결 되어 있는지 확인 합니다.  

 모든 클라이언트 컴퓨터에서 다음 절차를 완료하여 컴퓨터를 서버에 연결합니다.  

 절차를 완료하려면 다음 정보가 필요합니다.  

-   새 네트워크에서 컴퓨터를 사용할 사람의 사용자 이름 및 암호  

-   컴퓨터 로컬 관리자 계정의 사용자 이름 및 암호  

> [!NOTE]
> 
>  Windows server essentials 또는 Windows Server Essentials에 대 한 온-프레미스 클라이언트 배포에서는 컴퓨터를 Windows Server Essentials 도메인에 추가 하지 않고 서버에 연결할 수 있습니다. 이 방법은 모든 지원되는 클라이언트 운영 체제에서 사용할 수 있는 것은 아니며 그룹 정책 및 VPN(가상 사설망)과 같이 컴퓨터를 도메인에 연결해야 하는 기능은 사용할 수 없습니다. 요구 사항 및 지침은 [도메인에 가입 하지 않고 Windows Server Essentials 서버에 컴퓨터 연결](Get-Connected-in-Windows-Server-Essentials.md#BKMK_10)을 참조하세요.  
> 
>  Windows server essentials 또는 Windows Server Essentials에 대 한 온-프레미스 클라이언트 배포에서는 컴퓨터를 Windows Server Essentials 도메인에 추가 하지 않고 서버에 연결할 수 있습니다. 이 방법은 모든 지원되는 클라이언트 운영 체제에서 사용할 수 있는 것은 아니며 그룹 정책 및 VPN(가상 사설망)과 같이 컴퓨터를 도메인에 연결해야 하는 기능은 사용할 수 없습니다. 요구 사항 및 지침은 [도메인에 가입 하지 않고 Windows Server Essentials 서버에 컴퓨터 연결](Get-Connected-in-Windows-Server-Essentials.md#BKMK_10)을 참조하세요.  


##### <a name="to-connect-a-client-computer-to-the-server"></a>서버에 클라이언트 컴퓨터를 연결하려면  

1.  서버에 연결할 컴퓨터에 로그온합니다.  

    > [!NOTE]
    >  이 컴퓨터에 여러 사용자 계정이 있는 경우 컴퓨터를 서버에 연결한 후 문서, 그림 및 개인 기본 설정을 유지하려는 사용자 계정을 사용하여 로그온합니다.  

2.  Internet Explorer와 같은 인터넷 브라우저를 엽니다.  

3.  주소 표시줄에 **http://\>< servername/Connect**를 입력 한 다음 enter 키를 누릅니다.  

    > [!NOTE]
    >  컴퓨터가 Windows server Essentials 네트워크 외부의 원격 위치에 있는 경우 서버에 컴퓨터 연결 마법사를 실행 하려면 웹 브라우저의 주소 표시줄에 **http://\>< domainname/connect** 을 입력 합니다 (여기서 < 도메인\> 은 조직의 도메인 이름입니다. 도메인 이름 정보에 대해서는 네트워크 관리자에게 문의하세요.  

4.  **서버에 컴퓨터 연결** 페이지가 나타납니다. 다음 작업 중 하나를 수행합니다.  

    -   Windows 운영 체제를 실행하는 컴퓨터의 경우 **Windows용 소프트웨어 다운로드**를 클릭합니다.  

    -   Mac OS X 이상을 실행하는 컴퓨터의 경우 **Mac용 소프트웨어 다운로드**를 클릭합니다.  

5.  파일 다운로드 보안 경고 메시지에서 **실행**클릭합니다.  

6.  사용자 계정 컨트롤 메시지가 표시되면 **예** 를 클릭하거나 메시지에 따라 로컬 사용자 이름 및 암호를 입력합니다.  

7.  서버에 컴퓨터 연결 마법사가 나타납니다. 마법사를 완료하려면 다음을 수행합니다.  

    1.  최종 사용자 사용권 계약에 동의합니다.  

    2.  **내 서버 찾기** 페이지에서 로컬 네트워크에서 서버를 자동 검색하고 연결하려는 서버를 선택합니다. 또는 정보가 있는 경우 수동으로 서버 이름 또는 도메인 주소를 입력할 수 있습니다.  

    3.  **새 네트워크 사용자 이름 및 암호 입력** 페이지에서 다음을 수행합니다.  

        -   이 컴퓨터가 서버에 연결하는 첫 번째 컴퓨터이고 해당 컴퓨터에서 서버를 관리하려는 경우 설치하는 동안 만든 관리자 계정을 사용합니다.  

        -   다른 모든 컴퓨터의 경우 먼저 대시보드를 사용하여 서버에서 네트워크 사용자 계정을 만듭니다. 컴퓨터 사용자가 수행하는 작업에 따라 관리자 또는 표준 사용자 권한으로 사용자 계정을 만듭니다.  

    4.  컴퓨터에서 Windows 8, Windows 8.1 또는 Windows 10을 실행 하는 경우이 단계를 건너뜁니다. 컴퓨터에서 Windows 7을 실행 중인 경우 컴퓨터를 새 네트워크에 연결한 후에 문서, 사진 또는 개인 기본 설정(예: 바탕 화면 배경, 화면 보호기, Internet Explorer 즐겨찾기)을 보존하려면 마법사의 **기존 데이터 및 설정에 대한 이동 여부를 선택하세요.** 페이지에서 **데이터 및 설정을 새 네트워크 사용자 계정으로 이동합니다.** 를 선택합니다.  

    5.  **백업을 만들기 위해 이 컴퓨터의 절전 모드를 종료할지 선택하세요.** 페이지에서 백업을 만들기 위해 컴퓨터의 절전 모드를 자동으로 종료할지 여부를 선택합니다.  

    6.  마법사의 나머지 페이지에 표시되는 안내에 따라 컴퓨터를 네트워크에 연결합니다.  

8.  컴퓨터를 네트워크에 연결한 후 새 사용자 이름과 암호를 사용하여 컴퓨터에 로그온합니다.  

    > [!NOTE]
    >  Windows 8을 실행하는 컴퓨터를 서버에 연결한 후 네트워크 계정을 사용하여 처음 로그온하면 이전 사용자 계정에서 파일 및 응용 프로그램을 마이그레이션하는 방법에 대한 지침이 표시됩니다. **이전 사용자 계정에서 파일 및 응용 프로그램을 마이그레이션하는 방법** 페이지의 안내에 따라 모든 파일 및 응용 프로그램을 네트워크 사용자 계정으로 마이그레이션합니다.  

9. 컴퓨터가 서버에 성공적으로 연결 되 면 커넥터 TrayApp 및 서버 대시보드에 대 한 바로 가기가 시작 메뉴에 표시 됩니다 .이 메뉴에는 다음과 같이 사용할 수 있습니다. 컴퓨터에서 Windows 8, Windows 8.1 또는 Windows 10, 대시보드 및 커넥터를 실행 하는 경우에 사용할 수 있습니다. TrayApp는 컴퓨터의 시작 화면에서 사용할 수 있습니다.):  

    -   컴퓨터에서 Windows 8, Windows 8.1 또는 Windows 10을 실행 하는 경우 대시보드 및 커넥터 TrayApp는 앱으로 검색 가능 합니다.  

    -   Connector TrayApp에서 **원격 연결 상태 유지** 기능을 사용하거나 사용하지 않도록 설정합니다. TrayApp을 두 번 클릭하여 실행 패드를 시작할 수도 있습니다. 실행 패드에서 공유 폴더 바로 가기에 액세스하고, 컴퓨터 백업을 구성하고, 경고를 해결하고, 원격 웹 액세스 사이트를 열 수 있습니다.  

    -   **대시보드** 링크에서 서버를 관리할 수 있습니다.  

###  <a name="BKMK_10"></a>도메인에 가입 하지 않고 Windows Server Essentials 서버에 컴퓨터 연결  
 이 항목에서는 온-프레미스 클라이언트 배포에서 컴퓨터를 Windows Server Essentials 도메인에 가입시 키 지 않고 windows 7, Windows 8, Windows 8.1 또는 Windows 10 컴퓨터를 Windows Server Essentials 네트워크에 추가 하는 방법에 대해 설명 합니다. 이 연결 방법은 Windows Server Essentials 및 Windows Server Essentials에서 지원 됩니다.  

 이 방법은 컴퓨터를 Windows Server Essentials 도메인에 가입시켜야 하는 일반적인 방법의 대안입니다. 해당 방법을 사용할 때 컴퓨터가 다른 도메인에 있으면 컴퓨터를 도메인에서 제거해야 Windows Server Essentials 도메인에 추가할 수 있습니다.  

#### <a name="feature-limits"></a>기능 제한  
 클라이언트 컴퓨터가 Windows Server Essentials 도메인에 추가되지 않으면 일부 기능이 제한됩니다.  

-   도메인 자격 증명, 그룹 정책 및 Vpn (가상 사설망)을 포함 하 여 컴퓨터가 도메인에 가입 되어 있어야 하는 모든 기능을 사용할 수 있는 것은 아닙니다.  

-   컴퓨터가 도메인에 가입되어야 하는 타사 추가 기능이 제대로 작동하지 않습니다.  

-   오프-프레미스 컴퓨터를 서버에 연결하는 데 이 방법을 사용할 수 없습니다.  

#### <a name="prerequisites"></a>사전 요구 사항  

-   컴퓨터는 로컬 네트워크에 실제로 연결되어 있어야 합니다.  

-   다음 운영 체제의 하나가 컴퓨터에 설치되어 있어야 합니다.  

    -   Windows 10 Pro, Windows 10 Enterprise  

    -    Windows 8.1 Pro, Windows 8.1 Enterprise, Windows 8 Pro, Windows 8 Enterprise  

    -    Windows 7 Professional (x86 및 x64), Windows 7 Enterprise (x86 및 x64), Windows 7 Ultimate (x86 및 x64)  


-   컴퓨터는 Windows Server Essentials의 클라이언트 컴퓨터에 대한 모든 요구 사항을 충족해야 합니다. 자세한 내용은 [서버에 컴퓨터를 연결 하기 위한 필수 구성 요소](Get-Connected-in-Windows-Server-Essentials.md#BKMK_2)를 참조하세요.  


-   도메인에 가입하지 않고 연결을 사용하도록 설정하려면 로컬 관리자 그룹의 구성원인 계정으로 컴퓨터에 로그온해야 합니다.  

-   컴퓨터를 Windows Server Essentials 서버에 연결하려면 다음 계정 정보가 필요합니다.  

    -   Windows Server Essentials에 대한 관리자 권한이 있는 계정(계정).  

    -   컴퓨터를 사용하는 사용자의 도메인 계정에 대한 사용자 이름 및 암호. 도메인 계정에도 Windows Server Essentials 서버에 대한 관리자 권한이 있어야 합니다.  

#### <a name="connect-to-a-windows-server-essentials-network"></a>Windows Server Essentials 네트워크에 연결  
 모든 필수 구성 요소가 충족되었는지 확인하고 나서 컴퓨터를 Windows Server Essentials 네트워크에 연결합니다.  

###### <a name="to-connect-a-computer-in-a-different-domain-to-a-windows-server-essentials-network"></a>다른 도메인의 컴퓨터를 Windows Server Essentials 네트워크에 연결하려면  

1.  로컬 관리자 그룹의 구성원인 계정으로 클라이언트 컴퓨터에 로그온합니다.  

2.  관리자 권한으로 명령 프롬프트를 엽니다.  

    -   Windows 10에서 **시작** 단추를 클릭 하 고 **모든 앱** -> **Windows 시스템 도구** -> **명령 프롬프트**를 마우스 오른쪽 단추로 클릭 한 다음 **관리자 권한으로 실행**을 클릭 합니다.  

    -   Windows 8의 **시작** 페이지에서 **command** 를 입력 한 다음 enter 키를 누릅니다. 결과에서 **명령 프롬프트**를 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행**을 클릭합니다.  

    -   Windows 7의 **시작** 메뉴에서 검색 상자에 **command** 를 입력 하 고 **명령 프롬프트**를 마우스 오른쪽 단추로 클릭 한 다음 **관리자 권한으로 실행**을 클릭 합니다.  

3.  명령 프롬프트에서 다음 명령을 입력하고 Enter 키를 누릅니다.  

    ```  
    reg add "HKLM\SOFTWARE\Microsoft\Windows Server\ClientDeployment" /v SkipDomainJoin /t REG_DWORD /d 1  
    ```  


4.  [서버에 컴퓨터 연결](Get-Connected-in-Windows-Server-Essentials.md#BKMK_9)의 단계를 완료합니다.  


####  <a name="BKMK_SecondServer"></a>네트워크에 두 번째 서버 연결  

###### <a name="to-join-a-second-server-to-the-network"></a>네트워크에 두 번째 서버를 연결하려면  

1.  Windows Server Essentials 네트워크에 연결할 서버에 로그온합니다.  

2.  인터넷 브라우저를 열고 주소 표시줄에 **http:/\>/< servername/Connect**를 입력 한 다음 enter 키를 누릅니다. 여기서 *< servername\>*  은 Windows server Essentials를 실행 하는 서버의 이름입니다.  

3.  Windows Server Essentials 네트워크에 연결하려는 서버에서 Internet Explorer 보안 강화 구성이 사용하도록 설정되어 있으면 다음을 완료하고, 그렇지 않으면 이 단계를 건너뜁니다.  

    1.  차단 메시지를 허용하려면 **닫기**를 클릭합니다.  

    2.  다음과 같이 신뢰할 수 있는 웹 사이트에 **http://\>< servername/Connect** 웹 사이트를 추가 합니다.  

        1.  브라우저 탐색 창에서 **도구**, **인터넷 옵션**을 차례로 클릭합니다.  

        2.  **보안** 탭, **신뢰할 수 있는 사이트**를 차례로 클릭합니다.  

        3.  **사이트**를 클릭합니다.  

        4.  웹 사이트가 **영역에 웹 사이트 추가** 필드에 표시되어야 합니다. **추가**를 클릭합니다.  

        5.  **닫기**를 클릭한 다음 **확인**을 클릭합니다.  

    3.  웹 페이지를 새로 고칩니다.  


    4.  Windows Server Essentials를 실행하는 서버에 두 번째 서버를 연결하려면 [Connect computers to the server](Get-Connected-in-Windows-Server-Essentials.md#BKMK_9)의 지침에 따릅니다.  


~~~
> [!NOTE]
>  Connecting a second server to a server running Windows Server Essentials differs from connecting to a client computer as follows:  
>   
>  -   There is no user profile migration; therefore, the current profile will not be migrated.  
> -   You cannot back up the second server by using client computer backup, and there is no option to wake up the computer for backup.  
~~~

 Windows Server Essentials를 실행하는 서버에 두 번째 서버를 연결하고 나면 연결된 서버에 다음 기능이 제공됩니다.  

- 업데이트 및 경고 상태 기능은 다른 클라이언트 컴퓨터와 같게 작동합니다.  

- 온라인 및 오프라인 기능은 다른 클라이언트 컴퓨터와 같게 작동합니다.  

- 원격 웹 액세스를 사용하여 두 번째 서버에 연결할 수 있습니다.  

- Windows Server Essentials에서 이 서버와 관련된 경고를 생성하므로 두 번째 서버가 상태 보고서에 포함됩니다.  

  Windows Server Essentials를 실행 중인 서버에서 두 번째 서버를 관리하는 것은 기타 클라이언트 컴퓨터를 관리하는 것과 다음과 같이 다릅니다.  

- TrayApp, 실행 패드 및 대시보드 클라이언트에 대한 진입점이 없습니다.  

- 두 번째 서버는 **장치** 탭의 **서버** 그룹에 나열됩니다.  

- 두 번째 서버에 대한 클라이언트 컴퓨터 백업이 지원되지 않으므로 백업 상태는 **지원되지 않음**으로 표시됩니다. 또한 두 번째 서버를 선택하고 마우스 오른쪽 단추를 클릭하면 두 번째 서버에 대한 백업 및 복원 관련 작업이 표시되지 않습니다.  

- 두 번째 서버를 선택 하 고 **서버 속성 보기** 작업을 클릭 하면 서버 속성 페이지에 **백업** 탭이 표시 되지 않습니다.  

- Windows Server 운영 체제에 Security Center 없기 때문에 두 번째 서버의 보안 상태는 **해당 없음**으로 표시 됩니다.  

- 두 번째 서버의 그룹 정책 상태는 **해당 없음**으로 표시 됩니다.  

###  <a name="BKMK_11"></a>Connector 소프트웨어 설치  
 Windows Server Essentials의 Connector 소프트웨어는 서버에 컴퓨터 연결 마법사를 사용하여 서버에 컴퓨터를 연결할 때 설치됩니다. 웹 브라우저의 주소 표시줄에 **http://< ServerName\>/connect** 를 입력 하 여이 마법사를 시작할 수 있습니다. 여기서 *< servername\>*  은 서버 이름입니다.  

> [!NOTE]
>  컴퓨터가 원격 위치에 있는 경우 서버에 컴퓨터 연결 마법사를 실행 하려면 웹 브라우저의 주소 표시줄에 **http://< domainname\>/connect** 을 입력 합니다. 여기서 *< 도메인\>*  은의 도메인 이름입니다. 조직). 도메인 이름 정보에 대해서는 네트워크 관리자에게 문의하세요.  

 Connector 소프트웨어에서는 다음을 수행합니다.  

-   Windows Server Essentials에 컴퓨터를 연결합니다.  

-   컴퓨터를 야간에 자동으로 백업합니다(클라이언트 백업을 만들도록 서버를 구성한 경우).  

-   관리자가 컴퓨터 상태를 모니터링하도록 도와줍니다.  

-   홈 컴퓨터에서 Windows Server Essentials를 구성하고 원격으로 관리할 수 있게 합니다.  


 Windows Server Essentials 서버에 컴퓨터를 연결하는 방법에 대한 단계별 지침은 [Connect computers to the server](Get-Connected-in-Windows-Server-Essentials.md#BKMK_9)을 참조하세요.   


###  <a name="BKMK_12"></a>수동으로 컴퓨터 데이터 및 설정 이동  
  Windows Server Essentials 및 Windows Server Essentials는 Windows 7 운영 체제를 실행 하는 클라이언트 컴퓨터에 대해서만 사용자 프로필 마이그레이션을 지원 합니다. Windows 7 기반 컴퓨터를 서버에 연결하면 서버에 컴퓨터 연결 마법사에서는 사용자 프로필을 자동으로 마이그레이션합니다.  

 Windows 8, Windows 8.1 또는 Windows 10 컴퓨터를 서버에 연결할 때는 사용자 프로필을 자동으로 전송할 수 없습니다. 그러나 Windows 8 컴퓨터에서는 Windows 사용자 환경 전송을 사용하여 원래 로컬 사용자의 데이터와 설정을 도메인 가입 컴퓨터에 전송할 수 있습니다. 이 작업을 하려면 Windows 8 원본 컴퓨터와 Windows 8 대상 컴퓨터에서 모두 관리자여야 합니다. Windows 사용자 환경 전송을 사용하여 파일과 설정을 전송하는 방법에 대한 자세한 내용은 Microsoft 기술 자료 문서에서 [문서 2735227](https://support.microsoft.com/kb/2735227) (영문)을 참조하세요.  

###  <a name="BKMK_Transfer"></a>컴퓨터 배포 중에 여러 사용자 프로필 전송  
 Windows 7 또는 Windows 7 SP1 운영 체제를 실행하는 컴퓨터를 Windows Server Essentials 서버에 연결하기 전에 여러 로컬 사용자 프로필을 전송하려면 먼저 서버에서 해당하는 네트워크 사용자 계정을 만들어야 합니다. 네트워크 사용자 계정을 만드는 방법에 대한 자세한 내용은 [사용자 계정 추가](../manage/Manage-User-Accounts-in-Windows-Server-Essentials.md#BKMK_Manage1)를 참조하세요.  

 사용자 프로필 마이그레이션은 windows 7 (Windows Server Essentials의 경우) 또는 Windows 7 SP1 (Windows Server Essentials의 경우)을 실행 하는 컴퓨터 에서만 지원 됩니다. 서버에 컴퓨터 연결 마법사를 사용하여 Windows Server Essentials 서버에 컴퓨터를 연결하면 이전 사용자 로컬 계정의 사용자 데이터와 설정을 새 네트워크 사용자 계정으로 이동하는 옵션이 제공됩니다. 이 작업을 하려면 마법사의 **기존 사용자 데이터 및 설정 이동** 페이지에서 클라이언트 컴퓨터에 있는 여러 사용자 프로필을 전송할 컴퓨터에 있는 로컬 사용자 계정에 네트워크 사용자 계정을 매핑합니다.  

###  <a name="BKMK_13"></a>Connector 소프트웨어 제거  
 제어판을 사용하여 컴퓨터에서 Connector 소프트웨어를 제거할 수 있습니다. Connector 소프트웨어에 문제가 있거나 Connector 소프트웨어의 최신 버전을 설치해야 하면 일반적으로 이 작업을 수행합니다. 이 절차를 완료하려면 관리자로 컴퓨터에 로그온되어 있어야 합니다.  

> [!IMPORTANT]
>  클라이언트 컴퓨터에서 운영 체제를 업그레이드하면 Connector 소프트웨어가 자동으로 제거됩니다. 업그레이드가 완료되고 나서 Connector 소프트웨어를 다시 설치해야 합니다. Connector 소프트웨어를 제거하고 나서 운영 체제를 업그레이드하는 것이 좋습니다. 업그레이드가 완료되고 나서 Connector 소프트웨어를 제거해도 되지만 이 경우 Connector 소프트웨어를 제거했다가 다시 설치할 때까지 클라이언트 컴퓨터의 상태가 서버와 일치하지 않을 수 있습니다.  

##### <a name="to-uninstall-connector-software-from-a-computer"></a>컴퓨터에서 Connector 소프트웨어를 제거하려면  

1.  Windows 7, Windows 8, Windows 8.1 또는 Windows 10을 실행 하는 컴퓨터에서 **제어판**을 열고 **프로그램** 섹션에서 **설치 된 업데이트 보기**를 클릭 합니다.  

2.  설치된 프로그램 목록에서 **Windows Server Essentials Connector**를 선택하고 **제거**를 클릭합니다.  

3.  경고 페이지에서 **예**를 클릭합니다.  

4.  **사용자 계정 컨트롤** 창이 나타나면 **허용**을 클릭합니다.  

5.  Windows Server Essentials에서 실행 패드를 닫도록 제안 하는 Windows Server Essentials Connector 페이지가 나타나면 **확인**을 클릭 합니다.  

6.  프로그램이 제거될 때까지 기다립니다. 소프트웨어가 제거되고 나면 설치된 프로그램 또는 업데이트 목록에 **Windows Server Essentials Connector**가 더 이상 나타나지 않습니다. 또한 실행 패드 및 대시보드의 바로 가기가 더 이상 컴퓨터 바탕 화면에 표시 되지 않습니다.  

> [!NOTE]
> - Connector 소프트웨어를 제거해도 대시보드의 **장치** 탭에 표시되는 컴퓨터 목록에서 컴퓨터가 제거되지 않습니다. 대시보드에서 컴퓨터를 제거하려면 [서버에서 컴퓨터 제거](../manage/Manage-Devices-in-Windows-Server-Essentials.md#BKMK_3)를 참조하세요.  
>   -   Connector 소프트웨어를 제거해도 서버에 매핑된 클라이언트 컴퓨터의 공유 폴더가 삭제되지 않습니다. 서버에 매핑된 공유 폴더를 수동으로 삭제해야 합니다.  
> 
> -   Connector 소프트웨어를 제거해도 컴퓨터가 원래 도메인에서 가입 해제되지 않습니다. 컴퓨터를 도메인에서 수동으로 가입 해제해야 합니다. 지침은 [Remove a computer from a Windows domain](Get-Connected-in-Windows-Server-Essentials.md#BKMK_8)항목을 참조하세요.  


###  <a name="BKMK_14"></a>서버에서 컴퓨터 연결 끊기 또는 서버에 컴퓨터 다시 연결  
 서버에서 컴퓨터의 연결을 끊으려면 다음 단계를 완료해야 합니다.  


1. 제어판을 사용하여 컴퓨터에서 Connector 소프트웨어를 제거합니다. 단계별 지침에 대해서는 [Uninstall the Connector software](Get-Connected-in-Windows-Server-Essentials.md#BKMK_13)항목을 참조하세요.   


2. Windows Server Essentials 도메인에서 컴퓨터를 가입 해제하고 작업 그룹에 연결합니다. Windows를 작업 그룹에 연결하는 방법에 대한 단계별 지침은 [작업 그룹 연결 또는 만들기](https://windows.microsoft.com/windows7/Join-or-create-a-workgroup)를 참조하세요.  

3. 대시보드를 사용하여 서버에서 컴퓨터를 제거합니다. 단계별 지침에 대해서는 [Remove a computer from the server](../manage/Manage-Devices-in-Windows-Server-Essentials.md#BKMK_3)항목을 참조하세요.  

   이전에 Windows Server Essentials 서버 네트워크에서 연결이 끊어진 서버에 컴퓨터를 다시 연결하려면 다음 단계를 완료해야 합니다.  


4. 제어판을 사용하여 컴퓨터에서 Connector 소프트웨어를 제거합니다. 단계별 지침에 대해서는 [Uninstall the Connector software](Get-Connected-in-Windows-Server-Essentials.md#BKMK_13)항목을 참조하세요.  

5. Windows Server Essentials 도메인에서 컴퓨터를 가입 해제하고 작업 그룹에 연결합니다. Windows를 작업 그룹에 연결하는 방법에 대한 단계별 지침은 [작업 그룹 연결 또는 만들기](https://windows.microsoft.com/windows7/Join-or-create-a-workgroup)를 참조하세요.  

6. 컴퓨터 연결 마법사를 사용하여 서버에 컴퓨터를 연결합니다. 단계별 지침에 대해서는 [Connect computers to the server](Get-Connected-in-Windows-Server-Essentials.md#BKMK_9)항목을 참조하세요.  

###  <a name="BKMK_Sleep"></a>백업이 절전 모드 및 최대 절전 모드에서 작동 하는 방식  
 서버에 컴퓨터를 연결할 때 **Wake This Computer for Backup** 옵션을 선택하면 컴퓨터를 백업할 수 있도록 매일 백업 일정에 지정된 대로 컴퓨터의 절전 또는 최대 절전 모드가 자동으로 해제됩니다. 백업이 완료되면 전원 관리 설정에 따라 컴퓨터가 절전 또는 최대 절전 모드로 돌아갑니다. 이 옵션을 선택하지 않으면 컴퓨터가 절전 또는 최대 절전 모드에 있을 경우 컴퓨터가 백업되지 않습니다. 자세한 내용은 [클라이언트 백업 관리](../manage/Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md)를 참조 하세요.  

##  <a name="BKMK_C"></a>실행 패드 사용  
 실행 패드를 사용하여 Windows Server Essentials 서버의 공유 리소스에 액세스하고 컴퓨터 백업을 수행하고 시스템 상태 경고에 응답할 수 있습니다.  

-   [실행 패드 개요](../manage/Overview-of-the-Launchpad-in-Windows-Server-Essentials.md)  

-   [Mac 컴퓨터에서 실행 패드 사용](../manage/Overview-of-the-Launchpad-in-Windows-Server-Essentials.md#BKMK_Mac)  

## <a name="see-also"></a>참조  

-   [서버에 컴퓨터 연결 문제 해결](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md)  

-   [사용자 계정 관리](../manage/Manage-User-Accounts-in-Windows-Server-Essentials.md)  


-   [공유 폴더 사용](Use-Shared-Folders-in-Windows-Server-Essentials.md)  

-   [원격으로 작업](Work-Remotely-in-Windows-Server-Essentials.md)  

-   [디지털 미디어 재생](Play-Digital-Media-in-Windows-Server-Essentials.md)

-   [공유 폴더 사용](../use/Use-Shared-Folders-in-Windows-Server-Essentials.md)  

-   [원격으로 작업](../use/Work-Remotely-in-Windows-Server-Essentials.md)  

-   [디지털 미디어 재생](../use/Play-Digital-Media-in-Windows-Server-Essentials.md)

