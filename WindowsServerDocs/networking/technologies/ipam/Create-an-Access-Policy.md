---
title: 액세스 정책 만들기
description: 이 항목은 Windows Server 2016에서 관리 IPAM (IP 주소) 관리 가이드의 일부입니다.
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
ms.openlocfilehash: c8a97cd145a695bc8755f9111291e5c8bba2e572
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59881904"
---
# <a name="create-an-access-policy"></a>액세스 정책 만들기

>적용 대상: Windows Server (반기 채널), Windows Server 2016

IPAM 클라이언트 콘솔에 대 한 액세스 정책을 만들려면이 항목에서는 사용할 수 있습니다.  
  
이 절차를 수행하려면 최소한 **Administrators** 그룹의 구성원이거나 이와 동등한 자격이 있어야 합니다.  
  
> [!NOTE]  
> Active Directory에서 특정 사용자 또는 사용자 그룹에 대 한 액세스 정책을 만들 수 있습니다. 액세스 정책을 만들 때 기본 제공 IPAM 역할 또는 사용자가 만든 사용자 지정 역할을 선택 해야 합니다. 사용자 지정 역할에 대 한 자세한 내용은 참조 하세요. [Access Control에 대 한 사용자 역할을 만드는](../../technologies/ipam/Create-a-User-Role-for-Access-Control.md)합니다.  
  
### <a name="to-create-an-access-policy"></a>액세스 정책을 만들려면  
  
1.  서버 관리자에서 클릭  **IPAM**합니다. IPAM 클라이언트 콘솔에 나타납니다.  
  
2.  탐색 창에서 클릭 **ACCESS CONTROL**합니다. 아래쪽 탐색 창에서 마우스 오른쪽 단추로 클릭 **액세스 정책**를 클릭 하 고 **액세스 정책 추가**합니다.  
  
    ![액세스 정책 추가](../../media/Create-an-Access-Policy/ipam_CreateAP_01.jpg)  
  
3.  합니다 **액세스 정책 추가** 대화 상자가 열립니다. **사용자 설정**, 클릭 **추가**합니다.  
  
    ![액세스 정책 추가](../../media/Create-an-Access-Policy/ipam_CreateAP_02.jpg)  
  
4.  합니다 **사용자 또는 그룹 선택** 대화 상자가 열립니다. 클릭 **위치**합니다.  
  
    ![사용자 또는 그룹 위치](../../media/Create-an-Access-Policy/ipam_CreateAP_03.jpg)  
  
5.  합니다 **위치** 대화 상자가 열립니다. 사용자 계정을 포함 하는 위치를 검색할 위치를 선택 하 고 클릭 **확인**합니다. 합니다 **위치** 대화 상자가 닫힙니다.  
  
    ![위치 선택](../../media/Create-an-Access-Policy/ipam_CreateAP_04.jpg)  
  
6.  에 **사용자 또는 그룹 선택** 대화 상자의 **선택할 개체 이름 입력**, 액세스 정책을 만들려면 사용자 계정 이름을 입력 합니다. **확인**을 클릭합니다.  
  
7.  **액세스 정책 추가**의 **사용자 설정**에 **사용자 별칭** 이제는 정책이 적용 되는 사용자 계정이 포함 되어 있습니다. **액세스 설정을**, 클릭 **새로 만들기**합니다.  
  
    ![새 액세스 설정](../../media/Create-an-Access-Policy/ipam_CreateAP_05.jpg)  
  
8.  **액세스 정책 추가**를 **액세스 설정을** 변경 **새 설정을**합니다.  
  
    ![새 설정 대화 상자 이름 변경](../../media/Create-an-Access-Policy/ipam_CreateAP_06.jpg)  
  
9. 클릭 **역할 선택** 역할의 목록을 확장 합니다. 기본 제공 역할 중 하나를 선택 하거나 새 역할을 만든 경우 사용자가 만든 역할 중 하나를 선택 합니다. 예를 들어 사용자에 게 적용할 IPAMSrv 역할을 만든 경우 클릭 **IPAMSrv**합니다.  
  
    ![역할 선택](../../media/Create-an-Access-Policy/ipam_CreateAP_07.jpg)  
  
10. 클릭 **설정 추가**합니다.  
  
    ![새 설정 추가](../../media/Create-an-Access-Policy/ipam_CreateAP_08.jpg)  
  
11. 역할은 액세스 정책에 추가 됩니다. 추가 액세스 정책을 만들려면 **적용**, 한 다음 만들려면 원하는 각 정책에 대 한이 단계를 반복 합니다. 정책을 추가로 만들 하려면 클릭 **확인**합니다.  
  
    ![적용 또는 확인을 클릭](../../media/Create-an-Access-Policy/ipam_CreateAP_09.jpg)  
  
12. IPAM 클라이언트 콘솔 디스플레이 창에서 새 액세스 정책을 생성 되었는지 확인 합니다.  
  
    ![새 액세스 정책 보기](../../media/Create-an-Access-Policy/ipam_CreateAP_09a.jpg)  
  
## <a name="see-also"></a>관련 항목  
[역할 기반 액세스 제어](Role-based-Access-Control.md)  
[IPAM 관리](Manage-IPAM.md)  
  


