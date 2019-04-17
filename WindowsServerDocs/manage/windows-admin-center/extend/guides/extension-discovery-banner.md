---
title: 확장 검색 배너를 사용 하도록 설정
description: 확장 검색 배너를 사용 하도록 설정
ms.technology: manage
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 03/08/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 389acba6d1fe6f65320bd780c9fde6469b387e0b
ms.sourcegitcommit: e558dda2774345e9ad17ff04b759f68c59d88139
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2019
ms.locfileid: "9262965"
---
# 확장 검색 배너를 사용 하도록 설정 #

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

Windows Admin Center 미리 보기 1903에서 사용할 수 있는 새로운 기능 확장 검색 배너입니다. 이 기능을 사용 하는 서버 하드웨어 제조업체 및 모델을 지 원하는 선언에 대 한 확장 하 고 알림 배너 쉽게 확장을 설치 하려면 표시 됩니다 사용자를 서버 또는 확장을 사용할 수 있는 클러스터에 연결 합니다. 확장 개발자는 확장에 대 한 자세한 표시 여부를 가져올 수 및 사용자가 서버에 대해 더 많은 관리 기능을 쉽게 알 수 있게 됩니다.

![확장 검색 배너](../../media/extend-guides-extension-discovery-banner/extension-discovery-banner.png)

## 확장 검색 배너 작동 방식 ##

Windows Admin Center를 시작 하는 등록 된 확장 피드에 연결 되 고 사용할 수 있는 확장 패키지에 대 한 메타 데이터를 가져옵니다. 다음 사용자가 서버 또는 클러스터에 Windows Admin Center에 연결 하는 경우 서버 하드웨어 제조업체 및 모델 개요 도구에서 표시를 읽습니다. 현재 서버의 제조업체 및/또는 모델을 지원 한다고 선언 하는 확장에 증명이 사용자에 게 알리는를 배너 됩니다 표시 됩니다. "지금 설정" 링크를 클릭 하면 걸릴 사용자 확장을 설치할 수 있도록 확장 관리자를 됩니다.

## 확장 검색 배너를 구현 하는 방법 ##

.Nuspec 파일에 "태그" 메타 데이터는 하드웨어 제조업체를 선언 하는 데 사용 되 및/또는 확장 지원 모델링 합니다. 태그는 공백을 구분 하 고 제조업체 또는 모델 태그 또는 둘 다 지원 되는 제조업체 및/또는 모델을 선언 하려면 추가할 수 있습니다. 태그 형식은 ``"[value type]_[value condition]"`` "중 제조업체" 또는 "모델" (대/소문자 구분) 및 [값 조건] [값 형식]은는 [Javascript 정규식](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions) 정의 제조업체 또는 모델 문자열과 [값 형식을] 및 [조건 값]는 밑줄로 구분합니다. 이 문자열은 다음 인코딩되며 인코딩 및.nuspec "태그" 메타 데이터 문자열에 추가 하는 URI를 사용 하 여

### 예 ###

확장을 지 원하는 서버 모델을 사용 하 여 Contoso Inc. 라는 회사에서 개발한 않는 경우를 가정해 보겠습니다 R3xx 및 R4xx 이름을 지정 합니다.

1. 제조업체에 대 한 태그 것 ``"Manufacturer_/Contoso Inc./"``. 모델에 대 한 태그 수 ``"Model_/^R[34][0-9]{2}$/"``. 얼마나 엄격 하 게 일치 하는 조건을 정의 하려면, 따라 정규식 정의 하는 여러 가지 수 있습니다. 예를 들어 모델 태그 수, 여러 태그에 태그 제조업체 또는 모델을 구분할 수 있습니다 ``"Model_/R3../ Model_/R4../"``.
2. 웹 브라우저의 개발자 도구 콘솔 정규식을 테스트할 수 있습니다. Edge, Chrome에서 F12 개발자 도구 창을 열려면 적중 하 고 콘솔 탭에서 다음 및 적중 Enter를 입력 합니다.

```javascript
var regex = /^R[34][0-9]{2}$/
```

다음을 입력 하 고 다음을 실행 하는 경우 't r u 반환 됩니다.

```javascript
regex.test('R300')
```

다음을 실행 하는 경우 'false' 반환 합니다.

```javascript
regex.test('R500')
```

3. 정규식을 확인 한 후 인코딩할 수 있습니다 것도 개발자 도구 콘솔에서 다음 Javascript 메서드를 사용 하 여.

```javascript
encodeURI(/^R[34][0-9]{2}$/)
```

최종.nuspec 파일에 추가할 태그 문자열 형식은 다음과 같습니다.

```
<tags>Manufacturer_/Contoso%20Inc./ Model_/%5ER%5B34%5D%5B0-9%5D%7B2%7D$/</tags>
```

> [!Tip]
> 하드웨어 제조업체는 일부 지원 될 수 있습니다 일부 상태인 모델 이름의 다양할 수 있다고 이해 이 기능은 확장, **검색** 에 도움이 되는 이므로 있다는 점에 유의 해야 하지만 모든 모델의 완벽 하 게 최신 인벤토리 될 필요가 없습니다. 정규식 모델의 하위 집합에 일치 하는 간단한 식를 정의할 수 있습니다. 먼저 조건을 일치 하지 않는 서버 모델에 연결 하는 경우 사용자가 검색 배너를 표시 되지 않을 수도 있지만 조만간 않는 검색 및 확장을 설치 하는 다른 서버에 연결 됩니다. 만 제조업체 이름과 일치 하는 간단한 정규식 정의 고려할 수 있습니다. 경우에 따라 확장 실제로 특정 모델을 지원 하지 않을 수 있지만 수 [동적 도구 기능을 표시](./dynamic-tool-display.md) 모델 지원을 확인 하 고만 해당 하는 경우, 확장을 표시 하는 사용자 지정 PowerShell 스크립트를 정의 하 나 사용할 제한 제공 모든 기능을 지원 하지 않는 모델에 대 한 확장 기능입니다.