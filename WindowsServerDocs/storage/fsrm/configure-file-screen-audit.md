---
title: 파일 차단 감사 구성
description: 이 문서에서는 파일 차단 감사 보고서를 생성 하도록 파일 화면 감사를 구성 하는 방법을 설명 합니다.
ms.date: 7/7/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: cf1824e514c34ee89870daa6d15190bffd822a8b
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85475320"
---
# <a name="configure-file-screen-audit"></a>파일 차단 감사 구성

> 적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

파일 서버 리소스 관리자를 사용 하 여 감사 데이터베이스에 파일 차단 작업을 기록할 수 있습니다. 이 데이터베이스에 저장 된 정보는 파일 차단 감사 보고서를 생성 하는 데 사용 됩니다.

> [!Important]
> **감사 데이터베이스의 기록 파일 차단 작업** 확인란의 선택을 취소 하면 파일 차단 감사 보고서에 정보가 포함 되지 않습니다.

## <a name="to-configure-file-screen-audit"></a>파일 화면 감사를 구성 하려면

1.  콘솔 트리에서 **파일 서버 리소스 관리자**를 마우스 오른쪽 단추로 클릭 하 고 **옵션 구성**을 클릭 합니다. **파일 서버 리소스 관리자 옵션** 대화 상자가 열립니다.

2.  **파일 화면 감사** 탭의 **감사 데이터베이스에서 파일 차단 작업 기록** 확인란을 선택 합니다.

3.  **확인**을 클릭합니다. 모든 파일 차단 작업은 이제 감사 데이터베이스에 저장 되며 파일 차단 감사 보고서를 실행 하 여 볼 수 있습니다.

## <a name="additional-references"></a>추가 참조

-   [파일 서버 리소스 관리자 옵션 설정](setting-file-server-resource-manager-options.md)
-   [스토리지 보고서 관리](storage-reports-management.md)