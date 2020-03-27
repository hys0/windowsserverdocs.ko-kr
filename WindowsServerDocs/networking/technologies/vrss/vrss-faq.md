---
title: vRSS 질문과 대답
description: 이 항목에서는 vRSS 사용에 대 한 몇 가지 일반적인 질문과 대답을 찾을 수 있습니다.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 61ae242e-82a8-430d-b07d-52b86c01e686
ms.localizationpriority: medium
manager: dougkim
ms.date: 09/05/2018
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 0ee9bf121d64eebe98798df907a2584747a00c7a
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80315364"
---
# <a name="vrss-frequently-asked-questions"></a>vRSS 질문과 대답

이 항목에서는 vRSS 사용에 대 한 몇 가지 일반적인 질문과 대답을 찾을 수 있습니다.

## <a name="what-are-the-requirements-for-the-physical-network-adapters-that-i-use-with-vrss"></a>VRSS에서 사용 하는 실제 네트워크 어댑터에 대 한 요구 사항은 무엇 인가요?

네트워크 어댑터는 VMQ\) 가상 머신 큐 \(와 호환 되어야 하며, 10gbps 이상의 링크 속도가 필요 합니다.

자세한 내용은 [VRSS 사용 계획](vrss-plan.md)을 참조 하세요.

## <a name="does-vrss-work-with-hyper-threaded-processor-cores"></a>VRSS는 하이퍼\-스레드 프로세서 코어에서 작동 하나요?

No. VRSS와 VMQ는 모두 하이퍼\-스레드 프로세서 코어를 무시 합니다.

## <a name="does-vrss-work-for-host-virtual-nics-vnics"></a>\(vNICs\)호스트 가상 Nic에 대해 vRSS가 작동 하나요?

예. **VMNetworkAdapter** Windows PowerShell 명령에서 가상 컴퓨터 \(VM\) 이름 대신 **-managementos** 매개 변수를 사용 하 고 호스트 vNIC에서 **-set-netadapterrss을 사용 하도록 설정** 합니다.

자세한 내용은 [RSS 및 vRSS에 대 한 Windows PowerShell 명령](vrss-wps.md)을 참조 하세요.

## <a name="how-many-logical-processors-does-a-vm-need-to-use-vrss"></a>VM에서 vRSS를 사용 하는 데 필요한 논리적 프로세서 수는 몇 개입니까?

VRSS를 사용할 수 있으려면 Vm에 LPs\) \(두 개 이상의 논리 프로세서가 필요 합니다.

자세한 내용은 [VRSS 사용 계획](vrss-plan.md)을 참조 하세요.

## <a name="is-vrss-compatible-with-nic-teaming"></a>VRSS는 NIC 팀과 호환 되나요?

예. NIC 팀을 사용 하는 경우 NIC 팀 설정과 함께 작동 하도록 VMQ를 올바르게 구성 하는 것이 중요 합니다. NIC 팀 배포 및 관리에 대 한 자세한 내용은 [Nic 팀](https://docs.microsoft.com/windows-server/networking/technologies/nic-teaming/nic-teaming)을 참조 하세요.

## <a name="vrss-is-enabled-but-how-do-i-know-if-it-is-working"></a>vRSS를 사용할 수 있지만 작동 하는지 어떻게 알 수 있나요? 

VM에서 작업 관리자를 열고 가상 프로세서 사용률을 확인 하 여 vRSS가 작동 하는 것을 확인할 수 있습니다. VM에 여러 연결이 설정 된 경우 0%를 초과 하는 코어를 둘 이상 볼 수 있습니다.

단일 TCP 세션은 여러 논리 프로세서 코어에서 부하가 분산 될 수 없으므로 vRSS가 작동 하는지 여부를 확인 하려면 VM에서 여러 TCP 세션을 수신 해야 합니다.

VM이 여러 TCP 세션을 수신 하지만 0%를 초과 하는 LP 코어가 하나 이상 표시 되지 않으면 [VRSS 사용 계획](vrss-plan.md)항목의 모든 준비 단계를 완료 했는지 확인 합니다.

## <a name="im-looking-at-the-host-and-not-all-of-the-processors-are-being-used-it-looks-like-every-other-one-is-being-skipped"></a>호스트를 찾고 있지만 일부 프로세서를 사용 하 고 있지 않습니다. 하나 걸러 하나씩 건너뛰는 것 같습니다.
  
하이퍼 스레딩이 사용하도록 설정되어 있는지 확인해 보세요. VMQ와 vRSS는 모두 하이퍼\-스레드 코어를 건너뛰도록 설계 되었습니다.

## <a name="are-there-different-windows-powershell-commands-for-rss-and-vrss"></a>RSS 및 vRSS에 대해 다른 Windows PowerShell 명령이 있나요?

그렇기도 하고 그렇지 않기도 하고. 네이티브 호스트의 RSS와 Vm의 RSS 모두에 동일한 명령을 사용 하는 동안에는 vRSS에서 VMQ를 실제 NIC에서 사용 하도록 설정 하 고 VM 및 vRSS를 스위치 포트에서 사용 하도록 설정 해야 합니다.

자세한 내용은 [RSS 및 vRSS에 대 한 Windows PowerShell 명령](vrss-wps.md)을 참조 하세요.

---
