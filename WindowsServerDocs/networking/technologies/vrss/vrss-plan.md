---
title: VRSS 사용 계획
description: Windows Server 2016에서 vRSS 사용 하기 위한 가상 컴퓨터와 Hyper-v 호스트를 준비 하려면이 항목에서는 사용할 수 있습니다.
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
ms.sourcegitcommit: e84e328c13a701e8039b16a4824a6e58a6e59b0b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/22/2018
ms.locfileid: "4133389"
---
# VRSS 사용 계획

>적용 대상: Windows Server(반기 채널), Windows Server 2016

하지만 Windows Server 2016에서 vRSS는 기본적으로 활성화 되어 vRSS 가상 컴퓨터에서 제대로 작동 하도록 허용 하도록 환경을 준비 해야 \(VM\) 또는 호스트 가상 어댑터 \(vNIC\) 합니다. Windows Server 2012 R2 vRSS는 기본적으로 비활성화 되었습니다.

계획 하 고 vRSS의 사용을 준비 하는 경우 다음을 확인 합니다.

- 실제 네트워크 어댑터는 가상 컴퓨터 큐 \(VMQ\) 호환 되며 10 g b p s의 연결 속도 이상 있습니다.
- Hyper\-v 가상 스위치 포트와 물리적 NIC에 VMQ 사용 하도록 설정
- VM에 대해 구성 된 단일 루트 Input\ 출력 가상화 \(SR\-IOV\) 없는 경우.
- NIC 팀 올바르게 구성 됩니다.
- VM에 여러 개의 논리 프로세서가 \(LPs\) 있습니다.

>[!NOTE]
>vRSS는 또한 RSS 사용할 수 있는 모든 호스트 Vnic 기본적으로 사용 됩니다.

다음은 이러한 준비 단계를 완료 하는 데 필요한 추가 정보입니다.
  
1. **네트워크 어댑터 용량**입니다. 네트워크 어댑터 가상 컴퓨터 큐 \(VMQ\) 호환 되 고 10 g b p s 이상의 연결 속도 확인 합니다. 연결 속도 10 미만 g b p s 이면 Hyper\-v 가상 스위치의 Windows PowerShell 명령 **Get NetAdapterVmq**결과에 사용으로 VMQ 여전히 표시 하는 경우에 기본적으로 VMQ를 비활성화 합니다. VMQ가 활성화 또는 비활성화를 확인 하는 데 사용할 수는 한 가지 방법은 명령 **Get NetAdapterVmqQueue**를 사용 하는 것입니다.  VMQ 하지 않으면이 명령의 결과 VM 또는 호스트 가상 네트워크 어댑터에 할당 된 없는 QueueID을 표시 합니다. 
  
2. **VMQ를 사용 하도록 설정**합니다. VMQ 호스트 컴퓨터에서 활성화 되어 있는지 확인 합니다. 호스트 VMQ를 지원 하지 않는 경우에 vRSS 작동 하지 않습니다. **Get VMSwitch** 를 실행 하 고 가상 스위치를 사용 하는 어댑터를 찾는 VMQ 활성화 되어 있는지 확인할 수 있습니다. 다음으로 **Get NetAdapterVmq** 를 실행 하 고 어댑터는 결과에 표시 하 고 VMQ 활성화를 확인 합니다.
  
3. **SR\ IOV 없는 경우**. 확인 하는 단일 루트 Input\ 출력 가상화 \(SR\-IOV\) 가상 함수 \(VF\) 드라이버 VM 네트워크 인터페이스에 연결 되지 않은 합니다. **Get NetAdapterSriov** 명령을 사용 하 여이 확인할 수 있습니다. VF 드라이버 로드 되는 경우 RSS vRSS 하 여 구성 하는 대신이 드라이버의 크기 조정 설정을 사용 합니다. VF 드라이버 RSS를 지원 하지 않는 경우 vRSS 비활성화 됩니다.
  
4. **NIC 팀 구성**합니다. NIC 팀을 사용 하는 경우에 VMQ NIC 팀 설정과 함께 작동 하도록 적절 하 게 구성 하는 것이 중요 합니다. NIC 팀 배포 및 관리 하는 방법에 대 한 자세한 내용은 [NIC 팀](https://docs.microsoft.com/windows-server/networking/technologies/nic-teaming/nic-teaming)을 참조 하세요.

5. **Lp의 수**입니다. VM에 여러 개의 논리 프로세서가 있는지 확인 \(LP\) 합니다. vRSS 병렬 처리를 위해 여러 Lp 트래픽을 수신 잔액을 로드 하려면 Hyper-v 호스트 또는 VM에서 RSS에 의존 합니다. 호스트에서 **Get VMProcessor** Windows PowerShell 명령을 실행 하 여 VM에 얼마나 많은 Lp 확인할 수 있습니다. 명령을 실행 한 후 Lp 수에 대 한 횟수 열 항목을 확인할 수 있습니다.

호스트 vNIC 항상 모든 물리적 프로세서;에 액세스할 수 있습니다. 특정 개수의 프로세서를 사용 하도록 호스트 vNIC를 구성 하려면 설정을 사용 하 여 **-BaseProcessorNumber** 및 **-MaxProcessors** **집합 NetAdapterRss** Windows PowerShell 명령을 실행 합니다.

---