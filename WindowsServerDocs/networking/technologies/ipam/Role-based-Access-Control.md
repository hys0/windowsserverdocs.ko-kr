---
title: 역할 기반 액세스 제어
description: 이 항목은 Windows Server 2016의 IPAM (IP 주소 관리) 관리 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ecdfc589-fa14-4bb3-ab7e-456ebc719385
ms.author: lizross
author: eross-msft
ms.openlocfilehash: dc4dc26a5079a34cdaa3d455e59f6bfb4d1f74c1
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80309526"
---
# <a name="role-based-access-control"></a>역할 기반 액세스 제어

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목에서는 IPAM에서 역할 기반 액세스 제어를 사용 하는 방법에 대 한 정보를 제공 합니다.  
  
> [!NOTE]  
> 이 항목 외에 다음 IPAM 액세스 제어 설명서를이 섹션에서 사용할 수 있습니다.  
>   
> -   [서버 관리자를 사용 하 여 역할 기반 Access Control 관리](../../technologies/ipam/Manage-Role-Based-Access-Control-with-Server-Manager.md)  
> -   [Windows PowerShell을 사용 하 여 역할 기반 Access Control 관리](../../technologies/ipam/Manage-Role-Based-Access-Control-with-Windows-PowerShell.md)  
  
역할 기반 액세스 제어를 사용 하면 DNS 서버, DNS 영역 및 DNS 리소스 레코드 수준을 포함 하 여 다양 한 수준에서 액세스 권한을 지정할 수 있습니다.  
역할 기반 액세스 제어를 사용 하 여 다른 유형의 DNS 리소스 레코드를 만들고, 편집 하 고, 삭제 하는 작업을 세부적으로 제어 하는 사용자를 지정할 수 있습니다.  
  
사용자가 다음 사용 권한으로 제한 되도록 액세스 제어를 구성할 수 있습니다.  
  
-   사용자는 특정 DNS 리소스 레코드만 편집할 수 있습니다.  
  
-   사용자는 PTR 또는 MX와 같은 특정 유형의 DNS 리소스 레코드를 편집할 수 있습니다.  
  
-   사용자는 특정 영역에 대 한 DNS 리소스 레코드를 편집할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
[서버 관리자를 사용 하 여 역할 기반 Access Control 관리](../../technologies/ipam/Manage-Role-Based-Access-Control-with-Server-Manager.md)  
[Windows PowerShell을 사용 하 여 역할 기반 Access Control 관리](../../technologies/ipam/Manage-Role-Based-Access-Control-with-Windows-PowerShell.md)  
[IPAM 관리](Manage-IPAM.md)  
  


