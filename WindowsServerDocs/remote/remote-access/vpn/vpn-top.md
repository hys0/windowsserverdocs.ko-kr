---
title: VPN(가상 사설망)
description: Windows Server 2016 및 Windows 10 VPN 특징과 기능에 대해 자세히 알아보려면이 항목에서는 사용할 수 있습니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: cd4908f0-0d6f-4c02-8f98-4dc88c3dcb65
ms.date: 11/05/2018
ms.author: pashort
author: shortpatti
ms.localizationpriority: medium
ms.openlocfilehash: bf38995f0a2b396044d1f45b45eff8c3c2de329d
ms.sourcegitcommit: 4893d79345cea85db427224bb106fc1bf88ffdbc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2018
ms.locfileid: "6067305"
---
# 가상 사설망 \(VPN\) 네트워킹

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows 10

## 단일 테 넌 트를 VPN 서버로 RAS 게이트웨이

Windows Server 2016 원격 액세스 서버 역할은 다음과 같은 관련된 네트워크 액세스 기술을 논리적 그룹.

- 원격 액세스 서비스 (RAS)
- 라우팅
- 웹 응용 프로그램 프록시

이러한 기술을 원격 액세스 서버 역할의 역할 서비스입니다.

추가 역할 및 기능 마법사 또는 Windows PowerShell을 사용 하 여 원격 액세스 서버 역할을 설치할 때 이러한 세 가지 역할 서비스 중 하나 이상을 설치할 수 있습니다.

원격 액세스 서비스 게이트웨이 배포 하는 **DirectAccess, VPN (RAS)** 역할 서비스를 설치 하면 \ (**RAS 게이트웨이**\). RAS 게이트웨이 많은 고급 기능 및 향상 기능을 제공 하는 단일 테 넌 트 RAS 게이트웨이 가상 사설망 \(VPN\) 서버도 배포할 수 있습니다.

>[!NOTE]
>소프트웨어 정의 네트워킹 \(SDN\)와 함께 사용에 대 한 다중 테 넌 트 VPN 서버 또는 DirectAccess 서버 RAS 게이트웨이 배포할 수도 있습니다. 자세한 내용은 [RAS 게이트웨이](https://docs.microsoft.com/windows-server/remote/remote-access/ras-gateway/ras-gateway), [소프트웨어 정의 네트워킹 (SDN)](https://docs.microsoft.com/windows-server/networking/sdn/software-defined-networking)및 [DirectAccess](https://docs.microsoft.com/windows-server/remote/remote-access/directaccess/directaccess)를 참조 하세요.

## 관련 항목
- [Always On VPN 특징과 기능](vpn-map-da.md):이 항목에서는 Always On VPN 특징과 기능에 대 한 설명입니다. 

- [Windows 10의 VPN 장치 터널 구성](vpn-device-tunnel-config.md): Always On VPN 장치 또는 컴퓨터에 대 한 전용된 VPN 프로필을 만들 수는 기능을 제공 합니다. Always On VPN 연결에는 두 가지 유형의 터널 포함: _장치 터널_ 및 _사용자 터널_합니다. 장치 터널 pre-logon 연결 시나리오 및 장치 관리 목적으로 사용 됩니다. 사용자 터널 VPN 서버를 통해 조직의 리소스에 액세스할 수 있습니다.

- [항상에서 VPN 배포에 대 한 Windows Server 2016 및 Windows 10](always-on-vpn/deploy/always-on-vpn-deploy.md): 단일 장치로 원격 액세스 배포에 대 한 지침이 VPN RAS 게이트웨이 원격 작업자 조직에 연결을 허용 하는 중간 to\ 사이트 VPN 연결에 대 한 테 넌 트를 제공 합니다. Always On VPN 연결을 통해 네트워크입니다. 각이 배포에 사용 되는 기술에 대 한 디자인 및 배포 가이드를 검토 하는 것이 좋습니다.

- [Windows10 VPN 기술 가이드](https://docs.microsoft.com/windows/access-protection/vpn/vpn-guide): 엔터프라이즈 VPN 솔루션 및 배포를 구성 하는 방법에 대 한 Windows 10 클라이언트 결정할 단계별로 안내 합니다. VPNv2 구성 서비스 공급자 (CSP)에 대 한 참조를 찾을 수 및 모바일 장치 관리 (MDM) 구성 지침을 Windows 10에 대 한 Microsoft Intune 및 VPN 프로필 템플릿을 사용 하 여 제공 합니다.

- [System Center Configuration Manager에서 만드는 VPN 프로필 하는 방법](https://docs.microsoft.com/sccm/protect/deploy-use/create-vpn-profiles):이 항목에서는 System Center Configuration Manager (SCCM) VPN 프로필을 만드는 방법을 알아봅니다.

- [Windows 10 클라이언트 항상에서 VPN 연결 구성](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/vpn-deploy-client-vpn-connections):이 항목에서는 설명의 ProfileXML 옵션 및 스키마 및 ProfileXML VPN을 만드는 방법입니다. 서버 인프라를 설정한 후 VPN 연결을 사용 하 여 해당 인프라와 통신 하도록 Windows10 클라이언트 컴퓨터를 구성 해야 합니다. 

- [VPN 프로필 옵션](https://docs.microsoft.com/windows/access-protection/vpn/vpn-profile-options):이 항목에서는 Windows 10의 VPN 프로필 설정에 설명 하 고 Intune 또는 SCCM을 사용 하 여 VPN 프로필을 구성 하는 방법을 알아봅니다. ProfileXML 노드가 VPNv2 CSP에서 사용 하 여 Windows 10의 모든 VPN 설정을 구성할 수 있습니다.

---