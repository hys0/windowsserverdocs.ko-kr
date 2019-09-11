---
title: 하드웨어 요구 사항 및 성능 권장 사항
description: MultiPoint 서비스에 대 한 하드웨어 및 성능 요구 사항 및 권장 사항을 제공 합니다.
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 99a5c9c2-270f-4753-a28c-434882c03125
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: afabab738527e7a0994c917b0065baa4f8c53fda
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70871444"
---
# <a name="hardware-requirements-and-performance-recommendations"></a>하드웨어 요구 사항 및 성능 권장 사항
이 항목에서는 MultiPoint 서비스 시스템을 실행 하 고 사용자 응용 프로그램 시나리오를 지 원하는 데 필요한 하드웨어에 대해 설명 합니다. 사용자 시나리오는 CPU, RAM 및 네트워크 대역폭 요구 사항에 직접적인 영향을 줍니다.  

## <a name="optimize-multipoint-services-system-performance"></a>MultiPoint 서비스 시스템 성능 최적화  
MultiPoint 서비스 시스템의 성능은 CPU, GPU 및 MultiPoint 서비스를 실행 하는 컴퓨터에서 사용할 수 있는 RAM의 용량에 따라 직접적인 영향을 받습니다.  
  
### <a name="applications-and-internet-content"></a>응용 프로그램 및 인터넷 콘텐츠  
MultiPoint 서비스는 공유 리소스 컴퓨팅 솔루션 이므로 스테이션에서 실행 되는 응용 프로그램의 유형과 수는 MultiPoint 서비스 시스템의 성능에 영향을 줄 수 있습니다. 시스템을 계획할 때 정기적으로 사용 되는 프로그램의 유형을 고려해 야 합니다. 예를 들어 그래픽을 많이 사용 하는 응용 프로그램에는 워드 프로세서와 같은 응용 프로그램 보다 더 강력한 컴퓨터가 필요 합니다. 그래픽을 많이 사용 하는 응용 프로그램을 사용 하 여 컴퓨터를 오버 로드 하면 전체 시스템에서 지연 되는 문제가 발생할 수 있습니다.  
  
응용 프로그램에서 액세스 하는 콘텐츠 형식은 시스템의 성능에도 영향을 줍니다. 여러 스테이션이 웹 브라우저를 사용 하 여 전체 동작 비디오와 같은 멀티미디어 콘텐츠에 액세스 하는 경우 시스템 성능에 부정적인 영향을 주지 않으면 서 연결 될 수 있는 스테이션이 줄어듭니다. 반대로, 여러 스테이션에서 웹 브라우저를 사용 하 여 정적 웹 콘텐츠에 액세스 하는 경우 성능에 큰 영향을 주지 않으면 서 더 많은 스테이션이 연결 될 수 있습니다.  
  
### <a name="hardware-recommendations"></a>하드웨어 권장 사항  
다양 한 로드에서 MultiPoint 서비스 시스템을 사용 하 여 성능을 향상 시키려면 시스템을 계획 하 고 테스트할 때 다음 표에 설명 된 지침을 따르십시오. 다음은 forMultiPoint 서비스에 대 한 기본 요구 사항입니다. 실제 구성 크기 조정은 시스템 구성, 실행 중인 작업 및 하드웨어 기능에 따라 달라 집니다. 응용 프로그램 및 하드웨어를 테스트 하 여 항상 유효성을 검사 해야 합니다.  
  
> [!NOTE]  
> 2C = 2 개 코어, 4C = 4 코어, 6C = 6 코어, MT = 다중 스레딩 프로세서 속도는 2.0 GHz 이상 이어야 합니다.  
  
### <a name="minimum-recommended-hardware-for-running-default-multipoint-server-stations"></a>기본 MultiPoint Server 스테이션을 실행 하기 위한 최소 권장 하드웨어  
  
|응용 프로그램 시나리오|최대 5 개 스테이션|6-8 스테이션|9-12 스테이션|13-16 스테이션|17-20 스테이션|21-24 스테이션|  
|------------------------|----------------------|-------------------|------------------|-------------------|-------------------|-----------------|  
|**업무**<br /><br />Office, 웹 검색, lob (기간 업무) 응용 프로그램|CPU: 2C<br /><br />RAM: 2GB|CPU: 2C<br /><br />RAM: 4GB|CPU: 4C<br /><br />RAM: 6GB|CPU: 4C<br /><br />RAM: 8GB|CPU: 4C + MT 또는 6C<br /><br />RAM: 10GB| CPU: 6C + MT<br /><br />RAM: 12 GB|
|**모음집**<br /><br />Office, 웹 검색, 기간 업무 (lob) 응용 프로그램, 일부 사용자가 가끔씩 비디오 사용|CPU: 2C<br /><br />RAM: 2GB|CPU: 2C<br /><br />RAM: 4GB|CPU: 4C<br /><br />RAM: 6GB|CPU: 4C + MT 또는 6C<br /><br />RAM: 8GB|CPU: 6C + MT<br /><br />RAM: 10GB| CPU: 6C + MT<br /><br />RAM: 12 GB| 
|**비디오 집약적**<br /><br />Office, 웹 검색, lob (기간 업무) 응용 프로그램 및 모든 사용자가 자주 사용 하는 비디오 사용에 대 한 **정보:** 비디오 테스트는 네이티브 해상도에서 360p H. 264 비디오를 사용 하 여 수행 되었습니다.|CPU: 4C + MT<br /><br />RAM: 2GB|CPU: 6C + MT<br /><br />RAM: 4GB|CPU: 8C + MT<br /><br />RAM: 6GB|CPU: 12C + MT<br /><br />RAM: 8GB|CPU: 16C + MT<br /><br />RAM: 10GB<br /><br />-씬 클라이언트: RemoteFX<br />-USB 비디오 권장 안 됨| CPU: 20C + MT<br /><br />RAM: 12 GB<br /><br />-씬 클라이언트: RemoteFX<br />-USB 비디오 권장 안 됨|   
  
## <a name="minimum-recommended-hardware-for-running-full-windows-10-virtual-desktops"></a>전체 Windows 10 가상 데스크톱을 실행 하기 위한 최소 권장 하드웨어  
각 스테이션에 대해 전체 가상 운영 체제 인스턴스를 실행 하는 것은 기본 MultiPoint 데스크톱 세션을 실행 하는 것 보다 더 많은 계산 리소스를 사용 하므로, 스테이션 당 호스트 하드웨어 요구 사항이 더 높습니다.  
  
1.  CPU: 1 개 코어 또는 스테이션 당 스레드  
  
2.  솔리드 스테이트 드라이브 (SSD)  
  
    1.  용량 > = 20GB, WMS 호스트 운영 체제에 대 한 40GB  
  
    2.  임의 읽기/쓰기 IOPS > =/스테이션 당 3K  
  
3.  RAM > = 스테이션 당 2GB + WMS 호스트 운영 체제의 경우 2GB  
  
BIOS CPU 설정이 가상화-두 번째 수준 주소 변환 (SLAT)을 사용 하도록 구성 되었습니다.  
  
사용자 요구에 가장 적합 한 MultiPoint 서비스 하드웨어를 선택 하는 방법에 대 한 자세한 내용은 하드웨어 공급 업체에 문의 하세요.  