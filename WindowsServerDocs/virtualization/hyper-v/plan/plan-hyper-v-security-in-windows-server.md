---
title: Windows Server에서 Hyper-v 보안 계획
description: Hyper-v 호스트 및 virtual machines에 대 한 보안 고려 사항 목록을 제공합니다.
ms.prod: windows-server-threshold
ms.service: na
ms.suite: na
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 115db481-b57e-41c3-8354-504f4bc6113a
manager: dongill
author: larsiwer
ms.author: kathyDav
ms.date: 08/03/2018
ms.openlocfilehash: 462124e1907ef03aa7746dd050be3e8c84c7abda
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59877414"
---
# <a name="plan-for-hyper-v-security-in-windows-server"></a>Windows Server에서 Hyper-v 보안 계획

>적용 대상: Windows Server 2016, Microsoft Hyper-V Server 2016, Windows Server 2019, Microsoft Hyper-V Server 2019

Hyper-v 호스트 운영 체제, 가상 컴퓨터, 구성 파일 및 가상 머신 데이터를 보호 합니다. 검사 목록으로 다음과 같은 모범 사례를 사용 하 여 Hyper-v 환경을 보호할 수 있습니다.

## <a name="secure-the-hyper-v-host"></a>Hyper-v 호스트를 보호 합니다.
- **호스트 OS 보안 상태를 유지 합니다.**
    - 관리 운영 체제에 필요한 최소 Windows Server 설치 옵션을 사용 하 여 공격 노출 영역을 최소화 합니다. 자세한 내용은 참조는 [설치 옵션 섹션](/windows-server/windows-server#installation-options) Windows Server 기술 콘텐츠 라이브러리의 합니다. Windows 10의 Hyper-v에서 프로덕션 워크 로드를 실행 하는 권장 하지 않습니다.
    - Hyper-v 호스트 운영 체제, 펌웨어 및 드라이버 최신 보안 업데이트를 사용 하 여 최신 상태로 유지 합니다. 펌웨어 및 드라이버 업데이트는 공급 업체의 권장 사항을 확인 합니다.
    - 불필요 한 소프트웨어를 설치 또는 워크스테이션으로 Hyper-v 호스트를 사용 하지 마세요.
    - Hyper-v 호스트를 원격으로 관리 합니다. 로컬 Hyper-v 호스트를 관리 해야 하는 경우 Credential Guard 사용 합니다. 자세한 정보는 [Credential Guard를 사용하여 파생된 도메인 자격 증명 보호](https://docs.microsoft.com/windows/access-protection/credential-guard/credential-guard)를 참조하세요.
    - 코드 무결성 정책을 사용 하도록 설정 합니다. 가상화 기반 보안을 사용 하 여 코드 무결성 서비스를 보호 합니다. 자세한 내용은 [Device Guard 배포 가이드](https://docs.microsoft.com/windows/device-security/device-guard/device-guard-deployment-guide)합니다.
- **보안 네트워크를 사용 합니다.**
    - 별도 네트워크를 실제 Hyper-v 컴퓨터에 대 한 전용된 네트워크 어댑터를 사용 합니다.
    - 개인 또는 보안 네트워크 액세스 VM 구성 파일과 가상 하드 디스크를 사용 합니다.
    - 실시간 마이그레이션 트래픽에 대 한 개인/전용 네트워크를 사용 합니다. 암호화를 사용 하 고 마이그레이션하는 동안 네트워크를 통해 이동 하는 VM의 데이터 보호를이 네트워크에서 IPSec을 사용 하도록 설정 하는 것이 좋습니다. 자세한 내용은 [장애 조치 클러스터링이 없는 실시간 마이그레이션에 대해 호스트 설정](../deploy/set-up-hosts-for-live-migration-without-failover-clustering.md)합니다.
- **저장소 마이그레이션 트래픽의 보안을 유지 합니다.** 

    SMB 데이터 및 데이터 보호 변조 또는 신뢰할 수 없는 네트워크에서 도청의 종단 간 암호화를 위해 SMB 3.0을 사용 합니다. 개인 네트워크를 사용 하 여 중간자 개입 공격을 방지 하기 위해 SMB 공유 내용에 액세스할 수 있습니다. 자세한 내용은 [SMB 강화 된 보안](https://technet.microsoft.com/library/dn551363.aspx)합니다. 
- **호스트 보호 된 패브릭의 일부가 되도록 구성 합니다.** 

    자세한 내용은 [패브릭에 보호 된](../../../security/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms-top-node.md)합니다.
- **장치를 보호 합니다.** 

    가상 머신 리소스 파일을 둔 저장소 장치를 보호 합니다.
    
- **하드 드라이브를 보호 합니다.** 

    BitLocker 드라이브 암호화를 사용 하 여 리소스를 보호 합니다.
    
- **Hyper-v 호스트 운영 체제를 강화 합니다.** 

    에 설명 된 기본 보안 설정을 권장 사항을 사용 합니다 [Windows Server 보안 기준](https://docs.microsoft.com/windows/device-security/windows-security-baselines)합니다.
    
- **적절 한 권한을 부여 합니다.**
    - Hyper-v 관리자 그룹에 Hyper-v 호스트를 관리 해야 하는 사용자를 추가 합니다.
    - 권한을 부여 하지 않으면 가상 컴퓨터 관리자가 Hyper-v에 대 한 운영 체제를 호스트 합니다.

- **바이러스 백신 제외 사항 및 Hyper-v에 대 한 옵션을 구성 합니다.**  

    Windows Defender 이미 [자동 제외](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-antivirus/configure-server-exclusions-windows-defender-antivirus) 구성 합니다. 제외에 대 한 자세한 내용은 참조 하세요. [권장 되는 Hyper-v 호스트에 대 한 바이러스 백신 제외](https://support.microsoft.com/kb/3105657)합니다. 

- **알 수 없는 Vhd를 탑재 하지 마십시오.** 이 호스트 파일 시스템 수준 공격에 노출할 수 있습니다.

- **필요한 경우가 아니면 프로덕션 환경에서 중첩을 사용 하지 않는 합니다.**

    중첩을 사용 하도록 설정 하면 가상 머신에서 지원 되지 않는 하이퍼바이저를 실행 하지 마세요.  

더 안전한 환경:

- **보호 된 패브릭 설정 하는 모듈 TPM (Trusted Platform) 2.0 칩을 사용 하 여 하드웨어를 사용 합니다.** 

    자세한 내용은 [Windows Server 2016에서 Hyper-v에 대 한 시스템 요구 사항](../system-requirements-for-hyper-v-on-windows.md)합니다.

## <a name="secure-virtual-machines"></a>가상 머신 보호
- **지원 되는 게스트 운영 체제에 대 한 가상 머신 2 세대를 만듭니다.** 

    자세한 내용은 [2 세대 보안 설정을](../learn-more/Generation-2-virtual-machine-security-settings-for-Hyper-V.md)합니다.
    
- **보안 부팅을 사용 합니다.** 

    자세한 내용은 [2 세대 보안 설정을](../learn-more/Generation-2-virtual-machine-security-settings-for-Hyper-V.md)합니다.
    
- **게스트 OS 보안을 유지 합니다.**

    - 프로덕션 환경에서 가상 컴퓨터를 설정 하기 전에 최신 보안 업데이트를 설치 합니다.
    - 필요 하 고 최신 상태로 유지 하는 지원 되는 게스트 운영 체제에 대 한 integration services를 설치 합니다. 지원 되는 Windows 버전을 실행 하는 게스트에 대 한 통합 서비스 업데이트는 Windows Update를 통해 사용할 수 있습니다.
    - 수행 하는 역할에 따라 각 가상 컴퓨터에서 실행 되는 운영 체제를 강화 합니다. 에 설명 된 기본 보안 설정을 권장 사항을 사용 합니다 [Windows 보안 기준](https://docs.microsoft.com/windows/device-security/windows-security-baselines)합니다.
    
- **보안 네트워크를 사용 합니다.** 

    올바른 가상 스위치에 가상 네트워크 어댑터 연결 제한 확인 하 고 적절 한 보안 설정을 적용 되었는지 확인 합니다.
    
- **가상 하드 디스크 및 스냅숏 파일을 안전한 위치에 저장 합니다.**

- **장치를 보호 합니다.** 

    가상 컴퓨터만 필요한 장치를 구성 합니다. 특정 시나리오에 필요 하지 않은 경우 프로덕션 환경에서 불연속 장치 할당을 사용 하도록 설정 하지 마십시오. 있도록 수행 하는 경우에 신뢰할 수 있는 공급 업체에서 장치를 노출 해야 합니다. 
    
- **구성 바이러스 백신, 방화벽 및 침입 검색 소프트웨어** 가상 컴퓨터 역할을 기반으로 적절 하 게 가상 머신 내에서.

- **Windows 10 또는 Windows Server 2016 이상을 실행 하는 게스트에 대 한 가상화 기반 보안을 사용 합니다.** 

    자세한 내용은 참조는 [Device Guard 배포 가이드](https://docs.microsoft.com/windows/device-security/device-guard/device-guard-deployment-guide)합니다.
    
- **특정 워크 로드에 필요한 경우에 불연속 장치 할당을 사용**합니다. 

    물리적 장치를 통해 전달의 특성상 장치 제조업체에 이해 하는 경우 사용할 보안 환경에서 작동 합니다.

더 안전한 환경:

- **사용을 보호 된 가상 컴퓨터를 배포 하 고 보호 된 패브릭 배포 합니다.** 

    자세한 내용은 [2 세대 보안 설정](../learn-more/Generation-2-virtual-machine-security-settings-for-Hyper-V.md) 하 고 [패브릭에 보호 된](../../../security/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms-top-node.md)합니다.
