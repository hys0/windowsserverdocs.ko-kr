---
title: QoS에 대 한 질문과 대답
description: 이 항목에서는 Windows Server 2016의 서비스 품질 (QoS) 정책에 대 한 질문과 대답을 제공합니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 74c97a14-b957-4568-b48e-8963a674fdb3
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: f9fb54cc3bda9a259188ae02fb2ef2836dd8718d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59833754"
---
# <a name="qos-policy-frequently-asked-questions"></a>QoS 정책에 대 한 질문과 대답

>적용 대상: Windows Server (반기 채널), Windows Server 2016

다음은-질문과 대답 질문에 – QoS 정책에 대 한 질문과입니다.
  
1.  **내 도메인 컨트롤러에서 QoS 정책을 사용 하 여 실행 되 고 운영 체제 필요 합니까?**
  
     Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 또는 Windows Server 2008

2.  **어떤 운영 체제 사용자 또는 컴퓨터에 QoS 정책 적용을 지원 하나요?**

     사용자 또는 Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows Server 2008 및 Windows Vista를 실행 하는 컴퓨터에 QoS 정책을 적용할 수 있습니다.

3.  **발신자 또는 수신자 트래픽의 QoS 정책을 적용지 않습니다?**

     QoS 정책은 해당 아웃 바운드 트래픽에 영향을 보내는 컴퓨터에 적용 되어야 합니다. 양방향 트래픽을 두 대의 컴퓨터에 영향을 주는 하려면 QoS 정책을 모두 컴퓨터에 적용 되도록 해야 합니다.

4.  **QoS 정책이 충돌 하는 동일한 컴퓨터에 배포 된 경우 어떻게 되나요?**  
  
     여러 정책을 적용 하는 경우 구체적인 QoS 정책이 우선 합니다. 예를 들어 호스트 주소 (192.168.4.12) 하는 정책은 덜 구체적인 네트워크 주소 (192.168.0.0/16) 대신 적용 됩니다. 컴퓨터 수준 및 사용자 수준 정책을 동일한 특이성에 있으면 컴퓨터 수준 QoS 정책 대신 사용자 수준 QoS 정책이 적용 됩니다. 

5.  **기본적으로 사용 하도록 설정 하는 QoS 정책은?**

     아니요, QoS 정책이 기본적으로 사용 되지 않습니다. QoS를 사용 하도록 설정 하려면 수동으로 QoS 정책을 만들어야 합니다.  자세한 내용은 [QoS 정책 관리](qos-policy-manage.md)합니다.

이 가이드의 첫 번째 항목을 참조 하세요 [의 QoS (서비스 품질) 정책을](qos-policy-top.md)합니다.
