---
title: 주 전에 integration services를 설치 해야 하거나 복제본 가상 컴퓨터가 장애 조치 후 대체 IP 주소를 사용할 수 있는
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전으로, 자세한 정보에 대 한 링크를 제공 합니다.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: a7fdd185-d6c8-4f58-9b58-2df5827bb056
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 58e744c182fb2013e55e91f58140c6ba14181f9f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71393594"
---
# <a name="integration-services-must-be-installed-before-primary-or-replica-virtual-machines-can-use-an-alternate-ip-address-after-a-failover"></a>주 전에 integration services를 설치 해야 하거나 복제본 가상 컴퓨터가 장애 조치 후 대체 IP 주소를 사용할 수 있는

>적용 대상: Windows Server 2016

모범 사례 분석기 및 검사에 대한 자세한 내용은 [모범 사례 분석기 검사 실행 및 검사 결과 관리](https://go.microsoft.com/fwlink/p/?LinkID=223177)를 참조하세요.  
  
|속성|세부 정보|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**Severity**|Error|  
|**범주**|Configuration|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>문제점  
*복제에 참여 하는 가상 컴퓨터는 장애 조치 (failover) 시에 특정 IP 주소를 사용 하도록 구성할 수 있습니다. 단, 가상 컴퓨터의 게스트 운영 체제에 integration services가 설치 되어 있는 경우에만 가능 합니다.*  
  
## <a name="impact"></a>영향  
*장애 조치 (failover) (계획 됨, 계획 되지 않음 또는 테스트)가 발생 한 경우 복제본 가상 머신은 주 가상 머신과 동일한 IP 주소를 사용 하 여 온라인 상태로 전환 됩니다. 이 구성으로 인해 연결 문제가 발생할 수 있습니다. 이는 다음과 같은 가상 컴퓨터에 영향을 줍니다.*  
  
가상 컴퓨터 \<목록 >  
  
## <a name="resolution"></a>해결 방법  
*가상 컴퓨터 연결을 사용 하 여 가상 컴퓨터에 integration services를 설치 합니다.*  
  
Windows Server 2016 년 Windows 가상 컴퓨터에 대 한 통합 서비스는 Windows Update를 통해 전달 됩니다. 이러한 가상 컴퓨터 통합 서비스의 최신 버전을 가져오려면 Windows 업데이트를 수신 하도록 구성 되었는지 확인 합니다. Linux 커널 이제 Linux 통합 서비스 (LIS)을 포함 하 고 새 릴리스를 위한 업데이트 하지만 최신 기능 향상 또는 수정 이전 커널에 따라 Linux 배포판 없을 수 있습니다. 자세한 내용은 [Windows에서 hyper-v에 대해 지원 되는 Linux 및 FreeBSD 가상 컴퓨터](../Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md)를 참조 하세요.


