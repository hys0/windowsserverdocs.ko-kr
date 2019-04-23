---
title: QoS 정책 아키텍처
description: 이 항목에서는 그룹 정책을 사용 하 여 특정 응용 프로그램 및 Windows Server 2016에서 서비스의 네트워크 트래픽을 대역폭 우선 순위를 지정할 수 있는 서비스 품질 (QoS) 정책의 개요를 제공 합니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 25097cb8-b9b1-41c9-b3c7-3610a032e0d8
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: bad37ba3558137b02ae495fe8dd9be2c903cdd97
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59843144"
---
# <a name="qos-policy-architecture"></a>QoS 정책 아키텍처

>적용 대상: Windows Server (반기 채널), Windows Server 2016

QoS 정책의 아키텍처에 대해 자세히 알아보려면이 항목에서는 사용할 수 있습니다.

다음 그림의 정책 기반 QoS 아키텍처를 보여 줍니다.

![QoS 정책의 아키텍처](../../media/QoS/QoS-Policy-Architecture.jpg)

정책 기반 QoS의 아키텍처는 다음 구성 요소가 구성 됩니다.

- **그룹 정책 클라이언트 서비스**합니다. 사용자 및 컴퓨터 구성 그룹 정책 설정을 관리 하는 Windows 서비스입니다.

- **그룹 정책 엔진**합니다. 변경 내용에 대 한 시작으로 이동 하 고 정기적으로 Active Directory에서 사용자 및 컴퓨터 구성 그룹 정책 설정을 검색 하는 그룹 정책 클라이언트 서비스의 구성 요소 확인 \(기본적으로 90 분 마다\)합니다. 변경이 감지 되 면 그룹 정책 엔진이 새 그룹 정책 설정을 검색 합니다. 그룹 정책 엔진이 들어오는 Gpo를 처리 하 고 QoS 정책이 업데이트 될 때 QoS 클라이언트 쪽 확장에 알립니다.

- **QoS 클라이언트 쪽 확장**합니다. QoS 정책이 변경 된 그룹 정책 엔진에서 표시 될 때까지 대기 하는 QoS 검사 모듈에 알립니다 그룹 정책 클라이언트 서비스는 구성 요소입니다.

- **TCP/IP 스택**합니다. IPv4 및 IPv6에 대 한 통합된 지원을 포함 하 고 Windows 필터링 플랫폼을 지 원하는 TCP/IP 스택. 

- **QoS 검사**합니다. QoS 정책 설정을 검색 하 고 전송 계층 및 Pacer.sys QoS를 일치 하는 트래픽을 내부적으로 표시할 상호 작용 하는 QoS 클라이언트 쪽 확장에서 QoS 정책 변경의 징후에 대해 대기 하는 TCP/IP 스택 내의 모듈은 구성 요소 정책입니다.

- **NDIS 6.x**. 커널 모드 네트워크 드라이버와 Windows Server 및 클라이언트 운영 체제에서 운영 체제는 표준 인터페이스입니다. NDIS 6.x 지원 lightweight 필터, 이것은 더 나은 성능을 제공 하는 NDIS 중간 드라이버 및 미니 포트 드라이버에 대 한 간소화 된 드라이버 모델입니다.

- **QoS 네트워크 공급자 인터페이스 \(NPI\)** 합니다. Pacer.sys와 상호 작용 하는 커널 모드 드라이버에 대 한 인터페이스입니다.

- **Pacer.sys**합니다. 패킷 일정 정책 기반 QoS 및 일반 QoS를 사용 하는 응용 프로그램의 트래픽을 제어 하는 NDIS 6.x 간단한 필터 드라이버 \(GQoS\) 및 트래픽 제어 \(TC\) Api. Pacer.sys Psched.sys Windows Server 2003 및 Windows XP를 대체 합니다. Pacer.sys는 네트워크 연결 또는 어댑터의 속성에서 QoS 패킷 Scheduler 구성 요소를 사용 하 여 설치 됩니다.

이 가이드의 다음 항목을 참조 하세요 [QoS 정책 시나리오](qos-policy-scenarios.md)합니다.

이 가이드의 첫 번째 항목을 참조 하세요 [의 QoS (서비스 품질) 정책을](qos-policy-top.md)합니다.

