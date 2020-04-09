---
title: 필요한 경우 디바이스 드라이버 업데이트 및 설치
description: MultiPoint 서비스에서 장치 드라이버를 확인 하 고 업데이트 하는 방법을 알아봅니다.
ms.date: 07/22/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.topic: article
ms.assetid: 16be3ef9-a05b-4621-a431-5806b567e997
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 6d20aa80edeafa4311262a380cfd7aad65ae0315
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80820606"
---
# <a name="update-and-install-device-drivers-if-needed"></a>필요한 경우 디바이스 드라이버 업데이트 및 설치
USB 제로 클라이언트 또는 드라이버가 필요한 주변 장치를 사용 하는 경우 지금 드라이버를 설치 해야 합니다. 드라이버 경고에 대 한 **Device Manager** 를 확인 하 고 해당 장치에 대 한 드라이버를 설치 하는 것도 좋습니다.  
  
일반적으로 최신 드라이버는 다음과 같은 종류의 장치에 필요 합니다.  
  
-   USB 제로 클라이언트  
  
-   USB 이더넷 0 클라이언트  
  
-   디스크 컨트롤러  
  
-   네트워크 어댑터  
  
-   사운드 컨트롤러  
  
-   USB 호스트 컨트롤러

-   그래픽 카드


## <a name="to-check-for-driver-alerts-in-device-manager"></a>Device Manager에서 드라이버 경고를 확인 하려면  
  
1.  시작 화면을 엽니다.  
  
2.  **컴퓨터 관리**를 입력 하 고 결과에서 **컴퓨터 관리** 를 클릭 합니다.  
  
3.  컴퓨터 관리 콘솔 트리에서 **Device Manager**를 클릭 합니다.  
  
4.  오른쪽의 시스템 장치에서 MultiPoint Server에 영향을 줄 수 있는 드라이버 경고를 확인 합니다.  
  
## <a name="to-install-device-drivers-in-multipoint-manager"></a>다중 포인트 관리자에서 장치 드라이버를 설치 하려면  
  
1.  다중 포인트 관리자를 열려면 "MultiPoint 관리자"를 검색 한 다음 결과에서 **Multipoint 관리자** 를 클릭 합니다.  
  
2.  다중 포인트 관리자에서 **홈** 탭을 클릭 한 다음 **콘솔 모드로 전환**을 클릭 합니다.  
  
3.  장치 드라이버를 설치 하려면 드라이버 파일을 두 번 클릭 하 고 지침에 따라 드라이버를 설치 합니다.  
  
4.  위의 단계를 반복 하 여 필요한 모든 드라이버를 설치 합니다.  
  
    > [!NOTE]  
    > 설치를 위해 컴퓨터를 다시 시작 해야 하는 경우 다음 드라이버를 설치 하기 전에 콘솔 모드로 다시 전환 해야 합니다. MultiPoint server는 항상 스테이션 모드에서 시작 됩니다. 콘솔 모드로 전환 하려면 MultiPoint 관리자의 **홈** 탭으로 이동 하 고 **콘솔 모드로 전환**을 클릭 합니다.