---
title: vRSS(가상 수신측 배율)
description: Windows Server의 vRSS (가상 수신측 배율)에 대해 알아보고, VM의 여러 논리 프로세서 코어에서 들어오는 네트워크 트래픽의 부하를 분산 하도록 가상 네트워크 어댑터를 구성 하는 방법에 대해 알아봅니다. 호스트 가상 네트워크 인터페이스 카드 (vNIC)에 대 한 여러 실제 코어를 구성할 수도 있습니다.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 9be477b3-f81d-4e84-a6b0-ac4c1ea97715
ms.date: 09/05/2018
ms.localizationpriority: medium
manager: dougkim
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 8841e0e5b33df6b44d63598ebf1f29caf89e1f3f
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80315251"
---
# <a name="virtual-receive-side-scaling-vrss"></a>가상 수신측 배율 \(vRSS\)

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목에서는 가상 수신측 배율 (vRSS) 및 VM의 여러 논리 프로세서 코어에서 들어오는 네트워크 트래픽의 부하를 분산 하도록 가상 네트워크 어댑터를 구성 하는 방법에 대해 알아봅니다. 또한 vRSS를 사용 하 여 호스트 가상 네트워크 인터페이스 카드 \(vNIC\)에 대 한 여러 실제 코어를 구성할 수도 있습니다.

이 구성을 사용 하면 가상 네트워크 어댑터의 부하를 VM\)\(가상 컴퓨터의 여러 가상 프로세서에 분산 하 여 VM이 단일 논리적 프로세서를 사용 하는 것 보다 더 많은 네트워크 트래픽을 더 빠르게 처리할 수 있습니다.

>[!TIP]
>여러 프로세서, 단일 다중 코어 프로세서 또는 둘 이상의 코어 프로세서를 설치 하 고 VM 사용을 위해 구성 하는\-Hyper-v 호스트의 Vm에서 vRSS를 사용할 수 있습니다.

vRSS는 다른 모든 하이퍼\-V 네트워킹 기술과 호환 됩니다. vRSS는\-Hyper-v 호스트의 가상 머신 큐 \(VMQ\) VM 또는 호스트 vNIC에 따라 달라 집니다.

기본적으로 Windows Server는 vRSS를 사용 하도록 설정 하지만, Windows PowerShell을 사용 하 여 VM에서 사용 하지 않도록 설정할 수 있습니다. 자세한 내용은 [RSS 및 vrss를 위한 vrss 및 Windows PowerShell 명령](vrss-wps.md) [관리](vrss-manage.md) 를 참조 하세요.



## <a name="operating-system-compatibility"></a>운영 체제 호환성

Windows Server 2016를 실행 하는 다중 프로세서 또는 다중 코어 VM의 모든 다중 프로세서 또는 다중 코어 컴퓨터에서 RSS를 사용할 수 있습니다.

다음 Microsoft 운영 체제를 실행 하는 다중 프로세서 또는 다중 코어 Vm은 vRSS도 지원 합니다.

- Windows Server 2016
- Windows 10 Pro 또는 Enterprise
- Windows Server 2012 R2
- Windows 8.1 Pro 또는 Enterprise
- Windows server 2012 R2 통합 구성 요소가 설치 된 windows Server 2012
- Windows 8 및 Windows Server 2012 R2 통합 구성 요소가 설치 되어 있습니다.

Hyper-v에서 게스트 운영 체제로 FreeBSD 또는 Linux를 실행 하는 Vm에 대 한 vRSS 지원에 대 한 자세한 내용은 [Windows에서 hyper-v에 대해 지원 되는 linux 및 FreeBSD virtual machines](https://docs.microsoft.com/windows-server/virtualization/hyper-v/Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows)를 참조 하세요.
  
## <a name="hardware-requirements"></a>하드웨어 요구 사항

다음은 vRSS에 대 한 하드웨어 요구 사항입니다.
 
- 실제 네트워크 어댑터는 VMQ\)가상 머신 큐 \(를 지원 해야 합니다. VMQ를 사용 하지 않도록 설정 하거나 지원 하지 않는 경우 하이퍼\-V 호스트와 호스트에 구성 된 모든 Vm에 대해 vRSS를 사용 하지 않도록 설정 합니다.
- 네트워크 어댑터의 연결 속도는 10gbps 이상 이어야 합니다.
- VRSS를 사용 하려면 여러 프로세서나 하나 이상의 다중\-코어 프로세서를 사용 하 여 하이퍼\-V 호스트를 구성 해야 합니다.
- 가상 컴퓨터 \(Vm\) 둘 이상의 논리 프로세서를 사용 하도록 구성 해야 합니다.


## <a name="use-case-scenarios"></a>사용 사례 시나리오

다음 두 가지 사용 사례 시나리오에서는 프로세서 부하 분산 및 소프트웨어 부하 분산을 위한 vRSS의 일반적인 사용법을 나타냅니다.

### <a name="processor-load-balancing"></a>프로세서 부하 분산
  
네트워크 관리자 인 Anthony는 단일 루트 입력-출력 가상화 \(\-SR-IOV\)를 지 원하는 두 개의 네트워크 어댑터를 사용 하 여 새 Hyper-v 호스트를 설정 합니다. VM 파일 서버를 호스트 하는 Windows Server 2016을 배포 합니다.

하드웨어 및 소프트웨어를 설치한 후 Anthony는 8 개의 가상 프로세서와 4096의 메모리를 사용 하도록 VM을 구성 합니다. 불행 하 게, Anthony는 가상 스위치를 사용 하\-여 만든 가상 스위치를 통해 Vm이 정책 적용을 사용 하기 때문에\-SR-IOV를 사용 하도록 설정 하는 옵션이 없습니다. 이로 인해 Anthony는 sr-iov\-대신 vRSS를 사용 하기로 결정 합니다.

처음에 Anthony는 vRSS에서 사용할 수 있도록 Windows PowerShell을 사용 하 여 4 개의 가상 프로세서를 할당 합니다. 일주일 후 파일 서버를 사용 하는 것이 매우 인기 있으므로 Anthony는 VM의 성능을 확인 합니다.  4 개의 가상 프로세서의 전체 사용률을 검색 합니다.

이로 인해 Anthony는 vRSS에서 사용 하기 위해 VM에 프로세서를 추가 하기로 결정 합니다.  가상 프로세서를 두 개 더 할당 합니다 .이 VM은 vRSS에서 자동으로 사용 하 여 대량 네트워크 부하를 처리할 수 있도록 합니다. 이로 인해 VM 파일 서버에 대 한 성능이 향상 되 고 6 개 프로세서가 네트워크 트래픽 부하를 효율적으로 처리 합니다.


### <a name="software-load-balancing"></a>소프트웨어 부하 분산

네트워크 관리자 인 Sandra는 해당 시스템 중 하나에서 하나의 고성능 VM을 설정 하 여 소프트웨어 부하 분산 장치 역할을 합니다. 이 단일 VM에 사용 가능한 모든 논리적 프로세서를 할당 했습니다.

Windows Server를 설치한 후에는 vRSS를 사용 하 여 VM의 여러 논리적 프로세서에서 병렬 네트워크 트래픽 처리를 가져옵니다. Windows Server는 vRSS를 사용 하도록 설정 하므로 Sandra는 구성을 변경할 필요가 없습니다.


## <a name="related-topics"></a>관련 항목

- [VRSS 사용 계획](vrss-plan.md)
- [Virtual Network 어댑터에서 vRSS 사용](vrss-enable.md)
- [vRSS 관리](vrss-manage.md)
- [vRSS 질문과 대답](vrss-faq.md)
- [RSS 및 vRSS에 대 한 Windows PowerShell 명령](vrss-wps.md)

---
