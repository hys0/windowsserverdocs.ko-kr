---
title: VRSS 사용 계획
description: VRSS를 사용 하 여 Windows Server 2016에서에 대 한 가상 머신 및 Hyper-v 호스트를 준비 하려면이 항목에서는 사용할 수 있습니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 695e6192-5e84-4ab4-b33e-8ebf6b8f5cbb
ms.localizationpriority: medium
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/04/2018
ms.openlocfilehash: e6558b00e87721d8ab81c84946a14745c4faa812
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59850444"
---
# <a name="plan-the-use-of-vrss"></a>VRSS 사용 계획

>적용 대상: Windows Server (반기 채널), Windows Server 2016

하지만 Windows Server 2016에서 vRSS는 기본적으로 가상 컴퓨터에서 제대로 작동 하려면 vRSS를 허용 하도록 환경을 준비 해야 \(VM\) 컴퓨터나 호스트 가상 어댑터 \(vNIC\)합니다. Windows Server 2012 R2에서 vRSS는 기본적으로 비활성화 되었습니다.

계획을 vRSS 사용 준비를 확인 합니다.

- 실제 네트워크 어댑터는 가상 머신 큐를 사용 하 여 호환 \(VMQ\) 10gbps의 링크 속도 이상 및 합니다.
- 실제 NIC에를 Hyper VMQ가 사용\-V 가상 스위치 포트
- 입력이 없는 단일 루트\-출력 가상화 \(SR\-IOV\) VM에 대해 구성 합니다.
- NIC 팀 올바르게 구성 됩니다.
- VM에 여러 개의 논리적 프로세서 \(LPs\)합니다.

>[!NOTE]
>vRSS는 또한 RSS가 설정 되어 있는 모든 호스트 Vnic에 대해 기본적으로 사용 하도록 설정 됩니다.

다음은 이러한 준비 단계를 완료 하는 데 필요한 추가 정보입니다.
  
1. **네트워크 어댑터 용량**합니다. 네트워크 어댑터를 가상 머신 큐와 호환 되는지 확인 하십시오 \(VMQ\) 10gbps의 링크 속도 이상 및 합니다. 링크 속도가 경우 10gbps 미만인, Hyper\-V 가상 스위치에서 Windows PowerShell 명령 실행 하면 사용 하도록 설정 하는 대로 VMQ 계속 표시 하는 경우에 기본적으로 VMQ를 비활성화 **Get NetAdapterVmq**합니다. 명령을 사용 하 여 VMQ이 활성화 되거나 비활성화를 확인 하는 데 사용할 수 하는 한 가지 방법은 것 **Get NetAdapterVmqQueue**합니다.  VMQ는 사용 하지 않도록 설정 하는 경우이 명령 실행 하면 VM 또는 호스트 가상 네트워크 어댑터에 할당 된 QueueID 없습니다 임을 보여 줍니다. 
  
2. **VMQ를 사용 하도록 설정**합니다. VMQ가 호스트 컴퓨터에서 사용되는지 확인합니다. vRSS는 호스트에서 VMQ를 지원 하지 않으면 작동 하지 않습니다. 실행 하 여 VMQ가 사용 되는지 확인할 수 있습니다 **Get-vmswitch** 및 가상 스위치를 사용 하는 어댑터를 검색 합니다. 그런 다음 **Get NetAdapterVmq** 를 실행하여 어댑터가 결과에 표시되고 VMQ를 사용하는지 확인합니다.
  
3. **SR의 부재\-IOV**합니다. 단일 루트를 입력 하는 확인\-출력 가상화 \(SR\-IOV\) 가상 함수 \(VF\) 드라이버 VM 네트워크 인터페이스 연결 되어 있지 않습니다. 사용 하 여이 확인할 수 있습니다 합니다 **Get-netadaptersriov** 명령입니다. VF 드라이버가 로드 되 면 RSS vRSS에서 구성한 대신이 드라이버의 배율 설정을 사용 합니다. VF 드라이버에서 RSS를 지원 하지 않습니다, 경우에 vRSS 비활성화 됩니다.
  
4. **NIC 팀 구성**합니다. NIC 팀을 사용 하는 경우 NIC 팀 설정으로 작동 하도록 VMQ을 적절히 구성 하는 것이 중요 합니다. NIC 팀 배포 및 관리 하는 방법에 대 한 자세한 내용은 [NIC 팀](https://docs.microsoft.com/windows-server/networking/technologies/nic-teaming/nic-teaming)합니다.

5. **LPs 수가**합니다. VM에 둘 이상의 논리 프로세서 있는지 확인 하십시오 \(LP\)합니다. vRSS는 트래픽을 부하 분산 받은 병렬 처리를 위해 여러 LPs Hyper-v 호스트 또는 VM에서 RSS에 의존 합니다. Windows PowerShell 명령을 실행 하 여 VM에 얼마나 많은 LPs를 확인할 수 있습니다 **Get-vmprocessor** 호스트에서 합니다. 명령을 실행 하면 LPs 수가 개수 열 항목을 확인할 수 있습니다.

호스트 vNIC에는 항상 모든 물리적 프로세서;에 대 한 액세스 권한이 특정 수의 프로세서를 사용 하도록 호스트 vNIC를 구성 하는 설정을 사용 하 여 **-BaseProcessorNumber** 하 고 **-MaxProcessors** 실행 하는 경우는 **Set-netadapterrss** Windows PowerShell 명령입니다.

---