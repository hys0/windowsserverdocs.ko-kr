---
title: AD FS 문제 해결-Fiddler
description: 이 문서에서는 Fiddler에 대해 설명 하 고, AD FS 클레임 문제를 해결 하기 위해 Fiddler를 설치 및 구성 하는 방법을 설명 합니다.
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 03/02/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: f2abf1a0b844e8e8799458f5237d7a80059880ff
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71366154"
---
# <a name="ad-fs-troubleshooting---fiddler"></a>AD FS 문제 해결-Fiddler
Fiddler은 HTTP/HTTPS 웹 트래픽을 캡처하는 데 사용할 수 있는 도구입니다.  이 도구를 사용 하 여 클레임 발급 프로세스를 쉽게 해결할 수 있습니다.  트래픽을 살펴보면 상호 작용이 중단 되는 위치를 보다 잘 이해할 수 있습니다.  이 문서에서는 AD FS 트래픽을 캡처하기 위해 Fiddler를 설치 하 고 설정 하는 방법을 설명 합니다.  WS-FEDERATION을 사용 하는 fiddler 추적 예제는 [AD FS 문제 해결-fiddler](ad-fs-tshoot-fiddler-ws-fed.md) 을 참조 하세요.

## <a name="download-and-install-fiddler"></a>Fiddler 다운로드 및 설치
[여기](https://www.telerik.com/download/fiddler)에서 Fiddler를 다운로드할 수 있습니다.  다운로드 한 후에는 계속 해 서 설치 합니다.

## <a name="configure-fiddler-to-capture-ad-fs-traffic"></a>AD FS 트래픽을 캡처하도록 Fiddler 구성
AD FS 트래픽을 캡처하려면 SSL 트래픽을 해독 하도록 Fiddler을 구성 해야 합니다. 

### <a name="configure-the-fiddler-ssl-certificate"></a>Fiddler SSL 인증서 구성
 다음 절차에 따라 Fiddler를 설정 하 여 SSL 트래픽을 해독 합니다.

1.  Fiddler 열기
2.  맨 위에 있는 **도구**에서 **Fiddler 옵션**을 선택 합니다.
3.  HTTPS 탭을 클릭 합니다.
4.  **HTTPS 트래픽 암호 해독** 의 확인란을 선택 하 고 드롭다운에서 **브라우저 에서만** 을 선택 합니다.
5.  **서버 인증서 무시 오류**에 체크 인을 추가 합니다.
6.  **확인**을 클릭합니다.

![Fiddler](media/ad-fs-tshoot-fiddler/fiddler1.png)

## <a name="next-steps"></a>다음 단계

- [AD FS 문제 해결](ad-fs-tshoot-overview.md)