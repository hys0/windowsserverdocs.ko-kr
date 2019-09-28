---
ms.assetid: 45a65504-70b5-46ea-b2e0-db45263fabaa
title: 가상화된 도메인 컨트롤러에 Hyper-V 복제본 사용 지원
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 92324ef7c0fab81e80974a1f05eeec4833f09875
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71390433"
---
# <a name="support-for-using-hyper-v-replica-for-virtualized-domain-controllers"></a>가상화된 도메인 컨트롤러에 Hyper-V 복제본 사용 지원

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 DC(도메인 컨트롤러)로 실행되는 VM(가상 컴퓨터)을 복제하는 데 Hyper-V 복제본을 사용할 수 있는지에 대해 설명합니다. Hyper-V 복제본은 Windows Server 2012부터 제공되는 Hyper-V의 새로운 기능으로, VM 수준의 기본 제공 복제 메커니즘을 제공합니다.  
  
Hyper-V 복제본은 주 Hyper-V 호스트에서 선택한 VM을 LAN 또는 WAN 링크를 통해 복제본 Hyper-V 호스트로 비동기식으로 복제합니다. 초기 복제가 완료된 후에는 이후 변경 내용이 관리자가 정의한 간격으로 복제됩니다.  
  
장애 조치(failover)는 계획되거나 계획되지 않을 수 있습니다. 계획된 장애 조치(failover)는 주 VM에서 관리자에 의해 시작되며, 데이터 손실을 방지하기 위해 복제되지 않은 모든 변경 내용이 복제된 VM으로 복사됩니다. 계획되지 않은 장애 조치(failover)는 주 VM의 예기치 않은 오류로 대한 응답으로 복제본 VM에서 시작됩니다. 아직 복제되지 않았을 수 있는 주 VM의 변경 내용을 전송할 기회가 없으므로 데이터가 손실될 수 있습니다.  
  
Hyper-V 복제본에 대한 자세한 내용은 [Hyper-V 복제본 개요](https://technet.microsoft.com/library/jj134172.aspx) 및 [Hyper-V 복제본 배포](https://technet.microsoft.com/library/jj134207.aspx)를 참조하세요.  
  
> [!NOTE]  
> Hyper-V 복제본은 Windows Server Hyper-V에서만 실행할 수 있으며, Windows 8을 실행하는 Hyper-V 버전에서는 실행할 수 없습니다.  
  
## <a name="windows-server-2012-or-newer-domain-controllers-required"></a>Windows Server 2012 이상의 도메인 컨트롤러가 필요 합니다.

Windows Server 2012 Hyper-v는 VM Vm-generationid (VMGenID)를 도입 했습니다. VMGenID는 중요한 변경 내용이 발생한 경우 하이퍼바이저에서 게스트 운영 체제와 통신할 수 있는 방법을 제공합니다. 예를 들어 하이퍼바이저는 스냅샷 복원(백업 복원이 아닌 Hyper-V 스냅샷 복원 기술)이 발생한 가상화된 DC와 통신할 수 있습니다. Windows Server 2012 이상 버전의 AD DS는 VMGenID VM 기술을 인식 하 고이를 사용 하 여 스냅숏 복원과 같은 하이퍼바이저 작업이 수행 되는 시기를 감지 하 여 자신을 보다 효율적으로 보호할 수 있도록 합니다.  
  
> [!NOTE]
> Windows Server 2012 Dc 이상의 AD DS만 VMGenID에서 발생 하는 이러한 안전 조치를 제공 합니다. 모든 이전 버전의 Windows Server를 실행 하는 Dc는 스냅숏 복원과 같은 지원 되지 않는 메커니즘을 사용 하 여 가상화 된 DC를 복원할 때 발생할 수 있는 USN 롤백 등의 문제가 발생 합니다. 이러한 안전 조치와 각 안전 조치가 트리거되는 경우에 대한 자세한 내용은 [가상화된 도메인 컨트롤러 아키텍처](https://technet.microsoft.com/library/jj574118.aspx)를 참조하세요.  
  
Hyper-v 복제본 장애 조치 (failover)가 발생 하는 경우 (계획 또는 계획 되지 않음) 가상화 된 DC는 VMGenID reset을 검색 하 여 앞서 언급 한 안전 기능을 트리거합니다. 그런 다음 Active Directory 작업이 정상적으로 계속 진행됩니다. 주 VM 대신 복제본 VM이 실행됩니다.  
  
> [!NOTE]  
> 이제 DC ID가 동일한 인스턴스가 두 개 있으므로 주 인스턴스와 복제된 인스턴스가 둘 다 실행될 수 있습니다. Hyper-V 복제본에는 주 VM과 복제본 VM이 동시에 실행되지 않도록 하는 제어 메커니즘이 있지만 VM 복제 후 두 VM 간의 링크에서 오류가 발생한 경우 두 VM이 동시에 실행될 수 있습니다. 이와 같이 드문 상황이 발생한 경우 Windows Server 2012를 실행하는 가상화된 DC에는 AD DS를 보호할 수 있는 보호 기능이 있지만 이전 버전의 Windows Server를 실행하는 가상화된 DC에는 보호 기능이 없습니다.  
  
Hyper-V 복제본을 사용할 때는 [Hyper-V에서의 가상 도메인 컨트롤러 실행](https://technet.microsoft.com/library/virtual_active_directory_domain_controller_virtualization_hyperv(v=WS.10).aspx)에 대한 모범 사례를 따라야 합니다. 이 문서에는 Active Directory 파일을 가상 SCSI 디스크에 저장하여 데이터 내구성을 강화하는 방법에 대한 권장 사항 등이 나와 있습니다.  
  
## <a name="supported-and-unsupported-scenarios"></a>지원되는 시나리오와 지원되지 않는 시나리오

Windows Server 2012 이상을 실행 하는 Vm만 계획 되지 않은 장애 조치 (failover) 및 테스트 장애 조치 (failover)를 지원 합니다. 계획 된 장애 조치 (failover)의 경우에도 관리자가 주 VM과 복제 된 VM을 실수로 모두 동시에 시작 하는 경우 위험을 완화 하기 위해 가상화 된 DC에 Windows Server 2012 이상이 권장 됩니다.  
  
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
|테스트 사례:<br /><br />-DC1 및 d c 2는 Windows Server 2012를 실행 합니다.<br /><br />-D c 2는 종료 되 고 DC2에서 장애 조치 (failover)가 수행 됩니다. 장애 조치(failover)는 계획되거나 계획되지 않을 수 있습니다.<br /><br />-DC2-Rec가 시작 된 후에는 해당 데이터베이스에 있는 VMGenID의 값이 Hyper-v 복제본 서버에서 저장 한 가상 컴퓨터 드라이버의 값과 동일한 지 여부를 확인 합니다.<br /><br />따라서 DC2-Rec는 가상화 보호를 트리거합니다. 즉, InvocationID를 다시 설정 하 고, RID 풀을 삭제 하 고, 초기 동기화 요구 사항을 설정 하 여 작업 마스터 역할을 가정 합니다. 초기 동기화 요구 사항에 대한 자세한 내용은 다음을 참조하세요.<br /><br />-DC2-Rec는 해당 데이터베이스에 VMGenID의 새 값을 저장 하 고 새 InvocationID의 컨텍스트에서 후속 업데이트를 커밋합니다.<br /><br />-InvocationID reset의 결과로 DC1은 시간이 롤백된 경우에도 DC2-Rec에 의해 도입 된 모든 AD 변경 내용에 대해 수렴 합니다. 즉, 장애 조치 (failover) 후 DC2에서 수행 되는 모든 AD 업데이트가 안전 하 게 수렴 됩니다.|테스트 사례는 다음을 제외하고 계획된 장애 조치(failover)의 테스트 사례와 같습니다.<br /><br />-DC2에서 받았지만 장애 조치 (failover) 이벤트 전에 AD에서 복제 파트너로 아직 복제 하지 않은 AD 업데이트는 모두 손실 됩니다.<br /><br />-AD에서 DC1으로 복제 된 복구 지점의 시간이 d c 2에서 DC1으로 받은 AD 업데이트는 d c 1에서 d c 1로 다시 복제 됩니다.|  
  
### <a name="windows-server-2008-r2-and-earlier-versions"></a>Windows Server 2008 R2 이하 버전

다음 표에서는 Windows Server 2008 R2 이하 버전을 실행하는 가상화된 DC에 대한 지원 및 테스트 사례를 설명합니다.  
  
|||  
|-|-|  
|계획된 장애 조치(failover)|계획되지 않은 장애 조치(failover)|  
|지원되지만, 이러한 버전의 Windows Server를 실행하는 DC는 VMGenID를 지원하거나 연관된 가상화 세이프가드을 사용하지 않으므로 권장되지 않습니다. USN 롤백에 대한 위험이 따릅니다. 자세한 내용은 [USN 및 USN 롤백](https://technet.microsoft.com/library/d2cae85b-41ac-497f-8cd1-5fbaa6740ffe(v=ws.10))을 참조하세요.|지원 되지 않음 **참고 사항:** 계획되지 않은 장애 조치(failover)는 포리스트의 단일 DC(권장되지 않는 구성)와 같이 USN 롤백이 위험하지 않은 경우에 지원됩니다.|  
|테스트 사례:<br /><br />-DC1 및 d c 2는 Windows Server 2008 r 2를 실행 합니다.<br /><br />-DC2가 종료 되 고 계획 된 장애 조치 (failover)가 DC2에서 수행 됩니다. DC2의 모든 데이터는 종료가 완료되기 전에 DC2-Rec에 복제됩니다.<br /><br />-DC2-Rec가 시작 된 후 DC2와 동일한 invocationID를 사용 하 여 d c 1을 사용 하 여 복제를 다시 시작 합니다.|해당 사항 없음|  
