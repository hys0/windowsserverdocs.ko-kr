---
title: 인증서 기반 인증이 구성 되어 있지만 지정된 된 인증서가 복제 서버 또는 장애 조치 클러스터 노드에 설치 되어 있지
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 4cabbce3-9367-4ddc-a108-1e5e1ab2bcff
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: feef30d2f798057e4bd8e53ebab240af6b1d25b8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59832944"
---
# <a name="certificate-based-authentication-is-configured-but-the-specified-certificate-is-not-installed-on-the-replica-server-or-failover-cluster-nodes"></a>인증서 기반 인증이 구성 되어 있지만 지정된 된 인증서가 복제 서버 또는 장애 조치 클러스터 노드에 설치 되어 있지

>적용 대상: Windows Server 2016


  
*모범 사례 및 검사 하는 방법에 대 한 자세한 내용은 참조 하십시오* [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786)합니다.  
  
|속성|설명|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**Severity**|Error|  
|**범주**|Configuration|  

다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.

## <a name="issue"></a>문제점  
  
*보안 인증서를 Hyper-v 복제본 인증서 기반 복제 복제 서버 (또는 모든 장애 조치 클러스터 노드)에 설치 되어 있지 제공를 사용 하도록 구성 되어 있습니다.*  
  
## <a name="impact"></a>영향  
  
*클러스터 장애 조치 또는 다른 노드로 이동 발생할 경우 새 노드도 없는 경우 적절 한 인증서가 설치 되어 Hyper-v 복제 일시 중지 됩니다. 다음 노드에 영향을 주는:*  
  
\<노드 목록 >  
  
## <a name="resolution"></a>해결 방법  
  
*복제본 서버 (및 연결 된 모든 노드 장애 조치 클러스터에 있는 경우)에 구성 된 인증서를 설치 합니다.*  
  


