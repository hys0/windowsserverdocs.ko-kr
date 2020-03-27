---
title: VPN(가상 사설망)
description: 이 항목을 사용 하 여 Windows Server 2016 및 Windows 10 VPN 기능에 대해 알아볼 수 있습니다.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: cd4908f0-0d6f-4c02-8f98-4dc88c3dcb65
ms.date: 11/05/2018
ms.author: lizross
author: eross-msft
ms.localizationpriority: medium
ms.openlocfilehash: 55e99d4a02b88a7b5367d3b389237bf96829fd89
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80307801"
---
# <a name="virtual-private-networking-vpn"></a>VPN(가상 사설망)

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows 10

## <a name="ras-gateway-as-a-single-tenant-vpn-server"></a>단일 테 넌 트 VPN 서버로 서의 RAS 게이트웨이

Windows Server 2016에서 원격 액세스 서버 역할은 다음과 같은 관련 네트워크 액세스 기술의 논리적 그룹화입니다.

- RAS (원격 액세스 서비스)
- 라우팅
- 웹 응용 프로그램 프록시

이러한 기술은 원격 액세스 서버 역할의 역할 서비스입니다.

역할 및 기능 추가 마법사 또는 Windows PowerShell을 사용 하 여 원격 액세스 서버 역할을 설치 하는 경우이 세 가지 역할 서비스 중 하나 이상을 설치할 수 있습니다.

**DirectAccess 및 VPN (ras)** 역할 서비스를 설치할 때**Ras Gateway**(원격 액세스 서비스 게이트웨이)를 배포 합니다. 여러 고급 기능 및 향상 된 기능을 제공 하는 단일 테 넌 트 RAS 게이트웨이 VPN (가상 사설망) 서버로 RAS 게이트웨이를 배포할 수 있습니다.

>[!NOTE]
>또한 SDN (소프트웨어 정의 네트워킹) 또는 DirectAccess 서버로 사용할 수 있도록 다중 테 넌 트 VPN 서버로 RAS 게이트웨이를 배포할 수 있습니다. 자세한 내용은 [RAS 게이트웨이](https://docs.microsoft.com/windows-server/remote/remote-access/ras-gateway/ras-gateway), [SDN (소프트웨어 정의 네트워킹)](https://docs.microsoft.com/windows-server/networking/sdn/software-defined-networking)및 [DirectAccess](https://docs.microsoft.com/windows-server/remote/remote-access/directaccess/directaccess)를 참조 하세요.

## <a name="related-topics"></a>관련 항목
- [ALWAYS ON vpn 기능 및 기능](vpn-map-da.md):이 항목에서는 Always On vpn의 기능과 기능에 대해 알아봅니다. 

- [Windows 10에서 Vpn 장치 터널 구성](vpn-device-tunnel-config.md): Always On vpn은 장치 또는 컴퓨터에 대 한 전용 vpn 프로필을 만드는 기능을 제공 합니다. Always On VPN 연결에는 두 가지 유형의 터널 인 _장치 터널_ 및 _사용자 터널이_포함 됩니다. 장치 터널은 사전 로그온 연결 시나리오 및 장치 관리 목적으로 사용 됩니다. 사용자 터널을 통해 사용자는 VPN 서버를 통해 조직 리소스에 액세스할 수 있습니다.

- [Windows Server 2016 및 windows 10 용 ALWAYS ON VPN 배포](always-on-vpn/deploy/always-on-vpn-deploy.md): 원격 직원이 Always On vpn 연결을 사용 하 여 조직 네트워크에 연결할 수 있도록 하는 지점 및 사이트 간 vpn 연결에 대 한 단일 테 넌 트 Vpn RAS 게이트웨이로 원격 액세스를 배포 하는 방법에 대 한 지침을 제공 합니다. 이 배포에 사용 되는 각 기술에 대 한 디자인 및 배포 가이드를 검토 하는 것이 좋습니다.

- [Windows 10 Vpn 기술 가이드](https://docs.microsoft.com/windows/access-protection/vpn/vpn-guide): 엔터프라이즈 vpn 솔루션의 windows 10 클라이언트에 대해 결정 하는 사항 및 배포를 구성 하는 방법을 안내 합니다. VPNv2 CSP (구성 서비스 공급자)에 대 한 참조를 찾을 수 있으며 Microsoft Intune 및 Windows 10 용 VPN 프로필 템플릿을 사용 하 여 MDM (모바일 장치 관리) 구성 지침을 제공 합니다.

- [Configuration Manager에서 vpn 프로필을 만드는 방법](https://docs.microsoft.com/configmgr/protect/deploy-use/create-vpn-profiles):이 항목에서는 CONFIGURATION MANAGER에서 vpn 프로필을 만드는 방법에 대해 알아봅니다.

- [Windows 10 클라이언트 ALWAYS ON VPN 연결 구성](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/vpn-deploy-client-vpn-connections):이 항목에서는 프로 파일링 옵션 및 스키마에 대해 설명 하 고 PROFILEXML VPN을 만드는 방법을 설명 합니다. 서버 인프라를 설정한 후에는 VPN 연결을 사용 하 여 해당 인프라와 통신 하도록 Windows 10 클라이언트 컴퓨터를 구성 해야 합니다.

- [Vpn 프로필 옵션](https://docs.microsoft.com/windows/access-protection/vpn/vpn-profile-options):이 항목에서는 Windows 10의 vpn 프로필 설정에 대해 설명 하 고 Intune 또는 Configuration Manager를 사용 하 여 vpn 프로필을 구성 하는 방법을 알아봅니다. VPNv2 CSP의 프로 파일링 노드를 사용 하 여 Windows 10의 모든 VPN 설정을 구성할 수 있습니다.
