---
title: QoS 정책의 작동 방식
description: 이 항목에서는 그룹 정책을 사용 하 여 네트워크 교통 대역폭 특정 응용 프로그램 및 Windows Server 2016 서비스의 우선 순위를 지정할 수 있습니다 (QoS) 서비스 품질 정책의 소개 합니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 25097cb8-b9b1-41c9-b3c7-3610a032e0d8
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 1073308b5939e648fdcc2006acdce76ecf0331c9
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="how-qos-policy-works"></a>QoS 정책의 작동 방식

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

을 시작 하거나 업데이트 된 사용자 또는 컴퓨터 구성 그룹 정책 설정을 QoS에 대 한 다음 프로세스 발생 합니다.

1. 그룹 정책 엔진 Active Directory에서 사용자 또는 컴퓨터 구성 그룹 정책 설정을 검색합니다.

2. 그룹 정책 엔진 QoS 정책에서 변경 된 QoS 클라이언트 확장 알립니다.

3. QoS 클라이언트 확장 QoS 검사 모듈 QoS 정책 이벤트 알림을 보냅니다.

4. QoS 검사 모듈 QoS 사용자 또는 컴퓨터 정책의 검색 하 고 저장 합니다.

새 Transport Layer 끝점 때 \ (TCP 연결 또는 UDP traffic\)이 만든 다음 프로세스가 발생 합니다.

1. TCP/IP 스택 Transport Layer 구성 요소 QoS 검사 모듈 알립니다.

2. QoS 검사 모듈에 저장 된 QoS 정책 Transport Layer 끝점 매개 비교합니다.

3. 일치 하는 경우 QoS 검사 모듈 연락처 Pacer.sys DSCP 값과 조절 QoS 해당 하는 정책 설정 교통을 포함 하는 데이터 구조 흐름을 만들 수 있습니다. 여러 개의 QoS 정책을 Transport Layer 끝점 매개 변수와 일치 하는 경우 가장 특정 QoS 정책 사용 됩니다.

4. Pacer.sys 흐름을 저장 하 고 해당 QoS 검사 모듈 흐름 하는 흐름 번호를 반환 합니다.

5. QoS 검사 모듈 Transport Layer에 흐름 번호를 반환합니다.

6. Transport Layer Transport Layer 끝점으로 흐름 번호를 저장 합니다.

해당 하는 Transport Layer 끝점 패킷 흐름 번호로 표시 되는 경우 전송 다음 프로세스가 발생 합니다.

1. Transport Layer 흐름 번호로 패킷을 내부적으로 표시 됩니다.

2. 네트워크 계층 패킷 흐름 번호에 해당 하는 DSCP 가치에 대 한 Pacer.sys 쿼리.

3. Pacer.sys는 네트워크 계층 DSCP 값을 반환 됩니다.

4. 네트워크 계층 IPv4 TOS 필드 또는 IPv6 교통 클래스 필드 Pacer.sys에 지정 된 DSCP 값으로 변경 하 고 IPv4 패킷이 계산 최종 IPv4 머리글 검사 합니다.

5. 네트워크 계층 패킷이 프레이밍 계층을 전달 합니다.

6. 프레이밍 계층 패킷을 Pacer.sys NDIS 통해를 전달 패킷이 흐름 번호 표시 된을 하기 때문에 6.x 합니다.

7. Pacer.sys 패킷 흐름 번호를 사용 하 여 패킷이 제한 될 하는 경우 있고 결정를 보내는 데 패킷 일정을 조정 합니다.

8. Pacer.sys 전달 패킷을 하거나 즉시 \ (교통 throttling\ 없는 경우) 또는으로 예약 된 \ (교통 throttling\ 있는 경우) NDIS에 적절 한 네트워크 어댑터를 통해 전송 하기 위해 6.x 합니다.

이러한 프로세스 qos 정책 기반 다음과 같은 이점을 제공합니다.

- QoS 정책이 적용 있는지 여부를 결정 하는 교통 검사 패킷 것이 아니라 별로 Transport Layer 끝점 수행 됩니다.

- 교통량 QoS 정책와 일치 하지 않는 성능 영향은 없습니다.

- 응용 프로그램 DSCP 기반 차별화 된 서비스를 이용 하거나 조절 교통 수정할 필요가 없습니다.

- QoS 정책을 IPsec로 보호 교통 적용할 수 있습니다.

이 가이드에 다음 항목에 대 한 참고 [QoS 정책 아키텍처](qos-policy-architecture.md)합니다.

이 가이드의 첫 번째 항목을 참조 하세요. [(QoS) 서비스 품질 정책](qos-policy-top.md)합니다.
