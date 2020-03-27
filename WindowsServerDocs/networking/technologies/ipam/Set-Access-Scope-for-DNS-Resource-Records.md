---
title: DNS 리소스 레코드에 대한 액세스 범위 설정
description: 이 항목은 Windows Server 2016의 IPAM (IP 주소 관리) 관리 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a96a8752-5678-49c5-b069-d2cce8042a51
ms.author: lizross
author: eross-msft
ms.openlocfilehash: fd084c856b4f78810ce732fd64b801d6b0f7b67d
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80316781"
---
# <a name="set-access-scope-for-dns-resource-records"></a>DNS 리소스 레코드에 대한 액세스 범위 설정

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목을 사용 하 여 IPAM 클라이언트 콘솔을 사용 하 여 DNS 리소스 레코드에 대 한 액세스 범위를 설정할 수 있습니다.  
  
이 절차를 수행하려면 최소한 **Administrators** 그룹의 구성원이거나 이와 동등한 자격이 있어야 합니다.  
  
### <a name="to-set-access-scope-for-dns-resource-records"></a>DNS 리소스 레코드에 대 한 액세스 범위를 설정 하려면  
  
1.  서버 관리자에서 클릭  **IPAM**합니다. IPAM 클라이언트 콘솔에 나타납니다.  
  
2.  탐색 창에서 **DNS 영역**을 클릭 합니다.  아래쪽 탐색 창에서 **전방 조회** 를 확장 하 고, 액세스 범위를 변경 하려는 리소스 레코드가 포함 된 영역을 찾아 선택 합니다.  
  
3.  디스플레이 창에서 액세스 범위를 변경 하려는 리소스 레코드를 찾아 선택 합니다.  
  
    ![리소스 레코드 선택](../../media/Set-Access-Scope-for-DNS-Resource-Records/ipam_RestrictUserToRRControl_02.jpg)  
  
4.  선택한 DNS 리소스 레코드를 마우스 오른쪽 단추로 클릭 한 다음 **액세스 범위 설정**을 클릭 합니다.  
  
    ![액세스 범위 설정](../../media/Set-Access-Scope-for-DNS-Resource-Records/ipam_RestrictUserToRRControl_03.jpg)  
  
5.  **액세스 범위 설정** 대화 상자가 열립니다. 배포에 필요한 경우 **부모에서 액세스 범위 상속**을 클릭 하 여 선택 취소 합니다. **액세스 범위 선택**에서 항목을 선택 하 고 **확인**을 클릭 합니다.  
  
    ![액세스 범위 선택](../../media/Set-Access-Scope-for-DNS-Resource-Records/ipam_RestrictUserToRRControl_04.jpg)  
  
## <a name="see-also"></a>관련 항목  
[역할 기반 Access Control](Role-based-Access-Control.md)  
[IPAM 관리](Manage-IPAM.md)  
  


