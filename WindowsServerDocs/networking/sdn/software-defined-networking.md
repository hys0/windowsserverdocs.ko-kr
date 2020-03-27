---
title: SDN(소프트웨어 정의 네트워킹)
description: SDN(소프트웨어 방식 네트워킹)은 데이터 센터의 라우터, 스위치 및 게이트웨이 같은 실제 및 가상 네트워크 디바이스를 중앙에서 구성하고 관리하는 방법을 제공합니다. 이 항목을 사용 하 여 Windows Server, System Center 및 Microsoft Azure에 제공 된 SDN (소프트웨어 정의 네트워킹) 기술에 대해 알아봅니다.
manager: dougkim
ms.prod: windows-server
ms.technology: networking-sdn
ms.topic: article
ms.assetid: 9a1ea73c-20cd-42c5-95ad-b003b9cc6d64
ms.author: lizross
author: eross-msft
ms.date: 08/09/2018
ms.openlocfilehash: a1283c6afcebe7b6abc12f9847865d6305bd3f2c
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80317274"
---
# <a name="sdn-in-windows-server-overview"></a>Windows Server의 SDN 개요

>적용 대상: Windows Server(반기 채널), Windows Server 2016


SDN(소프트웨어 방식 네트워킹)은 데이터 센터의 라우터, 스위치 및 게이트웨이 같은 실제 및 가상 네트워크 디바이스를 중앙에서 구성하고 관리하는 방법을 제공합니다. 기존 SDN 호환 장치를 사용 하 여 가상 네트워크와 실제 네트워크 간의 긴밀 한 통합을 구현할 수 있습니다. Hyper-v 가상 스위치, Hyper-v 네트워크 가상화, RAS 게이트웨이 등의 가상 네트워크 요소는 SDN 인프라의 필수적인 요소가 되도록 설계 되었습니다. 

>[!Note]
>네트워크 컨트롤러 및 소프트웨어 부하 분산 노드와 같은 SDN 인프라 서버를 실행 하는 hyper-v 호스트 및 Vm (가상 컴퓨터)에는 Windows Server 2016 Datacenter edition이 설치 되어 있어야 합니다. 
>
>SDN 제어 네트워크에 연결 된 테 넌 트 워크 로드 Vm만 포함 하는 hyper-v 호스트는 Windows Server 2016 Standard edition을 사용할 수 있습니다.

네트워크 평면이 네트워크 장치 자체에 더 이상 바인딩되지 않으므로 SDN이 가능 합니다. 그러나 System Center 2016와 같은 데이터 센터 관리 소프트웨어 등의 다른 엔터티는 네트워크 비행기를 사용 합니다. SDN을 사용 하면 데이터 센터 네트워크를 동적으로 관리 하 여 응용 프로그램 및 작업의 요구 사항을 충족 하는 자동화 되 고 중앙 집중화 된 방법을 제공할 수 있습니다. 

SDN을 사용 하 여 다음을 수행할 수 있습니다.

- 응용 프로그램의 진화 하는 요구에 맞게 동적으로 네트워크를 만들고, 보호 하 고, 연결
- 방해가 되지 않는 방식으로 워크 로드 배포 속도 향상
- 네트워크를 통해 확산 되는 보안 취약성 포함
- 실제 및 가상 네트워크를 모두 제어 하는 정책 정의 및 제어 
- 일관 되 게 대규모로 네트워크 정책 구현

SDN을 사용 하면 전체 인프라 비용을 줄일 수 있을 뿐만 아니라이 모든 것을 수행할 수 있습니다.



## <a name="contact-the-datacenter-and-cloud-networking-product-team"></a>데이터 센터 및 클라우드 네트워킹 제품 팀에 문의

Microsoft 또는 다른 SDN 고객과 SDN 기술을 논의 하는 데 관심이 있는 경우 연락처를 만들 수 있는 다양 한 방법이 있습니다.

자세한 내용은 [데이터 센터 및 클라우드 네트워킹 팀에 문의](contact-sdn-team.md)를 참조 하세요.
