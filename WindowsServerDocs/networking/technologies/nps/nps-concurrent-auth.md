---
title: 동시 인증 NPS에 의해 처리 늘리기
description: 이 항목 Windows Server 2016에 네트워크 정책 서버 동시 인증 구성에 대해 설명 합니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 2d9cdada-0625-41c8-8248-a32259b03e47
ms.author: pashort
author: shortpatti
ms.openlocfilehash: aa70c1a26e2c22d26545e1b46a6151d71a2b4095
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="increase-concurrent-authentications-processed-by-nps"></a>동시 인증 NPS에 의해 처리 늘리기

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

네트워크 정책 서버 동시 인증 구성에 대 한 내용은이 항목을 사용할 수 있습니다.

네트워크 정책 서버 \(NPS\) 도메인 컨트롤러 아닌 다른 컴퓨터에 설치한 경우 NPS 서버 인증 요청 초당 많은 수신 허용 NPS 서버와 도메인 컨트롤러 동시 인증 수가 증가 하 여 NPS 성능을 개선할 수 있습니다.

이렇게 하려면 다음 레지스트리 키를 편집 해야 합니다. 

`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Netlogon\Parameters`

라는 새로운 가치 **MaxConcurrentApi** 2-5에서에서 값을을 할당 합니다. 

>[!CAUTION]
>할당 값을 하는 경우 **MaxConcurrentApi** 너무 높게, NPS 서버 과도 한 로드 도메인 컨트롤러에 배치 될 수 있습니다.

NPS 관리에 대 한 자세한 내용은 참조 [네트워크 정책 서버 관리](nps-manage-top.md)합니다.

NPS에 대 한 자세한 내용은 참조 [네트워크 NPS 정책 서버 ()](nps-top.md)합니다.