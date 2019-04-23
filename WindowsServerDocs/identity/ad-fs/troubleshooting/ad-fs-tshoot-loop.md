---
title: AD FS 문제 해결-루프 검색
description: 이 문서에서는 루프 검색을 해결 하는 방법 설명
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/21/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: cc8eeb11e44da3b8f26b1ab94143c189bca9ed38
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59830914"
---
# <a name="ad-fs-troubleshooting---loop-detection"></a>AD FS 문제 해결-루프 검색 
 
AD FS에서 반복을 신뢰 당사자에서 지속적으로 유효한 보안 토큰을 거부 하 고 AD FS로 리디렉션합니다 때 발생 합니다.

## <a name="loop-detection-cookie"></a>루프 검색 쿠키
이를 방지 하려면 AD FS 루프 검색 쿠키를 어떻게 지칭 구현 했습니다. 기본적으로 AD FS 라는 웹 수동 클라이언트에 쿠키를 작성 **MSISLoopDetectionCookie**합니다. 이 쿠키는 타임 스탬프 값을 보유 하 고 토큰의 숫자 값을 발급 합니다.  이렇게 하면 AD FS의 클라이언트에도 여러 번이 특정 시간 범위 내에서 페더레이션 서비스를 방문한 방법과 빈도 추적 합니다.

수동 클라이언트 방문 하는 경우 5 (5) 시간에서 20 시간 (초), AD FS 토큰에 대 한 페더레이션 서비스에 다음 오류가 throw 됩니다.

**MSIS7042: 동일한 클라이언트 브라우저 세션에 대 한 '{0}'요청 지난 에서'{1}' 시간 (초)입니다. 자세한 내용은 관리자에 게 문의 합니다.**

신뢰 당사자 응용 프로그램에 성공적으로 AD FS에서 발급 된 토큰을 사용 하 고 있지는 오작동 하 여 자주 발생 무한 루프에 입력 하 고 응용 프로그램은 수동 클라이언트를 다시 보내는 AD FS를 반복적으로 새로운 토큰에 대 한 합니다.  AD FS는 수동 클라이언트를 새 토큰 발급 될 때마다 20 초에서 5 개의 요청을 초과 하지 않는으로 합니다. 

## <a name="adjusting-the-loop-detection-cookie"></a>루프 검색 쿠키를 조정합니다.
값과 시간 범위 값을 발급 된 토큰의 수를 변경 하려면 PowerShell을 사용할 수 있습니다.

```powershell
Set-AdfsProperties -LoopDetectionMaximumTokensIssuedInterval 5  -LoopDetectionTimeIntervalInSeconds 20
```
에 대 한 최소값 **LoopDetectionMaximumTokensIssuedInterval** 1입니다.

에 대 한 최소값 **LoopDetectionTimeIntervalInSeconds** 은 5입니다.

또한 성능 테스트를 수행할 때 루프 감지를 비활성화할 수 있습니다.

```powershell
Set-AdfsProperties -EnableLoopDetection $false
```

>[!IMPORTANT]
>것이 없습니다 이렇게 사용자 상태 무한 루프에 진입 하면 루프 검색을 영구적으로 해제 하는 것이 좋습니다.


## <a name="next-steps"></a>다음 단계

- [AD FS 문제 해결](ad-fs-tshoot-overview.md)



