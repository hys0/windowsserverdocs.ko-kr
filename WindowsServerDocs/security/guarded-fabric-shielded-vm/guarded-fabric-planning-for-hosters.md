---
title: 호스팅 서비스 공급자에 대 한 보호 된 패브릭 및 차폐 VM 계획 가이드
ms.prod: windows-server
ms.topic: article
ms.assetid: 854defc8-99f8-4573-82c0-f484e0785859
manager: dongill
author: nirb-ms
ms.author: nirb
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 2e64f8a43318f10db3bfcb604adcef4b0bdc9837
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856516"
---
# <a name="guarded-fabric-and-shielded-vm-planning-guide-for-hosters"></a>호스팅 서비스 공급자에 대 한 보호 된 패브릭 및 차폐 VM 계획 가이드

>적용 대상: Windows Server 2019, Windows Server (반기 채널), Windows Server 2016

이 항목에서는 보호 된 가상 컴퓨터를 패브릭에서 실행할 수 있도록 하기 위해 수행 해야 하는 계획 결정에 대해 설명 합니다. 기존 Hyper-v 패브릭을 업그레이드 하거나 새 패브릭을 만드는 경우 보호 된 Vm을 실행 하면 다음 두 가지 주요 구성 요소로 구성 됩니다.

- HGS (호스트 보호 서비스)는 보호 된 Vm이 승인 및 정상 Hyper-v 호스트 에서만 실행 되도록 하기 위해 증명 및 키 보호를 제공 합니다. 
- 보호 된 Vm (및 일반 Vm)을 실행할 수 있는 승인 및 정상 Hyper-v 호스트 (이러한 호스트를 보호 된 호스트 라고 함)

![HGS 및 보호 된 호스트](../media/Guarded-Fabric-Shielded-VM/guarded-host-hgs-plus-host-diagram-basic.png)

## <a name="decision-1-trust-level-in-the-fabric"></a>의사 결정 #1: 패브릭의 신뢰 수준

호스트 보호 서비스 및 보호 된 Hyper-v 호스트를 구현 하는 방법은 주로 패브릭에서 달성할 신뢰 수준에 따라 달라 집니다. 신뢰 수준은 증명 모드에 의해 제어 됩니다. 상호 배타적인 두 가지 옵션은 다음과 같습니다.

1. TPM에서 신뢰할 수 있는 증명

    악의적인 관리자 또는 손상 된 패브릭에서 가상 머신을 보호 하는 데 도움이 되는 경우 TPM으로 신뢰할 수 있는 증명을 사용 합니다. 이 옵션은 다중 테 넌 트 호스팅 시나리오 뿐만 아니라 도메인 컨트롤러 또는 SQL 또는 SharePoint와 같은 콘텐츠 서버와 같은 엔터프라이즈 환경에서 높은 가치의 자산에도 적합 합니다.
    하이퍼바이저에서 보호 된 Vm을 실행 하도록 허용 하기 전에 HGS에서 HVCI (보호 된 코드 무결성) 정책을 측정 하 고 해당 유효성을 적용 합니다. 

2. 호스트 키 증명

    요구 사항이 주로 가상 머신을 암호화 하는 데 필요한 규정 준수를 기반으로 하는 경우에는 호스트 키 증명을 사용 합니다. 이 옵션은 일상적인 유지 관리 및 운영에 대 한 가상 머신의 게스트 운영 체제에 액세스할 수 있는 Hyper-v 호스트 및 패브릭 관리자에 게 익숙한 범용 데이터 센터에 적합 합니다. 

    이 모드에서 패브릭 관리자는 단순히 Hyper-v 호스트의 상태를 확인 하는 일을 담당 합니다. 
    HGS는 실행할 수 있거나 실행할 수 없는 항목을 결정 하는 부분을 재생 하지 않으므로 맬웨어 및 디버거는 설계 된 대로 작동 합니다. 
    
    그러나 프로세스에 직접 연결을 시도 하는 디버거 (예: WinDbg)는 VM의 작업자 프로세스 (VMWP .exe)가 PPL (protected process light) 이므로 보호 된 Vm에 대해 차단 됩니다. 
    LiveKd에서 사용 하는 것과 같은 대체 디버깅 기술은 차단 되지 않습니다. 
    보호 된 Vm과 달리 암호화 지원 Vm에 대 한 작업자 프로세스는 PPL으로 실행 되지 않으므로 WinDbg와 같은 기존 디버거는 정상적으로 계속 작동 합니다.

    관리자가 신뢰할 수 있는 증명 (Active Directory 기반) 이라는 유사한 증명 모드는 Windows Server 2019부터 더 이상 사용 되지 않습니다. 

선택 하는 신뢰 수준에 따라 패브릭에서 적용 하는 정책 뿐만 아니라 Hyper-v 호스트의 하드웨어 요구 사항도 결정 됩니다. 필요한 경우 기존 하드웨어 및 관리자가 신뢰할 수 있는 증명을 사용 하 여 보호 된 패브릭을 배포한 다음, 하드웨어가 업그레이드 되 고 패브릭 보안을 강화 해야 하는 경우 TPM으로 신뢰할 수 있는 증명으로 변환할 수 있습니다.

## <a name="decision-2-existing-hyper-v-fabric-versus-a-new-separate-hyper-v-fabric"></a>의사 결정 #2: 기존 Hyper-v 패브릭과 새로운 별도 Hyper-v 패브릭 비교

기존 패브릭 (Hyper-v 또는 그렇지 않은 경우)이 있는 경우이를 사용 하 여 일반 Vm과 함께 보호 된 Vm을 실행할 수 있습니다. 일부 고객은 보호 된 Vm을 기존 도구와 패브릭에 통합 하도록 선택 하 고 다른 사용자는 비즈니스 목적을 위해 패브릭을 분리 합니다.

## <a name="hgs-admin-planning-for-the-host-guardian-service"></a>호스트 보호자 서비스에 대 한 HGS 관리자 계획

전용 물리적 서버, 보호 된 VM, isolated Hyper-v 호스트의 VM (보호 중인 패브릭에서 분리 됨) 또는 다른 Azure 구독을 사용 하 여 논리적으로 분리 된 환경에 있든 상관 없이 매우 안전한 환경에서 HGS (호스트 보호 서비스)를 배포 합니다.   

| 영역 | 세부 정보 |
|------|---------|
| 설치 요구 사항 | <ul><li>단일 서버 (고가용성을 위한 3 노드 클러스터 권장)</li><li>대체 (fallback)의 경우 둘 이상의 HGS 서버가 필요 합니다.</li><li>서버는 가상 또는 물리적 (TPM 2.0이 있는 실제 서버) 일 수 있습니다. TPM 1.2도 지원 됨)</li><li>Windows Server 2016 이상 버전의 server Core 설치</li><li>HTTP 또는 [대체 구성을](guarded-fabric-manage-branch-office.md#fallback-configuration) 허용 하는 패브릭의 네트워크 라인</li><li>액세스 유효성 검사에 권장 되는 HTTPS 인증서</li></ul> |
| 크기 조정 | 각 중간 크기 (8 개 코어/4gb) HGS 서버 노드가 1000 Hyper-v 호스트를 처리할 수 있습니다. |
| 관리 | HGS를 관리할 특정 사용자를 지정 합니다. 패브릭 관리자와 분리 해야 합니다. 비교를 위해, HGS 클러스터는 CA (인증 기관)와 동일한 방식으로 관리 격리, 물리적 배포 및 전반적인 보안 민감도의 측면에서 생각할 수 있습니다. |
| 호스트 보호자 서비스 Active Directory | 기본적으로 HGS는 관리를 위해 자체 내부 Active Directory를 설치 합니다. 자체 포함 된 자체 관리 포리스트 이며, 패브릭에서 HGS를 격리 하는 데 도움이 되는 권장 구성입니다.<br><br>격리에 사용 하는 권한이 높은 Active Directory 포리스트가 이미 있는 경우 HGS 기본 포리스트 대신 해당 포리스트를 사용할 수 있습니다. HGS가 Hyper-v 호스트 또는 패브릭 관리 도구와 동일한 포리스트에 있는 도메인에 가입 되어 있지 않아야 합니다. 이렇게 하면 패브릭 관리자가 HGS를 제어할 수 있습니다. |
| 재해 복구 | 다음과 같은 세 가지 옵션이 있습니다.<br><ol><li>각 데이터 센터에 별도의 HGS 클러스터를 설치 하 고 기본 및 백업 데이터 센터 모두에서 보호 된 Vm을 실행할 수 있는 권한을 부여 합니다. 이렇게 하면 WAN에서 클러스터를 스트레치 하지 않아도 되며, 지정 된 사이트 에서만 실행 되도록 가상 컴퓨터를 격리할 수 있습니다.</li><li>두 개 이상의 데이터 센터 간에 스트레치 클러스터에 HGS를 설치 합니다. WAN이 중단 되는 경우 복원 력을 제공 하지만 장애 조치 (failover) 클러스터링 제한을 푸시합니다. 작업을 한 사이트에 격리할 수 없습니다. 한 사이트에서 실행할 수 있는 권한이 있는 VM은 다른 사이트에서 실행할 수 있습니다.</li><li>다른 HGS로 Hyper-v 호스트를 장애 조치 (failover)로 등록 합니다.</li></ol>또한 언제 든 지 로컬로 복구할 수 있도록 구성을 내보내 모든 HGS를 백업 해야 합니다. 자세한 내용은 [HgsServerState](https://docs.microsoft.com/powershell/module/hgsserver/export-hgsserverstate) 및 [HgsServerState](https://docs.microsoft.com/powershell/module/hgsserver/import-hgsserverstate)를 참조 하세요. |
| 호스트 보호자 서비스 키 | 호스트 보호자 서비스는 SSL 인증서로 표시 되는 두 개의 비대칭 키 쌍 (암호화 키 및 서명 키)을 사용 합니다. 이러한 키를 생성 하는 두 가지 옵션은 다음과 같습니다.<br><ol><li>내부 인증 기관 – 내부 PKI 인프라를 사용 하 여 이러한 키를 생성할 수 있습니다. 이는 데이터 센터 환경에 적합 합니다.</li><li>공개적으로 신뢰할 수 있는 인증 기관 – 공개적으로 신뢰할 수 있는 인증 기관에서 가져온 키 집합을 사용 합니다. 이 옵션은 호스팅 서비스 공급자에서 사용 해야 하는 옵션입니다.</li></ol>자체 서명 된 인증서를 사용할 수 있지만 개념 증명 랩 이외의 배포 시나리오에는 권장 되지 않습니다.<br><br>서비스 공급자는 HGS 키를 포함 하는 것 외에도 "고유한 키 가져오기"를 사용할 수 있습니다. 여기서 테 넌 트는 자체 키를 제공 하 여 일부 또는 모든 테 넌 트가 고유한 특정 HGS 키를 가질 수 있습니다. 이 옵션은 테 넌 트가 키를 업로드 하는 대역 외 프로세스를 제공할 수 있는 호스팅 서비스 공급자에 적합 합니다. |
| 호스트 보호 서비스 키 저장소 | 가장 강력한 보안을 위해 HGS 키를 HSM (하드웨어 보안 모듈)에 독점적으로 만들고 저장 하는 것이 좋습니다. Hsm을 사용 하지 않는 경우 HGS 서버에 BitLocker를 적용 하는 것이 좋습니다. |

## <a name="fabric-admin-planning-for-guarded-hosts"></a>보호 된 호스트에 대 한 패브릭 관리자 계획

| 영역 | 세부 정보 |
|------|---------|
| 하드웨어 | <ul><li>호스트 키 증명: 보호 된 호스트로 기존 하드웨어를 사용할 수 있습니다. 몇 가지 예외가 있습니다. 호스트에서 Windows Server 2016부터 시작 하는 새로운 보안 메커니즘을 사용할 수 있도록 하려면 [코드 무결성을 Windows server 2016 가상화 기반 보호와 호환 되는 하드웨어](guarded-fabric-compatible-hardware-with-virtualization-based-protection-of-code-integrity.md)를 참조 하세요.</li><li>TPM에서 신뢰할 수 있는 증명: 적절 하 게 구성 된 경우 [하드웨어 보증 추가 자격이](https://msdn.microsoft.com/windows/hardware/commercialize/design/compatibility/systems#system-server-assurance) 있는 하드웨어를 사용할 수 있습니다 (특정 구성에 대 한 [코드 무결성의 가상화 기반 보호 및 보호 된 vm과 호환 되는 서버 구성](guarded-fabric-compatible-hardware-with-virtualization-based-protection-of-code-integrity.md) 참조). 여기에는 TPM 2.0 및 UEFI 버전 2.3.1 c 이상이 포함 됩니다.</li></ul> |
| OS | Hyper-v 호스트 OS에는 Server Core 옵션을 사용 하는 것이 좋습니다. |
| 성능에 미치는 영향 | 성능 테스트를 기반으로 보호 된 Vm과 차폐가 아닌 Vm을 실행 하는 것의 약 5% 밀도 차이를 예상 합니다. 즉, 지정 된 Hyper-v 호스트에서 20 개의 차폐가 아닌 Vm을 실행할 수 있는 경우 19 개의 차폐 Vm을 실행할 수 있습니다.<br><br>일반적인 워크 로드를 사용 하 여 크기를 확인 해야 합니다. 예를 들어 밀도 차이에 추가로 영향을 주는 집약적 쓰기 지향 IO 워크 로드의 일부 이상 값이 있을 수 있습니다. |
| 지점 고려 사항 | Windows Server 버전 1709부터 지점의 보호 된 VM으로 로컬로 실행 되는 가상화 된 HGS 서버에 대 한 대체 URL을 지정할 수 있습니다. 대체 URL은 지점에서 데이터 센터의 HGS 서버에 대 한 연결이 끊어질 때 사용할 수 있습니다. 이전 버전의 Windows Server에서 지점에서 실행 되는 Hyper-v 호스트는 전원을 켜고 보호 된 Vm을 실시간으로 마이그레이션하기 위해 호스트 보호자 서비스에 연결 해야 합니다. 자세한 내용은 [지점 고려 사항](guarded-fabric-manage-branch-office.md)을 참조 하세요. |
