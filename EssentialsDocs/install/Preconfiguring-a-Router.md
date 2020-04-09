---
title: 라우터 사전 구성
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: 9153ac90-bb0c-4b8d-93b2-e2121ed13636
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: c39bf3ac260a23b7fc9cc9feec7f34786b1e8aae
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80819946"
---
# <a name="preconfiguring-a-router"></a>라우터 사전 구성

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

일반적으로 운영 체제를 새로 설치하려면 고객의 내부 네트워크가 인터넷에 연결되도록 인터넷 지원 라우터와 방화벽이 필요합니다. 사전 구성된 서버와 함께 라우터를 부가 가치로 제공하는 경우 사용자가 더 편리하게 이용하도록 라우터를 사전 구성하기 위한 추가적 단계를 거칠 수 있습니다.  
  
 라우터에는 DHCP가 켜져 있어야 합니다. 서버에 하나의 고정 IP 주소를 할당해야 합니다. 이러한 작업은 IP 주소의 DHCP 예약을 통해 수행하거나, DHCP 주소 범위 밖에 있는 IP 주소를 할당하여 수행할 수 있습니다.  
  
 또한 라우터의 포트 전달 설정에서 라우터의 외부 인터페이스에서 내부 네트워크에 있는 서버의 주소로 특정 포트를 전달하도록 사전 구성해야 합니다. 다음 표에 권장 구성이 나와 있습니다.  
  
|구성 설정|세부 정보|  
|---------------------------|-------------|  
|DHCP|켜짐|  
|포트 전달|다음 포트를 서버 주소로 전달해야 합니다.<br /><br /> -80 (hosted 구성의 경우 443만 사용)<br />-443|  
|UPnP 지원|설치 하는 동안 고객에 게 가장 쉬운 라우터 구성과 최상의 고객 환경을 제공 하려면 UPnP 지원을 사용 하도록 설정 해야 합니다.<br /><br /> **경고:** UPnP 아키텍처를 사용 하는 경우 보안 위험이 발생할 수 있습니다.|  
  
 기본 라우터 사전 구성 설정 외에도 다음 작업을 수행하여 라우터 관리를 위해 좀 더 통합된 사용자 환경을 제공할 수 있습니다.  
  
-   서버에서 사용자가 사용자 지정 사용자 인터페이스를 통해 라우터를 관리할 수 있도록 설정하는 추가 기능을 제공하여 대시보드 확장  
  
-   알림 뷰어에 라우터의 알림이 표시될 수 있도록 상태 알림 확장  
  
-   라우터가 여러 서브넷을 지원하면 서버의 IP 주소는 DHCP를 통해 한 개의 DNS 서버로 보냅니다.  
  
-   라우터에 Active Directory&reg; 도메인 서비스에 대해 통합 된 액세스 제어 기능이 있는 경우 서버의 초기 구성 중에 Active Directory 통합을 자동화할 수 있습니다. 또한 대시보드에서 라우터 관리 추가 기능을 통해 이 기능을 제공해야 합니다.  
  
> [!NOTE]
>  무선 연결 구성에 대한 자세한 내용은 [무선 네트워크 지원 구성](Configure-Support-for-a-Wireless-Network.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [Windows Server ESSENTIALS ADK를 사용 하 여 시작](Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [이미지  만들기 및 사용자 지정](Creating-and-Customizing-the-Image.md)  
 [추가 사용자 지정](Additional-Customizations.md)   
 [배포할 이미지를 준비 하는 중](Preparing-the-Image-for-Deployment.md)   
 [사용자 환경 테스트](Testing-the-Customer-Experience.md)