---
title: 액세스 정책 만들기
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
ms.assetid: 854bd064-2f86-4678-a940-a04b3e48ae10
ms.author: pashort
author: shortpatti
ms.openlocfilehash: ac8229952c7e038f9af8fc4f9287b1821db887ac
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="create-an-access-policy"></a>액세스 정책 만들기

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 항목 IPAM 클라이언트 본체에 대 한 액세스 정책의 만드는 데 사용할 수 있습니다.  
  
회원 **관리자**, 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.  
  
> [!NOTE]  
> 특정 사용자를 위한 또는 사용자 그룹에 대 한 액세스 정책 Active Directory에 만들 수 있습니다. 액세스 정책의 만들 때 내장 IPAM 역할 또는 사용자가 만든 사용자 지정 역할 선택 해야 합니다. 에 대 한 자세한 내용은 사용자 지정 역할을 [액세스 제어를 위한 사용자 역할을 만들고](../../technologies/ipam/Create-a-User-Role-for-Access-Control.md)합니다.  
  
### <a name="to-create-an-access-policy"></a>액세스 정책 만들려면  
  
1.  서버 관리자 클릭 **IPAM**합니다. IPAM 클라이언트 콘솔이 나타납니다.  
  
2.  탐색 창에서 클릭 **액세스 제어**합니다. 낮은 탐색 창에서 마우스 오른쪽 단추로 클릭 **액세스 정책을**을 차례로 클릭 하 고 **추가 액세스 정책**합니다.  
  
    ![액세스 정책 추가](../../media/Create-an-Access-Policy/ipam_CreateAP_01.jpg)  
  
3.  **추가 액세스 정책** 대화 상자를 엽니다. **사용자 설정을**, 클릭 **추가**합니다.  
  
    ![액세스 정책 추가](../../media/Create-an-Access-Policy/ipam_CreateAP_02.jpg)  
  
4.  **사용자 또는 그룹 선택** 대화 상자를 엽니다. 클릭 **위치**합니다.  
  
    ![사용자 또는 그룹 위치](../../media/Create-an-Access-Policy/ipam_CreateAP_03.jpg)  
  
5.  **위치** 대화 상자를 엽니다. 사용자 계정에 있는 위치로 이동 위치를 선택한 다음 **확인**합니다. **위치** 대화 상자를 닫습니다.  
  
    ![위치를 선택 합니다.](../../media/Create-an-Access-Policy/ipam_CreateAP_04.jpg)  
  
6.  에 **사용자 또는 그룹 선택** 대화 상자의 **선택할 개체 이름을 입력**, 액세스 정책 만들려는 사용자 계정 이름을 입력 합니다. 클릭 **확인**합니다.  
  
7.  **추가 액세스 정책**에 **사용자 설정을**, **사용자 별칭** 정책이 적용 되는 사용자 계정에 있습니다. **액세스 설정**, 클릭 **새로**합니다.  
  
    ![새 액세스 설정](../../media/Create-an-Access-Policy/ipam_CreateAP_05.jpg)  
  
8.  **추가 액세스 정책**, **액세스 설정** 변경 **새 설정을**합니다.  
  
    ![새 설정 대화 상자 이름 변경](../../media/Create-an-Access-Policy/ipam_CreateAP_06.jpg)  
  
9. 클릭 **선택 역할** 역할 목록을 확장 합니다. 기본 제공 역할 중 하나를 선택 하거나 새 역할을 만든 경우 사용자가 만든 역할 중 하나를 선택 합니다. 예를 들어, 사용자에 게 적용할 IPAMSrv 역할을 만든 클릭 **IPAMSrv**합니다.  
  
    ![역할을 선택 합니다.](../../media/Create-an-Access-Policy/ipam_CreateAP_07.jpg)  
  
10. 클릭 **설정을 추가**합니다.  
  
    ![새 설정을 추가합니다](../../media/Create-an-Access-Policy/ipam_CreateAP_08.jpg)  
  
11. 역할은 액세스 정책을에 추가 됩니다. 추가 액세스 정책 만들려면 클릭 **적용**을 만들려는 각 정책에 대 한 다음이 단계를 반복 합니다. 추가 정책을 만들 하려면 클릭 **확인**합니다.  
  
    ![클릭 적용 또는 확인](../../media/Create-an-Access-Policy/ipam_CreateAP_09.jpg)  
  
12. IPAM 클라이언트 콘솔 디스플레이 창에서 새 액세스 정책 만들어집니다 확인 합니다.  
  
    ![새 액세스 정책 보기](../../media/Create-an-Access-Policy/ipam_CreateAP_09a.jpg)  
  
## <a name="see-also"></a>참조 하십시오  
[액세스 역할 기반 제어](Role-based-Access-Control.md)  
[IPAM 관리](Manage-IPAM.md)  
  


