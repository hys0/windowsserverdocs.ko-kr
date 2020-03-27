---
title: 엔터프라이즈에 원격 액세스 배포
description: 이 항목에서는 엔터프라이즈에 대 한 Windows Server 2016의 DirectAccess 시나리오를 소개 합니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4781df0a-158b-4562-b8f5-32b27615a4f8
ms.author: lizross
author: eross-msft
ms.openlocfilehash: aebdbd02ebe256872b52e794c755e0d590b175a5
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80308472"
---
# <a name="deploy-remote-access-in-an-enterprise"></a>엔터프라이즈에 원격 액세스 배포

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목에서는 엔터프라이즈에 대한 DirectAccess 시나리오를 소개합니다.  
  
  
> [!IMPORTANT]  
> 이 가이드를 사용 하 여 DirectAccess를 배포 하려면 Windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012를 실행 하는 DirectAccess 서버를 사용 해야 합니다.  
  
## <a name="before-you-begin-deploying-see-the-list-of-unsupported-configurations-known-issues-and-prerequisites"></a>배포를 시작하기 전에 지원되지 않는 구성, 알려진 문제 및 사전 요구 사항 목록을 참조하세요.  
  
-   [DirectAccess에서 지원되지 않는 구성](https://technet.microsoft.com/windows-server-docs/networking/remote-access/directaccess/directaccess-unsupported-configurations)  
  
-   [DirectAccess 알려진 문제](https://technet.microsoft.com/windows-server-docs/networking/remote-access/directaccess/directaccess-known-issues)  
  
-   [DirectAccess를 배포 하기 위한 필수 구성 요소](https://technet.microsoft.com/windows-server-docs/networking/remote-access/directaccess/prerequisites-for-deploying-directaccess)  
  
## <a name="scenario-description"></a><a name="BKMK_OVER"></a>시나리오 설명  
원격 액세스에는 Windows NLB(네트워크 부하 분산) 또는 외부 부하 분산 장치를 사용하여 부하가 분산된 클러스터에 여러 원격 액세스 서버를 배포하고, 원격 액세스 서버가 여러 장소에 배치되는 멀티 사이트 배포를 설정하며, OTP(1회용 암호)를 사용하여 2단계 클라이언트 인증을 통해 DirectAccess를 배포하는 등 다양한 엔터프라이즈 기능이 포함되어 있습니다.  
  
## <a name="in-this-scenario"></a>이 시나리오의 내용  
각 엔터프라이즈 시나리오에 대해서는 계획 및 배포 지침이 포함된 문서에서 설명합니다. 참조 항목:  
  
-   [클러스터에 원격 액세스 배포](cluster/Deploy-Remote-Access-In-Cluster.md)  
  
-   [멀티 사이트 배포에서 여러 원격 액세스 서버 배포](multisite/Deploy-Multiple-Remote-Access-Servers-in-a-Multisite-Deployment.md)  
  
-   [OTP 인증을 통한 원격 액세스 배포](otp/Deploy-RA-OTP.md)  
  
-   [다중 포리스트 환경에 원격 액세스 배포](multi-forest/Deploy-Remote-Access-in-a-Multi-Forest-Environment.md)  
  
## <a name="practical-applications"></a><a name="BKMK_APP"></a>실용적인 응용 프로그램  
원격 액세스 엔터프라이즈 시나리오의 경우 다음과 같은 이점이 있습니다.  
  
-   **가용성 향상**. 클러스터에 여러 원격 액세스 서버를 배포 하면 확장성을 제공 하 고 처리량 및 사용자 수에 대 한 용량을 늘립니다. 클러스터의 부하 분산을 통해 고가용성을 제공합니다. 클러스터의 한 서버에서 실패할 경우 원격 사용자가 클러스터의 다른 서버를 통해 내부 회사 네트워크에 지속적으로 액세스할 수 있습니다. 클라이언트가 VIP(가상 IP) 주소를 사용하여 클러스터에 연결하므로 장애 조치(failover)가 투명합니다.  
  
-   **관리 용이성**. 클러스터 서버 중 하나에서 실행 되는 원격 액세스 관리 콘솔을 사용 하 여 클러스터 또는 멀티 사이트 배포를 단일 엔터티로 구성 하 고 관리할 수 있습니다. 또한 멀티 사이트 배포를 사용하면 관리자가 원격 액세스 배포를 여러 Active Directory 사이트에 맞춰 배포할 수 있으므로 아키텍처가 간소화됩니다. 공유 설정은 클러스터 서버 전반 또는 모든 멀티 사이트 진입점 서버에서 설정할 수 있습니다. 원격 액세스 설정은 클러스터나 배포에 있는 임의의 서버에서 관리하거나 RSAT(원격 서버 관리 도구)를 원격으로 사용하여 관리할 수 있습니다. 또한 전체 클러스터나 멀티 사이트 배포는 단일 원격 액세스 관리 콘솔에서 모니터링할 수 있습니다.  
  
-   **비용 효율성**. 원격 액세스 멀티 사이트 배포를 통해 기업은 클라이언트 위치에 해당 하는 여러 사이트에 원격 액세스 서버를 배포할 수 있습니다. 이에 따라 위치에 관계없이 원격 클라이언트의 액세스 환경을 예측할 수 있으며, 인터넷을 통해 클라이언트 트래픽을 가장 가까운 원격 액세스 서버로 라우팅하여 비용과 인트라넷 대역폭을 절감할 수 있습니다.  
  
-   **보안**. 표준 Active Directory 암호 대신 OTP (일회성 암호)를 사용 하 여 강력한 클라이언트 인증을 배포 하면 보안이 강화 됩니다.  
  
## <a name="roles-and-features-included-in-this-scenario"></a><a name="BKMK_NEW"></a>이 시나리오에 포함 된 역할 및 기능  
다음 표에는 엔터프라이즈 시나리오에 사용되는 역할 및 기능이 나와 있습니다.  
  
|역할/기능|이 시나리오를 지원하는 방법|  
|---------|-----------------|  
|원격 액세스 서버 역할|이 역할은 서버 관리자 콘솔을 사용하여 설치 및 제거됩니다. 이 역할에는 DirectAccess(이전의 Windows Server 2008 R2 기능)와 라우팅 및 원격 액세스 서비스(이전의 NPAS(네트워크 정책 및 액세스 서비스) 서버 역할의 역할 서비스)가 모두 포함되어 있습니다. 원격 액세스 역할은 다음의 두 가지 구성 요소로 구성됩니다.<br /><br />1. DirectAccess 및 RRAS (라우팅 및 원격 액세스 서비스) VPN-DirectAccess와 VPN은 원격 액세스 관리 콘솔에서 함께 관리 됩니다.<br />2. RRAS 라우팅-RRAS 라우팅 기능은 레거시 라우팅 및 원격 액세스 콘솔에서 관리 됩니다.<br /><br />원격 액세스 서버 역할은 다음과 같은 서버 기능에 종속됩니다.<br /><br />-인터넷 정보 서비스 (IIS)-이 기능은 네트워크 위치 서버와 기본 웹 프로브를 구성 하는 데 필요 합니다.<br />-그룹 정책 관리 콘솔 기능은 DirectAccess가 Active Directory에서 Gpo (그룹 정책 개체)를 만들고 관리 하는 데 필요 하며, 서버 역할에 필요한 기능으로 설치 되어 있어야 합니다.|  
|원격 액세스 관리 도구 기능|이 기능은 다음과 같이 설치됩니다.<br /><br />-이 값은 원격 액세스 역할이 설치 되어 있고 원격 관리 콘솔 사용자 인터페이스를 지 원하는 때 기본적으로 원격 액세스 서버에 설치 됩니다.<br />-앱는 하지 원격 액세스 서버 역할을 실행 하는 서버에 필요에 따라 설치 수 있습니다. 이 경우 이 기능은 DirectAccess 및 VPN을 실행하는 원격 액세스 컴퓨터를 원격으로 관리하는 데 사용됩니다.<br /><br />원격 액세스 관리 도구 기능의 구성 요소는 다음과 같습니다.<br /><br />1. 원격 액세스 GUI 및 명령줄 도구<br />2. Windows PowerShell 용 원격 액세스 모듈<br /><br />이 기능은 다음 요소에 종속됩니다.<br /><br />1. 그룹 정책 관리 콘솔<br />2. RAS CMAK (연결 관리자 관리 키트)<br />3. Windows PowerShell 3.0<br />4. 그래픽 관리 도구 및 인프라|  
|Windows NLB|이 기능을 사용하면 여러 원격 액세스 서버에 부하를 분산할 수 있습니다.|  
  

  


