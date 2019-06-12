---
title: Corpnet에 반환 하는 경우 연결 하는 테스트에는 7 단계
description: 이 항목은 일부 테스트 랩 가이드-Windows Server 2016 Windows NLB를 사용 하 여 클러스터에서 DirectAccess 시연
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5a7252d0-6db8-4a9d-98ee-75082ecd2929
ms.author: pashort
author: shortpatti
ms.openlocfilehash: af22b1bbc923b9a06e4aebb910690050af1b7492
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446636"
---
# <a name="step-7-test-connectivity-when-returning-to-the-corpnet"></a>Corpnet에 반환 하는 경우 연결 하는 테스트에는 7 단계

>적용 대상: Windows Server (반기 채널), Windows Server 2016

경우에 게 반환 되는 회사 네트워크 구성을 확인 하지 않고도 리소스에 액세스 할 지 변경 하므로 대부분의 사용자는 원격 위치와 회사 네트워크 간에 이동 합니다. 원격 액세스 가능이 이므로 DirectAccess 클라이언트는 corpnet에 반환 될 때 네트워크 위치 서버에 연결할 수 있습니다. HTTPS 연결에서 네트워크 위치 서버에 설정 되 면 DirectAccess 클라이언트는 DirectAccess 클라이언트 구성을 사용 하지 않도록 설정 하 고 회사 네트워크에 직접 연결을 사용 합니다.  
  
### <a name="test-connectivity-on-client1"></a>CLIENT1에서 연결 테스트  
  
1. CLIENT1 종료 및 다음 CLIENT1 Homenet 서브넷 또는 가상 스위치에서 분리 및 Corpnet 서브넷 또는 가상 스위치에 연결 합니다. CLIENT1을 설정 하 고 CORP\User1로 로그온 합니다.  
  
2. 열고 관리자 권한 Windows PowerShell 창, 형식 **ipconfig /all**, ENTER 키를 누릅니다. CLIENT1에 IP 주소를 로컬 및 없는 활성 6to4, Teredo 또는 IP-HTTPS는 출력이 표시 됩니다 터널입니다.  
  
3. APP2의 네트워크 공유에 대 한 연결을 테스트 합니다. 에 **시작** 화면에서 입력<strong>\\\APP2\Files</strong>, 한 다음 ENTER를 누릅니다. 해당 폴더에서 파일을 열고 할 수 있습니다.  
  


