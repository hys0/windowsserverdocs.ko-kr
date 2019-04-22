---
title: 알림 제한 구성
description: 이 문서에서는 다양한 알림 유형에 시간 제한을 추가하는 방법을 설명합니다.
ms.date: 7/7/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: dba5b3b3c8b651935ec3c69695583d04087b7f2d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59826314"
---
# <a name="configure-notification-limits"></a>알림 제한 구성

> 적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

할당량 임계값을 반복적으로 초과하여 누적되거나 허가되지 않은 파일을 저장하려는 시도에 대한 알림의 수를 줄이려면, 파일 서버 리소스 관리자가 다음 알림 유형에 시간 제한을 적용합니다.

-   전자 메일
-   이벤트 로그
-   Command
-   보고서

각 제한은 동일한 문제에 대한 같은 유형의 구성된 알림이 생성되기 전의 기간을 지정합니다.

기본 60분 제한이 각 알림 유형에 설정되어 있지만, 이러한 제한을 변경할 수 있습니다. 제한은 지정된 유형의 모든 알림에 적용됩니다. 할당량 임계값 또는 파일 차단 이벤트에 의해 생성되었는지에 관계없습니다.

## <a name="to-specify-a-standard-notification-limit-for-each-notification-type"></a>각 알림 유형에 대한 표준 알림 제한을 지정하려면

1.  콘솔 트리에서 마우스 오른쪽 단추로 **파일 서버 리소스 관리자**를 클릭하고 **구성 옵션**을 클릭합니다. **파일 서버 리소스 관리자 옵션** 대화 상자가 열립니다.

2.  **알림 제한** 탭에서, 표시된 각 알림 유형에 대해 분 단위의 값을 입력합니다.

3.  **확인**을 클릭합니다.

> [!Note]
> 특정 할당량이나 파일 차단에 대한 알림과 관련된 시간 제한을 사용자 지정하려면, 파일 서버 리소스 관리자 명령줄 도구 **Dirquota.exe** 및 **Filescrn.exe**를 사용하거나 [파일 서버 리소스 관리자](https://technet.microsoft.com/itpro/powershell/windows/fileserverresourcemanager/fileserverresourcemanager) cmdlet을 사용합니다.

## <a name="see-also"></a>참조

-   [설정 파일 서버 리소스 관리자 옵션](setting-file-server-resource-manager-options.md)
-   [명령줄 도구](command-line-tools.md)