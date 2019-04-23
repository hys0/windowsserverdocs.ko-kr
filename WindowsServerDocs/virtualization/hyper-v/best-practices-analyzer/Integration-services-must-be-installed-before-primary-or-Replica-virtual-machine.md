---
title: 주 전에 integration services를 설치 해야 하거나 복제본 가상 컴퓨터가 장애 조치 후 대체 IP 주소를 사용할 수 있는
description: 자세한 정보에 대 한 링크를 사용 하 여이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: a7fdd185-d6c8-4f58-9b58-2df5827bb056
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 1ff8dbfd71655aee86ba7d0feac87ec2267a2171
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59865514"
---
# <a name="integration-services-must-be-installed-before-primary-or-replica-virtual-machines-can-use-an-alternate-ip-address-after-a-failover"></a>주 전에 integration services를 설치 해야 하거나 복제본 가상 컴퓨터가 장애 조치 후 대체 IP 주소를 사용할 수 있는

>적용 대상: Windows Server 2016

모범 사례 분석기 및 검사에 대한 자세한 내용은 [모범 사례 분석기 검사 실행 및 검사 결과 관리](https://go.microsoft.com/fwlink/p/?LinkID=223177)를 참조하세요.  
  
|속성|설명|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**Severity**|Error|  
|**범주**|Configuration|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>문제점  
*가상 컴퓨터 복제에 참여 하는 장애 조치의 경우 특정 IP 주소를 사용 하도록 구성 된 경우에 가상 컴퓨터의 게스트 운영 체제에 통합 서비스가 설치 되어 수 있습니다.*  
  
## <a name="impact"></a>영향  
*장애 조치 (계획 되지 않은 계획 또는 테스트)의 경우 복제본 가상 머신이 주 가상 컴퓨터와 동일한 IP 주소를 사용 하 여 온라인 상태가 됩니다. 이 구성은 연결에 문제가 발생할 수 있습니다. 이 가상 컴퓨터에 영향을 줍니다.*  
  
\<가상 머신의 목록 >  
  
## <a name="resolution"></a>해결 방법  
*가상 컴퓨터에서 integration services를 설치 하려면 가상 머신 연결을 사용 합니다.*  
  
Windows Server 2016 년 Windows 가상 컴퓨터에 대 한 통합 서비스는 Windows Update를 통해 전달 됩니다. 이러한 가상 컴퓨터 통합 서비스의 최신 버전을 가져오려면 Windows 업데이트를 수신 하도록 구성 되었는지 확인 합니다. Linux 커널 이제 Linux 통합 서비스 (LIS)을 포함 하 고 새 릴리스를 위한 업데이트 하지만 최신 기능 향상 또는 수정 이전 커널에 따라 Linux 배포판 없을 수 있습니다. 자세한 내용은 참조 하세요 [Windows의 Hyper-v에 대 한 지원 되는 Linux 및 FreeBSD 가상 컴퓨터](../Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md)합니다.


