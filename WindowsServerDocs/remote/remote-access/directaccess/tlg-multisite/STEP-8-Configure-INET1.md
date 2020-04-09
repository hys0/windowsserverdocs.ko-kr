---
title: 8 단계 INET1 구성
description: 이 항목은 테스트 랩 가이드-Windows Server 2016에 대 한 DirectAccess 멀티 사이트 배포 시연의 일부입니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-da
ms.topic: article
ms.assetid: 693acb5c-dffc-4484-8286-163bb67724c9
ms.author: coreyp
author: coreyp-at-msft
ms.openlocfilehash: ca8a49e612bef9c4a72c47e8d0e147a900686f84
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861546"
---
# <a name="step-8-configure-inet1"></a>8 단계: INET1 구성

>적용 대상: Windows Server(반기 채널), Windows Server 2016

인터넷을 통해 원격 액세스 서버에 연결 하려면 클라이언트 컴퓨터를 설정 하려면 INET1에 EDGE1 2에 대 한 DNS 항목을 구성 해야 합니다.  
  
### <a name="to-create-the-2-edge1-dns-entry"></a>2-EDGE1 DNS 항목을 만들려면  
  
1.  에 **시작** 화면에서 입력**dnsmgmt.msc**, 한 다음 ENTER를 누릅니다.  
  
2.  콘솔 트리에서 엽니다 **정방향 조회 영역**, 클릭 **contoso.com**, 마우스 오른쪽 단추로 클릭 **contoso.com**, 를 클릭 하 고 **새 호스트 (A 또는 AAAA)** .  
  
3.  **이름**, 형식 **2 EDGE1**합니다. **IP 주소**, 형식 **131.107.0.20**합니다. **호스트 추가**, **확인**, **완료**를 차례로 클릭합니다.  
  


