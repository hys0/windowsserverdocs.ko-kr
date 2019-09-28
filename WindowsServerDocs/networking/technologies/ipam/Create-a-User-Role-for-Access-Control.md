---
title: 액세스 제어를 위한 사용자 역할 만들기
description: 이 항목은 Windows Server 2016의 IPAM (IP 주소 관리) 관리 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ae6a42db-a104-401b-a8e6-b85c47d30b46
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 01e3216ca62cdb780342b477e575e00cdeedc6dd
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405702"
---
# <a name="create-a-user-role-for-access-control"></a>액세스 제어를 위한 사용자 역할 만들기

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목을 사용 하 여 IPAM 클라이언트 콘솔에서 새 Access Control 사용자 역할을 만들 수 있습니다.  
  
이 절차를 수행하려면 최소한 **Administrators** 그룹의 구성원이거나 이와 동등한 자격이 있어야 합니다.  
  
> [!NOTE]  
> 역할을 만든 후 특정 사용자 또는 Active Directory 그룹에 역할을 할당 하는 액세스 정책을 만들 수 있습니다. 자세한 내용은 [액세스 정책 만들기](../../technologies/ipam/Create-an-Access-Policy.md)를 참조 하세요.  
  
### <a name="to-create-a-role"></a>역할을 만들려면  
  
1.  서버 관리자에서 클릭  **IPAM**합니다. IPAM 클라이언트 콘솔에 나타납니다.  
  
2.  탐색 창에서 **액세스 제어**를 클릭 하 고 아래쪽 탐색 창에서 **역할**을 클릭 합니다.  
  
    ![액세스 제어 역할](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_01.jpg)  
  
3.  **역할**을 마우스 오른쪽 단추로 클릭 한 다음 **사용자 역할 추가**를 클릭 합니다.  
  
    ![사용자 역할 추가](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_02.jpg)  
  
4.  **역할 추가 또는 편집** 대화 상자가 열립니다. **이름**에 역할 함수를 명확 하 게 만드는 역할의 이름을 입력 합니다. 예를 들어 관리자가 DNS SRV 리소스 레코드를 관리할 수 있는 역할을 만들려는 경우 **IPAMSrv**역할의 이름을 지정할 수 있습니다. 필요한 경우 **작업** 에서 아래로 스크롤하여 역할에 대해 정의 하려는 작업 유형을 찾습니다. 이 예제에서는 **DNS 리소스 레코드 관리 작업**까지 아래로 스크롤합니다.  
  
    ![DNS 리소스 레코드 관리 작업](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_03.jpg)  
  
5.  **DNS 리소스 레코드 관리 작업**을 확장 한 다음 **SRV 레코드 작업**을 찾습니다.  
  
    ![SRV 레코드 작업](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_04.jpg)  
  
6.  **SRV 레코드 작업**을 확장 하 고 선택한 다음 **확인**을 클릭 합니다.  
  
    ![SRV 레코드 작업 선택](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_05.jpg)  
  
7.  IPAM 클라이언트 콘솔에서 방금 만든 역할을 클릭 합니다. **자세히 보기** 에는 역할에 대해 허용 된 작업이 표시 됩니다.  
  
    ![새 역할 정보](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_06.jpg)  
  
## <a name="see-also"></a>관련 항목  
[역할 기반 Access Control](Role-based-Access-Control.md)  
[IPAM 관리](Manage-IPAM.md)  
  


