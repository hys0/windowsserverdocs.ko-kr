---
ms.assetid: 45a65504-70b5-46ea-b2e0-db45263fabaa
title: 가상화된 도메인 컨트롤러에 Hyper-V 복제본 사용 지원
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 0203c6de55a4e691d7c484351a3280c49891f317
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59866284"
---
# <a name="support-for-using-hyper-v-replica-for-virtualized-domain-controllers"></a>가상화된 도메인 컨트롤러에 Hyper-V 복제본 사용 지원

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 DC(도메인 컨트롤러)로 실행되는 VM(가상 컴퓨터)을 복제하는 데 Hyper-V 복제본을 사용할 수 있는지에 대해 설명합니다. Hyper-V 복제본은 Windows Server 2012부터 제공되는 Hyper-V의 새로운 기능으로, VM 수준의 기본 제공 복제 메커니즘을 제공합니다.  
  
Hyper-V 복제본은 주 Hyper-V 호스트에서 선택한 VM을 LAN 또는 WAN 링크를 통해 복제본 Hyper-V 호스트로 비동기식으로 복제합니다. 초기 복제가 완료된 후에는 이후 변경 내용이 관리자가 정의한 간격으로 복제됩니다.  
  
장애 조치(failover)는 계획되거나 계획되지 않을 수 있습니다. 계획된 장애 조치(failover)는 주 VM에서 관리자에 의해 시작되며, 데이터 손실을 방지하기 위해 복제되지 않은 모든 변경 내용이 복제된 VM으로 복사됩니다. 계획되지 않은 장애 조치(failover)는 주 VM의 예기치 않은 오류로 대한 응답으로 복제본 VM에서 시작됩니다. 아직 복제되지 않았을 수 있는 주 VM의 변경 내용을 전송할 기회가 없으므로 데이터가 손실될 수 있습니다.  
  
Hyper-V 복제본에 대한 자세한 내용은 [Hyper-V 복제본 개요](https://technet.microsoft.com/library/jj134172.aspx) 및 [Hyper-V 복제본 배포](https://technet.microsoft.com/library/jj134207.aspx)를 참조하세요.  
  
> [!NOTE]  
> Hyper-V 복제본은 Windows Server Hyper-V에서만 실행할 수 있으며, Windows 8을 실행하는 Hyper-V 버전에서는 실행할 수 없습니다.  
  
## <a name="windows-server-2012-or-newer-domain-controllers-required"></a>Windows Server 2012 또는 필요한 새 도메인 컨트롤러

Windows Server 2012 Hyper-v는 Vm-generationid (VMGenID)를 도입 합니다. VMGenID는 중요한 변경 내용이 발생한 경우 하이퍼바이저에서 게스트 운영 체제와 통신할 수 있는 방법을 제공합니다. 예를 들어 하이퍼바이저는 스냅샷 복원(백업 복원이 아닌 Hyper-V 스냅샷 복원 기술)이 발생한 가상화된 DC와 통신할 수 있습니다. Windows Server 2012 이상 버전의 AD DS는 VMGenID VM 기술을 인식 및 자체를 보호할 수 있도록 하는 스냅숏 복원 같은 하이퍼바이저 작업이 수행 된 시기를 감지 하는 데 사용 합니다.  
  
> [!NOTE]
> AD DS Windows Server 2012 Dc에서 이상만 VMGenID;에서 이러한 안전 조치를 제공 합니다. 모든 이전 버전의 Windows Server를 실행 하는 Dc는 가상화 된 DC가 스냅숏 복원 같은 지원 되지 않는 메커니즘을 사용 하 여 복원 되는 경우 발생할 수 있는 USN 롤백이 같은 문제가 적용 됩니다. 이러한 안전 조치와 각 안전 조치가 트리거되는 경우에 대한 자세한 내용은 [가상화된 도메인 컨트롤러 아키텍처](https://technet.microsoft.com/library/jj574118.aspx)를 참조하세요.  
  
Hyper-v 복제 장애 조치 (계획 된 또는 계획 되지 않은) 경우 가상화 된 DC 검색 VMGenID 재설정을 트리거하는 앞서 언급 한 보안 기능 합니다. 그런 다음 Active Directory 작업이 정상적으로 계속 진행됩니다. 주 VM 대신 복제본 VM이 실행됩니다.  
  
> [!NOTE]  
> 이제 DC ID가 동일한 인스턴스가 두 개 있으므로 주 인스턴스와 복제된 인스턴스가 둘 다 실행될 수 있습니다. Hyper-V 복제본에는 주 VM과 복제본 VM이 동시에 실행되지 않도록 하는 제어 메커니즘이 있지만 VM 복제 후 두 VM 간의 링크에서 오류가 발생한 경우 두 VM이 동시에 실행될 수 있습니다. 이와 같이 드문 상황이 발생한 경우 Windows Server 2012를 실행하는 가상화된 DC에는 AD DS를 보호할 수 있는 보호 기능이 있지만 이전 버전의 Windows Server를 실행하는 가상화된 DC에는 보호 기능이 없습니다.  
  
Hyper-V 복제본을 사용할 때는 [Hyper-V에서의 가상 도메인 컨트롤러 실행](https://technet.microsoft.com/library/virtual_active_directory_domain_controller_virtualization_hyperv(v=WS.10).aspx)에 대한 모범 사례를 따라야 합니다. 이 문서에는 Active Directory 파일을 가상 SCSI 디스크에 저장하여 데이터 내구성을 강화하는 방법에 대한 권장 사항 등이 나와 있습니다.  
  
## <a name="supported-and-unsupported-scenarios"></a>지원되는 시나리오와 지원되지 않는 시나리오

Windows Server 2012를 실행된 하거나 최신 지원 계획 되지 않은 장애 조치 및 장애 조치 테스트를 위해 Vm만 합니다. 계획 된 장애 조치에 대해서도 관리자가 실수로 시작 주 VM과 복제 된 VM은 동시에 위험을 완화 하기 위해 Windows Server 2012 이상는 가상화 된 DC에 권장 됩니다.  
  
이전 버전의 Windows Server를 실행하는 VM에서는 계획된 장애 조치(failover)는 지원되지만 USN 롤백이 발생할 가능성이 있으므로 계획되지 않은 장애 조치(failover)는 지원되지 않습니다. USN 롤백에 대한 자세한 내용은 [USN 및 USN 롤백](https://technet.microsoft.com/library/d2cae85b-41ac-497f-8cd1-5fbaa6740ffe(v=ws.10))을 참조하세요.  
  
> [!NOTE]  
> 도메인 또는 포리스트에 대한 기능 수준 요구 사항은 없습니다. Hyper-V 복제본을 사용하여 복제된 VM으로 실행되는 DC에 대한 운영 체제 요구 사항만 있습니다. 이전 버전의 Windows Server를 실행하는 다른 실제 또는 가상 DC가 있는 포리스트에 VM을 배포할 수 있으며, 이는 Hyper-V 복제본을 사용하여 복제할 수도 있고 복제하지 못할 수도 있습니다.  
  
다중 도메인 포리스트 구성도 지원되지만 이 지원 설명은 단일 도메인 포리스트에서 수행된 테스트를 기반으로 합니다. 이러한 테스트에서 가상화된 도메인 컨트롤러 DC1 및 DC2는 Windows Server 2012에서 Hyper-V를 실행하는 서버에서 호스트되는 동일한 사이트에 있는 Active Directory 복제 파트너입니다. DC2를 실행하는 VM 게스트에는 Hyper-V 복제본이 활성화되어 있으며, 복제본 서버는 지리적으로 떨어져 있는 다른 데이터 센터에서 호스트됩니다. 아래에 나와 있는 테스트 사례 프로세스를 보다 쉽게 설명하기 위해 복제본 서버에서 실행되는 VM을 DC2-Rec(실제로는 원본 VM과 이름이 같음)라고 합니다.  
  
### <a name="windows-server-2012"></a>Windows Server 2012

다음 표에서는 Windows Server 2012를 실행하는 가상화된 DC에 대한 지원 및 테스트 사례를 설명합니다.  
  
|||  
|-|-|  
|계획된 장애 조치(failover)|계획되지 않은 장애 조치(failover)|  
|지원됨|지원됨|  
|테스트 사례:<br /><br />-DC1과 DC2 Windows Server 2012를 실행 합니다.<br /><br />-DC2가 종료 하 고 DC2-Rec에서 장애 조치를 수행 합니다. 장애 조치(failover)는 계획되거나 계획되지 않을 수 있습니다.<br /><br />-해당 데이터베이스에 있는 VMGenID 값 값과 같은지 여부를 확인 DC2-Rec는 시작 후 Hyper-v 복제본 서버에서 저장 된 가상 머신 드라이버에서.<br /><br />-결과적으로, DC2-Rec 트리거 가상화 세이프 가드; 즉, 해당 InvocationID를 다시 설정, 해당 RID 풀을 삭제 하 고 작업 마스터 역할을 맡 전에 초기 동기화 요구 사항을 설정 합니다. 초기 동기화 요구 사항에 대한 자세한 내용은 다음을 참조하세요.<br /><br />-그런 다음 DC2-Rec는 새 VMGenID 값을 해당 데이터베이스에 저장 하 고 새 InvocationID의 컨텍스트에서 모든 후속 업데이트를 커밋합니다.<br /><br />-의 결과로 InvocationID가 다시 설정, DC1는 수렴에 롤백된 시간 내에 있는 경우에 DC2-Rec에서 도입 된 모든 AD 변경 사항에 장애 조치는 안전 하 게 수렴 후 DC2-Rec에서 수행 되는 모든 AD 업데이트가 의미 합니다.|테스트 사례는 다음을 제외하고 계획된 장애 조치(failover)의 테스트 사례와 같습니다.<br /><br />-AD DC2에 수신된를 업데이트 하지만 아직 복제 하지 않은 AD 복제 파트너에 게 장애 조치 이벤트는 손실 됩니다.<br /><br />AD 업데이트는 DC1에 ad 복제 된 복구 지점의 시간 DC1에서 DC2-Rec로 다시 복제 됩니다 후 DC2에 수신 합니다.|  
  
### <a name="windows-server-2008-r2-and-earlier-versions"></a>Windows Server 2008 R2 이하 버전

다음 표에서는 Windows Server 2008 R2 이하 버전을 실행하는 가상화된 DC에 대한 지원 및 테스트 사례를 설명합니다.  
  
|||  
|-|-|  
|계획된 장애 조치(failover)|계획되지 않은 장애 조치(failover)|  
|지원되지만, 이러한 버전의 Windows Server를 실행하는 DC는 VMGenID를 지원하거나 연관된 가상화 세이프가드을 사용하지 않으므로 권장되지 않습니다. USN 롤백에 대한 위험이 따릅니다. 자세한 내용은 [USN 및 USN 롤백](https://technet.microsoft.com/library/d2cae85b-41ac-497f-8cd1-5fbaa6740ffe(v=ws.10))을 참조하세요.|지원 되지 않습니다 **참고 합니다.** 계획되지 않은 장애 조치(failover)는 포리스트의 단일 DC(권장되지 않는 구성)와 같이 USN 롤백이 위험하지 않은 경우에 지원됩니다.|  
|테스트 사례:<br /><br />-DC1과 DC2 Windows Server 2008 R2를 실행 합니다.<br /><br />-DC2가 종료 하 고 DC2-Rec에서 계획된 된 장애 조치를 수행 합니다. DC2의 모든 데이터는 종료가 완료되기 전에 DC2-Rec에 복제됩니다.<br /><br />-DC2-Rec는 시작 후 DC2와 동일한 invocationID를 사용 하 여 DC1 복제 다시 시작 합니다.|해당 사항 없음|  
