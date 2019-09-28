---
title: 가상 컴퓨터에 모든 integration services를 사용 하도록 설정
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 16e202ad-3795-40c9-8176-7ca319e56d26
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 1984c3d1d6261756bf83f899985b457681537046
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71364894"
---
# <a name="enable-all-integration-services-in-virtual-machines"></a>가상 컴퓨터에 모든 integration services를 사용 하도록 설정

>적용 대상: Windows Server 2016

모범 사례 및 검사에 대한 자세한 내용은 [모범 사례 분석기](https://go.microsoft.com/fwlink/?LinkId=122786)를 참조하세요.  
  
|속성|설명|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**Severity**|경고|  
|**범주**|Configuration|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>문제점  
  
*하나 이상의 integration services가 가상 머신에서 사용 하지 않도록 설정 되었거나 작동 하지 않습니다.*  
  
## <a name="impact"></a>영향  
  
*다음 가상 컴퓨터에 대해 서비스 또는 통합 기능이 제대로 작동 하지 않을 수 있습니다.*  
  
@no__t-가상 머신 이름의 목록 >  
  
## <a name="resolution"></a>해결 방법  
  
*서비스 스냅인 또는 sc config 명령줄 도구를 사용 하 여 서비스가 자동으로 시작 되도록 구성 되어 있고 중지 되지 않았는지 확인 합니다.*  
  
#### <a name="to-configure-how-a-service-is-started-using-the-services-snap-in"></a>서비스 스냅인을 사용 하 여 시작 되는 서비스 방법을 구성 하려면  
  
1.  원격 데스크톱 서비스 또는 가상 컴퓨터 연결을 사용 하 여 게스트 운영 체제에 가상 컴퓨터 및 로그에 연결 합니다.  
  
2.  서비스를 엽니다. (클릭 **시작**, 클릭는 **검색 시작** 상자에 입력 합니다 **services.msc**, 한 다음 ENTER를 누릅니다.)  
  
3.  세부 정보 창에서 서비스를 구성 하 고 클릭 한 다음 마우스 오른쪽 단추로 클릭 **속성**합니다.  
  
4.  에 **일반** 탭 **시작** 입력, 클릭 **자동**합니다.  
  
#### <a name="to-configure-how-a-service-is-started-using-sc-config"></a>SC Config를 사용 하 여 시작 되는 서비스 방법을 구성 하려면  
  
1.  Windows PowerShell을 엽니다. (바탕 화면에서 클릭 **시작** 입력을 시작 하 고 **Windows PowerShell**.)  
  
2.  마우스 오른쪽 단추로 클릭 **Windows PowerShell** 클릭 **관리자 권한으로 실행**합니다.  
  
3.  < 서비스 이름 > 대체 서비스의 이름으로 입력 합니다.  
  
    ```  
    sc config <service-name> start=auto  
    ```  
  


