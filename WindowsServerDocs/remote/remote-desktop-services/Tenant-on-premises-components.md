---
title: 테넌트 온-프레미스 구성 요소
description: RDS 배포의 온-프레미스 구성 요소에 대해 설명합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 08/01/2016
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b3eebb38-a835-4fa6-9e41-1966014bf2cb
author: lizap
manager: dongill
ms.openlocfilehash: ff584533eef70144e3bb6ba595fd0f8db89697e9
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2019
ms.locfileid: "63744045"
---
# <a name="tenant-on-premises-components"></a>테넌트 온-프레미스 구성 요소

>적용 대상: Windows Server(반기 채널), Windows Server 2019, Windows Server 2016

다음 정보는 데스크톱 호스팅 배포를 구성하는 온-프레미스 구성 요소를 설명합니다.  
  
##  <a name="clients"></a>클라이언트  
호스티드 데스크톱 및 애플리케이션에 액세스하려면 사용자는 RDP(원격 데스크톱 프로토콜) 7.1 이상을 지원하는 원격 데스크톱 클라이언트를 사용해야 합니다. 특히 클라이언트는 원격 데스크톱 게이트웨이 및 원격 데스크톱 연결 브로커를 지원해야 합니다. 애플리케이션을 로컬 데스크톱에 전달하려면 클라이언트는 RemoteApp 기능도 지원해야 합니다. 최대의 게이트웨이 규모를 달성하려면 클라이언트는 RD 게이트웨이에 대한 순수한 HTTP 전송 연결을 지원해야 합니다.  
  
추가 정보:  
[RemoteFX 사용 디바이스](https://social.technet.microsoft.com/wiki/contents/articles/14534.remotefx-enabled-devices.aspx)  
[Windows Server 2012 R2 원격 데스크톱 게이트웨이의 새로운 기능](https://blogs.technet.microsoft.com/enterprisemobility/2013/03/14/whats-new-in-windows-server-2012-remote-desktop-gateway/#transport)  
[Microsoft 원격 데스크톱 클라이언트](https://technet.microsoft.com/library/dn473009.aspx)  
[Microsoft Store의 Windows용 원격 데스크톱 앱](https://apps.microsoft.com/windows/app/remote-desktop/051f560e-5e9b-4dad-8b2e-fa5e0b05a480)  
[Microsoft 원격 데스크톱 - Google Play의 Android 앱](https://play.google.com/store/apps/details?id=com.microsoft.rdc.android)  
[Mac App Store - Microsoft 원격 데스크톱](https://itunes.apple.com/us/app/microsoft-remote-desktop/id715768417?mt=12)  
[App Store의 Microsoft 원격 데스크톱](https://itunes.apple.com/us/app/microsoft-remote-desktop/id714464092?mt=8)  
  
##  <a name="active-directory-domain-services"></a>Active Directory 도메인 서비스  
좀 더 크고 복잡한 일부 테넌트는 AD DS(Active Directory Domain Services) 서버를 온-프레미스에 호스트하도록 선택할 수도 있습니다. 이 경우 테넌트의 환경에 있는 AD DS 서버는 일반적으로 테넌트의 온-프레미스에 있는 AD DS 서버의 복제본이 됩니다. 이를 지원하기 위해 테넌트의 환경에서 가상 네트워크를 만들고 Azure VPN을 사용하여 Azure 데이터 센터에서 테넌트의 온-프레미스 네트워크와 테넌트의 가상 네트워크에 사이트 간 연결을 만듭니다.  
  
추가 정보:  
[Microsoft Azure Virtual Network 개요](https://azure.microsoft.com/documentation/articles/virtual-networks-overview/)  
[Azure Portal을 사용하여 사이트 간 VPN 연결을 사용하여 Resource Manager VNet 만들기](https://azure.microsoft.com/documentation/articles/vpn-gateway-howto-site-to-site-resource-manager-portal/)  


