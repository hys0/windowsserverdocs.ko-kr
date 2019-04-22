---
title: 기본 DirectAccess 서버를 구성 하는 2 단계
description: 이 항목은 시작 시작 마법사에 대 한 Windows Server 2016을 사용 하 여 단일 DirectAccess 서버 배포 가이드의 일부
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 82bf5fed-93b3-4fa6-8e71-522146eccdb1
ms.author: pashort
author: shortpatti
ms.openlocfilehash: fc0abf849d43c8ba6ec86e17b9ed86fce573ed47
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59813384"
---
# <a name="step-2-configure-the-basic-directaccess-server"></a>기본 DirectAccess 서버를 구성 하는 2 단계

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 항목에서는 기본 DirectAccess 배포에 필요한 클라이언트 및 서버 설정을 구성하는 방법에 대해 설명합니다. 에 설명 된 계획 단계를 완료 한 확인 배포 단계를 시작 하기 전에 [기본 DirectAccess 배포 계획](Plan-a-Basic-DirectAccess-Deployment.md)합니다.  
  
|태스크|설명|  
|----|--------|  
|원격 액세스 역할 설치|원격 액세스 역할을 설치합니다.|  
|시작 마법사를 사용하여 DirectAccess 구성|새로운 시작 마법사는 매우 간결한 구성 환경을 제공합니다. 이 마법사는 DirectAccess의 복잡성을 마스크하여 간단한 몇 가지 단계를 거쳐 자동으로 설정될 수 있도록 합니다. 또한 내부적으로 PKI를 배포할 필요가 없도록 Kerberos 프록시를 자동으로 구성하여 관리자에게 원활한 환경을 제공합니다.|  
|DirectAccess 구성으로 클라이언트 업데이트|DirectAccess 설정을 받으려면 클라이언트는 인트라넷에 연결된 상태에서 그룹 정책을 업데이트해야 합니다.|  
  
> [!NOTE]  
> 이 항목에는 설명한 절차의 일부를 자동화하는 데 사용할 수 있는 샘플 Windows PowerShell cmdlet이 포함되어 있습니다. 자세한 내용은 참조 [Cmdlet를 사용 하 여](https://go.microsoft.com/fwlink/p/?linkid=230693)합니다.  
  
## <a name="BKMK_Role"></a>원격 액세스 역할 설치  
원격 액세스를 배포하려면 조직에서 원격 액세스 서버로 사용할 서버에 원격 액세스 역할을 설치해야 합니다.  
  
#### <a name="to-install-the-remote-access-role"></a>원격 액세스 역할을 설치하려면  
  
1.  원격 액세스 서버의 서버 관리자 콘솔에는 **대시보드**, 클릭 **역할 및 기능 추가**합니다.  
  
2.  **다음** 을 세 번 클릭하여 서버 역할 선택 화면으로 이동합니다.  
  
3.  **서버 역할 선택** 대화 상자에서 **원격 액세스**를 선택하고 **다음**을 클릭합니다.  
  
4.  **기능 선택** 대화 상자에서 **다음**을 클릭합니다.  
  
5.  클릭 **다음**, 를 선택한 다음는 **역할 서비스 선택** 대화 상자에서 클릭는 **DirectAccess 및 VPN (RAS)** 확인란입니다.  
  
6.  클릭 **기능 추가**, 클릭 **다음**, 를 클릭 하 고 **설치**합니다.  
  
7.  **설치 진행률** 대화 상자에서 설치가 완료되었는지 확인하고 **닫기**를 클릭합니다.  
  
![Windows PowerShell](../../../media/Step-2-Configure-the-DirectAccess-Server/PowerShellLogoSmall.gif)Windows PowerShell 해당 명령을 * * *  
  
다음 Windows PowerShell cmdlet 또는 cmdlet을 원격 액세스 역할을 설치 합니다. 

1. 관리자 권한으로 PowerShell을 엽니다.

2. 원격 액세스 기능을 설치 합니다.

   ```  
   Install-WindowsFeature RemoteAccess   
   ```  

3. 컴퓨터를 다시 시작 합니다.

   ```
   Restart-Computer
   ```
   
4. 원격 액세스 PowerShell을 설치 합니다.

   ```
   Install-WindowsFeature RSAT-RemoteAccess-PowerShell
   ```



  
## <a name="configure-directaccess-with-the-getting-started-wizard"></a>시작 마법사로 DirectAccess 구성  
  
#### <a name="to-configure-directaccess-using-the-getting-started-wizard"></a>시작 마법사로 DirectAccess를 구성하려면  
  
1.  서버 관리자에서 **도구**, 를 클릭 하 고 **원격 액세스 관리**합니다.  
  
2.  원격 액세스 관리 콘솔의 왼쪽된 탐색 창에서 구성 하는 역할 서비스를 선택 하 고 클릭 한 다음 **시작 마법사 실행**합니다.  
  
3.  클릭 **DirectAccess만 배포**합니다.  
  
4.  네트워크 구성의 토폴로지를 선택하고 원격 액세스 클라이언트가 연결될 공개 이름을 입력합니다. **다음**을 클릭합니다.  
  
    > [!NOTE]  
    > 기본적으로 시작 마법사에서는 WMI 필터를 클라이언트 설정 GPO에 적용하면 도메인 내의 모든 랩톱 및 노트북 컴퓨터에 DirectAccess를 배포합니다.  
  
5.  **마침**을 클릭합니다.  
  
6.  이 배포에서 사용되는 PKI가 없으므로 인증서가 없는 경우 마법사는 IP-HTTPS와 네트워크 위치 서버에 자체 서명된 인증서를 자동으로 프로비전하고 Kerberos 프록시를 자동으로 사용합니다. 또한 마법사는 IPv4 전용 환경에서의 프로토콜 변환에 NAT64 및 DNS64를 사용하도록 설정합니다. 마법사가 구성을 적용하고 나면 **닫기**를 클릭합니다.  
  
7.  원격 액세스 관리 콘솔의 콘솔 트리에서 선택 **작동 상태**합니다. 모든 모니터의 상태가 "작업 중"으로 표시될 때까지 기다립니다. 모니터링 아래의 작업 창에서 주기적으로 **새로 고침**을 클릭하여 화면 표시를 업데이트합니다.  
  
## <a name="update-clients-with-the-directaccess-configuration"></a>DirectAccess 구성으로 클라이언트 업데이트  
  
#### <a name="to-update-directaccess-clients"></a>DirectAccess 클라이언트를 업데이트하려면  
  
1.  관리자 권한으로 PowerShell을 엽니다.  
  
2.  PowerShell 창에 **gpupdate**를 입력하고 **Enter** 키를 누릅니다.  
  
3.  컴퓨터 정책 업데이트가 성공적으로 완료될 때까지 기다립니다.  
  
4.  **Get-DnsClientNrptPolicy**를 입력하고 **Enter** 키를 누릅니다.  
  
    DirectAccess의 NRPT(이름 확인 정책 테이블) 항목이 표시됩니다. NLS 서버 예외가 표시됩니다. 시작 마법사가 DirectAccess 서버의 DNS 항목을 자동으로 만들었으며, DirectAccess 서버를 네트워크 위치 서버로 사용할 수 있도록 연관된 자체 서명된 인증서를 제공했습니다.  
  
5.  **Get-NCSIPolicyConfiguration**을 입력하고 **Enter** 키를 누릅니다. 마법사에서 배포된 네트워크 연결 상태 표시기 설정이 표시됩니다. DomainLocationDeterminationURL의 값에 주목합니다. 클라이언트는 이 네트워크 위치 서버 URL에 액세스할 수 있을 때면 언제나 클라이언트가 회사 네트워크 내부에 있는 것으로 판단하여 NRPT 설정이 적용되지 않습니다.  
  
6.  형식 **Get-daconnectionstatus** 누릅니다 **ENTER**합니다. 상태가으로 표시 됩니다 클라이언트가 네트워크 위치 서버 URL에 연결할 수 있으므로 **ConnectedLocally**합니다.  
  
## <a name="BKMK_Links"></a>이전 단계  
  
-   [1단계: DirectAccess 인프라 구성](Step-1-Configure-the-DirectAccess-Infrastructure.md)  
  
## <a name="next-step"></a>다음 단계  
  
-   [3 단계에는 기본 DirectAccess 배포 확인](da-basic-configure-s3-verify.md)  
  


