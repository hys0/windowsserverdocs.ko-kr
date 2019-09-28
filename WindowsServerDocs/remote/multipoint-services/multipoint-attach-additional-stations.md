---
title: 추가 스테이션 MultiPoint 서버에 연결
description: MultiPoint 서비스 배포에 더 많은 스테이션 추가
ms.custom: na
ms.prod: windows-server
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d78ebf4e-0968-4014-9a42-9f75cc50cb52
author: evaseydl
manager: scottman
ms.author: evas
ms.date: 08/04/2016
ms.openlocfilehash: 45340f02b120b1431b1f58a58ed03ea40e17a14c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71394751"
---
# <a name="attach-additional-stations-to-multipoint-services"></a>추가 스테이션을 MultiPoint 서비스에 연결 합니다.
MultiPoint 서비스 환경에서 사용자가 스테이션을 사용 하 여 MultiPoint 서비스에 연결 하 여 해당 작업을 수행 합니다. 참여 하는 스테이션은 Multipoint Service를 실행 하는 컴퓨터에 연결 하기 위한 사용자 끝점입니다.  
  
MultiPoint 서비스는 세 가지 유형의 스테이션을 지원 합니다.  
  
-   직접 비디오 연결 스테이션  
  
-   클라이언트 연결 스테이션 (및 0 이더넷 클라이언트 연결 스테이션을 통해 USB) USB 0  
  
-   RDP-over LAN으로 연결 된 스테이션  
  
분류는 스테이션의 하드웨어와 사용 하는 연결 유형을 기반으로 합니다. 혼합할 수 있으며 프로그램 스테이션에 대 한 연결 형식과 일치 하는 수 있습니다. 하기만 하면 됩니다 (이전에 설치한)는 기본 스테이션 직접 비디오 연결 스테이션을 이어야 합니다. 스테이션 설정에 대 한 자세한 내용은 참조 [MultiPoint 스테이션](MultiPoint-services-Stations.md)합니다.  
  
각 유형의 스테이션을 설정 하는 방법을 설명 하는 내용은 다음을 참조 합니다.  
  
-   [직접 비디오 연결 스테이션 설정](Set-up-a-direct-video-connected-station-in-MultiPoint-services.md)  
  
-   [USB 제로 클라이언트 연결 스테이션 설정](Set-up-a-USB-zero-client-connected-station-in-MultiPoint-services.md)  
  
-   [RDP-over-LAN 연결 스테이션 설정](Set-up-an-RDP-over-LAN-connected-station-in-MultiPoint-services.md)  
  
스테이션 형식의 자세한 비교 내용은 참조 하십시오. [스테이션 형식 비교](multipoint-services-stations.md#BKMK_StationTypeComparison)합니다.  
  
> [!NOTE]  
> -   스테이션에 연결 하는 절차에는 중간 허브 또는 다운스트림 허브를 설정 하는 방법을 설명 하지 않습니다. 이러한 허브를 설치 하는 위치에 대 한 정보를 참조 하십시오. [MultiPoint 스테이션](MultiPoint-services-Stations.md)합니다.  
> -   경우에 따라 가상 컴퓨터에서 실행 되는 가상 데스크톱 스테이션 만들기 할 수 있습니다. 예를 들어 Windows 서버에 설치할 수 없는 응용 프로그램 또는 동일한 호스트 컴퓨터에 여러 인스턴스를 실행 하지 않는 응용 프로그램을 사용할 수 있습니다. 자세한 내용은 참조 [스테이션에 대 한 가상 데스크톱 Windows 10 Enterprise 만들](Create-Windows-10-Enterprise-virtual-desktops-for-stations.md)합니다.  
  
> [!TIP]  
> MultiPoint Server에서 순차적으로 식별 된 있도록 해당 실제 위치가 순서 대로 프로그램 스테이션을 만들 수는 것이 유용 합니다. 나중에 스테이션의 이름을 변경 하려면 다중 포인트 관리자를 수행할 수 있습니다. 자세한 내용은 MultiPoint Server 도움말 및 지원에서 스테이션 모두 다시 매핑을 참조 하십시오.