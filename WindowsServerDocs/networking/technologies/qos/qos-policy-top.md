---
title: 품질 서비스 정책
description: 이 항목에서는 그룹 정책을 사용 하 여 네트워크 교통 대역폭 특정 응용 프로그램 및 Windows Server 2016 서비스의 우선 순위를 지정할 수 있습니다 (QoS) 서비스 품질 정책의 소개 합니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 16918506-102c-482e-89d3-004ad8d6aabe
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 76405c677fe7eb4d51f9c190499b909ac2fe4a0c
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="quality-of-service-qos-policy"></a>서비스 \(QoS\) 정책 품질

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

그룹 정책을 사용 하 여 설정을 배포 QoS 프로필 만들기 Active Directory 인프라 전체에서 QoS 정책 네트워크 대역폭 관리 중심점으로 사용할 수 있습니다.

>[!NOTE]
>  이 항목 외에 다음 QoS 정책 설명서를 사용할 수 있습니다.  
>   
>  - [정책 QoS 시작](qos-policy-get-started.md)
>  - [QoS 정책을 관리합니다](qos-policy-manage.md)
>  - [QoS 정책에 대 한 질문과 대답](qos-policy-faq.md)

그룹 정책 개체의 일부로 서 사용자 로그인 세션 또는 컴퓨터에 적용 되는 QoS 정책이 된 Active Directory 컨테이너 도메인, 사이트나 조직을 등에 연결할 때 \(GPO\) \(OU\) 합니다.

기존 응용 프로그램 QoS 정책에 따라 제공 되는 이점을 활용할 수 수정할 필요가 없습니다 의미 하는 응용 프로그램 계층 아래 QoS 교통 관리 발생 합니다.

## <a name="operating-systems-that-support-qos-policy"></a>지원 정책 QoS 운영 체제

컴퓨터 또는 사용자가 다음 Microsoft 운영 체제에 대 한 대역폭 관리 QoS 정책을 사용할 수 있습니다.

- Windows Server 2016
- Windows 10
- Windows Server 2012 r 2
- Windows 8.1
- Windows Server 2012
- Windows 8
- Windows Server 2008 R2
- Windows 7
- Windows Server 2008
- Windows Vista

### <a name="location-of-qos-policy-in-group-policy"></a>그룹 정책에서 QoS 정책의 위치

Windows Server 2016 그룹 정책 관리 편집기에서 컴퓨터 구성에 대 한 정책을 QoS 경로가 다음 합니다.

**기본 도메인 정책 | 컴퓨터 구성 | 정책 | Windows 설정 | Policy\ 기반 QoS**

이 경로 다음 이미지에 설명 되어 있습니다.

![그룹 정책에서 QoS 정책의 위치](../../media/QoS/QoS-Gp.jpg)

Windows Server 2016 그룹 정책 관리 편집기에서의 사용자 구성에 대 한 정책을 QoS 경로가 다음 합니다.

**기본 도메인 정책 | 사용자 구성 | 정책 | Windows 설정 | Policy\ 기반 QoS**

기본적으로 QoS 정책이 구성 됩니다.

## <a name="why-use-qos-policy"></a>QoS 정책을 사용 하는 이유
  
네트워크에서 교통량 증가 점점 더 중요 한-서비스의 비용으로 네트워크 성능을 하는 있지만 네트워크 교통 우선 순위를 지정 하 고 관리 하기 쉬운 일반적으로 아닙니다.

네트워크의 mission\ 중요 하며 latency\ 응용 프로그램 낮은 우선 순위가 교통 로부터 대역폭 경쟁 해야 합니다. 을 동시에 일부 사용자와 특정 네트워크 성능이 요구 사항이 필요할 수 있는 컴퓨터 서비스 수준을 구분 합니다.

효과적인 하 고 예측 가능한 네트워크 성능 수준 제공 하 고 도전 IP \(VoIP\) 및 스트리밍 비디오를 통해 음성 같은 대기 민감한 응용 프로그램 또는 다양 한 영역 네트워크 \(WAN\) 연결을 통해 먼저 자주 표시 됩니다. 그러나 모든 네트워크 환경 제공 하 고 예측 가능한 네트워크 서비스 수준을 최종 목표 적용 \ (예를 들어 엔터프라이즈의 로컬 영역 network\), 회사의 사용자 정의 line\ of\ 비즈니스 응용 프로그램 등의 VoIP 응용 프로그램 보다를 합니다.
  
정책 기반 QoS 응용 프로그램, 사용자가 컴퓨터에 따라 네트워크 제어 기능을 제공 하는 네트워크 대역폭 관리 도구입니다. 

QoS 정책을 사용 하 여 응용 프로그램에 대 한 특정 응용 프로그램 프로그래밍 인터페이스 \(APIs\) 쓸 수 필요가 없습니다. 이렇게 하면 QoS 기존 응용 프로그램으로 사용할 수 있습니다. 또한 정책 기반 QoS 활용 기존 관리 인프라, 그룹 정책으로 QoS 정책에 따라 기본 제공 되므로 합니다.

## <a name="define-qos-priority-through-a-differentiated-services-code-point-dscp"></a>정의 DSCP(Differentiated Services Code Point) \(DSCP\) 통해 QoS 우선 순위 부여
  
다른 종류의 네트워크 트래픽에 할당 DSCP(Differentiated Services Code Point) \(DSCP\) 값 네트워크 교통 우선 순위를 정의 하는 QoS 정책 만들 수 있습니다. 

DSCP 값 \(0–63\) 및 ipv6에서 교통 클래스 필드 내에서 서비스 종류 \(TOS\) 필드 IPv4 패킷 헤더에 적용할 수 있습니다. 

DSCP 값 라우터 하 여 교통 큐 동작을 결정 하는 인터넷 프로토콜 \(IP\) 수준 네트워크 교통 분류를 제공 합니다. 

예를 들어, 라우터 특정 DSCP 값으로 패킷을 세 개의 큐 중 하나에 장소를 구성할 수 있습니다: 높은 우선 순위를 최대한 또는 최상의 보다 낮춥니다. 

우선 순위가 높은 큐에는 네트워크 교통 중요 다른 교통 통해 기본 설정을 있습니다.

### <a name="limit-network-bandwidth-use-per-application-with-throttle-rate"></a>응용 프로그램 제한 속도와 별로 네트워크 대역폭 사용 제한

또한 QoS 정책에서 조절 속도 지정 하 여 네트워크 교통 아웃 바운드 응용 프로그램을 제한할 수 있습니다.

조절 제한 정의 하는 QoS 정책 아웃 바운드 네트워크 교통의 속도 결정 합니다. 예를 들어, IT 부서 WAN 비용 관리, 파일 서버 이상 특정 속도 다운로드 하지 제공할 수 있다는 지정 하는 서비스가 수준 계약을 구현할 수 있습니다.  

### <a name="use-qos-policy-to-apply-dscp-values-and-throttle-rates"></a>QoS 정책을 사용 하 여 DSCP 적용 값을 속도 제한

또한 QoS 정책 DSCP 값 적용 다음과 교통 아웃 바운드 네트워크에 대 한 요금이 부과 조절할을 사용할 수 있습니다.

- 디렉터리 경로 및 보내는 응용 프로그램

- 주소 접두사 또는 원본과 대상 V4 또는 IPv6 주소

- 프로토콜-전송 컨트롤 \(TCP\) 및 사용자 데이터 그램 프로토콜 \(UDP\) 프로토콜

- 포트 원본과 대상와 포트 범위 \(TCP or UDP\)

- 특정 사용자 또는 그룹에 배포에서 그룹 정책을 통해 컴퓨터

이러한 컨트롤을 사용 하 여 라우터에 낮음으로 대기 시간이 큐 VoIP 패킷을를 활성화 DSCP 46 VoIP 응용 프로그램에 대 한 값으로 QoS 정책을 지정 하거나 QoS 정책을 443 TCP 포트에서 보내면 서버의 아웃 바운드 두 번째 \(KBps\) 당 512kb 트래픽 집합을 조절를 사용할 수 있습니다.

또한 QoS 정책 특별 한 대역폭 요구 사항에 있는 특정 응용 프로그램에 적용할 수 있습니다. 자세한 내용은 참조 [QoS 정책 시나리오](qos-policy-scenarios.md)합니다.
  
## <a name="advantages-of-qos-policy"></a>장점 QoS 정책

QoS 정책을 사용 하 여 구성 하 고 라우터와 스위치를 구성할 수 없는 QoS 정책을 적용 수 있습니다. QoS 정책은 다음 이점을 제공합니다.
  
1. **하위 수준:** 어려운 주소 할당 동적 IP 사용 하 여 구성 하나 또는 스위치를 고정된 하거나 라우터 포트에 연결 되어 있지 않으면 컴퓨터의 경우 처럼 자주 노트북으로 사용자의 컴퓨터를 하는 경우에 특히 사용자 수준 QoS 정책을 라우터 또는 스위치를 만들 수 있습니다. 반면, QoS 정책 쉽게 도메인 컨트롤러에서 user\ 수준 QoS 정책을 구성 하는 사용자의 컴퓨터에 대 한 정책을 전파 있습니다.
2. **유연성**합니다. 어떻게 컴퓨터가 네트워크에 연결을 관계 없이 QoS 정책이 적용 되는-컴퓨터 WiFi 또는 이더넷 모든 위치에서 사용 하 여 연결할 수 있습니다. User\ 수준의 QoS 정책 QoS 정책 사용자 로그온 모든 위치에서 호환 되는 모든 장치에 적용 됩니다.
3. **보안:** 라우터의 IP 계층 패킷이에서 위에 모든 정보에 따라 교통 분류 수 없는 IT 부서 보안 \(IPsec\) 인터넷 프로토콜을 사용 하 여 사용자의 트래픽부터 끝까지 암호화를 \ (TCP port\ 예). 그러나 QoS 정책을 사용 하 여 IP 페이로드는 암호화 되며 패킷이 보내는 전에 IP 헤더에 패킷의 우선 순위를 표시 하는 최종 장치에서 패킷을 분류 수 있습니다.
4. **성능:** 원본에 가까이 있을 때 일부 QoS 기능을 제한 하는 등 더 나은 수행 합니다. QoS 정책을 원본으로 가장 가까운 같은 QoS 기능으로 이동합니다.
5. **관리:** QoS 정책 두 가지 방법으로 네트워크 관리를 향상 합니다.

    **a**. 그룹 정책 기반, 하므로 구성 하 고 필요할 때마다와 한 중앙 도메인 컨트롤러 컴퓨터의 컴퓨터 사용자/QoS 정책 관리 QoS 정책 사용할 수 있습니다.

    **b**. QoS 정책 정책을 Uniform Resource Locator \(URL\) 정책 기반 각 QoS 정책이 적용 해야 할 서버의 IP 주소를 지정 하는 대신 하 여 지정 하려면 장치를 제공 하 여 사용자/컴퓨터 구성을 수 있습니다. 예를 들어 네트워크 일반적인 URL을 공유 하는 서버 클러스터에 있습니다. QoS 정책을 사용 하 여 각 정책 각 서버의 IP 주소를 기준으로 각 서버에 대 한 정책을 클러스터의 만드는 대신 일반적인 URL에 따라 하나 정책을 만들 수 있습니다.

이 가이드에 다음 항목에 대 한 참고 [QoS 정책 시작](qos-policy-get-started.md)합니다.

