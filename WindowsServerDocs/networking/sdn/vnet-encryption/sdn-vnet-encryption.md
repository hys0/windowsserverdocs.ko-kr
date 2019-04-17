---
title: 가상 네트워크 암호화
description: 이 항목에 대해 설명 가상 네트워크 암호화 Windows Server에서 네트워킹 정의 된 소프트웨어에 대 한
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-hv-switch
ms.topic: get-started-article
ms.assetid: 7da0f509-7b02-4a0f-90fb-d97c83a2bc4e
ms.author: pashort
author: grcusanz
ms.openlocfilehash: 425cc1cff8c7241aeec7764b60c89b4586fd323b
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="virtual-network-encryption"></a>가상 네트워크 암호화

>Windows Server에 적용 됩니다.

가상 네트워크 암호화 가상 네트워크 교통 "암호화 활성화"으로 표시 된 서브넷 내 서로 통신할 가상 컴퓨터 간에 암호화 하는 기능을 제공 합니다.

이 기능은 데이터 그램 Transport Layer Security (DTLS) 가상 서브넷 패킷을 암호화를 사용 합니다.  DTLS 방지 도청, 조작 및 위조 실제 네트워크에 액세스할 수 있는 모든 사용자에 게 제공 합니다.

가상 네트워크 암호화 requries 한 암호화 인증서 각각의 SDN에 설치 되어 사용 Hyper-v 호스트 해당 인증서를 및 가상 네트워크의 각 구성 지문을 참조 네트워크 컨트롤러에서 자격 증명 개체 암호화를 요구 서브넷 포함 된.

서브넷에서 암호화가 활성화 되 면 모든 네트워크 교통 해당 서브넷 내 자동으로 암호화 됩니다.  이 외에 조정이 발생할 수도 있습니다 하는 모든 응용 프로그램 수준 암호화 됩니다.  자동으로, 서브넷 교차 서브넷 중으로 표시 된 경우에 암호화 교통 암호화 되지 않은 상태로 전송 됩니다.  또한 가상 네트워크 경계 모든 교통 암호화 되지 않은 상태로 전송 됩니다.

가상 네트워크 암호화 구성에 대 한 참고 [가상 네트워크에 대 한 암호화 구성](sdn-config-vnet-encryption.md)합니다.

암호화 서브넷에만 커뮤니케이션 응용 프로그램 제한 해야 합니다.  현재 서브넷 내 통신할 수 있도록만 액세스 제어 (Acl 목록)을 사용할 수 있습니다.  

액세스 제어 목록 구성에 대 한 참고 [사용 액세스 제어 (Acl 목록) Datacenter 네트워크 교통 이동 관리](../manage/use-acls-for-traffic-flow.md)합니다.