---
ms.assetid: 45a65504-70b5-46ea-b2e0-db45263fabaa
title: "Hyper-v 복제본 가상화 도메인 컨트롤러에 대 한 사용에 대 한 지원"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 0444198196ed08a22aba92a0f59cc6e7a2518a2e
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="support-for-using-hyper-v-replica-for-virtualized-domain-controllers"></a>Hyper-v 복제본 가상화 도메인 컨트롤러에 대 한 사용에 대 한 지원

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목 Hyper-v 복제본은 VM (가상 컴퓨터)에 DC (도메인 컨트롤러)를 실행 하는 복제을 사용 하 여 가능성에 설명 합니다. Hyper-v 복제본 Hyper-v 시작 하는 기본 제공 복제 메커니즘 VM 수준에서 제공 하는 Windows Server 2012와의 새로운 기능입니다.  
  
Hyper-v 복제본 비동기적 복제 선택한 Vm 기본 Hyper-v 복제본 Hyper-v 호스트 호스트에서 LAN 또는 WAN 연결 합니다. 초기 복제 완료 되 면 간격으로 관리자가 정의 된 변경은 복제 됩니다.  
  
장애 조치 계획 되거나 예상치 못한 될 수 있습니다. 계획된 장애 조치 기본 VM에서 관리자 권한으로 시작 되 고 없다고 복제 변경 통해 복제 VM 데이터 손실을 방지 하기 위해에 복사 됩니다. 예상치 못한 장애 조치에 응답에 오류가 기본으로 만들기 VM의 복제본 VM 시작 됩니다. 데이터가 손실 될 수 없는 아직 복제 되지 기본 VM에서 변경 내용을 전송할 수는 없으므로 하기 때문입니다.  
  
Hyper-v 복제본에 대 한 자세한 내용은 참조 [Hyper-v 복제본 개요](https://technet.microsoft.com/library/jj134172.aspx) 및 [Hyper-v 복제본 배포](https://technet.microsoft.com/library/jj134207.aspx)합니다.  
  
> [!NOTE]  
> Hyper-v 복제본만에 Windows Server Hyper-v, Windows 8을 실행 하는 Hyper-v의 버전이 아닌 실행할 수 있습니다.  
  
## <a name="windows-server-2012-domain-controllers-required"></a>Windows Server 2012 도메인 컨트롤러 필요  
또한 Windows Server 2012 Hyper-v VM-GenerationID (VMGenID)를 소개합니다. VMGenID는 하이퍼바이저 중요 한 변경이 발생 했을 때 게스트 OS와 통신할 수 있는 방법을 제공 합니다. 예를 들어, 하이퍼바이저 스냅숏에서 복원 (Hyper-v 스냅숏을 복원 기술, 하지 백업/복원)가 발생 했음을 가상화 dc 통신할 수 있습니다. Windows Server 2012에서 AD DS VMGenID VM 기술을 알고 하며 스냅숏 복원 자체 더 잘 보호할 수 있는 등 하이퍼바이저 작업을 수행할 때이 감지 하 사용 합니다.  
  
> [!NOTE]  
> Windows Server 2012 dc AD DS을 지점, 확실 하 게 발생 VMGenID;에서 이러한 보호 조치를 제공 일부 이전 버전의 Windows Server 실행 Dc 같은 가상화 DC 복원할 스냅숏 복원 등 지원 되지 않는 메커니즘을 사용 하는 경우 발생할 수 있는 USN 롤백 문제 적용 됩니다. 이러한 되는지 궁금할 및 트리거됩니다 때에 대 한 자세한 내용은 참조 [도메인 컨트롤러 아키텍처 가상화](https://technet.microsoft.com/library/jj574118.aspx)합니다.  
  
Hyper-v 복제본 장애 조치 (계획 또는 계획 되지 않음) 하면, Windows Server 2012 가상화 DC 감지 VMGenID 재설정 앞에서 언급 한 보호 기능 트리거하 합니다. Active Directory 작업 정상적으로 진행합니다. 복제본 기본 VM 대신 VM 실행 됩니다.  
  
> [!NOTE]  
> 이제 이제 두 가지 경우 동일한 DC id 된다는 실행 주 인스턴스 및 복제 인스턴스 가능성이 있습니다. Hyper-v 복제본 제어 메커니즘 주 확보 하에서는 동안 복제본 Vm 동시에 실행 하지 않는 간을 링크는 VM의 복제 후 작동 하지 않는 경우에 동시에 실행 공유할 수는 있습니다. 이 드문 발생 하는 경우 Windows Server 2012를 실행 하는 가상화 Dc 있는 AD DS 보호, Dc 실행 이전 버전의 Windows Server는 가상화 반면 없는 위해 보호 합니다.  
  
Hyper-v 복제본을 사용 하는 경우에 대 한 유용한 정보를 수행 확인 [Hyper-v의 가상 도메인 컨트롤러 실행](https://technet.microsoft.com/library/virtual_active_directory_domain_controller_virtualization_hyperv(v=WS.10).aspx)합니다. 이 설명, 예를 들어, 가상 SCSI 디스크에 Active Directory 파일을 저장 하기 위한 권장 데이터 내구성의 강력한 보증을 제공 하는 합니다.  
  
## <a name="supported-and-unsupported-scenarios"></a>지원 되 고 지원 되지 않는 경우  
예상치 못한 장애 조치를 테스트 하 고 장애 Windows Server 2012를 실행 하는 Vm만 지원 됩니다. 계획된 장애 조치 경우에 Windows Server 2012 하려면 관리자 실수로 시작 기본 VM 및 복제 VM 동시에는 위험을 완화 가상화 DC에 권장 됩니다.  
  
이전 버전의 Windows Server를 실행 하는 Vm 계획된 장애 조치에 대 한 지원 있더라도 예기치 않은 장애 조치 USN 롤백 가능성이으로 인해 지원 되지 않습니다. USN 롤백에 대 한 자세한 내용은 참조 [USN 및 USN 롤백](https://technet.microsoft.com/library/d2cae85b-41ac-497f-8cd1-5fbaa6740ffe(v=ws.10))합니다.  
  
> [!NOTE]  
> 요구 사항이 없습니다 기능 수준 도메인 또는 숲입니다. Hyper-v 복제본을 사용 하 여 복제는 Vm 실행 dc만 운영 체제 요구 사항이 있습니다. 이전 버전의 Windows Server를 실행 하 고 않을 수도 수도 복제 되지 Hyper-v 복제본을 사용 하 여 다른 실제 또는 가상 Dc 포함 된 숲 속의 Vm 배포할 수 있습니다.  
  
이 지원 정책 기반 단일 도메인-숲에서 수행 된 테스트 있지만 다중 도메인 숲 구성도 지원 됩니다. 이러한 테스트 가상화 도메인 컨트롤러 d c 1 및 d c 2 Hyper-v Windows Server 2012에서 실행 하는 서버에 호스트 같은 사이트의 Active Directory 복제 파트너 있습니다. D c 2 실행 되는 VM 게스트에 Hyper-v 복제본 사용할 수 있습니다. 다른 떨어진 데이터 센터에 복제 서버 호스트 됩니다. 아래에 설명 된 테스트 사례 프로세스를 설명 해 위해 복제 서버에서 실행 되는 VM 라고 d c 2 기록 (있지만 실제로 원래 VM 이름이 같은 유지 됨).  
  
### <a name="windows-server-2012"></a>Windows Server 2012  
다음 표에서 Windows Server 2012와 테스트 사례 실행 하는 가상화 Dc에 대 한 지원이 설명 합니다.  
  
|||  
|-|-|  
|계획된 장애 조치|예상치 못한 장애|  
|지원|지원|  
|테스트 경우:<br /><br />-D c 1 및 d c 2 Windows Server 2012를 실행 하는 합니다.<br /><br />-D c 2 종료 되 고 d c 2 기록에서 장애 조치를 수행 합니다. 장애 조치 계획 되거나 예상치 못한 될 수 있습니다.<br /><br />-데이터베이스에 VMGenID 값 값과 같은 인지 확인 d c 2 기록 시작 된 후에서 가상 컴퓨터 드라이버 Hyper-v 복제본 서버에 저장 합니다.<br /><br />-결과적으로, d c 2 기록 트리거하 virtualization 보호 합니다. 즉, 것 해당 InvocationID 재설정, RID 풀의 버리고 작업 마스터 역할 가정는 전에 초기 동기화 요구를 설정 합니다. 초기 동기화 요구 사항에 대 한 자세한 내용은 참조 합니다.<br /><br />-그런 다음 d c 2 기록 VMGenID의 새 값 데이터베이스에 저장 하 고 커밋합니다 새 InvocationID 컨텍스트가의 모든 이후 업데이트 합니다.<br /><br />-의 결과로 InvocationID 재설정 d c 1는 수렴 시간 내에 다시 롤백 된 경우에 d c 2 기록으로 인 한 모든 광고 변경에 장애 조치는 수렴 안전 하 게 후 d c 2 기록에 수행 광고 업데이트가 의미|테스트 사례 경우를이 제외 계획된 장애 조치와 같습니다.<br /><br />-어떤 광고에 받은 d c 2 업데이트 하지만 전에 장애 조치 이벤트 손실 되는 광고에 의해 복제 파트너에 게 아직 복제 합니다.<br /><br />광고 업데이트 d c 2에서 받은 d c 2 기록에 다시 d c 1에서 복제 d c 1 하는 광고에 의해 복제 된 복구 지점 시간 됩니다.|  
  
### <a name="windows-server-2008-r2-and-earlier-versions"></a>Windows Server 2008 R2 및 이전 버전  
다음 표에서 Windows Server 2008 R2 및 이전 버전을 실행 하는 가상화 Dc에 대 한 지원이 설명 합니다.  
  
|||  
|-|-|  
|계획된 장애 조치|예상치 못한 장애|  
|Windows Server의 이러한 버전을 실행 하는 Dc VMGenID 지원 하지 않거나 관련된 virtualization 보호 기능을 사용 하기 때문에 있지만 권장 하지 않음 지원 합니다. 이 USN 롤백에 대 한 위험에 넣습니다. 자세한 내용은 참조 [USN 및 USN 롤백](https://technet.microsoft.com/en-us/library/d2cae85b-41ac-497f-8cd1-5fbaa6740ffe(v=ws.10))합니다.|지원 되지 않는 **참고:** 예상치 못한 장애 조치 USN 롤백 하지 않은 경우 숲 (권장 하지 않는 구성)에서 하나 DC 등 위험에 지원 될 것입니다.|  
|테스트 경우:<br /><br />-D c 1 및 d c 2 실행 하 고 Windows Server 2008 R2.<br /><br />-D c 2 종료 되 고 d c 2 기록에서 계획된 장애 조치를 수행 합니다. 완료 되 고 종료 되기 전에 d c 2에 있는 모든 데이터가 d c 2 기록 복제 됩니다.<br /><br />-기록 d c 2 시작 된 후 d c 1와 복제 동일한 invocationID d c 2로 사용 하 여 다시 시작 합니다.|해당 없음|  
  


