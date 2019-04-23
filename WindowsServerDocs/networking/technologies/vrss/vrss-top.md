---
title: vRSS(가상 수신측 배율)
description: 가상 수신측 배율 (vRSS) 하는 방법에 대 한 Windows Server 및 들어오는 네트워크 트래픽 분산 부하를 여러 논리적 프로세서 코어 VM에서 가상 네트워크 어댑터를 구성 하는 방법에 알아봅니다. 호스트의 여러 실제 코어를 구성할 수도 있습니다 가상 네트워크 인터페이스 카드 (vNIC).
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 9be477b3-f81d-4e84-a6b0-ac4c1ea97715
ms.date: 09/05/2018
ms.localizationpriority: medium
manager: dougkim
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 0c1cb11cb8ce69463a31cfa5061290f79d8dda91
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59875234"
---
# <a name="virtual-receive-side-scaling-vrss"></a>가상 수신측 배율 \(vRSS\)

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 항목에서는 Virtual Receive Side Scaling (vRSS) 및 여러 논리적 프로세서 코어 VM에서 들어오는 네트워크 트래픽 분산을 로드 하도록 가상 네트워크 어댑터를 구성 하는 방법을 배웁니다. VRSS는 호스트에 대 한 여러 실제 코어를 구성 하려면 사용할 수도 있습니다 가상 네트워크 인터페이스 카드 \(vNIC\)합니다.

이 구성은 가상 네트워크 어댑터를 가상 컴퓨터의 여러 가상 프로세서를 분산할 수에서 부하를 허용 \(VM\), VM이 단일을 사용 하 여 보다 빠르게 더 많은 네트워크 트래픽을 처리할 수 있도록 논리 프로세서입니다.

>[!TIP]
>VRSS를 사용 하 여 하이퍼의 Vm에서\-다중 코어 프로세서, 다중 프로세서, 단일에 있는 호스트 또는 다중 코어 프로세서의 설치 및 사용 하 여 VM에 대해 구성 된 둘 이상의 합니다.

vRSS는 다른 모든 하이퍼 호환\-V 네트워킹 기술입니다. vRSS는 가상 머신 큐에 따라 달라 집니다 \(VMQ\) Hyper에서\-호스트 및 호스트 vNIC 또는 VM에서 RSS 합니다.

기본적으로 Windows Server에는 vRSS를 수행할 수 있지만 Windows PowerShell을 사용 하 여 VM에서 비활성화할 수 있습니다. 자세한 내용은 참조 하세요. [vRSS를 관리할](vrss-manage.md) 하 고 [RSS 및 vRSS Windows PowerShell 명령](vrss-wps.md)입니다.



## <a name="operating-system-compatibility"></a>운영 체제 호환성

다중 프로세서 또는 다중 코어 컴퓨터 또는 Windows Server 2016을 실행 하는 모든 다중 프로세서 또는 다중 코어 VM에서 vRSS에서 RSS를 사용할 수 있습니다.

다중 프로세서 또는 코어 다음 Microsoft 운영 체제를 실행 중인 Vm도 vRSS를 지원 합니다.

- Windows Server 2016
- Windows 10 Pro 또는 Enterprise
- Windows Server 2012 R2
- Windows 8.1 Pro 또는 Enterprise
- Windows Server 2012 R2 통합 구성 요소가 설치 된 Windows Server 2012.
- Windows Server 2012 R2 통합 구성 요소가 설치 된 Windows 8입니다.

Hyper-v에서 게스트 운영 체제로 Linux 또는 FreeBSD를 실행 하는 Vm에 대 한 vRSS 지원에 대 한 정보를 참조 하세요 [Windows의 Hyper-v에 대 한 지원 되는 Linux 및 FreeBSD 가상 컴퓨터](https://docs.microsoft.com/windows-server/virtualization/hyper-v/Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows)합니다.
  
## <a name="hardware-requirements"></a>하드웨어 요구 사항

다음은 vRSS 하드웨어 요구 사항입니다.
 
- 실제 네트워크 어댑터에서 가상 머신 큐를 지원 해야 합니다 \(VMQ\)합니다. VRSS Hyper 되지 VMQ를 사용할 수 없거나 지원 되지 않는 경우\-V 호스트 및 호스트에 구성 된 Vm입니다.
- 네트워크 어댑터에 10gbps의 링크 속도 이상 있어야 합니다.
- 하이퍼\-다중 프로세서 또는 다중 하나 이상의 호스트를 구성 해야\-코어 프로세서 vRSS를 사용 하도록 합니다.
- Virtual machines \(Vm\) 두 개 이상의 논리적 프로세서를 사용 하도록 구성 되어야 합니다.


## <a name="use-case-scenarios"></a>사용 사례 시나리오

다음 두 가지 사용 사례 시나리오는 프로세서 부하 분산 및 소프트웨어 부하 분산에 대 한 vRSS의 일반 용도 설명 합니다.

### <a name="processor-load-balancing"></a>프로세서 부하 분산
  
네트워크 관리자 인 Anthony 단일 루트 입출력 가상화를 지 원하는 두 개의 네트워크 어댑터를 사용 하 여 새 Hyper-v 호스트를 설정 하는 \(SR\-IOV\)합니다. 또한 VM 파일 서버를 호스팅하도록 Windows Server 2016을 배포 합니다.

하드웨어 및 소프트웨어를 설치한 후 Anthony는 8 개의 가상 프로세서를 사용 하는 VM 및 메모리 중 4096MB를 구성 합니다. 아쉽게도 Anthony는 옵션이 없으므로 SR 켜는\-IOV Vm 하이퍼를 사용 하 여 만든 가상 스위치를 통해 정책 적용을 의존 하므로\-V 가상 스위치 관리자입니다. 이 인해 Anthony SR 대신 vRSS를 사용 하기로\-IOV 합니다.

처음에 Anthony는 vRSS 사용 가능 하도록 Windows PowerShell을 사용 하 여 4 개의 가상 프로세서를 할당 합니다. 일주일 후 파일 서버의 사용 되도록 매우 인기 있는 Anthony는 성능을 VM의 확인 표시 되었습니다.  4 개의 가상 프로세서의 전체 사용률을 발견 했습니다.

이 인해 Anthony vRSS에서 사용할 VM에 프로세서를 추가 하기로 결정 합니다.  그는 대규모 네트워크 부하를 처리 하는 데는 vRSS를 자동으로 제공 하는 VM에 두 개의 가상 프로세서를 할당 합니다. 최소한만 VM 파일 서버에 대해 더 나은 성능을 효율적으로 네트워크 트래픽 부하를 처리 하는 6 개의 프로세서를 사용 하 여 발생 합니다.


### <a name="software-load-balancing"></a>소프트웨어 부하 분산

Sandra, 네트워크 관리자를 설정 하는 단일 고성능 VM 시스템 중 하나에서 소프트웨어 부하 분산 장치 역할을 합니다. 사용자가이 단일 VM에 사용 가능한 모든 논리적 프로세서 할당.

Windows Server를 설치한 후 VM에 여러 개의 논리적 프로세서에서 처리 하는 병렬 네트워크 트래픽을 vRSS 사용 합니다. Windows Server에는 vRSS 수, 때문에 Sandra 모든 구성을 변경할 필요가 없습니다.


## <a name="related-topics"></a>관련 항목

- [VRSS 사용 계획](vrss-plan.md)
- [가상 네트워크 어댑터에서 vRSS를 사용 하도록 설정](vrss-enable.md)
- [VRSS를 관리 합니다.](vrss-manage.md)
- [vRSS Frequently Asked Questions](vrss-faq.md)
- [RSS 및 vRSS Windows PowerShell 명령](vrss-wps.md)

---
