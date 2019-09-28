---
title: MultiPoint 서비스에서 직접 비디오 연결 스테이션을 설정 합니다.
description: MultiPoint 서비스에서 직접 비디오에 연결 된 스테이션을 만드는 방법에 대해 알아봅니다.
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 82ba3517-9743-4cde-8eea-63a17edb016f
author: lizap
manager: dongill
ms.author: elizapo
ms.openlocfilehash: ab57f3d996cfe9196fd256a76516a44dc146043b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71389357"
---
# <a name="set-up-a-direct-video-connected-station-in-multipoint-services"></a>MultiPoint 서비스에서 직접 비디오 연결 스테이션을 설정 합니다.
직접 비디오에 연결 된 스테이션 모니터가 MultiPoint 서버 컴퓨터에서 비디오 포트에 직접 연결 되어 있습니다. 키보드 및 마우스 USB 허브에 연결 되어 및 모니터와 연결 합니다.  
  
다음 그림에는 단일 MultiPoint Server 컴퓨터와 직접 비디오를 연결 하는 4 개의 스테이션 있는 MultiPoint Server 환경을 보여 줍니다. 자세한 내용은 참조 [MultiPoint Server 스테이션](MultiPoint-services-Stations.md)합니다.  
  
**직접 비디오 연결이 4 개인 MultiPoint 서비스 시스템**  
  
![MultiPoint 서비스 USB 기반 시스템 레이아웃 이미지](./media/WMSMultiPointServerUSBSystemLayout.gif)  
  
> [!NOTE]  
> 직접 비디오 연결 스테이션을 구성 하려면 (예:는 영어 또는 스페인어 언어 키보드) 라틴어 키보드를 사용 해야 합니다.  
  
## <a name="to-set-up-a-direct-video-connected-station"></a>직접 비디오에 연결 된 스테이션을 설정 하려면  
  
1.  아래와 같이 모니터 케이블 비디오 디스플레이 포트는 컴퓨터에 연결 합니다.  
  
    ![USB 허브 기반 시스템에 대한 동영상 연결 이미지](./media/WMSVideoConnection.gif) 
  
2.  비디오 모니터의 전원 코드를 전원 콘센트에 연결합니다.  
  
3.  아래와 같이 컴퓨터의 열려 있는 USB 포트에 USB 허브를 연결 합니다.  
  
    ![MultiPoint 서비스 USB 허브 연결 이미지](./media/WMSUSBHubConnection.gif)  
  
4.  키보드 및 마우스 USB 스테이션 허브에 연결 합니다.  
  
    ![USB 허브 입력 장치 연결 이미지](./media/WMSUSBDeviceConnection.gif)  
  
5.  헤드폰 등 추가 모든 주변 장치, USB 허브에 연결 합니다.  
  
6.  외부에서 전원이 공급 되는 허브를 사용 하는 경우 전원 콘센트에 허브의 전원 케이블을 연결 합니다.  
  
    > [!IMPORTANT]  
    > 전원이 켜진된 허브의 사용을 권장합니다. 언더 현재 상태에서 시스템 동작 오류가 발생할 수 있습니다.  
    >   
    > 사용자가 마우스 및 키보드는 컴퓨터의 USB 포트에 직접 하지 연결 해야 합니다. 이 방법은 여러 키보드 및 마우스를 동일한 스테이션 또는 스테이션이 없습니다의 잘못 된 연결을 전혀 발생할 가능성이 있습니다.  
  
7.  스테이션을 만들려는 모니터에 표시 되는 지침을 따릅니다.  
  
MultiPoint 서비스 환경에 둘 이상의 직접 비디오에 연결 된 스테이션을 추가 하는 경우 기본 스테이션 변경 될 수 있습니다. 직접 비디오 연결 된 스테이션에 기본 스테이션을 쉽게 찾을 수 있습니다.  
  
## <a name="to-find-out-which-direct-video-connected-station-is-the-primary-station"></a>기본 스테이션은 비디오에 연결 된 스테이션을 직접는 확인 하려면  
  
1.  컴퓨터의 디스플레이 어댑터 (비디오 카드)에 직접 연결 된 모든 모니터를 켭니다.  
  
2.  시작 (또는 다시 시작) MultiPoint 서비스 컴퓨터와 참조는 모니터 시작 화면을 표시 합니다. 해당 기본 스테이션이입니다.  
  
    > [!NOTE]  
    > 경우에 따라 BIOS 시작 정보가 표시 됩니다 여러 모니터에 동시에. 이 경우 모니터의 간주할 수 "기본 스테이션" BIOS에 액세스 하기 위해 있습니다.