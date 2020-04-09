---
title: 필터링 되지 않은 SCSI 명령을 허용 하도록 가상 컴퓨터를 구성 하지 않으려면
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: dd4a3d78-a77f-451e-a383-d5cf45ea17cf
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: ac059bce1704a4e72b2c373d8186dbd4e31f2164
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857796"
---
# <a name="avoid-configuring-virtual-machines-to-allow-unfiltered-scsi-commands"></a>필터링 되지 않은 SCSI 명령을 허용 하도록 가상 컴퓨터를 구성 하지 않으려면

>적용 대상: Windows Server 2016


  
*모범 사례 및 검사에 대 한 자세한 내용은 모범 사례 분석기를 참조* [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786)하세요.  
  
|속성|세부 정보|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**등급**|경고|  
|**범주**|작업|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>문제  
  
*가상 머신은 필터링 되지 않은 SCSI 명령을 허용 하도록 구성 됩니다.*  
  
## <a name="impact"></a>영향  
  
*SCSI 명령 필터링을 무시 하면 보안 위험이 발생 합니다. 게스트 운영 체제에서 실행 되는 저장소 응용 프로그램과의 호환성을 위해 필요한 경우에만이 구성을 사용 하도록 설정 해야 합니다. 다음 가상 머신은 필터링 되지 않은 SCSI 명령을 허용 하도록 구성 됩니다.*  
  
가상 컴퓨터 이름 목록 \<>  
  
## <a name="resolution"></a>해상도  
  
*이 구성이 필요한 지 확인 하려면 저장소 공급 업체에 문의 하세요. 또한 관리 운영 체제 또는 다른 게스트 운영 체제가 손상 되거나 비정상적인 동작을 발생 하는 경우 가상 컴퓨터를 다시 구성 하 여 명령을 차단 합니다.*  
  


