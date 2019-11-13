---
title: 볼륨 또는 폴더에 할당량 적용
description: 이 문서에서는 볼륨 또는 폴더에 저장소 할당량을 적용하는 방법을 설명합니다.
ms.date: 7/7/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 44eea3c3802e261239db9bf8350777e1b83fb9c4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71394326"
---
# <a name="checklist-apply-a-quota-to-a-volume-or-folder"></a>검사 목록: 볼륨 또는 폴더에 할당량 적용

> 적용 대상: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server (반기 채널)

1. 임계값 알림에 또는 저장소 보고서를 전자 메일로 보내려면 전자 메일 설정을 구성합니다. [전자 메일 알림 구성](configure-email-notifications.md)

2. 볼륨 또는 폴더에서 저장소 요구 사항을 평가합니다. **저장소 보고서 관리** 노드의 보고서를 사용하여 데이터를 제공할 수 있습니다. (예를 들어, 요청 시 소유자별 파일 보고서를 실행하여 디스크 공간의 많은 용량을 사용하는 사용자를 파악합니다.)[요청 시 보고서 생성](generate-reports-on-demand.md)

3. 사용 가능한 미리 구성된 할당량 템플릿을 검토합니다. **할당량 관리**에서 **할당량 템플릿** 노드를 클릭 합니다. [할당량 템플릿 속성 편집](edit-quota-template-properties.md) 
<br />-또는- <br /> 조직에 저장소 정책을 적용하기 위한 새 할당량 템플릿을 만듭니다. [할당량 템플릿 만들기](create-quota-template.md)

4. 볼륨 또는 폴더에서 템플릿을 기반으로 할당량을 만듭니다.  
 [할당량 만들기](create-quota.md) <br /> -또는- <br /> 볼륨 또는 폴더의 하위 폴더에 대한 할당량을 자동으로 생성하기 위한 할당량 자동 적용을 만듭니다. [할당량 자동 적용 만들기](create-auto-apply-quota.md)

6. 할당량 사용을 주기적으로 모니터링하기 위한 할당량 사용 보고서를 포함하는 보고서 작업을 예약합니다. [보고서 세트 예약](schedule-set-of-reports.md)

> [!Note]
> 볼륨 또는 폴더에서 파일을 차단하려는 경우 [검사 목록: 볼륨 또는 폴더에 파일 차단 적용](checklist-apply-file-screen-to-volume-or-folder.md)을 참조하세요.











