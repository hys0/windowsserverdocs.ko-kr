---
title: HGS 필수 구성 요소 검토
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: f4b4d1a8-bf6d-4881-9150-ddeca8b48038
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 9a668a39990b79862b99c2c7d9aeaf6540fa376d
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447370"
---
# <a name="review-prerequisites-for-the-host-guardian-service"></a>호스트 보호 서비스에 대 한 필수 구성 요소 검토

>적용 대상: Windows Server, Windows Server 2016, Windows Server (반기 채널) 2019


이 항목에서는 HGS 필수 구성 요소 및 HGS 배포를 준비 하는 초기 단계를 설명 합니다.

## <a name="prerequisites"></a>사전 요구 사항 

-   **하드웨어**: HGS 물리적 컴퓨터나 가상 컴퓨터에서 실행할 수 있지만 물리적 컴퓨터를 사용 하는 것이 좋습니다.

    HGS (가용성)에 대 한 3 개 노드 실제 클러스터로 실행 하려는 경우에 세 명의 물리적 서버가 있어야 합니다. (클러스터링에 대 한 모범 사례로, 3 명의 서버 있어야 매우 유사한 하드웨어 합니다.)
  
-   **운영 체제**: Windows Server 2019 Standard 또는 Datacenter edition 운영의 호스트 키 증명 필요 [v2 증명](guarded-fabric-tpm-trusted-attestation-capturing-hardware.md#versioned-attestation-policies)합니다. TPM 기반 증명에 대 한 Windows Server 2019 또는 Windows Server 2016, Standard 또는 Datacenter edition HGS 실행할 수 있습니다.

-   **서버 역할**: 호스트 보호 서비스 및 서버 역할을 지원 합니다.

-   **패브릭 (호스트) 도메인에 대 한 사용 권한/권한이 구성**: 패브릭 (호스트) 도메인 및 HGS 도메인 간에 DNS 전달을 구성 해야 합니다. 
    
## <a name="upgrading-hgs"></a>HGS를 업그레이드합니다.

HGS를 이미 배포한 하 고 해당 운영 체제를 업그레이드 하려고 할 경우에 따라를 [업그레이드 지침](guarded-fabric-upgrade-to-2019.md) 최신 os HGS 및 Hyper-v 서버를 업그레이드 합니다.

## <a name="next-step"></a>다음 단계

> [!div class="nextstepaction"]
> [HGS에 대 한 인증서를 가져오려면](guarded-fabric-obtain-certs.md)