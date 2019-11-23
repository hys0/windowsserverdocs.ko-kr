---
title: 네트워크 컨트롤러에 대한 배포 후 단계
description: 이 항목에서는 Windows Server 2016 Datacenter에서 네트워크 컨트롤러의 Kerberos가 아닌 배포에 대 한 인증서 구성 지침을 제공 합니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-sdn
ms.topic: article
ms.assetid: eea0aca9-8d89-48fb-8068-fca40c90d34b
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 3f95d2884a808239c1d171eecbc983e26e799102
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71355621"
---
# <a name="post-deployment-steps-for-network-controller"></a>네트워크 컨트롤러에 대한 배포 후 단계

네트워크 컨트롤러를 설치할 때 Kerberos 또는 Kerberos 이외의 배포를 선택할 수 있습니다.

\-Kerberos가 아닌 배포의 경우 인증서를 구성 해야 합니다.

## <a name="configure-certificates-for-non-kerberos-deployments"></a>Kerberos가 아닌 배포에 대 한 인증서 구성

컴퓨터 또는 가상 컴퓨터가 네트워크 컨트롤러에 대 한 Vm\) \(하 고 관리 클라이언트가 도메인\-가입 되어 있지 않으면 다음 단계를 완료 하 여 인증서\-기반 인증을 구성 해야 합니다.

- 컴퓨터 인증용 네트워크 컨트롤러에서 인증서를 만듭니다. 인증서 주체 이름은 네트워크 컨트롤러 컴퓨터 또는 VM의 DNS 이름과 동일 해야 합니다.

- 관리 클라이언트에서 인증서를 만듭니다. 이 인증서는 네트워크 컨트롤러에서 신뢰할 수 있어야 합니다.
  
- 네트워크 컨트롤러 컴퓨터 또는 VM에 인증서를 등록 합니다. 인증서는 다음 요구 사항을 충족 해야 합니다.
  
    -  서버 인증 목적 및 클라이언트 인증 용도는 EKU\) 또는 응용 프로그램 정책 확장 \(확장 된 키 사용에서 구성 해야 합니다. 서버 인증에 대 한 개체 식별자는 1.3.6.1.5.5.7.3.1입니다. 클라이언트 인증에 대 한 개체 식별자는 1.3.6.1.5.5.7.3.2입니다.
  
    - 인증서 주체 이름은 다음으로 확인 되어야 합니다.
  
        - 네트워크 컨트롤러를 단일 컴퓨터 또는 VM에 배포 하는 경우 네트워크 컨트롤러 컴퓨터 또는 VM의 IP 주소입니다.

        - 네트워크 컨트롤러를 여러 컴퓨터, 여러 Vm 또는 둘 다에 배포 하는 경우 REST IP 주소입니다.
  
    - 이 인증서는 모든 REST 클라이언트에서 신뢰할 수 있어야 합니다. 또한 SLB (소프트웨어 부하 분산) 멀티플렉서 (MUX) 및 네트워크 컨트롤러에서 관리 하는 southbound 호스트 컴퓨터에서 인증서를 신뢰할 수 있어야 합니다.
  
    - 인증서는 CA (인증 기관)에서 등록 하거나 자체 서명 된 인증서 일 수 있습니다. 자체 서명 된 인증서는 프로덕션 배포에는 권장 되지 않지만 테스트 랩 환경에는 사용할 수 있습니다.
  
    - 모든 네트워크 컨트롤러 노드에서 동일한 인증서를 프로 비전 해야 합니다. 한 노드에서 인증서를 만든 후 개인 키를 사용 하 여 인증서를 내보내고 다른 노드에 가져올 수 있습니다.

자세한 내용은 [네트워크 컨트롤러](Network-Controller.md)를 참조하세요.
