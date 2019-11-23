---
title: 이상을 사용 가상 컴퓨터에 대 한 파일을 저장 하는 파일 공유에 대 한 SMB 프로토콜 버전 3.0입니다.
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 4bb832b8-f1aa-4c1f-a0f2-324dd53553ea
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: af23c3c860a47d0dd9096bc3f5ff466aca7836b6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71393316"
---
# <a name="use-at-least-smb-protocol-version-30-for-file-shares-that-store-files-for-virtual-machines"></a>이상을 사용 가상 컴퓨터에 대 한 파일을 저장 하는 파일 공유에 대 한 SMB 프로토콜 버전 3.0입니다.

>적용 대상: Windows Server 2016

모범 사례 분석기 및 검사에 대한 자세한 내용은 [모범 사례 분석기 검사 실행 및 검사 결과 관리](https://go.microsoft.com/fwlink/p/?LinkID=223177)를 참조하세요.  
  
|속성|세부 정보|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**Severity**|Error|  
|**범주**|Configuration|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>**문제점**  
*가상 머신 파일 또는 가상 하드 디스크 파일은 SMB 프로토콜 버전 3.0 이상을 지원 하지 않는 파일 공유에 저장 됩니다.*  
  
## <a name="impact"></a>**식**  
*Microsoft는이 구성을 지원 하지 않습니다. 이는 다음과 같은 가상 컴퓨터에 영향을 줍니다.*  
  
가상 컴퓨터 \<목록 >  
  
## <a name="resolution"></a>**해결 방법**  
*SMB 프로토콜 버전 3.0 이상을 사용 하는 파일 공유로 파일을 이동 합니다.*  
  


