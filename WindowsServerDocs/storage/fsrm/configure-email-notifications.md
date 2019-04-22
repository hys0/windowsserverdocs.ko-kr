---
title: 전자 메일 알림 구성
description: 이 문서에서는 전자 메일 알림을 구성하는 방법을 설명합니다.
ms.date: 7/7/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: d53be34d04edfac9f30b6e269833be74a6ebcf22
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59820354"
---
# <a name="configure-e-mail-notifications"></a>전자 메일 알림 구성

> 적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

할당량 및 파일 차단을 만드는 경우, 할당량 한도에 도달했을 때 또는 사용자가 차단된 파일을 저장하려고 시도한 후 사용자에게 전자 메일 알림을 보낼 수 있는 옵션이 제공됩니다. 저장소 보고서를 생성하는 경우, 특정 수신자에게 전자 메일로 보고서를 보내는 옵션이 제공됩니다. 특정 관리자에게 할당량 및 파일 차단 이벤트에 대해 정기적으로 알리거나 저장소 보고서를 보내려는 경우, 하나 이상의 기본 수신자를 구성할 수 있습니다.

이러한 알림 및 저장소 보고서를 보내려면 전자 메일 메시지를 전달하는 데 사용할 SMTP 서버를 지정해야 합니다.

## <a name="to-configure-e-mail-options"></a>전자 메일 옵션을 구성하려면

1.  콘솔 트리에서 마우스 오른쪽 단추로 **파일 서버 리소스 관리자**를 클릭하고 **구성 옵션**을 클릭합니다. **파일 서버 리소스 관리자 옵션** 대화 상자가 열립니다.

2.  **전자 메일 알림** 탭의 **SMTP 서버 이름 또는 IP 주소**에서, 전자 메일 알림과 저장소 보고서를 전달할 SMTP 서버의 호스트 이름과 IP 주소를 입력합니다.

3.  특정 관리자에게 할당량 및 파일 차단 이벤트를 정기적으로 알리거나 전자 메일 저장소 보고서를 보내려면 **기본 수신 관리자** 아래에서 각 전자 메일 주소를 입력합니다.

    *account@domain*  형식을 사용합니다. 여러 계정을 구분하려면 세미콜론을 사용합니다.

4.  파일 서버 리소스 관리자에서 보내는 전자 메일 알림 및 저장소 보고서에 대해 다른 "보낸 사람" 주소를 지정하려면, **기본 "보낸 사람" 전자 메일 주소**에서 메시지에 표시될 전자 메일 주소를 입력합니다.

5.  설정을 테스트를 하려면 **테스트 전자 메일 보내기**를 클릭합니다.

6.  **확인**을 클릭합니다.


## <a name="see-also"></a>참조

-   [설정 파일 서버 리소스 관리자 옵션](setting-file-server-resource-manager-options.md)