---
title: 라우터 사전 구성
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
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
ms.openlocfilehash: 6c4f471b6042fb22d74c10663cc38db995a16eb5
ms.sourcegitcommit: 2977c707a299929c6ab0d1e0adab2e1c644b8306
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63720815"
---
# <a name="preconfiguring-a-router"></a>라우터 사전 구성

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

일반적으로 운영 체제를 새로 설치하려면 고객의 내부 네트워크가 인터넷에 연결되도록 인터넷 지원 라우터와 방화벽이 필요합니다. 사전 구성된 서버와 함께 라우터를 부가 가치로 제공하는 경우 사용자가 더 편리하게 이용하도록 라우터를 사전 구성하기 위한 추가적 단계를 거칠 수 있습니다.  
  
 라우터에는 DHCP가 켜져 있어야 합니다. 서버에 하나의 고정 IP 주소를 할당해야 합니다. 이러한 작업은 IP 주소의 DHCP 예약을 통해 수행하거나, DHCP 주소 범위 밖에 있는 IP 주소를 할당하여 수행할 수 있습니다.  
  
 또한 라우터의 포트 전달 설정에서 라우터의 외부 인터페이스에서 내부 네트워크에 있는 서버의 주소로 특정 포트를 전달하도록 사전 구성해야 합니다. 다음 표에 권장 구성이 나와 있습니다.  
  
|구성 설정|설명|  
|---------------------------|-------------|  
|DHCP|켜짐|  
|포트 전달|다음 포트를 서버 주소로 전달해야 합니다.<br /><br /> -80 (호스팅된 구성의 경우 443만 사용)<br />-   443|  
|UPnP 지원|고객에 게 최상의 고객 환경을 간편한 라우터 구성과 설치 중에 제공 UPnP™ 지원을 사용 해야 합니다.<br /><br /> **경고:** UPnP 아키텍처는 사용하도록 설정된 상태로 유지되면 보안 위험에 노출될 수 있습니다.|  
  
 기본 라우터 사전 구성 설정 외에도 다음 작업을 수행하여 라우터 관리를 위해 좀 더 통합된 사용자 환경을 제공할 수 있습니다.  
  
-   서버에서 사용자가 사용자 지정 사용자 인터페이스를 통해 라우터를 관리할 수 있도록 설정하는 추가 기능을 제공하여 대시보드 확장  
  
-   알림 뷰어에 라우터의 알림이 표시될 수 있도록 상태 알림 확장  
  
-   라우터가 여러 서브넷을 지원하면 서버의 IP 주소는 DHCP를 통해 한 개의 DNS 서버로 보냅니다.  
  
-   라우터에 Active DirectoryÂ® Domain Services에 대 한 통합 된 액세스 제어 기능을 있으면 서버의 초기 구성 중 Active Directory 통합을 자동화할 수 있습니다. 또한 대시보드에서 라우터 관리 추가 기능을 통해 이 기능을 제공해야 합니다.  
  
> [!NOTE]
>  무선 연결을 구성하는 방법에 대한 자세한 내용은 [Configure Support for a Wireless Network](Configure-Support-for-a-Wireless-Network.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [Windows Server Essentials ADK 시작 하기](Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [만들기 및 이미지를 사용자 지정](Creating-and-Customizing-the-Image.md)   
 [추가 사용자 지정](Additional-Customizations.md)   
 [배포용 이미지 준비](Preparing-the-Image-for-Deployment.md)   
 [사용자 환경 테스트](Testing-the-Customer-Experience.md)