---
title: 이 서버에서 복제는 하나 이상의 가상 컴퓨터에 대 한 일시 중지
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: e1119a40-eda3-4058-8648-7df81cbc6c29
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 248b5fbdbfb54380e441d14cde6beaa9146ce800
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59827774"
---
# <a name="replication-is-paused-for-one-or-more-virtual-machines-on-this-server"></a>이 서버에서 복제는 하나 이상의 가상 컴퓨터에 대 한 일시 중지

>적용 대상: Windows Server 2016

모범 사례 분석기 및 검사에 대한 자세한 내용은 [모범 사례 분석기 검사 실행 및 검사 결과 관리](https://go.microsoft.com/fwlink/p/?LinkID=223177)를 참조하세요.  
  
|속성|설명|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**Severity**|경고|  
|**범주**|작업|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>문제점  
*복제는 하나 이상의 가상 컴퓨터에 대 한 일시 중지 됩니다. 주 가상 컴퓨터 일시 중지 하는 동안 발생 하는 모든 변경 누적 됩니다 하 고 복제를 다시 시작 되 면 복제본 가상 컴퓨터에 전송 됩니다.*  
  
## <a name="impact"></a>영향  
*복제가 일시 중지,으로 주 가상 컴퓨터에서 발생 하는 누적 된 변경 주 서버에서 사용 가능한 디스크 공간을 사용 합니다. 복제를 다시 시작 된 후 복제 서버에 사용 되는 네트워크 트래픽의 큰 버스트 있을 수 있습니다. 이 가상 컴퓨터에 영향을 줍니다.*  
  
\<가상 머신의 목록 >  
  
## <a name="resolution"></a>해결 방법  
*복제가 일시 중지 하면 해당 의도 확인 합니다. 복제 주소 부족 한 디스크 공간 또는 네트워크 연결을 일시 중지 된 경우 복제는 이러한 문제가 해결 되는 즉시 다시 시작 합니다.*  
  

