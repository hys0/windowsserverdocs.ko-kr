---
title: VHD 포맷 동적 가상 하드 디스크는 프로덕션 환경에서 서버 작업을 실행 하는 가상 컴퓨터에 대 한 권장 되지 않습니다.
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 324a60a0-1d15-4ef2-9f17-23cbd2eb42ce
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: bf5464208fc145a31571f01822bb5ba54efe89c4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71364595"
---
# <a name="vhd-format-dynamic-virtual-hard-disks-are-not-recommended-for-virtual-machines-that-run-server-workloads-in-a-production-environment"></a>VHD 포맷 동적 가상 하드 디스크는 프로덕션 환경에서 서버 작업을 실행 하는 가상 컴퓨터에 대 한 권장 되지 않습니다.

>적용 대상: Windows Server 2016

모범 사례 분석기 및 검사에 대한 자세한 내용은 [모범 사례 분석기 검사 실행 및 검사 결과 관리](https://go.microsoft.com/fwlink/p/?LinkID=223177)를 참조하세요.  
  
|속성|설명|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**Severity**|경고|  
|**범주**|Configuration|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.
  
## <a name="issue"></a>**문제점**  
*하나 이상의 가상 컴퓨터에서 VHD 형식의 동적 확장 가상 하드 디스크를 사용 합니다.*  
  
## <a name="impact"></a>**식**  
*VHD 형식의 동적 가상 하드 디스크는 전원 오류가 발생 하는 경우 일관성 문제가 발생할 수 있습니다. 실제 디스크 전원 오류가 발생 하면 수정 되는.vhd 파일에는 섹터에 대 한 불완전 하거나 잘못 된 업데이트를 수행 하는 경우 일관성 문제가 발생할 수 있습니다. 이는 다음과 같은 가상 컴퓨터에 영향을 줍니다.*  
  
@no__t-가상 머신 목록 >  
  
## <a name="resolution"></a>**해결 방법**  
@no__t-가상 머신을 종료 하 고 VHD 포맷 동적 가상 하드 디스크를 VHDX 형식 가상 하드 디스크 또는 고정 가상 하드 디스크로 변환 합니다. (VHDX 형식의 디스크 시스템 전원 오류로 인 한 손상을에서 보호 하는 데 안정성 메커니즘에 있습니다.) 그러나 이전 버전 Windows의 어느 시점에 연결 될 가능성이 높은 경우에 가상 하드 디스크 변환 하지 않습니다. Windows Server 2012 이전의 windows 릴리스는 VHDX 형식을 지원 하지 않습니다. *  
  


