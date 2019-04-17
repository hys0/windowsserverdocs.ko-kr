---
ms.assetid: 7dd905ea-4235-4519-8400-31b4fa0ed1bf
title: "클라이언트 찾은 다음 가까운 도메인 컨트롤러를 사용"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 39b1b79bba944c10b0c74c4bb18f6dcf80f8230e
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="enabling-clients-to-locate-the-next-closest-domain-controller"></a>클라이언트 찾은 다음 가까운 도메인 컨트롤러를 사용

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Windows Server 2008 또는 Windows Server 2008 R2 실행 하는 도메인 컨트롤러를 사용 하는 경우 사용자 수 있도록 Windows Vista, Windows 7, Windows Server 2008 또는 Windows Server 2008 R2 도메인 컨트롤러 컨트롤러가 사용 하 여 더 효율적으로 실행 하는 컴퓨터에 대 한는 **다음 가까운 사이트 시도** 그룹 정책 설정 합니다. 이 설정을 특히 많은 지점와 사이트 대기업에서에서 네트워크 교통량을 간소화 하 여 도메인 컨트롤러 Locator (DC Locator)을 개선 합니다.  
  
이 새 설정을 도메인 컨트롤러 되는 순서 영향을 하기 때문에 사이트 링크 비용 구성 영향을 줄 수 있습니다. 많은 hub 사이트와 지사 포함 하는 엔터프라이즈 네트워크에 대 한 Active Directory 교통은 클라이언트 장애 조치를 다음 가까운 hub 사이트 가까운 hub 사이트에 도메인 컨트롤러를 찾을 수 없으면 될 수 있도록 하 여 크게 줄일 수 있습니다.  
  
일반 모범 사례로 사이트 토폴로지 간소화 해야 및 가능한 사용 하면 사이트 링크 비용이 **다음 가까운 사이트 시도** 설정 합니다. 많은 hub 사이트와 기업에서이 처리 한 사이트에 대 한 클라이언트를 통해 다른 사이트에 도메인 컨트롤러에 실패 하 해야 하는 경우에 대 한 계획을 모두 간소화할 수 있습니다.  
  
기본적으로는 **다음 가까운 사이트 시도** 설정을 사용할 수 없습니다. 설정을 활성화 되지 않은 경우 DC Locator 다음 알고리즘을 사용 하 여 도메인 컨트롤러를 찾습니다.  
  
-   동일한 사이트에 도메인 컨트롤러를 찾아 봅니다.  
  
-   같은 사이트에서 사용할 수 있는 도메인 컨트롤러 없는 경우 도메인에 있는 도메인 컨트롤러를 찾아 봅니다.  
  
> [!NOTE]  
> DC Locator 이전 버전의 Active Directory에 사용 되는 것과 동일한 알고리즘입니다. 자세한 내용은 참조 Active Directory 작품 DNS 지원 되는 방식을 ([https://go.microsoft.com/fwlink/?LinkId=108587](https://go.microsoft.com/fwlink/?LinkId=108587)).  
  
사용 하는 경우는 **다음 가까운 사이트 시도** 설정을 DC Locator를 사용 하 여 다음과 같은 알고리즘 도메인 컨트롤러 찾을:  
  
-   동일한 사이트에 도메인 컨트롤러를 찾아 봅니다.  
  
-   같은 사이트에서 사용할 수 있는 도메인 컨트롤러 없는 경우 다음 가까운 사이트에 도메인 컨트롤러를 찾아 봅니다. 사이트는 비용이 한 높은 사이트 링크와 함께 다른 사이트 보다 비용을 낮은 사이트 링크 있으면 가까이 합니다.  
  
-   다음 가까운 사이트에서 사용할 수 있는 도메인 컨트롤러 없는 경우 도메인에 있는 도메인 컨트롤러를 찾아 봅니다.  
  
기본적으로 DC Locator 다음 가까운 사이트를 확인 하는 읽기 전용 RODC (도메인 컨트롤러)를 포함 하는 사이트를 고려 하지 않습니다. 또한 같기 때문에 Windows Server 2008 및 Windows Server 2008 R2 도메인 컨트롤러 지원 다음 가까운 사이트 기능, Windows Server의 이전 버전을 실행 하는 도메인 컨트롤러에서 클라이언트 가져오는 응답 하는 경우, DC Locator 동작으로 때 다음 설정을 사용 되지 않습니다.  
  
예를 들어 사이트 토폴로지 다음 그림에서 사이트 링크 값으로 네 사이트에 있습니다. 여기에서 모든 도메인 컨트롤러에는 Windows Server 2008 또는 Windows Server 2008 R2 실행 하는 쓸 수 있는 도메인 컨트롤러 합니다.  
  
![Dc 찾을 클라이언트 사용](media/Enabling-Clients-to-Locate-the-Next-Closest-Domain-Controller/beff4087-fb2a-463b-96ac-d440a9e29b75.gif)  
  
때는 **다음 가까운 사이트 시도** 그룹 정책 설정을 여기에서 사용 하는 경우 Windows Vista, Windows 7, Windows Server 2008 실행 하는 클라이언트 컴퓨터 또는 Site_B에 Windows Server 2008 R2 도메인 컨트롤러 찾으려고, 처음에 자체 Site_B 도메인 컨트롤러를 시도 합니다. Site_B에서 사용할 수 없는 경우 Site_A에 도메인 컨트롤러를 시도 합니다.  
  
설정을 사용 하지 않는 경우 클라이언트 도메인 컨트롤러 Site_B에서 사용할 수 있는 경우 도메인 컨트롤러 Site_A, Site_C, 또는 Site_D 찾기 하 려 합니다.  
  
> [!NOTE]  
> **다음 가까운 사이트 시도** 설정은 자동 사이트 보도 함께 작동 합니다. 예를 들어 다음 가까운 사이트에 있는 경우 도메인 컨트롤러를 DC Locator 해당 사이트에 대 한 자동 사이트 검사를 수행 하는 도메인 컨트롤러를 시도 합니다.  
  
적용 하는 **다음 가까운 사이트 시도** 설정, Windows Vista, Windows 7, Windows Server 2008 또는 Windows Server 2008 R2 도메인에 실행 하는 모든 클라이언트에 영향을 줄 수를 기본 도메인 정책 수정할 수 있습니다 또는 그룹 정책 개체 GPO ()을 만들고 조직에 대 한 적절 한 개체에 연결할 수 있습니다. 설정 하는 방법에 대 한 자세한 내용은 **다음 가까운 사이트 시도** 참조 설정을 [다음 가까운 사이트에 도메인 컨트롤러를 찾을 수 클라이언트를 사용 하도록 설정](https://technet.microsoft.com/library/cc772592.aspx)합니다.  
  


