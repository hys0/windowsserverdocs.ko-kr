---
title: 스테이션 하드웨어 관리
description: MultiPoint 스테이션의 하드웨어를 관리 하는 방법에 대 한 개요를 제공 합니다.
ms.prod: windows-server
ms.technology: multipoint-services
ms.topic: article
ms.assetid: 429b8539-b17a-4e01-9576-860600466451
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: 8ffb6fd714293471a0e9aa020390943b201261c4
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80853526"
---
# <a name="manage-station-hardware"></a>스테이션 하드웨어 관리
MultiPoint 서비스 시스템은 한 대의 컴퓨터와 하나 이상의 스테이션으로 구성되어 있습니다. 일반적으로 스테이션 하드웨어는 스테이션 허브, 마우스, 키보드 및 비디오 모니터로 구성됩니다. 일반적으로 스테이션은 컴퓨터에 물리적으로 연결됩니다.  
  
다음 그림은 4개의 스테이션이 있는 MultiPoint 서비스 시스템의 레이아웃 예를 보여 줍니다. 각 장치는 멀티 모니터 비디오 카드 및 USB 허브를 사용 하 여 MultiPoint 서비스 컴퓨터에 연결 됩니다. 이 그림에 다기능 허브를 사용하여 연결된 스테이션은 없습니다.  
   
![MultiPoint 서비스 USB 기반 시스템 레이아웃 이미지](./media/WMSMultiPointServerUSBSystemLayout.gif)  
  
이 섹션의 항목에서는 MultiPoint 서비스 시스템에 연결된 하드웨어의 상태를 확인할 수 있는 방법을 설명하고 MultiPoint 서비스 스테이션을 설치하는 데 사용할 수 있는 USB 디바이스 유형 및 기타 주변 하드웨어 디바이스에 대한 자세한 정보를 제공합니다. 다음은 하드웨어를 선택하고 MultiPoint 서비스 스테이션을 설치하는 데 유용한 이 섹션의 항목에 대한 간략한 설명입니다.  
  
## <a name="view-hardware-status"></a>하드웨어 상태 보기  
다중 포인트 관리자에서 사용할 수는 **스테이션** 스테이션과 MultiPoint 서비스 컴퓨터에 연결 되는 하드웨어 장치 상태를 보려면 탭 합니다. MultiPoint 서비스 컴퓨터와 이 컴퓨터에 연결된 하드웨어 장치의 상태를 확인하는 방법에 대한 자세한 내용은 [하드웨어 상태 보기](View-Hardware-Status.md) 항목을 참조하세요.  
  
## <a name="work-with-usb-devices"></a>USB 장치 작업  
USB 디바이스 및 기타 주변 하드웨어 디바이스가 MultiPoint 서비스 시스템에 연결되어 있는 경우 이러한 디바이스는 MultiPoint 서비스 컴퓨터에 연결된 경우와 MultiPoint 서비스 스테이션에 연결된 경우에 서로 다르게 작동합니다. [USB 장치 작업](Work-with-USB-Devices.md) 항목에서는 다양한 하드웨어 장치가 이러한 시나리오에서 어떻게 작동하는지 설명하고 스테이션 허브에서 작업하는 방법에 대한 자세한 내용도 다룹니다.  
  
## <a name="work-with-video-devices"></a>비디오 장치 작업  
[비디오 디바이스 작업](Work-with-Video-Devices.md) 항목에서는 모니터, 프로젝터 등의 비디오 디바이스가 MultiPoint 서비스 시스템의 컴퓨터나 MultiPoint 서비스 스테이션에 연결된 경우 어떻게 작동하는지 논의합니다.  
  
## <a name="set-up-a-station"></a>스테이션 설치  
[스테이션 설치](Set-Up-a-Station.md) 항목에서는 MultiPoint 서비스 스테이션 허브에 주변 하드웨어 장치를 연결하여 MultiPoint 서비스 스테이션을 만드는 방법에 관해 설명합니다. MultiPoint 서비스는 다음과 같은 두 가지 유형의 스테이션 허브를 지원합니다.  
  
-   외부 저전력 또는 버스에서 지 원하는 다중 포트 *USB 허브* 마우스, 키보드 및 기타 USB 주변 장치를 지원할 수 있는  
  
-   통합 비디오 컨트롤러와 마우스, 키보드 및 오디오 주변 장치용 포트를 포함할 수 있는 *다기능 허브*  
  
두 가지 유형의 스테이션 허브는 모두 USB 케이블을 통해 컴퓨터에 연결됩니다. [스테이션 설치](Set-Up-a-Station.md) 항목의 절차에서는 각 스테이션 허브 유형에 하드웨어 장치를 연결하는 방법을 설명합니다.  
  
## <a name="see-also"></a>관련 항목  
[하드웨어 상태 보기](View-Hardware-Status.md)  
[USB 디바이스 작업](Work-with-USB-Devices.md)  
[비디오 디바이스 작업](Work-with-Video-Devices.md)  
[스테이션 설치](Set-Up-a-Station.md)