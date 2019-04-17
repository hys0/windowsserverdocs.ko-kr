---
title: QoS 질문과 대답
description: 이 항목에서는 Windows Server 2016 서비스의 품질 (QoS) 정책에 대 한 질문과 대답을 확인 합니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 74c97a14-b957-4568-b48e-8963a674fdb3
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: e63cd00a2016411e9f2c532c0e4c301dabdfd816
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="qos-policy-frequently-asked-questions"></a>QoS 정책에 대 한 질문과 대답

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

다음은 질문과-– QoS 정책에 대 한 이러한 질문에 대답 합니다.
  
1.  **내 도메인 컨트롤러에서 QoS 정책을 사용 하 여 실행 하려면 어떤 운영 체제가 필요 합니까?**
  
     Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 또는 Windows Server 2008

2.  **어떤 운영 체제 지원 QoS 정책 사용자 또는 컴퓨터에 적용 되나요?**

     QoS 정책을 사용자 또는 Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows Server 2008 및 Windows Vista를 실행 하는 컴퓨터에 적용할 수 있습니다.

3.  **QoS 정책을 하려면 보낸 사람 또는 트래픽 수신기에 적용 되나요?**

     QoS 정책은 해당 아웃 바운드 교통에 영향을 보내는 컴퓨터에서 적용 해야 합니다. 두 대의 컴퓨터의 양방향 교통에 영향을 위해 QoS 정책을 두 컴퓨터에 적용할 수 해야 합니다.

4.  **QoS 정책이 충돌 하는 동일한 컴퓨터에 배포 되는 경우 어떻게 되나요?**  
  
     여러 정책이 적용 구체적인 QoS 정책 우선 합니다. 예를 들어 정책 호스트 상태 (192.168.4.12 주소는) 적용 대신는 자세 네트워크 주소 (192.168.0.0/16). 컴퓨터 수준 및 사용자 수준 정책을 사용 하는 동일한 특이성 경우 컴퓨터 수준의 QoS 정책 하는 대신 사용자 수준 QoS 정책이 적용 됩니다. 

5.  **QoS 정책 기본적으로 사용할 수 있나요?**

     아니요, QoS 정책은 기본적으로 사용할 수 없습니다. 수동으로 QoS 수 있도록 QoS 정책 만들어야 합니다.  자세한 내용은 참조 [QoS 정책 관리](qos-policy-manage.md)합니다.

이 가이드의 첫 번째 항목을 참조 하세요. [(QoS) 서비스 품질 정책](qos-policy-top.md)합니다.
