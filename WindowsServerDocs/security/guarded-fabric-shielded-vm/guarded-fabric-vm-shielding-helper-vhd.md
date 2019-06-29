---
title: 보호 된 Vm-VM 실딩 도우미 VHD 준비
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 0e3414cf-98ca-4e91-9e8d-0d7bce56033b
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 81e6ed7950fe13c5bed4a3f8850d64e7185b8ddd
ms.sourcegitcommit: 63926404009f9e1330a4a0aa8cb9821a2dd7187e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/29/2019
ms.locfileid: "67469637"
---
# <a name="shielded-vms---preparing-a-vm-shielding-helper-vhd"></a>보호 된 Vm-VM 실딩 도우미 VHD 준비

>적용 대상: Windows Server, Windows Server 2016, Windows Server (반기 채널) 2019

> [!IMPORTANT]
> 이러한 절차를 시작 하기 전에 Windows Server 2016에 대 한 최신 누적 업데이트를 설치 하거나 최신 Windows 10을 사용 하는 확인 [원격 서버 관리 도구](https://www.microsoft.com/en-us/download/details.aspx?id=45520)합니다. 그렇지 않으면 절차에서는 작동 하지 않습니다. 

이 섹션에서는 보호 된 Vm에 기존 Vm을 변환 하는 것에 대 한 지원을 사용 하도록 설정 하는 호스팅 서비스 공급자가 수행 하는 단계를 간략하게 설명 합니다.

이 항목에서는 보호 된 Vm을 배포 하는 전체 과정에 얼마나 적합 한지 이해 하려면 [호스팅 서비스 공급자 구성 단계에 대 한 보호 된 호스트 및 차폐 Vm](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)합니다.

## <a name="which-vms-can-be-shielded"></a>Vm이 보호 수 있습니까?

기존 Vm에 대 한 보호 프로세스는 다음 필수 구성 요소를 충족 하는 Vm에 대 한 제공만 됩니다.

- 게스트 OS는 Windows Server 2012, 2012 R2, 2016, 또는 반기 채널 릴리스 합니다. 보호 된 Vm에 기존 Linux Vm은 변환할 수 없습니다.
- VM이 2 세대 VM (UEFI 펌웨어)
- VM의 OS 볼륨에 대 한 차이점 보관용 디스크를 사용 하지 않습니다.

## <a name="prepare-helper-vhd"></a>도우미 VHD 준비

1.  Hyper-v 및 원격 서버 관리 도구 기능을 사용 하 여 머신에 **보호 된 VM 도구** 새로운 2 세대를 만드는 설치에 Windows Server ISO 설치를 사용 하 여 Windows Server 2016 설치를 빈 VHDX를 사용 하 여 VM 미디어입니다. 이 VM 보호 해야 하 고 데스크톱 환경 포함 Server Core 또는 Server를 실행 해야 합니다.

    > [!IMPORTANT]
    > VM 실딩 도우미 VHD **안** 에서 만든 템플릿 디스크와 관련이 있을 [호스팅 서비스 공급자에는 보호 된 VM 템플릿을 만듭니다](guarded-fabric-create-a-shielded-vm-template.md)합니다. 템플릿 디스크를 다시 사용 하면 됩니다 보호 프로세스 동안 디스크 서명을 충돌이 때문 두 디스크 모두 동일한 GPT 디스크 식별자. 새 (비어 있음) VHD를 만들고 ISO 설치 미디어를 사용 하 여 Windows Server 2016을 설치 하 여이 방지할 수 있습니다.

2.  VM을 시작 하 고 모든 설치 단계를 완료 데스크톱에 로그인 합니다. VM이 작동 상태를 확인 한 후 VM을 종료 합니다.

3.  관리자 권한 Windows PowerShell 창에서 이전에 만든 VM 실딩 도우미 디스크를 VHDX를 준비 하려면 다음 명령을 실행 합니다. 사용자 환경에 대 한 올바른 경로 사용 하 여 경로 업데이트 합니다.

    ```powershell
    Initialize-VMShieldingHelperVHD -Path 'C:\VHD\shieldingHelper.vhdx'
    ```

4.  명령을 성공적으로 완료 되 면을 VMM 라이브러리 공유 VHDX를 복사 합니다. **그렇지 않은** 1 단계에서 VM을 다시 시작 합니다. 이렇게 하면 도우미 디스크를 손상 됩니다.

5.  이제 Hyper-v의 1 단계에서 VM을 삭제할 수 있습니다.

## <a name="configure-vmm-host-guardian-server-settings"></a>VMM 호스트 보호자 서버 설정 구성

VMM 콘솔에서 설정 창을 열고 차례로 **호스트 보호 서비스 설정** 아래에서 **일반**합니다. 이 창의 맨 아래에 필드 도우미 VHD의 위치를 구성할 수 있습니다. 찾아보기 단추를 사용 하 여 라이브러리 공유에서 VHD를 선택 합니다. 공유에서 디스크에 표시 되지 않으면 수동으로 표시에 대 한 VMM에서 라이브러리를 새로 고치려면 해야 합니다.

![VMM 호스트 보호 서비스 설정](../media/Guarded-Fabric-Shielded-VM/guarded-host-vmm-hgs-settings-01.png)

## <a name="see-also"></a>참조

- [보호 된 호스트 및 차폐 Vm 호스팅 서비스 공급자 구성 단계](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)
- [보호된 패브릭 및 보호된 VM](guarded-fabric-and-shielded-vms-top-node.md)
