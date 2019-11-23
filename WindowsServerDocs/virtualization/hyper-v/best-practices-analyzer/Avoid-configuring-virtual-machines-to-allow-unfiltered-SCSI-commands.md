---
title: 필터링 되지 않은 SCSI 명령을 허용 하도록 가상 컴퓨터를 구성 하지 않으려면
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: dd4a3d78-a77f-451e-a383-d5cf45ea17cf
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 5deb20862ed0e359febd4a9b58202d53c85058ca
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71365275"
---
# <a name="avoid-configuring-virtual-machines-to-allow-unfiltered-scsi-commands"></a>필터링 되지 않은 SCSI 명령을 허용 하도록 가상 컴퓨터를 구성 하지 않으려면

>적용 대상: Windows Server 2016


  
*모범 사례 및 검사에 대한 자세한 내용은* [모범 사례 분석기](https://go.microsoft.com/fwlink/?LinkId=122786)를 참조하세요.  
  
|속성|세부 정보|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**Severity**|경고|  
|**범주**|작업|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>문제점  
  
*가상 머신은 필터링 되지 않은 SCSI 명령을 허용 하도록 구성 됩니다.*  
  
## <a name="impact"></a>영향  
  
*SCSI 명령 필터링을 무시 하면 보안 위험이 발생 합니다. 게스트 운영 체제에서 실행 되는 저장소 응용 프로그램과의 호환성을 위해 필요한 경우에만이 구성을 사용 하도록 설정 해야 합니다. 다음 가상 머신은 필터링 되지 않은 SCSI 명령을 허용 하도록 구성 됩니다.*  
  
가상 컴퓨터 이름 목록 \<>  
  
## <a name="resolution"></a>해결 방법  
  
*이 구성이 필요한 지 확인 하려면 저장소 공급 업체에 문의 하세요. 또한 관리 운영 체제 또는 다른 게스트 운영 체제가 손상 되거나 비정상적인 동작을 발생 하는 경우 가상 컴퓨터를 다시 구성 하 여 명령을 차단 합니다.*  
  


