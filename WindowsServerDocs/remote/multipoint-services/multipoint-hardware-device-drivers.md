---
title: 설치에 필요한 하드웨어 및 장치 드라이버 수집
description: MultiPoint 서비스에 대해 설치 해야 하는 드라이버에 대 한 정보
ms.custom: na
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4cf5fdbe-b871-4360-b003-d65ac43b491e
author: evaseydl
manager: scottman
ms.author: evas
ms.date: 08/04/2016
ms.openlocfilehash: f7fec373bc62c93fbf31bbb24bf1a11a42c0736d
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70871430"
---
# <a name="collect-hardware-and-device-drivers-needed-for-the-installation"></a>설치에 필요한 하드웨어 및 장치 드라이버 수집
MultiPoint 서비스 시스템 배포를 시작 하기 전에 다음이 필요 합니다.  
  
-   **서버에 대 한 하드웨어 구성 요소** -이 시점에서 추가 비디오 카드나 기타 시스템 구성 요소를 설치 합니다.  
  
-   **스테이션의 하드웨어 구성 요소** -사용자 환경에 맞게 스테이션을 계획 하는 방법에 대 한 자세한 내용은 [MultiPoint 서비스 시스템에 대 한 하드웨어 선택](Selecting-Hardware-for-Your-MultiPoint-services-System.md)을 참조 하세요.
-   **비디오 카드용 최신 드라이버** -OEM 또는 장치 제조업체에서 이러한 드라이버를 제공 하지 않은 경우 장치 제조업체의 웹 사이트에서 다운로드 해야 합니다.  
  
-   **최신 usb 제로 클라이언트 드라이버** -usb 제로 클라이언트 스테이션을 사용 하는 경우 최신 usb 제로 클라이언트 드라이버를 설치 해야 합니다.  
  
    > [!IMPORTANT]  
    > MultiPoint 서비스를 설치 하려면 드라이버의 64 비트 버전을 설치 해야 합니다.  
  
> [!TIP]  
> 다른 버전의 Windows가 이미 설치 된 컴퓨터에 MultiPoint 서비스를 설치 하는 경우 Windows Server 설치를 시작 하기 전에 Device Manager에서 비디오 카드 제조업체 및 모델을 확인 하 고 Windows Server 2016에서 사용할 수 있습니다. Device Manager을 열고 **시작** 화면에서 **컴퓨터 관리** 를 엽니다. 그런 다음 콘솔 트리에서 **Device Manager**를 클릭 합니다.