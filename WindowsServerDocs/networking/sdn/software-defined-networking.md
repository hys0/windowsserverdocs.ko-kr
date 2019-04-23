---
title: SDN(소프트웨어 정의 네트워킹)
description: SDN(소프트웨어 방식 네트워킹)은 데이터 센터의 라우터, 스위치 및 게이트웨이 같은 실제 및 가상 네트워크 장치를 중앙에서 구성하고 관리하는 방법을 제공합니다. 이 항목에서는 사용 하 여 Windows Server, System Center 및 Microsoft Azure에서 제공 되는 소프트웨어 정의 네트워킹 (SDN) 기술에 대해 알아봅니다.
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.topic: article
ms.assetid: 9a1ea73c-20cd-42c5-95ad-b003b9cc6d64
ms.author: pashort
author: shortpatti
ms.date: 08/09/2018
ms.openlocfilehash: a6c4db97b1c55d5114eba09251685ef0f2b840bc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59855234"
---
# <a name="sdn-in-windows-server-overview"></a>Windows Server의 SDN 개요

>적용 대상: Windows Server (반기 채널), Windows Server 2016


SDN(소프트웨어 방식 네트워킹)은 데이터 센터의 라우터, 스위치 및 게이트웨이 같은 실제 및 가상 네트워크 장치를 중앙에서 구성하고 관리하는 방법을 제공합니다. 가상 네트워크와 실제 네트워크 간의 더욱 심층적인 통합을 위해 기존 SDN 호환 장치를 사용할 수 있습니다. Hyper-v 가상 스위치, Hyper-v 네트워크 가상화 및 RAS 게이트웨이 같은 가상 네트워크 요소는 SDN 인프라의 필수적인 요소가 되도록 설계 되었습니다. 

>[!Note]
>Hyper-v 호스트 및 virtual machines (Vm) 노드 네트워크 컨트롤러 및 소프트웨어 부하 분산 등의 SDN 인프라 서버를 실행 중인 Windows Server 2016 Datacenter edition이 설치 있어야 합니다. 
>
>포함 하는 유일한 테 넌 트 워크 로드 Vm SDN 제어 네트워크에 연결 하는 Hyper-v 호스트는 Windows Server 2016 Standard edition을 사용할 수 있습니다.

SDN은 네트워크 평면, 네트워크 장치 자체에 더 이상 바인딩되어 있기 때문에 가능 합니다. 그러나 System Center 2016과 같은 데이터 센터 관리 소프트웨어 같은 다른 엔터티를 네트워크 평면을 사용 합니다. SDN 응용 프로그램 및 워크 로드의 요구 사항을 충족 하는 자동화 된 중앙 집중식된 방법을 제공 합니다. 데이터 센터 네트워크를 동적으로 관리할 수 있습니다. 

SDN을 사용할 수 있습니다.

- 동적으로 만들기, 보호 및 변화 하는 앱의 요구를 충족 하기 위해 네트워크를 연결 합니다.
- 무중단 방식으로 워크 로드 배포 속도
- 네트워크를 통해 확산 되지 않도록 보안 취약성을 포함
- 정의 하 고 실제 및 가상 네트워크를 제어 하는 정책을 제어합니다 
- 네트워크 정책을 대규모로 일관 되 게 구현

SDN을 사용 하면 전체 인프라 비용을 낮출 수 하는 동안이 모든 작업을 수행할 수 있습니다.



## <a name="contact-the-datacenter-and-cloud-networking-product-team"></a>데이터 센터 및 클라우드 네트워킹 제품 팀에 문의

다양 한 방법 쉽게 가지 Microsoft 또는 다른 SDN 고객을 사용 하 여 SDN 기술 논의 하려는 경우 문의 하세요.

자세한 내용은 [의 데이터 센터 및 클라우드 네트워킹 팀에 문의](contact-sdn-team.md)합니다.
