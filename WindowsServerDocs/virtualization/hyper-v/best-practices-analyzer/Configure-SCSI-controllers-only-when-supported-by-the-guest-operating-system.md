---
title: 게스트 운영 체제에서 지 원하는 경우에 SCSI 컨트롤러를 구성 합니다.
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 861f194f-467e-4b07-a1c5-55b35f6327c4
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: cf206d9568ef7634d724f3fce450985c34ebfac5
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80862166"
---
# <a name="configure-scsi-controllers-only-when-supported-by-the-guest-operating-system"></a>게스트 운영 체제에서 지 원하는 경우에 SCSI 컨트롤러를 구성 합니다.

>적용 대상: Windows Server 2016


  
|속성|세부 정보|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**등급**|경고|  
|**범주**|구성|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>문제  
  
*게스트 운영 체제에서 SCSI 컨트롤러를 지원 하지 않기 때문에 사용할 수 없는 SCSI 컨트롤러를 사용 하 여 가상 컴퓨터를 구성 했습니다.*  
  
## <a name="impact"></a>영향  
  
*가상 컴퓨터는 SCSI 컨트롤러에 연결 된 저장소를 사용할 수 없습니다. 이는 다음과 같은 가상 컴퓨터에 영향을 줍니다.*  
  
가상 컴퓨터 \<목록 >  
  
## <a name="resolution"></a>해상도  
  
*가상 컴퓨터를 종료 하 고 Hyper-v 관리자를 사용 하 여 가상 컴퓨터에서 SCSI 컨트롤러를 제거 합니다. 그런 다음 가상 컴퓨터를 다시 시작 합니다.*  
  


