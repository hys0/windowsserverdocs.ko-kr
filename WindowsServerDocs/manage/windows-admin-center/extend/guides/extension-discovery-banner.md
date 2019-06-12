---
title: 확장 검색 배너를 사용 하도록 설정
description: 확장 검색 배너를 사용 하도록 설정
ms.technology: manage
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 06/06/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: fafc16d6acae3c5a7a58a379d2f88998b8e98c3d
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66811873"
---
# <a name="enabling-the-extension-discovery-banner"></a>확장 검색 배너를 사용 하도록 설정

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

확장 검색 배너는 하는 새로운 기능 Windows Admin Center 미리 보기 1903에서 사용할 수 있습니다. 이 기능을 사용 하는 서버 하드웨어 제조업체 및 모델을 지 원하는 선언에 대 한 확장 및 사용자가 서버 또는 클러스터 확장을 사용할 수 있는 연결을 쉽게 확장을 설치 하려면 알림 배너가 표시 됩니다. 확장 개발자는 해당 확장명에 대 한 자세한 파악할 수 및 사용자가 서버에 대 한 더 많은 관리 기능을 쉽게 검색할 수 있습니다.

![확장 검색 배너](../../media/extend-guides-extension-discovery-banner/extension-discovery-banner.png)

## <a name="how-the-extension-discovery-banner-works"></a>확장 검색 배너의 작동 원리

Windows Admin Center 시작 하는 등록 된 확장 피드에 연결 하 고 사용 가능한 확장 패키지에 대 한 메타 데이터를 인출 합니다. 사용자가 서버 또는 Windows Admin Center 클러스터에 연결 하는 경우 개요 도구에서 표시할 서버 하드웨어 제조업체 및 모델을 읽은 그런 다음. 현재 서버 제조업체 및/또는 모델 지원함을 선언 하는 확장을 찾을 것을 사용자에 게 알리는 배너가 표시 됩니다. "이제 설정" 링크를 클릭 하면 걸립니다 사용자 확장을 설치할 수 있는 확장 관리자를 합니다.

## <a name="how-to-implement-the-extension-discovery-banner"></a>확장 검색 배너를 구현 하는 방법

.Nuspec 파일에서 "tags" 메타 데이터는 하드웨어 제조업체를 선언 하는 데 사용 됩니다 및/또는 모델에 확장 프로그램은 지원 합니다. 공백으로 구분 된 태그 및 제조업체 또는 모델 태그 또는 둘 다 지원 되는 제조업체 및/또는 모델 선언에 추가할 수 있습니다. 태그 형식은 ``"[value type]_[value condition]"`` [값] 형식은 "Manufacturer" 또는 "Model" (대/소문자 구분), 않았고 [값] 조건은 [Javascript 정규식](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions) [값 유형] 또는 제조업체와 모델 문자열을 정의 하 고 [ 값 조건] 밑줄로 구분 됩니다. 그런 다음 인코딩 및.nuspec "tags" 메타 데이터 문자열에 추가 하는 URI를 사용 하 여이 문자열이 인코딩됩니다.

### <a name="example"></a>예제

모델을 사용 하 여 Contoso inc 라는 회사에서 서버를 지 원하는 확장명 개발한 않는 경우를 가정해 보겠습니다 R3xx 및 R4xx 이름을 지정 합니다.

1. 제조업체에 대 한 태그 것 ``"Manufacturer_/Contoso Inc./"``입니다. 모델에 대 한 태그 수 ``"Model_/^R[34][0-9]{2}$/"``입니다. 얼마나 엄격 하 게 일치 하는 조건을 정의 하려면에 따라 정규식을 정의 하는 다양 한 방법 없을 것입니다. 예를 들어 모델 태그 수, 제조업체 또는 모델 태그를 여러 태그를 분리할 수도 있습니다 ``"Model_/R3../ Model_/R4../"``합니다.
2. 웹 브라우저의 DevTools 콘솔을 사용 하 여 정규식을 테스트할 수 있습니다. Edge 또는 Chrome DevTools 창을 열려면 f12 키를 누른 하 고 콘솔 탭에서 다음 및 적중 Enter를 입력 합니다.

   ```javascript
   var regex = /^R[34][0-9]{2}$/
   ```

   입력 하 고 다음을 실행 하는 경우 'true' 반환 됩니다.

   ```javascript
   regex.test('R300')
   ```

   다음을 실행 하는 경우 'false' 반환 합니다.

   ```javascript
   regex.test('R500')
   ```

3. 정규식을 확인 한 후 인코딩할 수 있습니다도 DevTools 콘솔에서 다음 Javascript 메서드를 사용 하 여:

   ```javascript
   encodeURI(/^R[34][0-9]{2}$/)
   ```

   .Nuspec 파일에 추가할 태그 문자열의 최종 형식은 다음과 같습니다.

   ```
   <tags>Manufacturer_/Contoso%20Inc./ Model_/%5ER%5B34%5D%5B0-9%5D%7B2%7D$/</tags>
   ```

> [!Tip]
> 에 하드웨어 제조업체 있을 수 있는 일부 지원 될 수 없는 일부 하는 동안 모델 이름 매우 다양 한 범위의 이해 합니다. 이 기능에 도움이 되도록 것을 염두에 둡니다 합니다 **검색** 확장 프로그램의 하지만 모든 모델의 완벽 하 게 최신 인벤토리를 사용할 필요가 없습니다. 모델의 하위 집합에 일치 하는 간단한 식에 정규식을 정의할 수 있습니다. 먼저 조건에 일치 하지 않는 서버 모델에 연결 하는 경우 사용자는 검색 배너가 표시 되지 않을 수 있지만 조만간 않습니다 하 고 검색 하 고 확장을 설치 하는 다른 서버에 연결 됩니다. 만 제조업체 이름과 일치 하는 간단한 정규식을 정의할 수도 있습니다. 경우에 따라 확장 지원 하지 않습니다 실제로 특정 모델, 하지만 사용할 수 있습니다는 [동적 도구 표시 기능](./dynamic-tool-display.md) 모델에서 지를 확인 하 고만 해당 되는 경우에 확장 프로그램을 표시 하는 사용자 지정 PowerShell 스크립트를 정의 합니다. 또는 모든 기능을 지원 하지 않는 모델에 대 한 확장 프로그램에서 제한 된 기능을 제공 합니다.