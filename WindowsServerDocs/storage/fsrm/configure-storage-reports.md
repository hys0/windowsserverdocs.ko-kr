---
title: "저장소 보고서 구성"
description: "이 문서에서는 저장소 보고서에 대한 기본 매개 변수를 구성하는 방법을 설명합니다."
ms.date: 7/7/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: f62109a8d3ea3e4e6386956789d276f9aa911e80
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2017
---
# <a name="configure-storage-reports"></a>저장소 보고서 구성

> 적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

저장소 보고서에 대한 기본 매개 변수를 구성할 수 있습니다. 이러한 기본 매개 변수는 할당량 또는 파일 차단 이벤트가 발생했을 때 생성되는 문제 보고서에 사용됩니다. 또한 예약된 보고서와 요청 시 보고서에도 사용되며, 이러한 보고서의 특정 속성을 정의할 때 기본 매개 변수를 재정의할 수 있습니다.

> [!Important]
> 보고서 유형에 대한 기본 매개 변수를 변경하면, 변경 내용이 모든 문제 보고서와 기본값을 사용하는 기존의 예약된 보고서 작업에 영향을 미칩니다.

## <a name="to-configure-the-default-parameters-for-storage-reports"></a>저장소 보고서에 대한 기본 매개 변수를 구성하려면

1. 콘솔 트리에서 마우스 오른쪽 단추로 **파일 서버 리소스 관리자**를 클릭하고 **구성 옵션**을 클릭합니다. **파일 서버 리소스 관리자 옵션** 대화 상자가 열립니다.

2. **저장소 보고서** 탭의 **기본 매개 변수 구성**에서 수정하려는 보고서의 유형을 선택합니다.

3. **매개 변수 편집**을 클릭합니다.

4. 선택한 보고서의 유형에 따라, 편집할 수 있는 보고서 매개 변수가 달라집니다. 필요한 모든 수정 작업을 수행하고, **확인**을 클릭하여 해당 유형의 보고서에 대한 기본 매개 변수로 저장합니다.

5.  편집하려는 각 보고서 유형에 대해 2 - 4단계를 반복합니다.

6. 모든 보고서에 대한 기본 매개 변수의 목록을 보려면 **보고서 검토**를 클릭합니다. 그런 다음 **닫기**를 클릭합니다.

7.  **확인**을 클릭합니다.

## <a name="see-also"></a>참고 항목

-   [파일 서버 리소스 관리자 옵션 설정](setting-file-server-resource-manager-options.md)
-   [저장소 보고서 관리](storage-reports-management.md)