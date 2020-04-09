---
title: 실제 컴퓨터 및 기본 스테이션 설정
description: MultiPoint 서비스에서 첫 번째 시스템, 기본 스테이션을 설정 하는 방법에 대해 알아봅니다.
ms.date: 07/22/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.topic: article
ms.assetid: 4e83b126-ce9a-4cd7-a0bd-6627c9e0f81b
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 0f52d3fa4aeca8fd4e036a93ee5a175bf1e96d0b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855626"
---
# <a name="set-up-the-physical-computer-and-primary-station"></a>실제 컴퓨터 및 기본 스테이션 설정
MultiPoint 서비스를 설치 하기 전에 MultiPoint 서비스 시스템에 대 한 기본 스테이션을 설정 해야 합니다. LAN (local area network)을 사용 하는 경우 컴퓨터를 LAN에 연결 합니다.  
  
*스테이션* 은 MultiPoint 서비스에 액세스 하는 끝점입니다. *기본 스테이션* 은 MultiPoint 서비스가 시작 될 때 시작할 첫 번째 스테이션입니다. 관리자는이를 사용 하 여 시작 메뉴와 설정에 액세스할 수 있습니다. 기본 스테이션은 시스템 구성에 대 한 액세스를 제공 하 고, 시스템 구성 및 MultiPoint 서비스 시스템이 실행 되기 전에만 사용할 수 있는 문제 해결 정보를 제공 합니다. 시작한 후에는 다른 스테이션 에서처럼 기본 스테이션을 사용할 수 있습니다.  
  
기본 스테이션 스테이션 직접 비디오를 연결 해야 합니다. 다음 절차에서는 필요한 하드웨어를 MultiPoint 서비스 컴퓨터에 연결 하는 방법을 설명 합니다.  
  
스테이션에 대 한 자세한 내용은 참조 [MultiPoint 스테이션](multipoint-services-stations.md)합니다. 하드웨어를 선택 하는 데 도움이 필요한 경우 [MultiPoint 서비스 시스템에 대 한 하드웨어 선택](Selecting-Hardware-for-Your-MultiPoint-services-System.md)을 참조 하세요. 다른 스테이션 유형을 MultiPoint 서비스에 연결 하는 방법에 대 한 자세한 내용은 [Multipoint 서비스 컴퓨터에 추가 스테이션 연결](Attach-additional-stations-to-your-MultiPoint-services-computer.md)을 참조 하세요.  
  
> [!NOTE]  
> 비디오에 연결 된 스테이션을 만들려면 라틴어 키보드 (예: 영어 또는 스페인어 언어 키보드)를 사용 해야 합니다.  
  
## <a name="to-set-up-your-primary-station"></a>기본 스테이션을 설정 하려면  
  
1.  MultiPoint 서비스를 실행 하는 컴퓨터가 꺼져 있고 분리 되었는지 확인 합니다.  
  
2.  모니터의 전원 코드를 전원 콘센트에 연결 하 고 아래와 같이 컴퓨터의 비디오 디스플레이 포트에 모니터 케이블을 연결 합니다.  
  
    ![USB 허브 기반 시스템에 대한 동영상 연결 이미지](./media/WMSVideoConnection.gif)  
  
3.  스테이션에서 USB 키보드 및 마우스를 사용 하는 경우 다음 단계를 완료 합니다.  
  
    1.  아래와 같이 컴퓨터의 열려 있는 USB 포트에 외부 USB 허브를 연결 합니다.  
  
        ![MultiPoint 서비스 USB 허브 연결 이미지](./media/WMSUSBHubConnection.gif)  
  
    2.  Usb 키보드 및 마우스를 USB 허브에 연결 합니다.  
  
        ![USB 허브 입력 디바이스 연결 이미지](./media/WMSUSBDeviceConnection.gif)  
  
        > [!NOTE]  
        > MultiPoint 서비스 컴퓨터에 PS/2 포트가 있는 경우 필요한 경우 PS/2 키보드와 마우스를 컴퓨터에 직접 연결 하 여 사용할 수 있습니다. 그러나이 설정에는 상당한 제한 사항이 있습니다. 사용자는 PS/2 스테이션에서 오디오 장치, 웹 카메라 및 플래시 드라이브를 사용할 수 없습니다.  
  
    3.  외부에서 전원이 공급 되는 허브를 사용 하는 경우 전원 콘센트에 허브의 전원 케이블을 연결 합니다.  
  
        > [!IMPORTANT]  
        > 전원이 켜진된 허브의 사용을 권장합니다. 언더 현재 상태에서 시스템 동작 오류가 발생할 수 있습니다.  
        >   
        > 사용자가 마우스 및 키보드는 컴퓨터의 USB 포트에 직접 하지 연결 해야 합니다. 이 방법은 여러 키보드 및 마우스를 동일한 스테이션 또는 스테이션이 없습니다의 잘못 된 연결을 전혀 발생할 가능성이 있습니다.  
  
        > [!NOTE]  
        > 시스템 마더보드의 호스트 오디오 장치는 MultiPoint 서비스가 콘솔 모드에 있는 동안에만 사용할 수 있습니다. 외부 USB 허브를 사용 하는 스테이션에서 중단 없는 오디오를 확인 하려면 허브에 연결 된 USB 오디오 장치를 사용 해야 합니다.  
  
## <a name="to-connect-the-computer-to-the-lan"></a>컴퓨터를 LAN에 연결 하려면  
  
-   LAN을 사용 하는 경우 네트워크 케이블을 사용 하 여 컴퓨터를 네트워크에 연결 합니다.