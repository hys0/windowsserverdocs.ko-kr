---
title: 네트워크 컨트롤러에 대한 배포 후 단계
description: 이 항목에서는 Windows Server 2016 Datacenter의 네트워크 컨트롤러의 비-Kerberos 배포에 대 한 인증서 구성 지침을 제공합니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.topic: article
ms.assetid: eea0aca9-8d89-48fb-8068-fca40c90d34b
ms.author: pashort
author: shortpatti
ms.openlocfilehash: f7d6bbd50537e24f392eabde7d103c91a4f07c90
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59871084"
---
# <a name="post-deployment-steps-for-network-controller"></a>네트워크 컨트롤러에 대한 배포 후 단계

네트워크 컨트롤러를 설치할 때에 Kerberos 또는 비-Kerberos 배포를 선택할 수 있습니다.

에 대 한 비\-Kerberos 배포 인증서를 구성 해야 합니다.

## <a name="configure-certificates-for-non-kerberos-deployments"></a>비-Kerberos 배포에 대 한 인증서를 구성 합니다.

경우 컴퓨터 또는 가상 컴퓨터 \(Vm\) 에 대해 네트워크 컨트롤러와 관리 클라이언트 도메인\-에 가입 된 경우 인증서를 구성 해야\-다음을 완료 하 여 기반 인증 단계입니다.

- 컴퓨터 인증에 대 한 네트워크 컨트롤러에서 인증서를 만듭니다. 인증서 주체 이름은 네트워크 컨트롤러 컴퓨터 또는 VM의 DNS 이름과 동일 해야 합니다.

- 관리 클라이언트에서 인증서를 만듭니다. 네트워크 컨트롤러에서이 인증서를 신뢰 해야 합니다.
  
- 네트워크 컨트롤러 컴퓨터 또는 VM에서 인증서를 등록 합니다. 인증서에는 다음 요구 사항을 충족 해야 합니다.
  
    -  향상 된 키 용도에 서버 인증 용도로 및 클라이언트 인증 용도의 모두를 구성 해야 합니다 \(EKU\) 또는 응용 프로그램 정책 확장 합니다. 서버 인증에 대 한 개체 식별자 1.3.6.1.5.5.7.3.1 됩니다. 클라이언트 인증에 대 한 개체 식별자는 1.3.6.1.5.5.7.3.2입니다.
  
    - 인증서 주체 이름이 확인 해야 합니다.
  
        - IP 주소는 네트워크 컨트롤러 컴퓨터 또는 VM을 단일 컴퓨터 또는 VM에 네트워크 컨트롤러 배포 하는 경우입니다.

        - 여러 컴퓨터, 여러 Vm 또는 둘 다에 네트워크 컨트롤러 배포 하는 경우 REST IP 주소입니다.
  
    - 모든 REST 클라이언트에서이 인증서를 신뢰 해야 합니다. 또한 소프트웨어 부하 분산 (SLB) 멀티플렉서 (MUX)와 네트워크 컨트롤러에서 관리 하는 southbound 호스트 컴퓨터에서 인증서를 신뢰 합니다.
  
    - 인증서는 인증 기관 (CA)에서 등록할 수 있습니다 또는 자체 서명 된 인증서 일 수 있습니다. 자체 서명 된 인증서는 프로덕션 배포에 권장 되지 않습니다 하지만 테스트 랩 환경에 적합 합니다.
  
    - 모든 네트워크 컨트롤러 노드에 동일한 인증서를 프로 비전 되어야 합니다. 노드 하나에서 인증서를 만든 후 개인 키가 있는 인증서를 내보낼 수 있으며 다른 노드에서 가져옵니다.

자세한 내용은 [네트워크 컨트롤러](Network-Controller.md)를 참조하세요.
