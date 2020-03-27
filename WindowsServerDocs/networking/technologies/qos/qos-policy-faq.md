---
title: QoS 질문과 대답
description: 이 항목에서는 Windows Server 2016의 QoS (서비스 품질) 정책에 대 한 질문에 대 한 대답을 제공 합니다.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 74c97a14-b957-4568-b48e-8963a674fdb3
manager: brianlic
ms.author: lizross
author: eross-msft
ms.openlocfilehash: a2b0990bd1416032cd519c60878c389f391e053d
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80315533"
---
# <a name="qos-policy-frequently-asked-questions"></a>QoS 정책 faq (질문과 대답)

>적용 대상: Windows Server(반기 채널), Windows Server 2016

다음은 QoS 정책에 대 한 질문과 대답 (질문과 대답)입니다.
  
1.  **도메인 컨트롤러가 QoS 정책을 사용 하기 위해 실행 해야 하는 운영 체제는 무엇 인가요?**
  
     Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 또는 Windows Server 2008

2.  **사용자 또는 컴퓨터에 대 한 QoS 정책 응용 프로그램을 지 원하는 운영 체제는 무엇 인가요?**

     Windows Server 2016, windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows Server 2008 및 Windows Vista를 실행 하는 사용자 또는 컴퓨터에 QoS 정책을 적용할 수 있습니다.

3.  **QoS 정책이 트래픽의 발신자 또는 수신자에 게 적용 되나요?**

     아웃 바운드 트래픽에 영향을 주기 위해 전송 컴퓨터에 QoS 정책을 적용 해야 합니다. 두 컴퓨터의 양방향 트래픽에 영향을 주려면 QoS 정책을 두 컴퓨터에 모두 적용 해야 합니다.

4.  **충돌 하는 QoS 정책을 동일한 컴퓨터에 배포 하는 경우 어떻게 되나요?**  
  
     여러 정책이 적용 되는 경우 더 구체적인 QoS 정책이 우선적으로 적용 됩니다. 예를 들어 호스트 주소 (192.168.4.12)를 명시 하는 정책은 더 작은 특정 네트워크 주소 (192.168.0.0/16) 대신 적용 됩니다. 컴퓨터 수준 및 사용자 수준 정책에 동일한 특이성 있는 경우 컴퓨터 수준 QoS 정책 대신 사용자 수준 QoS 정책이 적용 됩니다. 

5.  **QoS 정책이 기본적으로 사용 하도록 설정 되어 있습니까?**

     아니요, QoS 정책은 기본적으로 사용 되지 않습니다. Qos를 사용 하도록 설정 하려면 수동으로 QoS 정책을 만들어야 합니다.  자세한 내용은 [QoS 정책 관리](qos-policy-manage.md)를 참조 하세요.

이 가이드의 첫 번째 항목은 [QoS (서비스 품질) 정책](qos-policy-top.md)을 참조 하세요.
