---
title: 차폐 Vm-VM 실딩 도우미 VHD 준비
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: 0e3414cf-98ca-4e91-9e8d-0d7bce56033b
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 7984d1c965c15f7d8c3f3abfdc99f01e3adc215f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403429"
---
# <a name="shielded-vms---preparing-a-vm-shielding-helper-vhd"></a>차폐 Vm-VM 실딩 도우미 VHD 준비

>적용 대상: Windows server 2019, Windows Server (반기 채널), Windows Server 2016

> [!IMPORTANT]
> 이러한 절차를 시작 하기 전에 Windows Server 2016에 대 한 최신 누적 업데이트를 설치 했거나 최신 Windows 10 [원격 서버 관리 도구](https://www.microsoft.com/en-us/download/details.aspx?id=45520)를 사용 하 고 있는지 확인 합니다. 그렇지 않으면 프로시저가 작동 하지 않습니다. 

이 섹션에서는 기존 Vm을 보호 된 Vm으로 변환 하는 작업을 지원 하기 위해 호스팅 서비스 공급자가 수행 하는 단계를 간략하게 설명 합니다.

이 항목이 보호 된 Vm을 배포 하는 전체 프로세스에 어떻게 부합 하는지 이해 하려면 [보호 된 호스트 및 보호 된 vm에 대 한 서비스 공급자 구성 단계 호스팅](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)을 참조 하세요.

## <a name="which-vms-can-be-shielded"></a>보호할 수 있는 Vm은 무엇 인가요?

기존 Vm에 대 한 보호 프로세스는 다음 필수 구성 요소를 충족 하는 Vm에 대해서만 사용할 수 있습니다.

- 게스트 OS는 Windows Server 2012, 2012 R2, 2016 또는 반기 채널 릴리스입니다. 기존 Linux Vm을 보호 된 Vm으로 변환할 수 없습니다.
- VM은 2 세대 VM (UEFI 펌웨어)입니다.
- VM은 OS 볼륨에 차이점 보관용 디스크를 사용 하지 않습니다.

## <a name="prepare-helper-vhd"></a>도우미 VHD 준비

1.  Hyper-v가 설치 된 컴퓨터와 원격 서버 관리 도구 기능 **차폐 Vm 도구가** 설치 된 컴퓨터에서 빈 VHDX로 새로운 2 세대 VM을 만들고 WINDOWS server ISO 설치 미디어를 사용 하 여 windows server 2016을 설치 합니다. 이 VM은 보호 되지 않아야 하 고 Server Core 또는 데스크톱 환경에서 서버를 실행 해야 합니다.

    > [!IMPORTANT]
    > VM 실딩 도우미 VHD는 호스팅 서비스 공급자에서 만든 템플릿 디스크와 관련 **되지 않아야** 합니다. [보호 된 vm 템플릿을 만듭니다](guarded-fabric-create-a-shielded-vm-template.md). 템플릿 디스크를 다시 사용 하는 경우 두 디스크의 GPT 디스크 식별자가 동일 하기 때문에 보호 프로세스 중에 디스크 서명 충돌이 발생 합니다. 새 (빈) VHD를 만든 다음 ISO 설치 미디어를 사용 하 여 Windows Server 2016을 설치 하면이 문제를 방지할 수 있습니다.

2.  VM을 시작 하 고, 모든 설정 단계를 완료 하 고, 바탕 화면에 로그인 합니다. VM이 작동 중 상태 인지 확인 한 후 VM을 종료 합니다.

3.  관리자 권한 Windows PowerShell 창에서 다음 명령을 실행 하 여 이전에 만든 VHDX를 VM 실딩 도우미 디스크로 준비 합니다. 사용자 환경에 맞는 경로를 사용 하 여 경로를 업데이트 합니다.

    ```powershell
    Initialize-VMShieldingHelperVHD -Path 'C:\VHD\shieldingHelper.vhdx'
    ```

4.  명령이 성공적으로 완료 되 면 VHDX를 VMM 라이브러리 공유에 복사 합니다. 1 단계에서 VM을 다시 시작 **하지** 않습니다. 이렇게 하면 도우미 디스크가 손상 됩니다.

5.  이제 Hyper-v의 1 단계에서 만든 VM을 삭제할 수 있습니다.

## <a name="configure-vmm-host-guardian-server-settings"></a>VMM 호스트 보호 서버 설정 구성

VMM 콘솔에서 설정 창을 열고 **일반**에서 **보호자 서비스 설정을 호스트** 합니다. 이 창의 맨 아래에는 도우미 VHD의 위치를 구성 하는 필드가 있습니다. 찾아보기 단추를 사용 하 여 라이브러리 공유에서 VHD를 선택 합니다. 공유에 디스크가 표시 되지 않으면 VMM에서 라이브러리를 수동으로 새로 고쳐 표시 해야 할 수도 있습니다.

![VMM-호스트 보호자 서비스 설정](../media/Guarded-Fabric-Shielded-VM/guarded-host-vmm-hgs-settings-01.png)

## <a name="see-also"></a>참조

- [보호 된 호스트 및 보호 된 Vm에 대 한 호스팅 서비스 공급자 구성 단계](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)
- [보호된 패브릭 및 보호된 VM](guarded-fabric-and-shielded-vms-top-node.md)
