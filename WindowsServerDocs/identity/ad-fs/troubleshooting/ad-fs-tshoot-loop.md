---
title: AD FS 문제 해결-루프 검색
description: 이 문서에서는 루프 검색 문제를 해결 하는 방법을 설명 합니다.
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/21/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 2f8842dc53756cc4f65b6d6794a8c4952e111c00
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71385340"
---
# <a name="ad-fs-troubleshooting---loop-detection"></a>AD FS 문제 해결-루프 검색 
 
AD FS의 반복은 신뢰 당사자가 지속적으로 유효한 보안 토큰을 거부 하 고 AD FS 다시 리디렉션할 때 발생 합니다.

## <a name="loop-detection-cookie"></a>루프 검색 쿠키
이러한 상황이 발생 하지 않도록 하기 위해 AD FS 루프 검색 쿠키를 구현 했습니다. 기본적으로 AD FS는 **MSISLoopDetectionCookie**이라는 웹 수동 클라이언트에 쿠키를 작성 합니다. 이 쿠키에는 타임 스탬프 값과 발급 된 많은 토큰 값이 포함 됩니다.  이를 통해 AD FS는 특정 시간 범위 내에서 클라이언트가 페더레이션 서비스를 방문한 빈도와 횟수를 추적할 수 있습니다.

수동 클라이언트가 20 초 이내에 토큰 5 번 (5)에 대 한 페더레이션 서비스를 방문 하는 경우 AD FS는 다음 오류를 throw 합니다.

@NO__T 0MSIS7042: 동일한 클라이언트 브라우저 세션이 지난 ' {1} ' 초 동안 ' {0} ' 요청을 만들었습니다. 자세한 내용은 관리자에 게 문의 하십시오. **

무한 루프를 입력 하는 것은 AD FS에서 발급 된 토큰을 정상적으로 사용 하지 않는 오동작 신뢰 당사자 응용 프로그램에 의해 발생 하며, 응용 프로그램은 수동 클라이언트를 다시 AD FS 하 여 새 토큰에 대해 반복적으로 전송 하는 경우가 많습니다.  20 초 내에 5 개의 요청을 초과 하지 않는 한, AD FS는 매번 수동 클라이언트에 새 토큰을 발급 합니다. 

## <a name="adjusting-the-loop-detection-cookie"></a>루프 검색 쿠키 조정
PowerShell을 사용 하 여 발급 된 토큰의 수와 timespan 값을 변경할 수 있습니다.

```powershell
Set-AdfsProperties -LoopDetectionMaximumTokensIssuedInterval 5  -LoopDetectionTimeIntervalInSeconds 20
```
**LoopDetectionMaximumTokensIssuedInterval** 의 최소값은 1입니다.

**LoopDetectionTimeIntervalInSeconds** 의 최소값은 5입니다.

성능 테스트를 수행할 때 루프 검색을 사용 하지 않도록 설정할 수도 있습니다.

```powershell
Set-AdfsProperties -EnableLoopDetection $false
```

>[!IMPORTANT]
>사용자가 무한 루프 상태를 입력 하지 못하도록 하므로 루프 검색을 영구적으로 사용 하지 않도록 설정 하는 것은 좋지 않습니다.


## <a name="next-steps"></a>다음 단계

- [AD FS 문제 해결](ad-fs-tshoot-overview.md)



