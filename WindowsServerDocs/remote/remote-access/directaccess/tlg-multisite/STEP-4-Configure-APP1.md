---
title: 4 단계 APP1 구성
description: 이 항목은 테스트 랩 가이드-Windows Server 2016에 대 한 DirectAccess 멀티 사이트 배포 시연의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7000e80f-31b1-43c5-b51e-1469d26909e5
ms.author: pashort
author: shortpatti
ms.openlocfilehash: dc4715fcec778d1fa63ff84e801961572b9cd589
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404785"
---
# <a name="step-4-configure-app1"></a>4 단계 APP1 구성

>적용 대상: Windows Server(반기 채널), Windows Server 2016

2 Corpnet 서브넷에 대 한 APP1 액세스를 사용할 수 있도록 정적 IPv6 주소 지정 및 게이트웨이 설정을 구성 합니다.  
  
- 기본 게이트웨이 및 DNS 서버를 구성 합니다. 멀티 사이트 구성에서는 ROUTER1 컴퓨터를 기본 게이트웨이로 사용 합니다. APP1에 기본 게이트웨이를 구성 합니다.  
  
## <a name="to-configure-the-default-gateway-and-dns-server"></a>기본 게이트웨이 및 DNS 서버를 구성 하려면  
  
1.  서버 관리자 콘솔에서 **로컬 서버**를 클릭 한 다음 **속성** 영역에서 **유선 이더넷 연결**옆에 있는 링크를 클릭 합니다.  
  
2.  **네트워크 연결** 창에서 **유선 이더넷 연결**을 마우스 오른쪽 단추로 클릭 한 다음 **속성**을 클릭 합니다.  
  
3.  **유선 이더넷 연결 속성** 대화 상자에서 **인터넷 프로토콜 버전 4 (TCP/IPv4)** 를 클릭 한 다음 **속성**을 클릭 합니다.  
  
4.  **기본 게이트웨이에서** **10.0.0.254**를 입력 하 고 **대체 DNS 서버**에 **10.2.0.1**를 입력 한 다음 **확인**을 클릭 합니다.  
  
5.  **유선 이더넷 연결 속성** 대화 상자에서 **인터넷 프로토콜 버전 6 (TCP/IPv6)** 을 클릭 한 다음 **속성**을 클릭 합니다.  
  
6.  **기본 게이트웨이에서** **2001: db8:1:: fe**를 입력 합니다. **대체 DNS 서버**에 **2001: db8:2:: 1**을 입력 한 다음 **확인**을 클릭 합니다.  
  
7.  **유선 이더넷 연결 속성** 대화 상자에서 **닫기**를 클릭 한 다음 **네트워크 연결** 창을 닫습니다.  
  


