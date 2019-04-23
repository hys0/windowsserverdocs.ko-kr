---
title: 3 단계는 배포를 확인 합니다.
description: 이 항목은 가이드 Windows Server 2016에서 원격으로 관리 DirectAccess 클라이언트의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6a78a078-d2e7-4cbd-b8d5-20cfb6d1524b
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 89b9e53b7321ebeddda50a448829ad73395eeed0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59835614"
---
# <a name="step-3-verify-the-deployment"></a>3 단계는 배포를 확인 합니다.

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 항목에서는 DirectAccess 클라이언트의 원격 관리에 대 한 배포 올바르게 구성 되었는지 확인 하는 방법을 설명 합니다.  
  
### <a name="to-verify-proper-deployment"></a>적절 한 배포를 확인 하려면  
  
1.  회사 네트워크에 DirectAccess 클라이언트 컴퓨터를 연결 하 고 그룹 정책 개체를 가져옵니다.  
  
2.  클라이언트 컴퓨터에서를 클릭 합니다 **네트워크 연결** DirectAccess 미디어 관리자에 액세스 하려면 알림 영역에서 아이콘입니다.  
  
3.  클릭 **DirectAccess 연결**에 상태가 표시 됩니다 **로컬로 연결**합니다.  
  
4.  회사 네트워크에서 컴퓨터를 제거 하 고 공용 네트워크에 연결 합니다.  
  
5.  명령 프롬프트에서 입력 **nltest /dsgetdc: [정규화 된 도메인 이름]** 합니다. 이 명령은 회사 네트워크에 클라이언트에 액세스할 수 있는지 확인 합니다. 도메인 컨트롤러에 액세스할 수 없는 경우 도메인 존재 하지 않는 보고 다음과 같은 오류 메시지가 표시 됩니다. ERROR_NO_SUCH_DOMAIN.  
  


