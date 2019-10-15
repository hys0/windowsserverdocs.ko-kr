---
title: 인증서 기반 인증이 구성 되어 있지만 지정된 된 인증서가 복제 서버 또는 장애 조치 클러스터 노드에 설치 되어 있지
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 4cabbce3-9367-4ddc-a108-1e5e1ab2bcff
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 0b107a4760cc3470c7f80d53feef00a2f8f789c5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71365205"
---
# <a name="certificate-based-authentication-is-configured-but-the-specified-certificate-is-not-installed-on-the-replica-server-or-failover-cluster-nodes"></a>인증서 기반 인증이 구성 되어 있지만 지정된 된 인증서가 복제 서버 또는 장애 조치 클러스터 노드에 설치 되어 있지

>적용 대상: Windows Server 2016


  
*모범 사례 및 검사에 대한 자세한 내용은* [모범 사례 분석기](https://go.microsoft.com/fwlink/?LinkId=122786)를 참조하세요.  
  
|속성|설명|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**Severity**|Error|  
|**범주**|Configuration|  

다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.

## <a name="issue"></a>문제점  
  
*Hyper-v 복제본이 인증서 기반 복제를 제공 하는 데 사용 하도록 구성 된 보안 인증서가 복제 서버 (또는 장애 조치 (failover) 클러스터 노드)에 설치 되어 있지 않습니다.*  
  
## <a name="impact"></a>영향  
  
클러스터 장애 조치 (failover) 또는 다른 노드로 이동 하는 경우에 *새 노드에 적절 한 인증서가 설치 되어 있지 않으면 Hyper-v 복제가 일시 중지 됩니다. 이는 다음 노드에 영향을 줍니다.*  
  
\< 개 노드 목록 >  
  
## <a name="resolution"></a>해결 방법  
  
*복제 서버 (및 장애 조치 (failover) 클러스터의 모든 연결 된 노드 (있는 경우)에 구성 된 인증서를 설치 합니다.*  
  


