---
title: 필요한 경우 장치 드라이버 업데이트 및 설치
description: 확인 하 고 MultiPoint 서비스에서 장치 드라이버를 업데이트 하는 방법을 알아봅니다
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 16be3ef9-a05b-4621-a431-5806b567e997
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 66477634e06df217656876b084ae37be8cb311c0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829134"
---
# <a name="update-and-install-device-drivers-if-needed"></a>필요한 경우 장치 드라이버 업데이트 및 설치
USB 제로 클라이언트 또는 드라이버를 필요로 하는 주변 장치를 사용 하는 경우에이 이번에 드라이버를 설치 해야 합니다. 확인 하는 것이 좋습니다 **장치 관리자** 드라이버 경고 및 해당 장치에 대 한 드라이버를 설치 합니다.  
  
일반적으로 최신 드라이버는 다음 장치 유형에 대 한 필요 합니다.  
  
-   USB 제로 클라이언트  
  
-   USB 이더넷 0 클라이언트  
  
-   디스크 컨트롤러  
  
-   네트워크 어댑터  
  
-   사운드 컨트롤러  
  
-   USB 호스트 컨트롤러

-   그래픽 카드


## <a name="to-check-for-driver-alerts-in-device-manager"></a>장치 관리자에서 드라이버 경고에 대 한 확인 하려면  
  
1.  시작 화면을 엽니다.  
  
2.  형식 **컴퓨터 관리**를 클릭 하 고 **컴퓨터 관리** 결과에서입니다.  
  
3.  컴퓨터 관리 콘솔 트리에서 **장치 관리자**합니다.  
  
4.  오른쪽의 시스템 장치 드라이버 경고 MultiPoint 서버에 영향을 줄 수를 확인 합니다.  
  
## <a name="to-install-device-drivers-in-multipoint-manager"></a>다중 포인트 관리자에서 장치 드라이버를 설치 하려면  
  
1.  다중 포인트 관리자를 열려면 "다중 포인트 관리자에서" 검색 하 고 클릭 **다중 포인트 관리자** 결과에서입니다.  
  
2.  다중 포인트 관리자에서 클릭 합니다 **홈** 탭을 클릭 한 다음 **콘솔 모드로 전환**합니다.  
  
3.  장치 드라이버를 설치 하려면 드라이버 파일을 두 번 클릭 하 고 드라이버를 설치 하려면 지침을 따릅니다.  
  
4.  모든 필수 드라이버를 설치 하려면 이전 단계를 반복 합니다.  
  
    > [!NOTE]  
    > 설치 된 컴퓨터를 다시 시작에 필요한 경우에 다음 드라이버를 설치 하기 전에 콘솔 모드로 다시 전환 해야 합니다. 항상 multiPoint server 스테이션 모드로 시작합니다. 콘솔 모드로 전환 하려면로 이동 합니다 **홈** 다중 포인트 관리자에서 탭을 클릭 **콘솔 모드로 전환**합니다.