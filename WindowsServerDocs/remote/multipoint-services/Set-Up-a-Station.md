---
title: 스테이션 설치
description: MultiPoint 서비스에서 스테이션을 설정 하는 방법을 알아봅니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dce05b6c-795e-43b2-9920-026550b873c5
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: 043b0d8dba844f40569a854a4f4f2a2efb38a870
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70871615"
---
# <a name="set-up-a-station"></a>스테이션 설치
일반적으로 MultiPoint 서비스 *스테이션*은 *스테이션 허브*, 마우스, 키보드 및 비디오 모니터로 구성됩니다. 이 항목에서는 MultiPoint 서비스 스테이션을 만들기 위해 하드웨어 장치를 스테이션 허브에 연결하는 방법을 설명합니다.  
  
스테이션 허브는 MultiPoint 서비스 시스템의 컴퓨터에 주변 장치를 연결하는 하드웨어 장치입니다. MultiPoint 서비스는 다음과 같은 두 가지 유형의 스테이션 허브를 지원합니다.  
  
-   **USB 허브:** 범용 직렬 버스 2.0 이상 사양을 준수 하는 일반 다중 포트 USB 확장 허브입니다. 이러한 허브에는 일반적으로 여러 USB 장치를 컴퓨터의 단일 USB 포트에 연결할 수 있는 2개 또는 4개 이상의 USB 포트가 있습니다. USB 허브는 외부에서 전원이 공급 하거나 버스에서 지 원하는 수 있는 일반적으로 별도 장치입니다. MultiPoint 서비스에서 스테이션 허브로 사용할 경우에는 포트가 4개 이상 있는 허브를 사용하는 것이 좋습니다.  
  
    > [!IMPORTANT]  
    > 키보드와 마우스 이외의 다른 USB 장치를 허브에 연결하려는 경우 성능을 최적화하려면 외부에서 전원이 공급되는 허브를 사용하는 것이 좋습니다.  
  
-   **다기능 허브:** USB 포트를 통해 컴퓨터에 연결 하 고, 비디오 모니터를 비롯 한 다양 한 비 USB 장치를 허브에 연결할 수 있게 하는 확장 허브입니다. 다기능 허브 특정 하드웨어 제조업체에서 생성 되 고 장치별 드라이버를 설치 해야 할 수 있습니다.  
  
MultiPoint 서비스 시스템에 스테이션을 추가하려면 먼저 사용하려는 스테이션 하드웨어에 사용할 연결 포트가 충분한지 확인해야 합니다. 적절 한 수의 보안을 유지 해야는 또한 *클라이언트 액세스 라이선스 (Cal)* MultiPoint 서비스 시스템입니다.  
  
## <a name="setting-up-station-hardware"></a>스테이션 하드웨어 설치  
이 섹션의 절차에서는 MultiPoint 서비스 스테이션 하드웨어를 다양한 유형의 스테이션 허브에 연결하는 방법에 대해 설명합니다.  
  
### <a name="to-set-up-a-station-with-a-usb-hub"></a>USB 허브를 사용하여 스테이션을 설치하려면  
  
1.  새 스테이션을 연결하려면 먼저 모든 사용자 *세션*을 *종료*한 후 MultiPoint 서비스 시스템에서 전원이 공급된 기타 장치 및 컴퓨터를 종료합니다.  
  
2.  다음 그림과 같이 컴퓨터의 비디오 디스플레이 포트에 새 비디오 모니터 케이블을 연결합니다.  
  
    ![USB 허브 기반 시스템에 대한 동영상 연결 이미지](./media/WMSVideoConnection.gif)  
  
3.  다음과 같이 컴퓨터의 열려 있는 USB 포트에 새 USB 허브를 연결합니다.  
  
    ![MultiPoint Server USB 허브 연결 이미지](./media/WMSUSBHubConnection.gif)  
  
4.  다음과 같이 키보드 및 마우스를 USB 허브에 연결합니다.  
  
    ![USB 허브 입력 장치 연결 이미지](./media/WMSUSBDeviceConnection.gif)  
  
5.  비디오 모니터의 전원 코드를 전원 콘센트에 연결합니다.  
  
6.  컴퓨터를 켭니다.  
  
7.  MultiPoint 서비스가 시작됩니다. 새 스테이션의 비디오 모니터에 표시 되는 지침에 따라 장치를 새 스테이션에 연결 합니다.  
  
### <a name="to-set-up-a-station-with-a-multifunction-hub"></a>다기능 허브를 사용하여 스테이션을 설치하려면  
  
1.  새 스테이션을 연결하려면 먼저 모든 사용자 세션을 종료한 후 MultiPoint 서비스 시스템에서 전원이 공급된 기타 장치 및 컴퓨터를 종료합니다.  
  
2.  다음 그림과 같이 다기능 허브의 DVI 또는 VGA 비디오 디스플레이 포트에 새 비디오 모니터 케이블을 연결합니다.  
  
    ![다기능 허브 및 동영상 연결 이미지](./media/WMSMultifunctionHubVideoConnection.gif)  
  
3.  다음과 같이 컴퓨터의 열려 있는 USB 포트에 새 다기능 허브를 연결합니다.  
  
    ![다기능 허브 연결 이미지](./media/WMSMultifunctionHubConnection.gif)  
  
4.  다음과 같이 다기능 허브의 PS2 또는 USB 커넥터에 키보드 및 마우스를 연결합니다.  
  
    ![다기능 허브 및 PS2 커넥터 이미지](./media/WMSMultifunctionHubPS2Connection.gif)  
  
5.  비디오 모니터의 전원 코드를 전원 콘센트에 연결합니다.  
  
6.  컴퓨터를 켭니다.  
  
7.  MultiPoint 서비스가 시작됩니다. 메시지가 표시 되 면 새 스테이션의 비디오 모니터에 표시 되는 지침에 따라 장치를 새 스테이션에 *연결* 합니다.  
  
## <a name="see-also"></a>관련 항목  
[사용자 세션 종료](End-a-User-Session.md)  
[다시 시작 또는 종료](Restart-or-Shut-Down.md)  
[스테이션 하드웨어 관리](Manage-Station-Hardware.md)  
[USB 디바이스 작업](Work-with-USB-Devices.md)