---
title: 7 단계 Corpnet 반환 시 연결 테스트
description: 이 항목은 테스트 랩 가이드-windows Server 2016 용 Windows NLB를 사용 하는 클러스터의 DirectAccess 시연에 포함 되어 있습니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5a7252d0-6db8-4a9d-98ee-75082ecd2929
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 491533ae5d141de4ab4f15126d8977cf15c8f7f4
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80314681"
---
# <a name="step-7-test-connectivity-when-returning-to-the-corpnet"></a>7 단계 Corpnet 반환 시 연결 테스트

>적용 대상: Windows Server(반기 채널), Windows Server 2016

대부분의 사용자는 원격 위치와 corpnet 간에 이동 하므로 구성 변경을 수행 하지 않고도 리소스에 액세스할 수 있는 corpnet로 돌아올 수 있습니다. 원격 액세스는 DirectAccess 클라이언트가 corpnet로 반환 될 때 네트워크 위치 서버에 연결할 수 있기 때문에 가능 합니다. 네트워크 위치 서버에 HTTPS 연결이 성공적으로 설정 되 면 DirectAccess 클라이언트는 DirectAccess 클라이언트 구성을 사용 하지 않도록 설정 하 고 corpnet에 대 한 직접 연결을 사용 합니다.  
  
### <a name="test-connectivity-on-client1"></a>C l i e n t 1의 연결 테스트  
  
1. C l i e n t 1을 종료 한 다음 HoCorpnet Et 서브넷 또는 가상 스위치에서 CLIENT1을 분리 하 고이를 서브넷 또는 가상 스위치에 연결 합니다. CLIENT1을 켜고 Corp\user1 계정로 로그온 합니다.  
  
2. 관리자 권한 Windows PowerShell 창을 열고 **ipconfig/all**을 입력 한 다음 enter 키를 누릅니다. 출력은 c l i e n t 1에 로컬 IP 주소가 있고 활성 6to4, Teredo 또는 IP-HTTPS 터널이 없음을 표시 합니다.  
  
3. APP2의 네트워크 공유에 대 한 연결을 테스트 합니다. **시작** 화면에서<strong>\\\APP2\Files</strong>를 입력 한 다음 enter 키를 누릅니다. 해당 폴더에서 파일을 열 수 있습니다.  
  


