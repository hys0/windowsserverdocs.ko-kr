---
ms.assetid: af76ddbe-83a2-4a62-9989-873e3bb1c772
title: 사이트 토폴로지 소유자 역할
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 69443c2fc1af855c7df002e0ac91d43986eff6da
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59832114"
---
# <a name="site-topology-owner-role"></a>사이트 토폴로지 소유자 역할

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

사이트 토폴로지를 관리 하는 관리자는 사이트 토폴로지 소유자 라고 합니다. 사이트 간 네트워크의 조건을 이해 하 고 Active Directory Domain Services (AD DS) 사이트 토폴로지 변경 내용을 구현 하려면에서 설정을 변경할 수 있는 권한이 하는 사이트 토폴로지 소유자입니다. 사이트 토폴로지 변경에는 복제 토폴로지의 변경 내용이 적용 됩니다. 사이트 토폴로지 소유자의 책임은 다음과 같습니다.  
  
-   네트워크 연결을 변경 하는 경우 사이트 토폴로지 변경 내용을 제어 합니다.  
  
-   가져오기 및 네트워크 그룹에서 라우터 및 네트워크 연결에 대 한 정보를 유지 관리 합니다. 사이트 토폴로지 소유자 서브넷 주소, 서브넷 마스크 및 각 속해 있는 위치 목록을 유지 해야 합니다. 사이트 토폴로지 소유자 사이트 링크에 대 한 비용을 효과적으로 설정 하는 사이트 토폴로지에 영향을 주는 네트워크 속도 및 용량에 대 한 모든 문제를 파악 해야 합니다.  
  
-   서브넷 자체는 다른 사이트에 할당 된 경우 또는 도메인 컨트롤러의 IP 주소를 다른 사이트의 다른 서브넷으로 변경 하는 경우 사이트 간 도메인 컨트롤러를 나타내는 Active Directory 서버 개체를 이동 합니다. 두 경우 모두 사이트 토폴로지 소유자 새 사이트에 도메인 컨트롤러의 Active Directory 서버 개체를 수동으로 이동 해야 합니다.  
  


