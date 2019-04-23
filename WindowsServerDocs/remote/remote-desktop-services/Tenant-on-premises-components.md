---
title: 테넌트 온-프레미스 구성 요소
description: RDS 배포 온-프레미스 구성 요소를 설명합니다.
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
ms.openlocfilehash: a01dbd12d76b1efa84e38f2ded38cfd613fb2ac4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59857404"
---
# <a name="tenant-on-premises-components"></a>테넌트 온-프레미스 구성 요소

>적용 대상: Windows Server (반기 채널), Windows Server 2016

다음 정보를 데스크톱 호스팅 배포를 구성 하는 온-프레미스 구성 요소를 설명 합니다.  
  
##  <a name="clients"></a>클라이언트  
호스팅되는 데스크톱 및 응용 프로그램에 액세스 하려면 사용자는 원격 데스크톱 프로토콜 (RDP) 7.1 이상을 지 원하는 원격 데스크톱 클라이언트를 사용 해야 합니다. 특히 클라이언트는 원격 데스크톱 게이트웨이 및 원격 데스크톱 연결 브로커를 지원 해야 합니다. 로컬 데스크톱 응용 프로그램을 제공 하려면 클라이언트는 RemoteApp 기능을 지원도 해야 합니다. 클라이언트는 가장 높은 게이트웨이 규모를 달성 하려면 RD 게이트웨이 순수 HTTP 전송 연결을 지원 해야 합니다.  
  
추가 정보:  
[RemoteFX 사용 장치](https://social.technet.microsoft.com/wiki/contents/articles/14534.remotefx-enabled-devices.aspx)  
[Windows Server 2012 R2 원격 데스크톱 게이트웨이의 새로운 기능](https://blogs.technet.microsoft.com/enterprisemobility/2013/03/14/whats-new-in-windows-server-2012-remote-desktop-gateway/#transport)  
[Microsoft 원격 데스크톱 클라이언트](https://technet.microsoft.com/library/dn473009.aspx)  
[Microsoft Store Windows에 대 한 원격 데스크톱 앱](https://apps.microsoft.com/windows/app/remote-desktop/051f560e-5e9b-4dad-8b2e-fa5e0b05a480)  
[Microsoft 원격 데스크톱-Google Play에서 Android 앱](https://play.google.com/store/apps/details?id=com.microsoft.rdc.android)  
[Mac 앱 스토어에서 Microsoft 원격 데스크톱](https://itunes.apple.com/us/app/microsoft-remote-desktop/id715768417?mt=12)  
[앱 스토어에서 Microsoft 원격 데스크톱](https://itunes.apple.com/us/app/microsoft-remote-desktop/id714464092?mt=8)  
  
##  <a name="active-directory-domain-services"></a>Active Directory 도메인 서비스  
일부 크고 더 복잡 한 테 넌 트를 온-프레미스 Active Directory Domain Services (AD DS) 서버를 호스트할 수도 있습니다. 이 경우 테 넌 트의 환경에서 AD DS 서버 테 넌 트의 온-프레미스에는 AD DS 서버의 복제본 같아야 합니다. 테 넌 트의 환경에서 가상 네트워크를 만들고 테 넌 트의 온-프레미스 네트워크에서 Azure 데이터 센터에서 테 넌 트의 가상 네트워크 사이트 간 연결을 만들려면 Azure VPN을 사용 하 여 지원 됩니다.  
  
추가 정보:  
[Microsoft Azure Virtual Network 개요](https://azure.microsoft.com/documentation/articles/virtual-networks-overview/)  
[Azure Portal을 사용 하 여 사이트 간 VPN 연결을 사용 하 여 리소스 관리자 VNet 만들기](https://azure.microsoft.com/documentation/articles/vpn-gateway-howto-site-to-site-resource-manager-portal/)  


