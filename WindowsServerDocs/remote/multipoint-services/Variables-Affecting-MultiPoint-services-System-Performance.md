---
title: MultiPoint 서비스 시스템 성능에 영향을 주는 변수
description: MultiPoint 서비스에 대 한 성능 정보
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0f3e8875-1b5e-4789-b16c-d06d6e31f38e
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: cba973e3b0a89c26f886a67154c27831adb2c8cc
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71394833"
---
# <a name="variables-affecting-multipoint-services-system-performance"></a>MultiPoint 서비스 시스템 성능에 영향을 주는 변수
많은 변수가 MultiPoint 서비스 시스템의 전반적인 성능에 영향을 줄 수 있습니다. 이러한 시스템을 설계할 때 고려해 야 할 수 있습니다.  
  
## <a name="usage"></a>사용법  
  
-   **응용 프로그램** 특히 그래픽 같은 시간에 실행 중인 응용 프로그램의 수와 유형\-중형 또는 메모리 사용량이 많은 응용 프로그램에는 시스템의 전반적인 성능 영향을 줍니다. 자세한 내용은 참조 [응용 프로그램 및 인터넷 콘텐츠](hardware-and-performance-recommendations.md#applications-and-internet-content)합니다.  
  
-   **인터넷 사용** 멀티미디어 콘텐츠 또는 완전 한 동영상 비디오를 사용 하는 웹 페이지 사용자가 볼 경우 고려해 야 합니다. 이 유형의 콘텐츠 너무 많은 사용자가 동시에 보고 하는 경우 시스템을 오버 로드할 수 있습니다.  
  
    > [!NOTE]  
    > 전체 화면 비디오를 프로젝션 하는 교사 학생 모니터의 화면에 투사 하에 있도록 MultiPoint 서비스에서 프로젝션 기능 설계 되지 않았습니다. 프로젝션 기능 같은 프로시저를 보여 주는 데모를 위해 설계 되었습니다.  
  
-   **고속 장치** 미치면 시스템의 전반적인 성능이 너무 많은 사용자가 동시에 웹 카메라 또는 DVD 플레이어와 같은 고속 장치를 사용 하는 경우.  
  
## <a name="configuration"></a>Configuration  
  
-   **CPU, GPU, 및 RAM** 참조 [MultiPoint 서비스 시스템 성능 최적화](hardware-and-performance-recommendations.md#optimize-multipoint-services-system-performance) CPU, GPU, 및 RAM 권장 사항에 대 한이 가이드에 있습니다.  
-   **네트워크 대역폭** RDP over LAN에 연결 된 스테이션의 경우 특히 사용자의 세션에서 비디오가 실행 되는 경우 네트워크 대역폭과 클라이언트의 기능 (예: 씬 클라이언트, 데스크톱 PC 또는 랩톱)이 중요 합니다. USB 이더넷 0 클라이언트를 사용 하는 경우 네트워크 대역폭도 고려해 야 합니다. 이러한 장치를 사용 하는 경우 별도 기가 비트 이더넷 네트워크 설정을 고려해 야 할 수 있도록 모든 장치에 대 한 비디오 데이터 같은 이더넷 연결을 통해 전송 됩니다.  
-   **RemoteFX** RDP-조치-LAN 연결 된 스테이션 수 있습니다 RemoteFX 고화질 멀티미디어 콘텐츠를 배달을 향상 시키기 위해 사용할 수 있습니다.  
-   **디스플레이 해상도** 전체 화면 비디오 사용량이 수 하려는 경우 성능을 최대화 하기 위해 모니터 해상도 줄이는 것이 좋습니다.  
-   **USB 제로 클라이언트 수가** USB 제로 클라이언트 서버에 단일 루트 허브에서의 총 비디오 성능이 저하 직접 될 수 있습니다. 자세한 내용은 참조 [USB 0 클라이언트 연결 스테이션에 대 한 레이아웃](MultiPoint-services-Site-Planning.md#layout-for-usb-zero-client-connected-stations)합니다. 지원 되는 USB 이더넷 0 클라이언트 스테이션 수가 USB 제로 클라이언트 수가 보다 약간 작을 수 있습니다.  
-   **USB 대역폭** 시스템을 디자인할 때 USB 대역폭을 고려 하십시오.  이 USB 연결을 통해 비디오 데이터를 보내는 USB 제로 클라이언트의 경우 특히 중요 합니다. 대역폭을 최적화 하려면 서버에 단일 USB 포트에 연결 된 장치 수를 최소화 합니다. 데이지 체인 스테이션 및 중간 허브가 적용 됩니다. 자세한 내용은 참조 [허브 워크스테이션](MultiPoint-services-Site-Planning.md#station-hubs) 및 [허브에 대 한 약간](MultiPoint-services-Site-Planning.md#intermediate-hubs)합니다.  
  
-   **USB 종류** Usb 2.0 대신 USB 3.0을 사용 하면 세 개 이상의 USB 제로 클라이언트를 허브에 연결 하거나 고대역폭 USB 장치를 사용 하는 경우 서버와 중간 허브 간에 사용 가능한 대역폭이 증가 합니다.  
  
-   **스테이션** 스테이션의 총 수는 성능에 영향을 줍니다. 고급 그래픽, 처리 또는 비디오 요구 하는 경우에 스테이션의 전체 수를 제한 하는 것이 좋습니다. 자세한 내용은 참조 [최적화 MultiPoint 서비스 시스템 성능](hardware-and-performance-recommendations.md#optimize-multipoint-services-system-performance)합니다.