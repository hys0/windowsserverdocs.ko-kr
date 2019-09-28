---
title: Hyper-v 가상 컴퓨터에 대 한 가상 스위치 만들기
description: Hyper-v 관리자 또는 Windows PowerShell을 사용 하 여 가상 스위치를 만드는 방법에 대 한 지침을 제공 합니다.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: fdc8063c-47ce-4448-b445-d7ff9894dc17
author: KBDAzure
ms.author: kathydav
ms.date: 10/04/2016
ms.openlocfilehash: f1a814060e763545411b5c4345367638a5161ac2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392929"
---
# <a name="create-a-virtual-switch-for-hyper-v-virtual-machines"></a>Hyper-v 가상 컴퓨터에 대 한 가상 스위치 만들기

>적용 대상: Windows 10, Windows Server 2016, Microsoft Hyper-V Server 2016, Windows Server 2019, Microsoft Hyper-V Server 2019
  
가상 스위치에 가상 컴퓨터를 다른 컴퓨터와 통신 하는 Hyper-v 호스트에 만들어진 있습니다. Windows Server에 Hyper-v 역할을 처음 설치할 때 가상 스위치를 만들 수 있습니다. 추가 가상 스위치를 만들려면 Hyper-v 관리자 또는 Windows PowerShell을 사용 합니다. 가상 스위치에 대 한 자세한 참조 [Hyper-v 가상 스위치](../../hyper-v-virtual-switch/Hyper-V-Virtual-Switch.md)합니다.  
  
가상 컴퓨터 네트워킹 복잡 한 주제를 수 있습니다. 처럼 사용할 수 있는 몇 가지 새로운 가상 스위치 기능 되며 [포함 된 팀 전환 (SET)](../../hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md#switch-embedded-teaming-set)합니다. 하지만 기본 네트워킹은 매우 쉽습니다. 이 항목에서는 Hyper-v에서 네트워크로 연결 된 가상 컴퓨터를 만들 수 있도록 데 필요한 만큼만 다룹니다. 네트워킹 인프라를 설정 하는 방법을 하는 방법에 대 한 자세한 내용은 검토는 [네트워킹](../../../networking/Networking.md) 설명서입니다.   
  
## <a name="create-a-virtual-switch-by-using-hyper-v-manager"></a>Hyper-v 관리자를 사용 하 여 가상 스위치 만들기  
  
1.  Hyper-v 관리자를 열고 Hyper-v 호스트 컴퓨터 이름을 선택 합니다.  
  
2.  선택 **작업** > **가상 스위치 관리자**합니다.  
  
    ![작업 메뉴 옵션을 보여 주는 스크린 샷 > 가상 스위치 관리자](../media/Hyper-V-Action-VSwitchManager.png)  
  
3.  원하는 가상 스위치의 형식을 선택 합니다.  
  
    |연결 형식|설명|  
    |-------------------|---------------|  
    |외부|서버와 외부 네트워크에 있는 클라이언트와 통신 하는 실제 네트워크에 가상 컴퓨터에 액세스를 제공 합니다. 상호 통신에 동일한 Hyper-v 서버에 가상 컴퓨터를 허용 합니다.|  
    |내부|가상 컴퓨터와 관리 호스트 운영 체제 및 동일한 Hyper-v 서버에 가상 컴퓨터 간의 통신을 허용 합니다.|  
    |프라이빗|동일한 Hyper-v 서버에서 가상 컴퓨터 간의 통신만 허용합니다. 프라이빗 네트워크는 Hyper-v 서버에서 모든 외부 네트워크 트래픽으로부터 격리 됩니다. 이 유형의 네트워크와 격리 된 테스트 도메인과 같은 격리 된 네트워킹 환경을 만들어야 하는 경우에 유용 합니다.|  
  
4.  선택 **가상 스위치를 만들**합니다.  
  
5.  가상 스위치에 대 한 이름을 추가 합니다.  
  
6.  외부를 선택 하면 사용 하 여 원하는 네트워크 어댑터 (NIC) 및 다음 표에 설명 된 다른 모든 옵션을 선택 합니다.  
  
    ![외부 네트워크 옵션을 보여 주는 스크린 샷](../media/Hyper-V-NewVSwitch-ExternalOptions.png)  
  
    |설정 이름|설명|  
    |----------------|---------------|  
    |이 네트워크 어댑터를 공유하는 관리 운영 체제 허용|Hyper-v 호스트가 가상 스위치의 사용을 공유할 수 있도록 하 고 가상 컴퓨터와 nic 팀이 옵션을 선택 합니다. 이 옵션을 사용 호스트 사용할 수 설정을 구성 하는 가상 스위치와 같은 서비스 품질 (QoS) 설정, 보안 설정 또는 Hyper-v 가상 스위치의 다른 기능.|  
    |단일 루트 I/O 가상화 (SR-IOV) 사용|가상 컴퓨터 스위치를 무시 하 고 실제 NIC에 직접 이동에 대 한 가상 컴퓨터 트래픽을 허용 하려는 경우에이 옵션을 선택 합니다. 자세한 내용은 포스터 도우미 참조에서 [단일 루트 I/o 가상화](https://technet.microsoft.com/library/dn641211.aspx#Sec4) 를 참조 하세요. Hyper-v 네트워킹.|  
  
7.  관리 Hyper-v 호스트 운영 체제 또는 동일한 가상 스위치를 공유 하는 다른 가상 컴퓨터에서 네트워크 트래픽을 격리 하려면 **관리 운영 체제에 대 한 가상 LAN Id 사용**을 선택 합니다. 원하는 수의 VLAN ID를 변경 하거나 기본값을 그대로 적용 수 있습니다. 이 관리 운영 체제에서이 가상 스위치를 통해 모든 네트워크 통신에 사용할 가상 LAN id입니다.  
  
    ![VLAN ID 옵션을 보여 주는 스크린 샷](../media/Hyper-V-NewSwitch-VLAN.png)  
  
8.  **확인**을 클릭합니다.  
  
9. **예**를 클릭합니다.  
  
    !["보류 중인 변경 내용을 방해가 될 수 있습니다 네트워크 연결이" 메시지를 보여 주는 스크린 샷](../media/Hyper-V-NewVSwitch-DisruptNetwork.png)  
  
## <a name="create-a-virtual-switch-by-using-windows-powershell"></a>Windows PowerShell을 사용 하 여 가상 스위치 만들기  
  
1.  Windows 데스크톱에서 시작 단추를 클릭하고 **Windows PowerShell** 이름의 일부를 입력합니다.  
  
2.  Windows PowerShell을 마우스 오른쪽 단추로 클릭 하 고 선택 **관리자 권한으로 실행**합니다.  
  
3.  실행 하 여 기존 네트워크 어댑터를 찾을 [Get-netadapter](https://technet.microsoft.com/library/jj130867.aspx) cmdlet입니다. 가상 스위치를 사용 하 여 원하는 네트워크 어댑터 이름을 기록해 둡니다.  
  
    ```  
    Get-NetAdapter  
    ```  
  
4.  사용 하 여 가상 스위치를 만들기는 [New-vmswitch](https://technet.microsoft.com/library/hh848455.aspx) cmdlet입니다. 예를 들어 외부 가상 스위치 라는 이더넷 네트워크 어댑터를 사용 하 여 ExternalSwitch 및 **관리 운영 체제를이 네트워크 어댑터를 공유할 수 있도록** 를 설정한 다음 명령을 입력 합니다.  
  
    ```  
    New-VMSwitch -name ExternalSwitch  -NetAdapterName Ethernet -AllowManagementOS $true  
    ```  
  
    내부 스위치를 만들려면 다음 명령을 실행 합니다.  
  
    ```  
    New-VMSwitch -name InternalSwitch -SwitchType Internal  
    ```  
  
    프라이빗 스위치를 만들려면 다음 명령을 실행 합니다.  
  
    ```  
    New-VMSwitch -name PrivateSwitch -SwitchType Private  
    ```  
  
Windows Server 2016에서 개선 된 또는 새 가상 스위치 기능을 소개 하는 고급 Windows PowerShell 스크립트를 참조 하십시오. [원격 직접 메모리 액세스 및 포함 된 팀 전환](../../hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md)합니다.  

  
## <a name="next-step"></a>다음 단계  
[Hyper-V에서 가상 머신 만들기](Create-a-virtual-machine-in-Hyper-V.md)  
  


