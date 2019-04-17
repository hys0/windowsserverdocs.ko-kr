---
title: "검사 목록 - 볼륨 또는 폴더에 파일 차단 적용"
description: "이 문서에서는 볼륨 또는 폴더에 파일 차단을 적용하는 방법을 설명합니다."
ms.date: 7/7/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: f4c6953d27361ab2e3210a1574a5988e434f701f
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2017
---
# <a name="checklist---apply-a-file-screen-to-a-volume-or-folder"></a>검사 목록 - 볼륨 또는 폴더에 파일 차단 적용

> 적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

볼륨 또는 폴더에 파일 차단을 적용하려면 다음 목록을 사용합니다.
1. [전자 메일 알림 구성](configure-email-notifications.md)의 지침에 따라 전자 메일로 파일 차단 알림 또는 저장소 보고서를 보내려면 전자 메일 설정을 구성합니다.

2. 파일 차단 감사 보고서를 생성하려면 감사 데이터베이스에서 차단 이벤트를 기록하도록 설정합니다.
[파일 차단 감사 구성](configure-file-screen-audit.md)

3. 차단 규칙의 후보인 저장된 파일 형식을 평가합니다. **저장소 보고서 관리** 노드의 보고서를 사용하여 데이터를 제공할 수 있습니다. (예를 들어, 파일을 파일 그룹 보고서 또는 요청 시 대용량 파일 보고서를 실행하여 많은 디스크 공간을 차지하는 파일을 파악합니다.)[요청 시 보고서 생성](generate-reports-on-demand.md) 

4. 미리 구성된 파일 그룹을 검토하거나 조직에 특정 차단 정책을 적용하기 위한 새 파일 그룹을 만듭니다. [차단을 위한 파일 그룹 정의](define-file-groups-for-screening.md)  

5. 사용할 수 있는 파일 차단 템플릿의 속성을 검토합니다. (**파일 차단 관리**에서 **파일 차단 템플릿** 노드를 클릭합니다.)[파일 차단 템플릿 속성 편집](edit-file-screen-template-properties.md) 
<br />
 -또는-
 <br /> 조직에 저장소 정책을 적용하기 위한 새 파일 차단 템플릿을 만듭니다.  [파일 차단 템플릿 만들기](create-file-screen-template.md) 

6. 볼륨 또는 폴더에서 템플릿을 기반으로 파일 차단을 만듭니다. 
 [파일 차단 만들기](create-file-screen.md)
 
7. 볼륨 또는 폴더의 하위 폴더에서 파일 차단 예외를 구성합니다. [파일 차단 예외 만들기](create-file-screen-exception.md) 

8. 차단 활동을 주기적으로 모니터링할 수 있도록 파일 차단 감사 보고서가 포함된 작업을 예약합니다.
  [보고서 집합 예약](schedule-set-of-reports.md)


> [!NOTE]
> 볼륨 또는 폴더에서 저장소를 제한하려면 [검사 목록: 볼륨 또는 폴더에 할당량 적용](checklist-apply-file-screen-to-volume-or-folder.md)