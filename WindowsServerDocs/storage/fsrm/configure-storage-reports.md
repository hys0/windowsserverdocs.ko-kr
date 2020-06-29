---
title: 스토리지 보고서 구성
description: 이 문서에서는 저장소 보고서의 기본 매개 변수를 구성 하는 방법을 설명 합니다.
ms.date: 7/7/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 94d1b75bba4edac5ad8df80adb13d95a7b8dec39
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85474160"
---
# <a name="configure-storage-reports"></a>스토리지 보고서 구성

> 적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

저장소 보고서에 대 한 기본 매개 변수를 구성할 수 있습니다. 이러한 기본 매개 변수는 할당량 또는 파일 차단 이벤트가 발생할 때 생성 되는 인시던트 보고서에 사용 됩니다. 예약 된 보고서와 요청 시 실행 보고서에도 사용 되며 이러한 보고서의 특정 속성을 정의할 때 기본 매개 변수를 재정의할 수 있습니다.

> [!Important]
> 보고서 유형에 대 한 기본 매개 변수를 변경 하면 모든 인시던트 보고서와 기본값을 사용 하는 예약 된 기존 보고서 태스크가 변경 내용에 영향을 줍니다.

## <a name="to-configure-the-default-parameters-for-storage-reports"></a>저장소 보고서에 대 한 기본 매개 변수를 구성 하려면

1. 콘솔 트리에서 **파일 서버 리소스 관리자**를 마우스 오른쪽 단추로 클릭 하 고 **옵션 구성**을 클릭 합니다. **파일 서버 리소스 관리자 옵션** 대화 상자가 열립니다.

2. **저장소 보고서** 탭의 **기본 매개 변수 구성**에서 수정할 보고서 유형을 선택 합니다.

3. **매개 변수 편집**을 클릭 합니다.

4. 선택한 보고서 유형에 따라 다양 한 보고서 매개 변수를 편집할 수 있습니다. 필요한 모든 수정 작업을 수행 하 고 **확인** 을 클릭 하 여 해당 보고서 유형에 대 한 기본 매개 변수로 저장 합니다.

5.  편집 하려는 각 보고서 형식에 대해 2 ~ 4 단계를 반복 합니다.

6. 모든 보고서에 대 한 기본 매개 변수 목록을 보려면 **보고서 검토**를 클릭 합니다. 그런 다음 **닫기**를 클릭합니다.

7.  **확인**을 클릭합니다.

## <a name="additional-references"></a>추가 참조

-   [파일 서버 리소스 관리자 옵션 설정](setting-file-server-resource-manager-options.md)
-   [스토리지 보고서 관리](storage-reports-management.md)