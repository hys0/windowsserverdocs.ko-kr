---
title: 액세스 정책 만들기
description: 이 항목은 Windows Server 2016의 IPAM (IP 주소 관리) 관리 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 854bd064-2f86-4678-a940-a04b3e48ae10
ms.author: lizross
author: eross-msft
ms.openlocfilehash: b5ce4c6dae668372521e5b8e0d5168a94cbb86e2
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80312647"
---
# <a name="create-an-access-policy"></a>액세스 정책 만들기

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목을 사용 하 여 IPAM 클라이언트 콘솔에서 액세스 정책을 만들 수 있습니다.  
  
이 절차를 수행하려면 최소한 **Administrators** 그룹의 구성원이거나 이와 동등한 자격이 있어야 합니다.  
  
> [!NOTE]  
> Active Directory에서 특정 사용자 또는 사용자 그룹에 대 한 액세스 정책을 만들 수 있습니다. 액세스 정책을 만들 때 기본 제공 IPAM 역할 또는 만든 사용자 지정 역할 중 하나를 선택 해야 합니다. 사용자 지정 역할에 대 한 자세한 내용은 [Access Control 사용자 역할 만들기](../../technologies/ipam/Create-a-User-Role-for-Access-Control.md)를 참조 하세요.  
  
### <a name="to-create-an-access-policy"></a>액세스 정책을 만들려면  
  
1.  서버 관리자에서 클릭  **IPAM**합니다. IPAM 클라이언트 콘솔에 나타납니다.  
  
2.  탐색 창에서 **액세스 제어**를 클릭 합니다. 아래쪽 탐색 창에서 **액세스 정책**을 마우스 오른쪽 단추로 클릭 한 다음 **액세스 정책 추가**를 클릭 합니다.  
  
    ![액세스 정책 추가](../../media/Create-an-Access-Policy/ipam_CreateAP_01.jpg)  
  
3.  **액세스 정책 추가** 대화 상자가 열립니다. **사용자 설정**에서 **추가**를 클릭 합니다.  
  
    ![액세스 정책 추가](../../media/Create-an-Access-Policy/ipam_CreateAP_02.jpg)  
  
4.  **사용자 또는 그룹 선택** 대화 상자가 열립니다. **위치**를 클릭 합니다.  
  
    ![사용자 또는 그룹 위치](../../media/Create-an-Access-Policy/ipam_CreateAP_03.jpg)  
  
5.  **위치** 대화 상자가 열립니다. 사용자 계정이 포함 된 위치로 이동 하 여 위치를 선택한 다음 **확인**을 클릭 합니다. **위치** 대화 상자가 닫힙니다.  
  
    ![위치 선택](../../media/Create-an-Access-Policy/ipam_CreateAP_04.jpg)  
  
6.  **사용자 또는 그룹 선택** 대화 상자의 **선택할 개체 이름 입력**에 액세스 정책을 만들 사용자 계정 이름을 입력 합니다. **확인**을 클릭합니다.  
  
7.  **액세스 정책 추가**의 **사용자 설정**에서 이제 정책이 적용 되는 사용자 계정을 **사용자 별칭** 에 포함 합니다. **액세스 설정**에서 **새로 만들기**를 클릭 합니다.  
  
    ![새 액세스 설정](../../media/Create-an-Access-Policy/ipam_CreateAP_05.jpg)  
  
8.  **액세스 정책 추가**에서 **액세스 설정이** **새 설정**으로 변경 됩니다.  
  
    ![대화 상자 이름이 새 설정으로 변경](../../media/Create-an-Access-Policy/ipam_CreateAP_06.jpg)  
  
9. **역할 선택** 을 클릭 하 여 역할 목록을 확장 합니다. 기본 제공 역할 중 하나를 선택 하거나 새 역할을 만든 경우 만든 역할 중 하나를 선택 합니다. 예를 들어 사용자에 게 적용할 IPAMSrv 역할을 만든 경우 **IPAMSrv**를 클릭 합니다.  
  
    ![역할 선택](../../media/Create-an-Access-Policy/ipam_CreateAP_07.jpg)  
  
10. **설정 추가**를 클릭합니다.  
  
    ![새 설정 추가](../../media/Create-an-Access-Policy/ipam_CreateAP_08.jpg)  
  
11. 역할이 액세스 정책에 추가 됩니다. 추가 액세스 정책을 만들려면 **적용**을 클릭 하 고 만들려는 각 정책에 대해 이러한 단계를 반복 합니다. 추가 정책을 만들지 않으려면 **확인**을 클릭 합니다.  
  
    ![적용 또는 확인을 클릭 합니다.](../../media/Create-an-Access-Policy/ipam_CreateAP_09.jpg)  
  
12. IPAM 클라이언트 콘솔 디스플레이 창에서 새 액세스 정책이 만들어졌는지 확인 합니다.  
  
    ![새 액세스 정책 보기](../../media/Create-an-Access-Policy/ipam_CreateAP_09a.jpg)  
  
## <a name="see-also"></a>관련 항목  
[역할 기반 Access Control](Role-based-Access-Control.md)  
[IPAM 관리](Manage-IPAM.md)  
  


