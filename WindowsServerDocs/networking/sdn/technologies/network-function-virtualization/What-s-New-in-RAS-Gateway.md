---
title: RAS 게이트웨이의 새로운 기능
description: 다중 테 넌 트, Windows Server 2016에서 프로토콜 BGP (Border Gateway) 가능 라우터는 소프트웨어 기반 RAS 게이트웨이의 새 기능에 알아보려면이 항목을 사용할 수 있습니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 709cb192-313a-47b5-954e-eb5f6fee51a7
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 5cc7d8bab3f2783750dbd723da745b1df3c2e462
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59863024"
---
# <a name="whats-new-in-ras-gateway"></a>RAS 게이트웨이의 새로운 기능

>적용 대상: Windows Server (반기 채널), Windows Server 2016

다중 테 넌 트, Windows Server 2016에서 프로토콜 BGP (Border Gateway) 가능 라우터는 소프트웨어 기반 RAS 게이트웨이의 새 기능에 알아보려면이 항목을 사용할 수 있습니다. RAS 게이트웨이 다중 테 넌 트 BGP 라우터는 클라우드 서비스 공급자 (Csp) 및 Hyper-v 네트워크 가상화를 사용 하 여 여러 테 넌 트 가상 네트워크를 호스팅하는 회사를 위해 설계 되었습니다.  
  
> [!NOTE]  
> RAS 게이트웨이 RRAS 게이트웨이; Windows Server 2012 r 2 라는 고 System Center Virtual Machine Manager에서 RAS 게이트웨이 Windows Server 게이트웨이 이름은입니다.  
  
이 항목에는 다음 섹션이 수록되어 있습니다.  
  
-   [사이트 간 연결 옵션](#bkmk_s2s)  
  
-   [게이트웨이 풀](#bkmk_pools)  
  
-   [게이트웨이 풀 확장성](#bkmk_gps)  
  
-   [M + N 게이트웨이 풀 중복성](#bkmk_m)  
  
-   [경로 Reflector](#bkmk_rr)  
  
## <a name="bkmk_s2s"></a>사이트 간 연결 옵션  
RAS 게이트웨이 이제 세 가지 유형의 VPN 사이트 간 연결을 지원합니다.  Internet Key Exchange version 2 (IKEv2) 사이트 간 가상 사설망 (VPN), (L3) 계층 3 VPN 및 라우팅 GRE (Generic Encapsulation) 터널링 합니다.  
  
Gre 방식에 대 한 자세한 내용은 참조 [Windows Server 2016에서 GRE 터널링](../../../../remote/remote-access/ras-gateway/gre-tunneling-windows-server.md)합니다.  
  
## <a name="bkmk_pools"></a>게이트웨이 풀  
Windows Server 2016에서 서로 다른 유형의 게이트웨이 풀을 만들 수 있습니다. 게이트웨이 풀 RAS 게이트웨이의 여러 인스턴스를 포함 하 고 실제 및 가상 네트워크 간에 네트워크 트래픽을 라우팅합니다. 게이트웨이 풀에 개별 게이트웨이 함수-Internet Key Exchange version 2 (IKEv2)를 수행할 수 또는 사이트 간 VPN(가상 사설망), (L3) 계층 3 VPN 및 Generic Routing Encapsulation GRE () 터널링-풀 혼합된 풀으로 역할 및 이러한 모든 함수를 수행할 수 있습니다.  
  
인프라 요구 사항에 따라 선호 하는 논리를 사용 하 여 게이트웨이 풀을 만들 수 있습니다. 예를 들어 다음과 같은 특징 중 하나에 따라 게이트웨이 풀을 만들 수 있습니다.  
  
-   터널 종류 (IKEv2 VPN, l 3 VPN GRE VPN)  
  
-   용  
  
-   중복 수준 (테 넌 트에 대 한 청구 계획에 따라 안정성)  
  
-   고객에 대 한 사용자 지정 된 분리  
  
자세한 내용은 참조 [RAS 게이트웨이 고가용성](RAS-Gateway-High-Availability.md)합니다.  
  
## <a name="bkmk_gps"></a>게이트웨이 풀 확장성  
쉽게 확장할 수 있습니다 게이트웨이 풀 위로 또는 아래로 추가 하거나 풀에서 게이트웨이 Vm을 제거 합니다. 게이트웨이 추가 또는 제거는 풀에서 제공 되는 서비스를 방해 하지 않도록 합니다. 또한 추가 및 게이트웨이 전체 풀을 제거할 수 있습니다.  
  
자세한 내용은 참조 [RAS 게이트웨이 고가용성](RAS-Gateway-High-Availability.md)합니다.  
  
## <a name="bkmk_m"></a>M + N 게이트웨이 풀 중복성  
모든 게이트웨이 풀은 M + N 중복입니다. 즉, 한 여기 ' 활성 게이트웨이 가상 컴퓨터 (Vm)의 수는 ' n ' 수가 대기 게이트웨이 Vm으로 백업 합니다. M + N 중복 RAS 게이트웨이 배포할 때 필요한 안정성 수준을 결정 하는 데 더 많은 융통성을 제공 합니다. Windows Server 2012 r 2로만 구성 옵션에는-활성 RAS 게이트웨이 VM 당 하나의 대기 RAS 게이트웨이 사용 하는 대신 이제 필요한 만큼의 대기 Vm을 구성할 수 있습니다. 네트워크 컨트롤러 게이트웨이 서비스 관리자 기능 효율적으로를 사용 하 여 대기 RAS 게이트웨이 VM 용량 활성 RAS 게이트웨이 VM 실패 하거나 연결이 끊어지는 경우 신뢰할 수 있는 장애 조치를 제공 합니다.  
  
자세한 내용은 참조 [RAS 게이트웨이 고가용성](RAS-Gateway-High-Availability.md)합니다.  
  
## <a name="bkmk_rr"></a>경로 Reflector  
프로토콜 BGP (Border Gateway) 경로 Reflector는 이제 RAS 게이트웨이와 포함 되어 있으며 라우터 간의 경로 동기화에 필요한 BGP 풀 메시 토폴로지에 대 한 대안을 제공 합니다. 풀 메시 동기화를 수행 하면 모든 BGP 라우터 라우팅 토폴로지에 있는 다른 모든 라우터 연결 해야 합니다. 그러나 경로 Reflector를 사용 하면 경로 Reflector는 연결 된 모든 다른 라우터에, BGP 클라이언트, 따라서 간소화 경로 동기화 되 고 네트워크 트래픽 감소 효과 호출 하는 유일한 라우터. 경로 Reflector 모든 경로 학습 최상의 경로 계산 하 고 최상의 경로 BGP 클라이언트를 다시 배포 합니다.  
  
Windows Server 2016 RAS 게이트웨이 VM을 여러 개를 종료 하는 개별 테 넌 트의 원격 액세스 터널을 구성할 수 있습니다. 유연성이 향상 하나의 RAS 게이트웨이 VM 만나는 수 없는 상황에 직면 하는 경우 클라우드 서비스 공급자에 대 한 모든 테 넌 트 연결의 대역폭 요구 합니다.  
  
그러나이 기능을 경로 관리의 복잡성 및 테 넌 트 원격 사이트와 클라우드 데이터 센터에서 가상 리소스 간에 경로의 유효한 동기화를 소개합니다. 각 테 넌 트 사이트는 별도 라우팅 인접 한 항목에 주소를 갖는 엔터프라이즈 완료 되 면 구성에서 더욱 복잡을 해질 여러 RAS 게이트웨이에 연결 된 테 넌 트를 제공 합니다.  
  
컨트롤이 평면에서 BGP 경로 Reflector에서는 이러한 문제를 해결 하 고 엔터프라이즈 테 넌 트에 CSP 내부 패브릭 배포를 투명 하 게 만듭니다. 다음은 BGP 경로 리플렉터 RAS 게이트웨이와 함께 포함 되어 있으며 네트워크 컨트롤러와 통합 하는 방법에 대 한 몇 가지 주요 사항입니다.  
  
-   소프트웨어 정의 네트워킹 배포에는 경로 Reflector는 RAS 게이트웨이 및 네트워크 컨트롤러 간의 제어 평면에 위치 하는 논리 엔터티입니다. 그러나 데이터 평면 라우팅에 관여 하지 않습니다.  
  
-   데이터 센터에 새 테 넌 트를 추가 하면 네트워크 컨트롤러는 자동으로 첫 번째 테 넌 트 RAS 게이트웨이 경로 Reflector로 구성 됩니다.  
  
-   각 테 넌 트는 해당 경로 Reflector를 하 고 해당 테 넌 트와 연관 된 RAS 게이트웨이 Vm 중 하나에 상주 합니다.  
  
-   테 넌 트 경로 Reflector의 모든 테 넌 트와 연관 된 RAS 게이트웨이 Vm에 대 한 경로 Reflector 처럼 작동 합니다. RAS 게이트웨이 경로 Reflector 이외의 테 넌 트 게이트웨이 경로 Reflector 클라이언트입니다. 경로 Reflector는 실제 데이터 경로 라우팅 발생할 수 있도록 모든 경로 Reflector 클라이언트 간의 경로 동기화를 수행 합니다.  
  
-   A 경로 Reflector RAS 게이트웨이는 구성에 대 한 경로 reflector 서비스를 제공 하지 않습니다.  
  
-   A 경로 Reflector는 테 넌 트 엔터프라이즈 사이트에 해당 하는 엔터프라이즈 경로 가진 네트워크 컨트롤러를 업데이트 합니다. 따라서 네트워크 컨트롤러 종단 간 데이터 경로 액세스에 대 한 테 넌 트 가상 네트워크에 필요한 Hyper-v 네트워크 가상화 정책을 구성할 수 있습니다.  
  
-   RAS 게이트웨이 경로 Reflector 기업 고객 BGP 라우팅을 사용 하 여 고객 주소 공간에, 경우 모든 해당 테 넌 트 사이트에 대 한 유일한 외부 BGP (eBGP) 환경이 있습니다. 엔터프라이즈 테 넌 트의 터널 종료 지점에 관계 없이 마찬가지입니다. 즉, 데이터 센터에 테 넌 트 사이트에 대 한 사이트 간 VPN 터널 종료 되는 RAS 게이트웨이 VM CSP에 관계 없이, 모든 테 넌 트 사이트에 대 한 피어 eBGP 경로 Reflector 있습니다.  
  
자세한 내용은 [RAS 게이트웨이 배포 아키텍처](RAS-Gateway-Deployment-Architecture.md) 의견 항목에 대 한 Task Force IETF (Internet Engineering) 요청 [RFC 4456 BGP 경로 리플렉션: 대신 전체 메시 내부 BGP (IBGP)](https://tools.ietf.org/html/rfc4456)합니다.  
  

