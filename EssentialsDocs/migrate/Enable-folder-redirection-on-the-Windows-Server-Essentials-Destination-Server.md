---
title: Windows Server Essentials 대상 서버1에서 폴더 리디렉션 사용
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
H1: Windows Server Essentials 대상 서버에서 폴더 리디렉션 사용
ms.assetid: f67d195e-36f6-495a-8361-6d5faa889441
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: f93d7b28177f96725f2e62c40f9c81cbf186ee6d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59819384"
---
# <a name="enable-folder-redirection-on-the-windows-server-essentials-destination-server1"></a>Windows Server Essentials 대상 서버1에서 폴더 리디렉션 사용

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

원본 서버에서 폴더 리디렉션이 사용하도록 설정되어 있으면 이 작업을 수행할 수 있습니다.  
  
 첫째, Windows Server Essentials 대시보드를 사용 하 여 대상 서버에서 폴더 리디렉션을 사용 하도록 설정 합니다. 그런 다음 이전 폴더 리디렉션 그룹 정책 설정을 삭제합니다.  
  
### <a name="to-enable-folder-redirection-on-the-destination-server"></a>대상 서버에서 폴더 리디렉션을 사용하도록 설정하려면  
  
1.  대상 서버에서 Windows Server Essentials 대시보드를 엽니다.  
  
2.  탐색 모음에서 **장치**를 클릭합니다.  
  
3.  **장치 작업** 창에서 **그룹 정책 구현**을 클릭합니다.  
  
4.  **폴더 리디렉션 그룹 정책 사용** 페이지에서 리디렉션할 폴더를 선택하고 **다음**을 클릭합니다.  
  
5.  **보안 정책 설정 사용** 페이지에서 **마침**을 클릭합니다.  
  
### <a name="to-delete-the-old-folder-redirection-group-policy-setting"></a>이전 폴더 리디렉션 그룹 정책 설정을 삭제하려면  
  
1.  대상 서버에서 **그룹 정책 관리** 관리 도구를 엽니다.  
  
2.  **그룹 정책 관리**를 확장 하 고 **포리스트: * * * YourNetworkDomainName*를 확장 **도메인**를 확장 *YourNetworkDomainName* 을 펼쳐 **그룹 정책 개체**합니다.  
  
3.  마우스 오른쪽 단추로 클릭 **W7PVP 폴더 리디렉션**을 클릭하고 **삭제**합니다.  
  
4.  경고를 읽고 **예**를 클릭합니다.  
  
5.  **그룹 정책 관리**를 닫습니다.  
  
 폴더 리디렉션에 변경 내용을 적용하려면 네트워크 사용자가 컴퓨터에서 로그오프한 다음 다시 로그온해야 합니다. 이렇게 하면 모든 리디렉션된 폴더가 대상 서버로 전송됩니다.
