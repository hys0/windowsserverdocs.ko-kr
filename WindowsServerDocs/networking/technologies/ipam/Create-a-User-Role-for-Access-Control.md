---
title: 액세스 제어를 위한 사용자 역할 만들기
description: 이 항목은 Windows Server 2016에서 관리 IPAM (IP 주소) 관리 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ae6a42db-a104-401b-a8e6-b85c47d30b46
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 3798b074a0ca7e20602da7986fe6b54e81da5495
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67284094"
---
# <a name="create-a-user-role-for-access-control"></a>액세스 제어를 위한 사용자 역할 만들기

>적용 대상: Windows Server (반기 채널), Windows Server 2016

IPAM 클라이언트 콘솔에서 새 액세스 제어 사용자 역할을 만들려면이 항목에서는 사용할 수 있습니다.  
  
이 절차를 수행하려면 최소한 **Administrators** 그룹의 구성원이거나 이와 동등한 자격이 있어야 합니다.  
  
> [!NOTE]  
> 역할을 만든 후 특정 사용자 또는 Active Directory 그룹에 역할을 할당 하는 액세스 정책을 만들 수 있습니다. 자세한 내용은 [액세스 정책 만들기](../../technologies/ipam/Create-an-Access-Policy.md)합니다.  
  
### <a name="to-create-a-role"></a>역할을 만들려면  
  
1.  서버 관리자에서 클릭  **IPAM**합니다. IPAM 클라이언트 콘솔에 나타납니다.  
  
2.  탐색 창에서 클릭 **액세스 제어**, 아래쪽 탐색 창에서 클릭 **역할**입니다.  
  
    ![액세스 제어 역할](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_01.jpg)  
  
3.  마우스 오른쪽 단추로 클릭 **역할**를 클릭 하 고 **사용자 역할 추가**합니다.  
  
    ![사용자 역할 추가](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_02.jpg)  
  
4.  합니다 **추가 또는 편집 역할** 대화 상자가 열립니다. **이름을**, 역할 함수 선택을 취소 하는 역할에 대 한 이름을 입력 합니다. 예를 들어, DNS SRV 리소스 레코드를 관리할 수 있게 하는 역할을 만들려는 경우 이름을 지정할 수 있습니다 역할 **IPAMSrv**합니다. 필요한 경우에서 아래로 스크롤하여 **Operations** 역할을 정의 하려는 작업의 유형을 찾을 수 있습니다. 예를 들어까지 아래로 스크롤하고 **DNS 리소스 레코드를 관리 작업**합니다.  
  
    ![DNS 리소스 레코드를 관리 작업](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_03.jpg)  
  
5.  확장 **DNS 리소스 레코드를 관리 작업**를 찾은 후 **SRV 레코드 작업**합니다.  
  
    ![SRV 레코드 작업](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_04.jpg)  
  
6.  확장 하 고 선택 **SRV 레코드 operations**를 클릭 하 고 **확인**합니다.  
  
    ![SRV 레코드 작업 선택](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_05.jpg)  
  
7.  IPAM 클라이언트 콘솔에서 방금 만든 역할을 클릭 합니다. **세부 정보 보기** 역할에 대해 허용 되는 작업에 표시 됩니다.  
  
    ![새 역할 정보](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_06.jpg)  
  
## <a name="see-also"></a>관련 항목  
[역할 기반 액세스 제어](Role-based-Access-Control.md)  
[IPAM 관리](Manage-IPAM.md)  
  


