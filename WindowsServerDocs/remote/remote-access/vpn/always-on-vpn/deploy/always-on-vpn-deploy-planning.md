---
title: Always On VPN 배포 계획 수립
description: 이 항목에서는 Always On VPN Windows Server 2016의 배포 계획 지침을 제공 합니다.
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.assetid: 3c9de3ec-4bbd-4db0-b47a-03507a315383
ms.localizationpriority: medium
ms.author: pashort
author: shortpatti
ms.date: 11/05/2018
ms.openlocfilehash: d629f04abda0ce22deb75e487f5b485f50a60a53
ms.sourcegitcommit: 4893d79345cea85db427224bb106fc1bf88ffdbc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2018
ms.locfileid: "6067322"
---
# 1단계. Always On VPN 배포 계획

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows 10


& #171;  [ **이전:** Always On VPN을 배포 하기 위한 워크플로에 대해 알아보기](always-on-vpn-deploy-deployment.md)<br>
& #187;  [ **다음:** 2 단계입니다. 서버 인프라 구성](vpn-deploy-server-infrastructure.md)

이 단계를 계획 하 고 Always On VPN 배포 준비를 시작 합니다. VPN 서버를 사용 하 여 계획 이라면 컴퓨터에 원격 액세스 서버 역할을 설치 하기 전에 다음 작업을 수행 합니다. 후 적절 한 계획을 Always On VPN을 배포할 수 있으며 필요에 따라 Azure AD를 사용 하 여 VPN 연결에 대 한 조건부 액세스를 구성할 수 있습니다. 

[!INCLUDE [always-on-vpn-standard-config-considerations-include](../../../includes/always-on-vpn-standard-config-considerations-include.md)]


## 원격 액세스 서버를 준비 합니다.

VPN 서버를 사용 하는 컴퓨터에서 다음을 수행 해야 합니다. 

- **하드웨어 구성이 올바른지와 VPN 서버 소프트웨어를 확인**합니다. 원격 액세스 VPN 서버로 사용 하려는 컴퓨터에서 Windows Server 2016을 설치 합니다. 이 서버 설치 하는 두 개의 실제 네트워크 어댑터 개 외부 경계 네트워크에 연결할과 내부 경계 네트워크에 연결할 수 있어야 합니다.

- **네트워크 인터넷 및 개인에 연결 된 네트워크 어댑터에 연결 네트워크 어댑터를 식별**합니다. 인트라넷 향하는 어댑터는 로컬 네트워크에서 IP 주소를 사용할 수 있는 동안 공용 IP 주소를 사용 하 여 인터넷을 향하는 네트워크 어댑터를 구성 합니다.

    >[!TIP]
    >경계 네트워크에서 공용 IP 주소를 사용 하지 않으려는 경우에 공용 IP 주소를 사용 하 여 Edge 방화벽을 구성 하 고 VPN 서버에 대 한 VPN 연결 요청을 전달할 수 있도록 방화벽 구성 수 있습니다.

- **VPN 서버를 네트워크에 연결**합니다. 경계 네트워크 경계 방화벽 사이의 경계 방화벽에 VPN 서버를 설치 합니다.

## 인증 방법 계획

IKEv2 VPN 터널링 프로토콜에서 [Internet Engineering Task Force\ 요청 Comments7296에 대 한](https://datatracker.ietf.org/doc/rfc7296/)설명입니다. IKEv2의 기본 장점은에서 내부 네트워크 연결 중단을가 것입니다. 예를 들어 연결에서 임시 손실 하거나 사용자의 클라이언트 컴퓨터를 이동 하는 경우 네트워크 IKEv2 네트워크 연결을 다시 설정 하는 경우 다른 VPN 연결 자동으로 복원-사용자 개입 없이 합니다.

>[!TIP]
>서버 보안 공간을 줄일 수 있는 원격 액세스 VPN 서버도 사용 하지 않는 프로토콜을 사용 하지 않도록 설정 하는 동안 IKEv2 연결을 지원 하도록 구성할 수 있습니다. 

## 원격 클라이언트에 대 한 IP 주소를 계획

VPN 클라이언트를 구성 하는 정적 주소 풀에서 주소 또는 DHCP 서버에서 IP 주소를 할당 하도록 VPN 서버를 구성할 수 있습니다. 

## 환경 준비

- **외부 방화벽을 구성 하는 권한이 있고 유효한 공용 IP 주소가 있는지 확인**합니다. IKEv2 VPN 연결을 지원 하도록 방화벽 포트를 엽니다. 외부 클라이언트에서 연결을 허용 하도록 공용 IP 주소를 해야 합니다.

- **VPN 클라이언트에 대 한 정적 IP 주소의 범위를 선택**합니다. 지원 하고자 하는 동시 VPN 클라이언트의 최대 수를 결정 합니다. 또한 *고정 주소 풀*, 즉 해당 요구 사항을 충족 하도록 내부 경계 네트워크에서 고정 IP 주소 범위를 계획 합니다. DHCP를 사용 하 여 내부 DMZ에서 IP 주소를 제공 하는 경우 DHCP에 이러한 고정 IP 주소에 대 한 제외 만들기 해야 수도 있습니다.

- **공용 DNS 영역에를 편집할 수 있는지 확인**합니다. VPN 인프라를 지 원하는 공용 DNS 도메인에 DNS 레코드를 추가 합니다. 

- **모든 VPN 사용자에 게 Active Directory 사용자 \(AD DS\)에 사용자 계정이 있는지 확인**합니다. 전에 사용자가 VPN 연결을 사용 하 여 네트워크에 연결할 수 있는 추가에서 사용자 계정 있어야 합니다.

## 라우팅 준비 및 방화벽 

경계 네트워크 경계 내부 및 외부 네트워크에 파티션을 경계 네트워크 내부 VPN 서버를 설치 합니다. 네트워크 환경에 따라 여러 라우팅 많이 수정 해야 합니다.

- **\(Optional\) 구성 포트 전달 합니다.** Edge 방화벽 포트 및 프로토콜 Id IKEv2 VPN와 관련 된 열기를 VPN 서버에이 전달 해야 합니다. 대부분의 환경에서 이렇게 하려면 포트 전달 구성할 수 있습니다. VPN 서버에 유니버설 UDP 데이터 그램 프로토콜 () 포트를 500 및 4500 리디렉션하십시오.

- **구성 라우팅 DNS 서버와 VPN 서버 인터넷에 연결할 수 있도록**합니다. 이 배포 사용 IKEv2 및 네트워크 주소 변환 \(NAT\) 합니다. VPN 서버 모든 필수 내부 네트워크 및 네트워크 리소스를 연결할 수 있는지 확인 합니다. 네트워크 또는 VPN 서버에서 연결할 수 없는 리소스도 연결할 수 없는 경우 원격 위치에서 VPN 연결을 통해

대부분의 환경에서 새 내부 경계 네트워크에 연결 하려면 edge 방화벽 및 VPN 서버에서 정적 경로 조정 합니다. 그러나 더 복잡 한 환경에서 내부 라우터를 정적 경로 추가 하거나 VPN 서버와의 VPN 클라이언트와 관련 된 IP 주소 블록에 대 한 내부 방화벽 규칙을 조정 할 수도 있습니다.

## 다음 단계
2 [단계입니다. 서버 인프라 구성](vpn-deploy-server-infrastructure.md):이 단계에서 설치 하 고이 VPN을 지 원하는 데 필요한 서버 측 구성 요소를 구성 합니다. 서버 쪽 구성 요소는 사용자, VPN 서버 및 NPS 서버에서 사용 되는 인증서를 배포할 PKI 구성 포함 됩니다. 

---