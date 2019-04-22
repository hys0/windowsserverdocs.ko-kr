---
title: 보호 된 호스트 필수 조건
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 5f2c3ec4b2c434ea945d86c4b1593e2e416a5123
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59819234"
---
# <a name="prerequisites-for-guarded-hosts"></a>보호 된 호스트에 대 한 필수 구성 요소

>적용 대상: Windows Server, Windows Server 2016, Windows Server (반기 채널) 2019

선택한 증명 모드에 대 한 호스트 필수 조건을 검토 하 고 보호 된 호스트를 추가 하려면 다음 단계를 클릭 합니다.

## <a name="tpm-trusted-attestation"></a>TPM 신뢰할 수 있는 증명

TPM 모드를 사용 하 여 보호 된 호스트에는 다음 필수 조건을 충족 해야 합니다.

-   **하드웨어**: 호스트 초기 배포에 필요 합니다. Hyper-v 실시간 마이그레이션 보호 된 vm을 테스트 하려면 두 개 이상의 호스트 해야 합니다.

    호스트가 있어야 합니다.
    
    - IOMMU 및 두 번째 수준 주소 변환 (SLAT)
    - TPM 2.0
    - UEFI 2.3.1 이상
    - UEFI (BIOS 또는 "레거시" 모드)를 사용 하 여 부팅 하도록 구성
    - 보안 부팅 사용 함
        
-   **운영 체제**: Windows Server 2016 Datacenter edition 이상

    > [!IMPORTANT]
    > 설치 해야 합니다 [최신 누적 업데이트](https://support.microsoft.com/help/4000825/windows-10-and-windows-server-2016-update-history)합니다.  

-   **역할 및 기능**: Hyper-v 역할 및 호스트 보호 Hyper-v 지원 기능입니다. 호스트 보호 Hyper-v 지원 기능은 Windows server Datacenter edition에서 사용할 수만 있습니다. 

> [!WARNING]
> 호스트 보호 Hyper-v 지원 기능에는 일부 장치와 호환 되지 않을 수 있는 코드 무결성 보호를 가상화 기반 수 있습니다. 이 기능을 활성화 하기 전에 랩에이 구성을 테스트 하는 것이 좋습니다. 이렇게 하지 않으면 데이터 손실이나 블루 스크린 오류(중지 오류라고도 함)를 비롯한 예기치 않은 실패가 발생할 수 있습니다. 자세한 내용은 [코드 무결성에 대 한 Windows Server 가상화 기반 보호를 사용 하 여 호환 되는 하드웨어](guarded-fabric-compatible-hardware-with-virtualization-based-protection-of-code-integrity.md)합니다.

**다음 단계:** 
>[!div class="nextstepaction"]
[TPM 정보 캡처](guarded-fabric-tpm-trusted-attestation-capturing-hardware.md)

## <a name="host-key-attestation"></a>호스트 키 증명

호스트 키 증명을 사용 하 여 보호 된 호스트에는 다음 필수 조건을 충족 해야 합니다.

- **하드웨어**: Windows Server 2019를 사용 하 여 시작 하는 Hyper-v를 실행할 수 있는 모든 서버
- **운영 체제**: Windows Server 2019 Datacenter edition
- **역할 및 기능**: Hyper-v 역할 및 호스트 보호 Hyper-v 지원 기능 

호스트를 도메인 또는 작업 그룹에 가입할 수 있습니다. 

호스트 키 증명에 대 한 HGS 서버 2019 Windows를 실행 하 고 v2 증명을 사용 하 여 운영 합니다. 자세한 내용은 참조 [HGS 필수 구성 요소](guarded-fabric-prepare-for-hgs.md#prerequisites)합니다. 

**다음 단계:** 
>[!div class="nextstepaction"]
[키 쌍 만들기](guarded-fabric-create-host-key.md)

## <a name="admin-trusted-attestation"></a>관리자-신뢰할 수 있는 증명

>[!IMPORTANT]
>관리자-신뢰할 수 있는 증명 (AD 모드)는 Windows Server 2019로 시작 하는 사용 되지 않습니다. TPM 증명 수 없는 환경에 대 한 구성 [호스트 키 증명](#host-key-attestation)합니다. 호스트 키 증명 AD 모드에 유사한 보증을 제공 하며 간단 하 게 설정 합니다. 

Hyper-v 호스트에는 AD 모드는 다음과 같은 전제 조건을 충족 해야 합니다.

-   **하드웨어**: Windows Server 2016 Hyper-v 시작 부분을 실행할 수 있는 모든 서버. 호스트 초기 배포에 필요 합니다. 보호 된 Vm에 대 한 Hyper-v 실시간 마이그레이션을 테스트 하려면 두 개 이상의 호스트 해야 합니다.

-   **운영 체제**: Windows Server 2016 Datacenter edition

    > [!IMPORTANT]
    > 설치 합니다 [최신 누적 업데이트](https://support.microsoft.com/help/4000825/windows-10-and-windows-server-2016-update-history)합니다.

-   **역할 및 기능**: Hyper-v 역할 및 Windows Server 2016 Datacenter edition에서 사용할 수 있는 호스트 보호 Hyper-v 지원 기능을 합니다. 

> [!WARNING]
> 호스트 보호 Hyper-v 지원 기능에는 일부 장치와 호환 되지 않을 수 있는 코드 무결성 보호를 가상화 기반 수 있습니다. 이 기능을 활성화 하기 전에 랩에이 구성을 테스트 하는 것이 좋습니다. 이렇게 하지 않으면 데이터 손실이나 블루 스크린 오류(중지 오류라고도 함)를 비롯한 예기치 않은 실패가 발생할 수 있습니다. 자세한 내용은 [코드 무결성에 대 한 Windows Server 2016 가상화 기반 보호를 사용 하 여 호환 되는 하드웨어](guarded-fabric-compatible-hardware-with-virtualization-based-protection-of-code-integrity.md)합니다.

**다음 단계:** 
>[!div class="nextstepaction"]
[보안 그룹의 보호 된 호스트를 배치 합니다.](guarded-fabric-admin-trusted-attestation-creating-a-security-group.md)