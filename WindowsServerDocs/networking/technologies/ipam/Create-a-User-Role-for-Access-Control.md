---
title: 사용자 역할 액세스 제어 만들기
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
ms.assetid: ae6a42db-a104-401b-a8e6-b85c47d30b46
ms.author: pashort
author: shortpatti
ms.openlocfilehash: fa0ed71d399ad638a648946952fe170d93f69ceb
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="create-a-user-role-for-access-control"></a>사용자 역할 액세스 제어 만들기

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 항목 역할을 만드는 새로운 액세스 제어 사용자 IPAM 클라이언트 콘솔에서 사용할 수 있습니다.  
  
회원 **관리자**, 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.  
  
> [!NOTE]  
> 역할을 만든 후에 특정 사용자 또는 그룹 Active Directory에 역할 할당할 액세스 정책을 만들 수 있습니다. 자세한 내용은 참조 [액세스 정책을 만드는](../../technologies/ipam/Create-an-Access-Policy.md)합니다.  
  
### <a name="to-create-a-role"></a>역할을 만들려면  
  
1.  서버 관리자 클릭 **IPAM**합니다. IPAM 클라이언트 콘솔이 나타납니다.  
  
2.  탐색 창에서 클릭 **액세스 제어**, 낮은 탐색 창에서 클릭 **역할**합니다.  
  
    ![액세스 제어 역할](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_01.jpg)  
  
3.  마우스 오른쪽 단추로 클릭 **역할**을 차례로 클릭 하 고 **사용자 역할 추가**합니다.  
  
    ![사용자 역할 추가](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_02.jpg)  
  
4.  **추가 또는 편집 역할** 대화 상자를 엽니다. **이름**, 지우기 역할 기능을 사용 하면 역할 이름을 입력 합니다. 예를 들어, 관리자가 SRV 리소스 기록을 관리할 수 있도록 역할 만들려는 경우 이름을 지정할 수 있습니다 역할 **IPAMSrv**합니다. 필요한 경우에 아래로 스크롤하여 **작업** 작업의 역할 정의 하려는 유형의 찾을 수 있습니다. 예를이 들어가 때까지 아래로 스크롤하여 **DNS 리소스 기록 관리 작업**합니다.  
  
    ![DNS 리소스 기록 관리 작업](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_03.jpg)  
  
5.  확장 **DNS 리소스 기록 관리 작업**를 찾습니다 **SRV 녹화 작업**합니다.  
  
    ![SRV 기록 작업](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_04.jpg)  
  
6.  확장을 선택 하 고 **SRV 녹화 작업**을 차례로 클릭 하 고 **확인**합니다.  
  
    ![SRV 녹화 작업을 선택 합니다.](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_05.jpg)  
  
7.  IPAM 클라이언트 콘솔에서 방금 만든 역할을 클릭 합니다. **자세히 보기** 역할 허가 된 운영 표시 됩니다.  
  
    ![새 역할 세부 정보](../../media/Create-a-User-Role-for-Access-Control/ipam_CreateUserRole_06.jpg)  
  
## <a name="see-also"></a>참조 하십시오  
[액세스 역할 기반 제어](Role-based-Access-Control.md)  
[IPAM 관리](Manage-IPAM.md)  
  


