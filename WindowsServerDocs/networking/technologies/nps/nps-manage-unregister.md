---
title: Active Directory 도메인에서 NPS 등록 해제
description: 네트워크 정책 서버 NPS 기본 도메인 또는 다른 도메인의 Windows Server 2016에서 실행 하는 서버를 등록 하려면이 항목에서는 사용할 수 있습니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 68a94616-3c29-45bd-bd33-e4c578f119e1
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 8fe4773efd89aeb413b3793f874ad6a1b030294a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59864354"
---
# <a name="unregister-an-nps-from-an-active-directory-domain"></a>Active Directory 도메인에서 NPS 등록 해제

>적용 대상: Windows Server (반기 채널), Windows Server 2016

NPS 배포를 관리 하는 동안 유용할 수 있습니다 하는 NPS를 대체 하거나 NPS를 중지할 다른 도메인에는 NPS를 이동할입니다. 

을 이동 하거나 NPS 서비스를 해제 하는 경우에 NPS를 Active Directory에서 사용자 계정 속성을 읽을 권한이 있는 Active Directory 도메인에서 NPS를 등록 취소할 수 있습니다.

이 절차를 수행하려면 최소한 **Administrators** 그룹의 구성원이거나 이와 동등한 자격이 필요합니다.

## <a name="to-unregister-an-nps"></a>NPS 등록을 취소 하려면

1. 도메인 컨트롤러에서 서버 관리자에서 클릭 **도구**를 클릭 하 고 **Active Directory Users and Computers**합니다. Active Directory 사용자 및 컴퓨터 콘솔을 엽니다.

2. 클릭 **사용자가**를 차례로 클릭 한 다음 **RAS 및 IAS 서버**합니다.

3. 클릭 합니다 **멤버** 탭 한 다음 등록을 취소 하려는 NPS를 선택 합니다.

4. 클릭 **제거할**, 클릭 **예**를 클릭 하 고 **확인**합니다.

