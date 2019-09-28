---
title: MultiPoint 서비스에서 클라이언트 연결 스테이션 0을 USB를 설정
description: MultiPoint 서비스에서 USB 제로 클라이언트 스테이션을 만드는 방법에 대해 알아봅니다.
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d2908865-6be3-474d-88f1-995f40bb61d0
author: lizap
manager: dongill
ms.author: elizapo
ms.openlocfilehash: 80a73065024e5c40f1ebf8efd64022ee6d48fbe8
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71395066"
---
# <a name="set-up-a-usb-zero-client-connected-station-in-multipoint-services"></a>MultiPoint 서비스에서 클라이언트 연결 스테이션 0을 USB를 설정
USB 제로 클라이언트를 사용 하 여 MultiPoint 서비스 스테이션을 만들 때 각 장치에 대 한 모니터는 다음 그림에 표시 된 것 처럼 비디오 포트에 USB 제로 클라이언트 연결 됩니다. 이 및 다른 스테이션 형식에 대 한 자세한 내용은 참조 [MultiPoint 스테이션](MultiPoint-services-Stations.md)합니다.
  
**직접 비디오에 연결 된 스테이션 하나와 두 개의 USB 제로 클라이언트 연결 스테이션을 사용 하는 MultiPoint 서비스 시스템**  
  
![USB 제로 클라이언트 연결 스테이션](./media/WMS11_diagram7.gif)  
  
> [!IMPORTANT]  
> 0 개 클라이언트에 연결 된 스테이션을 USB를 설정 하기 전에 비디오 카드 및 USB 제로 클라이언트에 대 한 최신 드라이버를 설치 해야 합니다. 오래 된 드라이버를 성공적으로 완료할 MultiPoint 서비스 구성을 방지할 수 있습니다. 자세한 내용은 [업데이트 필요한 경우에 장치 드라이버를 설치 하 고](Update-and-install-device-drivers-if-needed.md)합니다.  
  
> [!IMPORTANT]  
> USB 이더넷 0 클라이언트를 사용 하는 경우 공급 업체에서이 절차는 대신 네트워크의 장치를 설정 하는 이더넷 연결을 사용 하 여 지침을 따릅니다.  
  
### <a name="to-set-up-a-usb-zero-client-connected-station"></a>0 개 클라이언트에 연결 된 스테이션에 USB를 설정 하려면  
  
1.  비디오 모니터 케이블을 연결 합니다 DVI 또는 VGA 비디오 디스플레이 포트에 USB에 0 클라이언트는 다음 그림과에서 같이 표시 합니다.  
  
    ![USB 허브 기반 시스템에 대한 동영상 연결 이미지](./media/WMSVideoConnection.gif)  
  
2.  USB 제로 클라이언트 컴퓨터에서 열려 있는 USB 포트에 연결 합니다.  
  
    ![MultiPoint 서비스 USB 허브 연결 이미지](./media/WMSUSBHubConnection.gif)  
  
3.  USB 제로 클라이언트에는 키보드와 마우스를 연결 합니다.  
  
    ![USB 허브 입력 장치 연결 이미지](./media/WMSUSBDeviceConnection.gif)  
  
4.  외부에서 전원이 공급 되는 USB 제로 클라이언트를 사용 하는 경우 USB 제로 클라이언트의 전원 코드를 전원 콘센트에 연결 합니다.  
  
5.  비디오 모니터의 전원 코드를 전원 콘센트에 연결합니다.  
  
6.  스테이션와 장치를 연결 하 라는 메시지가 나타나면 설치를 완료 하려면 모니터에 지시를 따릅니다. (일반적으로 USB 0 클라이언트 연결 스테이션 연관 된 스테이션 자동으로 서버에 추가 하면 됩니다.)