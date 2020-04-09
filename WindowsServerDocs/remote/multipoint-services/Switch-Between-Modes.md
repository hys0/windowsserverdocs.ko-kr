---
title: 모드 간 전환
description: MultiPoint 서비스에서 스테이션 모드와 콘솔 모드 간을 전환 하는 방법에 대해 알아봅니다.
ms.prod: windows-server
ms.technology: multipoint-services
ms.topic: article
ms.assetid: 5f1b2324-c1b0-4b61-ab51-39af15e7792a
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: 80b56fcf5aca3530e41fba0125341031bb8112a7
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855576"
---
# <a name="switch-between-modes"></a>모드 간 전환
다중 포인트 관리자를 다양 한 유형의 MultiPoint 서비스 시스템 관리를 수행할 수 있도록 다음과 같은 모드 포함 됩니다.  
  
-   *스테이션 모드*: 기본적으로 MultiPoint 서비스 시스템은 스테이션 모드로 시작합니다. 스테이션 모드에서는 MultiPoint 서비스 스테이션이 각각 Windows를 실행 중인 별도의 컴퓨터인 것처럼 작동하고 여러 사용자가 시스템을 동시에 사용할 수 있습니다. 관리자와 사용자가 파일을 공유할 수 있고 관리자가 수행해야 하는 작업을 사용자가 수행할 수 있습니다.  
  
-   *콘솔 모드*: MultiPoint 서비스 시스템이 콘솔 모드인 경우 소프트웨어와 드라이버를 설치 및 업데이트하거나 다른 유지 관리 작업을 수행할 수 있습니다. 시스템이 콘솔 모드이면 다른 컴퓨터 사용자가 *스테이션*을 사용할 수 없습니다. 이러한 스테이션 다중 포인트 관리자에 표시 되지 않습니다. 서버에 직접 연결 하는 모든 모니터는이 컴퓨터 시스템의 표시로 처리 됩니다.   
  
> [!NOTE]
> 서버의 설정에서 기본값을 변경하여 시스템이 콘솔 모드에서 시작하도록 강제할 수 있습니다.  
> ## <a name="to-switch-from-station-mode-to-console-mode"></a>스테이션 모드에서 콘솔 모드로 전환하려면  
  
1.  스테이션 모드의 다중 포인트 관리자를 열고 클릭는 **홈** 탭 합니다.  
  
2.  **컴퓨터** 열에서 모드를 변경할 컴퓨터를 클릭합니다.  
  
3.  *컴퓨터 이름* **작업**에서 **콘솔 모드로 전환**을 클릭 합니다. 컴퓨터가 다시 시작되고 고 모든 스테이션이 사용할 수 없게 됩니다.  
  
## <a name="to-switch-from-console-mode-to-station-mode"></a>콘솔 모드에서 스테이션 모드를 전환하려면  
  
1.  콘솔 모드의 다중 포인트 관리자를 열고 클릭는 **홈** 탭 합니다.  
  
2.  **컴퓨터** 열에서 모드를 변경할 컴퓨터를 클릭합니다.  
  
3.  *컴퓨터 이름* **작업**에서 **스테이션 모드로 전환**을 클릭 합니다. 컴퓨터가 다시 시작되고 모든 스테이션이 사용할 수 있게 됩니다.  
  
## <a name="see-also"></a>참고 항목  
[MultiPoint 관리자를 사용하여 시스템 작업 관리](Manage-System-Tasks-Using-MultiPoint-Manager.md)