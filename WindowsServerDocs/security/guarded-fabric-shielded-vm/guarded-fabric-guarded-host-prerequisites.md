---
title: 보호 된 호스트 필수 조건
ms.custom: na
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 8a9273eef906130b11b98148cf1e84f7e18812b0
ms.sourcegitcommit: 06ae7c34c648538e15c4d9fe330668e7df32fbba
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/05/2020
ms.locfileid: "78371465"
---
# <a name="prerequisites-for-guarded-hosts"></a>보호 된 호스트에 대 한 필수 구성 요소

>적용 대상: Windows Server 2019, Windows Server (반기 채널), Windows Server 2016

선택한 증명 모드의 호스트 필수 구성 요소를 검토 한 후 다음 단계를 클릭 하 여 보호 된 호스트를 추가 합니다.

## <a name="tpm-trusted-attestation"></a>TPM에서 신뢰할 수 있는 증명

TPM 모드를 사용 하는 보호 된 호스트는 다음 필수 구성 요소를 충족 해야 합니다.

-   **하드웨어**: 초기 배포에는 호스트가 하나 필요 합니다. 보호 된 Vm에 대 한 Hyper-v 실시간 마이그레이션을 테스트 하려면 둘 이상의 호스트가 있어야 합니다.

    호스트에는 다음이 있어야 합니다.
    
    - IOMMU 및 두 번째 수준 주소 변환 (SLAT)
    - TPM 2.0
    - UEFI 2.3.1 이상
    - UEFI (BIOS 또는 "레거시" 모드 아님)를 사용 하 여 부팅 하도록 구성 됨
    - 보안 부팅 사용
        
-   **운영**체제: Windows Server 2016 Datacenter edition 이상

    > [!IMPORTANT]
    > [최신 누적 업데이트](https://support.microsoft.com/help/4000825/windows-10-and-windows-server-2016-update-history)를 설치 했는지 확인 합니다.  

-   **역할 및 기능**: hyper-v 역할 및 호스트 보호자 hyper-v 지원 기능. 호스트 보호 Hyper-v 지원 기능은 Windows Server Datacenter edition 에서만 사용할 수 있습니다. 

> [!WARNING]
> 호스트 보호자 Hyper-v 지원 기능을 사용 하면 일부 장치와 호환 되지 않을 수 있는 코드 무결성을 가상화 기반으로 보호할 수 있습니다. 이 기능을 사용 하도록 설정 하기 전에 랩에서이 구성을 테스트 하는 것이 좋습니다. 이렇게 하지 않으면 데이터 손실이나 블루 스크린 오류(중지 오류라고도 함)를 비롯한 예기치 않은 실패가 발생할 수 있습니다. 자세한 내용은 [코드 무결성에 대 한 Windows Server 가상화 기반 보호와 호환 되는 하드웨어](guarded-fabric-compatible-hardware-with-virtualization-based-protection-of-code-integrity.md)를 참조 하세요.

**다음 단계:** 
> [!div class="nextstepaction"]
> [TPM 정보 캡처](guarded-fabric-tpm-trusted-attestation-capturing-hardware.md)

## <a name="host-key-attestation"></a>호스트 키 증명

호스트 키 증명을 사용 하는 보호 된 호스트는 다음 필수 구성 요소를 충족 해야 합니다.

- **하드웨어**: Windows server 2019부터 hyper-v를 실행할 수 있는 모든 서버
- **운영**체제: Windows Server 2019 Datacenter edition
- **역할 및 기능**: hyper-v 역할 및 호스트 보호자 hyper-v 지원 기능 

호스트는 도메인 또는 작업 그룹에 가입할 수 있습니다. 

호스트 키 증명의 경우 HGS는 Windows Server 2019를 실행 하 고 v2 증명을 사용 하 여 작동 해야 합니다. 자세한 내용은 [HGS 필수 구성 요소](guarded-fabric-prepare-for-hgs.md#prerequisites)를 참조 하세요. 

**다음 단계:** 
> [!div class="nextstepaction"]
> [키 쌍 만들기](guarded-fabric-create-host-key.md)

## <a name="admin-trusted-attestation"></a>관리자가 신뢰할 수 있는 증명

>[!IMPORTANT]
>관리자가 신뢰할 수 있는 증명 (AD 모드)은 Windows Server 2019부터 사용 되지 않습니다. TPM 증명을 사용할 수 없는 환경의 경우 [호스트 키 증명](#host-key-attestation)을 구성 합니다. 호스트 키 증명은 AD 모드와 비슷한 보증을 제공 하 고 설정 하는 것이 더 간단 합니다. 

Hyper-v 호스트는 AD 모드에 대해 다음과 같은 필수 조건을 충족 해야 합니다.

-   **하드웨어**: Windows server 2016부터 hyper-v를 실행할 수 있는 모든 서버. 초기 배포에는 호스트가 하나 필요 합니다. 보호 된 Vm에 대 한 Hyper-v 실시간 마이그레이션을 테스트 하려면 둘 이상의 호스트가 필요 합니다.

-   **운영**체제: Windows Server 2016 Datacenter edition

    > [!IMPORTANT]
    > [최신 누적 업데이트](https://support.microsoft.com/help/4000825/windows-10-and-windows-server-2016-update-history)를 설치 합니다.

-   **역할 및 기능**: hyper-v 역할 및 호스트 보호자 hyper-v 지원 기능-Windows Server 2016 Datacenter edition 에서만 사용할 수 있습니다. 

> [!WARNING]
> 호스트 보호자 Hyper-v 지원 기능을 사용 하면 일부 장치와 호환 되지 않을 수 있는 코드 무결성을 가상화 기반으로 보호할 수 있습니다. 이 기능을 사용 하도록 설정 하기 전에 랩에서이 구성을 테스트 하는 것이 좋습니다. 이렇게 하지 않으면 데이터 손실이나 블루 스크린 오류(중지 오류라고도 함)를 비롯한 예기치 않은 실패가 발생할 수 있습니다. 자세한 내용은 [코드 무결성에 대 한 Windows Server 2016 가상화 기반 보호와 호환 되는 하드웨어](guarded-fabric-compatible-hardware-with-virtualization-based-protection-of-code-integrity.md)를 참조 하세요.

**다음 단계:** 
> [!div class="nextstepaction"]
> [보호 된 호스트를 보안 그룹에 두기](guarded-fabric-admin-trusted-attestation-creating-a-security-group.md)