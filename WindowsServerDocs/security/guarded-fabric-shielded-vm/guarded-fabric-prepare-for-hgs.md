---
title: HGS 필수 구성 요소 검토
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: f4b4d1a8-bf6d-4881-9150-ddeca8b48038
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 9024557dd42ede27144bf10aa5873b6bb12d585c
ms.sourcegitcommit: 0a0a45bec6583162ba5e4b17979f0b5a0c179ab2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79322485"
---
# <a name="review-prerequisites-for-the-host-guardian-service"></a>호스트 보호자 서비스의 필수 구성 요소 검토

>적용 대상: Windows Server 2019, Windows Server (반기 채널), Windows Server 2016


이 항목에서는 hgs 필수 구성 요소 및 HGS 배포를 준비 하는 초기 단계에 대해 설명 합니다.

## <a name="prerequisites"></a>필수 조건 

-   **하드웨어**: HGS는 물리적 컴퓨터 또는 가상 컴퓨터에서 실행할 수 있지만 물리적 컴퓨터를 권장 합니다.

    사용 가능 여부에 대 한 3 개 노드 물리적 클러스터로 HGS를 실행 하려면 세 대의 물리적 서버가 있어야 합니다. (클러스터링에 대 한 모범 사례로, 세 서버의 하드웨어는 매우 유사 해야 합니다.)
  
-   **운영**체제: 호스트 키 증명을 사용 하려면 Windows Server 2019 Standard 또는 Datacenter edition에서 [v2 증명](guarded-fabric-tpm-trusted-attestation-capturing-hardware.md#versioned-attestation-policies)을 사용 해야 합니다. TPM 기반 증명의 경우 HGS는 Windows Server 2019 또는 Windows Server 2016, Standard 또는 Datacenter edition을 실행할 수 있습니다.

-   **서버 역할**: 호스트 보호 서비스 및 지원 서버 역할입니다.

-   **패브릭 (호스트) 도메인에 대 한 구성 권한/** 권한: 패브릭 (호스트) 도메인과 HGS 도메인 간에 DNS 전달을 구성 해야 합니다. 
    
## <a name="upgrading-hgs"></a>HGS 업그레이드

이미 HGS를 배포 했 고 해당 운영 체제를 업그레이드 하려는 경우 [업그레이드 지침](guarded-fabric-upgrade-to-2019.md) 에 따라 Hgs 및 hyper-v 서버를 최신 OS로 업그레이드 합니다.

## <a name="next-step"></a>다음 단계

> [!div class="nextstepaction"]
> [HGS 용 인증서 가져오기](guarded-fabric-obtain-certs.md)