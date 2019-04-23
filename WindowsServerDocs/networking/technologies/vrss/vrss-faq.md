---
title: vRSS Frequently Asked Questions
description: 이 항목에서는 일부 자주 묻는 질문 및 답변 vRSS를 사용 하는 것이 있습니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 61ae242e-82a8-430d-b07d-52b86c01e686
ms.localizationpriority: medium
manager: dougkim
ms.date: 09/05/2018
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 3fafe6c39285e65a9d39a76cc6b652dac5c3efbd
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59840244"
---
# <a name="vrss-frequently-asked-questions"></a>vRSS Frequently Asked Questions

이 항목에서는 일부 자주 묻는 질문 및 답변 vRSS를 사용 하는 것이 있습니다.

## <a name="what-are-the-requirements-for-the-physical-network-adapters-that-i-use-with-vrss"></a>VRSS를 사용 하 여 사용 하는 실제 네트워크 어댑터에 대 한 요구 사항은 무엇입니까?

네트워크 어댑터를 가상 머신 큐와 호환 되어야 합니다 \(VMQ\) 이상의 10gbps의 링크 속도 있어야 합니다.

자세한 내용은 [vRSS 사용 계획](vrss-plan.md)합니다.

## <a name="does-vrss-work-with-hyper-threaded-processor-cores"></a>VRSS와 함께 작동 하이퍼\-스레드 프로세서 코어?

아니요. VRSS 및 VMQ를 모두 무시 하이퍼\-스레드 프로세서 코어입니다.

## <a name="does-vrss-work-for-host-virtual-nics-vnics"></a>VRSS 작동에 대 한 호스트 가상 Nic \(Vnic\)?

예 사용 하 여는 **-ManagementOS** 가상 머신 대신 매개 변수 \(VM\) 이름에 **Set-vmnetworkadapter** Windows PowerShell 명령 및  **사용-NetAdapterRss** 호스트 vNIC에 있습니다.

자세한 내용은 [RSS 및 vRSS Windows PowerShell 명령](vrss-wps.md)입니다.

## <a name="how-many-logical-processors-does-a-vm-need-to-use-vrss"></a>VM에서 vRSS를 사용 하려면 얼마나 많은 논리 프로세서 필요 합니까?

Vm에 두 개 이상의 논리 프로세서가 필요 \(LPs\) vRSS를 사용 하는 일을 할 수 있습니다.

자세한 내용은 [vRSS 사용 계획](vrss-plan.md)합니다.

## <a name="is-vrss-compatible-with-nic-teaming"></a>VRSS는 NIC 팀과 호환 되나요?

예 NIC 팀을 사용 하는 경우 NIC 팀 설정으로 작동 하도록 VMQ을 적절히 구성 하는 것이 중요 합니다. NIC 팀 배포 및 관리 하는 방법에 대 한 자세한 내용은 [NIC 팀](https://docs.microsoft.com/windows-server/networking/technologies/nic-teaming/nic-teaming)합니다.

## <a name="vrss-is-enabled-but-how-do-i-know-if-it-is-working"></a>vRSS가 설정 되었지만 어떻게 작동 하는지? 

VRSS를 VM에서 작업 관리자를 열고 가상 프로세서 사용률을 보고 작동을 확인할 수 있습니다. VM에 설정 된 여러 연결의 경우 사용률이 0% 보다 높은 코어가 두 개를 볼 수 있습니다.

단일 TCP 세션을 부하가 분산 된 여러 논리 프로세서 코어 수 없으므로, VM 해야 받을 여러 TCP 세션 vRSS 작동 여부를 확인 합니다.

VM을 여러 TCP 세션을 수신 하는 경우 사용률이 0% 보다 높은 LP 코어가 두 개 이상 표시 되지 않도록 모든 항목의 준비 단계를 완료 했다고 [vRSS 사용 계획](vrss-plan.md)합니다.

## <a name="im-looking-at-the-host-and-not-all-of-the-processors-are-being-used-it-looks-like-every-other-one-is-being-skipped"></a>호스트를 확인해 보니 일부 프로세서가 사용되고 있지 않습니다. 하나 걸러 하나씩 건너뛰는 것 같습니다.
  
하이퍼 스레딩이 사용하도록 설정되어 있는지 확인해 보세요. VMQ와 vRSS 하이퍼 건너뛸 만들어진\-스레드 코어입니다.

## <a name="are-there-different-windows-powershell-commands-for-rss-and-vrss"></a>다른 Windows PowerShell 명령을 RSS 및 vRSS 사항이 있습니까?

그렇기도 하고 그렇지 않기도 하고. 동일한 명령을 사용 하 여 기본 호스트에서 RSS와 Vm에서 RSS에 대 한 vRSS 스위치 포트에서 사용 하도록 VM 및 vRSS-실제 NIC에 사용 하도록 VMQ을도 필요 합니다.

자세한 내용은 [RSS 및 vRSS Windows PowerShell 명령](vrss-wps.md)입니다.

---
