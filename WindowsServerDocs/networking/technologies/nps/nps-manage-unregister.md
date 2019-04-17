---
title: 등록 된 Active Directory 도메인 NPS 서버
description: Windows Server 2016 NPS 서버 기본 도메인 또는 다른 도메인 네트워크 정책 서버를 실행 하는 서버에 등록할 수이 항목을 사용할 수 있습니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 68a94616-3c29-45bd-bd33-e4c578f119e1
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 55c3b00146706831351ce63d1e5b74f45d7b9be1
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="unregister-an-nps-server-from-an-active-directory-domain"></a>등록 된 Active Directory 도메인 NPS 서버

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

NPS 서버 배포를 관리 하는 과정 유용 것 NPS 서버 NPS 서버, 교체 해야 또는 중지 NPS 서버를 다른 도메인에로 이동 합니다. 

이동 하거나 NPS 서버를 제거할 때 NPS 서버 NPS 서버 Active Directory에 사용자 계정의 속성에 읽을 수 있는 권한을 있는 Active Directory 도메인에 등록을 취소할 수 있습니다.

회원 **관리자**, 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.

## <a name="to-unregister-an-nps-server"></a>등록을 취소할 NPS 서버

1. 도메인 컨트롤러 서버 관리자에서 클릭 **도구**을 차례로 클릭 하 고 **Active Directory 사용자 및 컴퓨터**합니다. 콘솔 Active Directory 사용자 및 컴퓨터 엽니다.

2. 클릭 **사용자**, 다음 두 번 클릭 하 고 **RAS 및 IAS 서버**합니다.

3. 클릭 하 고 **회원** 탭을 선택한 다음 등록을 취소 하 고 싶은 NPS 서버 합니다.

4. 클릭 **제거**, 클릭 **예**을 차례로 클릭 하 고 **확인**합니다.

