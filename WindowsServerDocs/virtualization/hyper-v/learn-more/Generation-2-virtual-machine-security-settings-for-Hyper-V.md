---
title: Hyper-v에 대한 2세대 가상 머신의 보안 설정
description: 2세대 가상 머신의 Hyper-V 관리자에서 사용할 수 있는 보안 설정에 대해 설명합니다.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.topic: article
ms.assetid: 06ab4f5f-6b8e-4058-8108-76785aa93d4c
author: larsiwer
ms.author: kathydav
ms.date: 10/04/2016
ms.openlocfilehash: 7eb867529d38ab21ee21c19f92c89ed4128b0ea4
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80860806"
---
# <a name="generation-2-virtual-machine-security-settings-for-hyper-v"></a>Hyper-v에 대한 2세대 가상 머신의 보안 설정

>적용 대상: Windows Server 2016, Microsoft Hyper-V Server 2016, Windows Server 2019, Microsoft Hyper-V Server 2019

Hyper-v 관리자에서 가상 머신의 보안 설정을 사용하여 데이터 및 가상 머신의 상태를 보호합니다. 검사, 도난 및 호스트 및 데이터 센터 관리자에서 실행할 수 있는 두 맬웨어로부터 변조에서 가상 컴퓨터를 보호할 수 있습니다. 차폐 가상 머신을 시작하는 호스트에 권한을 부여하는 호스트 보호자 서비스를 호출하는 서비스를 설정 했는지 여부 및 호스트 하드웨어를 실행하면 가상 머신 세대에 얻게 되는 보안 수준에 따라 다릅니다.  

호스트 보호자 서비스는 Windows Server 2016에서 새로운 역할입니다. 합법적인 Hyper-v 호스트를 식별 하고 지정된 된 가상 머신을 실행할 수 있습니다. 가장 일반적으로 데이터 센터에 대 한 호스트 보호자 서비스를 설정 합니다. 하지만 호스트 보호자 서비스를 설정하지 않고 로컬에서 실행되도록 실드된 가상 머신을 만들 수 있습니다. 호스트 보호자 패브릭 차폐 가상 머신을 나중에 배포할 수 있습니다.  

ost Guardian Service를 설정하지 않았거나 Hyper-V 호스트에서 로컬 모드로 실행 중이고 호스트에 가상 머신 소유자의 보호자 키가 있는 경우 이 항목에서 설명하는 설정을 변경할 수 있습니다.   보호자 키의 소유자 만들어지는 조직 및 퍼블릭 또는 퍼블릭 키를 소유 하는 모든 가상 컴퓨터는 해당 키를 사용 하 여 만든 공유 됩니다.  

만드는 방법을 가상 컴퓨터 호스트 보호자 서비스와 보다 안전한 알아보려면 다음 리소스를 참조 합니다.  

- [패브릭 강화: Hyper-V에서 테넌트 비밀 보호(Ignite 비디오)](https://go.microsoft.com/fwlink/?LinkId=746379)
- [보호된 패브릭 및 보호된 VM](https://go.microsoft.com/fwlink/?LinkId=746381)

## <a name="secure-boot-setting-in-hyper-v-manager"></a>Hyper-v 관리자에서 부팅 설정을 보안합니다  

보안 부팅은 부팅 시 실행 권한 없는 펌웨어, 운영 체제 또는 펌웨어 인터페이스 UEFI (Unified Extensible) 드라이버 (라고도 옵션 rom을 보유) 하지 않도록 하는 기능을 2 세대 가상 컴퓨터와 함께 사용할 수 있습니다. 보안 부팅은 기본적으로 사용 됩니다. Windows 또는 Linux 배포 운영 체제를 실행 하는 2 세대 가상 컴퓨터와 보안 부팅을 사용할 수 있습니다.  

다음 표에 설명 된 서식 파일에서 부팅 프로세스의 무결성을 확인 해야 하는 인증서를 참조 하십시오.  

|템플릿 이름|설명|  
|-----------------|---------------|  
|Microsoft Windows|보안 부팅에는 Windows 운영 체제에 대한 가상 머신을 선택합니다.|  
|UEFI 인증 기관|보안 부팅에는 Linux 배포 운영 체제에 대한 가상 머신을 선택합니다.|  
|오픈 소스 보호 VM|이 템플릿은 [Linux 기반의 보호된 VM](https://docs.microsoft.com/windows-server/security/guarded-fabric-shielded-vm/guarded-fabric-create-a-linux-shielded-vm-template)에 대한 보안 부팅을 위해 활용됩니다.|

자세한 내용은 다음 항목을 참조하세요.  

- [Windows 10 보안 개요](https://docs.microsoft.com/windows/security/threat-protection/overview-of-threat-mitigations-in-windows-10)  
- [1세대 또는 2세대 가상 머신을 Hyper-V에서 만들어야 하나요?](../plan/Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md)  
- [Linux 및 Hyper-V의 FreeBSD Virtual Machines](../Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md)  

## <a name="encryption-support-settings-in-hyper-v-manager"></a>Hyper-v 관리자의 암호화 지원 설정

다음 암호화 지원 옵션을 선택하여 데이터와 가상 머신의 상태를 보호할 수 있습니다.  

- **신뢰할 수 있는 플랫폼 모듈을 사용하도록 설정** -이 설정은 신뢰할 수 있는 TPM (플랫폼 모듈) 칩을 가상화된 가상 머신을 사용할 수 있도록 합니다. 이렇게 하면 게스트에 BitLocker를 사용하여 가상 머신 디스크를 암호화합니다.
  - Hyper-v 호스트는 Windows 10 1511를 실행 하는 경우 격리 된 사용자 모드를 사용 하도록 설정 해야 합니다. 
- **상태 및 VM 마이그레이션 트래픽을 암호화** -저장된 가상 머신 상태를 암호화 하고 실시간 마이그레이션 트래픽입니다.

### <a name="enable-isolated-user-mode"></a>격리 된 사용자 모드를 사용 하도록 설정

선택 하는 경우 **신뢰할 수 있는 플랫폼 모듈을 사용 하도록 설정** Windows 10 기념일 업데이트 보다 이전 버전의 Windows 실행 하는 Hyper-v 호스트, 격리 된 사용자 모드를 설정 해야 합니다. Windows Server 2016 또는 Windows 10 1주년 업데이트 이상을 실행하는 Hyper-V 호스트에서는 이 작업을 수행할 필요가 없습니다.

격리 된 사용자 모드는 Hyper-v 호스트에서 가상 보안 모드 내에서 보안 애플리케이션을 호스팅하는 런타임 환경입니다. TPM 칩을 가상의 상태를 보호 하는 가상 보안 모드 사용 됩니다.  

이전 버전의 Windows 10을 실행 하는 Hyper-v 호스트에서 격리 된 사용자 모드를 사용 하도록 설정 하려면  

1.  관리자 권한으로 Windows PowerShell을 엽니다.  

2.  다음 명령을 실행 합니다.  

    ```  
    Enable-WindowsOptionalFeature -Feature IsolatedUserMode -Online  
    New-Item -Path HKLM:\SYSTEM\CurrentControlSet\Control\DeviceGuard -Force  
    New-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Control\DeviceGuard -Name EnableVirtualizationBasedSecurity -Value 1 -PropertyType DWord -Force  

    ```  

Windows Server 2016 실행되는 모든 호스트에 사용하도록 설정하는 가상 TPM이 있는 가상 머신을 마이그레이션할 수 있습니다. Windows 10 10586 이상 버전을 빌드합니다. 하지만 다른 호스트로 마이그레이션하는 경우에 시작할 수 없습니다. 새 호스트 가상 머신을 실행할 권한을 부여하려면 해당 가상 머신에 대한 키 보호기를 업데이트해야 합니다. 자세한 내용은 [보호된 패브릭 및 보호된 VM](https://go.microsoft.com/fwlink/?LinkId=746381) 및 [Windows Server의 Hyper-V에 대한 시스템 요구 사항](../System-requirements-for-Hyper-V-on-Windows.md)을 참조하세요.  

## <a name="security-policy-in-hyper-v-manager"></a>Hyper-v 관리자의 보안 정책  
가상 머신 보안을 강화하려면 **보호 설정** 옵션을 사용하여 콘솔 연결, PowerShell Direct 및 일부 통합 구성 요소와 같은 관리 기능을 비활성화할 수 있습니다. 이 옵션을 선택 하는 경우 **보안 부팅**, **신뢰할 수 있는 플랫폼 모듈을 사용 하도록 설정**, 및 **암호화 상태와 VM 마이그레이션 트래픽을** 옵션 선택 및 적용 합니다.   

차폐 가상 머신 호스트 보호자 서비스를 설정하지 않고 로컬에서 실행할 수 있습니다. 하지만 다른 호스트로 마이그레이션하는 경우에 시작할 수 없습니다. 새 호스트 가상 머신을 실행할 권한을 부여하려면 해당 가상 머신에 대한 키 보호기를 업데이트해야 합니다. 자세한 내용은 참조 [보호 된 패브릭 및 차폐 Vm](https://go.microsoft.com/fwlink/?LinkId=746381)합니다.  

Windows Server의 보안에 대한 자세한 내용은 [보안 및 보증](../../../security/Security-and-Assurance.md)을 참조하세요.  
