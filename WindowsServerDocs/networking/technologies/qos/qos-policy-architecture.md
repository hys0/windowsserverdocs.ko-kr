---
title: QoS 정책 아키텍처
description: 이 항목에서는 그룹 정책를 사용 하 여 Windows Server 2016의 특정 응용 프로그램 및 서비스에 대 한 네트워크 트래픽 대역폭의 우선 순위를 지정할 수 있는 QoS (서비스 품질) 정책의 개요를 제공 합니다.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 25097cb8-b9b1-41c9-b3c7-3610a032e0d8
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 609d3f28465380b7d15648cfeb73070a39b9362f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71395975"
---
# <a name="qos-policy-architecture"></a>QoS 정책 아키텍처

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목을 사용 하 여 QoS 정책의 아키텍처에 대해 알아볼 수 있습니다.

다음 그림은 정책 기반 QoS의 아키텍처를 보여 줍니다.

![QoS 정책 아키텍처](../../media/QoS/QoS-Policy-Architecture.jpg)

정책 기반 QoS의 아키텍처는 다음 구성 요소로 구성 됩니다.

- **클라이언트 서비스를 그룹 정책**합니다. 사용자 및 컴퓨터 구성 그룹 정책 설정을 관리 하는 Windows 서비스입니다.

- **그룹 정책 엔진**입니다. 시작 시 Active Directory에서 사용자 및 컴퓨터 구성 그룹 정책 설정을 검색 하 고 주기적으로 변경 @no__t 내용을 확인 하는 그룹 정책 클라이언트 서비스의 구성 요소입니다. 기본값은 90 분 @ no__t-1입니다. 변경 내용이 검색 되 면 그룹 정책 엔진은 새 그룹 정책 설정을 검색 합니다. 그룹 정책 엔진은 들어오는 Gpo를 처리 하 고 QoS 정책을 업데이트할 때 QoS 클라이언트 쪽 확장에 알립니다.

- **QoS 클라이언트 쪽 확장**입니다. 그룹 정책 엔진에서 표시 될 때까지 대기 하는 그룹 정책 클라이언트 서비스의 구성 요소로, QoS 정책이 변경 되었으며 QoS 검사 모듈을 알립니다.

- **Tcp/ip Stack**. IPv4 및 i p v 6에 대 한 통합 지원을 포함 하 고 Windows 필터링 플랫폼을 지 원하는 TCP/IP 스택입니다. 

- **QoS 검사**. 모듈은 qos 클라이언트 쪽 확장에서 QoS 정책 변경의 표시를 대기 하 고, QoS 정책 설정을 검색 하 고, 전송 계층과의 상호 작용을 통해 QoS와 일치 하는 트래픽을 내부적으로 표시 하는 TCP/IP 스택 내의 구성 요소입니다. 방침.

- **NDIS**6.x. 커널 모드 네트워크 드라이버와 Windows Server 및 클라이언트 운영 체제의 운영 체제 간의 표준 인터페이스입니다. NDIS 6.x는 더 나은 성능을 제공 하는 NDIS 중간 드라이버 및 미니 포트 드라이버를 위한 단순화 된 드라이버 모델인 간단한 필터를 지원 합니다.

- **QoS 네트워크 공급자 인터페이스 \(NPI @ no__t-2**. Config.sys와 상호 작용 하는 커널 모드 드라이버용 인터페이스입니다.

- **페이**서. 정책 기반 QoS의 패킷 일정을 제어 하는 NDIS 8.x 경량 필터 드라이버 및 일반 QoS \(GQoS @ no__t-1 및 트래픽 제어 \(TC @ no__t Api를 사용 하는 응용 프로그램의 트래픽 Windows Server 2003 및 Windows XP에서 node.js를 교체 했습니다. 페이는 네트워크 연결 또는 어댑터의 속성에서 QoS 패킷 스케줄러 구성 요소와 함께 설치 됩니다.

이 가이드의 다음 항목에 대해서는 [QoS 정책 시나리오](qos-policy-scenarios.md)를 참조 하십시오.

이 가이드의 첫 번째 항목은 [QoS (서비스 품질) 정책](qos-policy-top.md)을 참조 하세요.

