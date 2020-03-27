---
title: VRSS 사용 계획
description: 이 항목을 사용 하 여 Windows Server 2016에서 vRSS를 사용 하기 위해 가상 컴퓨터 및 Hyper-v 호스트를 준비할 수 있습니다.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 695e6192-5e84-4ab4-b33e-8ebf6b8f5cbb
ms.localizationpriority: medium
manager: dougkim
ms.author: lizross
author: eross-msft
ms.date: 09/04/2018
ms.openlocfilehash: befd2839319571827b88a1c7b2777c55861e31fa
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80315268"
---
# <a name="plan-the-use-of-vrss"></a>VRSS 사용 계획

>적용 대상: Windows Server(반기 채널), Windows Server 2016

Windows Server 2016에서는 vRSS가 기본적으로 사용 하도록 설정 되어 있습니다. 그러나 vRSS가 가상 컴퓨터 \(VM\) 또는 호스트 가상 어댑터 \(vNIC\)에서 올바르게 작동할 수 있도록 환경을 준비 해야 합니다. Windows Server 2012 r 2에서 vRSS는 기본적으로 사용 하지 않도록 설정 되었습니다.

VRSS 사용을 계획 하 고 준비 하는 경우 다음을 확인 합니다.

- 실제 네트워크 어댑터는 VMQ\) 가상 머신 큐 \(와 호환 되며 연결 속도가 10gbps 이상입니다.
- VMQ는 실제 NIC 및 하이퍼\-V 가상 스위치 포트에서 사용 하도록 설정 됩니다.
- VM에 대해 구성 된\)\-\(sr-iov\-단일 루트 입력이 없습니다.
- NIC 팀이 올바르게 구성 되어 있습니다.
- VM에 LPs\)\(여러 논리 프로세서가 있습니다.

>[!NOTE]
>또한 기본적으로 RSS를 사용 하는 모든 호스트 vNICs에 대해 vRSS를 사용 하도록 설정 됩니다.

다음은 이러한 준비 단계를 완료 하는 데 필요한 추가 정보입니다.
  
1. **네트워크 어댑터 용량**. 네트워크 어댑터가 VMQ\) 가상 머신 큐 \(와 호환 되 고 연결 속도가 10gbps 이상 인지 확인 합니다. 링크 속도가 10gbps 미만이 면 Windows PowerShell 명령 **set-netadaptervmq**의 결과에서 계속 vmq를 사용 하는 경우에도 하이퍼\-V 가상 스위치는 vmq를 기본적으로 사용 하지 않도록 설정 합니다. VMQ가 사용 또는 사용 안 함으로 설정 되었는지 확인 하는 데 사용할 수 있는 한 가지 방법은 **NetAdapterVmqQueue**명령을 사용 하는 것입니다.  VMQ를 사용 하지 않도록 설정 하면 VM 또는 호스트 가상 네트워크 어댑터에 할당 된 QueueID 없음을이 명령의 결과에 표시 됩니다. 
  
2. **VMQ를 사용 하도록 설정**합니다. VMQ가 호스트 컴퓨터에서 사용되는지 확인합니다. 호스트가 VMQ를 지원 하지 않는 경우 vRSS가 작동 하지 않습니다. **Vm** 을 실행 하 여 VMQ를 사용 하도록 설정 하 고 가상 스위치가 사용 중인 어댑터를 찾으면이를 확인할 수 있습니다. 그런 다음 **Get NetAdapterVmq** 를 실행하여 어댑터가 결과에 표시되고 VMQ를 사용하는지 확인합니다.
  
3. Sr-iov **\-의 존재**하지 않습니다. 단일 루트 입력\-\(SR\-장치\) 가상 함수가 VM 네트워크 인터페이스에 연결 되어 있지 않은지 확인 합니다 \(\) **이렇게 하려면 get-netadaptersriov** 명령을 사용 하 여이를 확인할 수 있습니다. VF 드라이버가 로드 되 면 RSS는 vRSS로 구성 된 드라이버 대신 크기 조정 설정을 사용 합니다. VF 드라이버에서 RSS를 지원 하지 않는 경우 vRSS를 사용할 수 없습니다.
  
4. **NIC 팀 구성**. NIC 팀을 사용 하는 경우 NIC 팀 설정과 함께 작동 하도록 VMQ를 올바르게 구성 하는 것이 중요 합니다. NIC 팀 배포 및 관리에 대 한 자세한 내용은 [Nic 팀](https://docs.microsoft.com/windows-server/networking/technologies/nic-teaming/nic-teaming)을 참조 하세요.

5. **LPs의 수**입니다. VM에 LP\)\(두 개 이상의 논리 프로세서가 있는지 확인 합니다. vRSS는 VM 또는 Hyper-v 호스트의 RSS를 사용 하 여 병렬 처리를 위해 수신 된 트래픽의 부하를 여러 LPs에 분산 합니다. 호스트에서 Windows PowerShell 명령 **가져오기-VMProcessor** 를 실행 하 여 VM에 있는 lps의 수를 확인할 수 있습니다. 명령을 실행 한 후 LPs의 개수 열 항목을 확인할 수 있습니다.

호스트 vNIC 항상 모든 실제 프로세서에 액세스할 수 있습니다. 호스트 vNIC에서 특정 수의 프로세서를 사용 하도록 구성 하려면 **Set-netadapterrss** Windows PowerShell 명령을 실행할 때 **BaseProcessorNumber** 및 **-maxprocessors** 설정을 사용 합니다.

---