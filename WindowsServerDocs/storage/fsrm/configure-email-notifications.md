---
title: 전자 메일 알림 구성
description: 이 문서에서는 전자 메일 알림을 구성 하는 방법을 설명 합니다.
ms.date: 7/7/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: b80aef85d6f4a1d6bd8c05b56d7c1a12b456d1ed
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85474190"
---
# <a name="configure-e-mail-notifications"></a>전자 메일 알림 구성

> 적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

할당량 및 파일 차단을 만들 때 할당량 한도가 임박 하거나 사용자가 차단 된 파일을 저장 하려고 시도 하는 경우 사용자에 게 전자 메일 알림을 보낼 수 있는 옵션이 있습니다. 저장소 보고서를 생성할 때 보고서를 특정 받는 사람에 게 전자 메일로 보낼 수 있는 옵션이 있습니다. 특정 관리자에 게 할당량 및 파일 차단 이벤트를 정기적으로 알리거나 저장소 보고서를 보내려면 하나 이상의 기본 받는 사람을 구성할 수 있습니다.

이러한 알림과 저장소 보고서를 보내려면 전자 메일 메시지를 전달 하는 데 사용할 SMTP 서버를 지정 해야 합니다.

## <a name="to-configure-e-mail-options"></a>전자 메일 옵션을 구성 하려면

1. 콘솔 트리에서 **파일 서버 리소스 관리자**를 마우스 오른쪽 단추로 클릭 하 고 **옵션 구성**을 클릭 합니다. **파일 서버 리소스 관리자 옵션** 대화 상자가 열립니다.

2. **전자 메일 알림** 탭에서 **smtp 서버 이름 또는 ip 주소**아래에 전자 메일 알림과 저장소 보고서를 전달할 smtp 서버의 호스트 이름 또는 ip 주소를 입력 합니다.

3. 특정 관리자에 게 할당량 또는 파일 차단 이벤트 또는 전자 메일 저장소 보고서에 대해 정기적으로 알리려면 **기본 관리자의 받는 사람**에 각 전자 메일 주소를 입력 합니다.

   형식을 사용 <em>account@domain</em> 합니다. 여러 계정을 구분 하려면 세미콜론을 사용 합니다.

4. 파일 서버 리소스 관리자에서 보낸 전자 메일 알림과 저장소 보고서에 대해 다른 "보낸 사람" 주소를 지정 하려면 **기본 "보낸 사람" 전자 메일 주소**에서 메시지에 표시할 전자 메일 주소를 입력 합니다.

5. 설정을 테스트 하려면 **테스트 전자 메일 보내기**를 클릭 합니다.

6. **확인**을 클릭합니다.


## <a name="additional-references"></a>추가 참조

-   [파일 서버 리소스 관리자 옵션 설정](setting-file-server-resource-manager-options.md)