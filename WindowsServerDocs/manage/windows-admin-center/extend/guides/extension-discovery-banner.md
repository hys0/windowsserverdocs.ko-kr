---
title: 확장 검색 배너 사용
description: 확장 검색 배너 사용
ms.technology: manage
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 06/06/2019
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: f51070abfeed3a790055b12f733fc61be383472c
ms.sourcegitcommit: 20d07170c7f3094c2fb4455f54b13ec4b102f2d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/13/2020
ms.locfileid: "81269260"
---
# <a name="enabling-the-extension-discovery-banner"></a>확장 검색 배너 사용

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

확장 검색 배너 기능은 Windows 관리 센터 Preview 1903 릴리스에서 도입 되었습니다. 이 기능을 사용 하면 확장에서 지원 되는 서버 하드웨어 제조업체 및 모델을 선언할 수 있으며, 사용자가 확장을 사용할 수 있는 서버 또는 클러스터에 연결 하는 경우 확장을 쉽게 설치할 수 있도록 알림 배너가 표시 됩니다. 확장 개발자는 확장에 대 한 더 많은 가시성을 얻을 수 있으며 사용자는 서버에 대 한 더 많은 관리 기능을 쉽게 검색할 수 있습니다.

![확장 검색 배너](../../media/extend-guides-extension-discovery-banner/extension-discovery-banner.png)

## <a name="how-the-extension-discovery-banner-works"></a>확장 검색 배너의 작동 원리

Windows 관리 센터를 시작 하면 등록 된 확장 피드에 연결 되 고 사용 가능한 확장 패키지에 대 한 메타 데이터를 가져옵니다. 그러면 사용자가 Windows 관리 센터에서 서버 또는 클러스터에 연결 하는 경우 개요 도구에 표시할 서버 하드웨어 제조업체 및 모델이 읽혀집니다. 현재 서버의 제조업체 및/또는 모델을 지원함을 선언 하는 확장 프로그램이 있는 경우 사용자에 게 알릴 수 있도록 배너를 표시 합니다. "지금 설정" 링크를 클릭 하면 사용자가 확장을 설치할 수 있는 확장 관리자로 이동 합니다.

## <a name="how-to-implement-the-extension-discovery-banner"></a>확장 검색 배너를 구현 하는 방법

Nuspec 파일의 "tags" 메타 데이터는 확장에서 지 원하는 하드웨어 제조업체 및/또는 모델을 선언 하는 데 사용 됩니다. 태그는 공백으로 구분 되며 제조업체 또는 모델 태그를 추가 하거나 둘 다를 추가 하 여 지원 되는 제조업체 및/또는 모델을 선언할 수 있습니다. 태그 형식은 ``"[value type]_[value condition]"``입니다. 여기서 [값 유형]은 "제조업체" 또는 "모델" (대/소문자 구분)이 고 [값 조건]은 제조업체 또는 모델 문자열을 정의 하는 [Javascript 정규식](https://developer.mozilla.org/docs/Web/JavaScript/Guide/Regular_Expressions) 이며 [value type] 및 [value condition]은 밑줄로 구분 됩니다. 그런 다음 URI 인코딩을 사용 하 여이 문자열을 인코딩하고. nuspec "tags" 메타 데이터 문자열에 추가 합니다.

### <a name="example"></a>예제

모델 이름이 R3xx 및 R4xx 인 Contoso i n c. 라는 회사의 서버를 지 원하는 확장 프로그램을 개발 했다고 가정해 보겠습니다.

1. 제조업체에 대 한 태그는 ``"Manufacturer_/Contoso Inc./"``됩니다. 모델에 대 한 태그를 ``"Model_/^R[34][0-9]{2}$/"``수 있습니다. 일치 조건을 정의 하는 방법에 따라 정규식을 정의 하는 다양 한 방법이 있습니다. 제조업체 또는 모델 태그를 여러 태그로 구분할 수도 있습니다. 예를 들어 모델 태그를 ``"Model_/R3../ Model_/R4../"``수도 있습니다.
2. 웹 브라우저의 DevTools 콘솔을 사용 하 여 정규식을 테스트할 수 있습니다. Edge 또는 Chrome에서 F12 키를 눌러 DevTools 창을 열고 콘솔 탭에서 다음을 입력 하 고 Enter 키를 누릅니다.

   ```javascript
   var regex = /^R[34][0-9]{2}$/
   ```

   다음을 입력 하 고 실행 하면 ' t r u e '가 반환 됩니다.

   ```javascript
   regex.test('R300')
   ```

   다음을 실행 하는 경우에는 ' f a l s e '를 반환 합니다.

   ```javascript
   regex.test('R500')
   ```

3. 정규식을 확인 한 후에는 다음 Javascript 메서드를 사용 하 여 DevTools 콘솔 에서도 인코딩할 수 있습니다.

   ```javascript
   encodeURI(/^R[34][0-9]{2}$/)
   ```

   Nuspec 파일에 추가할 태그 문자열의 최종 형식은 다음과 같습니다.

   ```
   <tags>Manufacturer_/Contoso%20Inc./ Model_/%5ER%5B34%5D%5B0-9%5D%7B2%7D$/</tags>
   ```

> [!Tip]
> 하드웨어 제조업체에는 일부 지원 될 수 있지만 일부는 지원 되지 않는 매우 광범위 한 모델 이름이 있을 수 있습니다. 이 기능은 확장을 **검색** 하는 데 도움을 주기 위한 것 이지만 모든 모델의 완벽 한 최신 인벤토리가 될 필요는 없습니다. 정규식을 모델의 하위 집합과 일치 하는 간단한 식으로 정의할 수 있습니다. 사용자는 조건과 일치 하지 않는 서버 모델에 처음 연결 하는 경우 검색 배너를 표시 하지 않을 수 있습니다. 단, 그 보다 더 빨리는 확장을 검색 하 고 설치 하는 다른 서버에 연결 합니다. 제조업체 이름과만 일치 하는 간단한 정규식을 정의 하는 것을 고려할 수도 있습니다. 일부 경우에 확장에서 실제로 특정 모델을 지원 하지 않을 수 있지만 [동적 도구 표시 기능](./dynamic-tool-display.md) 을 사용 하 여 사용자 지정 PowerShell 스크립트를 정의 하 여 모델 지원을 확인 하 고 해당 하는 경우 확장만 표시 하거나, 모든 기능을 지원 하지 않는 모델에 대해 확장에서 제한 된 기능을 제공할 수 있습니다.