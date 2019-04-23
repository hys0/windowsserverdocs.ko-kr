---
title: 가상 컴퓨터에서 하나 이상의 외부 가상 네트워크에 배타적으로 사용을 예약 합니다.
description: 이 모범 사례 분석기 규칙에 의해 보고 된 문제를 해결 하려면 지침을 제공 합니다.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: f7732258-93f1-44e8-835b-5ad2d1c45cd9
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: c8c90a74352bae0b348608db0fc05107e4d09010
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59884744"
---
# <a name="reserve-one-or-more-external-virtual-networks-for-exclusive-use-by-virtual-machines"></a>가상 컴퓨터에서 하나 이상의 외부 가상 네트워크에 배타적으로 사용을 예약 합니다.

>적용 대상: Windows Server 2016

모범 사례 및 검사에 대한 자세한 내용은 [모범 사례 분석기](https://go.microsoft.com/fwlink/?LinkId=122786)를 참조하세요.  
  
|속성|설명|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**Severity**|Error|  
|**범주**|Configuration|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>문제점  
  
*모든 외부 가상 네트워크 관리 운영 체제와 가상 컴퓨터에서 사용 하 여 구성 됩니다.*  
  
## <a name="impact"></a>영향  
  
*관리 운영 체제의 네트워킹 성능 저하 될 수 있습니다.*  
  
## <a name="resolution"></a>해결 방법  
  
*가상 스위치 관리자를 사용 하 여 관리 운영 체제와 외부 가상 네트워크의 공유를 중지 합니다.*  
  
#### <a name="to-stop-sharing-the-external-virtual-network-with-the-management-operating-system"></a>관리 운영 체제와 외부 가상 네트워크 공유를 중지 하려면  
  
1.  Hyper-V 관리자를 엽니다. 클릭 **시작**, 가리킨 **관리 도구**, 를 클릭 하 고 **Hyper-v 관리자**합니다.  
  
2.  **작업** 메뉴에서 **가상 스위치 관리자**를 클릭합니다.  
  
3.  아래에서 **가상 스위치**, 외부 가상 스위치의 이름을 클릭 합니다.  
  
4.  에 **연결 유형** 영역에 실제 네트워크 어댑터의 이름에서의 선택을 취소는 **이 네트워크 어댑터를 공유 하 여 관리 운영 체제** 확인란입니다.  
  
5.  **확인**을 클릭합니다.  
  


