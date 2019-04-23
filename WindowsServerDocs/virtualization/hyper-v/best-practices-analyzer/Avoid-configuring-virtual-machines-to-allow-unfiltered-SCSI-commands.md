---
title: 필터링 되지 않은 SCSI 명령을 허용 하도록 가상 컴퓨터를 구성 하지 않으려면
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: dd4a3d78-a77f-451e-a383-d5cf45ea17cf
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: f401ce4d72f88d72529a95acea2a999df93679b6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59888274"
---
# <a name="avoid-configuring-virtual-machines-to-allow-unfiltered-scsi-commands"></a>필터링 되지 않은 SCSI 명령을 허용 하도록 가상 컴퓨터를 구성 하지 않으려면

>적용 대상: Windows Server 2016


  
*모범 사례 및 검사 하는 방법에 대 한 자세한 내용은 참조 하십시오* [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786)합니다.  
  
|속성|설명|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**Severity**|경고|  
|**범주**|작업|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>문제점  
  
*가상 컴퓨터는 필터링 되지 않은 SCSI 명령을 허용 하도록 구성 됩니다.*  
  
## <a name="impact"></a>영향  
  
*보안 위험 SCSI 명령을 필터링 동작을 무시 합니다. 게스트 운영 체제에서 실행 중인 저장소 응용 프로그램 호환성을 위해 필요한 경우에이 구성은 사용 하도록 설정 해야 합니다. 다음 가상 컴퓨터는 필터링 되지 않은 SCSI 명령을 허용 하도록 구성 됩니다.*  
  
\<가상 머신 이름 목록 >  
  
## <a name="resolution"></a>해결 방법  
  
*이 구성은 필요한 지 확인 하려면 저장소 공급 업체에 문의 합니다. 또한 관리 운영 체제나 다른 게스트 운영 체제 손상 또는 비정상적인 동작을 노출 하는 경우 명령을 차단 하도록 가상 머신을 다시 구성 합니다.*  
  


