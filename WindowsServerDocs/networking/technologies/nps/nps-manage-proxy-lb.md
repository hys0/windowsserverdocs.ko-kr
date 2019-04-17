---
title: NPS 프록시 서버 부하 분산
description: Windows Server 2016 및 Windows 10 VPN 특징과 기능에 대 한 자세한 내용은이 항목을 사용할 수 있습니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 528280e6-b47e-489f-b310-b257d434aa0d
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 9f00eb6575284a69358c58b36d08672cdd69dc18
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="nps-proxy-server-load-balancing"></a>NPS 프록시 서버 부하 분산

Windows Server 2016 적용 됩니다.

RADIUS(Remote Authentication Dial-In User Service) 네트워크 액세스 서버 가상 개인 네트워크 (VPN) 서버, 무선 액세스 포인트 등 인 (RADIUS) 클라이언트 연결 요청 만들고 등 NPS RADIUS 서버에 전송 합니다. 경우에 따라 NPS 서버 요청을 받을 수 너무 많은 연결 한 번에 성능이 저하 되거나 오버 발생 합니다. NPS 서버 오버 때 부하 분산 더 많은 NPS 서버 구성 하 고 네트워크에 추가 하는 것이 좋습니다. 하나 이상의 NPS 서버 채우지 방지 하기 위해 여러 NPS 서버 간에 들어오는 연결 요청 하 게 배포 부하 분산 라고 합니다.

부하 분산에 특히 유용 합니다.

- Extensible 인증 프로토콜 Transport Layer 보안 \(EAP-TLS\) 또는 Extensible 인증 프로토콜 보호를 사용 하는 조직의 \ (PEAP\)-인증을 위한 TLS 합니다. 이 인증 방법을 사용자 또는 컴퓨터 인증 클라이언트 및 서버 인증을 위한 인증서를 사용을 하기 때문에 로드 RADIUS 프록시 서버에 암호가 기반 인증 방법을 사용 되는 시기 보다 과도입니다.
- 지속적인 서비스 사용 가능성 유지 해야 하는 조직의 합니다.
- 다른 조직에 대 한 VPN 액세스 하는 인터넷 서비스 공급자 \(ISPs\) 합니다. 외부 위탁된 VPN 서비스 많은 양의 인증 교통 생성할 수 있습니다.

두 가지가 NPS 서버에 전송 연결 요청 부하 분산를 사용할 수 있습니다.

- 네트워크 액세스 서버 여러 RADIUS 서버에 연결 요청을 보낼 구성 합니다. 예를 들어, 20 무선 액세스 포인트 및 두 RADIUS 서버를 사용 하는 경우 모두 RADIUS 서버에 연결 요청을 보낼 각 액세스 지점의 구성 합니다. 잔액을 로드할 수 있으며 장애 각 네트워크 액세스 서버에 요청을 보내려면 연결의 우선 순위 지정 순서로 여러 RADIUS 서버에 대 한 액세스 서버 구성 하 여 제공할 수도 있습니다. 이 방법은 부하 분산 일반적으로 가장 많은 RADIUS 클라이언트를 배포 하지 않는 작은 조직에 대 한 것입니다.
- NPS RADIUS 프록시로 구성를 사용 하 여 여러 NPS 또는 기타 RADIUS 서버 연결 요청 잔액을 로드할 수 있습니다. 예를 들어, 100 무선 액세스 포인트, NPS 프록시 한 및 세 RADIUS 서버를 사용 하는 경우 모든 교통 NPS 프록시 보내려고 액세스 지점 수가 가장 구성할 수 있습니다. NPS 프록시 부하 분산 프록시 세 RADIUS 서버 간의 연결이 요청을 동일 하 게 배포 하를 구성 합니다. 이 방법은 부하 분산 많은 RADIUS 클라이언트 및 서버 있는 중간 크고 조직에 대 한 것입니다.

대부분의 경우 부하 분산 하는 가장 좋은 방법은 RADIUS 클라이언트 두 NPS 프록시 서버에 연결 요청 보내기를 찾아 NPS RADIUS 서버 잔액을 로드할 수 프록시 다음 구성을 구성 하는 것입니다. 이 방법은 장애 조치 및 부하 분산 프록시 NPS RADIUS 서버를 제공 합니다.

## <a name="radius-server-priority-and-weight"></a>무게 및 RADIUS 서버 우선 순위 부여

NPS 프록시 구성 과정 원격 RADIUS 서버 그룹 만들고 RADIUS 서버 각 그룹에 추가 합니다. 부하 분산를 구성 원격 RADIUS 서버 그룹에 따라 여러 개 RADIUS 서버가 있어야 합니다. 그룹 구성원을 추가 하는 동안 또는 그룹 구성원 RADIUS 서버 만든 후 부하 분산 탭에서 다음 항목을 구성 하는 추가 RADIUS 서버 대화 상자에 액세스할 수 있습니다.

- **우선 순위 부여**합니다. 우선 순위 지정 프록시 서버 NPS RADIUS 서버의 중요성 순서 합니다. 우선 순위 1, 2, 3 등이 값을 할당 되어야 합니다. 낮게 수, 높은 우선 순위 프록시 NPS RADIUS 서버에 제공 합니다. 예를 들어, RADIUS 서버 높은 우선 순위 1 할당 되 면 NPS 프록시 연결 요청을 보냅니다 RADIUS 서버 먼저; 우선 순위 1 서버를 사용할 수 없는 경우 NPS RADIUS 서버 우선 순위 2 등에 연결 요청을 보냅니다. 여러 RADIUS 서버 동일한 우선 순위 지정 하 고 무게 설정을 사용 하 여 서로 잔액을 로드할 수 있습니다.

- **무게**합니다. 이 무게 설정을 개수 연결을 확인 하려면 각 보내려면 요청 NPS 사용 하는 그룹 구성원에 동일한 우선 순위 때 회원을 그룹화 합니다. 무게 설정을 100, 1과 할당 되어야 하며 값은 100% 비율로 나타냅니다. 예를 들어 원격 RADIUS 서버 그룹 두 회원 우선 순위 1 및 50 무게 등급이 있는 둘 다에 포함 되어, NPS 프록시 50%의 각 RADIUS 서버에 연결 요청을 전달 합니다.

- **고급 설정**합니다. 이러한 장애 설정을 NPS RADIUS 서버 원격를 사용할 수 있는지 확인 하는 방법을 제공 합니다. NPS RADIUS 서버를 사용할 수 있는지 여부를 결정을 다른 그룹 구성원에 연결 요청을 전송 시작할 수 있습니다. 이러한 설정을 사용 하 여 누락 되는; 요청을 고려 전에 프록시 NPS RADIUS 서버에서 응답을 기다리는 초 구성할 수 있습니다. NPS 프록시 하기 전에 장식 요청의 최대 수 식별 RADIUS 서버를 사용할 수 없습니다. 및 초 요청 NPS 프록시 하기 전에 간에 경과 될 수 있는 식별 RADIUS 서버를 사용할 수 없습니다.

## <a name="configure-nps-proxy-load-balancing"></a>프록시 부하 분산 NPS 구성

부하 분산 구성, 하기 전에 개수 원격 RADIUS 서버 그룹 해야 합니다. 서버 각각의 특정 그룹 하 고 각 서버에 대 한 우선 순위 부여 및 두께 설정의 회원을 포함 하는 배포 계획을 만듭니다.

>[!NOTE]
>다음 단계를 가정 사용자가 이미 배포 RADIUS 서버 구성 합니다.

프록시 서버와 RADIUS 클라이언트 앞으로 연결 요청 RADIUS 서버를 원격으로 NPS로 구성 하려면 다음 조치를 취합니다 해야 합니다.

1. RADIUS 클라이언트 배포 \ (VPN 서버의 전화 접속 서버, Terminal Services 게이트웨이 서버, 802.1 X 인증 스위치 및 802.1 X 무선 액세스 points\) NPS 프록시 서버에 연결 요청을 보낼 수 있도록 구성 하 고 있습니다.

2. NPS 프록시 RADIUS 클라이언트로 네트워크 액세스 서버를 구성 합니다. 자세한 내용은 참조 [구성 RADIUS 클라이언트](https://docs.microsoft.com/windows-server/networking/technologies/nps/nps-radius-clients-configure)합니다.

3. NPS 프록시에서 하나 이상의 원격 RADIUS 서버 그룹 만듭니다. 이 과정에서 RADIUS 서버를 원격 RADIUS 서버 그룹에 추가 합니다. 자세한 내용은 참조 [원격 RADIUS 서버 그룹 구성](https://docs.microsoft.com/windows-server/networking/technologies/nps/nps-crp-rrsg-configure)합니다.

4. 원격 RADIUS 서버 그룹에 추가 하는 각 RADIUS 서버에 대 한 NPS 프록시 RADIUS 서버 클릭 **부하 분산** 탭을 선택한 다음 구성 **우선 순위 부여**, **무게**, 및 **고급 설정**합니다.

5. NPS 프록시 인증과 계정 요청 원격 RADIUS 서버 그룹에 전달 하도록 요청 정책 연결을 구성 합니다. 원격 RADIUS 서버 그룹별로 한 연결 요청 정책을 만들어야 합니다. 자세한 내용은 참조 [구성 연결 요청 정책](https://docs.microsoft.com/windows-server/networking/technologies/nps/nps-crp-configure)합니다.


