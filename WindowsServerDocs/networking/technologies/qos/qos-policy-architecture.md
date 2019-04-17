---
title: 아키텍처 QoS 정책
description: 이 항목에서는 그룹 정책을 사용 하 여 네트워크 교통 대역폭 특정 응용 프로그램 및 Windows Server 2016 서비스의 우선 순위를 지정할 수 있습니다 (QoS) 서비스 품질 정책의 소개 합니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 25097cb8-b9b1-41c9-b3c7-3610a032e0d8
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 00d36604c57add6bf9f45b0166b08c1fb15be467
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="qos-policy-architecture"></a>아키텍처 QoS 정책

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

아키텍처 QoS 정책에 대 한 자세한 내용은이 항목을 사용할 수 있습니다.

다음 그림은 정책 기반 QoS 아키텍처 합니다.

![아키텍처 QoS 정책](../../media/QoS/QoS-Policy-Architecture.jpg)

정책 기반 QoS 아키텍처 다음과 같은 구성 요소 이루어져 있습니다.

- **그룹 정책 클라이언트 서비스**합니다. 사용자와 컴퓨터 구성 그룹 정책 설정을 관리 하는 Windows 서비스입니다.

- **그룹 정책 엔진**합니다. 변경 내용을 확인 및 주기적으로 시작 되 면 사용자 및 컴퓨터 구성 그룹 정책 설정을 Active Directory에서 검색 하는 그룹 정책 클라이언트 서비스의 구성 요소 \ (기본적으로 모든 90 minutes\). 변경 내용이 감지 되 면 그룹 정책 엔진 새 그룹 정책 설정을 검색 합니다. 그룹 정책 엔진 수신 Gpo 처리 하 고 QoS 정책 업데이트는 클라이언트 QoS 확장명 알립니다.

- **QoS 클라이언트 쪽 확장**합니다. 그룹 정책 QoS 정책을 변경 하는 엔진에서 표시 대기 하 고 QoS 검사 모듈 알립니다 하는 그룹 정책 클라이언트 서비스의 구성 요소입니다.

- **TCP/IP 스택**합니다. TCP/IP 스택 IPv4 및 IPv6에 대 한 통합된 지원을 포함 된 Windows 필터링 플랫폼을 지원 합니다. 

- **QoS 검사**합니다. QoS 클라이언트 쪽 확장 QoS 정책 변경이 표시 될 때 TCP/IP 스택 내 모듈 A 구성 요소 QoS 정책 설정을 가져오고,는 Transport Layer 및 Pacer.sys 내부적으로 QoS 정책을 일치 하는 교통 않은 상태로 표시와 상호 작용 합니다.

- **NDIS 6.x**합니다. 커널 모드 드라이버 네트워크와는 클라이언트와 Windows Server 운영 체제의 운영 체제 표준 인터페이스입니다. NDIS 6.x 지원 무게는 가벼우며 필터 NDIS 중간 드라이버 및 미니 드라이버에 대 한 성능 향상을 제공 하는 간단한 드라이버 모델은 합니다.

- **인터페이스 \(NPI\) QoS 네트워크 공급자**합니다. 커널 모드 드라이버 Pacer.sys와 상호 작용에 대 한 인터페이스 합니다.

- **Pacer.sys**합니다. 일반 QoS \(GQoS\) 및 교통 제어 \(TC\) Api 사용 하는 응용 프로그램 교통 및 정책에 따라 QoS에 대 한 패킷 일정을 제어 하는 NDIS 6.x 무게는 가벼우며 필터 드라이버 합니다. Pacer.sys는 Windows XP 및 Windows Server 2003 Psched.sys 바뀝니다. Pacer.sys 속성의 네트워크 연결 또는 어댑터에서 QoS 패킷을 스케줄러 구성 요소와 함께 설치 되어 있습니다.

이 가이드에 다음 항목에 대 한 참고 [QoS 정책 시나리오](qos-policy-scenarios.md)합니다.

이 가이드의 첫 번째 항목을 참조 하세요. [(QoS) 서비스 품질 정책](qos-policy-top.md)합니다.

