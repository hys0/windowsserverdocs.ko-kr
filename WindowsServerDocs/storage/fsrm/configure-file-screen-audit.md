---
title: 파일 차단 감사 구성
description: 이 문서에서는 파일 차단 감사 보고서를 생성하기 위해 파일 차단 감사를 구성하는 방법을 설명합니다.
ms.date: 7/7/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: a9444e158a935f4e931aa7a5d634d970c5acc88e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71394570"
---
# <a name="configure-file-screen-audit"></a>파일 차단 감사 구성

> 적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

파일 서버 리소스 관리자를 사용하여 파일 차단 활동을 감사 데이터베이스에 기록할 수 있습니다. 이 데이터베이스에 저장된 정보는 파일 차단 감사 보고서를 생성하는 데 사용됩니다.

> [!Important]
> **감사 데이터베이스에 파일 차단 활동 기록** 확인란의 선택을 취소하면, 파일 차단 감사 보고서에 아무런 정보가 포함되지 않습니다.

## <a name="to-configure-file-screen-audit"></a>파일 차단 감사를 구성하려면

1.  콘솔 트리에서 마우스 오른쪽 단추로 **파일 서버 리소스 관리자**를 클릭하고 **구성 옵션**을 클릭합니다. **파일 서버 리소스 관리자 옵션** 대화 상자가 열립니다.

2.  **파일 차단 감사** 탭에서 **감사 데이터베이스에 파일 차단 활동 기록** 확인란을 선택합니다.

3.  **확인**을 클릭합니다. 이제 모든 파일 차단 활동이 감사 데이터베이스에 저장되며, 파일 차단 감사 보고서를 실행하여 볼 수 있습니다.

## <a name="see-also"></a>참조

-   [파일 서버 리소스 관리자 옵션 설정](setting-file-server-resource-manager-options.md)
-   [스토리지 보고서 관리](storage-reports-management.md)