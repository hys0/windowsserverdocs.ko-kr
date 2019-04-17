---
title: 이후 Post-Deployment 네트워크 컨트롤러 단계
description: 이 항목에서는 Kerberos 비 네트워크 컨트롤러 Windows Server 2016 데이터 센터에 배포 인증서 구성 설명 합니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.topic: article
ms.assetid: eea0aca9-8d89-48fb-8068-fca40c90d34b
ms.author: pashort
author: shortpatti
ms.openlocfilehash: f7d6bbd50537e24f392eabde7d103c91a4f07c90
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="post-deployment-steps-for-network-controller"></a>이후 Post-Deployment 네트워크 컨트롤러 단계

네트워크 컨트롤러를 설치 하면 Kerberos 또는 비 Kerberos 배포 선택할 수 있습니다.

Non\ Kerberos 배포용 인증서를 구성 해야 합니다.

## <a name="configure-certificates-for-non-kerberos-deployments"></a>인증서 비 Kerberos 배포를 위해 구성

네트워크 컨트롤러 및 관리 클라이언트 컴퓨터 또는 가상 컴퓨터 \(VMs\) domain\에 가입 하지 않으면, 경우 다음 단계를 완료 하 여 certificate\ 기반 인증을 구성 해야 합니다.

- 네트워크 컨트롤러 컴퓨터 인증을 위한 인증서를 만듭니다. 인증서 제목 DNS 이름 네트워크 컨트롤러 컴퓨터 또는 VM와 동일 해야 합니다.

- 관리 클라이언트의 인증서를 만듭니다. 네트워크 컨트롤러가이 인증서 신뢰할 수 있어야 합니다.
  
- 네트워크 컨트롤러 컴퓨터 또는 VM 인증서를 등록 합니다. 인증서는 다음 조건을 충족 해야 합니다.
  
    -  서버 인증 목적 및 클라이언트 인증 목적 키 사용 향상 \(EKU\) 또는 응용 프로그램 정책을 확장 구성 합니다. 서버 인증을 위한 개체 식별자 1.3.6.1.5.5.7.3.1입니다. 클라이언트 인증 개체 식별자 1.3.6.1.5.5.7.3.2입니다.
  
    - 인증서 제목을 해결 해야 합니다.
  
        - 네트워크 컨트롤러 컴퓨터 또는 네트워크 컨트롤러는 한 대의 컴퓨터 또는 VM에서 배포 하는 경우 VM의 IP 주소 합니다.

        - 네트워크 컨트롤러 여러 대의 컴퓨터, 여러 Vm 또는 둘 다에 배포 되는 경우 나머지 IP 주소입니다.
  
    - 이 인증서 모든 나머지 클라이언트 신뢰할 수 있어야 합니다. 인증서의 소프트웨어 부하 분산 (SLB) 멀티플렉서 (MUX), 네트워크 컨트롤러에서 관리 하는 southbound 호스트 컴퓨터 에서도 신뢰할 수 있어야 합니다.
  
    - 인증서를 인증 기관 (캐나다)에서 등록할 수 있습니다 또는 자체 서명된 인증서를 될 수 있습니다. 자체 서명된 인증서 프로덕션 배포용 권장 하지 않음 하지만 테스트 랩 환경에 사용할 수 있습니다.
  
    - 모든 네트워크 컨트롤러 노드에서 여 동일한 인증서를 제공 해야 합니다. 한 노드에서 인증서를 만든 후 인증서 키가 있는 개인 내보내고 다른 노드에서 가져올 수 있습니다.

자세한 내용은 참조 [네트워크 컨트롤러](Network-Controller.md)합니다.
