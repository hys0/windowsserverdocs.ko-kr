---
ms.assetid: af76ddbe-83a2-4a62-9989-873e3bb1c772
title: "사이트 토폴로지 소유자 역할"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 7c98d313cac28ab07380791a384a87bffacfbda2
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="site-topology-owner-role"></a>사이트 토폴로지 소유자 역할

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

관리 하는 사이트 토폴로지 관리자 사이트 토폴로지 소유자 이라고 합니다. 사이트 토폴로지 소유자 사이트 간의 네트워크 상태를 이해 하 고 데 Active Directory Domain Services 변경을 구현 (AD DS)에서 설정을 변경할 수 있는 권한이 합니다. 데 변경 적용 복제 토폴로지에서 변경 됩니다. 사이트 토폴로지 소유자의 책임은 다음과 같습니다.  
  
-   네트워크 연결을 변경 하는 경우 변경 내용을 데를 제어 합니다.  
  
-   얻기 및 네트워크 연결 및 라우터가 네트워크 그룹에서에 대 한 정보를 유지 합니다. 사이트 토폴로지 소유자 서브넷 주소, 서브넷 마스크 및 각 속해 있는 위치 목록을 유지 해야 합니다. 네트워크 속도 용량이 대 한 비용 사이트 링크를 효과적으로 설정 하도록 사이트 토폴로지에 영향을 주는 문제 사이트 토폴로지 소유자 이해 해야 합니다.  
  
-   다른 서브넷 다른 사이트에 도메인 컨트롤러의 IP 주소를 변경 하거나 자체 서브넷 다른 사이트에 할당 되어 사이트 간의 도메인 컨트롤러 나타내는 Active Directory 서버 개체를 이동 합니다. 두 경우 모두 사이트 토폴로지 소유자 새 사이트에 도메인 컨트롤러 서버 Active Directory 개체 수동으로 이동 해야 합니다.  
  


