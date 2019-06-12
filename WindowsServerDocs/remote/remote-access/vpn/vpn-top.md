---
title: VPN(가상 사설망)
description: Windows Server 2016 및 Windows 10 VPN 기능 및 기능에 대해 자세히 알아보려면이 항목에서는 사용할 수 있습니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: cd4908f0-0d6f-4c02-8f98-4dc88c3dcb65
ms.date: 11/05/2018
ms.author: pashort
author: shortpatti
ms.localizationpriority: medium
ms.openlocfilehash: bfd00b7a13e9fad113da1191e7ccd33965223070
ms.sourcegitcommit: 0948a1abff1c1be506216eeb51ffc6f752a9fe7e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/06/2019
ms.locfileid: "66749560"
---
# <a name="virtual-private-networking-vpn"></a>VPN(가상 사설망)

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows 10

## <a name="ras-gateway-as-a-single-tenant-vpn-server"></a>단일 테 넌 트 VPN 서버로 RAS 게이트웨이

Windows Server 2016에서 원격 액세스 서버 역할 다음 관련된 네트워크 액세스 기술의 논리적 그룹화입니다.

- 원격 액세스 서비스 (RAS)
- 라우팅
- 웹 응용 프로그램 프록시

이러한 기술은 원격 액세스 서버 역할의 역할 서비스에 설명 합니다.

추가 역할 및 기능 마법사 또는 Windows PowerShell을 사용 하 여 원격 액세스 서버 역할을 설치할 때에 하나 이상의 이러한 세 가지 역할 서비스를 설치할 수 있습니다.

설치 하는 경우는 **DirectAccess 및 VPN (RAS)** 역할 서비스를 원격 액세스 서비스 게이트웨이 배포 하는 (**RAS 게이트웨이**). RAS 게이트웨이 여러 고급 기능 및 향상 된 기능을 제공 하는 단일 테 넌 트 RAS 게이트웨이 가상 사설망 (VPN) 서버로 배포할 수 있습니다.

>[!NOTE]
>또한 DirectAccess 서버 또는 다중 테 넌 트 VPN 서버로 사용 하 여 네트워킹 SDN (소프트웨어)를 사용 하 여 RAS 게이트웨이 배포할 수 있습니다. 자세한 내용은 [RAS 게이트웨이](https://docs.microsoft.com/windows-server/remote/remote-access/ras-gateway/ras-gateway)를 [소프트웨어 정의 네트워킹 (SDN)](https://docs.microsoft.com/windows-server/networking/sdn/software-defined-networking), 및 [DirectAccess](https://docs.microsoft.com/windows-server/remote/remote-access/directaccess/directaccess)합니다.

## <a name="related-topics"></a>관련 항목
- [Always On VPN 기능과](vpn-map-da.md): 이 항목에서는 Always On VPN의 특징과 기능에 대 한 알아봅니다. 

- [Windows 10의에서 VPN 장치 터널을 구성할](vpn-device-tunnel-config.md): Always On VPN 장치 또는 컴퓨터에 대 한 전용된 VPN 프로필을 만들 수가 있습니다. Always On VPN 연결에는 두 가지 유형의 터널 포함: _장치 터널_ 하 고 _사용자 터널_합니다. 장치 터널 pre-logon 연결 시나리오 및 장치 관리 목적으로 사용 됩니다. 사용자 터널을 사용 하면 VPN 서버를 통해 조직 리소스에 액세스할 수 있습니다.

- [Windows Server 2016 및 Windows 10 용 VPN 배포 무중단](always-on-vpn/deploy/always-on-vpn-deploy.md): 단일 테 넌 트 RAS 게이트웨이 VPN 원격 직원 Always On VPN 연결을 사용 하 여 조직 네트워크에 연결할 수 있도록 지점-사이트 간 VPN 연결에 대 한 원격 액세스를 배포 하는 방법에 지침을 제공 합니다. 각이 배포에 사용 되는 기술에 대 한 디자인 및 배포 가이드를 검토 하는 것이 좋습니다.

- [Windows 10 VPN에 대 한 기술 가이드](https://docs.microsoft.com/windows/access-protection/vpn/vpn-guide): VPN 솔루션을 기업에서 Windows 10 클라이언트 및 배포를 구성 하는 방법에 대 한 결정은 안내 합니다. VPNv2 구성 서비스 공급자 (CSP)에 대 한 참조를 찾을 수 있습니다 하 고이 정보를 모바일 장치 관리 Windows 10 용 Microsoft Intune 및 VPN 프로필 템플릿을 사용 하 여 (MDM) 구성 지침을 제공 합니다.

- [System Center Configuration Manager에서 VPN 프로필을 만드는 방법을](https://docs.microsoft.com/sccm/protect/deploy-use/create-vpn-profiles): 이 항목에서는 System Center Configuration Manager (SCCM)에서 VPN 프로필을 만드는 방법을 알아봅니다.

- [Always On VPN 연결에 Windows 10 클라이언트를 구성](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/vpn-deploy-client-vpn-connections): 이 항목에서는 설명의 ProfileXML 옵션 및 스키마 및 ProfileXML VPN을 만드는 방법. 서버 인프라를 설정한 후 VPN 연결을 사용 하 여 해당 인프라와 통신 하는 Windows 10 클라이언트 컴퓨터를 구성 해야 합니다.

- [VPN 프로필 옵션](https://docs.microsoft.com/windows/access-protection/vpn/vpn-profile-options): 이 항목에서는 Windows 10에서 VPN 프로필 설정에 설명 하 고 SCCM 또는 Intune을 사용 하 여 VPN 프로필을 구성 하는 방법을 알아봅니다. VPNv2 CSP에 ProfileXML 노드를 사용 하 여 Windows 10의 모든 VPN 설정을 구성할 수 있습니다.
