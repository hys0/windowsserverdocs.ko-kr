---
title: QoS 정책 작동 방식
description: 이 항목에서는 그룹 정책을 사용 하 여 특정 응용 프로그램 및 Windows Server 2016에서 서비스의 네트워크 트래픽을 대역폭 우선 순위를 지정할 수 있는 서비스 품질 (QoS) 정책의 개요를 제공 합니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 25097cb8-b9b1-41c9-b3c7-3610a032e0d8
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 272272c833bb38924f1daa5561037901f6ff4e25
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59864284"
---
# <a name="how-qos-policy-works"></a>QoS 정책 작동 방식

>적용 대상: Windows Server (반기 채널), Windows Server 2016

시작 또는 QoS에 대 한 컴퓨터 구성 그룹 정책 설정 또는 업데이트 된 사용자를 가져오는 경우 다음 프로세스가 발생 합니다.

1. 그룹 정책 엔진이 Active Directory에서 사용자 또는 컴퓨터 구성 그룹 정책 설정을 검색합니다.

2. 그룹 정책 엔진이 QoS 정책에 변경 내용이 QoS 클라이언트 쪽 확장에 알립니다.

3. QoS 클라이언트 쪽 확장 QoS 검사 모듈에 QoS 정책 이벤트 알림을 보냅니다.

4. QoS 검사 모듈에 사용자 또는 컴퓨터 QoS 정책을 검색 하 고 저장 합니다.

때 새 전송 계층 끝점 \(TCP 연결 또는 UDP 트래픽을\) 를 만든 다음 프로세스가 발생 합니다.

1. TCP/IP 스택의 전송 계층 구성 요소는 QoS 검사 모듈에 알립니다.

2. QoS 검사 모듈에 저장 된 QoS 정책 전송 계층 끝점의 매개 변수를 비교 합니다.

3. 일치 하는 항목이 없으면 흐름을 제한 하는 QoS 정책 설정을 트래픽과 DSCP 값을 포함 하는 데이터 구조를 만들려면 Pacer.sys QoS 검사 모듈에 연결 합니다. 여러 QoS 정책을 전송 계층 끝점의 매개 변수와 일치 하는 경우에 가장 구체적인 QoS 정책이 사용 됩니다.

4. Pacer.sys 흐름을 저장 하 고 흐름 QoS 검사 모듈에 해당 하는 흐름 숫자를 반환 합니다.

5. QoS 검사 모듈에는 전송 계층으로 흐름 수를 반환합니다.

6. 전송 계층 전송 계층 끝점과 흐름 수를 저장 합니다.

전송 계층 끝점에 해당 하는 패킷 흐름 숫자로 표시 하는 경우 다음 프로세스가 보내집니다.

1. 전송 계층에는 내부적으로 패킷 흐름 번호로 표시합니다.

2. 네트워크 계층 Pacer.sys 패킷 흐름 번호에 해당 하는 DSCP 값을 쿼리 합니다.

3. Pacer.sys는 네트워크 계층 DSCP 값을 반환합니다.

4. 네트워크 계층 Pacer.sys 지정한 DSCP 값 IPv4 TOS 필드 또는 IPv6 트래픽 클래스 필드를 변경 하 고 IPv4 패킷에 대 한 최종 IPv4 헤더 체크섬을 계산 합니다.

5. 네트워크 계층 프레이밍 계층에 패킷을 전달합니다.

6. 프레이밍 계층 NDIS 통해 Pacer.sys에 패킷을 전달 패킷을으로 흐름 숫자로 표시 되므로 6.x 합니다.

7. Pacer.sys 패킷 흐름 수를 사용 하 여 패킷을 제한 될 경우와 그럴 경우를 결정, 보내는 패킷을 예약 합니다.

8. Pacer.sys 전달 패킷을 하거나 즉시 \(트래픽이 없는 경우 제한\) 또는 예약 된 대로 \(트래픽이 있으면 제한\) NDIS에 6.x에 대 한 적절 한 네트워크 어댑터를 통해 전송 합니다.

정책 기반 QoS의 이러한 프로세스는 다음과 같은 이점을 제공합니다.

- QoS 정책 적용 여부를 결정 하는 트래픽 검사 패킷 단위 보다는 전송 계층 끝점 이루어집니다.

- QoS 정책 일치 하지 않는 트래픽에 대 한 성능 영향은 없습니다.

- 응용은 DSCP 기반 차별화 된 서비스를 활용 하거나 트래픽을 제한 하기 위해 수정할 필요가 없습니다.

- QoS 정책을 트래픽이 IPsec를 사용 하 여 보호를 적용할 수 있습니다.

이 가이드의 다음 항목을 참조 하세요 [QoS 정책 아키텍처](qos-policy-architecture.md)합니다.

이 가이드의 첫 번째 항목을 참조 하세요 [의 QoS (서비스 품질) 정책을](qos-policy-top.md)합니다.
