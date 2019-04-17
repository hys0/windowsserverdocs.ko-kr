---
title: "라우터 미리 구성"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9153ac90-bb0c-4b8d-93b2-e2121ed13636
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 7dc66c8a439552c2087d0348b0115adba04027ee
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="preconfiguring-a-router"></a>라우터 미리 구성

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

일반적으로 인터넷 가능 라우터와 방화벽 고객의 내부 네트워크에 인터넷에 연결을 운영 체제를 새로 설치 해야 합니다. 미리 구성 된 서버 추가 값으로 라우터를 제공 하는 경우 사용자 환경 개선을 위해 라우터 미리에 추가 단계를 수행할 수 있습니다.  
  
 라우터에서 DHCP 켜져 있어야 합니다. 서버에서 고정 IP 주소를 할당 되어야 합니다. IP 주소 DHCP 예약 하거나를 DHCP 주소 범위를 벗어나는 IP 주소를 지정 하 여 수행할 수 있습니다.  
  
 또한 전달 내부 네트워크에 서버의 주소를 라우터의 외부 인터페이스에서 특정 포트 전달 하는 라우터에 설정을 포트를 미리 해야 합니다. 다음 표에서 구성 것이 좋습니다.  
  
|구성 설정|세부 정보|  
|---------------------------|-------------|  
|DHCP|에서|  
|포트 전달|다음 포트 서버의 주소를 전달 합니다.<br /><br /> -80 (호스팅된 구성 사용 443만)<br />-   443|  
|UPnP 지원|설치 하는 동안 고객과 최상의 고객이 환경에 대 한 간단한 라우터 구성 제공 하기 위해 UPnP™ 지원을 사용 해야 합니다.<br /><br /> **경고:** UPnP 건축물과 왼쪽 설정 되어 있는 경우 보안 위험이 발생할 수 있습니다.|  
  
 기본 라우터 미리 구성 설정을 뿐 아니라 라우터 관리 하기 위한 더 통합된 사용자 경험을 제공 하기 위해 다음과 같은 작업을 수행할 수 있습니다.  
  
-   사용자 지정 사용자 인터페이스를 통해 라우터에 관리할 수 있도록 하는 서버에 추가 기능을 제공 하 여 대시보드를 확장 합니다.  
  
-   라우터에서 경고 알림 뷰어에서 볼 수 있도록 상태 경고를 확장 합니다.  
  
-   라우터 여러 서브넷을 지 원하는 경우 DHCP 통해 한 DNS 서버 서버의 IP 주소 인계 받았을 해야 합니다.  
  
-   라우터 활성 DirectoryÂ® 도메인 서비스에 대 한 통합된 액세스 제어 기능을는, Active Directory 통합 초기 구성 하는 동안 서버 자동 수 있습니다. 이 기능은 라우터 관리 추가 기능을 대시보드에 통해 노출도 해야 합니다.  
  
> [!NOTE]
>  무선 연결을 구성에 대 한 자세한 내용은 참조 [무선 네트워크에 대 한 지원을 구성](Configure-Support-for-a-Wireless-Network.md)합니다.  
  
## <a name="see-also"></a>참조 하십시오  
 [Windows Server Essentials ADK 시작](Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [만들기 및 이미지를 사용자 지정](Creating-and-Customizing-the-Image.md)   
 [추가로 사용자 지정](Additional-Customizations.md)   
 [배포에 대 한 이미지를 준비 중](Preparing-the-Image-for-Deployment.md)   
 [고객 만족도 테스트합니다.](Testing-the-Customer-Experience.md)