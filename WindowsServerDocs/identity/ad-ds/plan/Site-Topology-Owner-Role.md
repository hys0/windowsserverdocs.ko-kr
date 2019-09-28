---
ms.assetid: af76ddbe-83a2-4a62-9989-873e3bb1c772
title: 사이트 토폴로지 소유자 역할
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 7b010dcb7a150f4ebcfcc941aa9e5c016795e717
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402493"
---
# <a name="site-topology-owner-role"></a>사이트 토폴로지 소유자 역할

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

사이트 토폴로지를 관리 하는 관리자는 사이트 토폴로지 소유자 라고 합니다. 사이트 토폴로지 소유자는 사이트 간의 네트워크 상태를 이해 하 고 사이트 토폴로지에 대 한 변경 내용을 구현 하기 위해 Active Directory Domain Services (AD DS)의 설정을 변경할 수 있는 권한을 가집니다. 사이트 토폴로지를 변경 하면 복제 토폴로지의 변경 내용에 영향을 줍니다. 사이트 토폴로지 소유자의 책임은 다음과 같습니다.  
  
-   네트워크 연결이 변경 되는 경우 사이트 토폴로지에 대 한 변경 내용을 제어 합니다.  
  
-   네트워크 그룹에서 네트워크 연결 및 라우터에 대 한 정보 가져오기 및 유지 관리 사이트 토폴로지 소유자는 서브넷 주소, 서브넷 마스크 및 각 주소가 속한 위치의 목록을 유지 해야 합니다. 사이트 토폴로지 소유자는 사이트 링크에 대 한 비용을 효과적으로 설정 하기 위해 사이트 토폴로지에 영향을 주는 네트워크 속도 및 용량에 대 한 문제를 이해 해야 합니다.  
  
-   도메인 컨트롤러의 IP 주소를 다른 사이트의 다른 서브넷으로 변경 하거나 서브넷 자체를 다른 사이트에 할당 하는 경우 사이트 간 도메인 컨트롤러를 나타내는 Active Directory 서버 개체 이동 어떤 경우 든 사이트 토폴로지 소유자는 도메인 컨트롤러의 Active Directory server 개체를 새 사이트로 수동으로 이동 해야 합니다.  
  


