---
title: Hyper-v 가상 컴퓨터 관리 서비스는 자동으로 시작 되도록 구성 해야
description: 이 모범 사례 분석기 규칙에 의해 보고 된 문제를 해결 하려면 지침을 제공 합니다.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 222bbe76-c514-4a3f-b61b-860a4dc2826a
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: c33f81678d7fdc71e81834a002fd3d7917a6f632
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59833254"
---
# <a name="the-hyper-v-virtual-machine-management-service-should-be-configured-to-start-automatically"></a>Hyper-v 가상 컴퓨터 관리 서비스는 자동으로 시작 되도록 구성 해야

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
  
*Hyper-v 가상 머신 관리 서비스가 자동으로 시작 되도록 구성 되지 않았습니다.*  
  
## <a name="impact"></a>영향  
  
*서비스가 시작 될 때까지 가상 컴퓨터를 관리할 수 없습니다.*  
  
가상 컴퓨터를 실행 하는 계속 실행 됩니다. 그러나 가상 컴퓨터를 관리 하거나 만들거나 서비스가 실행 될 때까지를 삭제할 수 없습니다.  
  
## <a name="resolution"></a>해결 방법  
  
*서비스 스냅인 또는 sc config 명령줄 도구를 사용 하 여 자동으로 시작 되도록 서비스를 다시 구성 합니다.*  
  
> [!TIP]  
> 데스크톱 응용 프로그램에서 서비스를 찾을 수 없습니다 또는 명령줄 도구는 서비스가 존재 하지 않으면 Hyper-v 관리 도구 것을 보고 하는 경우 설치 되지 않습니다. 설치:  
>   
> - Windows server에서는 서버 관리자를 열고 역할 및 기능 추가 마법사를 사용 합니다. 자세한 내용은 다음을 참조 하십시오. [Windows Server 2016에 Hyper-v 역할을 설치](../get-started/Install-the-Hyper-V-role-on-Windows-Server.md)합니다.  
> - Windows에서 바탕 화면에서 입력을 시작 **프로그램**, 클릭 **프로그램 및 기능** (제어판) > **Windows 기능 설정 또는 해제** > **Hyper-v** > **Hyper-v 관리 도구**합니다. 클릭 **확인**합니다.  
  
#### <a name="to-reconfigure-the-service-to-start-automatically-using-the-services-desktop-app"></a>서비스 데스크톱 응용 프로그램을 사용 하 여 자동으로 시작 되도록 서비스를 다시 구성 하려면  
  
1.  서비스 데스크톱 응용 프로그램을 엽니다. (클릭 **시작**, 을 클릭 하 고 검색 상자에 입력 하기 시작 하면 **서비스**, 결과 목록에서 서비스를 차례로 클릭 하 고 있습니다.  
  
2.  세부 정보 창에서 마우스 오른쪽 단추로 클릭 **Hyper-v 가상 컴퓨터 관리**, 를 클릭 하 고 **속성**합니다.  
  
3.  에 **일반** 탭 **시작** 입력, 클릭 **자동**합니다.  
  
#### <a name="to-reconfigure-the-service-to-start-automatically-using-the-sc-config-command"></a>SC Config 명령을 통해 자동으로 시작 되도록 서비스를 다시 구성 하려면  
  
1.  Windows PowerShell을 엽니다.  
  
2.  형식:  
  
    ```  
    set-service  vmms -startuptype automatic  
    ```  
  
3.  서비스가 이미 실행 중이 아닌 경우 다음을 입력 합니다.  
  
    ```  
    start-service -name vmms  
    ```  
  


