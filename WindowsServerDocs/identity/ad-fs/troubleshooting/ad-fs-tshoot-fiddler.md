---
title: AD FS 문제 해결-Fiddler
description: 이 문서에서는 Fiddler 이란 무엇 이며 설치 및 AD FS 클레임 문제를 해결 하는 Fiddler를 구성 하는 방법을 설명 합니다.
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 03/02/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 822300d0e4b6ae462a3c942e22530bbed5f93e86
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59865634"
---
# <a name="ad-fs-troubleshooting---fiddler"></a>AD FS 문제 해결-Fiddler
Fiddler는 HTTP/HTTPS 웹 트래픽 캡처를 사용할 수 있는 도구입니다.  클레임 발급 프로세스 문제 해결 지원 하기 위해이 도구를 사용할 수 있습니다.  트래픽을 확인 하 여 더 잘 이해 상호 작용 세분화를 가져올 수 있습니다.  이 문서에서는 설치 및 AD FS 트래픽을 캡처하도록 Fiddler를 설치 하는 방법을 설명 합니다.  Ws-federation을 사용 하 여 예제에서는 fiddler 추적을 참조 하세요. [AD FS-Fiddler-문제 해결 WS-페더레이션](ad-fs-tshoot-fiddler-ws-fed.md)

## <a name="download-and-install-fiddler"></a>다운로드 하 고 Fiddler를 설치 합니다.
Fiddler를 다운로드할 수 있습니다 [여기](https://www.telerik.com/download/fiddler)합니다.  다운로드 한 후 계속 진행 하 고 설치 합니다.

## <a name="configure-fiddler-to-capture-ad-fs-traffic"></a>AD FS 트래픽을 캡처하도록 Fiddler를 구성 합니다.
AD FS 트래픽 캡처를 위해 SSL 트래픽을 해독 하도록 Fiddler를 구성 해야 합니다. 

### <a name="configure-the-fiddler-ssl-certificate"></a>Fiddler SSL 인증서 구성
 SSL 트래픽을 해독 하도록 Fiddler를 설치 하려면 다음 절차를 따르십시오.

1.  열기 Fiddler
2.  맨 아래 **도구**를 선택 **Fiddler 옵션**합니다.
3.  HTTPS 탭을 클릭 합니다.
4.  에 체크 **암호를 해독 하는 HTTPS 트래픽을** 선택한 **만 브라우저에서** 드롭다운 목록에서.
5.  에 체크 **서버 인증서 오류를 무시**합니다.
6.  **확인**을 클릭합니다.

![Fiddler](media/ad-fs-tshoot-fiddler/fiddler1.png)

## <a name="next-steps"></a>다음 단계

- [AD FS 문제 해결](ad-fs-tshoot-overview.md)