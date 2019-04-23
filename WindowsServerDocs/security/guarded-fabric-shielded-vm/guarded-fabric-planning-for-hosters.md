---
title: 보호 된 패브릭 및 차폐 VM 호스팅 서비스 공급자에 대 한 계획
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 854defc8-99f8-4573-82c0-f484e0785859
manager: dongill
author: nirb-ms
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: f280fbe682ebf706ce6ea5b53ea8af5e6f39d75d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59857814"
---
# <a name="guarded-fabric-and-shielded-vm-planning-guide-for-hosters"></a>보호 된 패브릭 및 차폐 VM 호스팅 서비스 공급자에 대 한 계획

>적용 대상: Windows Server, Windows Server 2016, Windows Server (반기 채널) 2019

이 항목에서는 패브릭에서 실행 하려면 가상 컴퓨터 보호 사용 되도록 해야 하는 계획 결정 합니다. 기존 Hyper-v 패브릭 업그레이드 하거나 새 패브릭 만들기, 실행 보호 된 Vm은 두 가지 주요 구성 요소

- 있습니다 수 있도록 보호 된 Vm를 승인 하 고 정상 상태에서 Hyper-v 호스트 에서만 실행 됩니다 (HGS (호스트 보호 서비스)는 증명과 키 보호를 제공 합니다. 
- 보호 된 Vm (및 일반 Vm) 실행할 수 있는 Hyper-v 호스트를 승인 하 고 정상-이 보호 된 호스트 라고 합니다.

![HGS와 보호 된 호스트](../media/Guarded-Fabric-Shielded-VM/guarded-host-hgs-plus-host-diagram-basic.png)

## <a name="decision-1-trust-level-in-the-fabric"></a>의사 결정 #1: 신뢰 수준 패브릭에서

호스트 보호자 서비스와 보호 된 Hyper-v 호스트를 구현 하는 방법을 주로 패브릭에 달성 하려는 트러스트의 따라 달라 집니다. 트러스트의 강도 증명 모드에 의해 제어 됩니다. 두 가지 상호 배타적인 옵션:

1. TPM 신뢰할 수 있는 증명

    악의적인 관리자 또는 손상된 된 패브릭에서 가상 컴퓨터를 보호 하는 것이 목표인 경우 TPM에서 신뢰할 수 있는 증명을 사용 합니다. 이 옵션은 다중 테 넌 트 호스팅 시나리오에도 도메인 컨트롤러 또는 SQL 또는 SharePoint와 같은 콘텐츠 서버와 같은 엔터프라이즈 환경에서는 높은 가치의 자산와 적합합니다.
    보호 된 Vm 호스트 실행을 허용 하기 전에 HGS에 의해 적용 유효성이 및 하이퍼바이저로 보호 된 코드 무결성 (HVCI) 정책은 측정 합니다. 

2. 호스트 키 증명

    요구 사항 주로 구동 하는 준수 해야 하는 가상 컴퓨터 암호화 미사용 및 진행 중인를 모두 호스트 키 증명을 사용 합니다. 이 옵션 있는 익숙한 Hyper-v 호스트 및 패브릭 관리자가 일상적인 유지 관리 및 작업에 대 한 가상 머신의 게스트 운영 체제에 대 한 액세스를 사용 하 여 범용 데이터 센터에 대 한 잘 작동 합니다. 

    이 모드에서는 패브릭 관리자는 Hyper-v 호스트의 상태를 확인 하는 것에 대 한 책임입니다. 
    HGS 재생 일부가 되었거나 실행 되지 무엇을 결정 하므로 맬웨어 및 디버거 설계 된 대로 작동 됩니다. 
    
    그러나 VM의 작업자 프로세스 (VMWP.exe) 보호 된 프로세스 광원 PPL ()는 디버거 (WinDbg.exe)와 같은 프로세스에 직접 연결 하려고 하는 보호 된 Vm에 대 한 차단 됩니다. 
    LiveKd.exe를 사용한 것과 같은 대체 디버깅 기법을 차단 되지 않습니다. 
    보호 된 Vm과 달리 암호화 지원 Vm에 대 한 작업자 프로세스는 기존 디버거 같은 WinDbg.exe 있도록 PPL는 계속 정상적으로 작동 하는 대로 실행 되지 않습니다.

    비슷한 증명 모드 관리자 신뢰할 수 있는 증명 이라는 Windows Server 2019부터 사용 되지 않습니다 (Active Directory 기반). 

선택한 신뢰 수준에서 Hyper-v 호스트 뿐만 아니라 패브릭에서 적용 되는 정책에 대 한 하드웨어 요구 사항에 따라 결정 됩니다. 필요한 경우 기존 하드웨어 및 관리-신뢰할 수 있는 증명을 사용 하 여 보호 된 패브릭에 배포한 다음 하드웨어 업그레이드 된 경우 fabric 보안을 강화 하려면 TPM 신뢰할 수 있는 증명으로 변환 합니다.

## <a name="decision-2-existing-hyper-v-fabric-versus-a-new-separate-hyper-v-fabric"></a># 2를 결정 합니다. 기존 Hyper-v 패브릭을 새 별도 Hyper-v 패브릭 비교

기존 fabric을 사용 하는 경우 (Hyper-v 또는 기타), 가능성이 매우 높습니다는 일반 Vm과 함께 보호 된 Vm 실행에 사용할 수 있습니다. 일부 고객은 다른 비즈니스 상의 이유로 패브릭을 구분 하는 동안 자신의 기존 도구 및 패브릭에 보호 된 Vm을 통합 하는 선택 합니다.

## <a name="hgs-admin-planning-for-the-host-guardian-service"></a>HGS 관리자 호스트 보호 서비스에 대 한 계획

물리적 전용된 서버에서 보호 된 VM, VM (보호 된 패브릭에서 구분 됨)는 격리 된 Hyper-v 호스트 또는 다른 Azure를 사용 하 여 논리적으로 구분 된 하나에서이 든 관계의 보호 서비스 (HGS (호스트) 보안 수준이 높은 환경에서 배포 구독입니다.   

| 영역 | 설명 |
|------|---------|
| 설치 요구 사항 | <ul><li>하나의 서버 (고가용성을 위해 권장 되는 3 노드 클러스터)</li><li>대체 (fallback)에 대 한 두 개 이상의 HGS 필요한 서버 수</li><li>가상 또는 물리적 서버 수 권장; TPM 2.0을 사용 하 여 (물리적 서버 TPM 1.2도 지원)</li><li>Windows Server 2016 이상의 server Core 설치</li><li>한 네트워크 시야가 HTTP 허용 패브릭에 또는 [대체 (fallback) 구성](guarded-fabric-manage-branch-office.md#fallback-configuration)</li><li>HTTPS 인증서에 대 한 액세스 유효성 검사에 대 한 권장</li></ul> |
| 크기 조정 | 각 중간 크기 (8 코어/4 GB) HGS 서버 노드에서 1,000 Hyper-v 호스트를 처리할 수 있습니다. |
| 관리 | HGS를 관리 하는 특정 사용자를 지정 합니다. 패브릭 관리자가 별개 여야 합니다. 비교를 위해 HGS 클러스터 동일한 방식으로 인증 기관 (CA) 관리 격리, 실제 배포 및 보안 민감도가의 전반적인 수준 측면에서 생각할 수 있습니다. |
| Host Guardian Service Active Directory | 기본적으로 HGS 관리에 대 한 내부 Active Directory 자체를 설치합니다. 이 자체 관리 되는 자체 포함 포리스트 및 패브릭에에서 HGS를 분리 하도록 하기 위해 권장 되는 구성입니다.<br><br>격리에 사용 하는 높은 권한 있는 Active Directory 포리스트를 이미 있는 경우 해당 포리스트의 HGS 기본 포리스트 대신 사용할 수 있습니다. HGS에서 Hyper-v 호스트 또는 패브릭 관리 도구와 동일한 포리스트에 도메인에 가입 되어 있지는 반드시 합니다. 이렇게 HGS를 제어할 수 패브릭 관리자를 허용할 수 있습니다. |
| 재해 복구 | 다음의 세 가지 옵션 중에서 선택할 수 있습니다.<br><ol><li>각 데이터 센터에서 별도 HGS 클러스터를 설치 하 고 보호 된 Vm의 기본 및 백업 데이터 센터에서 실행 되도록 권한을 부여 합니다. 이 WAN을 통해 클러스터를 확장 하지 않아도 되 고 지정된 된 사이트에만 실행 되도록 가상 컴퓨터를 격리할 수 있습니다.</li><li>두 개 이상의 데이터 센터 간에 확장 클러스터에서 HGS를 설치 합니다. WAN 다운 푸시 제한 장애 조치 클러스터링의 경우 복원 력을 제공 합니다. 한 사이트;에 대 한 워크 로드를 격리할 수 없습니다. 다른 하나의 사이트에 실행 권한이 부여 된 VM을 실행할 수 있습니다.</li><li>다른 HGS를 사용 하 여 장애 조치를 Hyper-v 호스트를 등록 합니다.</li></ol>또한 로컬로 항상 복구할 수 있도록 해당 구성을 내보내 모든 HGS를 백업 해야 합니다. 자세한 내용은 [내보내기 HgsServerState](https://technet.microsoft.com/library/mt652164.aspx) 하 고 [가져오기 HgsServerState](https://technet.microsoft.com/library/mt652168.aspx)합니다. |
| 호스트 보호자 서비스 키 | 두 비대칭 키 쌍을 사용 하는 호스트 보호자 서비스-암호화 키 및 서명 키-SSL 인증서에 의해 각각 표시 합니다. 이러한 키를 생성 하는 방법은 두 가지가 있습니다.<br><ol><li>내부 인증 기관 – 내부 PKI 인프라를 사용 하 여 이러한 키를 생성할 수 있습니다. 데이터 센터 환경에 적합합니다.</li><li>공개적으로 신뢰할 수 있는 인증서 기관 – 공개적으로 신뢰할 수 있는 인증 기관에서 얻은 키 집합을 사용 합니다. 호스팅 서비스 공급자를 사용 해야 하는 옵션입니다.</li></ol>자체 서명 된 인증서를 사용할 수 있지만, 좋지 않습니다 개념 증명 labs 이외의 배포 시나리오에 대 한 note 합니다.<br><br>HGS 키를 가져야 하는 것 외에도 호스팅 서비스 공급자는 "bring your own key" 테 넌 트 일부 또는 모든 테 넌 트 특정 HGS 키 자체를 유지할 수 있도록 자신의 키를 제공할 수를 사용할 수 있습니다. 이 옵션은 해당 키를 업로드 하려면 테 넌 트에 대 한 대역의 프로세스를 제공할 수 있는 호스팅 서비스 공급자에 적합 합니다. |
| 호스트 보호 서비스에 대 한 키 저장소 | 가능한 가장 강력한 보안을 위해 HGS 키 생성 되 고 단독으로에서 보안 모듈 (HSM (하드웨어)를 저장 하는 것이 좋습니다. Hsm을 사용 하지 않는 경우 HGS 서버에 BitLocker 적용 것이 좋습니다. |

## <a name="fabric-admin-planning-for-guarded-hosts"></a>보호 된 호스트 패브릭 관리자에 대 한 계획

| 영역 | 설명 |
|------|---------|
| 하드웨어 | <ul><li>호스트 키 증명: 보호 된 호스트로 기존 하드웨어를 사용할 수 있습니다. 몇 가지 예외 사항이 있습니다 (호스트를 Windows Server 2016 부터는 새로운 보안 메커니즘을 사용할 수 있는지를 참조 하세요 [코드 무결성에 대 한 Windows Server 2016 가상화 기반 보호를 사용 하 여 호환 되는 하드웨어](guarded-fabric-compatible-hardware-with-virtualization-based-protection-of-code-integrity.md)합니다.</li><li>TPM 신뢰할 수 있는 증명: 모든 하드웨어를 사용할 수는 [하드웨어 보증 추가 자격](https://msdn.microsoft.com/windows/hardware/commercialize/design/compatibility/systems#system-server-assurance) 적절 하 게 구성 되어 있다면 (참조 [보호 된 Vm과 호환 되는 서버 구성 및 가상화 기반 코드 무결성 보호](guarded-fabric-compatible-hardware-with-virtualization-based-protection-of-code-integrity.md) 특정 구성에 대 한). 여기에 TPM 2.0 및 UEFI 2.3.1c 버전 이상.</li></ul> |
| OS | Hyper-v 호스트 OS 용 Server Core 옵션을 사용 하는 것이 좋습니다. |
| 성능에 미치는 영향 | 성능 테스트에 따라 것 이라고 예상을 5% 밀도-실행 간의 차이 vm 차폐가 아닌 vm을 보호 하는 약 합니다. 이 의미는 지정된 된 Hyper-v 호스트 20 차폐가 아닌 Vm을 실행 하는 경우 기대 19 보호 된 Vm를 실행할 수 있도록 합니다.<br><br>일반적인 워크 로드를 사용 하 여 크기 조정 확인 해야 합니다. 예를 들어, 많은 쓰기 지향 IO 워크 로드가 있는 밀도 차이 추가로 영향을 주는 몇 가지 이상 있을 수 있습니다. |
| 지점 고려 사항 | Windows Server 버전 1709 부터는 분기 office에서 보호 된 VM으로 로컬로 실행 하는 가상화 된 HGS 서버에 대 한 대체 (fallback) URL을 지정할 수 있습니다. 지점 데이터 센터에서 HGS 서버에 대 한 연결을 잃을 때 대체 (fallback) URL은 사용할 수 있습니다. Windows Server의 이전 버전에서는 분기 office 요구 연결이 전원 켜기 또는 실시간으로 마이그레이션할 호스트 보호자 서비스를 실행 하는 Hyper-v 호스트 보호 된 Vm입니다. 자세한 내용은 [office 고려 사항 분기](guarded-fabric-manage-branch-office.md)합니다. |
