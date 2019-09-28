---
title: Hyper-v에 대 한 모범 사례 분석기
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 3747faa5-6e9f-499e-8a79-3fb9d73b6b92
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 671e1de78b390e1b595bb218ece375e88a47155b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71365152"
---
# <a name="best-practices-analyzer-for-hyper-v"></a>Hyper-v에 대 한 모범 사례 분석기

>적용 대상: Windows Server 2016
  
Windows 관리에서 *모범 사례*는 일반적인 환경에서 전문가가 정의한 대로 서버를 구성할 수 있는 이상적인 방법으로 간주됩니다. 모범 사례 위반은, 중요 한 것에도, 문제를 반드시 유발 될 수 있습니다. 그러나 성능 저하, 안정성 저하, 예상치 못한 충돌, 보안 위험 증가 또는 다른 잠재적 문제가 발생할 수 있는 서버 구성을 지정할 수 있습니다.  
  
이러한 모범 사례에 따라 규칙을 사용 하 여 컴퓨터를 검색 하 고 결과 보고 하는 모범 사례 분석기. 각 모범 사례 규칙 규칙을 준수 하는 방법에 대 한 세부 정보를 포함 합니다. 이 섹션의 문서 Hyper-v에 적용 되는 모범 사례를 이해할 수 있도록 하기 위해 이러한 규칙도 결과 해석 검사를 발견 하지 모범 사례를 준수 하는 조건입니다.  
  
모범 사례 분석기 및 검사 하는 방법에 대 한 자세한 내용은 참조 하십시오. [모범 사례 분석기](https://go.microsoft.com/fwlink/?LinkId=122786)합니다.  
  
## <a name="about-hyper-v"></a>Hyper-V 정보  
Hyper-v 가상 컴퓨터에서 실행 하 여 하나의 물리적 컴퓨터에서 동시에 여러 운영 체제를 실행할 수 있습니다. 가상 컴퓨터 보다 효율적이 고 유연 하 게 컴퓨팅 리소스를 사용할 수 있습니다. Hyper-v에 대 한 자세한 내용은 [Windows Server 2016에 Hyper-v](../Hyper-V-on-Windows-Server.md)합니다.  
  


