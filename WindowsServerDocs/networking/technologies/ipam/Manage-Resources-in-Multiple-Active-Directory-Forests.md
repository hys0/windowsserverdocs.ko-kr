---
title: 여러 Active Directory 숲에서 리소스 관리
description: 이 항목은 Windows Server 2016에는 IP 주소 관리 (IPAM) 관리 가이드의 일부입니다.
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
ms.openlocfilehash: b01680d4b35461ff85965781ebc60e7a613d1cb8
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="manage-resources-in-multiple-active-directory-forests"></a>여러 Active Directory 숲에서 리소스 관리

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 항목 IPAM 도메인 컨트롤러, DHCP 서버 및 여러 Active Directory 숲에서 DNS 서버 관리를 사용 하는 방법을 알아보려면 사용할 수 있습니다.  
  
IPAM 원격 Active Directory 숲에서 리소스를 관리를 사용 하는 두 가지 방법으로 IPAM 설치 되어 있는 숲 신뢰할 관리 하려면 각 숲 있어야 합니다.  
  
다른 Active Directory 숲에 대 한 검색 프로세스를 시작 하려면 관리자 서버 열고 IPAM을 클릭 합니다. IPAM 클라이언트 콘솔에서 클릭 **서버 검색 구성**을 차례로 클릭 하 고 **숲 다운로드**합니다. 신뢰할 수 있는 숲와 해당 도메인 검색 백그라운드 작업을 시작 합니다. 클릭 하 고 검색 프로세스를 완료 한 후 **서버 검색 구성**는 다음과 같은 대화 상자를 엽니다.  
  
![서버 검색 구성](../../media/Manage-Resources-in-Multiple-Active-Directory-Forests/ipam_serverdiscovery.jpg)  

>[!NOTE]
>그룹 Policy\ 기반 Active Directory 크로스 숲 시나리오에 대 한 공급, 다음 Windows PowerShell cmdlet 신뢰 도메인 Dc 아니라 IPAM 서버에 실행 하는 확인 합니다. 예를 들어 경우 IPAM 서버가 숲 corp.contoso.com에 가입 하 고 신뢰 숲 fabrikam.com를 실행할 수 있습니다 다음과 같은 Windows PowerShell cmdlet IPAM 서버의 fabrikam.com 숲 속의 공급 그룹 Policy\ 기반에 corp.contoso.com에 합니다. 이 cmdlet를 실행 하려면 fabrikam.com 숲 속의 관리자 도메인 그룹의 회원 이어야 합니다.

    
    Invoke-IpamGpoProvisioning -Domain fabrikam.COM -GpoPrefixName IPAMSERVER -IpamServerFqdn IPAM.CORP.CONTOSO.COM
    

에 **서버 검색 구성** 대화 상자를 클릭 **숲 선택**, IPAM를 관리 하려면 숲을 선택 합니다. 또한 관리 하 고 다음을 클릭 하려면 도메인 선택 **추가**합니다.

**서버 역할 검색을 선택**를 관리 하려면 각 도메인에 대 한 서버를 검색 유형의 지정 합니다. 옵션은 **도메인 컨트롤러**, **DHCP 서버**, 및 **DNS 서버**합니다.

기본적으로 도메인 컨트롤러 서버, DHCP 민 DNS 서버 발견 된-따라서 이러한 유형의 서버 중 하나를 발견 하지 않을 경우 수 있도록 해당 옵션에 대 한 확인란의 선택을 취소 합니다.

위 예제에서는 그림에서 IPAM 서버 contoso.com 숲 속의 설치 되 고 fabrikam.com 숲 루트 도메인 IPAM 관리에 대 한 추가 됩니다. 선택한 서버 역할 IPAM 도메인 컨트롤러, DHCP 서버 및 fabrikam.com 루트 도메인 및 contoso.com 루트 도메인 DNS 서버를 검색 및 관리할 수 있습니다.

숲, 도메인 및 서버 역할 지정한 후 클릭 **확인**합니다. IPAM 검색을 수행 하 고 검색 완료 되 면 리소스는 지역 및 원격 숲 속의 관리할 수 있습니다.
