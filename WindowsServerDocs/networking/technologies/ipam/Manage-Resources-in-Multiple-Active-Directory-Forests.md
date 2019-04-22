---
title: 여러 Active Directory 포리스트의 리소스 관리
description: 이 항목은 Windows Server 2016에서 관리 IPAM (IP 주소) 관리 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 82f8f382-246e-4164-8306-437f7a019e0f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: c6752d87be2e689e517b287092a2570e27943c18
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59815974"
---
# <a name="manage-resources-in-multiple-active-directory-forests"></a>여러 Active Directory 포리스트의 리소스 관리

>적용 대상: Windows Server (반기 채널), Windows Server 2016

도메인 컨트롤러, DHCP 서버 및 여러 Active Directory 포리스트에 대 한 DNS 서버를 관리 하려면 IPAM을 사용 하는 방법에 알아보려면이 항목을 사용할 수 있습니다.  
  
원격 Active Directory 포리스트에서 리소스를 관리 하려면 IPAM을 사용 하려면 두 IPAM 설치 되어 있는 포리스트와 양방향 트러스트를 관리 하려면 각 포리스트에 있어야 합니다.  
  
서로 다른 Active Directory 포리스트에 대 한 검색 프로세스를 시작 하려면 서버 관리자를 열고 IPAM을 클릭 합니다. IPAM 클라이언트 콘솔에서 클릭 **서버 검색 구성**, 를 클릭 하 고 **포리스트 가져오기**합니다. 신뢰할 수 있는 포리스트 및 도메인을 검색 하는 백그라운드 작업을 시작 합니다. 검색 프로세스가 완료 되 면 클릭 **서버 검색 구성**, 다음과 같은 대화 상자가 열립니다.  
  
![서버 검색 구성](../../media/Manage-Resources-in-Multiple-Active-Directory-Forests/ipam_serverdiscovery.jpg)  

>[!NOTE]
>그룹 정책에 대 한\-트러스팅 도메인의 Dc 아니라 IPAM 서버에 다음 Windows PowerShell cmdlet을 실행 하는 확인 기반 Active Directory 상호 포리스트 시나리오에 대 한 프로 비전 합니다. 예를 들어 경우 IPAM 서버 포리스트 corp.contoso.com에 가입 되어 있고 트러스팅 포리스트는 fabrikam.com을 실행할 수 있습니다 다음 Windows PowerShell cmdlet corp.contoso.com에 IPAM 서버에서 그룹 정책에 대 한\-기반 fabrikam.com 포리스트에서 프로 비전 합니다. 이 cmdlet을 실행 하려면 fabrikam.com 포리스트의 Domain Admins 그룹의 멤버 여야 합니다.

    
    Invoke-IpamGpoProvisioning -Domain fabrikam.COM -GpoPrefixName IPAMSERVER -IpamServerFqdn IPAM.CORP.CONTOSO.COM
    

에 **서버 검색 구성** 대화 상자를 클릭 **포리스트를 선택 합니다.**, IPAM을 사용 하 여 관리 하려는 포리스트를 선택 합니다. 또한 관리 하 고 클릭 하려는 도메인을 선택 **추가**합니다.

**를 검색 하는 서버 역할 선택**, 를 관리 하려면 각 도메인에 검색할 서버 유형을 지정 합니다. 옵션은 **도메인 컨트롤러**, **DHCP 서버**, 및 **DNS 서버**합니다.

기본적으로 도메인 컨트롤러, DHCP 서버 및 DNS 서버 검색-이러한 유형의 서버 중 하나를 검색 하려면 있도록 해당 옵션에 대 한 확인란의 선택을 취소 합니다.

위의 예제에서는 그림에서 IPAM 서버가 contoso.com 포리스트에 설치 하 고 fabrikam.com 포리스트 루트 도메인 IPAM 관리에 대 한 추가 됩니다. 선택한 서버 역할에는 IPAM이 검색 하 고 도메인 컨트롤러, DHCP 서버 및 fabrikam.com 루트 도메인 및 contoso.com 루트 도메인의 DNS 서버를 관리할 수 있도록 합니다.

포리스트, 도메인 및 서버 역할을 지정한 후 클릭 **확인**합니다. IPAM 검색을 수행 하 고 검색이 완료 되 면 로컬 및 원격 포리스트에 있는 리소스를 관리할 수 있습니다.
