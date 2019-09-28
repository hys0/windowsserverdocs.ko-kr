---
title: 보호 된 패브릭 배포에 대 한 빠른 시작
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: e060e052-39a0-4154-90bb-b97cc6dde68e
manager: dongill
author: justinha
ms.author: justinha
ms.technology: security-guarded-fabric
ms.date: 01/30/2019
ms.openlocfilehash: 8359532113e04e2247b4af34effc7f5b89d36f34
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402413"
---
# <a name="quick-start-for-guarded-fabric-deployment"></a>보호 된 패브릭 배포에 대 한 빠른 시작

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목에서는 보호 된 패브릭의 정의, 요구 사항 및 배포 프로세스에 대 한 요약을 설명 합니다. 자세한 배포 단계는 [보호 된 호스트 및 보호 된 vm에 대 한 호스트 보호자 서비스 배포](https://technet.microsoft.com/windows-server-docs/security/guarded-fabric-shielded-vm/guarded-fabric-deploying-hgs-overview)를 참조 하세요.

동영상 버전을 보시겠습니까? [Windows Server 2016를 사용 하 여 보호 된 vm 및 보호 된 패브릭 배포](https://mva.microsoft.com/en-US/training-courses/deploying-shielded-vms-and-a-guarded-fabric-with-windows-server-2016-17131?l=WFLef7vUD_4604300474)Microsoft 가상 교육 과정을 참조 하세요.

## <a name="what-is-a-guarded-fabric"></a>보호 된 패브릭 이란?

_보호 된 패브릭_ 은 호스트에서 실행 되는 맬웨어 및 시스템 관리자의 검사, 도난 및 변조에 대해 테 넌 트 작업을 보호할 수 있는 Windows Server 2016 hyper-v 패브릭입니다. 이러한 가상화 된 테 넌 트 워크 로드 (미사용 및 비행 모두로 보호)를 보호 된 _vm_이라고 합니다. 

## <a name="what-are-the-requirements-for-a-guarded-fabric"></a>보호 된 패브릭에 대 한 요구 사항

보호 된 패브릭에 대 한 요구 사항은 다음과 같습니다.

- **악성 소프트웨어에서 무료로 제공 되는 보호 된 Vm을 실행 하는 장소입니다.**

    이러한 호스트를 _보호 된 호스트_라고 합니다. 
    보호 된 호스트는 HGS (호스트 보호 서비스) 라는 외부 기관에 대해 알려진 신뢰할 수 있는 상태에서 실행 되 고 있음을 증명할 수 있는 경우에만 보호 된 Vm을 실행할 수 있는 Windows Server 2016 Datacenter edition Hyper-v 호스트입니다. 
    HGS는 Windows Server 2016의 새로운 서버 역할이 며 일반적으로 3 개 노드 클러스터로 배포 됩니다. 

- **호스트가 정상 상태 인지 확인 하는 방법입니다.**

    HGS는 보호 된 호스트의 상태를 측정 하는 _증명_을 수행 합니다.

- **정상 호스트에 키를 안전 하 게 해제 하는 프로세스입니다.**

    HGS는 키 _보호 및 키 릴리스_를 수행 하 여 키를 정상 호스트로 다시 릴리스 합니다.

- **보호 된 Vm의 보안 프로 비전 및 호스팅을 자동화 하는 관리 도구입니다.**

    필요에 따라 보호 된 패브릭에 다음 관리 도구를 추가할 수 있습니다.

    - System Center 2016 Virtual Machine Manager (VMM) VMM은 Hyper-v 및 보호 된 패브릭 워크 로드와 함께 제공 되는 PowerShell cmdlet을 사용 하는 것 외에 추가 관리 도구를 제공 하기 때문에 권장 됩니다.
    - SPF (System Center 2016 Service Provider Foundation). Windows Azure 팩와 VMM 간의 API 계층 이며 Windows Azure 팩를 사용 하기 위한 필수 구성 요소입니다.
    - Windows Azure 팩는 보호 된 패브릭 및 보호 된 Vm을 관리 하는 데 유용한 그래픽 웹 인터페이스를 제공 합니다. 

실제로는 보호 되는 패브릭에서 사용 하는 [증명의 모드인](guarded-fabric-and-shielded-vms.md#attestation-modes-in-the-guarded-fabric-solution) 한 가지 결정을 내려야 합니다. 두 가지 방법, 즉 함께 사용할 수 없는 두 가지 방법이 있습니다 .이는 HGS가 Hyper-v 호스트의 정상 상태를 측정 하는 것입니다. HGS를 초기화할 때 모드를 선택 해야 합니다.  

- 호스트 키 증명 또는 키 모드는 보안 수준이 낮지만 도입 하기 쉽습니다.  
- TPM 기반 증명 또는 TPM 모드는 더 안전 하지만 더 많은 구성과 특정 하드웨어가 필요 합니다.

필요한 경우 Windows Server 2019 Datacenter edition으로 업그레이드 된 기존 Hyper-v 호스트를 사용 하 여 키 모드로 배포한 다음 서버 하드웨어 지원 (TPM 2.0 포함)을 사용할 수 있는 경우 보다 안전한 TPM 모드로 변환할 수 있습니다. 

이제 조각이 무엇 인지 알고 있으므로 배포 모델의 예를 살펴보겠습니다.

## <a name="how-to-get-from-a-current-hyper-v-fabric-to-a-guarded-fabric"></a>현재 Hyper-v 패브릭에서 보호 된 패브릭에 가져오는 방법

다음 그림의 Contoso.com와 같은 기존 Hyper-v 패브릭을 사용 하 고 Windows Server 2016 보호 된 패브릭을 빌드하려고 하는 경우를 예로 들어 보겠습니다.

![기존 Hyper-v 패브릭](../media/Guarded-Fabric-Shielded-VM/guarded-fabric-existing-hyper-v.png)

## <a name="step-1-deploy-the-hyper-v-hosts-running-windows-server-2016"></a>1단계: Windows Server 2016를 실행 하는 Hyper-v 호스트 배포 

Hyper-v 호스트는 Windows Server 2016 Datacenter edition 이상을 실행 해야 합니다. 호스트를 업그레이드 하는 경우 Standard edition에서 Datacenter edition으로 [업그레이드할](https://technet.microsoft.com/windowsserver/dn527667.aspx) 수 있습니다.

![Hyper-v 호스트 업그레이드](../../security/media/Guarded-Fabric-Shielded-VM/guarded-fabric-deployment-step-one-upgrade-hyper-v.png)

## <a name="step-2-deploy-the-host-guardian-service-hgs"></a>2단계: HGS (호스트 보호 서비스) 배포

그런 다음, HGS 서버 역할을 설치 하 고 다음 그림의 relecloud.com 예제와 같이 3 개 노드 클러스터로 배포 합니다. 이를 위해서는 다음과 같은 세 가지 PowerShell cmdlet이 필요 합니다.

- HGS 역할을 추가 하려면 다음을 사용 합니다.`Install-WindowsFeature` 
- HGS를 설치 하려면 다음을 사용 합니다.`Install-HgsServer` 
- 선택한 증명 모드를 사용 하 여 HGS를 초기화 하려면 다음을 사용 합니다.`Initialize-HgsServer` 

기존 Hyper-v 서버가 TPM 모드에 대 한 필수 구성 요소를 충족 하지 않는 경우 (예: TPM 2.0을 포함 하지 않음) 관리 기반 증명 (AD 모드)을 사용 하 여 HGS를 초기화할 수 있습니다. 그러면 패브릭 도메인과 Active Directory 신뢰 해야 합니다. 

이 예에서는 Contoso가 처음에는 규정 준수 요구 사항을 충족 하기 위해 AD 모드에서 배포 하 고, 적절 한 서버 하드웨어를 구매할 수 있게 되 면 보다 안전한 TPM 기반 증명으로 변환할 계획 이라고 가정해 보겠습니다. 

![HGS 설치](../media/Guarded-Fabric-Shielded-VM/guarded-fabric-deployment-step-two-deploy-hgs.png)

## <a name="step-3-extract-identities-hardware-baselines-and-code-integrity-policies"></a>3단계: Id, 하드웨어 기준 및 코드 무결성 정책을 추출 합니다.

Hyper-v 호스트에서 id를 추출 하는 프로세스는 사용 중인 증명 모드에 따라 달라 집니다.

AD 모드의 경우 호스트의 ID는 도메인에 가입 된 컴퓨터 계정으로, 패브릭 도메인에서 지정 된 보안 그룹의 구성원 이어야 합니다.
호스트의 상태가 정상 인지 여부에 대 한 유일한 결정은 지정 된 그룹의 멤버 자격입니다. 

이 모드에서 패브릭 관리자는 단순히 Hyper-v 호스트의 상태를 확인 하는 일을 담당 합니다. HGS는 실행할 수 있거나 실행할 수 없는 항목을 결정 하는 부분을 재생 하지 않으므로 맬웨어 및 디버거는 설계 된 대로 작동 합니다. 

그러나 프로세스에 직접 연결을 시도 하는 디버거 (예: WinDbg)는 VM의 작업자 프로세스 (VMWP .exe)가 PPL (protected process light) 이므로 보호 된 Vm에 대해 차단 됩니다.
LiveKd에서 사용 하는 것과 같은 대체 디버깅 기술은 차단 되지 않습니다. 보호 된 Vm과 달리 암호화 지원 Vm에 대 한 작업자 프로세스는 PPL으로 실행 되지 않으므로 WinDbg와 같은 기존 디버거는 정상적으로 계속 작동 합니다.

다른 방법으로 명시 된 경우 TPM 모드에 사용 되는 엄격한 유효성 검사 단계는 어떤 방식으로든 AD 모드에 사용 되지 않습니다.

TPM 모드의 경우 다음과 같은 세 가지 작업이 필요 합니다. 

1.  각 및 모든 Hyper-v 호스트의 TPM 2.0에서 _공개 인증 키_ (또는 _EKpub_) EKpub를 캡처하려면를 사용 `Get-PlatformIdentifier`합니다. 
2.  _하드웨어 기준_입니다. Hyper-v 호스트가 동일한 경우에는 단일 기준이 모두 필요 합니다. 그렇지 않은 경우 각 하드웨어 클래스에 대해 하나가 필요 합니다. 기준은 신뢰할 수 있는 컴퓨팅 그룹 로그 파일 또는 TCGlog 형식입니다. TCGlog에는 호스트가 완전히 부팅 되는 것과 같이 UEFI 펌웨어에서 커널이 발생 한 모든 항목이 포함 됩니다. 하드웨어 기준을 캡처하려면 Hyper-v 역할 및 호스트 보호 Hyper-v 지원 기능을 설치 하 고를 사용 `Get-HgsAttestationBaselinePolicy`합니다. 
3.  _코드 무결성 정책_입니다. Hyper-v 호스트가 동일한 경우에는 단일 CI 정책만 있으면 됩니다. 그렇지 않은 경우 각 하드웨어 클래스에 대해 하나가 필요 합니다. Windows Server 2016 및 Windows 10에는 모두 _HVCI (하이퍼바이저 적용 코드 무결성)_ 라고 하는 CI 정책에 대 한 새로운 형태의 적용이 있습니다. HVCI는 강력한 적용을 제공 하며, 호스트가 신뢰할 수 있는 관리자가 실행할 수 있는 이진 파일만 실행할 수 있도록 합니다. 이러한 지침은 HGS에 추가 되는 CI 정책에 래핑됩니다. HGS는 보호 된 Vm을 실행 하도록 허용 되기 전에 각 호스트의 CI 정책을 측정 합니다. CI 정책을 캡처하려면를 사용 `New-CIPolicy`합니다. 그런 다음를 사용 하 여 `ConvertFrom-CIPolicy`정책을 이진 형식으로 변환 해야 합니다.

![Id, 기준 및 CI 정책 추출](../media/Guarded-Fabric-Shielded-VM/guarded-fabric-deployment-step-three-extract-identity-baseline-ci-policy.png)

즉, 보호 된 패브릭을 실행 하는 인프라를 기준으로 빌드됩니다.  
이제 보호 된 VM을 간단 하 고 안전 하 게 프로 비전 할 수 있도록 보호 된 VM 템플릿 디스크 및 보호 데이터 파일을 만들 수 있습니다. 

## <a name="step-4-create-a-template-for-shielded-vms"></a>4단계: 보호 된 Vm에 대 한 템플릿 만들기

보호 된 VM 템플릿은 알려진 신뢰 시점에서 디스크의 서명을 만들어 템플릿 디스크를 보호 합니다. 
템플릿 디스크가 나중에 맬웨어에 감염 된 경우 해당 서명은 안전한 보호 된 VM 프로 비전 프로세스에서 검색 되는 원래 템플릿과 다릅니다. 
차폐 템플릿 디스크는 **차폐 템플릿 디스크 만들기 마법사나** `Protect-TemplateDisk` 일반 템플릿 디스크를 실행 하 여 생성 됩니다. 

각은 [Windows 10 용 원격 서버 관리 도구](https://www.microsoft.com/download/details.aspx?id=45520)의 **차폐 VM 도구** 기능에 포함 되어 있습니다.
RSAT를 다운로드 한 후 다음 명령을 실행 하 여 **보호 된 VM 도구** 기능을 설치 합니다.

```powershell
Install-WindowsFeature RSAT-Shielded-VM-Tools -Restart
```

패브릭 관리자 또는 VM 소유자와 같은 신뢰할 수 있는 관리자에 게는 VHDX 템플릿 디스크에 서명 하는 인증서 (종종 호스팅 서비스 공급자가 제공)가 필요 합니다. 

![차폐 템플릿 디스크 마법사](../media/Guarded-Fabric-Shielded-VM/guarded-fabric-shielded-template-wizard.png)

디스크 서명은 가상 디스크의 OS 파티션에 대해 계산 됩니다.
OS 파티션에서 변경 내용이 하나라도 있으면 서명이 변경 됩니다.
이렇게 하면 사용자가 적절 한 서명을 지정 하 여 신뢰 하는 디스크를 강력 하 게 식별할 수 있습니다.

시작 하기 전에 [템플릿 디스크 요구 사항을](guarded-fabric-create-a-shielded-vm-template.md) 검토 합니다. 

## <a name="step-5-create-a-shielding-data-file"></a>5단계: 보호 데이터 파일 만들기 

.Pda 파일이 라고도 하는 보호 데이터 파일은 관리자 암호와 같은 가상 컴퓨터에 대 한 중요 한 정보를 캡처합니다. 

![보호 데이터](../media/Guarded-Fabric-Shielded-VM/guarded-fabric-deployment-step-five-create-shielding-data.png)

보호 데이터 파일에는 보호 된 VM에 대 한 보안 정책 설정도 포함 됩니다. 보호 데이터 파일을 만들 때 다음 두 가지 보안 정책 중 하나를 선택 해야 합니다.

- 차폐
   
    가장 안전한 옵션으로, 많은 관리 공격 벡터를 제거 합니다.

- 암호화 지원

    VM을 암호화할 수 있지만 Hyper-v 관리자가 VM 콘솔 연결 및 PowerShell Direct를 사용 하는 것과 같은 작업을 수행할 수 있도록 하는 더 낮은 수준의 보호를 제공 합니다. 

    ![새 암호화 지원 VM](../media/Guarded-Fabric-Shielded-VM/guarded-fabric-new-shielded-vm.png)

VMM 또는 Windows Azure 팩와 같은 선택적 관리 부분을 추가할 수 있습니다. 이러한 부분을 설치 하지 않고 VM을 만들려면 [단계별 절차 – VMM을 사용 하지 않고 보호 된 Vm 만들기](https://blogs.technet.microsoft.com/datacentersecurity/2016/06/06/step-by-step-creating-shielded-vms-without-vmm/)를 참조 하세요.

## <a name="step-6-create-a-shielded-vm"></a>6단계: 차폐 VM 만들기

차폐 가상 컴퓨터를 만드는 것은 일반 가상 컴퓨터와 거의 다르지 않습니다. Windows Azure 팩에서는 이름, 보호 데이터 파일 (기타 특수화 정보 포함) 및 VM 네트워크를 제공 하기만 하면 되므로 일반 VM을 만드는 것 보다 훨씬 쉽습니다. 

![Windows Azure 팩의 새 차폐 VM](../media/Guarded-Fabric-Shielded-VM/guarded-fabric-new-vm-config.png)

## <a name="next-step"></a>다음 단계

> [!div class="nextstepaction"]
> [HGS 필수 구성 요소](guarded-fabric-prepare-for-hgs.md)
