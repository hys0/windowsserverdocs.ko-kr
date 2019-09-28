---
title: Windows Server의 Hyper-v 보안 계획
description: Hyper-v 호스트 및 가상 컴퓨터에 대 한 보안 고려 사항 목록을 제공 합니다.
ms.prod: windows-server
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
ms.openlocfilehash: 8fd86ae500fff1e6b8c27b0d34d1dcbeeade9f81
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392953"
---
# <a name="plan-for-hyper-v-security-in-windows-server"></a>Windows Server의 Hyper-v 보안 계획

>적용 대상: Windows Server 2016, Microsoft Hyper-V Server 2016, Windows Server 2019, Microsoft Hyper-V Server 2019

Hyper-v 호스트 운영 체제, 가상 컴퓨터, 구성 파일 및 가상 컴퓨터 데이터를 보호 합니다. Hyper-v 환경을 보호 하는 데 도움이 되는 다음 권장 사항 목록을 검사 목록으로 사용 합니다.

## <a name="secure-the-hyper-v-host"></a>Hyper-v 호스트 보호
- **호스트 OS를 안전 하 게 유지 합니다.**
    - 관리 운영 체제에 필요한 최소 Windows Server 설치 옵션을 사용 하 여 공격 노출 영역을 최소화 합니다. 자세한 내용은 Windows Server 기술 콘텐츠 라이브러리의 [설치 옵션 섹션](/windows-server/windows-server#installation-options) 을 참조 하십시오. Windows 10의 Hyper-v에서 프로덕션 워크 로드를 실행 하지 않는 것이 좋습니다.
    - 최신 보안 업데이트를 사용 하 여 Hyper-v 호스트 운영 체제, 펌웨어 및 장치 드라이버를 최신으로 유지 합니다. 공급 업체의 권장 사항을 확인 하 여 펌웨어 및 드라이버를 업데이트 합니다.
    - Hyper-v 호스트를 워크스테이션으로 사용 하지 않거나 불필요 한 소프트웨어를 설치 하지 마세요.
    - Hyper-v 호스트를 원격으로 관리 합니다. Hyper-v 호스트를 로컬로 관리 해야 하는 경우 Credential Guard를 사용 합니다. 자세한 정보는 [Credential Guard를 사용하여 파생된 도메인 자격 증명 보호](https://docs.microsoft.com/windows/access-protection/credential-guard/credential-guard)를 참조하세요.
    - 코드 무결성 정책을 사용 하도록 설정 합니다. 가상화 기반 보안 보호 된 코드 무결성 서비스를 사용 합니다. 자세한 내용은 [Device Guard 배포 가이드](https://docs.microsoft.com/windows/device-security/device-guard/device-guard-deployment-guide)를 참조 하세요.
- **보안 네트워크를 사용 합니다.**
    - 실제 Hyper-v 컴퓨터에 전용 네트워크 어댑터를 사용 하 여 별도의 네트워크를 사용 합니다.
    - 개인 또는 보안 네트워크를 사용 하 여 VM 구성 및 가상 하드 디스크 파일에 액세스 합니다.
    - 실시간 마이그레이션 트래픽에 개인/전용 네트워크를 사용 합니다. 이 네트워크에서 IPSec을 사용 하도록 설정 하 여 마이그레이션 중에 네트워크를 통해 이동 하는 VM 데이터를 보호 하는 것이 좋습니다. 자세한 내용은 [장애 조치 (Failover) 클러스터링이 없는 실시간 마이그레이션에 대 한 호스트 설정](../deploy/set-up-hosts-for-live-migration-without-failover-clustering.md)을 참조 하세요.
- **저장소 마이그레이션 트래픽을 보호 합니다.** 

    Smb 데이터의 종단 간 암호화와 신뢰할 수 없는 네트워크에서 데이터 보호 변조 또는 도청에 SMB 3.0을 사용 합니다. 개인 네트워크를 사용 하 여 메시지 가로채기 (man-in-the-middle) 공격을 방지 하기 위해 SMB 공유 콘텐츠에 액세스 합니다. 자세한 내용은 [SMB 보안 강화](https://technet.microsoft.com/library/dn551363.aspx)를 참조 하세요. 
- **보호 된 패브릭의 일부가 되도록 호스트를 구성 합니다.** 

    자세한 내용은 [보호 된 패브릭](../../../security/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms-top-node.md)을 참조 하세요.
- **장치를 보호 합니다.** 

    가상 컴퓨터 리소스 파일을 보관 하는 저장 장치를 안전 하 게 보호 합니다.
    
- **하드 드라이브를 보호 합니다.** 

    BitLocker 드라이브 암호화를 사용 하 여 리소스를 보호 합니다.
    
- **Hyper-v 호스트 운영 체제를 강화 합니다.** 

    [Windows Server 보안 기준](https://docs.microsoft.com/windows/device-security/windows-security-baselines)에 설명 된 기본 보안 설정 권장 사항을 사용 합니다.
    
- **적절 한 사용 권한을 부여 합니다.**
    - Hyper-v 호스트를 관리 해야 하는 사용자를 Hyper-v administrators 그룹에 추가 합니다.
    - Hyper-v 호스트 운영 체제에 대 한 가상 컴퓨터 관리자 권한을 부여 하지 마세요.

- **Hyper-v에 대 한 바이러스 백신 제외 및 옵션을 구성 합니다.**  

    Windows Defender에 이미 [자동 제외](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-antivirus/configure-server-exclusions-windows-defender-antivirus) 가 구성 되어 있습니다. 제외에 대 한 자세한 내용은 [hyper-v 호스트에 권장 되는 바이러스 백신 제외](https://support.microsoft.com/kb/3105657)를 참조 하십시오. 

- **알 수 없는 Vhd를 탑재 하지 않습니다.** 이는 호스트를 파일 시스템 수준 공격에 노출 시킬 수 있습니다.

- **필요 하지 않은 경우 프로덕션 환경에서 중첩을 사용 하도록 설정 하지 마세요.**

    중첩을 사용 하도록 설정 하는 경우 가상 머신에서 지원 되지 않는 하이퍼바이저를 실행 하지 않습니다.  

더 안전한 환경:

- **TPM (신뢰할 수 있는 플랫폼 모듈) 2.0 칩과 함께 하드웨어를 사용 하 여 보호 된 패브릭을 설정 합니다.** 

    자세한 내용은 [Windows Server 2016의 hyper-v에 대 한 시스템 요구 사항](../system-requirements-for-hyper-v-on-windows.md)을 참조 하세요.

## <a name="secure-virtual-machines"></a>가상 컴퓨터 보호
- **지원 되는 게스트 운영 체제에 대 한 2 세대 가상 컴퓨터를 만듭니다.** 

    자세한 내용은 [2 세대 보안 설정](../learn-more/Generation-2-virtual-machine-security-settings-for-Hyper-V.md)을 참조 하세요.
    
- **보안 부팅을 사용 하도록 설정 합니다.** 

    자세한 내용은 [2 세대 보안 설정](../learn-more/Generation-2-virtual-machine-security-settings-for-Hyper-V.md)을 참조 하세요.
    
- **게스트 OS를 안전 하 게 유지 합니다.**

    - 프로덕션 환경에서 가상 컴퓨터를 설정 하기 전에 최신 보안 업데이트를 설치 합니다.
    - 이를 필요로 하는 지원 되는 게스트 운영 체제에 대 한 통합 서비스를 설치 하 고 최신 상태로 유지 합니다. 지원 되는 Windows 버전을 실행 하는 게스트에 대 한 통합 서비스 업데이트는 Windows 업데이트를 통해 제공 됩니다.
    - 각 가상 머신에서 실행 되는 운영 체제는 수행 하는 역할에 따라 강화 합니다. [Windows 보안 기준](https://docs.microsoft.com/windows/device-security/windows-security-baselines)에 설명 된 기본 보안 설정 권장 사항을 사용 합니다.
    
- **보안 네트워크를 사용 합니다.** 

    가상 네트워크 어댑터를 올바른 가상 스위치에 연결 하 고 적절 한 보안 설정 및 제한을 적용 했는지 확인 합니다.
    
- **가상 하드 디스크와 스냅숏 파일을 안전한 위치에 저장 합니다.**

- **장치를 보호 합니다.** 

    가상 컴퓨터에 필요한 장치만 구성 합니다. 특정 시나리오에 필요한 경우를 제외 하 고는 프로덕션 환경에서 개별 장치 할당을 사용 하지 마십시오. 사용 하도록 설정 하는 경우 신뢰할 수 있는 공급 업체의 장치만 표시 해야 합니다. 
    
- 가상 컴퓨터 역할에 따라 적절 하 게 가상 컴퓨터 내에서 **바이러스 백신, 방화벽 및 침입 검색 소프트웨어를 구성** 합니다.

- **Windows 10 또는 Windows Server 2016 이상을 실행 하는 게스트에 대 한 가상화 기반 보안을 사용 하도록 설정 합니다.** 

    자세한 내용은 [Device Guard 배포 가이드](https://docs.microsoft.com/windows/device-security/device-guard/device-guard-deployment-guide)를 참조 하세요.
    
- **특정 작업에 필요한 경우에만 불연속 장치 할당을 사용**합니다. 

    물리적 장치를 통과 하는 특성으로 인해 장치 제조업체와 협력 하 여 보안 환경에서 사용 해야 하는지 파악 합니다.

더 안전한 환경:

- **차폐를 사용 하는 가상 컴퓨터를 배포 하 고 보호 된 패브릭에 배포 합니다.** 

    자세한 내용은 [2 세대 보안 설정](../learn-more/Generation-2-virtual-machine-security-settings-for-Hyper-V.md) 및 [보호 된 패브릭](../../../security/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms-top-node.md)을 참조 하세요.
