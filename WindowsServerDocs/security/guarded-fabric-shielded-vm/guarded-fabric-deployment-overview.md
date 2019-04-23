---
title: 보호 된 패브릭 배포에 대 한 빠른 시작
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: e060e052-39a0-4154-90bb-b97cc6dde68e
manager: dongill
author: justinha
ms.author: justinha
ms.technology: security-guarded-fabric
ms.date: 01/30/2019
ms.openlocfilehash: d63726e7046896c9ef7aa0c3b3d85237bc3f788d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59879064"
---
# <a name="quick-start-for-guarded-fabric-deployment"></a>보호 된 패브릭 배포에 대 한 빠른 시작

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 항목을 파악할 보호 된 패브릭은 해당 요구 사항 및 배포 프로세스의 요약입니다. 자세한 배포 단계를 참조 하세요 [보호 된 호스트 및 차폐 Vm에 대 한 호스트 보호 서비스 배포](https://technet.microsoft.com/windows-server-docs/security/guarded-fabric-shielded-vm/guarded-fabric-deploying-hgs-overview)합니다.

동영상 버전을 보시겠습니까? Microsoft Virtual Academy 과정을 참조 하세요 [보호 된 Vm 배포 및 Windows Server 2016을 사용 하 여 보호 된 패브릭](https://mva.microsoft.com/en-US/training-courses/deploying-shielded-vms-and-a-guarded-fabric-with-windows-server-2016-17131?l=WFLef7vUD_4604300474)합니다.

## <a name="what-is-a-guarded-fabric"></a>보호 된 패브릭 이란

A _패브릭에 보호 된_ Windows Server 2016 Hyper-v 패브릭 검사, 도난 및 변조, 호스트에서 실행 되는 맬웨어에서와 시스템 관리자에 대 한 테 넌 트 워크 로드를 보호할 수 있습니다. 이러한 테 넌 트 워크 로드를 가상화-rest와-비행 보호-이라고 _보호 된 Vm_합니다. 

## <a name="what-are-the-requirements-for-a-guarded-fabric"></a>보호 된 패브릭에 대 한 요구 사항은 무엇입니까

보호 된 패브릭에 대 한 요구 사항은 같습니다.

- **보호 된 Vm는 악성 소프트웨어 로부터 무료을 실행할 수 있는 곳입니다.**

    이러한 이라고 _보호 된 호스트_합니다. 
    보호 된 호스트는 (HGS (호스트 보호 서비스)를 호출 하는 외부 기관에 알려진, 신뢰할 수 있는 상태에서 실행 중인지를 증명할 수 있습니다 하는 경우에 보호 된 Vm을 실행할 수 있는 Windows Server 2016 Datacenter edition Hyper-v 호스트입니다. 
    HGS는 Windows Server 2016의 새로운 서버 역할 및은 일반적으로 3 개 노드 클러스터로 배포 됩니다. 

- **호스트를 확인 하는 방법을 정상 상태입니다.**

    HGS 수행 _증명_, 보호 된 호스트의 상태를 측정 합니다.

- **정상 호스트에 대 한 키를 안전 하 게 해제 하는 프로세스입니다.**

    HGS 수행 _보호 및 주요 릴리스 키_, 여기서 다시 정상 호스트에 대 한 키를 해제 합니다.

- **보호 된 Vm을 관리 도구를 안전한 프로 비전 및 호스트를 자동화 합니다.**

    필요에 따라 보호 된 패브릭 관리 도구를 추가할 수 있습니다.

    - System Center 2016 Virtual Machine Manager (VMM). VMM은 Hyper-v 및 보호 된 패브릭 워크 로드를 사용 하 여 제공 되는 PowerShell cmdlet만을 사용 하 여 것 보다 도구 추가 관리를 제공 하기 때문에 권장 됩니다).
    - System Center 2016 Service Provider Foundation (SPF). 이것이 Windows Azure 팩 및 VMM 및 Windows Azure Pack을 사용 하기 위한 필수 구성 요소 간의 API 계층입니다.
    - Windows Azure Pack에는 보호 된 Vm 및 보호 된 패브릭 관리 하기 위한 좋은 그래픽 웹 인터페이스를 제공 합니다. 

실제로 결정 프런트로 구성 되어야 합니다: 합니다 [증명 모드는](guarded-fabric-and-shielded-vms.md#attestation-modes-in-the-guarded-fabric-solution) 보호 된 패브릭에서 사용 합니다. 두 가지 방법이 있습니다-상호 배타적인 두 가지 모드-는 HGS 측정할 수 있는 Hyper-v 호스트는 정상으로 합니다. HGS를 초기화할 경우 모드를 선택 해야 합니다.  

- 호스트 키 증명 또는 키 모드는 보안 수준은 낮지만 보다 쉽게 채택  
- TPM 기반 증명 또는 TPM 모드는 더 안전 하지만 자세한 구성 및 특정 하드웨어 필요

필요한 경우에 Windows Server 2019 Datacenter 버전으로 업그레이드 하는 기존 Hyper-v 호스트를 사용 하 여 키 모드에 배포할 수 있으며 서버 하드웨어 (TPM 2.0 포함)를 지 원하는 사용 가능한 경우 다음의 더 안전한 TPM 모드를 변환할 수 있습니다. 

구성 요소는 무엇을 파악 했으므로 배포 모델의 예를 살펴보겠습니다.

## <a name="how-to-get-from-a-current-hyper-v-fabric-to-a-guarded-fabric"></a>현재 Hyper-v 패브릭에서 시작 하는 보호 된 패브릭 하는 방법

이 시나리오를 가정해 보겠습니다-다음 그림에는 Contoso.com과 같은 기존 Hyper-v 패브릭을, 있고는 Windows Server 2016을 보호 된 패브릭을 빌드할 합니다.

![기존 Hyper-v 패브릭](../media/Guarded-Fabric-Shielded-VM/guarded-fabric-existing-hyper-v.png)

## <a name="step-1-deploy-the-hyper-v-hosts-running-windows-server-2016"></a>1단계: Windows Server 2016을 실행 하는 Hyper-v 호스트 배포 

Hyper-v 호스트를 Windows Server 2016 Datacenter edition을 실행 해야 합니다. 이상. 호스트를 업그레이드 하는 경우 [업그레이드](https://technet.microsoft.com/windowsserver/dn527667.aspx) Datacenter edition Standard edition에서.

![Hyper-v 호스트를 업그레이드 합니다.](../../security/media/Guarded-Fabric-Shielded-VM/guarded-fabric-deployment-step-one-upgrade-hyper-v.png)

## <a name="step-2-deploy-the-host-guardian-service-hgs"></a>2단계: 호스트 보호 서비스 (HGS) 배포

그런 다음 HGS 서버 역할을 설치 하 고 다음 그림과에서 relecloud.com 예제와 같이 3 개 노드 클러스터로 배포. 이 세 가지 PowerShell cmdlet을 필요합니다.

- HGS 역할을 추가 `Install-WindowsFeature` 
- HGS를 설치 하려면 사용 `Install-HgsServer` 
- HGS 증명의 선택된 모드를 사용 하 여 초기화를 사용 하 여 `Initialize-HgsServer` 

기존 Hyper-v 서버에서 TPM 모드에 대 한 필수 구성 요소를 충족 하지 않을 경우 (예를 들어 없는 TPM 2.0)에서 HGS 관리자 기반 증명 (AD 모드), 패브릭 도메인과 Active Directory 트러스트 해야 하는 사용 하 여 초기화할 수 있습니다. 

예제에서는 Contoso에서 처음에 즉시 규정 준수 요구 사항을 충족 하기 위해 AD 모드로 배포 하 고 적합 한 서버 하드웨어를 구입할 수 있습니다 후 보다 안전한 TPM 기반 증명 변환할 계획를 가정해 보겠습니다. 

![HGS 설치](../media/Guarded-Fabric-Shielded-VM/guarded-fabric-deployment-step-two-deploy-hgs.png)

## <a name="step-3-extract-identities-hardware-baselines-and-code-integrity-policies"></a>3단계: Id, 하드웨어 기준 및 코드 무결성 정책을 추출합니다

Hyper-v 호스트에서 identities를 추출 하는 프로세스는 사용 중인 증명 모드에 따라 다릅니다.

AD 모드에서 호스트의 ID는 해당 도메인에 가입 된 컴퓨터 계정, fabric 도메인에서 지정 된 보안 그룹의 멤버 여야 합니다.
지정 된 그룹의 구성원은 호스트 정상 인지 여부의 유일한 결정 합니다. 

이 모드에서는 패브릭 관리자는 Hyper-v 호스트의 상태를 확인 하는 것에 대 한 책임입니다. HGS 재생 일부가 되었거나 실행 되지 무엇을 결정 하므로 맬웨어 및 디버거 설계 된 대로 작동 됩니다. 

그러나 VM의 작업자 프로세스 (VMWP.exe) 보호 된 프로세스 광원 PPL ()는 디버거 (WinDbg.exe)와 같은 프로세스에 직접 연결 하려고 하는 보호 된 Vm에 대 한 차단 됩니다.
LiveKd.exe를 사용한 것과 같은 대체 디버깅 기법을 차단 되지 않습니다. 보호 된 Vm과 달리 암호화 지원 Vm에 대 한 작업자 프로세스는 기존 디버거 같은 WinDbg.exe 있도록 PPL는 계속 정상적으로 작동 하는 대로 실행 되지 않습니다.

즉, 어떤 방식으로든에서 AD 모드에 대 한 TPM 모드에 사용 되는 엄격한 유효성 검사 단계를 사용 되지 않습니다.

TPM 모드의 경우 다음 세 가지 요소가 필요 합니다. 

1.  A _공용 인증 키_ (또는 _EKpub_) 각 Hyper-v 호스트에 TPM 2.0에서. EKpub를 캡처하려면 사용 `Get-PlatformIdentifier`합니다. 
2.  A _하드웨어 기준_합니다. Hyper-v 호스트의 각 값이 동일 하면 단일 기준은 하기만 하면 됩니다. 그렇지 않은 경우 다음 해야 하드웨어의 각 클래스에 대 한 합니다. 기준선을 신뢰할 수 있는 컴퓨팅 그룹 로그 파일 또는 TCGlog 형식의 경우 TCGlog를 포함 하는 호스트를 부팅할 완전히 이르기까지 커널을 통해 UEFI 펌웨어에서 호스트에서 수행한 모든 합니다. 하드웨어 기준선을 캡처하려면 Hyper-v 역할 및 호스트 보호 Hyper-v 지원 기능을 설치 하 고 사용 하 여 `Get-HgsAttestationBaselinePolicy`입니다. 
3.  A _코드 무결성 정책_합니다. 각 Hyper-v 호스트에 동일한 경우, 단일 CI 정책 하기만 하면 됩니다. 그렇지 않은 경우 다음 해야 하드웨어의 각 클래스에 대 한 합니다. Windows Server 2016 및 Windows 10 적용 이라는 CI 정책에 대 한 새 폼이 있다고 _하이퍼바이저 적용 코드 무결성 (HVCI)_ 합니다. HVCI 강력한 적용을 제공 하 고 호스트에 신뢰할 수 있는 관리자를 실행 하도록 허용에 이진 파일을 실행할 수만 확인 합니다. 이러한 지침 HGS에 추가 되는 CI 정책에 래핑됩니다. HGS는 보호 된 Vm 실행을 허용 하는 해당 전에 각 호스트의 CI 정책을 측정 합니다. CI 정책을 캡처하려면 `New-CIPolicy`합니다. 정책을 사용 하 여 해당 이진 형식으로 변환 후 해야 `ConvertFrom-CIPolicy`합니다.

![Id, 기준 및 CI 정책 추출](../media/Guarded-Fabric-Shielded-VM/guarded-fabric-deployment-step-three-extract-identity-baseline-ci-policy.png)

이것이 전부-실행 하는 인프라 측면에서 보호 된 패브릭 작성 됩니다.  
이제 보호 된 VM 템플릿 디스크 및 따라서 보호 된 보호 데이터 파일을 만들 수 있습니다 단순히와 안전 하 게에 Vm 프로 비전 할 수 있습니다. 

## <a name="step-4-create-a-template-for-shielded-vms"></a>4단계: 보호 된 vm 템플릿 만들기

보호 된 VM 템플릿 신뢰할 수 있는 지점에서 디스크의 서명이 시간에서 만들어 템플릿 디스크를 보호 합니다. 
템플릿 디스크는 나중에 맬웨어에 감염 된 경우 해당 서명이 보안 보호 된 VM 프로 비전 프로세스에서 검색 되는 원래 템플릿을 달라 집니다. 
보호 된 템플릿 디스크를 실행 하 여 만들어집니다 합니다 **보호 된 템플릿 디스크 만들기 마법사** 또는 `Protect-TemplateDisk` 일반 템플릿 디스크에 대 한 합니다. 

에 포함 된 각 합니다 **보호 된 VM 도구** 기능을 [원격 서버 관리 도구에 대 한 Windows 10](https://www.microsoft.com/download/details.aspx?id=45520)합니다.
RSAT를 다운로드 한 후 설치 하려면이 명령을 실행 합니다 **보호 된 VM 도구** 기능:

```powershell
Install-WindowsFeature RSAT-Shielded-VM-Tools -Restart
```

패브릭 관리자 또는 VM 소유자와 같은 신뢰할 수 있는 관리자는 VHDX 템플릿 디스크 서명 인증서 (종종 호스팅 서비스 공급자에서 제공)을 해야 합니다. 

![보호 된 템플릿 디스크 마법사](../media/Guarded-Fabric-Shielded-VM/guarded-fabric-shielded-template-wizard.png)

가상 디스크의 OS 파티션을 통해 디스크 서명이 계산 됩니다.
OS 파티션에 변경 사항이 시그니처도 변경 됩니다.
이 강력한 적절 한 서명을 지정 하 여 신뢰할 수 있는 디스크를 식별 하는 사용자 수 있습니다.

검토 합니다 [템플릿 디스크 요구 사항을](guarded-fabric-create-a-shielded-vm-template.md) 시작 하기 전에 합니다. 

## <a name="step-5-create-a-shielding-data-file"></a>5단계: 실딩 데이터 파일을 만들려면 

실딩 데이터 파일,.pdk 파일이 라고도 관리자 암호와 같은 가상 컴퓨터에 대 한 중요 한 정보를 캡처합니다. 

![실딩 데이터](../media/Guarded-Fabric-Shielded-VM/guarded-fabric-deployment-step-five-create-shielding-data.png)

실딩 데이터 파일에는 보호 된 VM에 대 한 보안 정책 설정도를 포함 됩니다. 실딩 데이터 파일을 만들 때 두 개의 보안 정책 중 하나를 선택 해야 합니다.

- 보호 된
   
    많은 관리 공격 벡터를 제거 하는 가장 안전한 옵션입니다.

- 암호화 지원

    낮은 수준의 여전히 암호화 된 VM 수의 규정 준수 이점을 제공 하지만 같은 작업을 수행 하려면 Hyper-v 관리자를 사용 하면 보호를 VM 콘솔 연결 및 PowerShell Direct를 사용 합니다. 

    ![새 암호화 지원 VM](../media/Guarded-Fabric-Shielded-VM/guarded-fabric-new-shielded-vm.png)

VMM 또는 Windows Azure Pack과 같은 선택적 관리 정보를 추가할 수 있습니다. 해당 부분을 설치 하지 않고 VM을 만들기를 참조 하려는 경우 [단계별로 – VMM 없이 보호 된 Vm 만드는](https://blogs.technet.microsoft.com/datacentersecurity/2016/06/06/step-by-step-creating-shielded-vms-without-vmm/)합니다.

## <a name="step-6-create-a-shielded-vm"></a>6단계: 보호 된 VM 만들기

거의 다른 보호 된 가상 컴퓨터를 만드는 일반 virtual machines에서. Windows Azure pack에서 환경은 해야 하기 때문에 이름을 제공한 보호 데이터 파일 (나머지 특수화 정보 포함) 및 VM 네트워크는 일반 VM을 만드는 것 보다 더 쉽습니다. 

![Windows Azure 팩에서 새 보호 된 VM](../media/Guarded-Fabric-Shielded-VM/guarded-fabric-new-vm-config.png)

## <a name="next-step"></a>다음 단계

>[!div class="nextstepaction"]
[HGS 필수 구성 요소](guarded-fabric-prepare-for-hgs.md)
