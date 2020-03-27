---
title: Active Directory 도메인에서 NPS 등록 해제
description: 이 항목을 사용 하 여 NPS 기본 도메인 또는 다른 도메인의 Windows Server 2016에서 네트워크 정책 서버를 실행 하는 서버를 등록할 수 있습니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 68a94616-3c29-45bd-bd33-e4c578f119e1
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 366e3e7eef6ac1e8682dd3064e0d133f21d1a8da
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80315889"
---
# <a name="unregister-an-nps-from-an-active-directory-domain"></a>Active Directory 도메인에서 NPS 등록 해제

>적용 대상: Windows Server(반기 채널), Windows Server 2016

Nps 배포를 관리 하는 과정에서 nps를 다른 도메인으로 이동 하거나 NPS를 교체 하거나 NPS를 사용 중지 하는 것이 유용할 수 있습니다. 

NPS를 이동 하거나 서비스를 해제할 때 nps에 Active Directory의 사용자 계정 속성을 읽을 수 있는 권한이 있는 Active Directory 도메인에서 NPS를 등록 취소할 수 있습니다.

이 절차를 수행하려면 최소한 **Administrators** 그룹의 구성원이거나 이와 동등한 자격이 필요합니다.

## <a name="to-unregister-an-nps"></a>NPS를 등록 취소 하려면

1. 도메인 컨트롤러의 서버 관리자에서 **도구**를 클릭 한 다음 **사용자 및 컴퓨터 Active Directory**를 클릭 합니다. Active Directory 사용자 및 컴퓨터 콘솔을 엽니다.

2. **사용자**를 클릭 한 다음 **RAS 및 IAS 서버**를 두 번 클릭 합니다.

3. **멤버** 탭을 클릭 한 다음 등록을 취소 하려는 NPS를 선택 합니다.

4. **제거**를 클릭 하 고 **예**를 클릭 한 다음 **확인**을 클릭 합니다.

