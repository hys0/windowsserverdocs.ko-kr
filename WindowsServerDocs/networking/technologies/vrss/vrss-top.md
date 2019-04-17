---
title: 가상 수신측 배율(vRSS)
description: 가상 수신측 배율 (vRSS)에 대 한 Windows Server 및 VM의 여러 논리 프로세서 코어에서 들어오는 네트워크 트래픽을 잔액을 로드 하는 가상 네트워크 어댑터를 구성 하는 방법을 알아봅니다. 호스트에 대해 다중 물리적 코어를 구성할 수도 가상 네트워크 인터페이스 카드 (vNIC).
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
ms.sourcegitcommit: e84e328c13a701e8039b16a4824a6e58a6e59b0b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/22/2018
ms.locfileid: "4133689"
---
# 가상 \(vRSS\) 배율 쪽 수신

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목에서는 가상 수신측 배율 (vRSS) 및 VM의 여러 논리 프로세서 코어에서 들어오는 네트워크 트래픽을 잔액을 로드 하는 가상 네트워크 어댑터를 구성 하는 방법에 대해 알아봅니다. 호스트 가상 네트워크 인터페이스 카드 \(vNIC\)에 대 한 여러 물리적 코어를 구성 하려면 vRSS를 사용할 수도 있습니다.

이 구성을 가상 컴퓨터에서 여러 가상 프로세서 분산 하는 가상 네트워크 어댑터에서 로드를 통해 \(VM\), 단일 논리 프로세서가 있는 것 보다 더 신속 하 게 더 많은 네트워크 트래픽을 처리 하기 위해 VM을 허용 합니다.

>[!TIP]
>여러 개의 프로세서가 있는, 단일 여러 코어 프로세서 Hyper\-v 호스트에서 Vm에서 vRSS를 사용할 수 있는 또는 둘 이상의 여러 코어 프로세서 설치 하 고 VM 사용을 위해 구성 합니다.

vRSS 모든 다른 Hyper\-v 네트워킹 기술 호환 됩니다. vRSS는 Hyper\-v 호스트에서 가상 컴퓨터 큐 \(VMQ\) 및 호스트 vNIC 또는 VM에서 RSS에 따라 달라 집니다.

기본적으로 Windows Server를 vRSS, 사용 되지만 Windows PowerShell을 사용 하 여 VM에서 비활성화할 수 있습니다. 자세한 내용은 [관리 vRSS](vrss-manage.md) 및 [Windows PowerShell 명령 RSS 및 vRSS를](vrss-wps.md)참조 하세요.



## 운영 체제 호환성

모든 다중 프로세서 코어-컴퓨터 또는 Windows Server 2016을 실행 하는 모든 다중 프로세서 또는 코어 VM-에서 vRSS에서 RSS를 사용할 수 있습니다.

다중 프로세서 또는 다음 Microsoft 운영 체제를 실행 중인 Vm 코어 vRSS도 지원 합니다.

- Windows Server 2016
- Windows 10 Pro 또는 Enterprise
- Windows Server 2012 R2
- Windows 8.1 Pro 또는 Enterprise
- Windows Server 2012 설치 된 Windows Server 2012 R2 통합 구성 요소입니다.
- 설치 된 Windows Server 2012 R2 통합 구성 요소를 사용 하 여 Windows 8 합니다.

FreeBSD 또는 Linux 게스트 운영 체제로 Hyper-v에서 실행 되는 Vm에 대 한 vRSS 지원에 대 한 자세한 내용은 [Windows의 Hyper-v에 대 한 지원 되는 Linux 및 FreeBSD 가상 컴퓨터](https://docs.microsoft.com/windows-server/virtualization/hyper-v/Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows)를 참조 하세요.
  
## 하드웨어 요구 사항

다음은 vRSS에 대 한 하드웨어 요구 사항입니다.
 
- 실제 네트워크 어댑터는 가상 컴퓨터 큐 \(VMQ\) 지원 해야 합니다. VMQ, 사용 하지 않거나 지원 되지 않는 경우에 Hyper\-v 호스트와 호스트에서 구성 된 모든 Vm에 대 한 vRSS 비활성화 됩니다.
- 네트워크 어댑터를 연결 속도 10 g b p s 이상이 있어야 합니다.
- 여러 개의 프로세서 또는 vRSS를 사용 하 여 하나 이상의 \ 코어 프로세서 Hyper\-v 호스트를 구성 해야 합니다.
- 가상 컴퓨터 \(VMs\) 두 개 이상의 논리 프로세서를 사용 하 여 구성 해야 합니다.


## 사용 사례 시나리오

다음 두 가지 사용 사례 시나리오는 프로세서 부하 분산 및 소프트웨어 부하 분산 vRSS 일반적으로 사용을 나타냅니다.

### 프로세서 부하 분산
  
안토니, 네트워크 관리자가 단일 루트 입력 출력 가상화 \(SR\-IOV\)를 지 원하는 두 가지 네트워크 어댑터를 사용 하 여 새 Hyper-v 호스트 설정 그 Windows Server 2016 호스트 VM 파일 서버를 배포 합니다.

하드웨어 및 소프트웨어를 설치한 후 안토니 8 개의 가상 프로세서를 사용 하 여 VM 및 4096 MB의 메모리를 구성 합니다. 안타깝게도 안토니가 Vm Hyper\-v 가상 스위치 관리자를 사용 하 여 만든 그 가상 스위치를 통해 정책 적용에 의존 하므로 SR\ IOV에서 기능을 설정할 수는 없습니다. 이 인해 안토니 SR\ IOV 대신 vRSS 사용 하기로 결정 합니다.

처음에 안토니 vRSS에서 사용 가능 하도록 Windows PowerShell을 사용 하 여 4 개의 가상 프로세서를 할당 합니다. 일주일 안토니 VM의 성능을 확인 하므로 상당히 인기 있는 것 처럼 후 파일 서버를 사용 합니다.  그 전체 사용률 4 개의 가상 프로세서를 검색합니다.

이 인해 안토니 vRSS 하 여 프로세서 사용 하기 위해 VM에 추가 하기로 결정 합니다.  그 큰 네트워크 부하를 처리 하는 데 vRSS를 자동으로 제공 되는 VM에 두 개의 가상 프로세서를 할당 합니다. 자신의 노력을 효율적으로 네트워크 트래픽 부하를 처리 하는 6 개의 프로세서를 사용 하 여 VM 파일 서버에 대 한 더 나은 성능을 발생 합니다.


### 소프트웨어 부하 분산

조, 네트워크 관리자는 소프트웨어 부하 분산 장치 담당자가 시스템 중 하나에서 단일 고성능 VM를 설정 합니다. 사용자가 사용할 수 있는 모든 논리 프로세서가 단일 VM에 할당 합니다.

Windows Server를 설치한 후 vRSS 사용 하 여 VM에서 여러 논리 프로세서에서 처리 하는 병렬 네트워크 트래픽을 가져옵니다. Windows Server vRSS, 사용 하기 때문에 조 구성을 변경할 필요가 없습니다.


## 관련 항목

- [VRSS 사용 계획](vrss-plan.md)
- [VRSS 가상 네트워크 어댑터에서 사용 하도록 설정](vrss-enable.md)
- [VRSS 관리](vrss-manage.md)
- [vRSS 질문과 대답](vrss-faq.md)
- [RSS 및 vRSS Windows PowerShell 명령](vrss-wps.md)

---
